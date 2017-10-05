---
title: Chamar um webhook em alertas do Log de Atividades do Azure | Microsoft Docs
description: "Rotear eventos de log de atividade para outros serviços para ações personalizadas. Por exemplo, envie SMS, registre bugs ou notifique uma equipe por meio do serviço de bate-papo/mensagens."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 341ab32ad0ec691285fbf1537ee298ab30156a5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="45f4c-104">Chamar um webhook em alertas do Log de Atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="45f4c-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="45f4c-105">Os webhooks permitem rotear uma notificação de alerta do Azure para outros sistemas para pós-processamento ou notificações personalizadas.</span><span class="sxs-lookup"><span data-stu-id="45f4c-105">Webhooks allow you to route an Azure alert notification to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="45f4c-106">Você pode usar um webhook em um alerta para roteá-lo aos serviços que enviam SMS, registrar bugs, notificar uma equipe por meio de serviços de bate-papo/mensagens ou qualquer outra ação.</span><span class="sxs-lookup"><span data-stu-id="45f4c-106">You can use a webhook on an alert to route it to services that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="45f4c-107">Este artigo descreve como configurar um webhook para ser chamado quando um alerta do Log de Atividades do Azure é disparado.</span><span class="sxs-lookup"><span data-stu-id="45f4c-107">This article describes how to set a webhook to be called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="45f4c-108">Também mostra a aparência do conteúdo do HTTP POST para um webhook.</span><span class="sxs-lookup"><span data-stu-id="45f4c-108">It also shows what the payload for the HTTP POST to a webhook looks like.</span></span> <span data-ttu-id="45f4c-109">Para obter informações sobre a configuração e o esquema de um alerta de métrica do Azure, [consulte esta página](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="45f4c-109">For information on the setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="45f4c-110">Você também pode configurar um alerta do Log de Atividades para enviar um email quando estiver ativado.</span><span class="sxs-lookup"><span data-stu-id="45f4c-110">You can also set up an Activity Log alert to send email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="45f4c-111">Atualmente, esse recurso está em visualização e será removido em algum momento no futuro.</span><span class="sxs-lookup"><span data-stu-id="45f4c-111">This feature is currently in preview and will be removed at some point in the future.</span></span>
>
>

