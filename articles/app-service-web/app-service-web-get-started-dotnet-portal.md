---
title: Implantar um aplicativo Web do Umbraco no Portal do Azure em cinco minutos | Microsoft Docs
description: "Saiba como é fácil executar os aplicativos Web no Serviço de Aplicativo implantando um aplicativo ASP.NET de exemplo. Veja os resultados imediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="2134f-104">Implantar um aplicativo Web do Umbraco no Portal do Azure em cinco minutos</span><span class="sxs-lookup"><span data-stu-id="2134f-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="2134f-105">Este tutorial ajuda você a implantar um aplicativo Web do [Umbraco](https://our.umbraco.org/) no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) em alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2134f-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Aplicativo do Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="2134f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2134f-107">Prerequisites</span></span>
<span data-ttu-id="2134f-108">Você precisa de uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2134f-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="2134f-109">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="2134f-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="2134f-110">Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2134f-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="2134f-111">Crie um aplicativo inicial e brinque com ele por até uma hora: não é necessário cartão de crédito ou compromissos.</span><span class="sxs-lookup"><span data-stu-id="2134f-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="2134f-112">Implantar o aplicativo ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2134f-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="2134f-113">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2134f-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2134f-114">Abra [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="2134f-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="2134f-115">Esse link é um atalho para configurar imediatamente um novo aplicativo do Umbraco no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2134f-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="2134f-116">Em **Nome do aplicativo**, digite um nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2134f-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="2134f-117">Você verá uma marca de seleção verde na caixa se o nome for exclusivo no domínio `azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="2134f-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="2134f-118">Em **Grupo de Recursos**, clique em **Criar novo** para criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) e, em seguida, atribua um nome a ele.</span><span class="sxs-lookup"><span data-stu-id="2134f-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="2134f-119">Clique em **Plano do Serviço de Aplicativo/Local** > **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="2134f-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="2134f-120">Configure o [Plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="2134f-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="2134f-121">Em **Plano do Serviço de Aplicativo**, digite o nome desejado.</span><span class="sxs-lookup"><span data-stu-id="2134f-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="2134f-122">Em **Local**, escolha um local para hospedar seu plano.</span><span class="sxs-lookup"><span data-stu-id="2134f-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="2134f-123">Clique em **Tipo de preço** e selecione **F1 Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="2134f-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="2134f-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2134f-124">Click **OK**.</span></span>

    <span data-ttu-id="2134f-125">A configuração do CMS do Umbraco agora deve ser semelhante a seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="2134f-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuração em andamento – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="2134f-127">Clique em **Banco de Dados SQL** > **Criar um novo banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="2134f-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="2134f-128">Configure o Banco de Dados SQL, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="2134f-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="2134f-129">Em **Nome**, digite um nome, como **myDB**.</span><span class="sxs-lookup"><span data-stu-id="2134f-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="2134f-130">Clique em **Tipo de preço** e selecione **F Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="2134f-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="2134f-131">Clique em **Servidor de destino** > **Criar um novo servidor**.</span><span class="sxs-lookup"><span data-stu-id="2134f-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="2134f-132">Configure o servidor de banco de dados conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="2134f-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="2134f-133">Em **Nome do servidor**, digite um nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="2134f-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="2134f-134">Você verá uma marca de seleção verde na caixa se o nome for exclusivo no domínio `.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="2134f-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="2134f-135">Em **Logon de administrador do servidor**, digite o nome de usuário administrador desejado.</span><span class="sxs-lookup"><span data-stu-id="2134f-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="2134f-136">Em **Senha** e **Confirmar senha**, digite a senha desejada.</span><span class="sxs-lookup"><span data-stu-id="2134f-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="2134f-137">Em Local, selecione o mesmo local que você usar para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2134f-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="2134f-138">Verifique se **Permitir que os serviços do Azure acessem o servidor** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="2134f-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="2134f-139">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="2134f-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="2134f-140">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="2134f-140">Click **Select**.</span></span>

13. <span data-ttu-id="2134f-141">Clique em **Configurações do aplicativo Web**, especifique o nome de usuário e a senha do banco de dados e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2134f-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="2134f-142">A configuração do CMS do Umbraco agora deve ser semelhante a seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="2134f-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuração concluída – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="2134f-144">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2134f-144">Click **Create**.</span></span>
    
    <span data-ttu-id="2134f-145">Agora o Azure cria seu aplicativo do Umbraco com base em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="2134f-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="2134f-146">Você deve ver uma notificação **Implantação iniciada...**.</span><span class="sxs-lookup"><span data-stu-id="2134f-146">You should see a **Deployment started...** notification.</span></span>

    ![Implantação bem-sucedida – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="2134f-148">Iniciar e gerenciar seu aplicativo Web Umbraco</span><span class="sxs-lookup"><span data-stu-id="2134f-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="2134f-149">Quando o Azure concluir a implantação do aplicativo você verá outra notificação.</span><span class="sxs-lookup"><span data-stu-id="2134f-149">When Azure completes app deployment you see another notification.</span></span>

![Implantação bem-sucedida – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="2134f-151">Clique na notificação.</span><span class="sxs-lookup"><span data-stu-id="2134f-151">Click the notification.</span></span> <span data-ttu-id="2134f-152">Se você não viu a notificação, poderá sempre acessá-la clicando no sino de notificação (![Sino de notificação – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="2134f-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="2134f-153">Agora você deve ver a [folha](../azure-resource-manager/resource-group-portal.md#manage-resources) de gerenciamento de seu aplicativo Web (*folha*: uma página de portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="2134f-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="2134f-154">Na parte superior da página de Visão geral, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="2134f-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Procurar – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="2134f-156">Agora você vê a página **Inicial** do Umbraco.</span><span class="sxs-lookup"><span data-stu-id="2134f-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="2134f-157">Configure a instalação do Umbraco e comece a brincar com ele!</span><span class="sxs-lookup"><span data-stu-id="2134f-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Configuração do Umbraco – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="2134f-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2134f-159">Next steps</span></span>
* <span data-ttu-id="2134f-160">[Implantar um aplicativo Web ASP.NET no Serviço de Aplicativo do Azure usando o Visual Studio](app-service-web-get-started-dotnet.md) – Aprenda a criar um novo aplicativo Web do Azure no Visual Studio, usando qualquer um dos modelos de aplicativos incluídos.</span><span class="sxs-lookup"><span data-stu-id="2134f-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="2134f-161">[Implantar seu código no Serviço de Aplicativo do Azure](web-sites-deploy.md) – Aprenda como implantar do FTP ou de repositórios de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="2134f-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="2134f-162">[Adicionar funcionalidade ao seu primeiro aplicativo Web](app-service-web-get-started-2.md) – Leve seu aplicativo do Azure para o próximo patamar.</span><span class="sxs-lookup"><span data-stu-id="2134f-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="2134f-163">Autenticar os usuários.</span><span class="sxs-lookup"><span data-stu-id="2134f-163">Authenticate your users.</span></span> <span data-ttu-id="2134f-164">Dimensione-o com base na demanda.</span><span class="sxs-lookup"><span data-stu-id="2134f-164">Scale it based on demand.</span></span> <span data-ttu-id="2134f-165">Configure alguns alertas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="2134f-165">Set up some performance alerts.</span></span> <span data-ttu-id="2134f-166">Tudo isso com apenas alguns cliques.</span><span class="sxs-lookup"><span data-stu-id="2134f-166">All with a few clicks.</span></span>
