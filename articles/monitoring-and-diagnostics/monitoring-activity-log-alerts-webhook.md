---
title: "Noções básicas sobre o esquema de webhook usado em alertas do log de atividades | Microsoft Docs"
description: "Saiba mais sobre o esquema JSON que é enviado para uma URL de webhook quando um alerta do log de atividades é ativado."
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
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="18aba-103">Webhook para alertas de log de atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="18aba-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="18aba-104">Como parte da definição de um grupo de ações, você pode configurar pontos de extremidade de webhook para receber notificações de alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="18aba-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="18aba-105">Os webhooks permitem rotear uma notificação de alerta do Azure para outros sistemas para pós-processamento ou notificações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="18aba-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="18aba-106">Este artigo mostra a aparência do conteúdo para o HTTP POST para um webhook.</span><span class="sxs-lookup"><span data-stu-id="18aba-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="18aba-107">Para saber mais sobre alertas do log de atividades, veja como [Criar alertas do log de atividades do Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="18aba-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="18aba-108">Para saber mais sobre grupos de ações, veja como [criar grupos de ações](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="18aba-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="18aba-109">Autenticar o webhook</span><span class="sxs-lookup"><span data-stu-id="18aba-109">Authenticate the webhook</span></span>
<span data-ttu-id="18aba-110">Opcionalmente, o webhook pode usar a autorização baseada em token para autenticação.</span><span class="sxs-lookup"><span data-stu-id="18aba-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="18aba-111">O URI do webhook é salvo com uma ID de token, por exemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="18aba-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="18aba-112">Esquema de conteúdo</span><span class="sxs-lookup"><span data-stu-id="18aba-112">Payload schema</span></span>
<span data-ttu-id="18aba-113">O conteúdo JSON contida na operação POST difere com base no campo de data.context.activityLog.eventSource do conteúdo.</span><span class="sxs-lookup"><span data-stu-id="18aba-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="18aba-114">Comum</span><span class="sxs-lookup"><span data-stu-id="18aba-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="18aba-115">Administrativo</span><span class="sxs-lookup"><span data-stu-id="18aba-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="18aba-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="18aba-116">ServiceHealth</span></span>
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

<span data-ttu-id="18aba-117">Para obter detalhes de esquema específico sobre alertas de log de atividades de notificação do serviço integridade, veja [Notificações de integridade do serviço](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="18aba-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="18aba-118">Para obter detalhes de esquema específico em todos os outros alertas do log de atividades, veja [Visão geral do log de atividades do Azure](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="18aba-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="18aba-119">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="18aba-119">Element name</span></span> | <span data-ttu-id="18aba-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="18aba-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18aba-121">status</span><span class="sxs-lookup"><span data-stu-id="18aba-121">status</span></span> |<span data-ttu-id="18aba-122">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="18aba-122">Used for metric alerts.</span></span> <span data-ttu-id="18aba-123">Sempre definido como "ativado" para alertas do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="18aba-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="18aba-124">context</span><span class="sxs-lookup"><span data-stu-id="18aba-124">context</span></span> |<span data-ttu-id="18aba-125">Contexto do evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-125">Context of the event.</span></span> |
| <span data-ttu-id="18aba-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="18aba-126">resourceProviderName</span></span> |<span data-ttu-id="18aba-127">O provedor de recursos do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="18aba-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="18aba-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="18aba-128">conditionType</span></span> |<span data-ttu-id="18aba-129">Sempre "Evento".</span><span class="sxs-lookup"><span data-stu-id="18aba-129">Always "Event."</span></span> |
| <span data-ttu-id="18aba-130">name</span><span class="sxs-lookup"><span data-stu-id="18aba-130">name</span></span> |<span data-ttu-id="18aba-131">Nome da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="18aba-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="18aba-132">ID</span><span class="sxs-lookup"><span data-stu-id="18aba-132">id</span></span> |<span data-ttu-id="18aba-133">ID do recurso do alerta.</span><span class="sxs-lookup"><span data-stu-id="18aba-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="18aba-134">description</span><span class="sxs-lookup"><span data-stu-id="18aba-134">description</span></span> |<span data-ttu-id="18aba-135">Descrição do alerta definida quando o alerta é criado.</span><span class="sxs-lookup"><span data-stu-id="18aba-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="18aba-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="18aba-136">subscriptionId</span></span> |<span data-ttu-id="18aba-137">Id de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="18aba-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="18aba-138">timestamp</span><span class="sxs-lookup"><span data-stu-id="18aba-138">timestamp</span></span> |<span data-ttu-id="18aba-139">Hora quando o evento foi gerado pelo serviço do Azure que processou a solicitação.</span><span class="sxs-lookup"><span data-stu-id="18aba-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="18aba-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="18aba-140">resourceId</span></span> |<span data-ttu-id="18aba-141">ID de recurso do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="18aba-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="18aba-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="18aba-142">resourceGroupName</span></span> |<span data-ttu-id="18aba-143">Nome do grupo de recursos do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="18aba-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="18aba-144">propriedades</span><span class="sxs-lookup"><span data-stu-id="18aba-144">properties</span></span> |<span data-ttu-id="18aba-145">Conjunto de pares `<Key, Value>` (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="18aba-146">evento</span><span class="sxs-lookup"><span data-stu-id="18aba-146">event</span></span> |<span data-ttu-id="18aba-147">Elemento que contém metadados sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="18aba-148">autorização</span><span class="sxs-lookup"><span data-stu-id="18aba-148">authorization</span></span> |<span data-ttu-id="18aba-149">As propriedades de Controle de Acesso Baseado em Função do evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="18aba-150">Essas propriedades geralmente incluem a ação, função e escopo.</span><span class="sxs-lookup"><span data-stu-id="18aba-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="18aba-151">categoria</span><span class="sxs-lookup"><span data-stu-id="18aba-151">category</span></span> |<span data-ttu-id="18aba-152">Categoria do evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-152">Category of the event.</span></span> <span data-ttu-id="18aba-153">Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth e Recomendação.</span><span class="sxs-lookup"><span data-stu-id="18aba-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="18aba-154">chamador</span><span class="sxs-lookup"><span data-stu-id="18aba-154">caller</span></span> |<span data-ttu-id="18aba-155">Endereço de email do usuário que realizou a operação, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="18aba-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="18aba-156">Pode ser nulo para determinadas chamadas do sistema.</span><span class="sxs-lookup"><span data-stu-id="18aba-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="18aba-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="18aba-157">correlationId</span></span> |<span data-ttu-id="18aba-158">Geralmente um GUID no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="18aba-158">Usually a GUID in string format.</span></span> <span data-ttu-id="18aba-159">Eventos com correlationId pertencem à mesma ação maior e geralmente compartilham uma correlationId.</span><span class="sxs-lookup"><span data-stu-id="18aba-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="18aba-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="18aba-160">eventDescription</span></span> |<span data-ttu-id="18aba-161">Descrição de texto estático do evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-161">Static text description of the event.</span></span> |
| <span data-ttu-id="18aba-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="18aba-162">eventDataId</span></span> |<span data-ttu-id="18aba-163">Identificador exclusivo do evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="18aba-164">eventSource</span><span class="sxs-lookup"><span data-stu-id="18aba-164">eventSource</span></span> |<span data-ttu-id="18aba-165">Nome do serviço ou infraestrutura do Azure que gerou o evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="18aba-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="18aba-166">httpRequest</span></span> |<span data-ttu-id="18aba-167">A solicitação geralmente inclui o clientRequestId, clientIpAddress e método HTTP (por exemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="18aba-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="18aba-168">level</span><span class="sxs-lookup"><span data-stu-id="18aba-168">level</span></span> |<span data-ttu-id="18aba-169">Um dos seguintes valores: Crítico, Erro, Aviso, Informativo e Detalhado.</span><span class="sxs-lookup"><span data-stu-id="18aba-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="18aba-170">operationId</span><span class="sxs-lookup"><span data-stu-id="18aba-170">operationId</span></span> |<span data-ttu-id="18aba-171">Geralmente um GUID compartilhado entre os eventos correspondentes a uma única operação.</span><span class="sxs-lookup"><span data-stu-id="18aba-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="18aba-172">operationName</span><span class="sxs-lookup"><span data-stu-id="18aba-172">operationName</span></span> |<span data-ttu-id="18aba-173">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="18aba-173">Name of the operation.</span></span> |
| <span data-ttu-id="18aba-174">propriedades</span><span class="sxs-lookup"><span data-stu-id="18aba-174">properties</span></span> |<span data-ttu-id="18aba-175">Propriedades do evento.</span><span class="sxs-lookup"><span data-stu-id="18aba-175">Properties of the event.</span></span> |
| <span data-ttu-id="18aba-176">status</span><span class="sxs-lookup"><span data-stu-id="18aba-176">status</span></span> |<span data-ttu-id="18aba-177">Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="18aba-177">String.</span></span> <span data-ttu-id="18aba-178">Status da operação.</span><span class="sxs-lookup"><span data-stu-id="18aba-178">Status of the operation.</span></span> <span data-ttu-id="18aba-179">Os valores comuns incluem: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido.</span><span class="sxs-lookup"><span data-stu-id="18aba-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="18aba-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="18aba-180">subStatus</span></span> |<span data-ttu-id="18aba-181">Geralmente inclui o código de status HTTP da chamada REST correspondente.</span><span class="sxs-lookup"><span data-stu-id="18aba-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="18aba-182">Também pode incluir outras cadeias de caracteres que descrevam um substatus.</span><span class="sxs-lookup"><span data-stu-id="18aba-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="18aba-183">Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="18aba-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="18aba-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="18aba-184">Next steps</span></span>
* <span data-ttu-id="18aba-185">[Leia mais sobre o log de atividades](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="18aba-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="18aba-186">[Exemplos de scripts da automação do Azure (Runbooks) em alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="18aba-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="18aba-187">[Usar aplicativo lógico para enviar um SMS por meio do Twilio de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="18aba-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="18aba-188">Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="18aba-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="18aba-189">[Usar aplicativo lógico para enviar uma mensagem do Slack de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="18aba-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="18aba-190">Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="18aba-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="18aba-191">[Usar aplicativo lógico para enviar uma mensagem a uma fila do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="18aba-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="18aba-192">Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do log de atividades.</span><span class="sxs-lookup"><span data-stu-id="18aba-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
