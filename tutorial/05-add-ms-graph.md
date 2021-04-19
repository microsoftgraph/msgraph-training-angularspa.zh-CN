<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="4ed21-101">在此练习中，你将 Microsoft Graph 合并到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="4ed21-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="4ed21-102">对于此应用程序，你将使用 [microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) 库调用 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="4ed21-102">For this application, you will use the [microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="4ed21-103">从 Outlook 获取日历事件</span><span class="sxs-lookup"><span data-stu-id="4ed21-103">Get calendar events from Outlook</span></span>

1. <span data-ttu-id="4ed21-104">添加新服务以保留所有 Graph 调用。</span><span class="sxs-lookup"><span data-stu-id="4ed21-104">Add a new service to hold all of your Graph calls.</span></span> <span data-ttu-id="4ed21-105">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="4ed21-105">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate service graph
    ```

    <span data-ttu-id="4ed21-106">与之前创建的身份验证服务一样，通过为此创建服务，你可以将该服务注入需要访问 Microsoft Graph 的任何组件。</span><span class="sxs-lookup"><span data-stu-id="4ed21-106">Just as with the authentication service you created earlier, creating a service for this allows you to inject it into any components that need access to Microsoft Graph.</span></span>

1. <span data-ttu-id="4ed21-107">命令完成后，打开 **./src/app/graph.service.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4ed21-107">Once the command completes, open **./src/app/graph.service.ts** and replace its contents with the following.</span></span>

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

    <span data-ttu-id="4ed21-108">考虑此代码将执行什么工作。</span><span class="sxs-lookup"><span data-stu-id="4ed21-108">Consider what this code is doing.</span></span>

    - <span data-ttu-id="4ed21-109">它在服务的构造函数中初始化 Graph 客户端。</span><span class="sxs-lookup"><span data-stu-id="4ed21-109">It initializes a Graph client in the constructor for the service.</span></span>
    - <span data-ttu-id="4ed21-110">它通过 `getCalendarView` 以下方式实现使用 Graph 客户端的函数：</span><span class="sxs-lookup"><span data-stu-id="4ed21-110">It implements a `getCalendarView` function that uses the Graph client in the following way:</span></span>
      - <span data-ttu-id="4ed21-111">将调用的 URL 为 `/me/calendarview`。</span><span class="sxs-lookup"><span data-stu-id="4ed21-111">The URL that will be called is `/me/calendarview`.</span></span>
      - <span data-ttu-id="4ed21-112">`header`方法包括 标头，这将导致返回事件的开始时间和结束时间在 `Prefer: outlook.timezone` 用户的首选时区。</span><span class="sxs-lookup"><span data-stu-id="4ed21-112">The `header` method includes the `Prefer: outlook.timezone` header, which causes the start and end times of the returned events to be in the user's preferred time zone.</span></span>
      - <span data-ttu-id="4ed21-113">`query`方法添加 `startDateTime` 和 `endDateTime` 参数，定义日历视图的时间窗口。</span><span class="sxs-lookup"><span data-stu-id="4ed21-113">The `query` method adds the `startDateTime` and `endDateTime` parameters, defining the window of time for the calendar view.</span></span>
      - <span data-ttu-id="4ed21-114">`select`方法将每个事件返回的字段限定为视图将实际使用的字段。</span><span class="sxs-lookup"><span data-stu-id="4ed21-114">The `select` method limits the fields returned for each events to just those the view will actually use.</span></span>
      - <span data-ttu-id="4ed21-115">`orderby`方法按开始时间对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="4ed21-115">The `orderby` method sorts the results by start time.</span></span>

1. <span data-ttu-id="4ed21-116">创建 Angular 组件以调用此新方法并显示调用的结果。</span><span class="sxs-lookup"><span data-stu-id="4ed21-116">Create an Angular component to call this new method and display the results of the call.</span></span> <span data-ttu-id="4ed21-117">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="4ed21-117">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate component calendar
    ```

