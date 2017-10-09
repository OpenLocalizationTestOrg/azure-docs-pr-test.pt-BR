---
title: aaaCall um webhook em alertas de Log de atividades do Azure | Microsoft Docs
description: "Serviços de tooother de eventos de log de atividades para ações personalizadas de rota. Por exemplo, envie SMS, registre bugs ou notifique uma equipe por meio do serviço de bate-papo/mensagens."
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
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="174f7-104">Chamar um webhook em alertas do Log de Atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="174f7-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="174f7-105">Webhooks permitir tooroute um Azure alerta sistemas de notificação de tooother para ações de pós-processamento ou personalizados.</span><span class="sxs-lookup"><span data-stu-id="174f7-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="174f7-106">Você pode usar um webhook em um alerta tooroute-tooservices que enviar SMS, bugs de log, notificar uma equipe por meio de serviços de chat/mensagens ou fazer várias outras ações.</span><span class="sxs-lookup"><span data-stu-id="174f7-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="174f7-107">Este artigo descreve como tooset toobe um webhook chamado quando um dispara alertas de Log de atividades do Azure.</span><span class="sxs-lookup"><span data-stu-id="174f7-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="174f7-108">Ele também mostra quais carga Olá Olá HTTP POST tooa webhook parece.</span><span class="sxs-lookup"><span data-stu-id="174f7-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="174f7-109">Para obter informações sobre a instalação de saudação e esquema de um alerta de métrica do Azure, [consulte esta página em vez disso,](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="174f7-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="174f7-110">Você também pode configurar um email de alerta toosend do Log de atividades quando ativado.</span><span class="sxs-lookup"><span data-stu-id="174f7-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="174f7-111">Este recurso está atualmente em visualização e será removido em algum momento no futuro de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="174f7-112">Você pode configurar um alerta de Log de atividades usando Olá [Cmdlets do PowerShell do Azure](insights-powershell-samples.md#create-metric-alerts), [CLI de plataforma cruzada](insights-cli-samples.md#work-with-alerts), ou [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="174f7-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="174f7-113">No momento, você não pode definir um usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="174f7-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="174f7-114">Autenticando Olá webhook</span><span class="sxs-lookup"><span data-stu-id="174f7-114">Authenticating hello webhook</span></span>
<span data-ttu-id="174f7-115">Olá webhook pode autenticar usando um destes métodos:</span><span class="sxs-lookup"><span data-stu-id="174f7-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="174f7-116">**Autorização baseada em token** -Olá webhook URI é salvo com uma ID de token, por exemplo,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="174f7-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="174f7-117">**Básicas de autorização** -Olá webhook URI é salvo com um nome de usuário e senha, por exemplo,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="174f7-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="174f7-118">Esquema de conteúdo</span><span class="sxs-lookup"><span data-stu-id="174f7-118">Payload schema</span></span>
<span data-ttu-id="174f7-119">Olá operação POST contém Olá carga JSON e o esquema para alertas todas baseadas no Log de atividades a seguir.</span><span class="sxs-lookup"><span data-stu-id="174f7-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="174f7-120">Esse esquema é semelhante toohello um usado por alertas com base em métrica.</span><span class="sxs-lookup"><span data-stu-id="174f7-120">This schema is similar toohello one used by metric-based alerts.</span></span>

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

