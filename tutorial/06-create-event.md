<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="d2093-101">在本节中，您将添加在用户日历上创建事件的功能。</span><span class="sxs-lookup"><span data-stu-id="d2093-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="d2093-102">打开 **/src/app/graph.service.ts** ，并将以下函数添加到 `GraphService` 类中。</span><span class="sxs-lookup"><span data-stu-id="d2093-102">Open **./src/app/graph.service.ts** and add the following function to the `GraphService` class.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/graph.service.ts" id="AddEventSnippet":::

## <a name="create-a-new-event-form"></a><span data-ttu-id="d2093-103">创建新的事件表单</span><span class="sxs-lookup"><span data-stu-id="d2093-103">Create a new event form</span></span>

1. <span data-ttu-id="d2093-104">创建一个角度组件以显示窗体并调用此新函数。</span><span class="sxs-lookup"><span data-stu-id="d2093-104">Create an Angular component to display a form and call this new function.</span></span> <span data-ttu-id="d2093-105">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="d2093-105">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate component new-event
    ```

1. <span data-ttu-id="d2093-106">命令完成后，将组件添加到 `routes` **/src/app/app-routing.module.ts**中的数组中。</span><span class="sxs-lookup"><span data-stu-id="d2093-106">Once the command completes, add the component to the `routes` array in **./src/app/app-routing.module.ts**.</span></span>

    ```typescript
    import { NewEventComponent } from './new-event/new-event.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
      { path: 'calendar', component: CalendarComponent },
      { path: 'newevent', component: NewEventComponent },
    ];
    ```

1. <span data-ttu-id="d2093-107">在名为**new**的 **/src/app/new-event**目录中创建一个新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="d2093-107">Create a new file in the **./src/app/new-event** directory named **new-event.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/new-event/new-event.ts" id="NewEventSnippet":::

    <span data-ttu-id="d2093-108">此类将充当新事件窗体的模型。</span><span class="sxs-lookup"><span data-stu-id="d2093-108">This class will serve as the model for the new event form.</span></span>

1. <span data-ttu-id="d2093-109">打开 **/src/app/new-event/new-event.component.ts** 并将其内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="d2093-109">Open **./src/app/new-event/new-event.component.ts** and replace its contents with the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/new-event/new-event.component.ts" id="NewEventComponentSnippet":::

1. <span data-ttu-id="d2093-110">打开 **/src/app/new-event/new-event.component.html** 并将其内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="d2093-110">Open **./src/app/new-event/new-event.component.html** and replace its contents with the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/new-event/new-event.component.html" id="NewEventFormSnippet":::

1. <span data-ttu-id="d2093-111">保存更改并刷新应用。</span><span class="sxs-lookup"><span data-stu-id="d2093-111">Save the changes and refresh the app.</span></span> <span data-ttu-id="d2093-112">在 "日历" 页上选择 " **新建事件** " 按钮，然后使用该窗体在用户日历上创建事件。</span><span class="sxs-lookup"><span data-stu-id="d2093-112">Select the **New event** button on the calendar page, then use the form to create an event on the user's calendar.</span></span>

    ![新事件表单的屏幕截图](images/create-event.png)
