---
title: "Visão geral de integridade do recurso aaaAzure | Microsoft Docs"
description: "Visão geral do Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="551e4-103">Visão geral do Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="551e4-103">Azure resource health overview</span></span>
 
<span data-ttu-id="551e4-104">O Resource Health ajuda a diagnosticar e obter suporte quando um problema do Azure afeta seus recursos.</span><span class="sxs-lookup"><span data-stu-id="551e4-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="551e4-105">Ele informa sobre integridade de saudação atuais e anteriores de seus recursos e ajuda a mitigar os problemas.</span><span class="sxs-lookup"><span data-stu-id="551e4-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="551e4-106">O Resource Health fornece suporte técnico quando você precisa de ajuda com problemas de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="551e4-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="551e4-107">Enquanto [Status do Azure](https://status.azure.com) informa você sobre problemas de serviço que afetam um amplo conjunto de clientes do Azure, a integridade de recursos fornece um painel personalizado de integridade de saudação de seus recursos.</span><span class="sxs-lookup"><span data-stu-id="551e4-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="551e4-108">Integridade de recursos mostra todas as vezes Olá seus recursos não estavam disponíveis no hello devido a problemas de serviço tooAzure.</span><span class="sxs-lookup"><span data-stu-id="551e4-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="551e4-109">Isso torna fácil para você toounderstand se um SLA foi violado.</span><span class="sxs-lookup"><span data-stu-id="551e4-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="551e4-110">O que é considerado um recurso e como o Resource Health decide se um recurso está íntegro ou não?</span><span class="sxs-lookup"><span data-stu-id="551e4-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="551e4-111">Um recurso é uma instância criada de um tipo de recurso oferecido por um serviço do Azure por meio do Azure Resource Manager, por exemplo: uma máquina virtual, um aplicativo Web ou um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="551e4-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="551e4-112">Integridade de recursos depende de sinais emitidos pelo Olá diferentes serviços do Azure tooassess se um recurso é Íntegro ou não.</span><span class="sxs-lookup"><span data-stu-id="551e4-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="551e4-113">Se um recurso não está íntegro, integridade de recursos analisa informações adicionais toodetermine Olá origem Olá problema.</span><span class="sxs-lookup"><span data-stu-id="551e4-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="551e4-114">Ele também identifica ações que Microsoft está demorando problema de saudação toofix ou o que ações tooaddress Olá causam do problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="551e4-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="551e4-115">Lista completa de saudação de revisão dos tipos de recursos e de integridade verifica [integridade de recursos do Azure](resource-health-checks-resource-types.md) para obter detalhes adicionais sobre como a integridade é avaliada.</span><span class="sxs-lookup"><span data-stu-id="551e4-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="551e4-116">Status de integridade fornecida pelo Resource Health</span><span class="sxs-lookup"><span data-stu-id="551e4-116">Health status provided by resource health</span></span>
<span data-ttu-id="551e4-117">integridade de saudação de um recurso é um dos Olá status a seguir:</span><span class="sxs-lookup"><span data-stu-id="551e4-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="551e4-118">Disponível</span><span class="sxs-lookup"><span data-stu-id="551e4-118">Available</span></span>
<span data-ttu-id="551e4-119">serviço de saudação não detectou todos os eventos afetar a integridade de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="551e4-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="551e4-120">Em casos onde o recurso de saudação se recuperou de tempo de inatividade não planejado durante a saudação última 24 horas, você verá Olá **recuperado recentemente** notificação.</span><span class="sxs-lookup"><span data-stu-id="551e4-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Máquina virtual disponível do Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="551e4-122">Indisponível</span><span class="sxs-lookup"><span data-stu-id="551e4-122">Unavailable</span></span>
<span data-ttu-id="551e4-123">serviço de saudação detectou um evento de plataforma não afetar a integridade de saudação do recurso de saudação ou a plataforma em andamento.</span><span class="sxs-lookup"><span data-stu-id="551e4-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="551e4-124">Eventos de plataforma</span><span class="sxs-lookup"><span data-stu-id="551e4-124">Platform events</span></span>
<span data-ttu-id="551e4-125">Esses eventos são disparados por vários componentes de saudação infraestrutura do Azure e incluem ações agendadas, como manutenção planejada e incidentes inesperados, como uma reinicialização do host não planejado.</span><span class="sxs-lookup"><span data-stu-id="551e4-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="551e4-126">Integridade de recursos fornece detalhes adicionais sobre o evento hello, o processo de recuperação hello e habilita o suporte de toocontact mesmo se você não tiver um ativo do Microsoft contrato de suporte.</span><span class="sxs-lookup"><span data-stu-id="551e4-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Recurso integridade indisponível máquina de virtual vencimento evento tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="551e4-128">Eventos de não plataforma</span><span class="sxs-lookup"><span data-stu-id="551e4-128">Non-Platform events</span></span>
<span data-ttu-id="551e4-129">Esses eventos são disparados por ações realizadas por usuários, por exemplo parar uma máquina virtual ou alcançar Olá o número máximo de conexões tooa Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="551e4-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Recurso integridade indisponível máquina de virtual vencimento evento toonon plataforma](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="551e4-131">Desconhecido</span><span class="sxs-lookup"><span data-stu-id="551e4-131">Unknown</span></span>
<span data-ttu-id="551e4-132">Esse status de integridade indica que o Resource Health não recebeu informações sobre este recurso há mais de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="551e4-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="551e4-133">Embora esse status não é uma indicação definitiva do estado de saudação do recurso Olá, é um ponto de dados importantes no processo de solução de problemas de saudação:</span><span class="sxs-lookup"><span data-stu-id="551e4-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="551e4-134">Se estiver executando o recurso hello como status Olá esperado do recurso Olá atualizará tooAvailable após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="551e4-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="551e4-135">Se você estiver tendo problemas com o recurso de saudação, hello status de integridade desconhecido pode sugerir recursos Olá é afetado por um evento na plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="551e4-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Máquina virtual desconhecida do Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="551e4-137">Relatar um status incorreto</span><span class="sxs-lookup"><span data-stu-id="551e4-137">Report an incorrect status</span></span>
<span data-ttu-id="551e4-138">Se a qualquer momento você acredita que o status de integridade atual do hello está incorreto, você pode Fale conosco clicando **relatar status de integridade incorreto**.</span><span class="sxs-lookup"><span data-stu-id="551e4-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="551e4-139">Em casos em que será afetado por um problema do Azure, recomendamos que você toocontact suporte na folha de integridade de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="551e4-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Status incorreto do Relatório do Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="551e4-141">Informações de histórico</span><span class="sxs-lookup"><span data-stu-id="551e4-141">Historical Information</span></span>
<span data-ttu-id="551e4-142">Você pode acessar o too14 dias de dados de histórico de integridade clicando **Exibir histórico** na folha de integridade do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="551e4-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Histórico do Relatórios do Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="551e4-144">Introdução</span><span class="sxs-lookup"><span data-stu-id="551e4-144">Getting started</span></span>
<span data-ttu-id="551e4-145">tooopen integridade de recursos para um recurso</span><span class="sxs-lookup"><span data-stu-id="551e4-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="551e4-146">Entrar hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="551e4-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="551e4-147">Navegue tooyour recursos.</span><span class="sxs-lookup"><span data-stu-id="551e4-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="551e4-148">No menu de recurso Olá localizado no lado esquerdo da saudação, clique em **integridade de recursos**.</span><span class="sxs-lookup"><span data-stu-id="551e4-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Abra o Resource Health na folha Recurso](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="551e4-150">Você também pode acessar a integridade de recursos clicando **mais serviços**e digitando **integridade de recursos** na saudação de tooopen de caixa de texto de filtro **ajuda + suporte** folha.</span><span class="sxs-lookup"><span data-stu-id="551e4-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="551e4-151">Finalmente, clique em [**Resource Health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="551e4-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Abra o Resource Health em Mais serviços](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="551e4-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="551e4-153">Next steps</span></span>

<span data-ttu-id="551e4-154">Check-out toolearn esses recursos mais informações sobre a integridade de recursos:</span><span class="sxs-lookup"><span data-stu-id="551e4-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="551e4-155">Tipos de recursos e verificações de integridade no Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="551e4-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="551e4-156">Perguntas frequentes sobre o Azure Resource Health</span><span class="sxs-lookup"><span data-stu-id="551e4-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