1. <span data-ttu-id="4ed21-118">命令完成后，将组件添加到 `routes` **./src/app/app-routing.module.ts 中的数组**。</span><span class="sxs-lookup"><span data-stu-id="4ed21-118">Once the command completes, add the component to the `routes` array in **./src/app/app-routing.module.ts**.</span></span>

    ```typescript
    import { CalendarComponent } from './calendar/calendar.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
      { path: 'calendar', component: CalendarComponent },
    ];
    ```

1. <span data-ttu-id="4ed21-119">打开 **"tsconfig.js"，** 然后向 对象添加以下 `compilerOptions` 属性。</span><span class="sxs-lookup"><span data-stu-id="4ed21-119">Open **./tsconfig.json** and add the following property to the `compilerOptions` object.</span></span>

    ```json
    "resolveJsonModule": true
    ```

1. <span data-ttu-id="4ed21-120">打开 **./src/app/calendar/calendar.component.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4ed21-120">Open **./src/app/calendar/calendar.component.ts** and replace its contents with the following.</span></span>

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

<span data-ttu-id="4ed21-121">现在，这只是在页面上以 JSON 呈现事件数组。</span><span class="sxs-lookup"><span data-stu-id="4ed21-121">For now this just renders the array of events in JSON on the page.</span></span> <span data-ttu-id="4ed21-122">保存更改并重新启动该应用。</span><span class="sxs-lookup"><span data-stu-id="4ed21-122">Save your changes and restart the app.</span></span> <span data-ttu-id="4ed21-123">登录并单击导航 **栏中** 的"日历"链接。</span><span class="sxs-lookup"><span data-stu-id="4ed21-123">Sign in and click the **Calendar** link in the nav bar.</span></span> <span data-ttu-id="4ed21-124">如果一切正常，应在用户日历上看到事件被 JSON 卸载。</span><span class="sxs-lookup"><span data-stu-id="4ed21-124">If everything works, you should see a JSON dump of events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="4ed21-125">显示结果</span><span class="sxs-lookup"><span data-stu-id="4ed21-125">Display the results</span></span>

<span data-ttu-id="4ed21-126">现在，你可以 `CalendarComponent` 更新组件以更用户友好的方式显示事件。</span><span class="sxs-lookup"><span data-stu-id="4ed21-126">Now you can update the `CalendarComponent` component to display the events in a more user-friendly manner.</span></span>

1. <span data-ttu-id="4ed21-127">从 函数中删除添加警报的临时 `ngOnInit` 代码。</span><span class="sxs-lookup"><span data-stu-id="4ed21-127">Remove the temporary code that adds an alert from the `ngOnInit` function.</span></span> <span data-ttu-id="4ed21-128">更新的函数应如下所示。</span><span class="sxs-lookup"><span data-stu-id="4ed21-128">Your updated function should look like this.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/calendar/calendar.component.ts" id="ngOnInitSnippet":::

1. <span data-ttu-id="4ed21-129">将函数添加到 `CalendarComponent` 类，将对象 `DateTimeTimeZone` 格式化为 ISO 字符串。</span><span class="sxs-lookup"><span data-stu-id="4ed21-129">Add a function to the `CalendarComponent` class to format a `DateTimeTimeZone` object into an ISO string.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/calendar/calendar.component.ts" id="formatDateTimeTimeZoneSnippet":::

1. <span data-ttu-id="4ed21-130">打开 **"./src/app/calendar/calendar.component.html"，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4ed21-130">Open **./src/app/calendar/calendar.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/calendar/calendar.component.html" id="calendarHtml":::

<span data-ttu-id="4ed21-131">这将循环访问事件集合，并针对每个事件添加一个表行。</span><span class="sxs-lookup"><span data-stu-id="4ed21-131">This loops through the collection of events and adds a table row for each one.</span></span> <span data-ttu-id="4ed21-132">保存更改并重新启动应用。</span><span class="sxs-lookup"><span data-stu-id="4ed21-132">Save the changes and restart the app.</span></span> <span data-ttu-id="4ed21-133">单击" **日历"** 链接，应用现在应呈现一个事件表。</span><span class="sxs-lookup"><span data-stu-id="4ed21-133">Click on the **Calendar** link and the app should now render a table of events.</span></span>

![事件表的屏幕截图](./images/add-msgraph-01.png)
