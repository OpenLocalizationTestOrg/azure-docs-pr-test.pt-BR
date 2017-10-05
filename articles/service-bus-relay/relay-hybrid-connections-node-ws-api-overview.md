---
title: "Visão geral das APIs de Nó de Retransmissão do Azure | Microsoft Docs"
description: "Visão geral da API de Nó de Retransmissão"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="4d6ca-103">Visão geral da API do Nó de Conexões Híbridas de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="4d6ca-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="4d6ca-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4d6ca-104">Overview</span></span>

<span data-ttu-id="4d6ca-105">O [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacote de nó para as conexões de retransmissão híbridas do Azure baseia-se e estende o ['ws'](https://www.npmjs.com/package/ws) pacote NPM.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="4d6ca-106">Este pacote novamente exporta todas as exportações do pacote base e adiciona novos exportações que permitem a integração com o recurso de conexões híbridas do serviço de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="4d6ca-107">Os aplicativos existentes que `require('ws')` pode usar esse pacote com `require('hyco-ws')` em vez disso, que também permite cenários híbridos em que um aplicativo pode escutar conexões WebSocket localmente do "dentro do firewall" e por meio de conexões híbridas, tudo ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="4d6ca-108">Documentação</span><span class="sxs-lookup"><span data-stu-id="4d6ca-108">Documentation</span></span>

<span data-ttu-id="4d6ca-109">As APIs estão [documentadas no pacote principal 'ws'](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="4d6ca-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="4d6ca-110">Este artigo descreve como esse pacote difere essa linha de base.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="4d6ca-111">As principais diferenças entre o pacote básico e essa 'hyco-ws' é que ele adiciona uma nova classe de servidor exportada com `require('hyco-ws').RelayedServer`e alguns métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="4d6ca-112">Métodos auxiliares de pacote</span><span class="sxs-lookup"><span data-stu-id="4d6ca-112">Package helper methods</span></span>

<span data-ttu-id="4d6ca-113">Há vários métodos de utilitário disponível na exportação do pacote que você pode fazer referência da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4d6ca-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="4d6ca-114">Os métodos auxiliares para uso com este pacote, mas também podem ser usados por um servidor de nó para habilitar clientes da web ou dispositivo criar ouvintes ou remetentes.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="4d6ca-115">O servidor usa esses métodos, passando-os URIs que incorporar tokens de curta duração.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="4d6ca-116">Esses URIs também pode ser usado com pilhas WebSocket comuns que não oferecem suporte a cabeçalhos HTTP de configuração para o handshake do WebSocket.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="4d6ca-117">A incorporação de tokens de autorização no URI é suportada principalmente para os cenários de uso da biblioteca externa.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="4d6ca-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="4d6ca-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="4d6ca-119">Cria um URI do ouvinte da Conexão Híbrida de Retransmissão do Azure para determinado namespace e caminho.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="4d6ca-120">Esse URI, em seguida, pode ser usado com a versão de retransmissão da classe WebSocketServer.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="4d6ca-121">`namespaceName` (obrigatório) – o nome de domínio qualificado do namespace de retransmissão do Azure a ser usado.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="4d6ca-122">`path` (obrigatório) – o nome de uma Conexão Híbrida de Retransmissão do Azure no namespace.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="4d6ca-123">`token` (opcional) – um token de acesso de retransmissão emitido anteriormente que é incorporado no ouvinte da URI (consulte o exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="4d6ca-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="4d6ca-124">`id` (opcional) – um identificador de acompanhamento que permite o acompanhamento de diagnóstico de ponta a ponta de solicitações.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="4d6ca-125">O valor `token` é opcional e só deve ser usado quando não for possível enviar cabeçalhos HTTP junto com o handshake do WebSocket, como é o caso com a pilha do WebSocket do W3C.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="4d6ca-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="4d6ca-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="4d6ca-127">Cria um envio de Conexão do Azure retransmissão híbrida URI válido para o namespace específico e o caminho.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="4d6ca-128">Esse URI pode ser usado com qualquer cliente WebSocket.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="4d6ca-129">`namespaceName` (obrigatório) – o nome de domínio qualificado do namespace de retransmissão do Azure a ser usado.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="4d6ca-130">`path` (obrigatório) – o nome de uma Conexão Híbrida de Retransmissão do Azure no namespace.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="4d6ca-131">`token` (opcional) – um token de acesso de retransmissão emitido anteriormente que é inserido no URI de envio (consulte o exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="4d6ca-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="4d6ca-132">`id` (opcional) – um identificador de acompanhamento que permite o acompanhamento de diagnóstico de ponta a ponta de solicitações.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="4d6ca-133">O valor `token` é opcional e só deve ser usado quando não for possível enviar cabeçalhos HTTP junto com o handshake do WebSocket, como é o caso com a pilha do WebSocket do W3C.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="4d6ca-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="4d6ca-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="4d6ca-135">Cria um token de Assinatura de Acesso Compartilhado (SAS) da Retransmissão do Azure para o URI, a regra SAS e a chave da regra SAS de destino especificados válidos para o número de segundos determinado ou para uma hora a partir do instante atual caso o argumento de expiração seja omitido.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="4d6ca-136">`uri` (obrigatório) – o URI para o qual o token deve ser emitido.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="4d6ca-137">O URI é normalizado para usar o esquema HTTP e informações de cadeia de caracteres de consulta serão removidas.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="4d6ca-138">`ruleName` (obrigatório) – nome de regra SAS para uma entidade representada por determinado URI ou para o namespace representado pela parte do host do URI.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="4d6ca-139">`key` (obrigatório) – chave válida para a regra de SAS.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="4d6ca-140">`expirationSeconds` (opcional) – o número de segundos até que o token gerado deve expirar.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="4d6ca-141">O padrão é 1 hora (3600) se não for especificado.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="4d6ca-142">O token emitido confere os direitos associados a regra SAS especificada para o período especificado.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="4d6ca-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="4d6ca-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="4d6ca-144">Esse método é funcionalmente equivalente ao método `createRelayToken` documentado anteriormente, mas retorna o token anexado corretamente para a URI de entrada.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="4d6ca-145">Classe ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="4d6ca-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="4d6ca-146">O `hycows.RelayedServer` classe é uma alternativa para o `ws.Server` classe não escuta na rede local, mas delegados escuta para o serviço de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="4d6ca-147">As duas classes são em geral compatíveis em termos de contrato, o que significa que um aplicativo existente usando a classe `ws.Server` pode ser facilmente alterado para usar a versão retransmitida.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="4d6ca-148">As principais diferenças são no construtor e nas opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="4d6ca-149">Construtor</span><span class="sxs-lookup"><span data-stu-id="4d6ca-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="4d6ca-150">O construtor `RelayedServer` dá suporte a um conjunto diferente de argumentos do que o `Server`, porque ele não é nem um ouvinte autônomo, nem pode ser inserido em uma estrutura de ouvinte HTTP existente.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="4d6ca-151">Também há menos opções disponíveis desde que o gerenciamento do WebSocket amplamente é delegado ao serviço de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="4d6ca-152">Argumentos do Construtor:</span><span class="sxs-lookup"><span data-stu-id="4d6ca-152">Constructor arguments:</span></span>

- <span data-ttu-id="4d6ca-153">`server` (obrigatório) – o URI totalmente qualificado para um nome de Conexão Híbrida a escutar costuma ser construído com o método auxiliar WebSocket.createRelayListenUri().</span><span class="sxs-lookup"><span data-stu-id="4d6ca-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="4d6ca-154">`token` (obrigatório) – esse argumento contém uma cadeia de caracteres de token emitida anteriormente ou uma função de retorno de chamada que pode ser chamada para obter uma cadeia de caracteres tal token.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="4d6ca-155">A opção de retorno de chamada é preferencial, pois permite renovação de tokens.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="4d6ca-156">Eventos</span><span class="sxs-lookup"><span data-stu-id="4d6ca-156">Events</span></span>

<span data-ttu-id="4d6ca-157">`RelayedServer`instâncias de emitem três eventos que permitem lidar com solicitações de entrada, estabelecer conexões e detectar condições de erro.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="4d6ca-158">Você deve assinar o evento `connect` para lidar com mensagens.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="4d6ca-159">headers</span><span class="sxs-lookup"><span data-stu-id="4d6ca-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="4d6ca-160">O evento `headers` é gerado antes de uma conexão de entrada ser aceita, permitindo a modificação dos cabeçalhos a enviar ao cliente.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="4d6ca-161">connection</span><span class="sxs-lookup"><span data-stu-id="4d6ca-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="4d6ca-162">Emitido quando uma nova conexão WebSocket é aceita.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="4d6ca-163">O objeto é do tipo `ws.WebSocket`, igual ao do pacote básico.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="4d6ca-164">error</span><span class="sxs-lookup"><span data-stu-id="4d6ca-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="4d6ca-165">Se o servidor subjacente emite um erro, ele é encaminhado aqui.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="4d6ca-166">Auxiliares</span><span class="sxs-lookup"><span data-stu-id="4d6ca-166">Helpers</span></span>

<span data-ttu-id="4d6ca-167">Para simplificar a inicialização de um servidor de retransmissão e a assinatura imediata conexões de entrada, o pacote expõe uma função auxiliar simples, que também é usada nos exemplos, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4d6ca-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="4d6ca-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="4d6ca-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="4d6ca-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="4d6ca-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="4d6ca-170">Esse método chama o construtor para criar uma nova instância de RelayedServer e, em seguida, assina o retorno de chamada fornecido para o evento 'conexão'.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="4d6ca-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="4d6ca-171">relayedConnect</span></span>

<span data-ttu-id="4d6ca-172">O espelhamento simplesmente o `createRelayedServer` auxiliar na função, `relayedConnect` cria uma conexão de cliente e assina o evento 'open' no soquete resultante.</span><span class="sxs-lookup"><span data-stu-id="4d6ca-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="4d6ca-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d6ca-173">Next steps</span></span>
<span data-ttu-id="4d6ca-174">Para saber mais sobre a Retransmissão do Azure, visite estes links:</span><span class="sxs-lookup"><span data-stu-id="4d6ca-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="4d6ca-175">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="4d6ca-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="4d6ca-176">APIs de Retransmissão Disponíveis</span><span class="sxs-lookup"><span data-stu-id="4d6ca-176">Available Relay APIs</span></span>](relay-api-overview.md)
