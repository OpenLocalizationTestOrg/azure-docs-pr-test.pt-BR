---
title: "autenticação e segurança de grade de eventos aaaAzure"
description: Descreve a Grade de Eventos do Azure e seus conceitos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="a7d46-103">Segurança e autenticação da Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="a7d46-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="a7d46-104">A Grade de Eventos do Azure tem três tipos de autenticação:</span><span class="sxs-lookup"><span data-stu-id="a7d46-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="a7d46-105">Assinaturas de evento</span><span class="sxs-lookup"><span data-stu-id="a7d46-105">Event subscriptions</span></span>
* <span data-ttu-id="a7d46-106">Publicação de evento</span><span class="sxs-lookup"><span data-stu-id="a7d46-106">Event publishing</span></span>
* <span data-ttu-id="a7d46-107">Entrega de eventos do WebHook</span><span class="sxs-lookup"><span data-stu-id="a7d46-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="a7d46-108">Entrega de eventos do WebHook</span><span class="sxs-lookup"><span data-stu-id="a7d46-108">WebHook Event delivery</span></span>

<span data-ttu-id="a7d46-109">Webhooks são um dos muitos eventos tooreceive de maneiras em tempo real da grade de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7d46-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="a7d46-110">Sempre que houver um novo toobe pronto do evento entregue, grade de eventos envia uma solicitação HTTP com tooyour WebHook com o evento Olá no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="a7d46-111">Quando você registra seu próprio ponto de extremidade de WebHook com a grade de eventos, envia uma solicitação POST com um código de validação simples na propriedade de ponto de extremidade de tooprove de ordem.</span><span class="sxs-lookup"><span data-stu-id="a7d46-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="a7d46-112">Seu aplicativo precisa toorespond exibindo o código de validação back hello.</span><span class="sxs-lookup"><span data-stu-id="a7d46-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="a7d46-113">Grade de eventos não fornecerá eventos tooWebHook pontos de extremidade que não passaram na validação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="a7d46-114">Detalhes da validação:</span><span class="sxs-lookup"><span data-stu-id="a7d46-114">Validation details:</span></span>

* <span data-ttu-id="a7d46-115">Em tempo de saudação de criação/atualização de assinatura de evento, a grade de eventos lança um ponto de extremidade de destino de toohello do evento de "SubscriptionValidationEvent".</span><span class="sxs-lookup"><span data-stu-id="a7d46-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="a7d46-116">evento de saudação contém um valor de cabeçalho "Tipo de evento: validação".</span><span class="sxs-lookup"><span data-stu-id="a7d46-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="a7d46-117">corpo do evento Olá tem Olá mesmo esquema que outros eventos de grade de eventos.</span><span class="sxs-lookup"><span data-stu-id="a7d46-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="a7d46-118">dados de evento de saudação incluem uma propriedade de "Validação" com uma cadeia de caracteres gerada aleatoriamente, por exemplo "ValidationCode: acb13…".</span><span class="sxs-lookup"><span data-stu-id="a7d46-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="a7d46-119">Na propriedade de ponto de extremidade de tooprove ordem, por exemplo, o código de validação back Olá de eco "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="a7d46-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="a7d46-120">Por fim, é importante toonote que grade de eventos do Azure oferece suporte somente a pontos de extremidade HTTPS webhook.</span><span class="sxs-lookup"><span data-stu-id="a7d46-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="a7d46-121">Assinatura do evento</span><span class="sxs-lookup"><span data-stu-id="a7d46-121">Event subscription</span></span>

