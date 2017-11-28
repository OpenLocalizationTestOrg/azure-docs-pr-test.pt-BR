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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="f200e-103">Visão geral da API .NET Standard de Conexões Híbridas de Retransmissão do Azure</span><span class="sxs-lookup"><span data-stu-id="f200e-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="f200e-104">Este artigo resume algumas das chave de hello Azure retransmissão híbrida conexões .NET Standard [APIs de cliente](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="f200e-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="f200e-105">Construtor de Cadeia de Conexão de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="f200e-105">Relay Connection String Builder</span></span>

<span data-ttu-id="f200e-106">Olá [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe formatos de cadeias de caracteres de conexão que são as conexões híbridas tooRelay específico.</span><span class="sxs-lookup"><span data-stu-id="f200e-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="f200e-107">Você pode usá-lo tooverify formato de saudação de uma cadeia de caracteres de conexão ou toobuild uma cadeia de caracteres de conexão do zero.</span><span class="sxs-lookup"><span data-stu-id="f200e-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="f200e-108">Consulte Olá código para obter um exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f200e-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="f200e-109">Você também pode passar uma conexão de cadeia de caracteres diretamente toohello `RelayConnectionStringBuilder` método.</span><span class="sxs-lookup"><span data-stu-id="f200e-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="f200e-110">Esta operação permite que você tooverify a cadeia de caracteres de conexão hello está em um formato válido.</span><span class="sxs-lookup"><span data-stu-id="f200e-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="f200e-111">Se qualquer um dos parâmetros de saudação são inválidos, o construtor hello gera um `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="f200e-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="f200e-112">Fluxo de Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="f200e-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="f200e-113">Olá [HybridConnectionStream] [ HCStream] classe é toosend de objeto primário usado hello e receber dados de um ponto de extremidade de retransmissão do Azure, se você estiver trabalhando com um [HybridConnectionClient] [ HCClient], ou um [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="f200e-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="f200e-114">Obter um Fluxo de Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="f200e-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="f200e-115">Ouvinte</span><span class="sxs-lookup"><span data-stu-id="f200e-115">Listener</span></span>
<span data-ttu-id="f200e-116">Usando um [HybridConnectionListener][HCListener], você pode obter um `HybridConnectionStream` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f200e-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="f200e-117">Cliente</span><span class="sxs-lookup"><span data-stu-id="f200e-117">Client</span></span>
<span data-ttu-id="f200e-118">Usando um [HybridConnectionClient][HCClient], você pode obter um objeto `HybridConnectionStream` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f200e-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="f200e-119">Recebendo dados</span><span class="sxs-lookup"><span data-stu-id="f200e-119">Receiving data</span></span>
<span data-ttu-id="f200e-120">Olá [HybridConnectionStream] [ HCStream] classe habilita comunicação bidirecional.</span><span class="sxs-lookup"><span data-stu-id="f200e-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="f200e-121">Na maioria dos casos, você recebe continuamente de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f200e-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="f200e-122">Se você estiver lendo texto de fluxo de saudação, talvez você queira toouse um [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objeto, que habilita a análise mais fácil de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f200e-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="f200e-123">Por exemplo, você pode ler os dados como texto em vez de como `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="f200e-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="f200e-124">Hello código a seguir lê linhas de texto individuais de fluxo de saudação até que um cancelamento é solicitado:</span><span class="sxs-lookup"><span data-stu-id="f200e-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="f200e-125">Enviar dados</span><span class="sxs-lookup"><span data-stu-id="f200e-125">Sending data</span></span>
<span data-ttu-id="f200e-126">Depois que você tiver uma conexão estabelecida, você pode enviar um ponto de extremidade de retransmissão de toohello de mensagem.</span><span class="sxs-lookup"><span data-stu-id="f200e-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="f200e-127">Porque o objeto de conexão Olá herda [fluxo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), enviar os dados como um `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="f200e-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="f200e-128">Olá mostrado no exemplo a seguir como toodo isso:</span><span class="sxs-lookup"><span data-stu-id="f200e-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="f200e-129">No entanto, se você quiser toosend texto diretamente, sem a necessidade de cadeia de caracteres de saudação tooencode cada vez, você pode encapsular Olá `hybridConnectionStream` do objeto com um [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objeto.</span><span class="sxs-lookup"><span data-stu-id="f200e-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="f200e-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f200e-130">Next steps</span></span>
<span data-ttu-id="f200e-131">toolearn mais informações sobre a retransmissão do Azure, visite esses links:</span><span class="sxs-lookup"><span data-stu-id="f200e-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="f200e-132">Referência de Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="f200e-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="f200e-133">O que é Retransmissão do Azure?</span><span class="sxs-lookup"><span data-stu-id="f200e-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="f200e-134">APIs de Retransmissão Disponíveis</span><span class="sxs-lookup"><span data-stu-id="f200e-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener