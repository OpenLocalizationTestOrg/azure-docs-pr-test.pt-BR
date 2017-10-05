---
title: "Visão geral do modelo de autenticação e de segurança dos Hubs de Eventos do Azure | Microsoft Docs"
description: "Visão geral do modelo de autenticação e segurança dos Hubs de Eventos"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="cce49-103">Visão geral do modelo de autenticação e segurança dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="cce49-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="cce49-104">O modelo de segurança dos Hubs de Eventos do Azure atende aos seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="cce49-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="cce49-105">Somente clientes que apresentam credenciais válidas podem enviar dados para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="cce49-106">Um cliente não pode representar outro cliente.</span><span class="sxs-lookup"><span data-stu-id="cce49-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="cce49-107">Um cliente invasor pode ser impedido de enviar dados para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="cce49-108">Autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="cce49-108">Client authentication</span></span>
<span data-ttu-id="cce49-109">O modelo de segurança dos Hubs de Eventos se baseia em uma combinação de tokens [SAS (Assinatura de Acesso Compartilhado)](../service-bus-messaging/service-bus-sas.md) e de *editores de eventos*.</span><span class="sxs-lookup"><span data-stu-id="cce49-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="cce49-110">Um editor de eventos define um ponto de extremidade virtual para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="cce49-111">O editor só pode ser usado para enviar mensagens a um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="cce49-112">Não é possível receber mensagens de um editor.</span><span class="sxs-lookup"><span data-stu-id="cce49-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="cce49-113">Normalmente, um hub de eventos emprega um editor por cliente.</span><span class="sxs-lookup"><span data-stu-id="cce49-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="cce49-114">Todas as mensagens enviadas a um dos publicadores de um hub de eventos são enfileiradas nesse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="cce49-115">Os editores habilitam o controle de acesso detalhado e a limitação.</span><span class="sxs-lookup"><span data-stu-id="cce49-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="cce49-116">Cada cliente dos hubs de eventos recebe um token exclusivo que é carregado no cliente.</span><span class="sxs-lookup"><span data-stu-id="cce49-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="cce49-117">Os tokens são produzidos de modo que cada token exclusivo concede acesso a um editor exclusivo diferente.</span><span class="sxs-lookup"><span data-stu-id="cce49-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="cce49-118">Um cliente que possui um token só pode enviar para um editor específico, e para nenhum outro.</span><span class="sxs-lookup"><span data-stu-id="cce49-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="cce49-119">Se vários clientes compartilharem o mesmo token, cada um desses deles compartilhará um editor.</span><span class="sxs-lookup"><span data-stu-id="cce49-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="cce49-120">Embora não seja recomendado, é possível equipar os dispositivos com tokens que concedem acesso direto a um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="cce49-121">Qualquer dispositivo que contenha esse token pode enviar mensagens diretamente para esse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="cce49-122">Esse dispositivo não estará sujeito à limitação.</span><span class="sxs-lookup"><span data-stu-id="cce49-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="cce49-123">Além disso, o dispositivo não pode ser incluído na lista de bloqueios para ser impedido de enviar para esse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="cce49-124">Todos os tokens são assinados com uma chave SAS.</span><span class="sxs-lookup"><span data-stu-id="cce49-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="cce49-125">Normalmente, todos os tokens são assinados com a mesma chave.</span><span class="sxs-lookup"><span data-stu-id="cce49-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="cce49-126">Os clientes não estão cientes da chave; isso impede que outros clientes criem tokens.</span><span class="sxs-lookup"><span data-stu-id="cce49-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="cce49-127">Criar a chave SAS</span><span class="sxs-lookup"><span data-stu-id="cce49-127">Create the SAS key</span></span>

<span data-ttu-id="cce49-128">Ao criar um namespace de Hubs de Eventos, o serviço gera uma chave SAS de 256 bits chamada **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="cce49-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="cce49-129">Essa chave concede direitos de envio, escuta e gerenciamento ao namespace.</span><span class="sxs-lookup"><span data-stu-id="cce49-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="cce49-130">Você também pode criar chaves adicionais.</span><span class="sxs-lookup"><span data-stu-id="cce49-130">You can also create additional keys.</span></span> <span data-ttu-id="cce49-131">É recomendável que você crie uma chave que concede permissões de envio para o hub de eventos específico.</span><span class="sxs-lookup"><span data-stu-id="cce49-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="cce49-132">No restante deste tópico, pressupõe-se que você tenha nomeado esta chave como **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="cce49-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="cce49-133">O exemplo a seguir cria uma chave somente de envio ao criar o hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="cce49-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="cce49-134">Gerar tokens</span><span class="sxs-lookup"><span data-stu-id="cce49-134">Generate tokens</span></span>