<span data-ttu-id="a7d46-122">toosubscribe tooan eventos, você deve ter Olá **Microsoft.EventGrid/EventSubscriptions/Write** necessária a permissão em Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="a7d46-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="a7d46-123">Essa permissão é necessária porque você está escrevendo uma nova assinatura no escopo de saudação do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="a7d46-124">Olá necessário recursos varia de acordo com se você estiver assinando tooa sistema tópico ou personalizado.</span><span class="sxs-lookup"><span data-stu-id="a7d46-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="a7d46-125">Ambos os tipos são descritos nesta seção.</span><span class="sxs-lookup"><span data-stu-id="a7d46-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="a7d46-126">Tópicos do sistema (publicadores de serviço do Azure)</span><span class="sxs-lookup"><span data-stu-id="a7d46-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="a7d46-127">Tópicos do sistema, você precisa de permissão toowrite uma nova assinatura de evento no escopo de saudação do evento de publicação Olá Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="a7d46-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="a7d46-128">formato de saudação do recurso de saudação é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="a7d46-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="a7d46-129">Por exemplo, o evento de tooan toosubscribe em uma conta de armazenamento denominada **myacct**, você precisa de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="a7d46-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="a7d46-130">Tópicos personalizados</span><span class="sxs-lookup"><span data-stu-id="a7d46-130">Custom topics</span></span>

<span data-ttu-id="a7d46-131">Para tópicos personalizados, você precisa de permissão toowrite uma nova assinatura de evento no escopo de saudação do tópico de grade de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="a7d46-132">formato de saudação do recurso de saudação é:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="a7d46-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="a7d46-133">Por exemplo, toosubscribe tooa tópico personalizado chamado **mytopic**, você precisa de permissão de Microsoft.EventGrid/EventSubscriptions/Write Olá em:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="a7d46-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="a7d46-134">Publicação de tópico</span><span class="sxs-lookup"><span data-stu-id="a7d46-134">Topic publishing</span></span>

<span data-ttu-id="a7d46-135">Os tópicos usam a Assinatura de Acesso Compartilhado (SAS) ou a autenticação de chave.</span><span class="sxs-lookup"><span data-stu-id="a7d46-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="a7d46-136">Recomendamos a SAS, mas a autenticação de chave fornece programação simples e é compatível com vários publicadores de webhook existentes.</span><span class="sxs-lookup"><span data-stu-id="a7d46-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="a7d46-137">Incluir o valor de autenticação Olá no cabeçalho HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="a7d46-138">SAS, use **token de sas aeg** para valor de cabeçalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="a7d46-139">Para autenticação de chave, use **aeg chave de sas** para valor de cabeçalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="a7d46-140">Autenticação de chave</span><span class="sxs-lookup"><span data-stu-id="a7d46-140">Key authentication</span></span>

<span data-ttu-id="a7d46-141">Autenticação de chave é a forma mais simples de saudação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a7d46-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="a7d46-142">Use o formato de saudação:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="a7d46-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="a7d46-143">Por exemplo, você pode passar uma chave com:</span><span class="sxs-lookup"><span data-stu-id="a7d46-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="a7d46-144">Tokens SAS</span><span class="sxs-lookup"><span data-stu-id="a7d46-144">SAS tokens</span></span>

<span data-ttu-id="a7d46-145">Tokens SAS para a grade de eventos incluem recursos hello, um tempo de expiração e uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a7d46-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="a7d46-146">Olá formato do token SAS Olá é: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="a7d46-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="a7d46-147">recurso Hello é caminho Olá para Olá tópico toowhich estiver enviando eventos.</span><span class="sxs-lookup"><span data-stu-id="a7d46-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="a7d46-148">Por exemplo, um caminho de recurso válido é:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="a7d46-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="a7d46-149">Você pode gerar assinatura de saudação de uma chave.</span><span class="sxs-lookup"><span data-stu-id="a7d46-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="a7d46-150">Por exemplo, um valor válido de **aeg-sas-token** é:</span><span class="sxs-lookup"><span data-stu-id="a7d46-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="a7d46-151">saudação de exemplo a seguir cria um token SAS para uso com a grade de eventos:</span><span class="sxs-lookup"><span data-stu-id="a7d46-151">hello following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="a7d46-152">Controle de acesso de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="a7d46-152">Management Access Control</span></span>

