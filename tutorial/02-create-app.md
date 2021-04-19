<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="72a09-101">在此部分中，你将创建新的 Angular 项目。</span><span class="sxs-lookup"><span data-stu-id="72a09-101">In this section, you'll create a new Angular project.</span></span>

1. <span data-ttu-id="72a09-102">打开命令行接口 (CLI) ，导航到你拥有创建文件权限的目录，然后运行以下命令来安装 [Angular CLI](https://www.npmjs.com/package/@angular/cli) 工具并创建新的 Angular 应用。</span><span class="sxs-lookup"><span data-stu-id="72a09-102">Open your command-line interface (CLI), navigate to a directory where you have rights to create files, and run the following commands to install the [Angular CLI](https://www.npmjs.com/package/@angular/cli) tool and create a new Angular app.</span></span>

    ```Shell
    npm install -g @angular/cli@11.2.9
    ng new graph-tutorial
    ```

1. <span data-ttu-id="72a09-103">Angular CLI 将提示输入详细信息。</span><span class="sxs-lookup"><span data-stu-id="72a09-103">The Angular CLI will prompt for more information.</span></span> <span data-ttu-id="72a09-104">回答提示，如下所示。</span><span class="sxs-lookup"><span data-stu-id="72a09-104">Answer the prompts as follows.</span></span>

    ```Shell
    ? Do you want to enforce stricter type checking and stricter bundle budgets in the workspace? Yes
    ? Would you like to add Angular routing? Yes
    ? Which stylesheet format would you like to use? CSS
    ```

1. <span data-ttu-id="72a09-105">命令完成后，在 CLI 中更改为 目录并运行 `graph-tutorial` 以下命令以启动本地 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="72a09-105">Once the command finishes, change to the `graph-tutorial` directory in your CLI and run the following command to start a local web server.</span></span>

    ```Shell
    ng serve --open
    ```

1. <span data-ttu-id="72a09-106">默认浏览器将打开， [https://localhost:4200/](https://localhost:4200) 并打开一个默认的 Angular 页面。</span><span class="sxs-lookup"><span data-stu-id="72a09-106">Your default browser opens to [https://localhost:4200/](https://localhost:4200) with a default Angular page.</span></span> <span data-ttu-id="72a09-107">如果浏览器未打开，请打开它并浏览 [https://localhost:4200/](https://localhost:4200) 以验证新应用是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="72a09-107">If your browser doesn't open, open it and browse to [https://localhost:4200/](https://localhost:4200) to verify that the new app works.</span></span>

## <a name="add-node-packages"></a><span data-ttu-id="72a09-108">添加节点包</span><span class="sxs-lookup"><span data-stu-id="72a09-108">Add Node packages</span></span>

<span data-ttu-id="72a09-109">在继续之前，请安装一些你稍后将使用的其他程序包：</span><span class="sxs-lookup"><span data-stu-id="72a09-109">Before moving on, install some additional packages that you will use later:</span></span>

- <span data-ttu-id="72a09-110">[用于样式](https://github.com/twbs/bootstrap) 设置和常见组件的引导。</span><span class="sxs-lookup"><span data-stu-id="72a09-110">[bootstrap](https://github.com/twbs/bootstrap) for styling and common components.</span></span>
- <span data-ttu-id="72a09-111">[ng-bootstrap，](https://github.com/ng-bootstrap/ng-bootstrap) 用于使用 Angular 中的 Bootstrap 组件。</span><span class="sxs-lookup"><span data-stu-id="72a09-111">[ng-bootstrap](https://github.com/ng-bootstrap/ng-bootstrap) for using Bootstrap components from Angular.</span></span>
- <span data-ttu-id="72a09-112">[设置](https://github.com/moment/moment) 日期和时间格式的时间。</span><span class="sxs-lookup"><span data-stu-id="72a09-112">[moment](https://github.com/moment/moment) for formatting dates and times.</span></span>
- [<span data-ttu-id="72a09-113">windows-iana</span><span class="sxs-lookup"><span data-stu-id="72a09-113">windows-iana</span></span>](https://github.com/rubenillodo/windows-iana)
- <span data-ttu-id="72a09-114">[msal-angular，](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 用于对 Azure Active Directory 进行身份验证和检索访问令牌。</span><span class="sxs-lookup"><span data-stu-id="72a09-114">[msal-angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) for authenticating to Azure Active Directory and retrieving access tokens.</span></span>
- <span data-ttu-id="72a09-115">用于调用 Microsoft Graph 的[microsoft-graph-client。](https://github.com/microsoftgraph/msgraph-sdk-javascript)</span><span class="sxs-lookup"><span data-stu-id="72a09-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to Microsoft Graph.</span></span>

1. <span data-ttu-id="72a09-116">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="72a09-116">Run the following commands in your CLI.</span></span>

    ```Shell
    npm install bootstrap@4.6.0 @ng-bootstrap/ng-bootstrap@9.1.0
    npm install @azure/msal-browser@2.14.0 @azure/msal-angular@2.0.0-beta.4
    npm install moment-timezone@0.5.33 windows-iana@5.0.1
    npm install @microsoft/microsoft-graph-client@2.2.1 @microsoft/microsoft-graph-types@1.35.0
    ```

1. <span data-ttu-id="72a09-117">在 CLI 中运行以下命令，添加 ng-bootstrap (所需的 Angular 本地化) 。</span><span class="sxs-lookup"><span data-stu-id="72a09-117">Run the following command in your CLI to add the Angular localization package (required by ng-bootstrap).</span></span>

    ```Shell
    ng add @angular/localize
    ```

## <a name="design-the-app"></a><span data-ttu-id="72a09-118">设计应用</span><span class="sxs-lookup"><span data-stu-id="72a09-118">Design the app</span></span>

<span data-ttu-id="72a09-119">在此部分中，你将为应用创建用户界面。</span><span class="sxs-lookup"><span data-stu-id="72a09-119">In this section you'll create the user interface for the app.</span></span>

1. <span data-ttu-id="72a09-120">打开 **./src/styles.css** 并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="72a09-120">Open **./src/styles.css** and add the following lines.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/styles.css":::

1. <span data-ttu-id="72a09-121">将 Bootstrap 模块添加到应用。</span><span class="sxs-lookup"><span data-stu-id="72a09-121">Add the Bootstrap module to the app.</span></span> <span data-ttu-id="72a09-122">打开 **./src/app/app.module.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-122">Open **./src/app/app.module.ts** and replace its contents with the following.</span></span>

    ```typescript
    import { BrowserModule } from '@angular/platform-browser';
    import { FormsModule } from '@angular/forms';
    import { NgModule } from '@angular/core';
    import { NgbModule } from '@ng-bootstrap/ng-bootstrap';

    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';

    @NgModule({
      declarations: [
        AppComponent
      ],
      imports: [
        BrowserModule,
        FormsModule,
        AppRoutingModule,
        NgbModule
      ],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule { }
    ```

1. <span data-ttu-id="72a09-123">在名为 **user.ts** 的 **./src/app** 文件夹中创建新文件并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="72a09-123">Create a new file in the **./src/app** folder named **user.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/user.ts" id="UserSnippet":::

1. <span data-ttu-id="72a09-124">为页面上的顶部导航生成 Angular 组件。</span><span class="sxs-lookup"><span data-stu-id="72a09-124">Generate an Angular component for the top navigation on the page.</span></span> <span data-ttu-id="72a09-125">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="72a09-125">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate component nav-bar
    ```

1. <span data-ttu-id="72a09-126">命令完成后，打开 **./src/app/nav-bar/nav-bar.component.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-126">Once the command completes, open **./src/app/nav-bar/nav-bar.component.ts** and replace its contents with the following.</span></span>

    ```typescript
    import { Component, OnInit } from '@angular/core';

    import { User } from '../user';

    @Component({
      selector: 'app-nav-bar',
      templateUrl: './nav-bar.component.html',
      styleUrls: ['./nav-bar.component.css']
    })
    export class NavBarComponent implements OnInit {

      // Should the collapsed nav show?
      showNav: boolean = false;
      // Is a user logged in?
      authenticated: boolean = false;
      // The user
      user?: User = undefined;

      constructor() { }

      ngOnInit() { }

      // Used by the Bootstrap navbar-toggler button to hide/show
      // the nav in a collapsed state
      toggleNavBar(): void {
        this.showNav = !this.showNav;
      }

      signIn(): void {
        // Temporary
        this.authenticated = true;
        this.user = {
          displayName: 'Adele Vance',
          email: 'AdeleV@contoso.com',
          avatar: '',
          timeZone: ''
        };
      }

      signOut(): void {
        // Temporary
        this.authenticated = false;
        this.user = undefined;
      }
    }
    ```

1. <span data-ttu-id="72a09-127">打开 **"./src/app/nav-bar/nav-bar.component.html"，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-127">Open **./src/app/nav-bar/nav-bar.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.html" id="navHtml":::

1. <span data-ttu-id="72a09-128">为应用创建主页。</span><span class="sxs-lookup"><span data-stu-id="72a09-128">Create a home page for the app.</span></span> <span data-ttu-id="72a09-129">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="72a09-129">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate component home
    ```

1. <span data-ttu-id="72a09-130">命令完成后，打开 **./src/app/home/home.component.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-130">Once the command completes, open **./src/app/home/home.component.ts** and replace its contents with the following.</span></span>

    ```typescript
    import { Component, OnInit } from '@angular/core';

    import { User } from '../user';

    @Component({
      selector: 'app-home',
      templateUrl: './home.component.html',
      styleUrls: ['./home.component.css']
    })
    export class HomeComponent implements OnInit {

      // Is a user logged in?
      authenticated: boolean = false;
      // The user
      user?: User = undefined;

      constructor() { }

      ngOnInit() { }

      signIn(): void {
        // Temporary
        this.authenticated = true;
        this.user = {
          displayName: 'Adele Vance',
          email: 'AdeleV@contoso.com',
          avatar: '',
          timeZone: ''
        };
      }
    }
    ```

1. <span data-ttu-id="72a09-131">打开 **"./src/app/home/home.component.html"，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-131">Open **./src/app/home/home.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/home/home.component.html" id="homeHtml":::

1. <span data-ttu-id="72a09-132">创建一个简单的 `Alert` 类。</span><span class="sxs-lookup"><span data-stu-id="72a09-132">Create a simple `Alert` class.</span></span> <span data-ttu-id="72a09-133">在 **./src/app** 目录中创建一个名为 **alert.ts** 的新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="72a09-133">Create a new file in the **./src/app** directory named **alert.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alert.ts" id="AlertSnippet":::

1. <span data-ttu-id="72a09-134">创建应用可用于向用户显示消息的警报服务。</span><span class="sxs-lookup"><span data-stu-id="72a09-134">Create an alert service that the app can use to display messages to the user.</span></span> <span data-ttu-id="72a09-135">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="72a09-135">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate service alerts
    ```

1. <span data-ttu-id="72a09-136">打开 **./src/app/alerts.service.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-136">Open **./src/app/alerts.service.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts.service.ts" id="alertsService":::

1. <span data-ttu-id="72a09-137">生成警报组件以显示警报。</span><span class="sxs-lookup"><span data-stu-id="72a09-137">Generate an alerts component to display alerts.</span></span> <span data-ttu-id="72a09-138">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="72a09-138">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate component alerts
    ```

1. <span data-ttu-id="72a09-139">命令完成后，打开 **./src/app/alerts/alerts.component.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-139">Once the command completes, open **./src/app/alerts/alerts.component.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts/alerts.component.ts" id="AlertsComponentSnippet":::

1. <span data-ttu-id="72a09-140">打开 **./src/app/alerts/alerts.component.html，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-140">Open **./src/app/alerts/alerts.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/alerts/alerts.component.html" id="AlertHtml":::

1. <span data-ttu-id="72a09-141">打开 **"./src/app/app-routing.module.ts"，** 将 行 `const routes: Routes = [];` 替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="72a09-141">Open **./src/app/app-routing.module.ts** and replace the `const routes: Routes = [];` line with the following code.</span></span>

    ```typescript
    import { HomeComponent } from './home/home.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
    ];
    ```

1. <span data-ttu-id="72a09-142">打开 **"./src/app/app.component.html"，** 并将其全部内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="72a09-142">Open **./src/app/app.component.html** and replace its entire contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/app.component.html" id="AppHtml":::

1. <span data-ttu-id="72a09-143">在 **./src/assets** **目录中** 添加no-profile-photo.png选择的图像文件。</span><span class="sxs-lookup"><span data-stu-id="72a09-143">Add an image file of your choosing named **no-profile-photo.png** in the **./src/assets** directory.</span></span> <span data-ttu-id="72a09-144">当用户在 Microsoft Graph 中没有照片时，此图像将用作用户的照片。</span><span class="sxs-lookup"><span data-stu-id="72a09-144">This image will be used as the user's photo when the user has no photo in Microsoft Graph.</span></span>

<span data-ttu-id="72a09-145">保存所有更改并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="72a09-145">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="72a09-146">现在，应用看起来应该非常不同。</span><span class="sxs-lookup"><span data-stu-id="72a09-146">Now, the app should look very different.</span></span>

![重新设计的主页的屏幕截图](images/create-app-01.png)
