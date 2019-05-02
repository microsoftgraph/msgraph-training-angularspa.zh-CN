# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="21e6d-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="21e6d-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21e6d-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="21e6d-102">Prerequisites</span></span>

<span data-ttu-id="21e6d-103">若要在此文件夹中运行已完成的项目, 您需要以下各项:</span><span class="sxs-lookup"><span data-stu-id="21e6d-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="21e6d-104">在开发计算机上安装了[node.js](https://nodejs.org) 。</span><span class="sxs-lookup"><span data-stu-id="21e6d-104">[Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="21e6d-105">如果您没有 node.js, 请访问上一个链接 "下载选项"。</span><span class="sxs-lookup"><span data-stu-id="21e6d-105">If you do not have Node.js, visit the previous link for download options.</span></span> <span data-ttu-id="21e6d-106">(**注意:** 本教程是使用节点版本10.7.0 编写的。</span><span class="sxs-lookup"><span data-stu-id="21e6d-106">(**Note:** This tutorial was written with Node version 10.7.0.</span></span> <span data-ttu-id="21e6d-107">本指南中的步骤可能适用于其他版本, 但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="21e6d-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="21e6d-108">在开发计算机上安装了[角度 CLI](https://cli.angular.io/) 。</span><span class="sxs-lookup"><span data-stu-id="21e6d-108">[Angular CLI](https://cli.angular.io/) installed on your development machine.</span></span>
- <span data-ttu-id="21e6d-109">使用 Outlook.com 上的邮箱的个人 Microsoft 帐户, 或者是 Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="21e6d-109">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="21e6d-110">如果你没有 Microsoft 帐户, 可以使用以下几种方法获取免费帐户:</span><span class="sxs-lookup"><span data-stu-id="21e6d-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="21e6d-111">你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="21e6d-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="21e6d-112">你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="21e6d-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="21e6d-113">向 Azure Active Directory 管理中心注册 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="21e6d-113">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="21e6d-114">打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="21e6d-114">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="21e6d-115">使用**个人帐户**（亦称为“Microsoft 帐户”）或**工作或学校帐户**登录。</span><span class="sxs-lookup"><span data-stu-id="21e6d-115">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="21e6d-116">在左侧导航栏中选择 " **Azure Active Directory** ", 然后选择 "**管理**" 下的 "**应用程序注册**"。</span><span class="sxs-lookup"><span data-stu-id="21e6d-116">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="21e6d-117">应用注册的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="21e6d-117">A screenshot of the App registrations</span></span> ](/tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="21e6d-118">选择“新注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="21e6d-118">Select **New registration**.</span></span> <span data-ttu-id="21e6d-119">在“注册应用”\*\*\*\* 页上，按如下方式设置值。</span><span class="sxs-lookup"><span data-stu-id="21e6d-119">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="21e6d-120">将“名称”\*\*\*\* 设置为“`Angular Graph Tutorial`”。</span><span class="sxs-lookup"><span data-stu-id="21e6d-120">Set **Name** to `Angular Graph Tutorial`.</span></span>
    - <span data-ttu-id="21e6d-121">将“受支持的帐户类型”\*\*\*\* 设置为“任何组织目录中的帐户和个人 Microsoft 帐户”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="21e6d-121">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="21e6d-122">在“重定向 URI”\*\*\*\* 下，将第一个下拉列表设置为“`Web`”，并将值设置为“`http://localhost:4200`”。</span><span class="sxs-lookup"><span data-stu-id="21e6d-122">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `http://localhost:4200`.</span></span>

    !["注册应用程序" 页的屏幕截图](/tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="21e6d-124">选择“注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="21e6d-124">Choose **Register**.</span></span> <span data-ttu-id="21e6d-125">在 "**角度图" 教程**页上, 复制**应用程序 (客户端) ID**的值并保存它, 下一步将需要它。</span><span class="sxs-lookup"><span data-stu-id="21e6d-125">On the **Angular Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新应用注册的应用程序 ID 的屏幕截图](/tutorial/images/aad-application-id.png)

1. <span data-ttu-id="21e6d-127">选择“管理”\*\*\*\* 下的“身份验证”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="21e6d-127">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="21e6d-128">找到 "**隐式授予**" 部分并启用**访问令牌**和**ID 令牌**。</span><span class="sxs-lookup"><span data-stu-id="21e6d-128">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="21e6d-129">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="21e6d-129">Choose **Save**.</span></span>

    ![隐式 grant 部分的屏幕截图](/tutorial/images/aad-implicit-grant.png)

## <a name="configure-the-sample"></a><span data-ttu-id="21e6d-131">配置示例</span><span class="sxs-lookup"><span data-stu-id="21e6d-131">Configure the sample</span></span>

1. <span data-ttu-id="21e6d-132">将`oauth.ts.example`文件重命名`oauth.ts`为。</span><span class="sxs-lookup"><span data-stu-id="21e6d-132">Rename the `oauth.ts.example` file to `oauth.ts`.</span></span>
1. <span data-ttu-id="21e6d-133">编辑`oauth.ts`文件并进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="21e6d-133">Edit the `oauth.ts` file and make the following changes.</span></span>
    1. <span data-ttu-id="21e6d-134">将`YOUR_APP_ID_HERE`替换为你从应用注册门户获取的**应用程序 Id** 。</span><span class="sxs-lookup"><span data-stu-id="21e6d-134">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="21e6d-135">在命令行界面 (CLI) 中, 导航到此目录并运行以下命令以安装要求。</span><span class="sxs-lookup"><span data-stu-id="21e6d-135">In your command-line interface (CLI), navigate to this directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="21e6d-136">运行示例</span><span class="sxs-lookup"><span data-stu-id="21e6d-136">Run the sample</span></span>

1. <span data-ttu-id="21e6d-137">在 CLI 中运行以下命令以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="21e6d-137">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    ng serve
    ```

1. <span data-ttu-id="21e6d-138">打开浏览器，然后转到 `http://localhost:4200`。</span><span class="sxs-lookup"><span data-stu-id="21e6d-138">Open a browser and browse to `http://localhost:4200`.</span></span>