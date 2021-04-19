<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="dd438-101">在此练习中，你将从上一练习中扩展应用程序，以支持使用 Azure AD 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="dd438-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="dd438-102">这是获取调用 Microsoft Graph 所需的 OAuth 访问令牌所必需的。</span><span class="sxs-lookup"><span data-stu-id="dd438-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="dd438-103">在此步骤中，将 [Angular 的 Microsoft 身份验证库](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) 集成到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="dd438-103">In this step you will integrate the [Microsoft Authentication Library for Angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular/README.md) into the application.</span></span>

1. <span data-ttu-id="dd438-104">在 **./src** 目录中新建一个名为 **oauth.ts** 的文件并添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="dd438-104">Create a new file in the **./src** directory named **oauth.ts** and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/oauth.example.ts":::

    <span data-ttu-id="dd438-105">将 `YOUR_APP_ID_HERE` 替换为应用程序注册门户中的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="dd438-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="dd438-106">如果你使用的是源代码管理（如 git），那么现在应该从源代码管理中排除 **oauth.ts** 文件，以避免意外泄露应用 ID。</span><span class="sxs-lookup"><span data-stu-id="dd438-106">If you're using source control such as git, now would be a good time to exclude the **oauth.ts** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="dd438-107">打开 **./src/app/app.module.ts，** 将以下语句 `import` 添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="dd438-107">Open **./src/app/app.module.ts** and add the following `import` statements to the top of the file.</span></span>

    ```typescript
    import { IPublicClientApplication,
             PublicClientApplication,
             BrowserCacheLocation } from '@azure/msal-browser';
    import { MsalModule,
             MsalService,
             MSAL_INSTANCE } from '@azure/msal-angular';
    import { OAuthSettings } from '../oauth';
    ```

1. <span data-ttu-id="dd438-108">在 语句下方添加以下 `import` 函数。</span><span class="sxs-lookup"><span data-stu-id="dd438-108">Add the following function below the `import` statements.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="MSALFactorySnippet":::

1. <span data-ttu-id="dd438-109">将 `MsalModule` 添加到 `imports` 声明内的 `@NgModule` 数组。</span><span class="sxs-lookup"><span data-stu-id="dd438-109">Add the `MsalModule` to the `imports` array inside the `@NgModule` declaration.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="ImportsSnippet" highlight="6":::

1. <span data-ttu-id="dd438-110">将 `MSALInstanceFactory` 和 `MsalService` 添加到 `providers` 声明内的 `@NgModule` 数组。</span><span class="sxs-lookup"><span data-stu-id="dd438-110">Add the `MSALInstanceFactory` and `MsalService` to the `providers` array inside the `@NgModule` declaration.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/app.module.ts" id="ProvidersSnippet" highlight="2-6":::

## <a name="implement-sign-in"></a><span data-ttu-id="dd438-111">实施登录</span><span class="sxs-lookup"><span data-stu-id="dd438-111">Implement sign-in</span></span>

<span data-ttu-id="dd438-112">在此部分中，你将创建身份验证服务并实施登录和注销。</span><span class="sxs-lookup"><span data-stu-id="dd438-112">In this section you'll create an authentication service and implement sign-in and sign-out.</span></span>

1. <span data-ttu-id="dd438-113">在 CLI 中运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="dd438-113">Run the following command in your CLI.</span></span>

    ```Shell
    ng generate service auth
    ```

    <span data-ttu-id="dd438-114">通过为此创建服务，可以轻松地将该服务注入需要访问身份验证方法的任何组件。</span><span class="sxs-lookup"><span data-stu-id="dd438-114">By creating a service for this, you can easily inject it into any components that need access to authentication methods.</span></span>

