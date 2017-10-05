---
title: "Referência para navegar no portal do Azure"
description: "Conheça as diferentes experiências de usuário para aplicativos Web do Serviço de Aplicativo entre o portal de gerenciamento e o Portal do Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="9b04a-103">Referência para navegar no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b04a-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="9b04a-104">Os Sites da Web do Azure agora são chamados de [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="9b04a-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="9b04a-105">Estamos atualizando toda a nossa documentação para refletir essa alteração no nome e para fornecer instruções para o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b04a-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="9b04a-106">Até que esse processo seja concluído, você poderá usar este documento como um guia para trabalhar com Aplicativos Web no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b04a-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="9b04a-107">O futuro do Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="9b04a-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="9b04a-108">Você notará as alterações de identidade visual no Portal Clássico do Azure, mas esse portal está sendo substituído pelo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b04a-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="9b04a-109">Como o portal clássico está sendo desativado, o foco para o novo desenvolvimento está mudando para o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b04a-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="9b04a-110">Todos os novos recursos futuros para Aplicativos Web serão incluídos no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b04a-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="9b04a-111">Comece a usar o Portal do Azure para aproveitar os recursos mais recentes que os aplicativos Web têm a oferecer.</span><span class="sxs-lookup"><span data-stu-id="9b04a-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="9b04a-112">Diferenças de layout entre o portal clássico e o Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="9b04a-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="9b04a-113">No portal clássico, todos os serviços do Azure são listados no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="9b04a-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="9b04a-114">A navegação no portal antigo segue uma estrutura de árvore, em que você pode começar no serviço e navegar para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="9b04a-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="9b04a-115">Essa estrutura funciona bem para o gerenciamento de componentes independentes.</span><span class="sxs-lookup"><span data-stu-id="9b04a-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="9b04a-116">No entanto, os aplicativos criados no Azure são uma coleção de serviços interconectados, e essa estrutura de árvore não é ideal para trabalhar com coleções de serviços.</span><span class="sxs-lookup"><span data-stu-id="9b04a-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="9b04a-117">O Portal do Azure facilita a compilação de aplicativos de ponta a ponta com componentes de vários serviços.</span><span class="sxs-lookup"><span data-stu-id="9b04a-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="9b04a-118">O portal é organizado como *jornadas*.</span><span class="sxs-lookup"><span data-stu-id="9b04a-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="9b04a-119">Uma *jornada* é uma série de *folhas*, que são contêineres para os diferentes componentes.</span><span class="sxs-lookup"><span data-stu-id="9b04a-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="9b04a-120">Por exemplo, a configuração do dimensionamento automático para um aplicativo Web é uma *jornada* que leva várias folhas, conforme mostrado no exemplo a seguir: a folha **site** (o título dessa folha ainda não foi atualizado para usar a nova terminologia), a folha **Configurações** e a folha **Escalar horizontalmente**.</span><span class="sxs-lookup"><span data-stu-id="9b04a-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="9b04a-121">No exemplo, o dimensionamento automático está sendo configurado para depender do uso da CPU. Portanto, há também uma folha de **Percentual de CPU**.</span><span class="sxs-lookup"><span data-stu-id="9b04a-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="9b04a-122">Os componentes dentro das *folhas* são chamados de *partes*, que se parecem com blocos.</span><span class="sxs-lookup"><span data-stu-id="9b04a-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="9b04a-123">Exemplo de navegação: criar um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="9b04a-123">Navigation example: create a web app</span></span>
<span data-ttu-id="9b04a-124">A criação de novos aplicativos Web é muito fácil.</span><span class="sxs-lookup"><span data-stu-id="9b04a-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="9b04a-125">A imagem a seguir mostra o portal clássico e o portal lado a lado para demonstrar que não houve muitas mudanças no número de etapas necessárias para colocar um aplicativo Web em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="9b04a-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="9b04a-126">No portal, você pode escolher entre os tipos mais comuns de aplicativos Web, incluindo aplicativos de galerias populares, como o WordPress.</span><span class="sxs-lookup"><span data-stu-id="9b04a-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="9b04a-127">Para obter uma lista completa de aplicativos disponíveis, visite o [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="9b04a-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="9b04a-128">Ao criar um aplicativo Web, você especifica a URL, o plano do Serviço de Aplicativo e o local no portal, como faria no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9b04a-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="9b04a-129">Além disso, o portal permite definir outras configurações comuns.</span><span class="sxs-lookup"><span data-stu-id="9b04a-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="9b04a-130">Por exemplo, [grupos de recursos](../azure-resource-manager/resource-group-overview.md) tornam simples ver e gerenciar recursos relacionados do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b04a-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="9b04a-131">Exemplo de navegação: configurações e recursos</span><span class="sxs-lookup"><span data-stu-id="9b04a-131">Navigation example: settings and features</span></span>
<span data-ttu-id="9b04a-132">Todas as configurações e recursos agora são agrupados logicamente em uma única folha, da qual você pode navegar.</span><span class="sxs-lookup"><span data-stu-id="9b04a-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="9b04a-133">Por exemplo, você pode criar domínios personalizados clicando em **Domínios personalizados e SSL** na folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="9b04a-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="9b04a-134">Para configurar um alerta de monitoramento, clique em **Solicitações e erros** e em **Adicionar Alerta**.</span><span class="sxs-lookup"><span data-stu-id="9b04a-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="9b04a-135">Para habilitar o diagnóstico, clique em **Logs de diagnóstico** na folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="9b04a-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="9b04a-136">Para definir configurações de aplicativo, clique em **Configurações do aplicativo** na folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="9b04a-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="9b04a-137">Com exceção do nome da marca, alguns itens no portal foram renomeados ou agrupados de modo diferente para que seja mais fácil encontrá-los.</span><span class="sxs-lookup"><span data-stu-id="9b04a-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="9b04a-138">Por exemplo, veja a seguir uma captura de tela da página correspondente de configurações de aplicativo (**Configurar**) no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9b04a-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="9b04a-139">Mais Recursos</span><span class="sxs-lookup"><span data-stu-id="9b04a-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="9b04a-140">[Azure Marketplace]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="9b04a-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="9b04a-141">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b04a-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9b04a-142">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="9b04a-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="9b04a-143">O que mudou</span><span class="sxs-lookup"><span data-stu-id="9b04a-143">What's changed</span></span>
* <span data-ttu-id="9b04a-144">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="9b04a-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

