<!-- markdownlint-disable MD002 MD041 -->

在此部分中，你将创建新的 Angular 项目。

1. 打开命令行接口 (CLI) ，导航到你拥有创建文件权限的目录，然后运行以下命令来安装 [Angular CLI](https://www.npmjs.com/package/@angular/cli) 工具并创建新的 Angular 应用。

    ```Shell
    npm install -g @angular/cli@11.2.9
    ng new graph-tutorial
    ```

1. Angular CLI 将提示输入详细信息。 回答提示，如下所示。

    ```Shell
    ? Do you want to enforce stricter type checking and stricter bundle budgets in the workspace? Yes
    ? Would you like to add Angular routing? Yes
    ? Which stylesheet format would you like to use? CSS
    ```

1. 命令完成后，在 CLI 中更改为 目录并运行 `graph-tutorial` 以下命令以启动本地 Web 服务器。

    ```Shell
    ng serve --open
    ```

1. 默认浏览器将打开， [https://localhost:4200/](https://localhost:4200) 并打开一个默认的 Angular 页面。 如果浏览器未打开，请打开它并浏览 [https://localhost:4200/](https://localhost:4200) 以验证新应用是否正常工作。

## <a name="add-node-packages"></a>添加节点包

在继续之前，请安装一些你稍后将使用的其他程序包：

- [用于样式](https://github.com/twbs/bootstrap) 设置和常见组件的引导。
- [ng-bootstrap，](https://github.com/ng-bootstrap/ng-bootstrap) 用于使用 Angular 中的 Bootstrap 组件。
- [设置](https://github.com/moment/moment) 日期和时间格式的时间。
- [windows-iana](https://github.com/rubenillodo/windows-iana)
- [msal-angular，](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 用于对 Azure Active Directory 进行身份验证和检索访问令牌。
- 用于调用 Microsoft Graph 的[microsoft-graph-client。](https://github.com/microsoftgraph/msgraph-sdk-javascript)

1. 在 CLI 中运行以下命令。

    ```Shell
    npm install bootstrap@4.6.0 @ng-bootstrap/ng-bootstrap@9.1.0
    npm install @azure/msal-browser@2.14.0 @azure/msal-angular@2.0.0-beta.4
    npm install moment-timezone@0.5.33 windows-iana@5.0.1
    npm install @microsoft/microsoft-graph-client@2.2.1 @microsoft/microsoft-graph-types@1.35.0
    ```

1. 在 CLI 中运行以下命令，添加 ng-bootstrap (所需的 Angular 本地化) 。

    ```Shell
    ng add @angular/localize
    ```

## <a name="design-the-app"></a>设计应用

在此部分中，你将为应用创建用户界面。

1. 打开 **./src/styles.css** 并添加以下行。

    :::code language="css" source="../demo/graph-tutorial/src/styles.css":::

1. 将 Bootstrap 模块添加到应用。 打开 **./src/app/app.module.ts，** 并将其内容替换为以下内容。

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

1. 在名为 **user.ts** 的 **./src/app** 文件夹中创建新文件并添加以下代码。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/user.ts" id="UserSnippet":::

1. 为页面上的顶部导航生成 Angular 组件。 在 CLI 中，运行以下命令。

    ```Shell
    ng generate component nav-bar
    ```

1. 命令完成后，打开 **./src/app/nav-bar/nav-bar.component.ts，** 并将其内容替换为以下内容。

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

1. 打开 **"./src/app/nav-bar/nav-bar.component.html"，** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.html" id="navHtml":::

1. 为应用创建主页。 在 CLI 中运行以下命令。

    ```Shell
    ng generate component home
    ```

1. 命令完成后，打开 **./src/app/home/home.component.ts，** 并将其内容替换为以下内容。

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

1. 打开 **"./src/app/home/home.component.html"，** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/home/home.component.html" id="homeHtml":::

1. 创建一个简单的 `Alert` 类。 在 **./src/app** 目录中创建一个名为 **alert.ts** 的新文件，并添加以下代码。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alert.ts" id="AlertSnippet":::

1. 创建应用可用于向用户显示消息的警报服务。 在 CLI 中，运行以下命令。

    ```Shell
    ng generate service alerts
    ```

1. 打开 **./src/app/alerts.service.ts，** 并将其内容替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts.service.ts" id="alertsService":::

1. 生成警报组件以显示警报。 在 CLI 中，运行以下命令。

    ```Shell
    ng generate component alerts
    ```

1. 命令完成后，打开 **./src/app/alerts/alerts.component.ts，** 并将其内容替换为以下内容。

    :::code language="typescript" source="../demo/graph-tutorial/src/app/alerts/alerts.component.ts" id="AlertsComponentSnippet":::

1. 打开 **./src/app/alerts/alerts.component.html，** 并将其内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/alerts/alerts.component.html" id="AlertHtml":::

1. 打开 **"./src/app/app-routing.module.ts"，** 将 行 `const routes: Routes = [];` 替换为以下代码。

    ```typescript
    import { HomeComponent } from './home/home.component';

    const routes: Routes = [
      { path: '', component: HomeComponent },
    ];
    ```

1. 打开 **"./src/app/app.component.html"，** 并将其全部内容替换为以下内容。

    :::code language="html" source="../demo/graph-tutorial/src/app/app.component.html" id="AppHtml":::

1. 在 **./src/assets** **目录中** 添加no-profile-photo.png选择的图像文件。 当用户在 Microsoft Graph 中没有照片时，此图像将用作用户的照片。

保存所有更改并刷新页面。 现在，应用看起来应该非常不同。

![重新设计的主页的屏幕截图](images/create-app-01.png)
