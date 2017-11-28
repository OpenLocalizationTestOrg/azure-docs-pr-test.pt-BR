---
title: Implantar um aplicativo do WordPress no Portal do Azure em cinco minutos | Microsoft Docs
description: "Saiba como é fácil executar aplicativos Web no Serviço de Aplicativo implantando um aplicativo do WordPress. Veja os resultados imediatamente."
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
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="b23c1-104">Implantar um aplicativo do WordPress no Portal do Azure em cinco minutos</span><span class="sxs-lookup"><span data-stu-id="b23c1-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="b23c1-105">Este tutorial mostra como implantar seu primeiro aplicativo Web do [WordPress](https://wordpress.org/) no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) em minutos.</span><span class="sxs-lookup"><span data-stu-id="b23c1-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Site do WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="b23c1-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b23c1-107">Prerequisites</span></span>
<span data-ttu-id="b23c1-108">Você precisa de uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b23c1-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="b23c1-109">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b23c1-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="b23c1-110">Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="b23c1-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="b23c1-111">Crie um aplicativo inicial e brinque com ele por até uma hora: não é necessário cartão de crédito ou compromissos.</span><span class="sxs-lookup"><span data-stu-id="b23c1-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="b23c1-112">Implantar o aplicativo do WordPress</span><span class="sxs-lookup"><span data-stu-id="b23c1-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="b23c1-113">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b23c1-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b23c1-114">Abra [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="b23c1-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="b23c1-115">Esse link é um atalho para configurar imediatamente um novo aplicativo do WordPress no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b23c1-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="b23c1-116">Em **Nome do aplicativo**, digite um nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b23c1-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="b23c1-117">Você verá uma marca de seleção verde na caixa se o nome for exclusivo no domínio `azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b23c1-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="b23c1-118">Em **Grupo de Recursos**, clique em **Criar novo** para criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) e, em seguida, atribua um nome a ele.</span><span class="sxs-lookup"><span data-stu-id="b23c1-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="b23c1-119">Em **Provedor de Banco de Dados**, selecione **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="b23c1-120">Clique em **Plano do Serviço de Aplicativo/Local** > **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="b23c1-121">Configure o [Plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="b23c1-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="b23c1-122">Em **Plano do Serviço de Aplicativo**, digite o nome desejado.</span><span class="sxs-lookup"><span data-stu-id="b23c1-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="b23c1-123">Em **Local**, escolha um local para hospedar seu plano.</span><span class="sxs-lookup"><span data-stu-id="b23c1-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="b23c1-124">Clique em **Tipo de preço** e selecione **F1 Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="b23c1-125">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-125">Click **OK**.</span></span>

8. <span data-ttu-id="b23c1-126">Clique em **Banco de Dados** > **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="b23c1-127">Configure o Banco de Dados SQL, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="b23c1-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="b23c1-128">Em **Nome do Banco de Dados**, digite um nome de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b23c1-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="b23c1-129">Em **Local**, escolha o mesmo local do Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b23c1-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="b23c1-130">Clique em **Tipo de preço** e selecione **Mercúrio** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="b23c1-131">Clique em **Termos Legais** e clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="b23c1-132">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-132">Click **OK**.</span></span>

9. <span data-ttu-id="b23c1-133">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-133">Click **Create**.</span></span>

    <span data-ttu-id="b23c1-134">Agora o Azure cria seu aplicativo do WordPress com base em sua configuração.</span><span class="sxs-lookup"><span data-stu-id="b23c1-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="b23c1-135">Você deve ver uma notificação **Implantação iniciada...**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-135">You should see a **Deployment started...** notification.</span></span>

    ![Implantação iniciada – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="b23c1-137">Inicie e gerencie seu aplicativo Web do WordPress</span><span class="sxs-lookup"><span data-stu-id="b23c1-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="b23c1-138">Quando o Azure concluir a implantação do aplicativo você verá outra notificação.</span><span class="sxs-lookup"><span data-stu-id="b23c1-138">When Azure completes app deployment you see another notification.</span></span>

![Implantação bem-sucedida – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="b23c1-140">Clique na notificação.</span><span class="sxs-lookup"><span data-stu-id="b23c1-140">Click the notification.</span></span> <span data-ttu-id="b23c1-141">Se você não viu a notificação, poderá sempre acessá-la clicando no sino de notificação (![Sino de notificação – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="b23c1-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="b23c1-142">Agora você deve ver a [folha](../azure-resource-manager/resource-group-portal.md#manage-resources) de gerenciamento de seu aplicativo Web (*folha*: uma página de portal que se abre horizontalmente).</span><span class="sxs-lookup"><span data-stu-id="b23c1-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="b23c1-143">Na parte superior da página de Visão geral, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="b23c1-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Procurar – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="b23c1-145">Agora você vê a página **Inicial** do WordPress.</span><span class="sxs-lookup"><span data-stu-id="b23c1-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="b23c1-146">Configure a instalação do WordPress e comece a brincar com ele!</span><span class="sxs-lookup"><span data-stu-id="b23c1-146">Configure the WordPress installation and start playing with it!</span></span>

    ![Configuração do WordPress – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="b23c1-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b23c1-148">Next steps</span></span>
* <span data-ttu-id="b23c1-149">[Criar, configurar e implantar um aplicativo Web Laravel no Azure](app-service-web-php-get-started.md) – Aprenda as habilidades básicas que você precisa executar qualquer aplicativo Web de PHP no Azure, tais como:</span><span class="sxs-lookup"><span data-stu-id="b23c1-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="b23c1-150">Criar e configurar aplicativos no Azure do PowerShell/Bash.</span><span class="sxs-lookup"><span data-stu-id="b23c1-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="b23c1-151">Definir a versão do PHP.</span><span class="sxs-lookup"><span data-stu-id="b23c1-151">Set PHP version.</span></span>
    * <span data-ttu-id="b23c1-152">Usar um arquivo de inicialização que não está no diretório raiz do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b23c1-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="b23c1-153">Habilite a automação do Composer.</span><span class="sxs-lookup"><span data-stu-id="b23c1-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="b23c1-154">Acessar variáveis de ambiente específicas.</span><span class="sxs-lookup"><span data-stu-id="b23c1-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="b23c1-155">Solucionar erros comuns.</span><span class="sxs-lookup"><span data-stu-id="b23c1-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="b23c1-156">[Implantar seu código no Serviço de Aplicativo do Azure](web-sites-deploy.md) – Aprenda como implantar do FTP ou de repositórios de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="b23c1-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="b23c1-157">[Adicionar funcionalidade ao seu primeiro aplicativo Web](app-service-web-get-started-2.md) – Leve seu aplicativo do Azure para o próximo patamar.</span><span class="sxs-lookup"><span data-stu-id="b23c1-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="b23c1-158">Autenticar os usuários.</span><span class="sxs-lookup"><span data-stu-id="b23c1-158">Authenticate your users.</span></span> <span data-ttu-id="b23c1-159">Dimensione-o com base na demanda.</span><span class="sxs-lookup"><span data-stu-id="b23c1-159">Scale it based on demand.</span></span> <span data-ttu-id="b23c1-160">Configure alguns alertas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="b23c1-160">Set up some performance alerts.</span></span> <span data-ttu-id="b23c1-161">Tudo isso com apenas alguns cliques.</span><span class="sxs-lookup"><span data-stu-id="b23c1-161">All with a few clicks.</span></span>
