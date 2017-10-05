---
title: Escalar verticalmente um aplicativo no Azure | Microsoft Docs
description: "Saiba como escalar verticalmente um aplicativo no Serviço de Aplicativo do Azure a fim de adicionar capacidade e recursos."
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
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="5e088-103">Dimensionar um aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="5e088-103">Scale up an app in Azure</span></span>
<span data-ttu-id="5e088-104">Este artigo mostra como dimensionar seu aplicativo no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e088-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="5e088-105">Há dois fluxos de trabalho para dimensionamento, escalar verticalmente e escalar horizontalmente, e este artigo explica o fluxo de trabalho de escala vertical.</span><span class="sxs-lookup"><span data-stu-id="5e088-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="5e088-106">[Escalar verticalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenha mais CPU, memória, espaço em disco e recursos adicionais como VMs (máquinas virtuais) dedicadas, domínios e certificados personalizados, slots de preparação, dimensionamento automático e muito mais.</span><span class="sxs-lookup"><span data-stu-id="5e088-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="5e088-107">Você escala verticalmente alterando o tipo de preço do plano do Serviço de Aplicativo ao qual seu aplicativo pertence.</span><span class="sxs-lookup"><span data-stu-id="5e088-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="5e088-108">[Escalar horizontalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumenta o número de instâncias de VM que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e088-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="5e088-109">Você pode escalar horizontalmente até 20 instâncias, dependendo de seu tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="5e088-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="5e088-110">[Ambientes do Serviço de Aplicativo](../app-service/app-service-app-service-environments-readme.md) na camada **Premium** aumentará ainda mais sua contagem de expansão para 50 instâncias.</span><span class="sxs-lookup"><span data-stu-id="5e088-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="5e088-111">Para saber mais sobre a escala horizontal, consulte [Escalar a contagem de instâncias manualmente ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="5e088-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="5e088-112">Lá você encontrará como usar o dimensionamento automático, que serve para dimensionar automaticamente a contagem de instâncias com base em regras e programações predefinidas.</span><span class="sxs-lookup"><span data-stu-id="5e088-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="5e088-113">As configurações de escala terão apenas alguns segundos para serem aplicadas e afetam todos os aplicativos em seu [plano do Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e088-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="5e088-114">Elas não exigem a alteração de seu código ou a reimplantação de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e088-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="5e088-115">Para obter informações sobre os preços e recursos de planos individuais do Serviço de Aplicativo, consulte [Detalhes de Preços dos Serviços de Aplicativo](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="5e088-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="5e088-116">Antes de mudar um Plano do Serviço de Aplicativo do tipo **Gratuito** , é necessário remover os [limites de gastos](https://azure.microsoft.com/pricing/spending-limits/) em vigor para sua Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e088-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="5e088-117">Para exibir ou alterar as opções da sua assinatura do Serviço de Aplicativo do Microsoft Azure, consulte [Assinaturas do Microsoft Azure][azuresubscriptions].</span><span class="sxs-lookup"><span data-stu-id="5e088-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="5e088-118">Escale verticalmente seu tipo de preço</span><span class="sxs-lookup"><span data-stu-id="5e088-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="5e088-119">No seu navegador, abra o [Portal do Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="5e088-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="5e088-120">Na folha do aplicativo, clique em **Todas as configurações** e em **Escalar Verticalmente**.</span><span class="sxs-lookup"><span data-stu-id="5e088-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Navegue para escalar verticalmente seu aplicativo do Azure.][ChooseWHP]
3. <span data-ttu-id="5e088-122">Escolha seu tipo e depois clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5e088-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="5e088-123">A guia **Notificações** vai piscar **SUCESSO** em verde quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="5e088-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="5e088-124">Escalar recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="5e088-124">Scale related resources</span></span>
<span data-ttu-id="5e088-125">Se o seu aplicativo depender de outros serviços, como o Banco de Dados SQL do Azure ou o Armazenamento do Azure, você também poderá escalar verticalmente esses recursos com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="5e088-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="5e088-126">Esses recursos não são dimensionados com o Plano do Serviço de Aplicativo e devem ser dimensionados separadamente.</span><span class="sxs-lookup"><span data-stu-id="5e088-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="5e088-127">Em **Essentials**, clique no link **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="5e088-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Escale verticalmente os recursos relacionados de seu aplicativo do Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="5e088-129">Na parte **Resumo** da folha do **Grupo de recursos**, clique em um dos recursos que você quer dimensionar.</span><span class="sxs-lookup"><span data-stu-id="5e088-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="5e088-130">A captura de tela abaixo mostra um recurso do Banco de Dados SQL e um recurso do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e088-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![Navegue até a folha do grupo de recursos para escalar verticalmente seu aplicativo do Azure](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="5e088-132">Para um recurso do Banco de Dados SQL, clique em **Configurações** > **Tipo de preço** para dimensionar o tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="5e088-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Escalar verticalmente o back-end do Banco de Dados SQL para seu aplicativo do Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="5e088-134">Você também pode ativar a [replicação geográfica](../sql-database/sql-database-geo-replication-overview.md) de sua instância do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="5e088-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="5e088-135">Para um recurso de Armazenamento do Azure, clique em **Configurações** > **Configuração** para escalar verticalmente suas opções de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5e088-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Escalar verticalmente a conta do Armazenamento do Azure usada por seu aplicativo do Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="5e088-137">Saiba mais sobre os recursos de desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="5e088-137">Learn about developer features</span></span>
<span data-ttu-id="5e088-138">Dependendo da camada de preços, os seguintes recursos para desenvolvedores estarão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="5e088-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="5e088-139">Número de bits</span><span class="sxs-lookup"><span data-stu-id="5e088-139">Bitness</span></span>
* <span data-ttu-id="5e088-140">Os modos **Básico**, **Standard** e **Premium** dão suporte a aplicativos de 32 e 64 bits.</span><span class="sxs-lookup"><span data-stu-id="5e088-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="5e088-141">As camadas dos planos **Gratuito** e **Compartilhado** dão suporte apenas a aplicativos de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="5e088-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="5e088-142">Suporte ao depurador</span><span class="sxs-lookup"><span data-stu-id="5e088-142">Debugger support</span></span>
* <span data-ttu-id="5e088-143">O suporte ao depurador está disponível para os modos **Gratuito**, **Compartilhado** e **Básico** em uma conexão por Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e088-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="5e088-144">O suporte ao depurador está disponível para os modos **Standard** e **Premium** em cinco conexões simultâneas por Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e088-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="5e088-145">Saiba mais sobre outros recursos</span><span class="sxs-lookup"><span data-stu-id="5e088-145">Learn about other features</span></span>
* <span data-ttu-id="5e088-146">Para obter informações detalhadas sobre todos os recursos restantes nos planos do Serviço de Aplicativo, incluindo preços e recursos de interesse para todos os usuários (incluindo desenvolvedores), consulte [Detalhes de preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="5e088-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="5e088-147">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) , em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e088-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5e088-148">Nenhum cartão de crédito é exigido e não há compromissos.</span><span class="sxs-lookup"><span data-stu-id="5e088-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="5e088-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e088-149">Next steps</span></span>
* <span data-ttu-id="5e088-150">Para começar a usar o Azure, consulte [Avaliação Gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e088-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5e088-151">Para saber mais sobre preços, suporte e SLA, visite os links a seguir.</span><span class="sxs-lookup"><span data-stu-id="5e088-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="5e088-152">Detalhes de preços de transferências de dados</span><span class="sxs-lookup"><span data-stu-id="5e088-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="5e088-153">Planos de suporte do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5e088-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="5e088-154">Contratos de Nível de Serviço</span><span class="sxs-lookup"><span data-stu-id="5e088-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="5e088-155">Detalhes de preços do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="5e088-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="5e088-156">[Tamanhos de máquina virtual e de serviço de nuvem do Microsoft Azure][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="5e088-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="5e088-157">Detalhes de Preços do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="5e088-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="5e088-158">Detalhes de Preços do Serviço de Aplicativo - Conexões SSL</span><span class="sxs-lookup"><span data-stu-id="5e088-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="5e088-159">Para obter informações sobre práticas recomendadas do Serviço de Aplicativo do Azure, incluindo a criação de uma arquitetura escalonável e flexível, consulte [Práticas recomendadas: Aplicativos Web do Serviço de Aplicativo do Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e088-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="5e088-160">Para assistir a vídeos sobre o dimensionamento de aplicativos do Serviço de Aplicativo, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="5e088-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="5e088-161">Quando dimensionar Sites do Azure - com Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="5e088-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="5e088-162">Dimensionamento automático de Sites do Azure, CPU ou programado - com Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="5e088-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="5e088-163">Como dimensionar sites do Azure - com Stefan Schackow</span><span class="sxs-lookup"><span data-stu-id="5e088-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

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
