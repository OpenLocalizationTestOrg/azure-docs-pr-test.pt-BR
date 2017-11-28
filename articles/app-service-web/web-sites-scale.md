---
title: aaaScale backup de um aplicativo no Azure | Microsoft Docs
description: "Saiba como tooscale backup de um aplicativo no serviço de aplicativo do Azure tooadd capacidade e recursos."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="43fc5-103">Dimensionar um aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="43fc5-103">Scale up an app in Azure</span></span>
<span data-ttu-id="43fc5-104">Este artigo mostra como tooscale seu aplicativo no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="43fc5-104">This article shows you how tooscale your app in Azure App Service.</span></span> <span data-ttu-id="43fc5-105">Há dois fluxos de trabalho para a escala de dimensionamento, backup e expansão e este artigo explica escala Olá o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="43fc5-105">There are two workflows for scaling, scale up and scale out, and this article explains hello scale up workflow.</span></span>

* <span data-ttu-id="43fc5-106">[Escalar verticalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenha mais CPU, memória, espaço em disco e recursos adicionais como VMs (máquinas virtuais) dedicadas, domínios e certificados personalizados, slots de preparação, dimensionamento automático e muito mais.</span><span class="sxs-lookup"><span data-stu-id="43fc5-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="43fc5-107">Escalar verticalmente alterando Olá preço do plano de serviço de aplicativo que seu aplicativo pertence.</span><span class="sxs-lookup"><span data-stu-id="43fc5-107">You scale up by changing hello pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="43fc5-108">[Expansão](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentar Olá número de instâncias VM que executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43fc5-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase hello number of VM instances that run your app.</span></span>
  <span data-ttu-id="43fc5-109">Você pode expandir tooas muitos como 20 instâncias, dependendo do tipo de preços.</span><span class="sxs-lookup"><span data-stu-id="43fc5-109">You can scale out tooas many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="43fc5-110">[Ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md) na **Premium** camada aumentarão ainda mais suas instâncias de too50 de contagem de expansão.</span><span class="sxs-lookup"><span data-stu-id="43fc5-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count too50 instances.</span></span> <span data-ttu-id="43fc5-111">Para saber mais sobre a escala horizontal, consulte [Escalar a contagem de instâncias manualmente ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="43fc5-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="43fc5-112">Lá você encontrará fora como autoscaling toouse, que é a contagem de instâncias de tooscale automaticamente com base em regras predefinidas e agendas.</span><span class="sxs-lookup"><span data-stu-id="43fc5-112">There you will find out how toouse autoscaling, which is tooscale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="43fc5-113">Olá escala configurações take apenas segundos tooapply e afetam todos os aplicativos em seu [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43fc5-113">hello scale settings take only seconds tooapply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="43fc5-114">Eles não exigem que você toochange seu código ou reimplantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43fc5-114">They do not require you toochange your code or redeploy your application.</span></span>

<span data-ttu-id="43fc5-115">Para obter informações sobre preços de saudação e recursos de planos de serviço de aplicativo individuais, consulte [detalhes de preços do serviço de aplicativo](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="43fc5-115">For information about hello pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="43fc5-116">Antes de alternar um plano de serviço de aplicativo de saudação **livre** camada, você deve primeiro remover Olá [os limites de gastos](https://azure.microsoft.com/pricing/spending-limits/) em vigor para a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="43fc5-116">Before you switch an App Service plan from hello **Free** tier, you must first remove hello [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="43fc5-117">tooview ou alterar as opções para sua assinatura do serviço de aplicativo do Microsoft Azure, consulte [assinatura do Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="43fc5-117">tooview or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="43fc5-118">Escale verticalmente seu tipo de preço</span><span class="sxs-lookup"><span data-stu-id="43fc5-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="43fc5-119">No navegador, abra Olá [portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="43fc5-119">In your browser, open hello [Azure portal][portal].</span></span>
2. <span data-ttu-id="43fc5-120">Na folha do aplicativo, clique em **Todas as configurações** e em **Escalar Verticalmente**.</span><span class="sxs-lookup"><span data-stu-id="43fc5-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navegue tooscale backup de seu aplicativo do Azure.][ChooseWHP]
3. <span data-ttu-id="43fc5-122">Escolha seu tipo e depois clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="43fc5-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="43fc5-123">Olá **notificações** guia pisca uma verde **êxito** após a conclusão da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="43fc5-123">hello **Notifications** tab will flash a green **SUCCESS** after hello operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="43fc5-124">Escalar recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="43fc5-124">Scale related resources</span></span>
<span data-ttu-id="43fc5-125">Se o seu aplicativo depender de outros serviços, como o Banco de Dados SQL do Azure ou o Armazenamento do Azure, você também poderá escalar verticalmente esses recursos com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="43fc5-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="43fc5-126">Esses recursos não são dimensionados com hello plano de serviço de aplicativo e devem ser dimensionados separadamente.</span><span class="sxs-lookup"><span data-stu-id="43fc5-126">These resources are not scaled with hello App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="43fc5-127">Em **Essentials**, clique em Olá **grupo de recursos** link.</span><span class="sxs-lookup"><span data-stu-id="43fc5-127">In **Essentials**, click hello **Resource group** link.</span></span>
   
    ![Escale verticalmente os recursos relacionados de seu aplicativo do Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="43fc5-129">Em Olá **resumo** parte do hello **grupo de recursos** folha, clique em um recurso que você deseja tooscale.</span><span class="sxs-lookup"><span data-stu-id="43fc5-129">In hello **Summary** part of hello **Resource group** blade, click a resource that you want tooscale.</span></span> <span data-ttu-id="43fc5-130">Olá captura de tela a seguir mostra um recurso de banco de dados SQL e um recurso de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="43fc5-130">hello following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navegue tooresource grupo folha tooscale backup de seu aplicativo do Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="43fc5-132">Para um recurso de banco de dados SQL, clique em **configurações** > **preço** tooscale Olá preço.</span><span class="sxs-lookup"><span data-stu-id="43fc5-132">For a SQL Database resource, click **Settings** > **Pricing tier** tooscale hello pricing tier.</span></span>
   
    ![Dimensionar o hello back-end de banco de dados SQL para seu aplicativo do Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="43fc5-134">Você também pode ativar a [replicação geográfica](../sql-database/sql-database-geo-replication-overview.md) de sua instância do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="43fc5-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="43fc5-135">Para um recurso de armazenamento do Azure, clique em **configurações** > **configuração** tooscale as suas opções de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="43fc5-135">For an Azure Storage resource, click **Settings** > **Configuration** tooscale up your storage options.</span></span>
   
    ![Dimensionar a conta de armazenamento do Azure Olá usada pelo seu aplicativo do Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="43fc5-137">Saiba mais sobre os recursos de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="43fc5-137">Learn about developer features</span></span>
<span data-ttu-id="43fc5-138">Dependendo da saudação preço, hello seguintes recursos para desenvolvedores estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="43fc5-138">Depending on hello pricing tier, hello following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="43fc5-139">Número de bits</span><span class="sxs-lookup"><span data-stu-id="43fc5-139">Bitness</span></span>
* <span data-ttu-id="43fc5-140">Olá **básica**, **padrão**, e **Premium** camadas oferecem suporte a aplicativos de 64 bits e 32 bits.</span><span class="sxs-lookup"><span data-stu-id="43fc5-140">hello **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="43fc5-141">Olá **livre** e **compartilhado** plano camadas oferecem suporte apenas a aplicativos de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="43fc5-141">hello **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="43fc5-142">Suporte ao depurador</span><span class="sxs-lookup"><span data-stu-id="43fc5-142">Debugger support</span></span>
* <span data-ttu-id="43fc5-143">Suporte do depurador está disponível para Olá **livre**, **compartilhado**, e **básica** modos em uma conexão por plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43fc5-143">Debugger support is available for hello **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="43fc5-144">Suporte do depurador está disponível para Olá **padrão** e **Premium** modos em cinco conexões simultâneas por plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43fc5-144">Debugger support is available for hello **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="43fc5-145">Saiba mais sobre outros recursos</span><span class="sxs-lookup"><span data-stu-id="43fc5-145">Learn about other features</span></span>
* <span data-ttu-id="43fc5-146">Para obter informações detalhadas sobre todos os Olá restantes recursos saudação do serviço de aplicativo planos, inclusive de preço e recursos de interesse tooall os usuários (incluindo os desenvolvedores), consulte [detalhes de preços do serviço de aplicativo](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="43fc5-146">For detailed information about all of hello remaining features in hello App Service plans, including pricing and features of interest tooall users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="43fc5-147">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/) onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43fc5-147">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="43fc5-148">Nenhum cartão de crédito é exigido e não há compromissos.</span><span class="sxs-lookup"><span data-stu-id="43fc5-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="43fc5-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43fc5-149">Next steps</span></span>
* <span data-ttu-id="43fc5-150">tooget iniciado com o Azure, consulte [avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43fc5-150">tooget started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="43fc5-151">Para obter informações sobre preços, suporte e SLA, visite Olá links a seguir.</span><span class="sxs-lookup"><span data-stu-id="43fc5-151">For information about pricing, support, and SLA, visit hello following links.</span></span>
  
    [<span data-ttu-id="43fc5-152">Detalhes de preços de transferências de dados</span><span class="sxs-lookup"><span data-stu-id="43fc5-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="43fc5-153">Planos de suporte do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="43fc5-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="43fc5-154">Contratos de Nível de Serviço</span><span class="sxs-lookup"><span data-stu-id="43fc5-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="43fc5-155">Detalhes de preços do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="43fc5-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="43fc5-156">[Tamanhos de máquina virtual e de serviço de nuvem do Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="43fc5-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="43fc5-157">Detalhes de Preços do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="43fc5-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="43fc5-158">Detalhes de Preços do Serviço de Aplicativo - Conexões SSL</span><span class="sxs-lookup"><span data-stu-id="43fc5-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="43fc5-159">Para obter informações sobre práticas recomendadas do Serviço de Aplicativo do Azure, incluindo a criação de uma arquitetura escalonável e flexível, consulte [Práticas recomendadas: Aplicativos Web do Serviço de Aplicativo do Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="43fc5-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="43fc5-160">Para vídeos sobre como dimensionar aplicativos de serviço de aplicativo, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="43fc5-160">For videos about scaling App Service apps, see hello following resources:</span></span>
  
  * [<span data-ttu-id="43fc5-161">Quando tooScale sites do Azure - com Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="43fc5-161">When tooScale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="43fc5-162">Dimensionamento automático de Sites do Azure, CPU ou programado - com Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="43fc5-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="43fc5-163">Como dimensionar sites do Azure - com Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="43fc5-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
