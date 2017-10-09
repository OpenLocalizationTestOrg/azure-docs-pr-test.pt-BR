---
title: "esquema de webhook Olá aaaUnderstand usada em alertas de log de atividade | Microsoft Docs"
description: "Saiba mais sobre o esquema de saudação do hello JSON que é postada a URL do webhook tooa quando um alerta de log de atividade ativa."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="54964-103">Webhook para alertas de log de atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="54964-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="54964-104">Como parte da definição de saudação de um grupo de ação, você pode configurar notificações de alerta de log webhook pontos de extremidade tooreceive atividade.</span><span class="sxs-lookup"><span data-stu-id="54964-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="54964-105">Com webhooks, você pode rotear esses sistemas de tooother notificações para ações de pós-processamento ou personalizados.</span><span class="sxs-lookup"><span data-stu-id="54964-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="54964-106">Este artigo mostra quais carga Olá Olá HTTP POST tooa webhook parece.</span><span class="sxs-lookup"><span data-stu-id="54964-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="54964-107">Para obter mais informações sobre alertas de log de atividade, consulte como muito[criar alertas de log de atividades do Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="54964-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="54964-108">Para obter informações sobre grupos de ação, consulte como muito[criar grupos de ação](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="54964-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="54964-109">Autenticar Olá webhook</span><span class="sxs-lookup"><span data-stu-id="54964-109">Authenticate hello webhook</span></span>
<span data-ttu-id="54964-110">Olá webhook pode usar opcionalmente a autorização baseada em token para autenticação.</span><span class="sxs-lookup"><span data-stu-id="54964-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="54964-111">Olá webhook URI é salvo com uma ID de token, por exemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="54964-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="54964-112">Esquema de conteúdo</span><span class="sxs-lookup"><span data-stu-id="54964-112">Payload schema</span></span>
<span data-ttu-id="54964-113">carga JSON Olá contida em Olá operação POST varia com base no campo de data.context.activityLog.eventSource da carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="54964-114">Comum</span><span class="sxs-lookup"><span data-stu-id="54964-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="54964-115">Administrativo</span><span class="sxs-lookup"><span data-stu-id="54964-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="54964-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="54964-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="54964-117">Para obter detalhes de esquema específico sobre alertas de log de atividades de notificação do serviço integridade, veja [Notificações de integridade do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="54964-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="54964-118">Para obter detalhes de esquema específico em todos os outros alertas do log de atividade, consulte [visão geral do log de atividades do Azure Olá](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="54964-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="54964-119">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="54964-119">Element name</span></span> | <span data-ttu-id="54964-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="54964-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="54964-121">status</span><span class="sxs-lookup"><span data-stu-id="54964-121">status</span></span> |<span data-ttu-id="54964-122">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="54964-122">Used for metric alerts.</span></span> <span data-ttu-id="54964-123">Sempre defina muito "ativado" para alertas de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="54964-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="54964-124">context</span><span class="sxs-lookup"><span data-stu-id="54964-124">context</span></span> |<span data-ttu-id="54964-125">Contexto do evento hello.</span><span class="sxs-lookup"><span data-stu-id="54964-125">Context of hello event.</span></span> |
| <span data-ttu-id="54964-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="54964-126">resourceProviderName</span></span> |<span data-ttu-id="54964-127">provedor de recursos de saudação do hello afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="54964-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="54964-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="54964-128">conditionType</span></span> |<span data-ttu-id="54964-129">Sempre "Evento".</span><span class="sxs-lookup"><span data-stu-id="54964-129">Always "Event."</span></span> |
| <span data-ttu-id="54964-130">name</span><span class="sxs-lookup"><span data-stu-id="54964-130">name</span></span> |<span data-ttu-id="54964-131">Nome da regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="54964-132">ID</span><span class="sxs-lookup"><span data-stu-id="54964-132">id</span></span> |<span data-ttu-id="54964-133">ID do recurso de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="54964-134">description</span><span class="sxs-lookup"><span data-stu-id="54964-134">description</span></span> |<span data-ttu-id="54964-135">Descrição do alerta definida quando o alerta de saudação é criado.</span><span class="sxs-lookup"><span data-stu-id="54964-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="54964-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="54964-136">subscriptionId</span></span> |<span data-ttu-id="54964-137">Id de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="54964-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="54964-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="54964-138">timestamp</span></span> |<span data-ttu-id="54964-139">Hora na qual Olá evento foi gerado pelo saudação do serviço do Azure que processa Olá solicitação.</span><span class="sxs-lookup"><span data-stu-id="54964-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="54964-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="54964-140">resourceId</span></span> |<span data-ttu-id="54964-141">ID do recurso da saudação afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="54964-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="54964-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="54964-142">resourceGroupName</span></span> |<span data-ttu-id="54964-143">Nome do grupo de recursos de saudação para Olá afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="54964-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="54964-144">propriedades</span><span class="sxs-lookup"><span data-stu-id="54964-144">properties</span></span> |<span data-ttu-id="54964-145">Conjunto de `<Key, Value>` pares (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="54964-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="54964-146">evento</span><span class="sxs-lookup"><span data-stu-id="54964-146">event</span></span> |<span data-ttu-id="54964-147">Elemento que contém metadados sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="54964-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="54964-148">autorização</span><span class="sxs-lookup"><span data-stu-id="54964-148">authorization</span></span> |<span data-ttu-id="54964-149">Propriedades de controle de acesso baseado em função Hello de evento hello.</span><span class="sxs-lookup"><span data-stu-id="54964-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="54964-150">Geralmente, essas propriedades incluem hello ação, função hello e escopo de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="54964-151">categoria</span><span class="sxs-lookup"><span data-stu-id="54964-151">category</span></span> |<span data-ttu-id="54964-152">Categoria de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-152">Category of hello event.</span></span> <span data-ttu-id="54964-153">Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth e Recomendação.</span><span class="sxs-lookup"><span data-stu-id="54964-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="54964-154">chamador</span><span class="sxs-lookup"><span data-stu-id="54964-154">caller</span></span> |<span data-ttu-id="54964-155">Endereço de email do usuário de saudação que realizou a operação hello, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="54964-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="54964-156">Pode ser nulo para determinadas chamadas do sistema.</span><span class="sxs-lookup"><span data-stu-id="54964-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="54964-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="54964-157">correlationId</span></span> |<span data-ttu-id="54964-158">Geralmente um GUID no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="54964-158">Usually a GUID in string format.</span></span> <span data-ttu-id="54964-159">Os eventos com correlationId pertencem toohello mesma ação maior e geralmente compartilham um correlationId.</span><span class="sxs-lookup"><span data-stu-id="54964-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="54964-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="54964-160">eventDescription</span></span> |<span data-ttu-id="54964-161">Descrição de evento Olá texto estático.</span><span class="sxs-lookup"><span data-stu-id="54964-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="54964-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="54964-162">eventDataId</span></span> |<span data-ttu-id="54964-163">Identificador exclusivo do evento hello.</span><span class="sxs-lookup"><span data-stu-id="54964-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="54964-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="54964-164">eventSource</span></span> |<span data-ttu-id="54964-165">Nome do hello infraestrutura ou serviço do Azure que o evento Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="54964-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="54964-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="54964-166">httpRequest</span></span> |<span data-ttu-id="54964-167">Olá solicitação geralmente inclui Olá clientRequestId, clientIpAddress e método HTTP (por exemplo, colocar).</span><span class="sxs-lookup"><span data-stu-id="54964-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="54964-168">level</span><span class="sxs-lookup"><span data-stu-id="54964-168">level</span></span> |<span data-ttu-id="54964-169">Uma saudação valores a seguir: crítico, erro, aviso, informativo e detalhado.</span><span class="sxs-lookup"><span data-stu-id="54964-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="54964-170">operationId</span><span class="sxs-lookup"><span data-stu-id="54964-170">operationId</span></span> |<span data-ttu-id="54964-171">Normalmente um GUID compartilhado entre eventos Olá correspondente toosingle operação.</span><span class="sxs-lookup"><span data-stu-id="54964-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="54964-172">operationName</span><span class="sxs-lookup"><span data-stu-id="54964-172">operationName</span></span> |<span data-ttu-id="54964-173">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-173">Name of hello operation.</span></span> |
| <span data-ttu-id="54964-174">propriedades</span><span class="sxs-lookup"><span data-stu-id="54964-174">properties</span></span> |<span data-ttu-id="54964-175">Propriedades de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-175">Properties of hello event.</span></span> |
| <span data-ttu-id="54964-176">status</span><span class="sxs-lookup"><span data-stu-id="54964-176">status</span></span> |<span data-ttu-id="54964-177">Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="54964-177">String.</span></span> <span data-ttu-id="54964-178">Status da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-178">Status of hello operation.</span></span> <span data-ttu-id="54964-179">Os valores comuns incluem: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido.</span><span class="sxs-lookup"><span data-stu-id="54964-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="54964-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="54964-180">subStatus</span></span> |<span data-ttu-id="54964-181">Geralmente inclui o código de status HTTP saudação da chamada REST correspondente de saudação.</span><span class="sxs-lookup"><span data-stu-id="54964-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="54964-182">Também pode incluir outras cadeias de caracteres que descrevam um substatus.</span><span class="sxs-lookup"><span data-stu-id="54964-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="54964-183">Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="54964-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="54964-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54964-184">Next steps</span></span>
* <span data-ttu-id="54964-185">[Saiba mais sobre o log de atividades de saudação](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="54964-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="54964-186">[Exemplos de scripts da automação do Azure (Runbooks) em alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="54964-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="54964-187">[Usar um toosend de aplicativo um SMS por meio do Twilio lógica de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="54964-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="54964-188">Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="54964-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="54964-189">[Use um aplicativo de lógica toosend uma mensagem de margem de atraso de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="54964-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="54964-190">Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="54964-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="54964-191">[Usar um toosend do aplicativo de lógica de fila tooan uma mensagem do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="54964-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="54964-192">Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta de log de atividade.</span><span class="sxs-lookup"><span data-stu-id="54964-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
