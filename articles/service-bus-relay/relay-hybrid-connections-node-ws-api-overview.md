---
title: "aaaOverview de saudação APIs de nó de retransmissão do Azure | Microsoft Docs"
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
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="04f43-103">Visão geral da API do Nó de Conexões Híbridas de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="04f43-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="04f43-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="04f43-104">Overview</span></span>

<span data-ttu-id="04f43-105">Olá [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacote de nó para as conexões de retransmissão híbridas Azure baseia-se e estende Olá ['ws'](https://www.npmjs.com/package/ws) pacote NPM.</span><span class="sxs-lookup"><span data-stu-id="04f43-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="04f43-106">Este pacote novamente exporta todas as exportações de pacote básico e adiciona novos exportações que habilitar a integração com o recurso de conexões híbridas do serviço de retransmissão do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="04f43-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="04f43-107">Os aplicativos existentes que `require('ws')` pode usar esse pacote com `require('hyco-ws')` em vez disso, que também permite cenários híbridos em que um aplicativo pode escutar conexões WebSocket localmente do "dentro do firewall de hello" e por meio de conexões híbridas, todos Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="04f43-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="04f43-108">Documentação</span><span class="sxs-lookup"><span data-stu-id="04f43-108">Documentation</span></span>

<span data-ttu-id="04f43-109">Olá APIs são [documentado no pacote de principal 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="04f43-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="04f43-110">Este artigo descreve como esse pacote difere essa linha de base.</span><span class="sxs-lookup"><span data-stu-id="04f43-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="04f43-111">Olá principais diferenças entre o pacote básico hello e este 'hyco-ws' é que ele adiciona uma nova classe de servidor, exportada por meio de `require('hyco-ws').RelayedServer`e alguns métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="04f43-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="04f43-112">Métodos auxiliares de pacote</span><span class="sxs-lookup"><span data-stu-id="04f43-112">Package helper methods</span></span>

<span data-ttu-id="04f43-113">Há vários métodos de utilitário disponível na exportação de pacote de saudação que você pode fazer referência da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="04f43-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="04f43-114">métodos de auxiliares de saudação são para uso com este pacote, mas também podem ser usados por um servidor de nó para habilitar ouvintes toocreate de clientes da web ou dispositivo ou remetentes.</span><span class="sxs-lookup"><span data-stu-id="04f43-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="04f43-115">servidor de saudação usa esses métodos passando os URIs que insira tokens de curta duração.</span><span class="sxs-lookup"><span data-stu-id="04f43-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="04f43-116">Esses URIs também pode ser usado com comuns pilhas de WebSocket que não dão suporte a cabeçalhos HTTP de configuração para o handshake do WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="04f43-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="04f43-117">Incorporar tokens de autorização hello, há suporte para o URI principalmente para os cenários de uso da biblioteca externa.</span><span class="sxs-lookup"><span data-stu-id="04f43-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="04f43-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="04f43-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="04f43-119">Cria um ouvinte de Azure retransmissão híbrida Conexão URI válido para Olá dado namespace e o caminho.</span><span class="sxs-lookup"><span data-stu-id="04f43-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="04f43-120">Esse URI, em seguida, pode ser usado com versão de retransmissão de saudação do hello WebSocketServer classe.</span><span class="sxs-lookup"><span data-stu-id="04f43-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="04f43-121">`namespaceName`(obrigatório) - Olá nome qualificado do domínio do hello Azure retransmissão namespace toouse.</span><span class="sxs-lookup"><span data-stu-id="04f43-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="04f43-122">`path`(obrigatório) - Olá o nome de uma Conexão existente de híbrida de retransmissão do Azure no namespace.</span><span class="sxs-lookup"><span data-stu-id="04f43-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="04f43-123">`token`(opcional) - um acesso de retransmissão emitido anteriormente token que é inserida no URI de escuta de saudação (consulte Olá exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="04f43-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="04f43-124">`id` (opcional) – um identificador de acompanhamento que permite o acompanhamento de diagnóstico de ponta a ponta de solicitações.</span><span class="sxs-lookup"><span data-stu-id="04f43-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="04f43-125">Olá `token` valor é opcional e só deve ser usado quando não é possível toosend HTTP cabeçalhos junto com o handshake do WebSocket hello, como Olá caso com pilha de W3C WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="04f43-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="04f43-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="04f43-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="04f43-127">Cria um envio de Azure retransmissão híbrida Conexão URI válido para Olá dado espaço para nome e caminho.</span><span class="sxs-lookup"><span data-stu-id="04f43-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="04f43-128">Esse URI pode ser usado com qualquer cliente WebSocket.</span><span class="sxs-lookup"><span data-stu-id="04f43-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="04f43-129">`namespaceName`(obrigatório) - Olá nome qualificado do domínio do hello Azure retransmissão namespace toouse.</span><span class="sxs-lookup"><span data-stu-id="04f43-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="04f43-130">`path`(obrigatório) - Olá o nome de uma Conexão existente de híbrida de retransmissão do Azure no namespace.</span><span class="sxs-lookup"><span data-stu-id="04f43-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="04f43-131">`token`enviar um token de acesso de retransmissão emitido anteriormente inserida no hello (opcional) - URI (consulte Olá exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="04f43-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="04f43-132">`id` (opcional) – um identificador de acompanhamento que permite o acompanhamento de diagnóstico de ponta a ponta de solicitações.</span><span class="sxs-lookup"><span data-stu-id="04f43-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="04f43-133">Olá `token` valor é opcional e só deve ser usado quando não é possível toosend HTTP cabeçalhos junto com o handshake do WebSocket hello, como Olá caso com pilha de W3C WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="04f43-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="04f43-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="04f43-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="04f43-135">Cria um token de assinatura de acesso compartilhado (SAS) do Azure retransmissão para o URI de destino Olá fornecido, a regra SAS e a chave da regra SAS é válido para Olá fornecido o número de segundos ou de uma hora de saudação atual instantânea se Olá expiração argumento for omitido.</span><span class="sxs-lookup"><span data-stu-id="04f43-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="04f43-136">`uri`(obrigatório) - Olá URI para o qual Olá token é toobe emitido.</span><span class="sxs-lookup"><span data-stu-id="04f43-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="04f43-137">Olá URI é normalizado toouse esquema HTTP de saudação e informações de cadeia de caracteres de consulta será removido.</span><span class="sxs-lookup"><span data-stu-id="04f43-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="04f43-138">`ruleName`(obrigatório) - nome para a entidade de saudação representada por Olá fornecido URI da regra SAS ou para Olá namespace representado pela Olá parte do host URI.</span><span class="sxs-lookup"><span data-stu-id="04f43-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="04f43-139">`key`(obrigatório) - chave válida para a regra SAS hello.</span><span class="sxs-lookup"><span data-stu-id="04f43-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="04f43-140">`expirationSeconds`(opcional) - número de saudação de segundos até Olá gerado token deve expirar.</span><span class="sxs-lookup"><span data-stu-id="04f43-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="04f43-141">Se não for especificado, o padrão de saudação é 1 hora (3.600).</span><span class="sxs-lookup"><span data-stu-id="04f43-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="04f43-142">token Olá emitido confere direitos Olá Olá especificado regra SAS para Olá dada duração.</span><span class="sxs-lookup"><span data-stu-id="04f43-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="04f43-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="04f43-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="04f43-144">Esse método é funcionalmente equivalente toohello `createRelayToken` método documentado anteriormente, mas retorna Olá token toohello corretamente acrescentados entrada URI.</span><span class="sxs-lookup"><span data-stu-id="04f43-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="04f43-145">Classe ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="04f43-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="04f43-146">Olá `hycows.RelayedServer` classe é uma alternativa toohello `ws.Server` classe que não escutam na rede local hello, mas delega escuta toohello serviço de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="04f43-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="04f43-147">classes de saudação dois são principalmente contrato compatível, o que significa que um aplicativo existente usando Olá `ws.Server` classe pode ser facilmente versão de hello retransmitida toouse alterados.</span><span class="sxs-lookup"><span data-stu-id="04f43-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="04f43-148">Olá principais diferenças são no construtor de saudação e nas opções disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="04f43-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="04f43-149">Construtor</span><span class="sxs-lookup"><span data-stu-id="04f43-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="04f43-150">Olá `RelayedServer` construtor oferece suporte a um conjunto diferente de argumentos que Olá `Server`, porque ele não é um ouvinte autônomo ou capaz de toobe inserido em uma estrutura de ouvinte HTTP.</span><span class="sxs-lookup"><span data-stu-id="04f43-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="04f43-151">Também há menos opções disponíveis como Olá gerenciamento WebSocket é amplamente delegado toohello serviço de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="04f43-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="04f43-152">Argumentos do Construtor:</span><span class="sxs-lookup"><span data-stu-id="04f43-152">Constructor arguments:</span></span>

- <span data-ttu-id="04f43-153">`server`(obrigatório) - Olá totalmente qualificado URI para um nome de Conexão híbrida na qual toolisten, costuma ser construído com hello método auxiliar de WebSocket.createRelayListenUri().</span><span class="sxs-lookup"><span data-stu-id="04f43-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="04f43-154">`token`(obrigatório) - este argumento contém uma cadeia de caracteres de token emitida anteriormente ou uma função de retorno de chamada que pode ser chamada tooobtain tal token de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="04f43-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="04f43-155">opção de retorno de chamada de saudação é preferencial, pois permite renovação de tokens.</span><span class="sxs-lookup"><span data-stu-id="04f43-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="04f43-156">Eventos</span><span class="sxs-lookup"><span data-stu-id="04f43-156">Events</span></span>

<span data-ttu-id="04f43-157">`RelayedServer`instâncias de emissão de três eventos que permitem a você toohandle solicitações de entrada, estabelecem conexões e detectam condições de erro.</span><span class="sxs-lookup"><span data-stu-id="04f43-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="04f43-158">Você deve assinar toohello `connect` mensagens de toohandle de eventos.</span><span class="sxs-lookup"><span data-stu-id="04f43-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="04f43-159">headers</span><span class="sxs-lookup"><span data-stu-id="04f43-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="04f43-160">Olá `headers` evento é gerado antes de uma conexão de entrada é aceito, permitindo que a modificação do cliente do hello cabeçalhos toosend toohello.</span><span class="sxs-lookup"><span data-stu-id="04f43-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="04f43-161">connection</span><span class="sxs-lookup"><span data-stu-id="04f43-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="04f43-162">Emitido quando uma nova conexão WebSocket é aceita.</span><span class="sxs-lookup"><span data-stu-id="04f43-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="04f43-163">objeto Olá é do tipo `ws.WebSocket`, mesmo que com o pacote básico da saudação.</span><span class="sxs-lookup"><span data-stu-id="04f43-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="04f43-164">error</span><span class="sxs-lookup"><span data-stu-id="04f43-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="04f43-165">Se o servidor subjacente Olá emite um erro, ele é encaminhado aqui.</span><span class="sxs-lookup"><span data-stu-id="04f43-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="04f43-166">Auxiliares</span><span class="sxs-lookup"><span data-stu-id="04f43-166">Helpers</span></span>

<span data-ttu-id="04f43-167">toosimplify iniciar um servidor retransmitido e imediatamente assinando tooincoming conexões, hello pacote expõe uma função auxiliar simples, que também é usada nos exemplos hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="04f43-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="04f43-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="04f43-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="04f43-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="04f43-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="04f43-170">Este método chama Olá construtor toocreate uma nova instância da saudação RelayedServer e, em seguida, assina Olá fornecido de retorno de chamada toohello 'conexão' eventos.</span><span class="sxs-lookup"><span data-stu-id="04f43-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="04f43-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="04f43-171">relayedConnect</span></span>

<span data-ttu-id="04f43-172">Espelhamento simplesmente Olá `createRelayedServer` auxiliar na função, `relayedConnect` cria uma conexão de cliente e assina o evento de 'open' toohello no soquete resultante Olá.</span><span class="sxs-lookup"><span data-stu-id="04f43-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="04f43-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04f43-173">Next steps</span></span>
<span data-ttu-id="04f43-174">toolearn mais informações sobre a retransmissão do Azure, visite esses links:</span><span class="sxs-lookup"><span data-stu-id="04f43-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="04f43-175">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="04f43-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="04f43-176">APIs de Retransmissão Disponíveis</span><span class="sxs-lookup"><span data-stu-id="04f43-176">Available Relay APIs</span></span>](relay-api-overview.md)