| <span data-ttu-id="174f7-121">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="174f7-121">Element Name</span></span> | <span data-ttu-id="174f7-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="174f7-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="174f7-123">status</span><span class="sxs-lookup"><span data-stu-id="174f7-123">status</span></span> |<span data-ttu-id="174f7-124">Usado para alertas de métrica.</span><span class="sxs-lookup"><span data-stu-id="174f7-124">Used for metric alerts.</span></span> <span data-ttu-id="174f7-125">Sempre defina muito "ativado" para alertas de Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="174f7-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="174f7-126">context</span><span class="sxs-lookup"><span data-stu-id="174f7-126">context</span></span> |<span data-ttu-id="174f7-127">Contexto do evento hello.</span><span class="sxs-lookup"><span data-stu-id="174f7-127">Context of hello event.</span></span> |
| <span data-ttu-id="174f7-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="174f7-128">resourceProviderName</span></span> |<span data-ttu-id="174f7-129">provedor de recursos de saudação do hello afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="174f7-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="174f7-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="174f7-130">conditionType</span></span> |<span data-ttu-id="174f7-131">Sempre "Evento".</span><span class="sxs-lookup"><span data-stu-id="174f7-131">Always "Event."</span></span> |
| <span data-ttu-id="174f7-132">name</span><span class="sxs-lookup"><span data-stu-id="174f7-132">name</span></span> |<span data-ttu-id="174f7-133">Nome da regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="174f7-134">ID</span><span class="sxs-lookup"><span data-stu-id="174f7-134">id</span></span> |<span data-ttu-id="174f7-135">ID do recurso de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="174f7-136">description</span><span class="sxs-lookup"><span data-stu-id="174f7-136">description</span></span> |<span data-ttu-id="174f7-137">Descrição do alerta conforme definido durante a criação de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="174f7-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="174f7-138">subscriptionId</span></span> |<span data-ttu-id="174f7-139">ID de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="174f7-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="174f7-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="174f7-140">timestamp</span></span> |<span data-ttu-id="174f7-141">Hora na qual Olá evento foi gerado pelo saudação do serviço do Azure que processa Olá solicitação.</span><span class="sxs-lookup"><span data-stu-id="174f7-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="174f7-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="174f7-142">resourceId</span></span> |<span data-ttu-id="174f7-143">ID do recurso da saudação afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="174f7-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="174f7-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="174f7-144">resourceGroupName</span></span> |<span data-ttu-id="174f7-145">Nome do grupo de recursos de saudação para Olá afetado recursos</span><span class="sxs-lookup"><span data-stu-id="174f7-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="174f7-146">propriedades</span><span class="sxs-lookup"><span data-stu-id="174f7-146">properties</span></span> |<span data-ttu-id="174f7-147">Conjunto de `<Key, Value>` pares (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="174f7-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="174f7-148">evento</span><span class="sxs-lookup"><span data-stu-id="174f7-148">event</span></span> |<span data-ttu-id="174f7-149">Elemento que contém metadados sobre o evento hello.</span><span class="sxs-lookup"><span data-stu-id="174f7-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="174f7-150">autorização</span><span class="sxs-lookup"><span data-stu-id="174f7-150">authorization</span></span> |<span data-ttu-id="174f7-151">propriedades RBAC saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="174f7-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="174f7-152">Isso geralmente inclui hello "ação", "função" hello "escopo e."</span><span class="sxs-lookup"><span data-stu-id="174f7-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="174f7-153">categoria</span><span class="sxs-lookup"><span data-stu-id="174f7-153">category</span></span> |<span data-ttu-id="174f7-154">Categoria de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-154">Category of hello event.</span></span> <span data-ttu-id="174f7-155">Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth, Recomendação.</span><span class="sxs-lookup"><span data-stu-id="174f7-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="174f7-156">chamador</span><span class="sxs-lookup"><span data-stu-id="174f7-156">caller</span></span> |<span data-ttu-id="174f7-157">Endereço de email do usuário de saudação que realizou a operação hello, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="174f7-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="174f7-158">Pode ser nulo para determinadas chamadas do sistema.</span><span class="sxs-lookup"><span data-stu-id="174f7-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="174f7-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="174f7-159">correlationId</span></span> |<span data-ttu-id="174f7-160">Geralmente um GUID no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="174f7-160">Usually a GUID in string format.</span></span> <span data-ttu-id="174f7-161">Os eventos com correlationId pertencem toohello mesma ação maior e geralmente compartilham um correlationId.</span><span class="sxs-lookup"><span data-stu-id="174f7-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="174f7-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="174f7-162">eventDescription</span></span> |<span data-ttu-id="174f7-163">Descrição de evento Olá texto estático.</span><span class="sxs-lookup"><span data-stu-id="174f7-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="174f7-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="174f7-164">eventDataId</span></span> |<span data-ttu-id="174f7-165">Identificador exclusivo do evento hello.</span><span class="sxs-lookup"><span data-stu-id="174f7-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="174f7-166">eventSource</span><span class="sxs-lookup"><span data-stu-id="174f7-166">eventSource</span></span> |<span data-ttu-id="174f7-167">Nome do hello infraestrutura ou serviço do Azure que o evento Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="174f7-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="174f7-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="174f7-168">httpRequest</span></span> |<span data-ttu-id="174f7-169">Geralmente inclui "clientRequestId" Olá, "clientIpAddress" e "método" (método HTTP, como PUT).</span><span class="sxs-lookup"><span data-stu-id="174f7-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="174f7-170">level</span><span class="sxs-lookup"><span data-stu-id="174f7-170">level</span></span> |<span data-ttu-id="174f7-171">Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado".</span><span class="sxs-lookup"><span data-stu-id="174f7-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="174f7-172">operationId</span><span class="sxs-lookup"><span data-stu-id="174f7-172">operationId</span></span> |<span data-ttu-id="174f7-173">Normalmente um GUID compartilhado entre eventos Olá correspondente toosingle operação.</span><span class="sxs-lookup"><span data-stu-id="174f7-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="174f7-174">operationName</span><span class="sxs-lookup"><span data-stu-id="174f7-174">operationName</span></span> |<span data-ttu-id="174f7-175">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-175">Name of hello operation.</span></span> |
| <span data-ttu-id="174f7-176">propriedades</span><span class="sxs-lookup"><span data-stu-id="174f7-176">properties</span></span> |<span data-ttu-id="174f7-177">Propriedades de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-177">Properties of hello event.</span></span> |
| <span data-ttu-id="174f7-178">status</span><span class="sxs-lookup"><span data-stu-id="174f7-178">status</span></span> |<span data-ttu-id="174f7-179">Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="174f7-179">String.</span></span> <span data-ttu-id="174f7-180">Status da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-180">Status of hello operation.</span></span> <span data-ttu-id="174f7-181">Os valores comuns incluem: "Iniciado", "Em Andamento", "Êxito", "Falha", "Ativo", "Resolvido".</span><span class="sxs-lookup"><span data-stu-id="174f7-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="174f7-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="174f7-182">subStatus</span></span> |<span data-ttu-id="174f7-183">Geralmente inclui o código de status HTTP saudação da chamada REST correspondente de saudação.</span><span class="sxs-lookup"><span data-stu-id="174f7-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="174f7-184">Também pode incluir outras cadeias de caracteres que descrevam um substatus.</span><span class="sxs-lookup"><span data-stu-id="174f7-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="174f7-185">Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="174f7-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="174f7-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="174f7-186">Next steps</span></span>
* [<span data-ttu-id="174f7-187">Saiba mais sobre Olá Log de atividades</span><span class="sxs-lookup"><span data-stu-id="174f7-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="174f7-188">Exemplos de scripts da Automação do Azure (Runbooks) em alertas do Azure</span><span class="sxs-lookup"><span data-stu-id="174f7-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="174f7-189">[Use o aplicativo lógico toosend um SMS por meio do Twilio em um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="174f7-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="174f7-190">Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta do Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="174f7-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="174f7-191">[Use o aplicativo lógico toosend uma mensagem de margem de atraso de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="174f7-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="174f7-192">Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta do Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="174f7-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="174f7-193">[Use o aplicativo lógico toosend tooan uma mensagem fila do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="174f7-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="174f7-194">Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta do Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="174f7-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
