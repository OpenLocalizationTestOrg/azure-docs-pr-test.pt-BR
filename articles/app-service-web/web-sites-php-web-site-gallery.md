---
title: "Criar um aplicativo Web do WordPress no Serviço de Aplicativo do Azure | Microsoft Docs"
description: Saiba como criar um novo aplicativo Web do Azure para um blog do WordPress usando o Portal do Azure.
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="2d7cb-103">Criar um aplicativo Web do WordPress no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2d7cb-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="2d7cb-104">Este tutorial mostra como implantar um site de blog do WordPress no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="2d7cb-105">Ao concluir o tutorial, você terá seu próprio site de blog do WordPress ativo e em execução na nuvem.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![Site do WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="2d7cb-107">O que você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="2d7cb-107">You'll learn:</span></span>

* <span data-ttu-id="2d7cb-108">Como localizar um modelo de aplicativo no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="2d7cb-109">Como criar um aplicativo Web no Serviço de Aplicativo do Azure com base no modelo.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="2d7cb-110">Como definir configurações do Serviço de Aplicativo do Azure para o novo aplicativo Web e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="2d7cb-111">O Azure Marketplace disponibiliza uma ampla gama de aplicativos Web populares desenvolvidos pela Microsoft, por outras empresas e por iniciativas de software livre.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="2d7cb-112">Os aplicativos Web são criados em uma grande variedade de estruturas populares, como [PHP](/develop/nodejs/) neste exemplo do WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) e [Python](/develop/python/), para citar alguns.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="2d7cb-113">Para criar um aplicativo Web do Azure Marketplace, o único software necessário será o navegador que você usa para o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="2d7cb-114">O site do WordPress implantado neste tutorial usa o MySQL para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="2d7cb-115">Se, em vez disso, você quiser usar o Banco de Dados SQL para o banco de dados, consulte [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="2d7cb-116">**Project Nami** também está disponível por meio do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="2d7cb-117">Para concluir este tutorial, você precisa de uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="2d7cb-118">Se não tiver uma conta, você poderá [ativar os benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) ou [inscrever-se em uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="2d7cb-119">Se você quiser ter uma introdução ao Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="2d7cb-120">Lá, você poderá criar imediatamente um aplicativo Web de curta duração inicial no Serviço de Aplicativo – sem exigência de cartão de crédito e sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="2d7cb-121">Selecionar WordPress e configurar o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2d7cb-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="2d7cb-122">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2d7cb-123">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-123">Click **New**.</span></span>
   
    ![Criar Novo][5]
3. <span data-ttu-id="2d7cb-125">Procure **WordPress** e clique em **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="2d7cb-126">Se você desejar usar o Banco de Dados SQL em vez de MySQL, procure **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress da lista][7]
4. <span data-ttu-id="2d7cb-128">Depois de ler a descrição do aplicativo WordPress, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Criar](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="2d7cb-130">Digite um nome para o aplicativo Web na caixa **aplicativo Web** .</span><span class="sxs-lookup"><span data-stu-id="2d7cb-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="2d7cb-131">Esse nome deve ser exclusivo no domínio azurewebsites.net porque a URL do aplicativo Web será {nome}.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="2d7cb-132">Se o nome inserido não for exclusivo, um ponto de exclamação vermelho aparecerá na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="2d7cb-133">Se você tiver mais de uma assinatura, escolha a que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="2d7cb-134">Selecione um **grupo de recursos** ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="2d7cb-135">Para saber mais sobre os grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="2d7cb-136">Selecione um **Plano/Local do Serviço de Aplicativo** ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="2d7cb-137">Para obter mais informações sobre planos de serviço de aplicativo, consulte [Visão geral de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2d7cb-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="2d7cb-138">Clique em **Banco de Dados** e, em seguida, na folha **Novo Banco de Dados MySQL**, forneça os valores necessários para configurar o banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="2d7cb-139">a.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-139">a.</span></span> <span data-ttu-id="2d7cb-140">Digite um novo nome ou mantenha o nome padrão.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="2d7cb-141">b.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-141">b.</span></span> <span data-ttu-id="2d7cb-142">Deixe o **Tipo de Banco de Dados** definido como **Compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="2d7cb-143">c.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-143">c.</span></span> <span data-ttu-id="2d7cb-144">Escolha o mesmo local que o que você escolheu para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="2d7cb-145">d.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-145">d.</span></span> <span data-ttu-id="2d7cb-146">Escolha uma camada de preços.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-146">Choose a pricing tier.</span></span> <span data-ttu-id="2d7cb-147">Para este tutorial, Mercury (gratuito, com conexões e espaço em disco mínimos permitidos ) é adequado.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="2d7cb-148">Na folha **Novo Banco de Dados MySQL**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="2d7cb-149">Na folha **WordPress**, aceite os termos legais e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Configurar aplicativo Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="2d7cb-151">O Serviço de Aplicativo do Azure cria o aplicativo Web, geralmente em menos de um minuto.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="2d7cb-152">Você pode observar o progresso clicando no ícone de sino na parte superior da página do portal.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Indicador de progresso](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="2d7cb-154">Inicie e gerencie seu aplicativo Web do WordPress</span><span class="sxs-lookup"><span data-stu-id="2d7cb-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="2d7cb-155">Quando a criação de aplicativos Web for concluída, navegue no Portal do Azure para o grupo de recursos no qual você criou o aplicativo e você poderá ver o aplicativo Web e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="2d7cb-156">O recurso adicional com o ícone de lâmpada é o [Application Insights](/services/application-insights/), que fornece serviços de monitoramento para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="2d7cb-157">Na folha **Grupo de recursos** , clique na linha de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Configurar aplicativo Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="2d7cb-159">Na folha do aplicativo Web, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-159">In the Web app blade, click **Browse**.</span></span>
   
    ![URL do site][browse]
4. <span data-ttu-id="2d7cb-161">Na página de **Boas-vindas** do WordPress, insira as informações de configuração exigidas pelo WordPress e, em seguida, clique em **Instalar WordPress**.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configurar WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="2d7cb-163">Faça logon usando as credenciais que você criou na página de **Boas-vindas** .</span><span class="sxs-lookup"><span data-stu-id="2d7cb-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="2d7cb-164">A página de Painel do site é aberta.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-164">Your site Dashboard page opens.</span></span>    
   
    ![Site do WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="2d7cb-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d7cb-166">Next steps</span></span>
<span data-ttu-id="2d7cb-167">Você aprendeu como criar e implantar um aplicativo Web PHP por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="2d7cb-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="2d7cb-168">Para obter mais informações sobre como usar o PHP no Azure, consulte o [Centro de desenvolvedores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="2d7cb-169">Para obter mais informações sobre como trabalhar com aplicativos Web do Serviço de Aplicativo, consulte os links no lado esquerdo da página (para janelas de navegador amplas) ou na parte superior da página (para janelas de navegador estreitas).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="2d7cb-170">O que mudou</span><span class="sxs-lookup"><span data-stu-id="2d7cb-170">What's changed</span></span>
* <span data-ttu-id="2d7cb-171">Para obter um guia sobre a alteração dos Sites para o Serviço de Aplicativo, consulte [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="2d7cb-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
