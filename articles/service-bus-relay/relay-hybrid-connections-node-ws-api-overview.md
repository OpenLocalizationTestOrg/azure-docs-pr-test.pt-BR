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
# <a name="relay-hybrid-connections-node-api-overview"></a>Visão geral da API do Nó de Conexões Híbridas de Retransmissão

## <a name="overview"></a>Visão geral

Olá [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacote de nó para as conexões de retransmissão híbridas Azure baseia-se e estende Olá ['ws'](https://www.npmjs.com/package/ws) pacote NPM. Este pacote novamente exporta todas as exportações de pacote básico e adiciona novos exportações que habilitar a integração com o recurso de conexões híbridas do serviço de retransmissão do Azure de saudação. 

Os aplicativos existentes que `require('ws')` pode usar esse pacote com `require('hyco-ws')` em vez disso, que também permite cenários híbridos em que um aplicativo pode escutar conexões WebSocket localmente do "dentro do firewall de hello" e por meio de conexões híbridas, todos Olá mesmo tempo.
  
## <a name="documentation"></a>Documentação

Olá APIs são [documentado no pacote de principal 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md). Este artigo descreve como esse pacote difere essa linha de base. 

Olá principais diferenças entre o pacote básico hello e este 'hyco-ws' é que ele adiciona uma nova classe de servidor, exportada por meio de `require('hyco-ws').RelayedServer`e alguns métodos auxiliares.

### <a name="package-helper-methods"></a>Métodos auxiliares de pacote

Há vários métodos de utilitário disponível na exportação de pacote de saudação que você pode fazer referência da seguinte maneira:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

métodos de auxiliares de saudação são para uso com este pacote, mas também podem ser usados por um servidor de nó para habilitar ouvintes toocreate de clientes da web ou dispositivo ou remetentes. servidor de saudação usa esses métodos passando os URIs que insira tokens de curta duração. Esses URIs também pode ser usado com comuns pilhas de WebSocket que não dão suporte a cabeçalhos HTTP de configuração para o handshake do WebSocket hello. Incorporar tokens de autorização hello, há suporte para o URI principalmente para os cenários de uso da biblioteca externa. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Cria um ouvinte de Azure retransmissão híbrida Conexão URI válido para Olá dado namespace e o caminho. Esse URI, em seguida, pode ser usado com versão de retransmissão de saudação do hello WebSocketServer classe.

- `namespaceName`(obrigatório) - Olá nome qualificado do domínio do hello Azure retransmissão namespace toouse.
- `path`(obrigatório) - Olá o nome de uma Conexão existente de híbrida de retransmissão do Azure no namespace.
- `token`(opcional) - um acesso de retransmissão emitido anteriormente token que é inserida no URI de escuta de saudação (consulte Olá exemplo a seguir).
- `id` (opcional) – um identificador de acompanhamento que permite o acompanhamento de diagnóstico de ponta a ponta de solicitações.

Olá `token` valor é opcional e só deve ser usado quando não é possível toosend HTTP cabeçalhos junto com o handshake do WebSocket hello, como Olá caso com pilha de W3C WebSocket hello.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Cria um envio de Azure retransmissão híbrida Conexão URI válido para Olá dado espaço para nome e caminho. Esse URI pode ser usado com qualquer cliente WebSocket.

- `namespaceName`(obrigatório) - Olá nome qualificado do domínio do hello Azure retransmissão namespace toouse.
- `path`(obrigatório) - Olá o nome de uma Conexão existente de híbrida de retransmissão do Azure no namespace.
- `token`enviar um token de acesso de retransmissão emitido anteriormente inserida no hello (opcional) - URI (consulte Olá exemplo a seguir).
- `id` (opcional) – um identificador de acompanhamento que permite o acompanhamento de diagnóstico de ponta a ponta de solicitações.

Olá `token` valor é opcional e só deve ser usado quando não é possível toosend HTTP cabeçalhos junto com o handshake do WebSocket hello, como Olá caso com pilha de W3C WebSocket hello.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Cria um token de assinatura de acesso compartilhado (SAS) do Azure retransmissão para o URI de destino Olá fornecido, a regra SAS e a chave da regra SAS é válido para Olá fornecido o número de segundos ou de uma hora de saudação atual instantânea se Olá expiração argumento for omitido.

- `uri`(obrigatório) - Olá URI para o qual Olá token é toobe emitido. Olá URI é normalizado toouse esquema HTTP de saudação e informações de cadeia de caracteres de consulta será removido.
- `ruleName`(obrigatório) - nome para a entidade de saudação representada por Olá fornecido URI da regra SAS ou para Olá namespace representado pela Olá parte do host URI.
- `key`(obrigatório) - chave válida para a regra SAS hello. 
- `expirationSeconds`(opcional) - número de saudação de segundos até Olá gerado token deve expirar. Se não for especificado, o padrão de saudação é 1 hora (3.600).

token Olá emitido confere direitos Olá Olá especificado regra SAS para Olá dada duração.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Esse método é funcionalmente equivalente toohello `createRelayToken` método documentado anteriormente, mas retorna Olá token toohello corretamente acrescentados entrada URI.

### <a name="class-wsrelayedserver"></a>Classe ws.RelayedServer

Olá `hycows.RelayedServer` classe é uma alternativa toohello `ws.Server` classe que não escutam na rede local hello, mas delega escuta toohello serviço de retransmissão do Azure.

classes de saudação dois são principalmente contrato compatível, o que significa que um aplicativo existente usando Olá `ws.Server` classe pode ser facilmente versão de hello retransmitida toouse alterados. Olá principais diferenças são no construtor de saudação e nas opções disponíveis de saudação.

#### <a name="constructor"></a>Construtor  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Olá `RelayedServer` construtor oferece suporte a um conjunto diferente de argumentos que Olá `Server`, porque ele não é um ouvinte autônomo ou capaz de toobe inserido em uma estrutura de ouvinte HTTP. Também há menos opções disponíveis como Olá gerenciamento WebSocket é amplamente delegado toohello serviço de retransmissão.

Argumentos do Construtor:

- `server`(obrigatório) - Olá totalmente qualificado URI para um nome de Conexão híbrida na qual toolisten, costuma ser construído com hello método auxiliar de WebSocket.createRelayListenUri().
- `token`(obrigatório) - este argumento contém uma cadeia de caracteres de token emitida anteriormente ou uma função de retorno de chamada que pode ser chamada tooobtain tal token de cadeia de caracteres. opção de retorno de chamada de saudação é preferencial, pois permite renovação de tokens.

#### <a name="events"></a>Eventos

`RelayedServer`instâncias de emissão de três eventos que permitem a você toohandle solicitações de entrada, estabelecem conexões e detectam condições de erro. Você deve assinar toohello `connect` mensagens de toohandle de eventos. 

##### <a name="headers"></a>headers

```JavaScript 
function(headers)
```

Olá `headers` evento é gerado antes de uma conexão de entrada é aceito, permitindo que a modificação do cliente do hello cabeçalhos toosend toohello. 

##### <a name="connection"></a>connection

```JavaScript
function(socket)
```

Emitido quando uma nova conexão WebSocket é aceita. objeto Olá é do tipo `ws.WebSocket`, mesmo que com o pacote básico da saudação.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Se o servidor subjacente Olá emite um erro, ele é encaminhado aqui.  

#### <a name="helpers"></a>Auxiliares

toosimplify iniciar um servidor retransmitido e imediatamente assinando tooincoming conexões, hello pacote expõe uma função auxiliar simples, que também é usada nos exemplos hello, da seguinte maneira:

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Este método chama Olá construtor toocreate uma nova instância da saudação RelayedServer e, em seguida, assina Olá fornecido de retorno de chamada toohello 'conexão' eventos.
 
##### <a name="relayedconnect"></a>relayedConnect

Espelhamento simplesmente Olá `createRelayedServer` auxiliar na função, `relayedConnect` cria uma conexão de cliente e assina o evento de 'open' toohello no soquete resultante Olá.

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

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre a retransmissão do Azure, visite esses links:
* [O que é Retransmissão do Azure?](relay-what-is-it.md)
* [APIs de Retransmissão Disponíveis](relay-api-overview.md)
