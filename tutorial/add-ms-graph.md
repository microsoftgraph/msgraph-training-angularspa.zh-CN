<!-- markdownlint-disable MD002 MD041 -->

在本练习中, 将把 Microsoft Graph 合并到应用程序中。 对于此应用程序, 您将使用[microsoft graph 客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)库调用 microsoft graph。

## <a name="get-calendar-events-from-outlook"></a>从 Outlook 获取日历事件

首先, 创建一个`Event`定义应用程序将显示的字段的类。 在`./src/app`目录中创建一个名`event.ts`为的新文件, 并添加以下代码。

```TypeScript
// For a full list of fields, see
// https://docs.microsoft.com/graph/api/resources/event?view=graph-rest-1.0
export class Event {
  subject: string;
  organizer: Recipient;
  start: DateTimeTimeZone;
  end: DateTimeTimeZone;
}

// https://docs.microsoft.com/graph/api/resources/recipient?view=graph-rest-1.0
export class Recipient {
  emailAddress: EmailAddress;
}

// https://docs.microsoft.com/graph/api/resources/emailaddress?view=graph-rest-1.0
export class EmailAddress {
  name: string;
  address: string;
}

// https://docs.microsoft.com/graph/api/resources/datetimetimezone?view=graph-rest-1.0
export class DateTimeTimeZone {
  dateTime: string;
  timeZone: string;
}
```

接下来, 添加新服务以保存所有图形调用。 就像之前创建的身份验证服务一样, 为此创建服务可让您将其插入到需要访问 Microsoft Graph 的任何组件中。 在 CLI 中运行以下命令。

```Shell
ng generate service graph
```

命令完成后, 打开`./src/app/graph.service.ts`文件并将其内容替换为以下内容。

```TypeScript
import { Injectable } from '@angular/core';
import { Client } from '@microsoft/microsoft-graph-client';

import { AuthService } from './auth.service';
import { Event } from './event';
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
        let token = await this.authService.getAccessToken()
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

  async getEvents(): Promise<Event[]> {
    try {
      let result =  await this.graphClient
        .api('/me/events')
        .select('subject,organizer,start,end')
        .orderby('createdDateTime DESC')
        .get();

      return result.value;
    } catch (error) {
      this.alertsService.add('Could not get events', JSON.stringify(error, null, 2));
    }
  }
}
```

考虑此代码执行的操作。

- 它在服务的构造函数中初始化 Graph 客户端。
- 它实现了`getEvents`通过以下方式使用 Graph 客户端的函数:
  - 将调用的 URL 为`/me/events`。
  - 此`select`方法将为每个事件返回的字段限制为只是视图实际使用的字段。
  - `orderby`方法按其创建日期和时间对结果进行排序, 最新项目最先开始。

现在, 创建一个角度组件来调用此新方法, 并显示该调用的结果。 在 CLI 中运行以下命令。

```Shell
ng generate component calendar
```

命令完成后, 将组件添加到中`routes` `./src/app/app-routing.module.ts`的阵列。

```TypeScript
import { CalendarComponent } from './calendar/calendar.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'calendar', component: CalendarComponent }
];
```

打开`./src/app/calendar/calendar.component.ts`文件, 并将其内容替换为以下内容。

```TypeScript
import { Component, OnInit } from '@angular/core';
import * as moment from 'moment-timezone';

import { GraphService } from '../graph.service';
import { Event, DateTimeTimeZone } from '../event';
import { AlertsService } from '../alerts.service';

@Component({
  selector: 'app-calendar',
  templateUrl: './calendar.component.html',
  styleUrls: ['./calendar.component.css']
})
export class CalendarComponent implements OnInit {

  private events: Event[];

  constructor(
    private graphService: GraphService,
    private alertsService: AlertsService) { }

  ngOnInit() {
    this.graphService.getEvents()
      .then((events) => {
        this.events = events;
        // Temporary to display raw results
        this.alertsService.add('Events from Graph', JSON.stringify(events, null, 2));
      });
  }
}
```

现在, 这只是在页面上呈现 JSON 中的事件数组。 保存更改并重新启动该应用。 登录并单击导航栏中的 "**日历**" 链接。 如果一切正常, 应在用户的日历上看到一个 JSON 转储的事件。

## <a name="display-the-results"></a>显示结果

现在, 您可以更新`CalendarComponent`组件以以更用户友好的方式显示事件。 首先, 从`ngOnInit`函数中移除添加警报的临时代码。 更新的函数应如下所示。

```TypeScript
ngOnInit() {
  this.graphService.getEvents()
    .then((events) => {
      this.events = events;
    });
}
```

现在, 向`CalendarComponent`类中添加函数, 以将`DateTimeTimeZone`对象格式化为 ISO 字符串。

```TypeScript
formatDateTimeTimeZone(dateTime: DateTimeTimeZone): string {
  try {
    return moment.tz(dateTime.dateTime, dateTime.timeZone).format();
  }
  catch(error) {
    this.alertsService.add('DateTimeTimeZone conversion error', JSON.stringify(error));
  }
}
```

最后, 打开`./src/app/calendar/calendar.component.html`文件, 并将其内容替换为以下内容。

```html
<h1>Calendar</h1>
<table class="table">
  <thead>
    <th scope="col">Organizer</th>
    <th scope="col">Subject</th>
    <th scope="col">Start</th>
    <th scope="col">End</th>
  </thead>
  <tbody>
    <tr *ngFor="let event of events">
      <td>{{event.organizer.emailAddress.name}}</td>
      <td>{{event.subject}}</td>
      <td>{{formatDateTimeTimeZone(event.start) | date:'short' }}</td>
      <td>{{formatDateTimeTimeZone(event.end) | date: 'short' }}</td>
    </tr>
  </tbody>
</table>
```

这将遍历事件集合并为每个事件添加一个表行。 保存所做的更改, 然后重新启动应用程序。 单击 "**日历**" 链接, 应用现在应呈现一个事件表。

![事件表的屏幕截图](./images/add-msgraph-01.png)