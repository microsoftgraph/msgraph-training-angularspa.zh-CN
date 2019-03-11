# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="bba1f-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="bba1f-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bba1f-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="bba1f-102">Prerequisites</span></span>

<span data-ttu-id="bba1f-103">若要在此文件夹中运行已完成的项目, 您需要以下各项:</span><span class="sxs-lookup"><span data-stu-id="bba1f-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="bba1f-104">在开发计算机上安装了[node.js](https://nodejs.org) 。</span><span class="sxs-lookup"><span data-stu-id="bba1f-104">[Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="bba1f-105">如果您没有 node.js, 请访问上一个链接 "下载选项"。</span><span class="sxs-lookup"><span data-stu-id="bba1f-105">If you do not have Node.js, visit the previous link for download options.</span></span> <span data-ttu-id="bba1f-106">(**注意:** 本教程是使用节点版本10.7.0 编写的。</span><span class="sxs-lookup"><span data-stu-id="bba1f-106">(**Note:** This tutorial was written with Node version 10.7.0.</span></span> <span data-ttu-id="bba1f-107">本指南中的步骤可能适用于其他版本, 但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="bba1f-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="bba1f-108">在开发计算机上安装了[角度 CLI](https://cli.angular.io/) 。</span><span class="sxs-lookup"><span data-stu-id="bba1f-108">[Angular CLI](https://cli.angular.io/) installed on your development machine.</span></span>
- <span data-ttu-id="bba1f-109">使用 Outlook.com 上的邮箱的个人 Microsoft 帐户, 或者是 microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="bba1f-109">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="bba1f-110">如果你没有 Microsoft 帐户, 可以使用以下几种方法获取免费帐户:</span><span class="sxs-lookup"><span data-stu-id="bba1f-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="bba1f-111">你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="bba1f-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="bba1f-112">你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="bba1f-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-application-registration-portal"></a><span data-ttu-id="bba1f-113">在应用程序注册门户中注册 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="bba1f-113">Register a web application with the Application Registration Portal</span></span>

1. <span data-ttu-id="bba1f-114">打开浏览器并导航到[应用程序注册门户](https://apps.dev.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="bba1f-114">Open a browser and navigate to the [Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="bba1f-115">使用**个人帐户**(亦称: Microsoft 帐户) 或**工作或学校帐户**登录。</span><span class="sxs-lookup"><span data-stu-id="bba1f-115">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="bba1f-116">选择页面顶部的 "**添加应用**"。</span><span class="sxs-lookup"><span data-stu-id="bba1f-116">Select **Add an app** at the top of the page.</span></span>

    > <span data-ttu-id="bba1f-117">**注意:** 如果在页面上看到多个 "**添加应用程序**" 按钮, 请选择与 "**聚合应用程序**" 列表对应的项。</span><span class="sxs-lookup"><span data-stu-id="bba1f-117">**Note:** If you see more than one **Add an app** button on the page, select the one that corresponds to the **Converged apps** list.</span></span>

1. <span data-ttu-id="bba1f-118">在 "**注册应用程序**" 页上, 将**应用程序名称**设置为 "**角度图" 教程**, 然后选择 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="bba1f-118">On the **Register your application** page, set the **Application Name** to **Angular Graph Tutorial** and select **Create**.</span></span>

    ![在应用注册门户网站中创建新应用程序的屏幕截图](/tutorial/images/arp-create-app-01.png)

1. <span data-ttu-id="bba1f-120">在 "**角度图教程注册**" 页上的 "**属性**" 部分下, 复制**应用程序 Id** , 因为稍后将需要它。</span><span class="sxs-lookup"><span data-stu-id="bba1f-120">On the **Angular Graph Tutorial Registration** page, under the **Properties** section, copy the **Application Id** as you will need it later.</span></span>

    ![新创建的应用程序 ID 的屏幕截图](/tutorial/images/arp-create-app-02.png)

1. <span data-ttu-id="bba1f-122">向下滚动到 "**平台**" 部分。</span><span class="sxs-lookup"><span data-stu-id="bba1f-122">Scroll down to the **Platforms** section.</span></span>

    1. <span data-ttu-id="bba1f-123">选择 "**添加平台**"。</span><span class="sxs-lookup"><span data-stu-id="bba1f-123">Select **Add Platform**.</span></span>
    1. <span data-ttu-id="bba1f-124">在 "**添加平台**" 对话框中, 选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="bba1f-124">In the **Add Platform** dialog, select **Web**.</span></span>

        ![为应用程序创建平台的屏幕截图](/tutorial/images/arp-create-app-03.png)

    1. <span data-ttu-id="bba1f-126">在 " **Web**平台" 框中, 输入`http://localhost:4200` **重定向 url**的 url。</span><span class="sxs-lookup"><span data-stu-id="bba1f-126">In the **Web** platform box, enter the URL `http://localhost:4200` for the **Redirect URLs**.</span></span>

        ![应用程序新添加的 Web 平台的屏幕截图](/tutorial/images/arp-create-app-04.png)

1. <span data-ttu-id="bba1f-128">滚动到页面底部, 然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="bba1f-128">Scroll to the bottom of the page and select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="bba1f-129">配置示例</span><span class="sxs-lookup"><span data-stu-id="bba1f-129">Configure the sample</span></span>

1. <span data-ttu-id="bba1f-130">将`oauth.ts.example`文件重命名`oauth.ts`为。</span><span class="sxs-lookup"><span data-stu-id="bba1f-130">Rename the `oauth.ts.example` file to `oauth.ts`.</span></span>
1. <span data-ttu-id="bba1f-131">编辑`oauth.ts`文件并进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="bba1f-131">Edit the `oauth.ts` file and make the following changes.</span></span>
    1. <span data-ttu-id="bba1f-132">将`YOUR_APP_ID_HERE`替换为你从应用注册门户获取的**应用程序 Id** 。</span><span class="sxs-lookup"><span data-stu-id="bba1f-132">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="bba1f-133">在命令行界面 (CLI) 中, 导航到此目录并运行以下命令以安装要求。</span><span class="sxs-lookup"><span data-stu-id="bba1f-133">In your command-line interface (CLI), navigate to this directory and run the following command to install requirements.</span></span>

    ```Shell
    npm install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="bba1f-134">运行示例</span><span class="sxs-lookup"><span data-stu-id="bba1f-134">Run the sample</span></span>

1. <span data-ttu-id="bba1f-135">在 CLI 中运行以下命令以启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="bba1f-135">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    ng serve
    ```

1. <span data-ttu-id="bba1f-136">打开浏览器，然后转到 `http://localhost:4200`。</span><span class="sxs-lookup"><span data-stu-id="bba1f-136">Open a browser and browse to `http://localhost:4200`.</span></span>