1. <span data-ttu-id="dd438-115">命令完成后，打开 **./src/app/auth.service.ts，** 并将其内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="dd438-115">Once the command finishes, open **./src/app/auth.service.ts** and replace its contents with the following code.</span></span>

    ```typescript
    import { Injectable } from '@angular/core';
    import { AccountInfo } from '@azure/msal-browser';
    import { MsalService } from '@azure/msal-angular';

    import { AlertsService } from './alerts.service';
    import { OAuthSettings } from '../oauth';
    import { User } from './user';

    @Injectable({
      providedIn: 'root'
    })

    export class AuthService {
      public authenticated: boolean;
      public user?: User;

      constructor(
        private msalService: MsalService,
        private alertsService: AlertsService) {

        this.authenticated = false;
        this.user = undefined;
      }

      // Prompt the user to sign in and
      // grant consent to the requested permission scopes
      async signIn(): Promise<void> {
        const result = await this.msalService
          .loginPopup(OAuthSettings)
          .toPromise()
          .catch((reason) => {
            this.alertsService.addError('Login failed',
              JSON.stringify(reason, null, 2));
          });

        if (result) {
          this.msalService.instance.setActiveAccount(result.account);
          this.authenticated = true;
          // Temporary placeholder
          this.user = new User();
          this.user.displayName = 'Adele Vance';
          this.user.email = 'AdeleV@contoso.com';
          this.user.avatar = '/assets/no-profile-photo.png';
        }
      }

      // Sign out
      async signOut(): Promise<void> {
        await this.msalService.logout().toPromise();
        this.user = undefined;
        this.authenticated = false;
      }

      // Silently request an access token
      async getAccessToken(): Promise<string> {
        const result = await this.msalService
          .acquireTokenSilent({
            scopes: OAuthSettings.scopes
          })
          .toPromise()
          .catch((reason) => {
            this.alertsService.addError('Get token failed', JSON.stringify(reason, null, 2));
          });

        if (result) {
          // Temporary to display token in an error box
          this.alertsService.addSuccess('Token acquired', result.accessToken);
          return result.accessToken;
        }

        // Couldn't get a token
        this.authenticated = false;
        return '';
      }
    }
    ```

1. <span data-ttu-id="dd438-116">打开 **./src/app/nav-bar/nav-bar.component.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="dd438-116">Open **./src/app/nav-bar/nav-bar.component.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/nav-bar/nav-bar.component.ts" id="navBarSnippet" highlight="3,15-22,24,34-36,38-40":::

1. <span data-ttu-id="dd438-117">打开 **./src/app/home/home.component.ts，** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="dd438-117">Open **./src/app/home/home.component.ts** and replace its contents with the following.</span></span>

    :::code language="typescript" source="snippets/snippets.ts" id="homeSnippet" highlight="3,13-20,22,26-33":::

<span data-ttu-id="dd438-118">保存更改并刷新浏览器。</span><span class="sxs-lookup"><span data-stu-id="dd438-118">Save your changes and refresh the browser.</span></span> <span data-ttu-id="dd438-119">单击 **"单击此处登录"按钮** ，应重定向到 `https://login.microsoftonline.com` 。</span><span class="sxs-lookup"><span data-stu-id="dd438-119">Click the **Click here to sign in** button and you should be redirected to `https://login.microsoftonline.com`.</span></span> <span data-ttu-id="dd438-120">使用 Microsoft 帐户登录并同意请求的权限。</span><span class="sxs-lookup"><span data-stu-id="dd438-120">Login with your Microsoft account and consent to the requested permissions.</span></span> <span data-ttu-id="dd438-121">应用页面应刷新，显示令牌。</span><span class="sxs-lookup"><span data-stu-id="dd438-121">The app page should refresh, showing the token.</span></span>

### <a name="get-user-details"></a><span data-ttu-id="dd438-122">获取用户详细信息</span><span class="sxs-lookup"><span data-stu-id="dd438-122">Get user details</span></span>

<span data-ttu-id="dd438-123">现在，身份验证服务为用户的邮箱和电子邮件地址显示名称常量值。</span><span class="sxs-lookup"><span data-stu-id="dd438-123">Right now the authentication service sets constant values for the user's display name and email address.</span></span> <span data-ttu-id="dd438-124">现在你已拥有访问令牌，可以从 Microsoft Graph 获取用户详细信息，以便这些值对应于当前用户。</span><span class="sxs-lookup"><span data-stu-id="dd438-124">Now that you have an access token, you can get user details from Microsoft Graph so those values correspond to the current user.</span></span>

1. <span data-ttu-id="dd438-125">打开 **./src/app/auth.service.ts，** 将以下语句 `import` 添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="dd438-125">Open **./src/app/auth.service.ts** and add the following `import` statements to the top of the file.</span></span>

    ```typescript
    import { Client } from '@microsoft/microsoft-graph-client';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    ```

1. <span data-ttu-id="dd438-126">将新函数添加到称为 `AuthService` 的 `getUser` 类。</span><span class="sxs-lookup"><span data-stu-id="dd438-126">Add a new function to the `AuthService` class called `getUser`.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/auth.service.ts" id="GetUserSnippet":::

1. <span data-ttu-id="dd438-127">在 方法中查找并删除以下 `getAccessToken` 代码，以添加警报以显示访问令牌。</span><span class="sxs-lookup"><span data-stu-id="dd438-127">Locate and remove the following code in the `getAccessToken` method that adds an alert to display the access token.</span></span>

    ```typescript
    // Temporary to display token in an error box
    this.alertsService.addSuccess('Token acquired', result);
    ```

