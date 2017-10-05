---
title: "Visão Geral do Azure Monitor| Microsoft Docs"
description: "O Azure Monitor coleta estatísticas para uso em alertas, webhooks, dimensionamento automático e automação. O artigo também lista outras opções de monitoramento da Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: 619a004b9aff99be68988e1f7be3ccad400a8a0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="a4583-104">Visão geral do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="a4583-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="a4583-105">Este artigo fornece uma visão geral do Serviço do Azure Monitor no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4583-105">This article provides an overview of the Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="a4583-106">Ele aborda o que o Azure Monitor faz e fornece ponteiros para informações adicionais sobre como usar o Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="a4583-106">It discusses what Azure Monitor does and provides pointers to additional information on how to use Azure Monitor.</span></span>  <span data-ttu-id="a4583-107">Se preferir uma introdução em vídeo, consulte os links em Próximas etapas no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a4583-107">If you prefer a video introduction, see Next steps links at the bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="a4583-108">Por que monitorar seu aplicativo ou sistema</span><span class="sxs-lookup"><span data-stu-id="a4583-108">Why monitor your application or system</span></span>
<span data-ttu-id="a4583-109">Os aplicativos em nuvem são complexos com muitas partes móveis.</span><span class="sxs-lookup"><span data-stu-id="a4583-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="a4583-110">O monitoramento fornece dados para garantir que seu aplicativo permaneça ativo e em execução em um estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="a4583-110">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="a4583-111">Ele também ajuda a afastar os problemas potenciais ou solucionar problemas antigos.</span><span class="sxs-lookup"><span data-stu-id="a4583-111">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="a4583-112">Além disso, você pode usar os dados de monitoramento para obter mais informações sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a4583-112">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="a4583-113">Esse conhecimento pode ajudá-lo a melhorar o desempenho ou a capacidade de manutenção do aplicativo ou automatizar ações que normalmente exigiriam intervenção manual.</span><span class="sxs-lookup"><span data-stu-id="a4583-113">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="a4583-114">Azure Monitor e outros produtos de monitoramento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="a4583-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="a4583-115">O Azure Monitor fornece logs e métricas de infraestrutura de nível básico para a maioria dos serviços do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4583-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="a4583-116">Os serviços do Azure que ainda não colocam seus dados no Azure Monitor o farão no futuro.</span><span class="sxs-lookup"><span data-stu-id="a4583-116">Azure services that do not yet put their data into Azure Monitor will put it there in the future.</span></span>

<span data-ttu-id="a4583-117">A Microsoft fornece produtos e serviços adicionais que oferecem mais recursos de monitoramento para desenvolvedores, DevOps ou operações de TI que também têm instalações locais.</span><span class="sxs-lookup"><span data-stu-id="a4583-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="a4583-118">Para ter uma compreensão e visão geral de como esses diferentes produtos e serviços funcionam juntos, consulte [Monitoramento no Microsoft Azure](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4583-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="a4583-119">Fontes de monitoramento – Computação</span><span class="sxs-lookup"><span data-stu-id="a4583-119">Monitoring Sources - Compute</span></span>

