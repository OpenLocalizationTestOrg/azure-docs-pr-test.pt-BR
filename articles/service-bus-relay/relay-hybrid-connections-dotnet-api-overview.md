---
title: "Visão geral das APIs .NET Standard de Retransmissão do Azure | Microsoft Docs"
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="4a2e1-103">Visão geral da API .NET Standard de Conexões Híbridas de Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="4a2e1-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="4a2e1-104">Este artigo resume algumas das principais [APIs de cliente](/dotnet/api/microsoft.azure.relay) .NET Standard de Conexões Híbridas de Retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="4a2e1-105">Construtor de Cadeia de Conexão de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="4a2e1-105">Relay Connection String Builder</span></span>

<span data-ttu-id="4a2e1-106">A classe [RelayConnectionStringBuilder][RelayConnectionStringBuilder] formata cadeias de conexão que são específicas para Conexões Híbridas de Retransmissão.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="4a2e1-107">Você pode usá-la para verificar o formato de uma cadeia de conexão ou para criar uma cadeia de conexão do zero.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="4a2e1-108">Veja o código a seguir para obter um exemplo:</span><span class="sxs-lookup"><span data-stu-id="4a2e1-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="4a2e1-109">Você também pode passar uma cadeia de conexão diretamente para o método `RelayConnectionStringBuilder`.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="4a2e1-110">Esta operação permite que você verifique se a cadeia de conexão está em um formato válido.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="4a2e1-111">Se qualquer um dos parâmetros for inválido, o construtor gerará um `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="4a2e1-112">Fluxo de Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="4a2e1-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="4a2e1-113">Se você estiver trabalhando com um [HybridConnectionClient][HCClient] ou um [HybridConnectionListener][HCListener], a classe [HybridConnectionStream][HCStream] será o objeto principal usado para enviar e receber dados de um ponto de extremidade de retransmissão do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="4a2e1-114">Obter um Fluxo de Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="4a2e1-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="4a2e1-115">Ouvinte</span><span class="sxs-lookup"><span data-stu-id="4a2e1-115">Listener</span></span>
<span data-ttu-id="4a2e1-116">Usando um [HybridConnectionListener][HCListener], você pode obter um `HybridConnectionStream` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4a2e1-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="4a2e1-117">Cliente</span><span class="sxs-lookup"><span data-stu-id="4a2e1-117">Client</span></span>
<span data-ttu-id="4a2e1-118">Usando um [HybridConnectionClient][HCClient], você pode obter um objeto `HybridConnectionStream` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4a2e1-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="4a2e1-119">Recebendo dados</span><span class="sxs-lookup"><span data-stu-id="4a2e1-119">Receiving data</span></span>
<span data-ttu-id="4a2e1-120">A classe [HybridConnectionStream][HCStream] permite comunicação bidirecional.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="4a2e1-121">Na maioria dos casos de uso, você recebe continuamente do fluxo.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="4a2e1-122">Se você estiver lendo o texto do fluxo, talvez você queira usar um objeto [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx), que permite a análise mais fácil dos dados.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="4a2e1-123">Por exemplo, você pode ler os dados como texto em vez de como `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="4a2e1-124">O código a seguir lê linhas de texto individuais do fluxo até que um cancelamento seja solicitado:</span><span class="sxs-lookup"><span data-stu-id="4a2e1-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="4a2e1-125">Enviar dados</span><span class="sxs-lookup"><span data-stu-id="4a2e1-125">Sending data</span></span>
<span data-ttu-id="4a2e1-126">Quando você tiver uma conexão estabelecida, você poderá enviar uma mensagem para o ponto de extremidade de Retransmissão.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="4a2e1-127">Já que o objeto de conexão herda o [Fluxo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), envie os dados como um `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="4a2e1-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="4a2e1-128">O exemplo a seguir mostra como fazer isso:</span><span class="sxs-lookup"><span data-stu-id="4a2e1-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="4a2e1-129">No entanto, se você deseja enviar texto diretamente, sem a necessidade de codificar a cadeia de caracteres a cada vez, você pode encapsular o objeto `hybridConnectionStream` com um objeto [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="4a2e1-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="4a2e1-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a2e1-130">Next steps</span></span>
<span data-ttu-id="4a2e1-131">Para saber mais sobre a Retransmissão do Azure, visite estes links:</span><span class="sxs-lookup"><span data-stu-id="4a2e1-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="4a2e1-132">Referência de Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="4a2e1-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="4a2e1-133">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="4a2e1-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="4a2e1-134">APIs de Retransmissão Disponíveis</span><span class="sxs-lookup"><span data-stu-id="4a2e1-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener