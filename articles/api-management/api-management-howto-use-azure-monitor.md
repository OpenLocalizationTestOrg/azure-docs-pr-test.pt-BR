---
title: Monitorar o Gerenciamento de API com o Azure Monitor| Microsoft Docs
description: "Saiba como monitorar o serviço de Gerenciamento de API do Azure usando o Azure Monitor."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="45d54-103">Monitorar o Gerenciamento de API com o Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="45d54-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="45d54-104">O Azure Monitor é um serviço do Azure que fornece uma única fonte para monitorar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d54-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="45d54-105">Com o Azure Monitor, é possível visualizar, consultar, rotear, arquivar e executar ações nas métricas e nos logs provenientes dos recursos do Azure como o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="45d54-106">O vídeo a seguir mostra como monitorar o Gerenciamento de API usando o Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="45d54-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="45d54-107">Para obter mais informações sobre o Azure Monitor, consulte [Introdução ao Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="45d54-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="45d54-108">Métricas</span><span class="sxs-lookup"><span data-stu-id="45d54-108">Metrics</span></span>
<span data-ttu-id="45d54-109">No momento, o Gerenciamento de API emite cinco métricas e estamos planejando adicionar mais no futuro.</span><span class="sxs-lookup"><span data-stu-id="45d54-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="45d54-110">Essas métricas são emitidas a cada minuto, fornecendo uma visibilidade quase em tempo real do estado e da integridade de suas APIs.</span><span class="sxs-lookup"><span data-stu-id="45d54-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="45d54-111">A seguir, há um resumo das métricas:</span><span class="sxs-lookup"><span data-stu-id="45d54-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="45d54-112">Total de solicitações de gateway: o número de solicitações de API no período.</span><span class="sxs-lookup"><span data-stu-id="45d54-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="45d54-113">Solicitações de gateway bem-sucedidas: o número de solicitações de API que recebeu códigos de resposta HTTP bem-sucedidos, incluindo 304, 307 e unidades menores que 301 (por exemplo, 200).</span><span class="sxs-lookup"><span data-stu-id="45d54-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="45d54-114">Solicitações de gateway com falha: o número de solicitações de API que recebeu códigos de resposta HTTP errôneos, incluindo 400 e qualquer coisa maior do que 500.</span><span class="sxs-lookup"><span data-stu-id="45d54-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="45d54-115">Solicitações de gateway não autorizadas: o número de solicitações de API que recebeu códigos de resposta HTTP, incluindo 401, 403 e 429.</span><span class="sxs-lookup"><span data-stu-id="45d54-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="45d54-116">Outras solicitações de gateway: o número de solicitações de API que recebeu códigos de resposta HTTP que não pertencem a nenhuma das categorias acima (por exemplo, 418).</span><span class="sxs-lookup"><span data-stu-id="45d54-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="45d54-117">É possível acessar as métricas em seu serviço de Gerenciamento de API ou acessar as métricas de todos os seus recursos do Azure no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="45d54-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="45d54-118">Para exibir as métricas em seu serviço de Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="45d54-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="45d54-119">Abra o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d54-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="45d54-120">Acesse seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="45d54-121">Clique em **Métricas**.</span><span class="sxs-lookup"><span data-stu-id="45d54-121">Click **Metrics**.</span></span>

![Folha de métricas][metrics-blade]

<span data-ttu-id="45d54-123">Para obter mais informações sobre como usar as métricas, consulte [Overview of Metrics (Visão geral das Métricas)].</span><span class="sxs-lookup"><span data-stu-id="45d54-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="45d54-124">Logs de atividade</span><span class="sxs-lookup"><span data-stu-id="45d54-124">Activity Logs</span></span>
<span data-ttu-id="45d54-125">Os logs de atividades fornecem informações sobre as operações que foram realizadas em seus serviços de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="45d54-126">Anteriormente eles eram conhecidos como "logs de auditoria" ou "logs operacionais".</span><span class="sxs-lookup"><span data-stu-id="45d54-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="45d54-127">Usando logs de atividades, é possível determinar “o que, quem e quando” para quaisquer operações de gravação (PUT, POST, DELETE) realizadas em seus serviços de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="45d54-128">Os logs de atividades não incluem operações de leitura (GET) ou operações realizadas no Portal do Publicador clássico ou usando as APIs de gerenciamento original.</span><span class="sxs-lookup"><span data-stu-id="45d54-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="45d54-129">É possível acessar os logs de atividades em seu serviço de Gerenciamento de API ou acessar logs de todos os seus recursos do Azure no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="45d54-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="45d54-130">Para exibir os logs de atividades em seu serviço de Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="45d54-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="45d54-131">Abra o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d54-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="45d54-132">Acesse seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="45d54-133">Clique em **Log de atividades**.</span><span class="sxs-lookup"><span data-stu-id="45d54-133">Click **Activity log**.</span></span>

![Folha Logs de atividade][activity-logs-blade]

<span data-ttu-id="45d54-135">Para obter mais informações sobre como usar métricas, consulte [Overview of Activity Logs (Visão geral dos Logs de Atividades)].</span><span class="sxs-lookup"><span data-stu-id="45d54-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="45d54-136">Alertas</span><span class="sxs-lookup"><span data-stu-id="45d54-136">Alerts</span></span>
<span data-ttu-id="45d54-137">É possível configurar para receber alertas com base em métricas e logs de atividades.</span><span class="sxs-lookup"><span data-stu-id="45d54-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="45d54-138">O Azure Monitor permite configurar um alerta para que ele faça o seguinte quando for acionado:</span><span class="sxs-lookup"><span data-stu-id="45d54-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="45d54-139">Enviar uma notificação por email</span><span class="sxs-lookup"><span data-stu-id="45d54-139">Send an email notification</span></span>
* <span data-ttu-id="45d54-140">Chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="45d54-140">Call a webhook</span></span>
* <span data-ttu-id="45d54-141">Invocar um aplicativo lógico do Azure</span><span class="sxs-lookup"><span data-stu-id="45d54-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="45d54-142">É possível configurar regras de alerta em seu serviço de Gerenciamento de API ou no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="45d54-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="45d54-143">Para configurá-los no Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="45d54-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="45d54-144">Abra o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d54-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="45d54-145">Acesse seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="45d54-146">Clique em **Regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="45d54-146">Click **Alert rules**.</span></span>

![Folha Regras de alerta][alert-rules-blade]

<span data-ttu-id="45d54-148">Para obter mais informações sobre o uso de alertas, consulte [Overview of Alerts (Visão geral dos Alertas)].</span><span class="sxs-lookup"><span data-stu-id="45d54-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="45d54-149">Logs de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="45d54-149">Diagnostic Logs</span></span>
<span data-ttu-id="45d54-150">Os logs de diagnóstico fornecem informações avançadas sobre operações e erros importantes para auditoria, bem como para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="45d54-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="45d54-151">Os logs de diagnóstico são diferentes dos logs de atividades.</span><span class="sxs-lookup"><span data-stu-id="45d54-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="45d54-152">Os logs de atividades fornecem informações sobre as operações realizadas em seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d54-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="45d54-153">Os Logs de Diagnóstico fornecem informações em operações que o recurso realizou por conta própria.</span><span class="sxs-lookup"><span data-stu-id="45d54-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="45d54-154">No momento, o Gerenciamento de API oferece logs de diagnóstico (agrupados por hora) sobre a solicitação de API individual em que cada entrada que tem a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="45d54-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="45d54-155">É possível acessar os logs de diagnóstico em seu serviço de Gerenciamento de API ou acessar logs de todos os seus recursos do Azure no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="45d54-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="45d54-156">Para exibir os logs de diagnóstico em seu serviço de Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="45d54-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="45d54-157">Abra o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45d54-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="45d54-158">Acesse seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="45d54-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="45d54-159">Clique em **Log de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="45d54-159">Click **Diagnostic log**.</span></span>

![Folha Logs de Diagnóstico][diagnostic-logs-blade]

<span data-ttu-id="45d54-161">Para obter mais informações sobre como usar métricas, consulte [Overview of Diagnostic Logs (Visão geral dos Logs de Diagnóstico)].</span><span class="sxs-lookup"><span data-stu-id="45d54-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="45d54-162">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="45d54-162">Next Step</span></span>

* <span data-ttu-id="45d54-163">[Introdução ao Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="45d54-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="45d54-164">[Overview of Metrics (Visão geral das Métricas)]</span><span class="sxs-lookup"><span data-stu-id="45d54-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="45d54-165">[Overview of Activity Logs (Visão geral dos Logs de Atividades)]</span><span class="sxs-lookup"><span data-stu-id="45d54-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="45d54-166">[Overview of Diagnostic Logs (Visão geral dos Logs de Diagnóstico)]</span><span class="sxs-lookup"><span data-stu-id="45d54-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="45d54-167">[Overview of Alerts (Visão geral dos Alertas)]</span><span class="sxs-lookup"><span data-stu-id="45d54-167">[Overview of Alerts]</span></span>

<span data-ttu-id="45d54-168">[Introdução ao Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="45d54-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="45d54-169">[Overview of Metrics (Visão geral das Métricas)]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="45d54-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="45d54-170">[Overview of Activity Logs (Visão geral dos Logs de Atividades)]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="45d54-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="45d54-171">[Overview of Diagnostic Logs (Visão geral dos Logs de Diagnóstico)]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="45d54-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="45d54-172">[Overview of Alerts (Visão geral dos Alertas)]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="45d54-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
