---
title: "aaaOverview do modelo de segurança e autenticação de Hubs de eventos do Azure | Microsoft Docs"
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
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="3d4df-103">Visão geral do modelo de autenticação e segurança dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3d4df-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="3d4df-104">modelo de segurança de Hubs de eventos do Azure Olá atende Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d4df-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="3d4df-105">Somente os clientes que apresentam credenciais válidas podem enviar hub de eventos de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="3d4df-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="3d4df-106">Um cliente não pode representar outro cliente.</span><span class="sxs-lookup"><span data-stu-id="3d4df-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="3d4df-107">Um cliente não autorizado pode ser impedido de enviar o hub de eventos de tooan de dados.</span><span class="sxs-lookup"><span data-stu-id="3d4df-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="3d4df-108">Autenticação de cliente</span><span class="sxs-lookup"><span data-stu-id="3d4df-108">Client authentication</span></span>
<span data-ttu-id="3d4df-109">modelo de segurança de Hubs de eventos Olá baseia-se em uma combinação de [assinatura de acesso compartilhado (SAS)](../service-bus-messaging/service-bus-sas.md) tokens e *editores de eventos*.</span><span class="sxs-lookup"><span data-stu-id="3d4df-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="3d4df-110">Um editor de eventos define um ponto de extremidade virtual para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="3d4df-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="3d4df-111">publicador de saudação só pode ser usado toosend hub de eventos de tooan de mensagens.</span><span class="sxs-lookup"><span data-stu-id="3d4df-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="3d4df-112">Não é possível tooreceive mensagens de um publicador.</span><span class="sxs-lookup"><span data-stu-id="3d4df-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="3d4df-113">Normalmente, um hub de eventos emprega um editor por cliente.</span><span class="sxs-lookup"><span data-stu-id="3d4df-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="3d4df-114">Todas as mensagens são enviadas tooany de editores de saudação de um hub de eventos são colocadas dentro desse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="3d4df-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="3d4df-115">Os editores habilitam o controle de acesso detalhado e a limitação.</span><span class="sxs-lookup"><span data-stu-id="3d4df-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="3d4df-116">Cada cliente de Hubs de eventos é atribuído um token exclusivo, que é carregado toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="3d4df-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="3d4df-117">tokens de saudação são produzidos, de modo que cada token exclusivo conceda publicador exclusivo diferente de tooa acesso.</span><span class="sxs-lookup"><span data-stu-id="3d4df-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="3d4df-118">Um cliente que possui um token só pode enviar tooone publisher, mas nenhum outro editor.</span><span class="sxs-lookup"><span data-stu-id="3d4df-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="3d4df-119">Se o compartilhamento de vários clientes Olá mesmo token, em seguida, cada um deles compartilha um publicador.</span><span class="sxs-lookup"><span data-stu-id="3d4df-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="3d4df-120">Embora não seja recomendado, é possível tooequip dispositivos com tokens que concedam hub de eventos de tooan acesso direto.</span><span class="sxs-lookup"><span data-stu-id="3d4df-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="3d4df-121">Qualquer dispositivo que contenha esse token pode enviar mensagens diretamente para esse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="3d4df-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="3d4df-122">Tal dispositivo não poderá ser toothrottling de assunto.</span><span class="sxs-lookup"><span data-stu-id="3d4df-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="3d4df-123">Além disso, dispositivo Olá não pode estar na lista negra de envio toothat hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="3d4df-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="3d4df-124">Todos os tokens são assinados com uma chave SAS.</span><span class="sxs-lookup"><span data-stu-id="3d4df-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="3d4df-125">Normalmente, todos os tokens são assinados com hello mesma chave.</span><span class="sxs-lookup"><span data-stu-id="3d4df-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="3d4df-126">Os clientes não estão cientes da chave Olá; Isso impede que outros clientes criem tokens.</span><span class="sxs-lookup"><span data-stu-id="3d4df-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="3d4df-127">Criar chave SAS Olá</span><span class="sxs-lookup"><span data-stu-id="3d4df-127">Create hello SAS key</span></span>