![Modelo para o monitoramento e diagnóstico dos recursos não de computação](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="a4583-121">Os serviços de Computação incluem</span><span class="sxs-lookup"><span data-stu-id="a4583-121">The Compute services include</span></span> 
- <span data-ttu-id="a4583-122">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="a4583-122">Cloud Services</span></span> 
- <span data-ttu-id="a4583-123">Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="a4583-123">Virtual Machines</span></span> 
- <span data-ttu-id="a4583-124">Conjuntos de escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="a4583-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="a4583-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a4583-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="a4583-126">Aplicativo - Logs de Diagnóstico, Logs de Aplicativo e Métrica</span><span class="sxs-lookup"><span data-stu-id="a4583-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="a4583-127">Os aplicativos podem ser executados sobre o SO convidado no modelo de computação.</span><span class="sxs-lookup"><span data-stu-id="a4583-127">Applications can run on top of the Guest OS in the compute model.</span></span> <span data-ttu-id="a4583-128">Eles emitem seu próprio conjunto de métricas e logs.</span><span class="sxs-lookup"><span data-stu-id="a4583-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="a4583-129">O Azure Monitor se baseia na extensão de diagnóstico do Azure (Windows ou Linux) para coletar a maioria dos logs e métricas de nível do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a4583-129">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="a4583-130">Os tipos incluem</span><span class="sxs-lookup"><span data-stu-id="a4583-130">The types include</span></span>

* <span data-ttu-id="a4583-131">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="a4583-131">Performance counters</span></span>
* <span data-ttu-id="a4583-132">Logs de aplicativo</span><span class="sxs-lookup"><span data-stu-id="a4583-132">Application Logs</span></span>
* <span data-ttu-id="a4583-133">Logs de Eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="a4583-133">Windows Event Logs</span></span>
* <span data-ttu-id="a4583-134">Fonte de evento do .NET</span><span class="sxs-lookup"><span data-stu-id="a4583-134">.NET Event Source</span></span>
* <span data-ttu-id="a4583-135">Logs IIS</span><span class="sxs-lookup"><span data-stu-id="a4583-135">IIS Logs</span></span>
* <span data-ttu-id="a4583-136">Manifesto com base no ETW</span><span class="sxs-lookup"><span data-stu-id="a4583-136">Manifest based ETW</span></span>
* <span data-ttu-id="a4583-137">Despejos de Falha</span><span class="sxs-lookup"><span data-stu-id="a4583-137">Crash Dumps</span></span>
* <span data-ttu-id="a4583-138">Logs de Erro do Cliente</span><span class="sxs-lookup"><span data-stu-id="a4583-138">Customer Error Logs</span></span>

<span data-ttu-id="a4583-139">Sem a extensão de diagnóstico, somente algumas métricas, como o uso da CPU, estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a4583-139">Without the diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="a4583-140">Métricas de VM host e convidada</span><span class="sxs-lookup"><span data-stu-id="a4583-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="a4583-141">Os recursos de computação listados anteriormente têm uma VM host dedicada e SO convidado com que interagem.</span><span class="sxs-lookup"><span data-stu-id="a4583-141">The previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="a4583-142">A VM host e o SO convidado são equivalentes à VM raiz e à VM convidada no modelo de hipervisor Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a4583-142">The host VM and guest OS are the equivalent of root VM and guest VM in the Hyper-V hypervisor model.</span></span> <span data-ttu-id="a4583-143">Você pode coletar métricas sobre ambos.</span><span class="sxs-lookup"><span data-stu-id="a4583-143">You can collect metrics on both.</span></span> <span data-ttu-id="a4583-144">Você também pode coletar logs de diagnóstico sobre o SO convidado.</span><span class="sxs-lookup"><span data-stu-id="a4583-144">You can also collect diagnostics logs on the guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="a4583-145">Log de Atividade</span><span class="sxs-lookup"><span data-stu-id="a4583-145">Activity Log</span></span>
<span data-ttu-id="a4583-146">Você pode pesquisar o Log de atividade (anteriormente chamado de Logs de auditoria ou operacionais) para obter informações sobre o recurso como visto pela infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4583-146">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> <span data-ttu-id="a4583-147">O log contém informações como os horários quando os recursos são criados ou destruídos.</span><span class="sxs-lookup"><span data-stu-id="a4583-147">The log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="a4583-148">Para obter mais informações, consulte [Visão geral do log de atividades](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a4583-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="a4583-149">Fontes de monitoramento – todo o restante</span><span class="sxs-lookup"><span data-stu-id="a4583-149">Monitoring Sources - everything else</span></span>

![Modelo para o monitoramento e diagnóstico dos recursos de computação](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="a4583-151">Recursos - Métricas e Logs de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="a4583-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="a4583-152">As métricas e logs de diagnóstico que podem ser coletados variam com base no tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a4583-152">Collectable metrics and diagnostics logs vary based on the resource type.</span></span> <span data-ttu-id="a4583-153">Por exemplo, os Aplicativos Web fornecem estatísticas sobre E/S de disco e Porcentagem da CPU.</span><span class="sxs-lookup"><span data-stu-id="a4583-153">For example, Web Apps provides statistics on the Disk IO and Percent CPU.</span></span> <span data-ttu-id="a4583-154">Essas métricas não existem para uma fila do Barramento de Serviço, que, em vez disso, fornece métricas como tamanho da fila e taxa de transferência de mensagem.</span><span class="sxs-lookup"><span data-stu-id="a4583-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="a4583-155">Uma lista de métricas que podem ser coletadas para cada recurso está disponível em [métricas com suporte](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a4583-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="a4583-156">Métricas de VM host e convidada</span><span class="sxs-lookup"><span data-stu-id="a4583-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="a4583-157">Não há necessariamente um mapeamento individual entre o recurso e uma determinada VM host ou convidada, portanto, as métricas não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a4583-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="a4583-158">Log de Atividade</span><span class="sxs-lookup"><span data-stu-id="a4583-158">Activity Log</span></span>
<span data-ttu-id="a4583-159">O log de atividades é igual ao dos recursos de computação.</span><span class="sxs-lookup"><span data-stu-id="a4583-159">The activity log is the same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="a4583-160">Usos dos Dados de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="a4583-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="a4583-161">Depois de coletar os dados, você pode fazer o seguinte com eles no Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="a4583-161">Once you collect your data, you can do the following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="a4583-162">Rota</span><span class="sxs-lookup"><span data-stu-id="a4583-162">Route</span></span>
<span data-ttu-id="a4583-163">Você pode transmitir os dados de monitoramento para outros locais em tempo real.</span><span class="sxs-lookup"><span data-stu-id="a4583-163">You can stream monitoring data to other locations in real time.</span></span>

<span data-ttu-id="a4583-164">Os exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="a4583-164">Examples include:</span></span>

- <span data-ttu-id="a4583-165">Enviar para o Application Insights para que você possa usar ferramentas mais avançadas de visualização e análise.</span><span class="sxs-lookup"><span data-stu-id="a4583-165">Send to Application Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="a4583-166">Enviar para os Hubs de Eventos para que você possa rotear para ferramentas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="a4583-166">Send to Event Hubs so you can route to third-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="a4583-167">Armazenar e arquivar</span><span class="sxs-lookup"><span data-stu-id="a4583-167">Store and Archive</span></span>
<span data-ttu-id="a4583-168">Alguns dados de monitoramento já ficam armazenados e disponíveis no Azure Monitor por um período determinado.</span><span class="sxs-lookup"><span data-stu-id="a4583-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="a4583-169">As métricas são armazenadas por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="a4583-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="a4583-170">As entradas do log de atividades são armazenadas por 90 dias.</span><span class="sxs-lookup"><span data-stu-id="a4583-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="a4583-171">Logs de diagnóstico não são armazenados.</span><span class="sxs-lookup"><span data-stu-id="a4583-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="a4583-172">Se quiser armazenar dados por mais tempo que os períodos listados acima, você poderá usar um armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4583-172">If you want to store data longer than the time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="a4583-173">Os dados de monitoramento são mantidos em sua conta de armazenamento com base em uma política de retenção que você definir.</span><span class="sxs-lookup"><span data-stu-id="a4583-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="a4583-174">Você precisa pagar pelo espaço os dados ocupam no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4583-174">You do have to pay for the space the data takes up in Azure storage.</span></span> 

<span data-ttu-id="a4583-175">Algumas formas de usar esses dados:</span><span class="sxs-lookup"><span data-stu-id="a4583-175">A few ways to use this data:</span></span>

- <span data-ttu-id="a4583-176">Uma vez gravados, você pode ter outras ferramentas dentro ou fora do Azure para lê-los e processá-los.</span><span class="sxs-lookup"><span data-stu-id="a4583-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="a4583-177">Você baixa os dados localmente para um arquivo local ou altera a política de retenção na nuvem para manter os dados por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="a4583-177">You download the data locally for a local archive or change your retention policy in the cloud to keep data for extended periods of time.</span></span>  
- <span data-ttu-id="a4583-178">Deixe os dados no armazenamento do Azure indefinidamente para fins de arquivamento.</span><span class="sxs-lookup"><span data-stu-id="a4583-178">You leave the data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="a4583-179">Consultar</span><span class="sxs-lookup"><span data-stu-id="a4583-179">Query</span></span>
<span data-ttu-id="a4583-180">Você pode usar a API REST do Azure Monitor, comandos de CLI (interface de linha de comando) entre plataformas, cmdlets do PowerShell ou o SDK do .NET para acessar os dados no sistema ou no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a4583-180">You can use the Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or the .NET SDK to access the data in the system or Azure storage</span></span>

<span data-ttu-id="a4583-181">Alguns exemplos incluem: </span><span class="sxs-lookup"><span data-stu-id="a4583-181">Examples include:</span></span>

* <span data-ttu-id="a4583-182">Obtendo dados para um aplicativo de monitoramento personalizado escrito por você</span><span class="sxs-lookup"><span data-stu-id="a4583-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="a4583-183">Criando consultas personalizadas e enviando esses dados para um aplicativo de terceiros.</span><span class="sxs-lookup"><span data-stu-id="a4583-183">Creating custom queries and sending that data to a third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="a4583-184">Visualizar</span><span class="sxs-lookup"><span data-stu-id="a4583-184">Visualize</span></span>
<span data-ttu-id="a4583-185">Visualizar os dados de monitoramento em gráficos ajuda a localizar tendências mais rapidamente do que examinar os dados em si.</span><span class="sxs-lookup"><span data-stu-id="a4583-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through the data itself.</span></span>  

<span data-ttu-id="a4583-186">Alguns métodos de visualização incluem:</span><span class="sxs-lookup"><span data-stu-id="a4583-186">A few visualization methods include:</span></span>

* <span data-ttu-id="a4583-187">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a4583-187">Use the Azure portal</span></span>
* <span data-ttu-id="a4583-188">Rotear os dados para Application Insights do Azure</span><span class="sxs-lookup"><span data-stu-id="a4583-188">Route data to Azure Application Insights</span></span>
* <span data-ttu-id="a4583-189">Rotear os dados para o Microsoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="a4583-189">Route data to Microsoft PowerBI</span></span>
* <span data-ttu-id="a4583-190">Rotear os dados para uma ferramenta de visualização de terceiros usando a transmissão ao vivo ou com a ferramenta de leitura de um arquivo no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a4583-190">Route the data to a third-party visualization tool using either live streaming or by having the tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="a4583-191">Automatizar</span><span class="sxs-lookup"><span data-stu-id="a4583-191">Automate</span></span>
<span data-ttu-id="a4583-192">Você pode usar os dados de monitoramento para disparar alertas ou até processos inteiros.</span><span class="sxs-lookup"><span data-stu-id="a4583-192">You can use monitoring data to trigger alerts or even whole processes.</span></span> <span data-ttu-id="a4583-193">Os exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="a4583-193">Examples include:</span></span>

* <span data-ttu-id="a4583-194">Use os dados para dimensionar automaticamente as instâncias de computação com base na carga do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a4583-194">Use data to autoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="a4583-195">Envie emails quando uma métrica passar de um limite predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a4583-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="a4583-196">Chame uma URL da Web (webhook) para executar uma ação em um sistema fora do Azure</span><span class="sxs-lookup"><span data-stu-id="a4583-196">Call a web URL (webhook) to execute an action in a system outside of Azure</span></span>
* <span data-ttu-id="a4583-197">Inicie um runbook na automação do Azure para executar quaisquer tarefas</span><span class="sxs-lookup"><span data-stu-id="a4583-197">Start a runbook in Azure automation to perform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="a4583-198">Métodos para acessar o Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="a4583-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="a4583-199">Em geral, você pode manipular o controle, roteamento e recuperação dos dados usando um dos métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a4583-199">In general, you can manipulate data tracking, routing, and retrieval using one of the following methods.</span></span> <span data-ttu-id="a4583-200">Nem todos os métodos estão disponíveis para todas as ações ou tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="a4583-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="a4583-201">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a4583-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="a4583-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4583-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="a4583-203">CLI (Interface de linha de comando) de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="a4583-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="a4583-204">API REST</span><span class="sxs-lookup"><span data-stu-id="a4583-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="a4583-205">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a4583-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="a4583-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4583-206">Next steps</span></span>
<span data-ttu-id="a4583-207">Saiba mais sobre</span><span class="sxs-lookup"><span data-stu-id="a4583-207">Learn more about</span></span>
- <span data-ttu-id="a4583-208">Um passo a passo em vídeo do Azure Monitor está disponível em</span><span class="sxs-lookup"><span data-stu-id="a4583-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="a4583-209">[Introdução ao Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span><span class="sxs-lookup"><span data-stu-id="a4583-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="a4583-210">Um vídeo adicional explicando um cenário no qual você pode usar o Azure Monitor está disponível em [Explore o monitoramento e diagnósticos no Microsoft Azure](https://channel9.msdn.com/events/Ignite/2016/BRK2234) e [Azure Monitor em um vídeo do Ignite 2016](https://myignite.microsoft.com/videos/4977)</span><span class="sxs-lookup"><span data-stu-id="a4583-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="a4583-211">Percorra a interface do Azure Monitor na [Introdução ao Azure Monitor](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a4583-211">Run through the Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="a4583-212">Configure as [Extensões de Diagnóstico do Azure](../azure-diagnostics.md) se você estiver tentando diagnosticar problemas em seu Serviço de Nuvem, Máquina Virtual, conjunto de dimensionamento de máquinas virtuais ou aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a4583-212">Set up the [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting to diagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="a4583-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) se você tiver problemas de diagnóstico em seu aplicativo Web do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a4583-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying to diagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="a4583-214">[Solucionar de problemas no Armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md) ao usar os Blobs, Tabelas ou Filas de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a4583-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="a4583-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) e [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="a4583-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and the [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
