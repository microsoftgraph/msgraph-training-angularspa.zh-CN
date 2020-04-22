<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f1f5a-101">在本节中，您将创建一个新的角度项目。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-101">In this section, you'll create a new Angular project.</span></span>

1. <span data-ttu-id="f1f5a-102">打开命令行接口（CLI），导航到您有权在其中创建文件的目录，并运行以下命令来安装 "[角度" CLI](https://www.npmjs.com/package/@angular/cli)工具并创建一个新的角度应用。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-102">Open your command-line interface (CLI), navigate to a directory where you have rights to create files, and run the following commands to install the [Angular CLI](https://www.npmjs.com/package/@angular/cli) tool and create a new Angular app.</span></span>

    ```Shell
    npm install -g @angular/cli@9.0.6
    ng new graph-tutorial
    ```

1. <span data-ttu-id="f1f5a-103">角度 CLI 将提示详细信息。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-103">The Angular CLI will prompt for more information.</span></span> <span data-ttu-id="f1f5a-104">回答如下所示的提示。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-104">Answer the prompts as follows.</span></span>

    ```Shell
    ? Would you like to add Angular routing? Yes
    ? Which stylesheet format would you like to use? CSS
    ```

1. <span data-ttu-id="f1f5a-105">命令完成后，转到 CLI 中`graph-tutorial`的目录，并运行以下命令以启动本地 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-105">Once the command finishes, change to the `graph-tutorial` directory in your CLI and run the following command to start a local web server.</span></span>

    ```Shell
    ng serve --open
    ```

1. <span data-ttu-id="f1f5a-106">默认浏览器将打开[https://localhost:4200/](https://localhost:4200) ，并使用默认的角度页面。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-106">Your default browser opens to [https://localhost:4200/](https://localhost:4200) with a default Angular page.</span></span> <span data-ttu-id="f1f5a-107">如果你的浏览器未打开，请打开它[https://localhost:4200/](https://localhost:4200)并浏览以验证新应用是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-107">If your browser doesn't open, open it and browse to [https://localhost:4200/](https://localhost:4200) to verify that the new app works.</span></span>

## <a name="add-node-packages"></a><span data-ttu-id="f1f5a-108">添加节点包</span><span class="sxs-lookup"><span data-stu-id="f1f5a-108">Add Node packages</span></span>

<span data-ttu-id="f1f5a-109">在继续操作之前，请先安装将使用的其他一些程序包：</span><span class="sxs-lookup"><span data-stu-id="f1f5a-109">Before moving on, install some additional packages that you will use later:</span></span>

- <span data-ttu-id="f1f5a-110">用于样式和常用组件的[引导](https://github.com/twbs/bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-110">[bootstrap](https://github.com/twbs/bootstrap) for styling and common components.</span></span>
- <span data-ttu-id="f1f5a-111">用于从角度使用引导组件的[ng 引导](https://github.com/ng-bootstrap/ng-bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-111">[ng-bootstrap](https://github.com/ng-bootstrap/ng-bootstrap) for using Bootstrap components from Angular.</span></span>
- <span data-ttu-id="f1f5a-112">[fontawesome](https://github.com/FortAwesome/angular-fontawesome) ，以在角中使用 fontawesome 图标。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-112">[angular-fontawesome](https://github.com/FortAwesome/angular-fontawesome) to use FontAwesome icons in Angular.</span></span>
- <span data-ttu-id="f1f5a-113">[fontawesome-svg-core](https://github.com/FortAwesome/Font-Awesome)、 [free-regular-图标](https://github.com/FortAwesome/Font-Awesome)，以及示例中使用的 fontawesome 图标的[自由纯色 svg-图标](https://github.com/FortAwesome/Font-Awesome)。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-113">[fontawesome-svg-core](https://github.com/FortAwesome/Font-Awesome), [free-regular-svg-icons](https://github.com/FortAwesome/Font-Awesome), and [free-solid-svg-icons](https://github.com/FortAwesome/Font-Awesome) for the FontAwesome icons used in the sample.</span></span>
- <span data-ttu-id="f1f5a-114">日期和时间格式的[时刻](https://github.com/moment/moment)。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-114">[moment](https://github.com/moment/moment) for formatting dates and times.</span></span>
- <span data-ttu-id="f1f5a-115">[msal-](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md)用于对 Azure Active Directory 进行身份验证和检索访问令牌的角。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-115">[msal-angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) for authenticating to Azure Active Directory and retrieving access tokens.</span></span>
- <span data-ttu-id="f1f5a-116">microsoft graph-用于调用 Microsoft Graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-116">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to Microsoft Graph.</span></span>

1. <span data-ttu-id="f1f5a-117">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-117">Run the following commands in your CLI.</span></span>

    ```Shell
    npm install bootstrap@4.4.1 @fortawesome/angular-fontawesome@0.6.0 @fortawesome/fontawesome-svg-core@1.2.27
    npm install @fortawesome/free-regular-svg-icons@5.12.1 @fortawesome/free-solid-svg-icons@5.12.1
    npm install moment@2.24.0 moment-timezone@0.5.28 @ng-bootstrap/ng-bootstrap@6.0.0
    npm install msal@1.2.1 @azure/msal-angular@1.0.0-beta.4 @microsoft/microsoft-graph-client@2.0.0
    ```

1. <span data-ttu-id="f1f5a-118">在 CLI 中运行以下命令，以添加角度本地化包（由 ng-引导程序所必需）。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-118">Run the following command in your CLI to add the Angular localization package (required by ng-bootstrap).</span></span>

    ```Shell
    ng add @angular/localize
    ```

## <a name="design-the-app"></a><span data-ttu-id="f1f5a-119">设计应用程序</span><span class="sxs-lookup"><span data-stu-id="f1f5a-119">Design the app</span></span>

<span data-ttu-id="f1f5a-120">在本节中，您将为应用程序创建用户界面。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-120">In this section you'll create the user interface for the app.</span></span>

1. <span data-ttu-id="f1f5a-121">打开`./src/styles.css` ，并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-121">Open the `./src/styles.css` and add the following lines.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/styles.css":::

1. <span data-ttu-id="f1f5a-122">将 "引导" 和 "FontAwesome" 模块添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-122">Add the Bootstrap and FontAwesome modules to the app.</span></span> <span data-ttu-id="f1f5a-123">打开`./src/app/app.module.ts`并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-123">Open `./src/app/app.module.ts` and replace its contents with the following.</span></span>

    ```TypeScript
    import { BrowserModule } from '@angular/platform-browser';
    import { NgModule } from '@angular/core';
    import { NgbModule } from '@ng-bootstrap/ng-bootstrap';
    import { FontAwesomeModule, FaIconLibrary } from '@fortawesome/angular-fontawesome';
    import { faExternalLinkAlt } from '@fortawesome/free-solid-svg-icons';
    import { faUserCircle } from '@fortawesome/free-regular-svg-icons';

    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';
    import { NavBarComponent } from './nav-bar/nav-bar.component';
    import { HomeComponent } from './home/home.component';
    import { AlertsComponent } from './alerts/alerts.component';

    @NgModule({
      declarations: [
        AppComponent,
        NavBarComponent,
        HomeComponent,
        AlertsComponent
      ],
      imports: [
        BrowserModule,
        AppRoutingModule,
        NgbModule,
        FontAwesomeModule
      ],
      providers: [],
      bootstrap: [AppComponent]
    })
    export class AppModule {
      constructor(library: FaIconLibrary) {
        // Register the FontAwesome icons used by the app
        library.addIcons(faExternalLinkAlt, faUserCircle);
      }
     }
    ```

1. <span data-ttu-id="f1f5a-124">在名为`./src/app` `user.ts`的文件夹中创建一个新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-124">Create a new file in the `./src/app` folder named `user.ts` and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/user.ts" id="user":::

1. <span data-ttu-id="f1f5a-125">为页面上的顶部导航生成一个角度组件。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-125">Generate an Angular component for the top navigation on the page.</span></span> <span data-ttu-id="f1f5a-126">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-126">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate component nav-bar
    ```

1. <span data-ttu-id="f1f5a-127">命令完成后，打开`./src/app/nav-bar/nav-bar.component.ts`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-127">Once the command completes, open the `./src/app/nav-bar/nav-bar.component.ts` file and replace its contents with the following.</span></span>

    ```TypeScript
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

1. <span data-ttu-id="f1f5a-128">打开`./src/app/nav-bar/nav-bar.component.html`文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-128">Open the `./src/app/nav-bar/nav-bar.component.html` file and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.html" id="navHtml":::

1. <span data-ttu-id="f1f5a-129">为该应用程序创建一个主页。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-129">Create a home page for the app.</span></span> <span data-ttu-id="f1f5a-130">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-130">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate component home
    ```

1. <span data-ttu-id="f1f5a-131">命令完成后，打开`./src/app/home/home.component.ts`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-131">Once the command completes, open the `./src/app/home/home.component.ts` file and replace its contents with the following.</span></span>

    ```TypeScript
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

1. <span data-ttu-id="f1f5a-132">打开`./src/app/home/home.component.html`文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-132">Open the `./src/app/home/home.component.html` file and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/home/home.component.html" id="homeHtml":::

1. <span data-ttu-id="f1f5a-133">创建一个简单`Alert`的类。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-133">Create a simple `Alert` class.</span></span> <span data-ttu-id="f1f5a-134">在名为`./src/app` `alert.ts`的目录中创建一个新文件，并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-134">Create a new file in the `./src/app` directory named `alert.ts` and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alert.ts" id="alert":::

1. <span data-ttu-id="f1f5a-135">创建一个通知服务，应用程序可以使用该服务向用户显示邮件。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-135">Create an alert service that the app can use to display messages to the user.</span></span> <span data-ttu-id="f1f5a-136">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-136">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate service alerts
    ```

1. <span data-ttu-id="f1f5a-137">打开`./src/app/alerts.service.ts`文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-137">Open the `./src/app/alerts.service.ts` file and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts.service.ts" id="alertsService":::

1. <span data-ttu-id="f1f5a-138">生成警报组件以显示警告。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-138">Generate an alerts component to display alerts.</span></span> <span data-ttu-id="f1f5a-139">在 CLI 中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-139">In your CLI, run the following command.</span></span>

    ```Shell
    ng generate component alerts
    ```

1. <span data-ttu-id="f1f5a-140">命令完成后，打开`./src/app/alerts/alerts.component.ts`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-140">Once the command completes, open the `./src/app/alerts/alerts.component.ts` file and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts/alerts.component.ts" id="alertComponent":::

1. <span data-ttu-id="f1f5a-141">打开`./src/app/alerts/alerts.component.html`文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-141">Open the `./src/app/alerts/alerts.component.html` file and replace its contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/alerts/alerts.component.html" id="alertHtml":::

1. <span data-ttu-id="f1f5a-142">打开`./src/app/app-routing.module.ts`文件，并将`const routes: Routes = [];`该行替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-142">Open the `./src/app/app-routing.module.ts` file and replace the `const routes: Routes = [];` line with the following code.</span></span>

    ```typescript
    import { HomeComponent } from './home/home.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
    ];
    ```

1. <span data-ttu-id="f1f5a-143">打开 `./src/app/app.component.html` 文件，并将其全部内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-143">Open the `./src/app/app.component.html` file and replace its entire contents with the following.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/app/app.component.html" id="appHtml":::

<span data-ttu-id="f1f5a-144">保存所有更改并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-144">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="f1f5a-145">现在，应用程序看起来应非常不同。</span><span class="sxs-lookup"><span data-stu-id="f1f5a-145">Now, the app should look very different.</span></span>

![重新设计的主页的屏幕截图](images/create-app-01.png)