<span data-ttu-id="3d4df-128">Ao criar um namespace de Hubs de eventos, o serviço hello gera uma chave SAS de 256 bits chamada **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="3d4df-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="3d4df-129">Essa chave concede envia, ouvir e gerenciar direitos toohello namespace.</span><span class="sxs-lookup"><span data-stu-id="3d4df-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="3d4df-130">Você também pode criar chaves adicionais.</span><span class="sxs-lookup"><span data-stu-id="3d4df-130">You can also create additional keys.</span></span> <span data-ttu-id="3d4df-131">É recomendável que você gere uma chave que concede envia hub de eventos específicos de toohello de permissões.</span><span class="sxs-lookup"><span data-stu-id="3d4df-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="3d4df-132">Restante Olá deste tópico, supõe-se que você nomeou esta chave **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="3d4df-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="3d4df-133">saudação de exemplo a seguir cria uma chave de somente de envio ao criar o hub de eventos hello:</span><span class="sxs-lookup"><span data-stu-id="3d4df-133">hello following example creates a send-only key when creating hello event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="3d4df-134">Gerar tokens</span><span class="sxs-lookup"><span data-stu-id="3d4df-134">Generate tokens</span></span>

<span data-ttu-id="3d4df-135">Você pode gerar tokens usando a chave de SAS hello.</span><span class="sxs-lookup"><span data-stu-id="3d4df-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="3d4df-136">Você deve criar somente um token por cliente.</span><span class="sxs-lookup"><span data-stu-id="3d4df-136">You must produce only one token per client.</span></span> <span data-ttu-id="3d4df-137">Tokens podem ser gerados usando o seguinte método de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d4df-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="3d4df-138">Todos os tokens são gerados usando Olá **EventHubSendKey** chave.</span><span class="sxs-lookup"><span data-stu-id="3d4df-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="3d4df-139">A cada token é atribuído um URI exclusivo.</span><span class="sxs-lookup"><span data-stu-id="3d4df-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="3d4df-140">Ao chamar esse método, Olá URI deve ser especificado como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="3d4df-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="3d4df-141">Para todos os tokens, Olá URI é idêntico, com exceção de saudação do `PUBLISHER_NAME`, que deve ser diferente para cada token.</span><span class="sxs-lookup"><span data-stu-id="3d4df-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="3d4df-142">Idealmente, `PUBLISHER_NAME` representa Olá ID do cliente Olá que recebe esse token.</span><span class="sxs-lookup"><span data-stu-id="3d4df-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="3d4df-143">Este método gera um token com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d4df-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="3d4df-144">tempo de expiração do token de saudação é especificado em segundos desde 1º de janeiro de 1970.</span><span class="sxs-lookup"><span data-stu-id="3d4df-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="3d4df-145">Olá seguinte é um exemplo de um token:</span><span class="sxs-lookup"><span data-stu-id="3d4df-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="3d4df-146">Normalmente, os tokens de saudação têm um tempo de vida que é semelhante ou excede o tempo de vida de saudação do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3d4df-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="3d4df-147">Se cliente Olá Olá recurso tooobtain um novo token, tokens com um tempo de vida mais curto podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="3d4df-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="3d4df-148">Enviar dados</span><span class="sxs-lookup"><span data-stu-id="3d4df-148">Sending data</span></span>
<span data-ttu-id="3d4df-149">Após a criação de tokens hello, cada cliente é configurado com seu próprio token exclusivo.</span><span class="sxs-lookup"><span data-stu-id="3d4df-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="3d4df-150">Quando o cliente Olá envia dados a um hub de eventos, marcas de sua solicitação de envio com o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d4df-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="3d4df-151">tooprevent um invasor intercepte e roube o token hello, a comunicação de saudação entre cliente hello e hub de eventos Olá deve ocorrer em um canal criptografado.</span><span class="sxs-lookup"><span data-stu-id="3d4df-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="3d4df-152">Colocando clientes na lista de bloqueio</span><span class="sxs-lookup"><span data-stu-id="3d4df-152">Blacklisting clients</span></span>
<span data-ttu-id="3d4df-153">Se um token for roubado por um invasor, o invasor Olá pode representar o cliente de saudação cujo token foi roubado.</span><span class="sxs-lookup"><span data-stu-id="3d4df-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="3d4df-154">Colocar um cliente na lista de bloqueio o inutilizará até ele receber um novo token que usa um outro editor.</span><span class="sxs-lookup"><span data-stu-id="3d4df-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="3d4df-155">Autenticação de aplicativos back-end</span><span class="sxs-lookup"><span data-stu-id="3d4df-155">Authentication of back-end applications</span></span>