<span data-ttu-id="a7d46-153">Grade de eventos do Azure permite que você toocontrol Olá nível de acesso fornecido toodifferent usuários toodo várias operações de gerenciamento, como assinaturas de evento de lista, criar novos e gerar chaves.</span><span class="sxs-lookup"><span data-stu-id="a7d46-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="a7d46-154">A Grade de Eventos utiliza a verificação RBAC (Verificação de acesso com base em função) do Azure para isso.</span><span class="sxs-lookup"><span data-stu-id="a7d46-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="a7d46-155">Tipos de operação</span><span class="sxs-lookup"><span data-stu-id="a7d46-155">Operation types</span></span>

<span data-ttu-id="a7d46-156">Grade de eventos do Azure dá suporte a saudação ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a7d46-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="a7d46-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="a7d46-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="a7d46-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="a7d46-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="a7d46-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="a7d46-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="a7d46-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="a7d46-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="a7d46-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="a7d46-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="a7d46-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="a7d46-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="a7d46-163">Olá três operações retorno potencialmente informações secretas que obtém filtrado normais das operações de leitura.</span><span class="sxs-lookup"><span data-stu-id="a7d46-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="a7d46-164">É prática recomendada para você, operações de toothese toorestrict acesso.</span><span class="sxs-lookup"><span data-stu-id="a7d46-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="a7d46-165">Funções personalizadas podem ser criadas usando [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Interface de linha de comando (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)e hello [API REST](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a7d46-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="a7d46-166">Aplicação da Verificação RBAC (Verificação de acesso com base em função)</span><span class="sxs-lookup"><span data-stu-id="a7d46-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="a7d46-167">Use Olá etapas tooenforce RBAC para diferentes usuários a seguir:</span><span class="sxs-lookup"><span data-stu-id="a7d46-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="a7d46-168">Criar um arquivo de definição de função personalizado (.json)</span><span class="sxs-lookup"><span data-stu-id="a7d46-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="a7d46-169">Olá seguem definições de função de grade de eventos de exemplo que permitem aos usuários tooperform diferentes conjuntos de ações.</span><span class="sxs-lookup"><span data-stu-id="a7d46-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="a7d46-170">**EventGridReadOnlyRole.json**: permitir apenas operações somente leitura.</span><span class="sxs-lookup"><span data-stu-id="a7d46-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="a7d46-171">**EventGridNoDeleteListKeysRole.json**: permitir ações restritas posteriores, mas impedir ações de exclusão.</span><span class="sxs-lookup"><span data-stu-id="a7d46-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="a7d46-172">**EventGridContributorRole.json**: permitir todas as ações da grade de eventos.</span><span class="sxs-lookup"><span data-stu-id="a7d46-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="a7d46-173">Instalar e logon tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="a7d46-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="a7d46-174">CLI do Azure versão 0.8.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a7d46-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="a7d46-175">versão mais recente do tooinstall hello e associe-o com sua assinatura do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a7d46-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a7d46-176">Azure Resource Manager na Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7d46-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="a7d46-177">Vá muito[usando Olá CLI do Azure com o Gerenciador de recursos de hello](../xplat-cli-azure-resource-manager.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a7d46-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="a7d46-178">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="a7d46-178">Create a custom role</span></span>

<span data-ttu-id="a7d46-179">toocreate uma função personalizada, use:</span><span class="sxs-lookup"><span data-stu-id="a7d46-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="a7d46-180">Atribuir Olá função tooa usuário</span><span class="sxs-lookup"><span data-stu-id="a7d46-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="a7d46-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a7d46-181">Next steps</span></span>

* <span data-ttu-id="a7d46-182">Para uma introdução tooEvent grade, consulte [sobre a grade de eventos](overview.md)</span><span class="sxs-lookup"><span data-stu-id="a7d46-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
