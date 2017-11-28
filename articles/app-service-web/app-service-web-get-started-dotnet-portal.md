---
title: "aaaDeploy um aplicativo web de Umbraco Olá portal do Azure em cinco minutos | Microsoft Docs"
description: "Saiba como é fácil toorun os aplicativos web no serviço de aplicativo ao implantar um aplicativo ASP.NET de exemplo. Veja os resultados imediatamente."
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
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="cc9af-104">Implantar um aplicativo web de Umbraco Olá portal do Azure em cinco minutos</span><span class="sxs-lookup"><span data-stu-id="cc9af-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="cc9af-105">Esse tutorial ajudará você a implantar n [Umbraco](https://our.umbraco.org/) muito de aplicativo da web[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) em minutos.</span><span class="sxs-lookup"><span data-stu-id="cc9af-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Aplicativo do Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="cc9af-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cc9af-107">Prerequisites</span></span>
<span data-ttu-id="cc9af-108">Você precisa de uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9af-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="cc9af-109">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="cc9af-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="cc9af-110">Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9af-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="cc9af-111">Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.</span><span class="sxs-lookup"><span data-stu-id="cc9af-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="cc9af-112">Implantar o aplicativo de saudação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="cc9af-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="cc9af-113">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc9af-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="cc9af-114">Abra [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="cc9af-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="cc9af-115">O link é um atalho tooimmediately configurar um novo aplicativo Umbraco Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc9af-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="cc9af-116">Em **Nome do aplicativo**, digite um nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="cc9af-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="cc9af-117">Você verá uma marca de seleção verde na caixa Olá se nome hello é exclusivo no hello `azurewebsites.net` domínio.</span><span class="sxs-lookup"><span data-stu-id="cc9af-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="cc9af-118">Em **grupo de recursos**, clique em **criar novo** toocreate um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), dê a ele um nome.</span><span class="sxs-lookup"><span data-stu-id="cc9af-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="cc9af-119">Clique em **Plano do Serviço de Aplicativo/Local** > **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="cc9af-120">Configurar Olá [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="cc9af-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="cc9af-121">Em **plano de serviço de aplicativo**, o nome do tipo hello desejado.</span><span class="sxs-lookup"><span data-stu-id="cc9af-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="cc9af-122">Em **local**, escolha um local toohost seu plano.</span><span class="sxs-lookup"><span data-stu-id="cc9af-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="cc9af-123">Clique em **Tipo de preço** e selecione **F1 Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="cc9af-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-124">Click **OK**.</span></span>

    <span data-ttu-id="cc9af-125">Sua configuração Umbraco CMS deve agora ser semelhante Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc9af-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuração em andamento – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="cc9af-127">Clique em **Banco de Dados SQL** > **Criar um novo banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="cc9af-128">Configure Olá banco de dados SQL, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="cc9af-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="cc9af-129">Em **Nome**, digite um nome, como **myDB**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="cc9af-130">Clique em **Tipo de preço** e selecione **F Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="cc9af-131">Clique em **Servidor de destino** > **Criar um novo servidor**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="cc9af-132">Configure o servidor de banco de dados de saudação conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="cc9af-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="cc9af-133">Em **Nome do servidor**, digite um nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="cc9af-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="cc9af-134">Você verá uma marca de seleção verde na caixa Olá se nome hello é exclusivo no hello `.database.windows.net` domínio.</span><span class="sxs-lookup"><span data-stu-id="cc9af-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="cc9af-135">Em **logon de administrador de servidor**, Olá tipo desejado de nome de usuário administrador.</span><span class="sxs-lookup"><span data-stu-id="cc9af-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="cc9af-136">Em **senha** e **Confirmar senha**, digite a senha desejada hello.</span><span class="sxs-lookup"><span data-stu-id="cc9af-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="cc9af-137">No local, selecione Olá mesmo local que você pode usar para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc9af-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="cc9af-138">Certifique-se de **permitir servidor de tooaccess de serviços do azure** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="cc9af-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="cc9af-139">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="cc9af-140">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-140">Click **Select**.</span></span>

13. <span data-ttu-id="cc9af-141">Clique em **configurações de aplicativo da Web**, especificar o nome de usuário de banco de dados de saudação e a senha e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="cc9af-142">Sua configuração Umbraco CMS deve agora ser semelhante Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc9af-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuração concluída – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="cc9af-144">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-144">Click **Create**.</span></span>
    
    <span data-ttu-id="cc9af-145">Agora o Azure cria seu aplicativo do Umbraco com base em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="cc9af-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="cc9af-146">Você deve ver uma notificação **Implantação iniciada...**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-146">You should see a **Deployment started...** notification.</span></span>

    ![Implantação bem-sucedida – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="cc9af-148">Iniciar e gerenciar seu aplicativo Web Umbraco</span><span class="sxs-lookup"><span data-stu-id="cc9af-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="cc9af-149">Quando o Azure concluir a implantação do aplicativo você verá outra notificação.</span><span class="sxs-lookup"><span data-stu-id="cc9af-149">When Azure completes app deployment you see another notification.</span></span>

![Implantação bem-sucedida – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="cc9af-151">Clique em notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc9af-151">Click hello notification.</span></span> <span data-ttu-id="cc9af-152">Se perdidas, você sempre pode acessá-lo clicando sino de notificação de saudação (![abaixo de notificação - Umbraco primeiro no serviço de aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="cc9af-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="cc9af-153">Agora você deve ver a [folha](../azure-resource-manager/resource-group-portal.md#manage-resources) de gerenciamento de seu aplicativo Web (*folha*: uma página de portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="cc9af-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="cc9af-154">Na parte superior de saudação da página de visão geral de saudação, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="cc9af-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Procurar – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="cc9af-156">Agora você vê Olá Umbraco **bem-vindo** página.</span><span class="sxs-lookup"><span data-stu-id="cc9af-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="cc9af-157">Configurar Olá Umbraco instalação e iniciar a reprodução com ele!</span><span class="sxs-lookup"><span data-stu-id="cc9af-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Configuração do Umbraco – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="cc9af-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc9af-159">Next steps</span></span>
* <span data-ttu-id="cc9af-160">[Implantar um tooAzure de aplicativo web do ASP.NET do serviço de aplicativo, usando o Visual Studio](app-service-web-get-started-dotnet.md) -Saiba como toocreate um novo aplicativo web do Azure no Visual Studio, usando qualquer um dos Olá incluído modelos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc9af-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="cc9af-161">[Implantar seu código tooAzure do serviço de aplicativo](web-sites-deploy.md)-Saiba como toodeploy do FTP ou da origem controlar repositórios.</span><span class="sxs-lookup"><span data-stu-id="cc9af-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="cc9af-162">[Adicionar funcionalidade tooyour primeiro aplicativo web](app-service-web-get-started-2.md) -leve toohello seu aplicativo do Azure próximo nível.</span><span class="sxs-lookup"><span data-stu-id="cc9af-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="cc9af-163">Autenticar os usuários.</span><span class="sxs-lookup"><span data-stu-id="cc9af-163">Authenticate your users.</span></span> <span data-ttu-id="cc9af-164">Dimensione-o com base na demanda.</span><span class="sxs-lookup"><span data-stu-id="cc9af-164">Scale it based on demand.</span></span> <span data-ttu-id="cc9af-165">Configure alguns alertas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="cc9af-165">Set up some performance alerts.</span></span> <span data-ttu-id="cc9af-166">Tudo isso com apenas alguns cliques.</span><span class="sxs-lookup"><span data-stu-id="cc9af-166">All with a few clicks.</span></span>