1. <span data-ttu-id="dd438-128">从 方法中查找并删除以下 `signIn` 代码。</span><span class="sxs-lookup"><span data-stu-id="dd438-128">Locate and remove the following code from the `signIn` method.</span></span>

    ```typescript
    // Temporary placeholder
    this.user = new User();
    this.user.displayName = "Adele Vance";
    this.user.email = "AdeleV@contoso.com";
    this.user.avatar = '/assets/no-profile-photo.png';
    ```

1. <span data-ttu-id="dd438-129">在它的位置，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="dd438-129">In its place, add the following code.</span></span>

    ```typescript
    this.user = await this.getUser();
    ```

    <span data-ttu-id="dd438-130">此新代码使用 Microsoft Graph SDK 获取用户的详细信息，然后使用 API 调用返回的值 `User` 创建对象。</span><span class="sxs-lookup"><span data-stu-id="dd438-130">This new code uses the Microsoft Graph SDK to get the user's details, then creates a `User` object using values returned by the API call.</span></span>

1. <span data-ttu-id="dd438-131">将 `constructor` 类的 更改为检查用户是否已登录，如果已登录， `AuthService` 则加载其详细信息。</span><span class="sxs-lookup"><span data-stu-id="dd438-131">Change the `constructor` for the `AuthService` class to check if the user is already logged in and load their details if so.</span></span> <span data-ttu-id="dd438-132">将 现有的 `constructor` 替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="dd438-132">Replace the existing `constructor` with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/auth.service.ts" id="ConstructorSnippet" highlight="5-7":::

1. <span data-ttu-id="dd438-133">从 类中删除临时 `HomeComponent` 代码。</span><span class="sxs-lookup"><span data-stu-id="dd438-133">Remove the temporary code from the `HomeComponent` class.</span></span> <span data-ttu-id="dd438-134">打开 **"./src/app/home/home.component.ts"，** 将现有 `signIn` 函数替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="dd438-134">Open **./src/app/home/home.component.ts** and replace the existing `signIn` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/app/home/home.component.ts" id="SignInSnippet":::

<span data-ttu-id="dd438-135">现在，如果保存更改并启动应用，登录后应最终返回主页，但 UI 应更改以指示你已登录。</span><span class="sxs-lookup"><span data-stu-id="dd438-135">Now if you save your changes and start the app, after sign-in you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

![登录后主页的屏幕截图](./images/add-aad-auth-01.png)

<span data-ttu-id="dd438-137">单击右上角的用户头像以访问 **"注销"** 链接。</span><span class="sxs-lookup"><span data-stu-id="dd438-137">Click the user avatar in the top right corner to access the **Sign Out** link.</span></span> <span data-ttu-id="dd438-138">单击 **"注销** "将重置会话，并返回到主页。</span><span class="sxs-lookup"><span data-stu-id="dd438-138">Clicking **Sign Out** resets the session and returns you to the home page.</span></span>

![具有注销链接的下拉菜单的屏幕截图](./images/add-aad-auth-02.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="dd438-140">存储和刷新令牌</span><span class="sxs-lookup"><span data-stu-id="dd438-140">Storing and refreshing tokens</span></span>

<span data-ttu-id="dd438-141">此时，应用程序具有访问令牌，该令牌在 API 调用 `Authorization` 标头中发送。</span><span class="sxs-lookup"><span data-stu-id="dd438-141">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="dd438-142">这是允许应用代表用户访问 Microsoft Graph 的令牌。</span><span class="sxs-lookup"><span data-stu-id="dd438-142">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="dd438-143">但是，此令牌期很短。</span><span class="sxs-lookup"><span data-stu-id="dd438-143">However, this token is short-lived.</span></span> <span data-ttu-id="dd438-144">令牌在颁发后一小时过期。</span><span class="sxs-lookup"><span data-stu-id="dd438-144">The token expires an hour after it is issued.</span></span> <span data-ttu-id="dd438-145">由于应用使用的是 MSAL 库，因此不需要实现任何令牌存储或刷新逻辑。</span><span class="sxs-lookup"><span data-stu-id="dd438-145">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="dd438-146">缓存 `MsalService` 浏览器存储中的令牌。</span><span class="sxs-lookup"><span data-stu-id="dd438-146">The `MsalService` caches the token in the browser storage.</span></span> <span data-ttu-id="dd438-147">`acquireTokenSilent`方法首先检查缓存的令牌，如果令牌未过期，则返回它。</span><span class="sxs-lookup"><span data-stu-id="dd438-147">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="dd438-148">如果已过期，它将进行无提示请求以获取新请求。</span><span class="sxs-lookup"><span data-stu-id="dd438-148">If it is expired, it makes a silent request to obtain a new one.</span></span>