<span data-ttu-id="45f4c-112">Você pode configurar um alerta do Log de Atividades usando os [Cmdlets do Azure PowerShell](insights-powershell-samples.md#create-metric-alerts), [CLI entre plataformas](insights-cli-samples.md#work-with-alerts) ou [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="45f4c-112">You can set up an Activity Log alert using the [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="45f4c-113">No momento, você não pode definir um usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="45f4c-113">Currently, you cannot set one up using the Azure portal.</span></span>

## <a name="authenticating-the-webhook"></a><span data-ttu-id="45f4c-114">Autenticação do webhook</span><span class="sxs-lookup"><span data-stu-id="45f4c-114">Authenticating the webhook</span></span>
<span data-ttu-id="45f4c-115">O webhook pode autenticar usando um destes métodos:</span><span class="sxs-lookup"><span data-stu-id="45f4c-115">The webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="45f4c-116">**Autorização baseada em token** - O URI do webhook é salvo com uma ID de token, por exemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="45f4c-116">**Token-based authorization** - The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="45f4c-117">**Autorização básica** - O URI do webhook é salvo com um nome de usuário e senha, por exemplo, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="45f4c-117">**Basic authorization** - The webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="45f4c-118">Esquema de conteúdo</span><span class="sxs-lookup"><span data-stu-id="45f4c-118">Payload schema</span></span>
<span data-ttu-id="45f4c-119">A operação POST contém o seguinte esquema e carga JSON para todos os alertas baseados em Log de Atividade.</span><span class="sxs-lookup"><span data-stu-id="45f4c-119">The POST operation contains the following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="45f4c-120">Esse esquema é semelhante àquele usado por alertas baseados em métrica.</span><span class="sxs-lookup"><span data-stu-id="45f4c-120">This schema is similar to the one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="45f4c-121">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="45f4c-121">Element Name</span></span> | <span data-ttu-id="45f4c-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="45f4c-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45f4c-123">status</span><span class="sxs-lookup"><span data-stu-id="45f4c-123">status</span></span> |<span data-ttu-id="45f4c-124">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="45f4c-124">Used for metric alerts.</span></span> <span data-ttu-id="45f4c-125">Sempre definido como "ativado" para alertas do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="45f4c-125">Always set to "activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="45f4c-126">context</span><span class="sxs-lookup"><span data-stu-id="45f4c-126">context</span></span> |<span data-ttu-id="45f4c-127">Contexto do evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-127">Context of the event.</span></span> |
| <span data-ttu-id="45f4c-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="45f4c-128">resourceProviderName</span></span> |<span data-ttu-id="45f4c-129">O provedor de recursos do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="45f4c-129">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="45f4c-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="45f4c-130">conditionType</span></span> |<span data-ttu-id="45f4c-131">Sempre "Evento".</span><span class="sxs-lookup"><span data-stu-id="45f4c-131">Always "Event."</span></span> |
| <span data-ttu-id="45f4c-132">name</span><span class="sxs-lookup"><span data-stu-id="45f4c-132">name</span></span> |<span data-ttu-id="45f4c-133">Nome da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="45f4c-133">Name of the alert rule.</span></span> |
| <span data-ttu-id="45f4c-134">ID</span><span class="sxs-lookup"><span data-stu-id="45f4c-134">id</span></span> |<span data-ttu-id="45f4c-135">ID do recurso do alerta.</span><span class="sxs-lookup"><span data-stu-id="45f4c-135">Resource ID of the alert.</span></span> |
| <span data-ttu-id="45f4c-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="45f4c-136">description</span></span> |<span data-ttu-id="45f4c-137">Descrição do alerta conforme definido durante a criação do alerta.</span><span class="sxs-lookup"><span data-stu-id="45f4c-137">Alert description as set during creation of the alert.</span></span> |
| <span data-ttu-id="45f4c-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="45f4c-138">subscriptionId</span></span> |<span data-ttu-id="45f4c-139">ID de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="45f4c-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="45f4c-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="45f4c-140">timestamp</span></span> |<span data-ttu-id="45f4c-141">Hora quando o evento foi gerado pelo serviço do Azure que processou a solicitação.</span><span class="sxs-lookup"><span data-stu-id="45f4c-141">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="45f4c-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="45f4c-142">resourceId</span></span> |<span data-ttu-id="45f4c-143">ID de recurso do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="45f4c-143">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="45f4c-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="45f4c-144">resourceGroupName</span></span> |<span data-ttu-id="45f4c-145">Nome do grupo de recursos do recurso afetado</span><span class="sxs-lookup"><span data-stu-id="45f4c-145">Name of the resource group for the impacted resource</span></span> |
| <span data-ttu-id="45f4c-146">propriedades</span><span class="sxs-lookup"><span data-stu-id="45f4c-146">properties</span></span> |<span data-ttu-id="45f4c-147">Conjunto de pares `<Key, Value>` (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="45f4c-148">evento</span><span class="sxs-lookup"><span data-stu-id="45f4c-148">event</span></span> |<span data-ttu-id="45f4c-149">Elemento que contém metadados sobre o evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-149">Element containing metadata about the event.</span></span> |
| <span data-ttu-id="45f4c-150">autorização</span><span class="sxs-lookup"><span data-stu-id="45f4c-150">authorization</span></span> |<span data-ttu-id="45f4c-151">Propriedades RBAC do evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-151">The RBAC properties of the event.</span></span> <span data-ttu-id="45f4c-152">Isso geralmente inclui a “ação”, a “função” e o “escopo”.</span><span class="sxs-lookup"><span data-stu-id="45f4c-152">These usually include the “action”, “role” and the “scope.”</span></span> |
| <span data-ttu-id="45f4c-153">categoria</span><span class="sxs-lookup"><span data-stu-id="45f4c-153">category</span></span> |<span data-ttu-id="45f4c-154">Categoria do evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-154">Category of the event.</span></span> <span data-ttu-id="45f4c-155">Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth, Recomendação.</span><span class="sxs-lookup"><span data-stu-id="45f4c-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="45f4c-156">chamador</span><span class="sxs-lookup"><span data-stu-id="45f4c-156">caller</span></span> |<span data-ttu-id="45f4c-157">Endereço de email do usuário que realizou a operação, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="45f4c-157">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="45f4c-158">Pode ser nulo para determinadas chamadas do sistema.</span><span class="sxs-lookup"><span data-stu-id="45f4c-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="45f4c-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="45f4c-159">correlationId</span></span> |<span data-ttu-id="45f4c-160">Geralmente um GUID no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="45f4c-160">Usually a GUID in string format.</span></span> <span data-ttu-id="45f4c-161">Eventos com correlationId pertencem à mesma ação maior e geralmente compartilham uma correlationId.</span><span class="sxs-lookup"><span data-stu-id="45f4c-161">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="45f4c-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="45f4c-162">eventDescription</span></span> |<span data-ttu-id="45f4c-163">Descrição de texto estático do evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-163">Static text description of the event.</span></span> |
| <span data-ttu-id="45f4c-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="45f4c-164">eventDataId</span></span> |<span data-ttu-id="45f4c-165">Identificador exclusivo do evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-165">Unique identifier for the event.</span></span> |
| <span data-ttu-id="45f4c-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="45f4c-166">eventSource</span></span> |<span data-ttu-id="45f4c-167">Nome do serviço ou infraestrutura do Azure que gerou o evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-167">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="45f4c-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="45f4c-168">httpRequest</span></span> |<span data-ttu-id="45f4c-169">Geralmente inclui a “clientRequestId”, o “clientIpAddress” e o “método” (método HTTP, como PUT, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="45f4c-169">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="45f4c-170">level</span><span class="sxs-lookup"><span data-stu-id="45f4c-170">level</span></span> |<span data-ttu-id="45f4c-171">Um dos seguintes valores: “Crítico”, “Erro”, “Aviso”, “Informativo” e “Detalhado”.</span><span class="sxs-lookup"><span data-stu-id="45f4c-171">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="45f4c-172">operationId</span><span class="sxs-lookup"><span data-stu-id="45f4c-172">operationId</span></span> |<span data-ttu-id="45f4c-173">Geralmente um GUID compartilhado entre os eventos correspondentes a uma única operação.</span><span class="sxs-lookup"><span data-stu-id="45f4c-173">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="45f4c-174">operationName</span><span class="sxs-lookup"><span data-stu-id="45f4c-174">operationName</span></span> |<span data-ttu-id="45f4c-175">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="45f4c-175">Name of the operation.</span></span> |
| <span data-ttu-id="45f4c-176">propriedades</span><span class="sxs-lookup"><span data-stu-id="45f4c-176">properties</span></span> |<span data-ttu-id="45f4c-177">Propriedades do evento.</span><span class="sxs-lookup"><span data-stu-id="45f4c-177">Properties of the event.</span></span> |
| <span data-ttu-id="45f4c-178">status</span><span class="sxs-lookup"><span data-stu-id="45f4c-178">status</span></span> |<span data-ttu-id="45f4c-179">Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="45f4c-179">String.</span></span> <span data-ttu-id="45f4c-180">Status da operação.</span><span class="sxs-lookup"><span data-stu-id="45f4c-180">Status of the operation.</span></span> <span data-ttu-id="45f4c-181">Os valores comuns incluem: "Iniciado", "Em Andamento", "Êxito", "Falha", "Ativo", "Resolvido".</span><span class="sxs-lookup"><span data-stu-id="45f4c-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="45f4c-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="45f4c-182">subStatus</span></span> |<span data-ttu-id="45f4c-183">Geralmente inclui o código de status HTTP da chamada REST correspondente.</span><span class="sxs-lookup"><span data-stu-id="45f4c-183">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="45f4c-184">Também pode incluir outras cadeias de caracteres que descrevam um substatus.</span><span class="sxs-lookup"><span data-stu-id="45f4c-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="45f4c-185">Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="45f4c-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45f4c-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45f4c-186">Next steps</span></span>
* [<span data-ttu-id="45f4c-187">Leia mais sobre o Log de Atividades</span><span class="sxs-lookup"><span data-stu-id="45f4c-187">Learn more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="45f4c-188">Exemplos de scripts da Automação do Azure (Runbooks) em alertas do Azure</span><span class="sxs-lookup"><span data-stu-id="45f4c-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="45f4c-189">[Usar aplicativo lógico para enviar um SMS por meio de Twilio de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="45f4c-189">[Use Logic App to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="45f4c-190">Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="45f4c-190">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="45f4c-191">[Usar aplicativo lógico para enviar uma mensagem do Slack de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="45f4c-191">[Use Logic App to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="45f4c-192">Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="45f4c-192">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
* <span data-ttu-id="45f4c-193">[Usar aplicativo lógico para enviar uma mensagem a uma Fila do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="45f4c-193">[Use Logic App to send a message to an Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="45f4c-194">Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="45f4c-194">This example is for metric alerts, but could be modified to work with an Activity Log alert.</span></span>
