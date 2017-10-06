---
title: Esquema de evento do Log de atividade de aaaAzure | Microsoft Docs
description: "Entender o esquema de evento Olá para dados emitidas em Olá Log de atividades"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="0020b-103">Esquema sobre eventos do Log de Atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="0020b-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="0020b-104">Olá **o Log de atividades do Azure** é um log que fornece informações sobre quaisquer eventos de nível de assinatura que ocorreram no Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="0020b-105">Este artigo descreve o esquema de evento Olá por categoria de dados.</span><span class="sxs-lookup"><span data-stu-id="0020b-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="0020b-106">Administrativo</span><span class="sxs-lookup"><span data-stu-id="0020b-106">Administrative</span></span>
<span data-ttu-id="0020b-107">Esta categoria contém registro Olá de todos os criar, operações de atualização, exclusão e a ação executada por meio do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0020b-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="0020b-108">Exemplos de saudação tipos de eventos que você vê nessa categoria incluem "criar a máquina virtual" e "Excluir grupo de segurança de rede" cada ação tomada por um usuário ou aplicativo usando o Gerenciador de recursos é modelado como uma operação em um tipo de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="0020b-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="0020b-109">Se o tipo de operação de saudação é gravar, Delete ou ação, registros de saudação do início de saudação e o sucesso ou falha da operação são registradas na categoria administrativa hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="0020b-110">categoria administrativa Olá também inclui qualquer controle de acesso baseado em toorole alterações em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="0020b-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="0020b-111">Evento de exemplo</span><span class="sxs-lookup"><span data-stu-id="0020b-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="0020b-112">Descrições de propriedade</span><span class="sxs-lookup"><span data-stu-id="0020b-112">Property descriptions</span></span>
| <span data-ttu-id="0020b-113">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0020b-113">Element Name</span></span> | <span data-ttu-id="0020b-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="0020b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0020b-115">autorização</span><span class="sxs-lookup"><span data-stu-id="0020b-115">authorization</span></span> |<span data-ttu-id="0020b-116">Blob de propriedades RBAC do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="0020b-117">Geralmente inclui propriedades de "ação", "função" e "escopo" hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="0020b-118">chamador</span><span class="sxs-lookup"><span data-stu-id="0020b-118">caller</span></span> |<span data-ttu-id="0020b-119">Endereço de email do usuário de saudação que executou a operação de hello, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0020b-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="0020b-120">canais</span><span class="sxs-lookup"><span data-stu-id="0020b-120">channels</span></span> |<span data-ttu-id="0020b-121">Uma saudação valores a seguir: "Admin", "Operação"</span><span class="sxs-lookup"><span data-stu-id="0020b-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="0020b-122">declarações</span><span class="sxs-lookup"><span data-stu-id="0020b-122">claims</span></span> |<span data-ttu-id="0020b-123">token JWT Olá usado pelo Active Directory tooauthenticate Olá usuário ou aplicativo tooperform esta operação no Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0020b-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="0020b-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="0020b-124">correlationId</span></span> |<span data-ttu-id="0020b-125">Normalmente um GUID no formato de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="0020b-126">Os eventos que compartilham um correlationId pertencem toohello mesma ação uber.</span><span class="sxs-lookup"><span data-stu-id="0020b-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="0020b-127">description</span><span class="sxs-lookup"><span data-stu-id="0020b-127">description</span></span> |<span data-ttu-id="0020b-128">Descrição de texto estático de um evento.</span><span class="sxs-lookup"><span data-stu-id="0020b-128">Static text description of an event.</span></span> |
| <span data-ttu-id="0020b-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="0020b-129">eventDataId</span></span> |<span data-ttu-id="0020b-130">Identificador exclusivo de um evento.</span><span class="sxs-lookup"><span data-stu-id="0020b-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="0020b-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="0020b-131">httpRequest</span></span> |<span data-ttu-id="0020b-132">Blob Olá descrevendo solicitação Http.</span><span class="sxs-lookup"><span data-stu-id="0020b-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="0020b-133">Geralmente inclui "clientRequestId" Olá, "clientIpAddress" e "método" (método HTTP.</span><span class="sxs-lookup"><span data-stu-id="0020b-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="0020b-134">Por exemplo, PUT).</span><span class="sxs-lookup"><span data-stu-id="0020b-134">For example, PUT).</span></span> |
| <span data-ttu-id="0020b-135">level</span><span class="sxs-lookup"><span data-stu-id="0020b-135">level</span></span> |<span data-ttu-id="0020b-136">Nível de evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-136">Level of hello event.</span></span> <span data-ttu-id="0020b-137">Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"</span><span class="sxs-lookup"><span data-stu-id="0020b-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="0020b-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0020b-138">resourceGroupName</span></span> |<span data-ttu-id="0020b-139">Nome do grupo de recursos de saudação para Olá afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="0020b-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="0020b-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="0020b-140">resourceProviderName</span></span> |<span data-ttu-id="0020b-141">Nome do provedor de recursos Olá Olá afetado recursos</span><span class="sxs-lookup"><span data-stu-id="0020b-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="0020b-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="0020b-142">resourceId</span></span> |<span data-ttu-id="0020b-143">Id do recurso da saudação afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="0020b-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="0020b-144">operationId</span><span class="sxs-lookup"><span data-stu-id="0020b-144">operationId</span></span> |<span data-ttu-id="0020b-145">Um GUID compartilhado entre eventos Olá correspondentes tooa única operação.</span><span class="sxs-lookup"><span data-stu-id="0020b-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="0020b-146">operationName</span><span class="sxs-lookup"><span data-stu-id="0020b-146">operationName</span></span> |<span data-ttu-id="0020b-147">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-147">Name of hello operation.</span></span> |
| <span data-ttu-id="0020b-148">propriedades</span><span class="sxs-lookup"><span data-stu-id="0020b-148">properties</span></span> |<span data-ttu-id="0020b-149">Conjunto de `<Key, Value>` pares (ou seja, um dicionário) que descreve os detalhes de saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="0020b-150">status</span><span class="sxs-lookup"><span data-stu-id="0020b-150">status</span></span> |<span data-ttu-id="0020b-151">Cadeia de caracteres que descreve o status de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="0020b-152">Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido.</span><span class="sxs-lookup"><span data-stu-id="0020b-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="0020b-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="0020b-153">subStatus</span></span> |<span data-ttu-id="0020b-154">Geralmente Olá código de status HTTP da saudação correspondente chamada REST, mas também pode incluir outras cadeias de caracteres que descrevam um substatus, como esses valores comuns: Okey (código de Status HTTP: 200), criado (código de Status HTTP: 201), aceito (código de Status HTTP: 202), nenhum conteúdo (HTTP Código de status: 204), solicitação incorreta (código de Status HTTP: 400), não encontrado (código de Status HTTP: 404), conflito (código de Status HTTP: 409), erro de servidor interno (código de Status HTTP: 500), o Service não está disponível (código de Status HTTP: 503), tempo limite do Gateway (código de Status HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="0020b-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="0020b-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-155">eventTimestamp</span></span> |<span data-ttu-id="0020b-156">Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="0020b-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-157">submissionTimestamp</span></span> |<span data-ttu-id="0020b-158">Carimbo de hora do evento Olá se tornaram disponível para consulta.</span><span class="sxs-lookup"><span data-stu-id="0020b-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="0020b-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0020b-159">subscriptionId</span></span> |<span data-ttu-id="0020b-160">ID de Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="0020b-161">Integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="0020b-161">Service health</span></span>
<span data-ttu-id="0020b-162">Essa categoria contém o registro de saudação de qualquer incidente de integridade do serviço que ocorreram no Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="0020b-163">Um exemplo de tipo de saudação do evento que você vê nessa categoria é "SQL Azure no Leste dos EUA está passando por tempo de inatividade."</span><span class="sxs-lookup"><span data-stu-id="0020b-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="0020b-164">Eventos de serviço de integridade são fornecidos em cinco variedades: ação necessária, recuperação assistida, incidente, manutenção, informações ou segurança e só aparecerá se você tiver um recurso na assinatura de saudação que será afetada pelo evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="0020b-165">Evento de exemplo</span><span class="sxs-lookup"><span data-stu-id="0020b-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="0020b-166">Descrições de propriedade</span><span class="sxs-lookup"><span data-stu-id="0020b-166">Property descriptions</span></span>
<span data-ttu-id="0020b-167">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0020b-167">Element Name</span></span> | <span data-ttu-id="0020b-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="0020b-168">Description</span></span>
-------- | -----------
<span data-ttu-id="0020b-169">canais</span><span class="sxs-lookup"><span data-stu-id="0020b-169">channels</span></span> | <span data-ttu-id="0020b-170">É uma saudação valores a seguir: "Admin", "Operação"</span><span class="sxs-lookup"><span data-stu-id="0020b-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="0020b-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="0020b-171">correlationId</span></span> | <span data-ttu-id="0020b-172">É geralmente um GUID no formato de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="0020b-173">Eventos que pertencem a mesma ação uber geralmente compartilham de toohello Olá mesma correlationId.</span><span class="sxs-lookup"><span data-stu-id="0020b-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="0020b-174">description</span><span class="sxs-lookup"><span data-stu-id="0020b-174">description</span></span> | <span data-ttu-id="0020b-175">Descrição do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-175">Description of hello event.</span></span>
<span data-ttu-id="0020b-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="0020b-176">eventDataId</span></span> | <span data-ttu-id="0020b-177">Olá identificador exclusivo de um evento.</span><span class="sxs-lookup"><span data-stu-id="0020b-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="0020b-178">eventName</span><span class="sxs-lookup"><span data-stu-id="0020b-178">eventName</span></span> | <span data-ttu-id="0020b-179">título de saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-179">hello title of hello event.</span></span>
<span data-ttu-id="0020b-180">level</span><span class="sxs-lookup"><span data-stu-id="0020b-180">level</span></span> | <span data-ttu-id="0020b-181">Nível de evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-181">Level of hello event.</span></span> <span data-ttu-id="0020b-182">Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"</span><span class="sxs-lookup"><span data-stu-id="0020b-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="0020b-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="0020b-183">resourceProviderName</span></span> | <span data-ttu-id="0020b-184">Nome do provedor de recursos Olá Olá afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="0020b-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="0020b-185">Se não for conhecido, será nulo.</span><span class="sxs-lookup"><span data-stu-id="0020b-185">If not known, this will be null.</span></span>
<span data-ttu-id="0020b-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="0020b-186">resourceType</span></span>| <span data-ttu-id="0020b-187">tipo de saudação do recurso de saudação afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="0020b-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="0020b-188">Se não for conhecido, será nulo.</span><span class="sxs-lookup"><span data-stu-id="0020b-188">If not known, this will be null.</span></span>
<span data-ttu-id="0020b-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="0020b-189">subStatus</span></span> | <span data-ttu-id="0020b-190">Geralmente é null para eventos de Integridade do Serviço.</span><span class="sxs-lookup"><span data-stu-id="0020b-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="0020b-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-191">eventTimestamp</span></span> | <span data-ttu-id="0020b-192">Carimbo de hora do evento de log Olá foi gerado e enviado toohello Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="0020b-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="0020b-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-193">submissionTimestamp</span></span> |   <span data-ttu-id="0020b-194">Carimbo de hora do evento Olá foi disponibilizado em Olá Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="0020b-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="0020b-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0020b-195">subscriptionId</span></span> | <span data-ttu-id="0020b-196">Olá assinatura do Azure na qual este evento foi registrado.</span><span class="sxs-lookup"><span data-stu-id="0020b-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="0020b-197">status</span><span class="sxs-lookup"><span data-stu-id="0020b-197">status</span></span> | <span data-ttu-id="0020b-198">Cadeia de caracteres que descreve o status de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="0020b-199">Alguns valores comuns são: Ativo, Resolvido.</span><span class="sxs-lookup"><span data-stu-id="0020b-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="0020b-200">operationName</span><span class="sxs-lookup"><span data-stu-id="0020b-200">operationName</span></span> | <span data-ttu-id="0020b-201">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-201">Name of hello operation.</span></span> <span data-ttu-id="0020b-202">Normalmente Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="0020b-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="0020b-203">categoria</span><span class="sxs-lookup"><span data-stu-id="0020b-203">category</span></span> | <span data-ttu-id="0020b-204">“ServiceHealth”</span><span class="sxs-lookup"><span data-stu-id="0020b-204">"ServiceHealth"</span></span>
<span data-ttu-id="0020b-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="0020b-205">resourceId</span></span> | <span data-ttu-id="0020b-206">Id do recurso da saudação afetada recurso, se conhecido.</span><span class="sxs-lookup"><span data-stu-id="0020b-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="0020b-207">Caso contrário, a ID da assinatura é fornecida.</span><span class="sxs-lookup"><span data-stu-id="0020b-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="0020b-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="0020b-208">Properties.title</span></span> | <span data-ttu-id="0020b-209">Olá localizado título para essa comunicação.</span><span class="sxs-lookup"><span data-stu-id="0020b-209">hello localized title for this communication.</span></span> <span data-ttu-id="0020b-210">Inglês é o idioma padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-210">English is hello default language.</span></span>
<span data-ttu-id="0020b-211">Properties.communication</span><span class="sxs-lookup"><span data-stu-id="0020b-211">Properties.communication</span></span> | <span data-ttu-id="0020b-212">Olá localizado detalhes de comunicação de saudação com marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="0020b-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="0020b-213">Inglês é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-213">English is hello default.</span></span>
<span data-ttu-id="0020b-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="0020b-214">Properties.incidentType</span></span> | <span data-ttu-id="0020b-215">Possíveis valores: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span><span class="sxs-lookup"><span data-stu-id="0020b-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="0020b-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="0020b-216">Properties.trackingId</span></span> | <span data-ttu-id="0020b-217">Identifica o incidente Olá que esse evento está associado.</span><span class="sxs-lookup"><span data-stu-id="0020b-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="0020b-218">Use este incidente de tooan relacionados toocorrelate Olá eventos.</span><span class="sxs-lookup"><span data-stu-id="0020b-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="0020b-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="0020b-219">Properties.impactedServices</span></span> | <span data-ttu-id="0020b-220">Um blob com caracteres de escape do JSON que descreve os serviços de saudação e regiões que são afetados pelo incidente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="0020b-221">Uma lista de Services, que, individualmente, tem um ServiceName e uma lista de ImpactedRegions, que têm um RegionName.</span><span class="sxs-lookup"><span data-stu-id="0020b-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="0020b-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="0020b-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="0020b-223">comunicação de saudação em inglês</span><span class="sxs-lookup"><span data-stu-id="0020b-223">hello communication in English</span></span>
<span data-ttu-id="0020b-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="0020b-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="0020b-225">comunicação de saudação em inglês como marcação html ou como texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="0020b-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="0020b-226">Properties.stage</span><span class="sxs-lookup"><span data-stu-id="0020b-226">Properties.stage</span></span> | <span data-ttu-id="0020b-227">Os possíveis valores para AssistedRecovery, ActionRequired, Information, Incident e Security são Active e Resolved.</span><span class="sxs-lookup"><span data-stu-id="0020b-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="0020b-228">Para Maintenance, eles são: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span><span class="sxs-lookup"><span data-stu-id="0020b-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="0020b-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="0020b-229">Properties.communicationId</span></span> | <span data-ttu-id="0020b-230">comunicação Olá esse evento está associado.</span><span class="sxs-lookup"><span data-stu-id="0020b-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="0020b-231">Alerta</span><span class="sxs-lookup"><span data-stu-id="0020b-231">Alert</span></span>
<span data-ttu-id="0020b-232">Essa categoria contém o registro de saudação de todas as ativações de alertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="0020b-233">Um exemplo desse tipo de saudação do evento que você vê nessa categoria é "% da CPU em myVM 80 para hello nos últimos 5 minutos."</span><span class="sxs-lookup"><span data-stu-id="0020b-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="0020b-234">Uma variedade de sistemas do Azure têm um conceito de alerta – você pode definir uma regra de algum tipo e receber uma notificação quando as condições corresponderem a essa regra.</span><span class="sxs-lookup"><span data-stu-id="0020b-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="0020b-235">Cada vez que um tipo de alerta com suporte do Azure 'ativa,' ou condições hello são atendido toogenerate uma notificação, um registro de ativação de saudação também é enviada por push toothis categoria de saudação Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="0020b-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="0020b-236">Evento de exemplo</span><span class="sxs-lookup"><span data-stu-id="0020b-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="0020b-237">Descrições de propriedade</span><span class="sxs-lookup"><span data-stu-id="0020b-237">Property descriptions</span></span>
| <span data-ttu-id="0020b-238">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0020b-238">Element Name</span></span> | <span data-ttu-id="0020b-239">Descrição</span><span class="sxs-lookup"><span data-stu-id="0020b-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0020b-240">chamador</span><span class="sxs-lookup"><span data-stu-id="0020b-240">caller</span></span> | <span data-ttu-id="0020b-241">Always Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="0020b-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="0020b-242">canais</span><span class="sxs-lookup"><span data-stu-id="0020b-242">channels</span></span> | <span data-ttu-id="0020b-243">Sempre "Administrador, Operação"</span><span class="sxs-lookup"><span data-stu-id="0020b-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="0020b-244">declarações</span><span class="sxs-lookup"><span data-stu-id="0020b-244">claims</span></span> | <span data-ttu-id="0020b-245">Blob JSON com as tipo hello SPN (nome principal do serviço) ou de recurso, do mecanismo de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="0020b-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="0020b-246">correlationId</span></span> | <span data-ttu-id="0020b-247">Um GUID no formato de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="0020b-248">description</span><span class="sxs-lookup"><span data-stu-id="0020b-248">description</span></span> |<span data-ttu-id="0020b-249">Descrição de alerta de evento Olá texto estático.</span><span class="sxs-lookup"><span data-stu-id="0020b-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="0020b-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="0020b-250">eventDataId</span></span> |<span data-ttu-id="0020b-251">Identificador exclusivo do evento de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="0020b-252">level</span><span class="sxs-lookup"><span data-stu-id="0020b-252">level</span></span> |<span data-ttu-id="0020b-253">Nível de evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-253">Level of hello event.</span></span> <span data-ttu-id="0020b-254">Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"</span><span class="sxs-lookup"><span data-stu-id="0020b-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="0020b-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0020b-255">resourceGroupName</span></span> |<span data-ttu-id="0020b-256">Nome do grupo de recursos de saudação para Olá afetados recurso se ele é um alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="0020b-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="0020b-257">Para outros tipos de alerta, esse é o nome de Olá Olá do grupo de recursos que contém o alerta de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="0020b-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="0020b-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="0020b-258">resourceProviderName</span></span> |<span data-ttu-id="0020b-259">Nome do provedor de recursos Olá Olá afetados recurso se ele é um alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="0020b-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="0020b-260">Para outros tipos de alerta, este é o nome de saudação do provedor de recursos de saudação para alerta Olá em si.</span><span class="sxs-lookup"><span data-stu-id="0020b-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="0020b-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="0020b-261">resourceId</span></span> | <span data-ttu-id="0020b-262">Nome da ID de recurso Olá para Olá afetados recurso se ele é um alerta de métrica.</span><span class="sxs-lookup"><span data-stu-id="0020b-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="0020b-263">Para outros tipos de alerta, isso é o ID de recurso de saudação do recurso de alerta de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="0020b-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="0020b-264">operationId</span><span class="sxs-lookup"><span data-stu-id="0020b-264">operationId</span></span> |<span data-ttu-id="0020b-265">Um GUID compartilhado entre eventos Olá correspondentes tooa única operação.</span><span class="sxs-lookup"><span data-stu-id="0020b-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="0020b-266">operationName</span><span class="sxs-lookup"><span data-stu-id="0020b-266">operationName</span></span> |<span data-ttu-id="0020b-267">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-267">Name of hello operation.</span></span> |
| <span data-ttu-id="0020b-268">propriedades</span><span class="sxs-lookup"><span data-stu-id="0020b-268">properties</span></span> |<span data-ttu-id="0020b-269">Conjunto de `<Key, Value>` pares (ou seja, um dicionário) que descreve os detalhes de saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="0020b-270">status</span><span class="sxs-lookup"><span data-stu-id="0020b-270">status</span></span> |<span data-ttu-id="0020b-271">Cadeia de caracteres que descreve o status de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="0020b-272">Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido.</span><span class="sxs-lookup"><span data-stu-id="0020b-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="0020b-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="0020b-273">subStatus</span></span> | <span data-ttu-id="0020b-274">Geralmente é null para alertas.</span><span class="sxs-lookup"><span data-stu-id="0020b-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="0020b-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-275">eventTimestamp</span></span> |<span data-ttu-id="0020b-276">Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="0020b-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-277">submissionTimestamp</span></span> |<span data-ttu-id="0020b-278">Carimbo de hora do evento Olá se tornaram disponível para consulta.</span><span class="sxs-lookup"><span data-stu-id="0020b-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="0020b-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0020b-279">subscriptionId</span></span> |<span data-ttu-id="0020b-280">ID de Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="0020b-281">Campo de propriedades por tipo de alerta</span><span class="sxs-lookup"><span data-stu-id="0020b-281">Properties field per alert type</span></span>
<span data-ttu-id="0020b-282">campo de propriedades Olá conterá valores diferentes dependendo da fonte de saudação do alerta de evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="0020b-283">Dois provedores de alerta de evento comuns são alertas do Log de Atividades e de métrica.</span><span class="sxs-lookup"><span data-stu-id="0020b-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="0020b-284">Propriedades de alertas do Log de Atividades</span><span class="sxs-lookup"><span data-stu-id="0020b-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="0020b-285">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0020b-285">Element Name</span></span> | <span data-ttu-id="0020b-286">Descrição</span><span class="sxs-lookup"><span data-stu-id="0020b-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0020b-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0020b-287">properties.subscriptionId</span></span> | <span data-ttu-id="0020b-288">ID de assinatura de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="0020b-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="0020b-289">properties.eventDataId</span></span> | <span data-ttu-id="0020b-290">Olá evento ID de dados de evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="0020b-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="0020b-291">properties.resourceGroup</span></span> | <span data-ttu-id="0020b-292">grupo de recursos de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="0020b-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="0020b-293">properties.resourceId</span></span> | <span data-ttu-id="0020b-294">ID do recurso de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="0020b-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-295">properties.eventTimestamp</span></span> | <span data-ttu-id="0020b-296">Olá carimbo de hora de eventos do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="0020b-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="0020b-297">properties.operationName</span></span> | <span data-ttu-id="0020b-298">nome da operação de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="0020b-299">properties.status</span><span class="sxs-lookup"><span data-stu-id="0020b-299">properties.status</span></span> | <span data-ttu-id="0020b-300">status de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.</span><span class="sxs-lookup"><span data-stu-id="0020b-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="0020b-301">Propriedades de alertas de métrica</span><span class="sxs-lookup"><span data-stu-id="0020b-301">Properties for metric alerts</span></span>
| <span data-ttu-id="0020b-302">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0020b-302">Element Name</span></span> | <span data-ttu-id="0020b-303">Descrição</span><span class="sxs-lookup"><span data-stu-id="0020b-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0020b-304">properties.RuleUri</span><span class="sxs-lookup"><span data-stu-id="0020b-304">properties.RuleUri</span></span> | <span data-ttu-id="0020b-305">ID do recurso de saudação métrica regra de alerta em si.</span><span class="sxs-lookup"><span data-stu-id="0020b-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="0020b-306">properties.RuleName</span><span class="sxs-lookup"><span data-stu-id="0020b-306">properties.RuleName</span></span> | <span data-ttu-id="0020b-307">nome de saudação da regra de alerta métrica hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="0020b-308">properties.RuleDescription</span><span class="sxs-lookup"><span data-stu-id="0020b-308">properties.RuleDescription</span></span> | <span data-ttu-id="0020b-309">Descrição de saudação da regra de alerta métrica hello (conforme definido na regra de alerta de saudação).</span><span class="sxs-lookup"><span data-stu-id="0020b-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="0020b-310">properties.Threshold</span><span class="sxs-lookup"><span data-stu-id="0020b-310">properties.Threshold</span></span> | <span data-ttu-id="0020b-311">valor de limite de saudação usado na avaliação de saudação da regra de alerta métrica hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="0020b-312">properties.WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="0020b-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="0020b-313">tamanho da janela Olá usado na avaliação de saudação da regra de alerta métrica hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="0020b-314">properties.Aggregation</span><span class="sxs-lookup"><span data-stu-id="0020b-314">properties.Aggregation</span></span> | <span data-ttu-id="0020b-315">tipo de agregação Olá definido na regra de alerta métrica hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="0020b-316">properties.Operator</span><span class="sxs-lookup"><span data-stu-id="0020b-316">properties.Operator</span></span> | <span data-ttu-id="0020b-317">operador condicional Olá usada na avaliação de saudação da regra de alerta métrica hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="0020b-318">properties.MetricName</span><span class="sxs-lookup"><span data-stu-id="0020b-318">properties.MetricName</span></span> | <span data-ttu-id="0020b-319">nome da métrica Olá da métrica de saudação usada na avaliação de saudação da regra de alerta métrica hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="0020b-320">properties.MetricUnit</span><span class="sxs-lookup"><span data-stu-id="0020b-320">properties.MetricUnit</span></span> | <span data-ttu-id="0020b-321">unidade de métrica Olá para métrica de saudação usada na avaliação de saudação da regra de alerta métrica Olá.</span><span class="sxs-lookup"><span data-stu-id="0020b-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="0020b-322">Autoscale</span><span class="sxs-lookup"><span data-stu-id="0020b-322">Autoscale</span></span>
<span data-ttu-id="0020b-323">Esta categoria contém registro Olá de qualquer operação de toohello relacionados de eventos do mecanismo de dimensionamento automático de saudação com base em quaisquer configurações de dimensionamento automático que você definiu na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0020b-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="0020b-324">Um exemplo desse tipo de saudação do evento que você vê nessa categoria é "Escala de dimensionamento automático das ações de falha".</span><span class="sxs-lookup"><span data-stu-id="0020b-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="0020b-325">Usar o dimensionamento automático, você pode automaticamente expansão ou escala em Olá o número de instâncias em um tipo de recurso com suporte com base na hora do dia e/ou carregar dados (métricas) usando uma configuração de AutoEscala.</span><span class="sxs-lookup"><span data-stu-id="0020b-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="0020b-326">Quando Olá condições tooscale para cima ou para baixo, Olá início e foi bem-sucedida ou eventos com falha serão registrados nessa categoria.</span><span class="sxs-lookup"><span data-stu-id="0020b-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="0020b-327">Evento de exemplo</span><span class="sxs-lookup"><span data-stu-id="0020b-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="0020b-328">Descrições de propriedade</span><span class="sxs-lookup"><span data-stu-id="0020b-328">Property descriptions</span></span>
| <span data-ttu-id="0020b-329">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="0020b-329">Element Name</span></span> | <span data-ttu-id="0020b-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="0020b-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0020b-331">chamador</span><span class="sxs-lookup"><span data-stu-id="0020b-331">caller</span></span> | <span data-ttu-id="0020b-332">Always Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="0020b-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="0020b-333">canais</span><span class="sxs-lookup"><span data-stu-id="0020b-333">channels</span></span> | <span data-ttu-id="0020b-334">Sempre "Administrador, Operação"</span><span class="sxs-lookup"><span data-stu-id="0020b-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="0020b-335">declarações</span><span class="sxs-lookup"><span data-stu-id="0020b-335">claims</span></span> | <span data-ttu-id="0020b-336">Blob JSON com tipo de recurso ou o SPN (nome principal do serviço), do mecanismo de dimensionamento automático de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="0020b-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="0020b-337">correlationId</span></span> | <span data-ttu-id="0020b-338">Um GUID no formato de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="0020b-339">description</span><span class="sxs-lookup"><span data-stu-id="0020b-339">description</span></span> |<span data-ttu-id="0020b-340">Descrição de texto estático do evento de dimensionamento automático de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="0020b-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="0020b-341">eventDataId</span></span> |<span data-ttu-id="0020b-342">Identificador exclusivo do evento de dimensionamento automático hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="0020b-343">level</span><span class="sxs-lookup"><span data-stu-id="0020b-343">level</span></span> |<span data-ttu-id="0020b-344">Nível de evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-344">Level of hello event.</span></span> <span data-ttu-id="0020b-345">Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"</span><span class="sxs-lookup"><span data-stu-id="0020b-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="0020b-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0020b-346">resourceGroupName</span></span> |<span data-ttu-id="0020b-347">Nome do grupo de recursos de saudação para configuração de dimensionamento automático de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="0020b-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="0020b-348">resourceProviderName</span></span> |<span data-ttu-id="0020b-349">Nome do provedor de recursos de saudação para configuração de dimensionamento automático hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="0020b-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="0020b-350">resourceId</span></span> |<span data-ttu-id="0020b-351">Id do recurso de configuração de dimensionamento automático hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="0020b-352">operationId</span><span class="sxs-lookup"><span data-stu-id="0020b-352">operationId</span></span> |<span data-ttu-id="0020b-353">Um GUID compartilhado entre eventos Olá correspondentes tooa única operação.</span><span class="sxs-lookup"><span data-stu-id="0020b-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="0020b-354">operationName</span><span class="sxs-lookup"><span data-stu-id="0020b-354">operationName</span></span> |<span data-ttu-id="0020b-355">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-355">Name of hello operation.</span></span> |
| <span data-ttu-id="0020b-356">propriedades</span><span class="sxs-lookup"><span data-stu-id="0020b-356">properties</span></span> |<span data-ttu-id="0020b-357">Conjunto de `<Key, Value>` pares (ou seja, um dicionário) que descreve os detalhes de saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0020b-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="0020b-358">properties.Description</span><span class="sxs-lookup"><span data-stu-id="0020b-358">properties.Description</span></span> | <span data-ttu-id="0020b-359">Descrição detalhada do qual o mecanismo de dimensionamento automático Olá estava fazendo.</span><span class="sxs-lookup"><span data-stu-id="0020b-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="0020b-360">properties.ResourceName</span><span class="sxs-lookup"><span data-stu-id="0020b-360">properties.ResourceName</span></span> | <span data-ttu-id="0020b-361">ID do recurso da saudação afetado recursos (Olá recursos no qual Olá ação de escala estava sendo executada)</span><span class="sxs-lookup"><span data-stu-id="0020b-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="0020b-362">properties.OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="0020b-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="0020b-363">número de saudação de instâncias antes da ação de dimensionamento automático hello está em vigor.</span><span class="sxs-lookup"><span data-stu-id="0020b-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="0020b-364">properties.NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="0020b-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="0020b-365">número de saudação de instâncias após a ação de dimensionamento automático hello está em vigor.</span><span class="sxs-lookup"><span data-stu-id="0020b-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="0020b-366">properties.LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="0020b-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="0020b-367">Olá carimbo de hora de quando a ação de dimensionamento automático Olá ocorreu.</span><span class="sxs-lookup"><span data-stu-id="0020b-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="0020b-368">status</span><span class="sxs-lookup"><span data-stu-id="0020b-368">status</span></span> |<span data-ttu-id="0020b-369">Cadeia de caracteres que descreve o status de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0020b-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="0020b-370">Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido.</span><span class="sxs-lookup"><span data-stu-id="0020b-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="0020b-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="0020b-371">subStatus</span></span> | <span data-ttu-id="0020b-372">Geralmente é null para dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="0020b-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="0020b-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-373">eventTimestamp</span></span> |<span data-ttu-id="0020b-374">Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="0020b-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="0020b-375">submissionTimestamp</span></span> |<span data-ttu-id="0020b-376">Carimbo de hora do evento Olá se tornaram disponível para consulta.</span><span class="sxs-lookup"><span data-stu-id="0020b-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="0020b-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0020b-377">subscriptionId</span></span> |<span data-ttu-id="0020b-378">ID de Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0020b-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0020b-379">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0020b-379">Next steps</span></span>
* [<span data-ttu-id="0020b-380">Saiba mais sobre hello (anteriormente conhecida como Logs de auditoria) do Log de atividades</span><span class="sxs-lookup"><span data-stu-id="0020b-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="0020b-381">Fluxo de tooEvent de Log de atividades do Azure Olá Hubs</span><span class="sxs-lookup"><span data-stu-id="0020b-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