<span data-ttu-id="3d4df-156">aplicativos de back-end tooauthenticate que consomem dados Olá gerados por clientes de Hubs de eventos, os Hubs de eventos emprega um modelo de segurança que é modelo toohello semelhante que é usado para tópicos do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="3d4df-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="3d4df-157">Um grupo de consumidores de Hubs de eventos é um tópico de barramento de serviço do tooa equivalente assinatura tooa.</span><span class="sxs-lookup"><span data-stu-id="3d4df-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="3d4df-158">Um cliente pode criar um grupo de consumidores, se o grupo de consumidores do hello solicitação toocreate Olá é acompanhado por um token que concede privilégios para o hub de eventos de saudação de gerenciamento ou para Olá namespace toowhich hub de eventos Olá pertence.</span><span class="sxs-lookup"><span data-stu-id="3d4df-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="3d4df-159">Um cliente pode tooconsume dados de um grupo de consumidores se Olá receber a solicitação são acompanhados por um token que concede direitos no grupo de consumidores de recebimento, hello hub de eventos ou hub de eventos Olá namespace toowhich Olá pertence.</span><span class="sxs-lookup"><span data-stu-id="3d4df-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="3d4df-160">versão atual de saudação do barramento de serviço não dá suporte a regras SAS para assinaturas individuais.</span><span class="sxs-lookup"><span data-stu-id="3d4df-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="3d4df-161">Olá que mesmo se aplica para grupos de consumidores de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="3d4df-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="3d4df-162">Suporte a SAS será adicionado para ambos os recursos no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="3d4df-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="3d4df-163">Na ausência de saudação de autenticação de SAS para grupos de consumidores individuais, você pode usar SAS chaves toosecure todos os grupos de consumidores com uma chave comum.</span><span class="sxs-lookup"><span data-stu-id="3d4df-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="3d4df-164">Essa abordagem permite que os dados de tooconsume um aplicativo de qualquer um dos grupos de consumidores de saudação de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="3d4df-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d4df-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d4df-165">Next steps</span></span>
<span data-ttu-id="3d4df-166">toolearn mais sobre Hubs de eventos, visite Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="3d4df-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="3d4df-167">[Visão Geral dos Hubs de Eventos]</span><span class="sxs-lookup"><span data-stu-id="3d4df-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="3d4df-168">[Visão Geral de Assinatura de Acesso Compartilhado]</span><span class="sxs-lookup"><span data-stu-id="3d4df-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="3d4df-169">[Aplicativos de exemplo que usam Hub de Eventos]</span><span class="sxs-lookup"><span data-stu-id="3d4df-169">[Sample applications that use Event Hubs]</span></span>

[Visão Geral dos Hubs de Eventos]: event-hubs-what-is-event-hubs.md
[Aplicativos de exemplo que usam Hub de Eventos]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Visão Geral de Assinatura de Acesso Compartilhado]: ../service-bus-messaging/service-bus-sas.md

