<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ceb05-101">打开命令行接口 (CLI), 导航到您有权在其中创建文件的目录, 并运行以下命令来安装 "[角度" CLI](https://www.npmjs.com/package/@angular/cli)工具并创建一个新的角度应用。</span><span class="sxs-lookup"><span data-stu-id="ceb05-101">Open your command-line interface (CLI), navigate to a directory where you have rights to create files, and run the following commands to install the [Angular CLI](https://www.npmjs.com/package/@angular/cli) tool and create a new Angular app.</span></span>

```Shell
npm install -g @angular/cli
ng new graph-tutorial
```

<span data-ttu-id="ceb05-102">角度 CLI 将提示详细信息。</span><span class="sxs-lookup"><span data-stu-id="ceb05-102">The Angular CLI will prompt for more information.</span></span> <span data-ttu-id="ceb05-103">回答如下所示的提示。</span><span class="sxs-lookup"><span data-stu-id="ceb05-103">Answer the prompts as follows.</span></span>

```Shell
? Would you like to add Angular routing? Yes
? Which stylesheet format would you like to use? CSS
```

<span data-ttu-id="ceb05-104">命令完成后, 转到 CLI 中`graph-tutorial`的目录, 并运行以下命令以启动本地 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="ceb05-104">Once the command finishes, change to the `graph-tutorial` directory in your CLI and run the following command to start a local web server.</span></span>

```Shell
ng serve --open
```

<span data-ttu-id="ceb05-105">默认浏览器将打开[https://localhost:4200/](https://localhost:4200) , 并使用默认的角度页面。</span><span class="sxs-lookup"><span data-stu-id="ceb05-105">Your default browser opens to [https://localhost:4200/](https://localhost:4200) with a default Angular page.</span></span> <span data-ttu-id="ceb05-106">如果你的浏览器未打开, 请打开它[https://localhost:4200/](https://localhost:4200)并浏览以验证新应用是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="ceb05-106">If your browser doesn't open, open it and browse to [https://localhost:4200/](https://localhost:4200) to verify that the new app works.</span></span>

<span data-ttu-id="ceb05-107">在继续操作之前, 请先安装将使用的其他一些程序包:</span><span class="sxs-lookup"><span data-stu-id="ceb05-107">Before moving on, install some additional packages that you will use later:</span></span>

- <span data-ttu-id="ceb05-108">用于样式和常用组件的[引导](https://github.com/twbs/bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="ceb05-108">[bootstrap](https://github.com/twbs/bootstrap) for styling and common components.</span></span>
- <span data-ttu-id="ceb05-109">用于从角度使用引导组件的[ng 引导](https://github.com/ng-bootstrap/ng-bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="ceb05-109">[ng-bootstrap](https://github.com/ng-bootstrap/ng-bootstrap) for using Bootstrap components from Angular.</span></span>
- <span data-ttu-id="ceb05-110">[fontawesome](https://github.com/FortAwesome/angular-fontawesome) , 以在角中使用 fontawesome 图标。</span><span class="sxs-lookup"><span data-stu-id="ceb05-110">[angular-fontawesome](https://github.com/FortAwesome/angular-fontawesome) to use FontAwesome icons in Angular.</span></span>
- <span data-ttu-id="ceb05-111">[fontawesome-svg-core](https://github.com/FortAwesome/Font-Awesome)、 [free-regular-图标](https://github.com/FortAwesome/Font-Awesome), 以及示例中使用的 fontawesome 图标的[自由纯色 svg-图标](https://github.com/FortAwesome/Font-Awesome)。</span><span class="sxs-lookup"><span data-stu-id="ceb05-111">[fontawesome-svg-core](https://github.com/FortAwesome/Font-Awesome), [free-regular-svg-icons](https://github.com/FortAwesome/Font-Awesome), and [free-solid-svg-icons](https://github.com/FortAwesome/Font-Awesome) for the FontAwesome icons used in the sample.</span></span>
- <span data-ttu-id="ceb05-112">日期和时间格式的[时刻](https://github.com/moment/moment)。</span><span class="sxs-lookup"><span data-stu-id="ceb05-112">[moment](https://github.com/moment/moment) for formatting dates and times.</span></span>
- <span data-ttu-id="ceb05-113">[msal-](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md)用于对 Azure Active Directory 进行身份验证和检索访问令牌的角。</span><span class="sxs-lookup"><span data-stu-id="ceb05-113">[msal-angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) for authenticating to Azure Active Directory and retrieving access tokens.</span></span>
- <span data-ttu-id="ceb05-114">[rxjs-兼容](https://github.com/ReactiveX/rxjs/tree/master/compat)性, `msal-angular`包所需。</span><span class="sxs-lookup"><span data-stu-id="ceb05-114">[rxjs-compat](https://github.com/ReactiveX/rxjs/tree/master/compat), required for the `msal-angular` package.</span></span>
- <span data-ttu-id="ceb05-115">microsoft graph-用于调用 microsoft graph 的[客户端](https://github.com/microsoftgraph/msgraph-sdk-javascript)。</span><span class="sxs-lookup"><span data-stu-id="ceb05-115">[microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) for making calls to Microsoft Graph.</span></span>

<span data-ttu-id="ceb05-116">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ceb05-116">Run the following command in your CLI.</span></span>

```Shell
npm install bootstrap@4.3.1 @fortawesome/angular-fontawesome@0.3.0 @fortawesome/fontawesome-svg-core@1.2.15
npm install @fortawesome/free-regular-svg-icons@5.7.2 @fortawesome/free-solid-svg-icons@5.7.2
npm install moment@2.24.0 moment-timezone@0.5.23 @ng-bootstrap/ng-bootstrap@4.1.0
npm install @azure/msal-angular@0.1.2 rxjs-compat@6.4.0 @microsoft/microsoft-graph-client@1.4.0
```

## <a name="design-the-app"></a><span data-ttu-id="ceb05-117">设计应用程序</span><span class="sxs-lookup"><span data-stu-id="ceb05-117">Design the app</span></span>

<span data-ttu-id="ceb05-118">首先将引导数据库的 CSS 文件添加到应用程序, 并添加一些全局样式。</span><span class="sxs-lookup"><span data-stu-id="ceb05-118">Start by adding the Bootstrap CSS files to the app, as well as some global styles.</span></span> <span data-ttu-id="ceb05-119">打开`./src/styles.css` , 并添加以下行。</span><span class="sxs-lookup"><span data-stu-id="ceb05-119">Open the `./src/styles.css` and add the following lines.</span></span>

```CSS
@import "~bootstrap/dist/css/bootstrap.css";

/* Add padding for the nav bar */
body {
  padding-top: 4.5rem;
}

/* Style debug info in alerts */
.alert-pre {
  word-wrap: break-word;
  word-break: break-all;
  white-space: pre-wrap;
}
```

<span data-ttu-id="ceb05-120">接下来, 将 "引导" 和 "FontAwesome" 模块添加到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="ceb05-120">Next, add the Bootstrap and FontAwesome modules to the app.</span></span> <span data-ttu-id="ceb05-121">打开`./src/app/app.module.ts`并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="ceb05-121">Open `./src/app/app.module.ts` and add the following `import` statements to the top of the file.</span></span>

```TypeScript
import { NgbModule } from '@ng-bootstrap/ng-bootstrap';
import { FontAwesomeModule } from '@fortawesome/angular-fontawesome';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faExternalLinkAlt } from '@fortawesome/free-solid-svg-icons';
import { faUserCircle } from '@fortawesome/free-regular-svg-icons';
```

<span data-ttu-id="ceb05-122">然后, 在所有`import`语句后面添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="ceb05-122">Then add the following code after all of the `import` statements.</span></span>

```TypeScript
library.add(faExternalLinkAlt);
library.add(faUserCircle);
```

<span data-ttu-id="ceb05-123">在`@NgModule`声明中, 将现有`imports`数组替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="ceb05-123">In the `@NgModule` declaration, replace the existing `imports` array with the following.</span></span>

```TypeScript
imports: [
  BrowserModule,
  AppRoutingModule,
  NgbModule,
  FontAwesomeModule
]
```

<span data-ttu-id="ceb05-124">现在, 为页面上的顶部导航生成一个角度组件。</span><span class="sxs-lookup"><span data-stu-id="ceb05-124">Now generate an Angular component for the top navigation on the page.</span></span> <span data-ttu-id="ceb05-125">在 CLI 中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ceb05-125">In your CLI, run the following command.</span></span>

```Shell
ng generate component nav-bar
```

<span data-ttu-id="ceb05-126">命令完成后, 打开`./src/app/nav-bar/nav-bar.component.ts`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-126">Once the command completes, open the `./src/app/nav-bar/nav-bar.component.ts` file and replace its contents with the following.</span></span>

```TypeScript
import { Component, OnInit } from '@angular/core';

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
  user: any;

  constructor() { }

  ngOnInit() {
    this.showNav = false;
    this.authenticated = false;
    this.user = {};
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
      email: 'AdeleV@contoso.com'
    };
  }

  signOut(): void {
    // Temporary
    this.authenticated = false;
    this.user = {};
  }
}
```

<span data-ttu-id="ceb05-127">打开`./src/app/nav-bar/nav-bar.component.html`文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-127">Open the `./src/app/nav-bar/nav-bar.component.html` file and replace its contents with the following.</span></span>

```html
<nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
  <div class="container">
    <a routerLink="/" class="navbar-brand">Angular Graph Tutorial</a>
    <button class="navbar-toggler" type="button" (click)="toggleNavBar()" [attr.aria-expanded]="showNav"
    aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" [class.show]="showNav" id="navbarCollapse">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item">
          <a routerLink="/" class="nav-link" routerLinkActive="active">Home</a>
        </li>
        <li *ngIf="authenticated" class="nav-item">
          <a routerLink="/calendar" class="nav-link" routerLinkActive="active">Calendar</a>
        </li>
      </ul>
      <ul class="navbar-nav justify-content-end">
        <li class="nav-item">
          <a class="nav-link" href="https://docs.microsoft.com/graph/overview" target="_blank">
            <fa-icon [icon]="[ 'fas', 'external-link-alt' ]" class="mr-1"></fa-icon>Docs
          </a>
        </li>
        <li *ngIf="authenticated" ngbDropdown placement="bottom-right" class="nav-item">
          <a ngbDropdownToggle id="userMenu" class="nav-link" href="javascript:undefined" role="button" aria-haspopup="true"
            aria-expanded="false">
            <div *ngIf="user.avatar; then userAvatar else defaultAvatar"></div>
            <ng-template #userAvatar>
              <img src="user.avatar" class="rounded-circle align-self-center mr-2" style="width: 32px;">
            </ng-template>
            <ng-template #defaultAvatar>
              <fa-icon [icon]="[ 'far', 'user-circle' ]" fixedWidth="true" size="lg"
                class="rounded-circle align-self-center mr-2"></fa-icon>
            </ng-template>
          </a>
          <div ngbDropdownMenu aria-labelledby="userMenu">
            <h5 class="dropdown-item-text mb-0">{{user.displayName}}</h5>
            <p class="dropdown-item-text text-muted mb-0">{{user.email}}</p>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="javascript:undefined" role="button" (click)="signOut()">Sign Out</a>
          </div>
        </li>
        <li *ngIf="!authenticated" class="nav-item">
          <a class="nav-link" href="javascript:undefined" role="button" (click)="signIn()">Sign In</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

<span data-ttu-id="ceb05-128">接下来, 为该应用程序创建一个主页。</span><span class="sxs-lookup"><span data-stu-id="ceb05-128">Next, create a home page for the app.</span></span> <span data-ttu-id="ceb05-129">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ceb05-129">Run the following command in your CLI.</span></span>

```Shell
ng generate component home
```

<span data-ttu-id="ceb05-130">命令完成后, 打开`./src/app/home/home.component.ts`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-130">Once the command completes, open the `./src/app/home/home.component.ts` file and replace its contents with the following.</span></span>

```TypeScript
import { Component, OnInit } from '@angular/core';

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

<span data-ttu-id="ceb05-131">然后, 打开`./src/app/home/home.component.html`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-131">Then open the `./src/app/home/home.component.html` file and replace its contents with the following.</span></span>

```html
<div class="jumbotron">
  <h1>Angular Graph Tutorial</h1>
  <p class="lead">This sample app shows how to use the Microsoft Graph API from Angular</p>
  <div *ngIf="authenticated; then welcomeUser else signInPrompt"></div>
  <ng-template #welcomeUser>
    <h4>Welcome {{ user.displayName }}!</h4>
    <p>Use the navigation bar at the top of the page to get started.</p>
  </ng-template>
  <ng-template #signInPrompt>
    <a href="javascript:undefined" class="btn btn-primary btn-large" role="button" (click)="signIn()">Click here to sign in</a>
  </ng-template>
</div>
```

<span data-ttu-id="ceb05-132">现在, 创建一个通知服务, 应用程序可以使用该服务向用户显示邮件。</span><span class="sxs-lookup"><span data-stu-id="ceb05-132">Now create an alert service that the app can use to display messages to the user.</span></span> <span data-ttu-id="ceb05-133">首先创建一个简单`Alert`的类。</span><span class="sxs-lookup"><span data-stu-id="ceb05-133">Start by creating a simple `Alert` class.</span></span> <span data-ttu-id="ceb05-134">在名为`./src/app` `alert.ts`的目录中创建一个新文件, 并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="ceb05-134">Create a new file in the `./src/app` directory named `alert.ts` and add the following code.</span></span>

```TypeScript
export class Alert {
  message: string;
  debug: string;
}
```

<span data-ttu-id="ceb05-135">在 CLI 中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ceb05-135">In your CLI, run the following command.</span></span>

```Shell
ng generate service alerts
```

<span data-ttu-id="ceb05-136">打开`./src/app/alerts.service.ts`文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-136">Open the `./src/app/alerts.service.ts` file and replace its contents with the following.</span></span>

```TypeScript
import { Injectable } from '@angular/core';
import { Alert } from './alert';

@Injectable({
  providedIn: 'root'
})
export class AlertsService {

  alerts: Alert[] = [];

  add(message: string, debug: string) {
    this.alerts.push({message: message, debug: debug});
  }

  remove(alert: Alert) {
    this.alerts.splice(this.alerts.indexOf(alert), 1);
  }
}
```

<span data-ttu-id="ceb05-137">现在生成一个警报组件以显示警报。</span><span class="sxs-lookup"><span data-stu-id="ceb05-137">Now generate an alerts component to display alerts.</span></span> <span data-ttu-id="ceb05-138">在 CLI 中, 运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="ceb05-138">In your CLI, run the following command.</span></span>

```Shell
ng generate component alerts
```

<span data-ttu-id="ceb05-139">命令完成后, 打开`./src/app/alerts/alerts.component.ts`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-139">Once the command completes, open the `./src/app/alerts/alerts.component.ts` file and replace its contents with the following.</span></span>

```TypeScript
import { Component, OnInit } from '@angular/core';
import { AlertsService } from '../alerts.service';
import { Alert } from '../alert';

@Component({
  selector: 'app-alerts',
  templateUrl: './alerts.component.html',
  styleUrls: ['./alerts.component.css']
})
export class AlertsComponent implements OnInit {

  constructor(private alertsService: AlertsService) { }

  ngOnInit() {
  }

  close(alert: Alert) {
    this.alertsService.remove(alert);
  }
}
```

<span data-ttu-id="ceb05-140">然后, 打开`./src/app/alerts/alerts.component.html`文件并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-140">Then open the `./src/app/alerts/alerts.component.html` file and replace its contents with the following.</span></span>

```html
<div *ngFor="let alert of alertsService.alerts">
  <ngb-alert type="danger" (close)="close(alert)">
    <p>{{alert.message}}</p>
    <pre *ngIf="alert.debug" class="alert-pre border bg-light p-2"><code>{{alert.debug}}</code></pre>
  </ngb-alert>
</div>
```

<span data-ttu-id="ceb05-141">现在, 定义了这些基本组件, 更新应用程序以使用它们。</span><span class="sxs-lookup"><span data-stu-id="ceb05-141">Now with those basic components defined, update the app to use them.</span></span> <span data-ttu-id="ceb05-142">首先, 打开`./src/app/app-routing.module.ts`文件并将`const routes: Routes = [];`该行替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="ceb05-142">First, open the `./src/app/app-routing.module.ts` file and replace the `const routes: Routes = [];` line with the following code.</span></span>

```TypeScript
import { HomeComponent } from './home/home.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
];
```

<span data-ttu-id="ceb05-143">打开 `./src/app/app.component.html` 文件，并将其全部内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ceb05-143">Open the `./src/app/app.component.html` file and replace its entire contents with the following.</span></span>

```html
<app-nav-bar></app-nav-bar>
<main role="main" class="container">
  <app-alerts></app-alerts>
  <router-outlet></router-outlet>
</main>
```

<span data-ttu-id="ceb05-144">保存所有更改并刷新页面。</span><span class="sxs-lookup"><span data-stu-id="ceb05-144">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="ceb05-145">现在, 应用程序看起来应非常不同。</span><span class="sxs-lookup"><span data-stu-id="ceb05-145">Now, the app should look very different.</span></span>

![重新设计的主页的屏幕截图](images/create-app-01.png)