<!-- markdownlint-disable MD002 MD041 -->

在此练习中，你将 Microsoft Graph 合并到应用程序中。 对于此应用程序，你将使用 [microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) 库调用 Microsoft Graph。

## <a name="get-calendar-events-from-outlook"></a>从 Outlook 获取日历事件

1. 添加新服务以保留所有 Graph 调用。 在 CLI 中运行以下命令。

    ```Shell
    ng generate service graph
    ```

    与之前创建的身份验证服务一样，通过为此创建服务，你可以将该服务注入需要访问 Microsoft Graph 的任何组件。

1. 命令完成后，打开 **./src/app/graph.service.ts，** 并将其内容替换为以下内容。

    ```typescript
    import { Injectable } from '@angular/core';
    import { Client } from '@microsoft/microsoft-graph-client';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';

    import { AuthService } from './auth.service';
    import { AlertsService } from './alerts.service';

    @Injectable({
      providedIn: 'root'
    })

    export class GraphService {

      private graphClient: Client;
      constructor(
        private authService: AuthService,
        private alertsService: AlertsService) {

        // Initialize the Graph client
        this.graphClient = Client.init({
          authProvider: async (done) => {
            // Get the token from the auth service
            const token = await this.authService.getAccessToken()
              .catch((reason) => {
                done(reason, null);
              });

            if (token)
            {
              done(null, token);
            } else {
              done("Could not get an access token", null);
            }
          }
        });
      }

      async getCalendarView(start: string, end: string, timeZone: string): Promise<MicrosoftGraph.Event[] | undefined> {
        try {
          // GET /me/calendarview?startDateTime=''&endDateTime=''
          // &$select=subject,organizer,start,end
          // &$orderby=start/dateTime
          // &$top=50
          const result =  await this.graphClient
            .api('/me/calendarview')
            .header('Prefer', `outlook.timezone="${timeZone}"`)
            .query({
              startDateTime: start,
              endDateTime: end
            })
            .select('subject,organizer,start,end')
            .orderby('start/dateTime')
            .top(50)
            .get();

          return result.value;
        } catch (error) {
          this.alertsService.addError('Could not get events', JSON.stringify(error, null, 2));
        }
        return undefined;
      }
    }
    ```

    考虑此代码将执行什么工作。

    - 它在服务的构造函数中初始化 Graph 客户端。
    - 它通过 `getCalendarView` 以下方式实现使用 Graph 客户端的函数：
      - 将调用的 URL 为 `/me/calendarview`。
      - `header`方法包括 标头，这将导致返回事件的开始时间和结束时间在 `Prefer: outlook.timezone` 用户的首选时区。
      - `query`方法添加 `startDateTime` 和 `endDateTime` 参数，定义日历视图的时间窗口。
      - `select`方法将每个事件返回的字段限定为视图将实际使用的字段。
      - `orderby`方法按开始时间对结果进行排序。

1. 创建 Angular 组件以调用此新方法并显示调用的结果。 在 CLI 中运行以下命令。

    ```Shell
    ng generate component calendar
    ```

1. 命令完成后，将组件添加到 `routes` **./src/app/app-routing.module.ts 中的数组**。

    ```typescript
    import { CalendarComponent } from './calendar/calendar.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
      { path: 'calendar', component: CalendarComponent },
    ];
    ```

1. 打开 **"tsconfig.js"，** 然后向 对象添加以下 `compilerOptions` 属性。

    ```json
    "resolveJsonModule": true
    ```

1. 打开 **./src/app/calendar/calendar.component.ts，** 并将其内容替换为以下内容。

    ```typescript
    import { Component, OnInit } from '@angular/core';
    import * as moment from 'moment-timezone';
    import { findIana } from 'windows-iana';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';

    import { AuthService } from '../auth.service';
    import { GraphService } from '../graph.service';
    import { AlertsService } from '../alerts.service';

    @Component({
      selector: 'app-calendar',
      templateUrl: './calendar.component.html',
      styleUrls: ['./calendar.component.css']
    })
    export class CalendarComponent implements OnInit {

      public events?: MicrosoftGraph.Event[];

      constructor(
        private authService: AuthService,
        private graphService: GraphService,
        private alertsService: AlertsService) { }

      ngOnInit() {
        // Convert the user's timezone to IANA format
        const ianaName = findIana(this.authService.user?.timeZone ?? 'UTC');
        const timeZone = ianaName![0].valueOf() || this.authService.user?.timeZone || 'UTC';

        // Get midnight on the start of the current week in the user's timezone,
        // but in UTC. For example, for Pacific Standard Time, the time value would be
        // 07:00:00Z
        var startOfWeek = moment.tz(timeZone).startOf('week').utc();
        var endOfWeek = moment(startOfWeek).add(7, 'day');

        this.graphService.getCalendarView(
          startOfWeek.format(),
          endOfWeek.format(),
          this.authService.user?.timeZone ?? 'UTC')
            .then((events) => {
              this.events = events;
              // Temporary to display raw results
              this.alertsService.addSuccess('Events from Graph', JSON.stringify(events, null, 2));
            });
      }
    }
    ```

现在，这只是在页面上以 JSON 呈现事件数组。 保存更改并重新启动该应用。 登录并单击导航 **栏中** 的"日历"链接。 如果一切正常，应在用户日历上看到事件被 JSON 卸载。

## <a name="display-the-results"></a>显示结果

现在，你可以 `CalendarComponent` 更新组件以更用户友好的方式显示事件。

1. 从 函数中删除添加警报的临时 `ngOnInit` 代码。 更新的函数应如下所示。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/calendar/calendar.component.ts" id="ngOnInitSnippet":::

1. 将函数添加到 `CalendarComponent` 类，将对象 `DateTimeTimeZone` 格式化为 ISO 字符串。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/calendar/calendar.component.ts" id="formatDateTimeTimeZoneSnippet":::

1. 打开 **"./src/app/calendar/calendar.component.html"，** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/calendar/calendar.component.html" id="calendarHtml":::

这将循环访问事件集合，并针对每个事件添加一个表行。 保存更改并重新启动应用。 单击" **日历"** 链接，应用现在应呈现一个事件表。

![事件表的屏幕截图](./images/add-msgraph-01.png)
