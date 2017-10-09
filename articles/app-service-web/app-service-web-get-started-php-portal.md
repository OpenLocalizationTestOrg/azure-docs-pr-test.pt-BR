---
title: aaaDeploy um aplicativo de WordPress no hello portal do Azure em cinco minutos | Microsoft Docs
description: "Saiba como é fácil toorun os aplicativos web no serviço de aplicativo ao implantar um aplicativo de WordPress. Veja os resultados imediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="e3df9-104">Implantar um aplicativo de WordPress no portal do Azure de saudação em cinco minutos</span><span class="sxs-lookup"><span data-stu-id="e3df9-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="e3df9-105">Este tutorial mostra como toodeploy seu primeiro [WordPress](https://wordpress.org/) muito de aplicativo da web[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) em minutos.</span><span class="sxs-lookup"><span data-stu-id="e3df9-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Site do WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="e3df9-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3df9-107">Prerequisites</span></span>
<span data-ttu-id="e3df9-108">Você precisa de uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e3df9-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="e3df9-109">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e3df9-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="e3df9-110">Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3df9-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="e3df9-111">Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.</span><span class="sxs-lookup"><span data-stu-id="e3df9-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="e3df9-112">Implantar o aplicativo de WordPress Olá</span><span class="sxs-lookup"><span data-stu-id="e3df9-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="e3df9-113">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3df9-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e3df9-114">Abra [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="e3df9-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="e3df9-115">O link é um atalho tooimmediately configurar um novo aplicativo de WordPress Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3df9-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="e3df9-116">Em **Nome do aplicativo**, digite um nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e3df9-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="e3df9-117">Você verá uma marca de seleção verde na caixa Olá se nome hello é exclusivo no hello `azurewebsites.net` domínio.</span><span class="sxs-lookup"><span data-stu-id="e3df9-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="e3df9-118">Em **grupo de recursos**, clique em **criar novo** toocreate um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), dê a ele um nome.</span><span class="sxs-lookup"><span data-stu-id="e3df9-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="e3df9-119">Em **Provedor de Banco de Dados**, selecione **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="e3df9-120">Clique em **Plano do Serviço de Aplicativo/Local** > **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="e3df9-121">Configurar Olá [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="e3df9-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="e3df9-122">Em **plano de serviço de aplicativo**, o nome do tipo hello desejado.</span><span class="sxs-lookup"><span data-stu-id="e3df9-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="e3df9-123">Em **local**, escolha um local toohost seu plano.</span><span class="sxs-lookup"><span data-stu-id="e3df9-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="e3df9-124">Clique em **Tipo de preço** e selecione **F1 Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="e3df9-125">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-125">Click **OK**.</span></span>

8. <span data-ttu-id="e3df9-126">Clique em **Banco de Dados** > **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="e3df9-127">Configure Olá banco de dados SQL, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="e3df9-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="e3df9-128">Em **Nome do Banco de Dados**, digite um nome de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e3df9-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="e3df9-129">Em **local**, escolha Olá mesmo local que Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3df9-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="e3df9-130">Clique em **Tipo de preço** e selecione **Mercúrio** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="e3df9-131">Clique em **Termos Legais** e clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="e3df9-132">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-132">Click **OK**.</span></span>

9. <span data-ttu-id="e3df9-133">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-133">Click **Create**.</span></span>

    <span data-ttu-id="e3df9-134">Agora o Azure cria seu aplicativo do WordPress com base em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="e3df9-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="e3df9-135">Você deve ver uma notificação **Implantação iniciada...**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-135">You should see a **Deployment started...** notification.</span></span>

    ![Implantação iniciada – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="e3df9-137">Inicie e gerencie seu aplicativo Web do WordPress</span><span class="sxs-lookup"><span data-stu-id="e3df9-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="e3df9-138">Quando o Azure concluir a implantação do aplicativo você verá outra notificação.</span><span class="sxs-lookup"><span data-stu-id="e3df9-138">When Azure completes app deployment you see another notification.</span></span>

![Implantação bem-sucedida – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="e3df9-140">Clique em notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3df9-140">Click hello notification.</span></span> <span data-ttu-id="e3df9-141">Se perdidas, você sempre pode acessá-lo clicando sino de notificação de saudação (![abaixo de notificação - WordPress primeiro no serviço de aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="e3df9-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="e3df9-142">Agora você deve ver a [folha](../azure-resource-manager/resource-group-portal.md#manage-resources) de gerenciamento de seu aplicativo Web (*folha*: uma página de portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="e3df9-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="e3df9-143">Na parte superior de saudação da página de visão geral de saudação, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="e3df9-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Procurar – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="e3df9-145">Agora você vê Olá WordPress **bem-vindo** página.</span><span class="sxs-lookup"><span data-stu-id="e3df9-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="e3df9-146">Configurar a instalação do WordPress hello e iniciar a reprodução com ele!</span><span class="sxs-lookup"><span data-stu-id="e3df9-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Configuração do WordPress – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="e3df9-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3df9-148">Next steps</span></span>
* <span data-ttu-id="e3df9-149">[Criar, configurar e implantar um tooAzure de aplicativo web Laravel](app-service-web-php-get-started.md) -aprender as habilidades básicas Olá você precisa toorun qualquer aplicativo da web PHP no Azure, como:</span><span class="sxs-lookup"><span data-stu-id="e3df9-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="e3df9-150">Criar e configurar aplicativos no Azure do PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="e3df9-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="e3df9-151">Definir a versão do PHP.</span><span class="sxs-lookup"><span data-stu-id="e3df9-151">Set PHP version.</span></span>
    * <span data-ttu-id="e3df9-152">Use um arquivo de início que não está no diretório de aplicativo hello raiz.</span><span class="sxs-lookup"><span data-stu-id="e3df9-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="e3df9-153">Habilite a automação do Composer.</span><span class="sxs-lookup"><span data-stu-id="e3df9-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="e3df9-154">Acessar variáveis de ambiente específicas.</span><span class="sxs-lookup"><span data-stu-id="e3df9-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="e3df9-155">Solucionar erros comuns.</span><span class="sxs-lookup"><span data-stu-id="e3df9-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="e3df9-156">[Implantar seu código tooAzure do serviço de aplicativo](web-sites-deploy.md)-Saiba como toodeploy do FTP ou da origem controlar repositórios.</span><span class="sxs-lookup"><span data-stu-id="e3df9-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="e3df9-157">[Adicionar funcionalidade tooyour primeiro aplicativo web](app-service-web-get-started-2.md) -leve toohello seu aplicativo do Azure próximo nível.</span><span class="sxs-lookup"><span data-stu-id="e3df9-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="e3df9-158">Autenticar os usuários.</span><span class="sxs-lookup"><span data-stu-id="e3df9-158">Authenticate your users.</span></span> <span data-ttu-id="e3df9-159">Dimensione-o com base na demanda.</span><span class="sxs-lookup"><span data-stu-id="e3df9-159">Scale it based on demand.</span></span> <span data-ttu-id="e3df9-160">Configure alguns alertas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e3df9-160">Set up some performance alerts.</span></span> <span data-ttu-id="e3df9-161">Tudo isso com apenas alguns cliques.</span><span class="sxs-lookup"><span data-stu-id="e3df9-161">All with a few clicks.</span></span>
