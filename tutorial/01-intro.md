<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="669ba-101">本教程向您介绍如何构建一个使用 Microsoft Graph 来检索用户的日历信息的角单页面应用。</span><span class="sxs-lookup"><span data-stu-id="669ba-101">This tutorial teaches you how to build an Angular single-page app that uses Microsoft Graph to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="669ba-102">如果您只想下载已完成的教程，可以下载或克隆[GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-angularspa)。</span><span class="sxs-lookup"><span data-stu-id="669ba-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-angularspa).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="669ba-103">先决条件</span><span class="sxs-lookup"><span data-stu-id="669ba-103">Prerequisites</span></span>

<span data-ttu-id="669ba-104">在开始本教程之前，您应已在开发计算机上安装了[node.js](https://nodejs.org) 。</span><span class="sxs-lookup"><span data-stu-id="669ba-104">Before you start this tutorial, you should have [Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="669ba-105">如果您没有 node.js，请访问上一个链接 "下载选项"。</span><span class="sxs-lookup"><span data-stu-id="669ba-105">If you do not have Node.js, visit the previous link for download options.</span></span>

<span data-ttu-id="669ba-106">您还应具有一个个人的 Microsoft 帐户，其中包含 Outlook.com 上的邮箱，或 Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="669ba-106">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="669ba-107">如果你没有 Microsoft 帐户，可以使用以下几种方法获取免费帐户：</span><span class="sxs-lookup"><span data-stu-id="669ba-107">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="669ba-108">你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="669ba-108">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="669ba-109">你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="669ba-109">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="669ba-110">本教程是使用节点版本12.16.1 编写的。</span><span class="sxs-lookup"><span data-stu-id="669ba-110">This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="669ba-111">本指南中的步骤可能适用于其他版本，但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="669ba-111">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="watch-the-tutorial"></a><span data-ttu-id="669ba-112">观看教程</span><span class="sxs-lookup"><span data-stu-id="669ba-112">Watch the tutorial</span></span>

<span data-ttu-id="669ba-113">此模块已记录，在 Office 开发 YouTube 频道中可用。</span><span class="sxs-lookup"><span data-stu-id="669ba-113">This module has been recorded and is available in the Office Development YouTube channel.</span></span>

<!-- markdownlint-disable MD033 MD034 -->
<br/>

> [!VIDEO https://www.youtube-nocookie.com/embed/KUPRTTOUzz8]
<!-- markdownlint-enable MD033 MD034 -->

## <a name="feedback"></a><span data-ttu-id="669ba-114">反馈</span><span class="sxs-lookup"><span data-stu-id="669ba-114">Feedback</span></span>

<span data-ttu-id="669ba-115">请在[GitHub 存储库](https://github.com/microsoftgraph/msgraph-training-angularspa)中提供有关本教程的任何反馈。</span><span class="sxs-lookup"><span data-stu-id="669ba-115">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-angularspa).</span></span>
