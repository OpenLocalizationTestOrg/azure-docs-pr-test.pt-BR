---
title: "aaaOverview de saudação APIs padrão do .NET do Azure retransmissão | Microsoft Docs"
description: "Visão geral da API .NET Standard de Retransmissão"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Visão geral da API .NET Standard de Conexões Híbridas de Retransmissão do Azure

Este artigo resume algumas das chave de hello Azure retransmissão híbrida conexões .NET Standard [APIs de cliente](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Construtor de Cadeia de Conexão de Retransmissão

Olá [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe formatos de cadeias de caracteres de conexão que são as conexões híbridas tooRelay específico. Você pode usá-lo tooverify formato de saudação de uma cadeia de caracteres de conexão ou toobuild uma cadeia de caracteres de conexão do zero. Consulte Olá código para obter um exemplo a seguir:

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

Você também pode passar uma conexão de cadeia de caracteres diretamente toohello `RelayConnectionStringBuilder` método. Esta operação permite que você tooverify a cadeia de caracteres de conexão hello está em um formato válido. Se qualquer um dos parâmetros de saudação são inválidos, o construtor hello gera um `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Fluxo de Conexão Híbrida
Olá [HybridConnectionStream] [ HCStream] classe é toosend de objeto primário usado hello e receber dados de um ponto de extremidade de retransmissão do Azure, se você estiver trabalhando com um [HybridConnectionClient] [ HCClient], ou um [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Obter um Fluxo de Conexão Híbrida

#### <a name="listener"></a>Ouvinte
Usando um [HybridConnectionListener][HCListener], você pode obter um `HybridConnectionStream` da seguinte maneira:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Cliente
Usando um [HybridConnectionClient][HCClient], você pode obter um objeto `HybridConnectionStream` da seguinte maneira:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Recebendo dados
Olá [HybridConnectionStream] [ HCStream] classe habilita comunicação bidirecional. Na maioria dos casos, você recebe continuamente de fluxo de saudação. Se você estiver lendo texto de fluxo de saudação, talvez você queira toouse um [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objeto, que habilita a análise mais fácil de dados de saudação. Por exemplo, você pode ler os dados como texto em vez de como `byte[]`.

Hello código a seguir lê linhas de texto individuais de fluxo de saudação até que um cancelamento é solicitado:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Enviar dados
Depois que você tiver uma conexão estabelecida, você pode enviar um ponto de extremidade de retransmissão de toohello de mensagem. Porque o objeto de conexão Olá herda [fluxo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), enviar os dados como um `byte[]`. Olá mostrado no exemplo a seguir como toodo isso:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

No entanto, se você quiser toosend texto diretamente, sem a necessidade de cadeia de caracteres de saudação tooencode cada vez, você pode encapsular Olá `hybridConnectionStream` do objeto com um [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objeto.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre a retransmissão do Azure, visite esses links:

* [Referência de Microsoft.Azure.Relay](/dotnet/api/microsoft.azure.relay)
* [O que é Retransmissão do Azure?](relay-what-is-it.md)
* [APIs de Retransmissão Disponíveis](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener