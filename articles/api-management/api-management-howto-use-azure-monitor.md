---
title: aaaMonitor gerenciamento de API com o Monitor do Azure | Microsoft Docs
description: "Saiba como toomonitor gerenciamento do Azure API de serviço usando o Monitor do Azure."
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
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="fdb6e-103">Monitorar o Gerenciamento de API com o Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="fdb6e-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="fdb6e-104">O Azure Monitor é um serviço do Azure que fornece uma única fonte para monitorar todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="fdb6e-105">Monitor do Azure, você pode visualizar, consultar, encaminhar, arquivar e executar ações nas métricas de saudação e logs vindos de recursos do Azure, como gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="fdb6e-106">Olá seguindo o vídeo mostra como toomonitor gerenciamento de API usando o Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="fdb6e-107">Para obter mais informações sobre o Azure Monitor, consulte [Introdução ao Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="fdb6e-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="fdb6e-108">Métricas</span><span class="sxs-lookup"><span data-stu-id="fdb6e-108">Metrics</span></span>
<span data-ttu-id="fdb6e-109">Gerenciamento de API atualmente emite cinco métricas e estamos planejando tooadd mais no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="fdb6e-110">Essas métricas são emitidas a cada minuto, fornecendo próximo visibilidade em tempo real de estado de saudação e a integridade de suas APIs.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="fdb6e-111">A seguir está um resumo das métricas de saudação:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="fdb6e-112">Total de solicitações de Gateway: o número de saudação da API de solicitações no período de saudação.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="fdb6e-113">Solicitações bem sucedidas de Gateway: número de saudação de solicitações de API que recebeu os códigos de resposta HTTP bem-sucedida incluindo 304, 307 e nada menor que 301 (por exemplo, 200).</span><span class="sxs-lookup"><span data-stu-id="fdb6e-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="fdb6e-114">Falha nas solicitações de Gateway: o número de saudação de solicitações de API que recebeu os códigos de resposta HTTP incorretos incluindo 400 e tudo o que é maior que 500.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="fdb6e-115">Solicitações não autorizadas de Gateway: número de saudação de solicitações de API que recebeu os códigos de resposta HTTP como 401, 403 e 429.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="fdb6e-116">Outras solicitações de Gateway: número de saudação de solicitações de API que recebeu os códigos de resposta HTTP que não pertencem tooany de saudação anterior categorias (por exemplo, 418).</span><span class="sxs-lookup"><span data-stu-id="fdb6e-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="fdb6e-117">É possível acessar as métricas em seu serviço de Gerenciamento de API ou acessar as métricas de todos os seus recursos do Azure no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="fdb6e-118">métricas de tooview em seu serviço de gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="fdb6e-119">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="fdb6e-120">Serviço de gerenciamento de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="fdb6e-121">Clique em **Métricas**.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-121">Click **Metrics**.</span></span>

![Folha de métricas][metrics-blade]

<span data-ttu-id="fdb6e-123">Para obter mais informações sobre como toouse métricas, consulte [visão geral das métricas].</span><span class="sxs-lookup"><span data-stu-id="fdb6e-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="fdb6e-124">Logs de atividade</span><span class="sxs-lookup"><span data-stu-id="fdb6e-124">Activity Logs</span></span>
<span data-ttu-id="fdb6e-125">Logs de atividade fornecem informações sobre operações de saudação que foram executadas em seus serviços de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="fdb6e-126">Anteriormente eles eram conhecidos como "logs de auditoria" ou "logs operacionais".</span><span class="sxs-lookup"><span data-stu-id="fdb6e-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="fdb6e-127">Usando logs de atividade, você pode determinar hello ", que e quando" para qualquer gravação as operações executadas em seus serviços de gerenciamento de API (PUT, POST, DELETE).</span><span class="sxs-lookup"><span data-stu-id="fdb6e-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="fdb6e-128">Logs de atividade não incluem operações de leitura (GET) ou as operações executadas no hello Portal clássico do publicador ou usando Olá APIs de gerenciamento original.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="fdb6e-129">É possível acessar os logs de atividades em seu serviço de Gerenciamento de API ou acessar logs de todos os seus recursos do Azure no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="fdb6e-130">logs de atividades de tooview em seu serviço de gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="fdb6e-131">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="fdb6e-132">Serviço de gerenciamento de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="fdb6e-133">Clique em **Log de atividades**.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-133">Click **Activity log**.</span></span>

