---
title: "Operações de execução longa de aaaPolling | Microsoft Docs"
description: "Este tópico mostra como toopoll operações de execução longa."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="253eb-103">Fornecendo mídia sob demanda com os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="253eb-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="253eb-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="253eb-104">Overview</span></span>

<span data-ttu-id="253eb-105">Serviços de mídia do Microsoft Azure oferece APIs que enviam solicitações de operações de toostart tooMedia serviços (por exemplo: criar, iniciar, interromper ou excluir um canal).</span><span class="sxs-lookup"><span data-stu-id="253eb-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="253eb-106">Essas operações são de execução longa.</span><span class="sxs-lookup"><span data-stu-id="253eb-106">These operations are long-running.</span></span>

<span data-ttu-id="253eb-107">Olá Media Services .NET SDK fornece APIs que enviar solicitação hello e aguarde Olá toocomplete de operação (internamente, Olá APIs estão sondando o andamento da operação em alguns intervalos).</span><span class="sxs-lookup"><span data-stu-id="253eb-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="253eb-108">Por exemplo, quando você chama o canal. Start (), o método hello retorna depois do início do canal de saudação.</span><span class="sxs-lookup"><span data-stu-id="253eb-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="253eb-109">Você também pode usar a versão assíncrona Olá: await canal. StartAsync() (para obter informações sobre o padrão assíncrono baseado em tarefa, consulte [toque](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="253eb-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="253eb-110">APIs que enviam uma solicitação de operação e então sondam status Olá até Olá operação ser concluída são chamadas de "métodos de sondagem".</span><span class="sxs-lookup"><span data-stu-id="253eb-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="253eb-111">Esses métodos (especialmente versão assíncrona Olá) são recomendados para aplicativos cliente avançados e/ou serviços com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="253eb-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="253eb-112">Há cenários em que um aplicativo não puder aguardar uma solicitação http em tempo de execução e deseja toopoll de andamento da operação Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="253eb-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="253eb-113">Um exemplo típico seria um navegador interagindo com um serviço web sem monitoração de estado: quando o navegador Olá solicitações toocreate um canal, serviço web de saudação inicia uma operação de longa duração e retorna Olá navegador de toohello de ID de operação.</span><span class="sxs-lookup"><span data-stu-id="253eb-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="253eb-114">navegador de saudação pode então solicitar Olá web serviço tooget Olá status da operação com base na ID de saudação.</span><span class="sxs-lookup"><span data-stu-id="253eb-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="253eb-115">Olá Media Services .NET SDK fornece APIs que são úteis para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="253eb-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="253eb-116">Essas APIs são chamadas de "métodos sem sondagem".</span><span class="sxs-lookup"><span data-stu-id="253eb-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="253eb-117">Olá, "métodos sem sondagem" têm saudação padrão de nomenclatura a seguir: enviar*OperationName*operação (por exemplo, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="253eb-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="253eb-118">Enviar*OperationName*métodos de operação retornam Olá **IOperation** objeto; hello, objeto retornado contém informações que podem ser usados tootrack Olá operação.</span><span class="sxs-lookup"><span data-stu-id="253eb-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="253eb-119">Olá enviar*OperationName*OperationAsync métodos retornam **tarefa<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="253eb-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="253eb-120">Atualmente, Olá métodos sem sondagem de classes de suporte a seguir: **Channel**, **StreamingEndpoint**, e **programa**.</span><span class="sxs-lookup"><span data-stu-id="253eb-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="253eb-121">toopoll para o status da operação hello, use Olá **GetOperation** método hello **OperationBaseCollection** classe.</span><span class="sxs-lookup"><span data-stu-id="253eb-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="253eb-122">Use Olá status da operação de saudação toocheck intervalos a seguir: para **Channel** e **StreamingEndpoint** operações, use 30 segundos; para **programa** operações, use 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="253eb-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="253eb-123">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="253eb-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="253eb-124">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="253eb-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="253eb-125">Exemplo</span><span class="sxs-lookup"><span data-stu-id="253eb-125">Example</span></span>

<span data-ttu-id="253eb-126">Olá, exemplo a seguir define uma classe chamada **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="253eb-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="253eb-127">Essa definição de classe pode ser um ponto de partida para a definição de classe de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="253eb-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="253eb-128">Para simplificar, hello exemplos a seguir usam versões assíncronas não Olá métodos.</span><span class="sxs-lookup"><span data-stu-id="253eb-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="253eb-129">exemplo Hello também mostra como o cliente Olá pode usar essa classe.</span><span class="sxs-lookup"><span data-stu-id="253eb-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="253eb-130">Definição da classe ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="253eb-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="253eb-131">código de saudação do cliente</span><span class="sxs-lookup"><span data-stu-id="253eb-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="253eb-132">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="253eb-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="253eb-133">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="253eb-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

