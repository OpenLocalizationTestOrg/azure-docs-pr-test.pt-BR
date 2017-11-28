---
title: "aaaCreate um aplicativo web do WordPress no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toocreate um novo Azure web aplicativo para um blog do WordPress usando Olá Portal do Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="98d34-103">Criar um aplicativo Web do WordPress no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="98d34-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="98d34-104">Este tutorial mostra como toodeploy um blog do WordPress do site do hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="98d34-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="98d34-105">Quando você concluiu o tutorial de saudação terá seu próprio site de blog do WordPress para cima e em execução na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="98d34-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![Site do WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="98d34-107">Você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="98d34-107">You'll learn:</span></span>

* <span data-ttu-id="98d34-108">Como toofind um modelo de aplicativo hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="98d34-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="98d34-109">Como toocreate um aplicativo web no aplicativo do Azure que serviço baseado no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d34-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="98d34-110">Como tooconfigure as configurações de serviço de aplicativo do Azure para Olá novo web app e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="98d34-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="98d34-111">Hello Azure Marketplace disponibiliza uma ampla gama de aplicativos web populares desenvolvidos pela Microsoft, outras empresas e iniciativas de software de código aberto.</span><span class="sxs-lookup"><span data-stu-id="98d34-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="98d34-112">Olá os aplicativos web são criados em uma ampla variedade de estruturas populares, como [PHP](/develop/nodejs/) neste exemplo WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), e [Python](/develop/python/), tooname alguns.</span><span class="sxs-lookup"><span data-stu-id="98d34-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="98d34-113">toocreate um aplicativo web do hello Azure Marketplace Olá somente software que você precisa é saudação do navegador que você usa para Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="98d34-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="98d34-114">site de WordPress Olá que você implantar este tutorial usa MySQL Olá de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="98d34-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="98d34-115">Se você quiser usar tooinstead banco de dados SQL do banco de dados de saudação, consulte [Nami projeto](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="98d34-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="98d34-116">**Projeto Nami** também está disponível por meio de saudação Marketplace.</span><span class="sxs-lookup"><span data-stu-id="98d34-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="98d34-117">toocomplete neste tutorial, você precisa de uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="98d34-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="98d34-118">Se não tiver uma conta, você poderá [ativar os benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) ou [inscrever-se em uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="98d34-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="98d34-119">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="98d34-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="98d34-120">Lá, você poderá criar imediatamente um aplicativo Web de curta duração inicial no Serviço de Aplicativo – sem exigência de cartão de crédito e sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="98d34-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="98d34-121">Selecionar WordPress e configurar o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="98d34-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="98d34-122">Faça logon no toohello [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="98d34-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="98d34-123">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="98d34-123">Click **New**.</span></span>
   
    ![Criar Novo][5]
3. <span data-ttu-id="98d34-125">Procure **WordPress** e clique em **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="98d34-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="98d34-126">Se você quiser toouse banco de dados SQL em vez do MySQL, procure **Nami projeto**.</span><span class="sxs-lookup"><span data-stu-id="98d34-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress da lista][7]
4. <span data-ttu-id="98d34-128">Depois de ler a descrição de saudação do aplicativo de WordPress hello, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="98d34-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Criar](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="98d34-130">Insira um nome para o aplicativo web de saudação em Olá **aplicativo Web** caixa.</span><span class="sxs-lookup"><span data-stu-id="98d34-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="98d34-131">Esse nome deve ser exclusivo no domínio azurewebsites.net de saudação porque Olá URL do aplicativo web de Olá {name}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="98d34-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="98d34-132">Se o nome de saudação não for exclusivo, um ponto de exclamação vermelho é exibido na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d34-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="98d34-133">Se você tiver mais de uma assinatura, escolha Olá aquele que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="98d34-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="98d34-134">Selecione um **Grupo de Recursos** ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="98d34-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="98d34-135">Para saber mais sobre os grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98d34-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="98d34-136">Selecione um **Plano/Local do Serviço de Aplicativo** ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="98d34-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="98d34-137">Para saber mais sobre os planos do Serviço de Aplicativo, confira [Visão geral dos planos do Serviço de Aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="98d34-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="98d34-138">Clique em **banco de dados**e, em seguida, em Olá **novo banco de dados MySQL** folha fornecem valores de saudação necessárias para configurar o banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="98d34-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="98d34-139">a.</span><span class="sxs-lookup"><span data-stu-id="98d34-139">a.</span></span> <span data-ttu-id="98d34-140">Digite um novo nome ou deixe o nome padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d34-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="98d34-141">b.</span><span class="sxs-lookup"><span data-stu-id="98d34-141">b.</span></span> <span data-ttu-id="98d34-142">Deixe Olá **tipo de banco de dados** definido muito**compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="98d34-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="98d34-143">c.</span><span class="sxs-lookup"><span data-stu-id="98d34-143">c.</span></span> <span data-ttu-id="98d34-144">Escolha Olá mesmo local como Olá aquele que você escolheu para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d34-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="98d34-145">d.</span><span class="sxs-lookup"><span data-stu-id="98d34-145">d.</span></span> <span data-ttu-id="98d34-146">Escolha uma camada de preços.</span><span class="sxs-lookup"><span data-stu-id="98d34-146">Choose a pricing tier.</span></span> <span data-ttu-id="98d34-147">Para este tutorial, Mercury (gratuito, com conexões e espaço em disco mínimos permitidos ) é adequado.</span><span class="sxs-lookup"><span data-stu-id="98d34-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="98d34-148">Em Olá **novo banco de dados MySQL** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="98d34-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="98d34-149">Em Olá **WordPress** folha, aceite os termos legais hello e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="98d34-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Configurar aplicativo Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="98d34-151">Serviço de aplicativo do Azure cria Olá web app, normalmente em menos de um minuto.</span><span class="sxs-lookup"><span data-stu-id="98d34-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="98d34-152">Você pode assistir andamento Olá clicando o ícone de sino Olá na parte superior de saudação da página de portal hello.</span><span class="sxs-lookup"><span data-stu-id="98d34-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Indicador de progresso](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="98d34-154">Inicie e gerencie seu aplicativo Web do WordPress</span><span class="sxs-lookup"><span data-stu-id="98d34-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="98d34-155">Depois da criação do aplicativo web Olá, navegue no hello Azure Portal toohello grupo de recursos no qual você criou o aplicativo hello e você pode ver Olá web app e o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d34-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="98d34-156">Olá adicional do recurso com ícone de lâmpada Olá é [Application Insights](/services/application-insights/), que fornece serviços de monitoramento para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="98d34-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="98d34-157">Em Olá **grupo de recursos** folha, clique em linha de aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="98d34-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Configurar aplicativo Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="98d34-159">Na folha de saudação do aplicativo Web, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="98d34-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![URL do site][browse]
4. <span data-ttu-id="98d34-161">Em Olá WordPress **bem-vindo** página, insira as informações de configuração do hello exigidas pelo WordPress e, em seguida, clique em **instalar o WordPress**.</span><span class="sxs-lookup"><span data-stu-id="98d34-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configurar WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="98d34-163">Faça logon usando credenciais Olá criado no hello **bem-vindo** página.</span><span class="sxs-lookup"><span data-stu-id="98d34-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="98d34-164">A página de Painel do site é aberta.</span><span class="sxs-lookup"><span data-stu-id="98d34-164">Your site Dashboard page opens.</span></span>    
   
    ![Site do WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="98d34-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98d34-166">Next steps</span></span>
<span data-ttu-id="98d34-167">Você viu como toocreate e implantar um aplicativo web do PHP da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d34-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="98d34-168">Para obter mais informações sobre como usar PHP no Azure, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="98d34-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="98d34-169">Para obter mais informações sobre como toowork com aplicativos de Web do serviço de aplicativo, consulte os links de saudação em Olá lado esquerdo da página hello (para janelas de navegador ampla) ou na parte superior de saudação da página de saudação (para janelas de navegador estreita).</span><span class="sxs-lookup"><span data-stu-id="98d34-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="98d34-170">O que mudou</span><span class="sxs-lookup"><span data-stu-id="98d34-170">What's changed</span></span>
* <span data-ttu-id="98d34-171">Uma alteração de toohello do guia de sites tooApp serviço, consulte [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="98d34-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