![Folha Logs de atividade][activity-logs-blade]

<span data-ttu-id="fdb6e-135">Para obter mais informações sobre como toouse métricas, consulte [visão geral dos Logs de atividade].</span><span class="sxs-lookup"><span data-stu-id="fdb6e-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="fdb6e-136">Alertas</span><span class="sxs-lookup"><span data-stu-id="fdb6e-136">Alerts</span></span>
<span data-ttu-id="fdb6e-137">Você pode configurar alertas de tooreceive com base nas métricas e registros de atividades.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="fdb6e-138">Monitor do Azure permite que você tooconfigure uma saudação de alerta toodo após quando ele dispara:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="fdb6e-139">Enviar uma notificação por email</span><span class="sxs-lookup"><span data-stu-id="fdb6e-139">Send an email notification</span></span>
* <span data-ttu-id="fdb6e-140">Chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="fdb6e-140">Call a webhook</span></span>
* <span data-ttu-id="fdb6e-141">Invocar um aplicativo lógico do Azure</span><span class="sxs-lookup"><span data-stu-id="fdb6e-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="fdb6e-142">É possível configurar regras de alerta em seu serviço de Gerenciamento de API ou no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="fdb6e-143">tooconfigure-los no gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="fdb6e-144">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="fdb6e-145">Serviço de gerenciamento de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="fdb6e-146">Clique em **Regras de alerta**.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-146">Click **Alert rules**.</span></span>

![Folha Regras de alerta][alert-rules-blade]

<span data-ttu-id="fdb6e-148">Para obter mais informações sobre o uso de alertas, consulte [Overview of Alerts (Visão geral dos Alertas)].</span><span class="sxs-lookup"><span data-stu-id="fdb6e-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="fdb6e-149">Logs de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="fdb6e-149">Diagnostic Logs</span></span>
<span data-ttu-id="fdb6e-150">Os logs de diagnóstico fornecem informações avançadas sobre operações e erros importantes para auditoria, bem como para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="fdb6e-151">Os logs de diagnóstico são diferentes dos logs de atividades.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="fdb6e-152">Logs de atividade fornecem informações sobre operações de saudação que foram executadas em recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="fdb6e-153">Os Logs de Diagnóstico fornecem informações em operações que o recurso realizou por conta própria.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="fdb6e-154">Gerenciamento de API no momento fornece diagnósticos de solicitação de logs (lotes por hora) sobre API individual com cada entrada tendo Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

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

<span data-ttu-id="fdb6e-155">É possível acessar os logs de diagnóstico em seu serviço de Gerenciamento de API ou acessar logs de todos os seus recursos do Azure no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="fdb6e-156">logs de diagnóstico tooview em seu serviço de gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="fdb6e-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="fdb6e-157">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="fdb6e-158">Serviço de gerenciamento de API de tooyour go.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="fdb6e-159">Clique em **Log de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="fdb6e-159">Click **Diagnostic log**.</span></span>

![Folha Logs de Diagnóstico][diagnostic-logs-blade]

<span data-ttu-id="fdb6e-161">Para obter mais informações sobre como toouse métricas, consulte [visão geral dos Logs de diagnóstico].</span><span class="sxs-lookup"><span data-stu-id="fdb6e-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="fdb6e-162">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="fdb6e-162">Next Step</span></span>

* <span data-ttu-id="fdb6e-163">[Introdução ao Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="fdb6e-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="fdb6e-164">[visão geral das métricas]</span><span class="sxs-lookup"><span data-stu-id="fdb6e-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="fdb6e-165">[visão geral dos Logs de atividade]</span><span class="sxs-lookup"><span data-stu-id="fdb6e-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="fdb6e-166">[visão geral dos Logs de diagnóstico]</span><span class="sxs-lookup"><span data-stu-id="fdb6e-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="fdb6e-167">[Overview of Alerts (Visão geral dos Alertas)]</span><span class="sxs-lookup"><span data-stu-id="fdb6e-167">[Overview of Alerts]</span></span>

[Introdução ao Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[visão geral das métricas]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[visão geral dos Logs de atividade]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[visão geral dos Logs de diagnóstico]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Overview of Alerts (Visão geral dos Alertas)]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
