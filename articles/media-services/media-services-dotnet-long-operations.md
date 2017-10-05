---
title: "Operações de Sondagem de Longa Execução | Microsoft Docs"
description: "Este tópico mostra como sondar as operações de longa execução."
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
ms.openlocfilehash: 7123a2d44d3b7c332afe30fb0fcea88ca29e313a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="3a7ba-103">Fornecendo mídia sob demanda com os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="3a7ba-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="3a7ba-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3a7ba-104">Overview</span></span>

<span data-ttu-id="3a7ba-105">Os Serviços de Mídia do Microsoft Azure oferecem APIs que enviam solicitações aos Serviços de Mídia para iniciar operações (por exemplo: criar, iniciar, interromper ou excluir um canal).</span><span class="sxs-lookup"><span data-stu-id="3a7ba-105">Microsoft Azure Media Services offers APIs that send requests to Media Services to start operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="3a7ba-106">Essas operações são de execução longa.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-106">These operations are long-running.</span></span>

<span data-ttu-id="3a7ba-107">O SDK .NET de Serviços de Mídia fornece APIs que enviam a solicitação e aguardam a conclusão da operação (internamente, as APIs realizam a sondagem do andamento da operação em intervalos).</span><span class="sxs-lookup"><span data-stu-id="3a7ba-107">The Media Services .NET SDK provides APIs that send the request and wait for the operation to complete (internally, the APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="3a7ba-108">Por exemplo, quando você chama o channel.Start(), o método retorna depois que o canal é iniciado.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-108">For example, when you call channel.Start(), the method returns after the channel is started.</span></span> <span data-ttu-id="3a7ba-109">Você também pode usar a versão assíncrona: await channel.StartAsync() (para obter informações sobre o padrão assíncrono baseado em tarefa, consulte [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="3a7ba-109">You can also use the asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="3a7ba-110">"Métodos de sondagem" é como são chamadas as APIs que enviam uma solicitação de operação e então sondam o status até que a operação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-110">APIs that send an operation request and then poll for the status until the operation is complete are called “polling methods”.</span></span> <span data-ttu-id="3a7ba-111">Esses métodos (especialmente a versão assíncrona) são recomendados para aplicativos cliente sofisticados e/ou serviços com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-111">These methods (especially the Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="3a7ba-112">Existem cenários em que um aplicativo não pode esperar uma solicitação http de execução longa e desejar sondar o andamento da operação manualmente.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-112">There are scenarios where an application cannot wait for a long running http request and wants to poll for the operation progress manually.</span></span> <span data-ttu-id="3a7ba-113">Um exemplo típico seria um navegador interagindo com um serviço Web sem monitoração de estado: quando o navegador solicita a criação de um canal, o serviço Web inicia uma operação de execução longa e retorna a ID da operação para o navegador.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-113">A typical example would be a browser interacting with a stateless web service: when the browser requests to create a channel, the web service initiates a long running operation and returns the operation ID to the browser.</span></span> <span data-ttu-id="3a7ba-114">O navegador pode pedir ao serviço Web para obter o status da operação com base na ID.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-114">The browser could then ask the web service to get the operation status based on the ID.</span></span> <span data-ttu-id="3a7ba-115">O SDK .NET dos Serviços de Mídia fornece APIs úteis para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-115">The Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="3a7ba-116">Essas APIs são chamadas de "métodos sem sondagem".</span><span class="sxs-lookup"><span data-stu-id="3a7ba-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="3a7ba-117">Os "métodos sem sondagem" têm o padrão de nomenclatura a seguir: Send*OperationName*Operation (por exemplo, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="3a7ba-117">The “non-polling methods” have the following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="3a7ba-118">Os métodos Send*OperationName*Operation retornam o objeto **IOperation** ; o objeto retornado contém informações que podem ser usadas para controlar a operação.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-118">Send*OperationName*Operation methods return the **IOperation** object; the returned object contains information that can be used to track the operation.</span></span> <span data-ttu-id="3a7ba-119">Os métodos Send*OperationName*OperationAsync retornam **Task<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-119">The Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="3a7ba-120">Atualmente, as classes a seguir dão suporte a métodos sem sondagem: **Channel**, **StreamingEndpoint** e **Program**.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-120">Currently, the following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="3a7ba-121">Para monitorar o status da operação, use o método **GetOperation** na classe **OperationBaseCollection**.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-121">To poll for the operation status, use the **GetOperation** method on the **OperationBaseCollection** class.</span></span> <span data-ttu-id="3a7ba-122">Use os seguintes intervalos para verificar o status da operação: para as operações **Channel** e **StreamingEndpoint**, use 30 segundos; para operações **Program**, use 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-122">Use the following intervals to check the operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3a7ba-123">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3a7ba-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3a7ba-124">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3a7ba-124">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="3a7ba-125">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3a7ba-125">Example</span></span>

<span data-ttu-id="3a7ba-126">O exemplo a seguir define uma classe chamada **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-126">The following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="3a7ba-127">Essa definição de classe pode ser um ponto de partida para a definição de classe de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="3a7ba-128">Para simplificar, os exemplos a seguir usam as versões de métodos não assíncronas.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-128">For simplicity, the following examples use the non-async versions of methods.</span></span>

<span data-ttu-id="3a7ba-129">O exemplo também mostra como o cliente pode usar essa classe.</span><span class="sxs-lookup"><span data-stu-id="3a7ba-129">The example also shows how the client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="3a7ba-130">Definição da classe ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="3a7ba-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// The ChannelOperations class only implements 
    /// the Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from the App.config file.
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
        /// Initiates the creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name to be given to the new channel</param>  
        /// <returns>  
        /// Operation Id for the long running operation being executed by Media Services. 
        /// Use this operation Id to poll for the channel creation status. 
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
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created channel Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the created channel Id is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle the failure. 
                    // For example, throw an exception. 
                    // Use the following information in the exception: operationId, operation.ErrorMessage.
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

### <a name="the-client-code"></a><span data-ttu-id="3a7ba-131">O código do cliente</span><span class="sxs-lookup"><span data-stu-id="3a7ba-131">The client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have the newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="3a7ba-132">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="3a7ba-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3a7ba-133">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="3a7ba-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

