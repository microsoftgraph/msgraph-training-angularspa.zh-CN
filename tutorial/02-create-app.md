<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="0cedb-101">在本节中，您将创建一个新的角度项目。</span><span class="sxs-lookup"><span data-stu-id="0cedb-101">In this section, you'll create a new Angular project.</span></span>

1. <span data-ttu-id="0cedb-102">打开命令行界面 (CLI) ，导航到您有权创建文件的目录，然后运行以下命令来安装 " [角度" CLI](https://www.npmjs.com/package/@angular/cli) 工具并创建一个新的角度应用。</span><span class="sxs-lookup"><span data-stu-id="0cedb-102">Open your command-line interface (CLI), navigate to a directory where you have rights to create files, and run the following commands to install the [Angular CLI](https://www.npmjs.com/package/@angular/cli) tool and create a new Angular app.</span></span>

    ```Shell
    npm install -g @angular/cli@10.1.7
    ng new graph-tutorial
    ```

1. <span data-ttu-id="0cedb-103">角度 CLI 将提示详细信息。</span><span class="sxs-lookup"><span data-stu-id="0cedb-103">The Angular CLI will prompt for more information.</span></span> <span data-ttu-id="0cedb-104">回答如下所示的提示。</span><span class="sxs-lookup"><span data-stu-id="0cedb-104">Answer the prompts as follows.</span></span>

    ```Shell
    ? Would you like to add Angular routing? Yes
    ? Which stylesheet format would you like to use? CSS
    ```

1. <span data-ttu-id="0cedb-105">命令完成后，转到 `graph-tutorial` CLI 中的目录，并运行以下命令以启动本地 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="0cedb-105">Once the command finishes, change to the `graph-tutorial` directory in your CLI and run the following command to start a local web server.</span></span>

    ```Shell
    ng serve --open
    ```

1. <span data-ttu-id="0cedb-106">默认浏览器将打开， [https://localhost:4200/](https://localhost:4200) 并使用默认的角度页面。</span><span class="sxs-lookup"><span data-stu-id="0cedb-106">Your default browser opens to [https://localhost:4200/](https://localhost:4200) with a default Angular page.</span></span> <span data-ttu-id="0cedb-107">如果你的浏览器未打开，请打开它并浏览以 [https://localhost:4200/](https://localhost:4200) 验证新应用是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="0cedb-107">If your browser doesn't open, open it and browse to [https://localhost:4200/](https://localhost:4200) to verify that the new app works.</span></span>

## <a name="add-node-packages"></a><span data-ttu-id="0cedb-108">添加节点包</span><span class="sxs-lookup"><span data-stu-id="0cedb-108">Add Node packages</span></span>

<span data-ttu-id="0cedb-109">在继续操作之前，请先安装将使用的其他一些程序包：</span><span class="sxs-lookup"><span data-stu-id="0cedb-109">Before moving on, install some additional packages that you will use later:</span></span>

- <span data-ttu-id="0cedb-110">用于样式和常用组件的[引导](https://github.com/twbs/bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="0cedb-110">[bootstrap](https://github.com/twbs/bootstrap) for styling and common components.</span></span>
- <span data-ttu-id="0cedb-111">用于从角度使用引导组件的[ng 引导](https://github.com/ng-bootstrap/ng-bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="0cedb-111">[ng-bootstrap](https://github.com/ng-bootstrap/ng-bootstrap) for using Bootstrap components from Angular.</span></span>
- <span data-ttu-id="0cedb-112">日期和时间格式的[时刻](https://github.com/moment/moment)。</span><span class="sxs-lookup"><span data-stu-id="0cedb-112">[moment](https://github.com/moment/moment) for formatting dates and times.</span></span>
- [<span data-ttu-id="0cedb-113">windows-iana</span><span class="sxs-lookup"><span data-stu-id="0cedb-113">windows-iana</span></span>](https://github.com/rubenillodo/windows-iana)
- <span data-ttu-id="0cedb-114">[msal-](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 用于对 Azure Active Directory 进行身份验证和检索访问令牌的角。</span><span class="sxs-lookup"><span data-stu-id="0cedb-114">[msal-angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) for authenticating to Azure Active Directory and retrieving access tokens.</span></span>
- <span data-ttu-id="0cedb-115">microsoft graph-用于调用 Microsoft Graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。</span><span class="sxs-lookup"><span data-stu-id="0cedb-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to Microsoft Graph.</span></span>

1. <span data-ttu-id="0cedb-116">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="0cedb-116">Run the following commands in your CLI.</span></span>

    ```Shell
    npm install bootstrap@4.5.3 @ng-bootstrap/ng-bootstrap@7.0.0 msal@1.4.2 @azure/msal-angular@1.1.1
    npm install moment@2.29.1 moment-timezone@0.5.31 windows-iana@4.2.1
    npm install @microsoft/microsoft-graph-client@2.1.0 @microsoft/microsoft-graph-types@1.24.0
    ```

1. <span data-ttu-id="0cedb-117">在 CLI 中运行以下命令，以添加 (由 ng-引导) 所需的角度本地化包。</span><span class="sxs-lookup"><span data-stu-id="0cedb-117">Run the following command in your CLI to add the Angular localization package (required by ng-bootstrap).</span></span>

    ```Shell
    ng add @angular/localize
    ```

## <a name="design-the-app"></a><span data-ttu-id="0cedb-118">设计应用程序</span><span class="sxs-lookup"><span data-stu-id="0cedb-118">Design the app</span></span>

<span data-ttu-id="0cedb-119">在本节中，您将为应用程序创建用户界面。</span><span class="sxs-lookup"><span data-stu-id="0cedb-119">In this section you'll create the user interface for the app.</span></span>

1. <span data-ttu-id="0cedb-120">打开 **/src/styles.css** ，并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="0cedb-120">Open **./src/styles.css** and add the following lines.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/styles.css":::

1. <span data-ttu-id="0cedb-121">将 "启动" 模块添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="0cedb-121">Add the Bootstrap module to the app.</span></span> <span data-ttu-id="0cedb-122">打开 **/src/app/app.module.ts** ，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-122">Open **./src/app/app.module.ts** and replace its contents with the following.</span></span>

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

1. <span data-ttu-id="0cedb-123">在 " **/src/app** " 文件夹中创建一个名为 " **user** " 的新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="0cedb-123">Create a new file in the **./src/app** folder named **user.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/user.ts" id="user":::

1. <span data-ttu-id="0cedb-124">为页面上的顶部导航生成一个角度组件。</span><span class="sxs-lookup"><span data-stu-id="0cedb-124">Generate an Angular component for the top navigation on the page.</span></span> <span data-ttu-id="0cedb-125">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="0cedb-125">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate component nav-bar
    ```

1. <span data-ttu-id="0cedb-126">命令完成后，打开 **/src/app/nav-bar/nav-bar.component.ts** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-126">Once the command completes, open **./src/app/nav-bar/nav-bar.component.ts** and replace its contents with the following.</span></span>

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
      showNav: boolean;
      // Is a user logged in?
      authenticated: boolean;
      // The user
      user: User;

      constructor() { }

      ngOnInit() {
        this.showNav = false;
        this.authenticated = false;
        this.user = null;
      }

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
          avatar: null
        };
      }

      signOut(): void {
        // Temporary
        this.authenticated = false;
        this.user = null;
      }
    }
    ```

1. <span data-ttu-id="0cedb-127">打开 **/src/app/nav-bar/nav-bar.component.html** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-127">Open **./src/app/nav-bar/nav-bar.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.html" id="navHtml":::

1. <span data-ttu-id="0cedb-128">为该应用程序创建一个主页。</span><span class="sxs-lookup"><span data-stu-id="0cedb-128">Create a home page for the app.</span></span> <span data-ttu-id="0cedb-129">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="0cedb-129">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate component home
    ```

1. <span data-ttu-id="0cedb-130">命令完成后，打开 **/src/app/home/home.component.ts** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-130">Once the command completes, open **./src/app/home/home.component.ts** and replace its contents with the following.</span></span>

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
      authenticated: boolean;
      // The user
      user: any;

      constructor() { }

      ngOnInit() {
        this.authenticated = false;
        this.user = {};
      }

      signIn(): void {
        // Temporary
        this.authenticated = true;
        this.user = {
          displayName: 'Adele Vance',
          email: 'AdeleV@contoso.com'
        };
      }
    }
    ```

1. <span data-ttu-id="0cedb-131">打开 **/src/app/home/home.component.html** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-131">Open **./src/app/home/home.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/home/home.component.html" id="homeHtml":::

1. <span data-ttu-id="0cedb-132">创建一个简单的 `Alert` 类。</span><span class="sxs-lookup"><span data-stu-id="0cedb-132">Create a simple `Alert` class.</span></span> <span data-ttu-id="0cedb-133">在 **/src/app** 目录中创建一个名为 " **alert** " 的新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="0cedb-133">Create a new file in the **./src/app** directory named **alert.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alert.ts" id="alert":::

1. <span data-ttu-id="0cedb-134">创建一个通知服务，应用程序可以使用该服务向用户显示邮件。</span><span class="sxs-lookup"><span data-stu-id="0cedb-134">Create an alert service that the app can use to display messages to the user.</span></span> <span data-ttu-id="0cedb-135">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="0cedb-135">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate service alerts
    ```

1. <span data-ttu-id="0cedb-136">打开 **/src/app/alerts.service.ts** ，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-136">Open **./src/app/alerts.service.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts.service.ts" id="alertsService":::

1. <span data-ttu-id="0cedb-137">生成警报组件以显示警告。</span><span class="sxs-lookup"><span data-stu-id="0cedb-137">Generate an alerts component to display alerts.</span></span> <span data-ttu-id="0cedb-138">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="0cedb-138">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate component alerts
    ```

1. <span data-ttu-id="0cedb-139">命令完成后，打开 **/src/app/alerts/alerts.component.ts** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-139">Once the command completes, open **./src/app/alerts/alerts.component.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts/alerts.component.ts" id="alertComponent":::

1. <span data-ttu-id="0cedb-140">打开 **/src/app/alerts/alerts.component.html** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-140">Open **./src/app/alerts/alerts.component.html** and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/alerts/alerts.component.html" id="alertHtml":::

1. <span data-ttu-id="0cedb-141">打开 **/src/app/app-routing.module.ts** ，并 `const routes: Routes = [];` 将该行替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="0cedb-141">Open **./src/app/app-routing.module.ts** and replace the `const routes: Routes = [];` line with the following code.</span></span>

    ```typescript
    import { HomeComponent } from './home/home.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
    ];
    ```

1. <span data-ttu-id="0cedb-142">打开 **/src/app/app.component.html** 并将其全部内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0cedb-142">Open **./src/app/app.component.html** and replace its entire contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/app.component.html" id="appHtml":::

1. <span data-ttu-id="0cedb-143">在 **/src/assets**目录中，添加您选择的命名**no-profile-photo.png**的图像文件。</span><span class="sxs-lookup"><span data-stu-id="0cedb-143">Add an image file of your choosing named **no-profile-photo.png** in the **./src/assets** directory.</span></span> <span data-ttu-id="0cedb-144">当用户在 Microsoft Graph 中没有照片时，此图像将用作用户的照片。</span><span class="sxs-lookup"><span data-stu-id="0cedb-144">This image will be used as the user's photo when the user has no photo in Microsoft Graph.</span></span>

<span data-ttu-id="0cedb-145">保存所有更改并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="0cedb-145">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="0cedb-146">现在，应用程序看起来应非常不同。</span><span class="sxs-lookup"><span data-stu-id="0cedb-146">Now, the app should look very different.</span></span>

![重新设计的主页的屏幕截图](images/create-app-01.png)