<span data-ttu-id="cce49-135">Você pode gerar tokens usando a chave SAS.</span><span class="sxs-lookup"><span data-stu-id="cce49-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="cce49-136">Você deve criar somente um token por cliente.</span><span class="sxs-lookup"><span data-stu-id="cce49-136">You must produce only one token per client.</span></span> <span data-ttu-id="cce49-137">Tokens podem ser criados usando o seguinte método.</span><span class="sxs-lookup"><span data-stu-id="cce49-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="cce49-138">Todos os tokens são gerados usando a chave **EventHubSendKey** .</span><span class="sxs-lookup"><span data-stu-id="cce49-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="cce49-139">A cada token é atribuído um URI exclusivo.</span><span class="sxs-lookup"><span data-stu-id="cce49-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="cce49-140">Ao chamar esse método, o URI deve ser especificado como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="cce49-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="cce49-141">Para todos os tokens, o URI é idêntico, com exceção de `PUBLISHER_NAME`, que deve ser diferente para cada token.</span><span class="sxs-lookup"><span data-stu-id="cce49-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="cce49-142">O ideal é que `PUBLISHER_NAME` represente a ID do cliente que recebe esse token.</span><span class="sxs-lookup"><span data-stu-id="cce49-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="cce49-143">Esse método gera um token com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="cce49-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="cce49-144">O tempo de expiração do token é especificado em segundos desde 1º de janeiro de 1970.</span><span class="sxs-lookup"><span data-stu-id="cce49-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="cce49-145">Segue um exemplo de um token:</span><span class="sxs-lookup"><span data-stu-id="cce49-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="cce49-146">Normalmente, os tokens têm um tempo de vida semelhante a superior ao tempo de vida do cliente.</span><span class="sxs-lookup"><span data-stu-id="cce49-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="cce49-147">Se o cliente tiver a capacidade de obter um novo token, tokens com um tempo de vida mais curto podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="cce49-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="cce49-148">Enviar dados</span><span class="sxs-lookup"><span data-stu-id="cce49-148">Sending data</span></span>
<span data-ttu-id="cce49-149">Depois que os tokens são criados, cada cliente é configurado com seu próprio token exclusivo.</span><span class="sxs-lookup"><span data-stu-id="cce49-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="cce49-150">Quando o cliente envia dados a um hub de eventos, ele marca a solicitação de envio com o token.</span><span class="sxs-lookup"><span data-stu-id="cce49-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="cce49-151">Para evitar que um invasor intercepte e roube o token, a comunicação entre o cliente e o hub de eventos deve ocorrer em um canal criptografado.</span><span class="sxs-lookup"><span data-stu-id="cce49-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="cce49-152">Colocando clientes na lista de bloqueio</span><span class="sxs-lookup"><span data-stu-id="cce49-152">Blacklisting clients</span></span>
<span data-ttu-id="cce49-153">Se um token for roubado por um invasor, este poderá representar o cliente cujo token foi roubado.</span><span class="sxs-lookup"><span data-stu-id="cce49-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="cce49-154">Colocar um cliente na lista de bloqueio o inutilizará até ele receber um novo token que usa um outro editor.</span><span class="sxs-lookup"><span data-stu-id="cce49-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="cce49-155">Autenticação de aplicativos back-end</span><span class="sxs-lookup"><span data-stu-id="cce49-155">Authentication of back-end applications</span></span>

<span data-ttu-id="cce49-156">Para autenticar aplicativos back-end que consomem os dados gerados por clientes dos Hubs de Eventos, estes empregam um modelo de segurança semelhante ao modelo usado para os tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="cce49-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="cce49-157">Um grupo de consumidores de Hubs de Eventos é equivalente a uma assinatura de um tópico do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="cce49-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="cce49-158">Um cliente pode criar um grupo de consumidores se a solicitação para criar o grupo for acompanhada por um token que concede privilégios de gerenciamento para o hub de eventos ou para o namespace ao qual o hub de eventos pertence.</span><span class="sxs-lookup"><span data-stu-id="cce49-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="cce49-159">Um cliente pode consumir dados de um grupo de consumidores, se a solicitação de recebimento for acompanhada por um token que concede direitos de recebimento no grupo de consumidores, o hub de eventos ou o namespace ao qual o hub de eventos pertence.</span><span class="sxs-lookup"><span data-stu-id="cce49-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="cce49-160">A versão atual do Barramento de Serviço não dá suporte a regras SAS para assinaturas individuais.</span><span class="sxs-lookup"><span data-stu-id="cce49-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="cce49-161">O mesmo se aplica a grupos de consumidores de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="cce49-162">O suporte a SAS será adicionado para os dois recursos no futuro.</span><span class="sxs-lookup"><span data-stu-id="cce49-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="cce49-163">Na ausência de autenticação SAS para grupos de consumidores individuais, você pode utilizar chaves SAS para proteger todos os grupos de consumidores com uma chave comum.</span><span class="sxs-lookup"><span data-stu-id="cce49-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="cce49-164">Essa abordagem permite que um aplicativo consuma dados de qualquer grupo de consumidores de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cce49-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cce49-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cce49-165">Next steps</span></span>
<span data-ttu-id="cce49-166">Para saber mais sobre os Hubs de Eventos, veja os tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cce49-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="cce49-167">[Visão Geral dos Hubs de Eventos]</span><span class="sxs-lookup"><span data-stu-id="cce49-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="cce49-168">[Visão Geral de Assinatura de Acesso Compartilhado]</span><span class="sxs-lookup"><span data-stu-id="cce49-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="cce49-169">[Aplicativos de exemplo que usam Hub de Eventos]</span><span class="sxs-lookup"><span data-stu-id="cce49-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="cce49-170">[Visão Geral dos Hubs de Eventos]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="cce49-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="cce49-171">[Aplicativos de exemplo que usam Hub de Eventos]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="cce49-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="cce49-172">[Visão Geral de Assinatura de Acesso Compartilhado]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="cce49-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

