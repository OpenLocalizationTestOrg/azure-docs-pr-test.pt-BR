---
title: Gerenciar pontos de extremidade de streaming com o SDK .NET. | Microsoft Docs
description: "Este tópico mostra como gerenciar pontos de extremidade de streaming usando o portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="9b816-104">Gerenciar pontos de extremidade de streaming com o SDK .NET</span><span class="sxs-lookup"><span data-stu-id="9b816-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="9b816-105">Certifique-se de examinar o tópico [Visão geral](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b816-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="9b816-106">Além disso, revise [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="9b816-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="9b816-107">O código deste tópico mostra como realizar as seguintes tarefas usando o SDK do .NET dos Serviços de Mídia do Azure:</span><span class="sxs-lookup"><span data-stu-id="9b816-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="9b816-108">Examine o ponto de extremidade de streaming padrão.</span><span class="sxs-lookup"><span data-stu-id="9b816-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="9b816-109">Crie ou adicione um novo ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="9b816-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="9b816-110">Você talvez queira ter vários pontos de extremidade de streaming se planeja ter diferentes CDNs ou um CDN e acesso direto.</span><span class="sxs-lookup"><span data-stu-id="9b816-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b816-111">Você será cobrado apenas quando seu ponto de extremidade de streaming estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="9b816-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="9b816-112">Atualize o ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="9b816-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="9b816-113">Certifique-se de chamar a função Update().</span><span class="sxs-lookup"><span data-stu-id="9b816-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="9b816-114">Exclua o ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="9b816-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9b816-115">O ponto de extremidade de streaming não pode ser excluído.</span><span class="sxs-lookup"><span data-stu-id="9b816-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="9b816-116">Para obter informações sobre como dimensionar o ponto de extremidade de streaming, consulte [este](media-services-portal-scale-streaming-endpoints.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="9b816-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9b816-117">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b816-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="9b816-118">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9b816-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="9b816-119">Adicionar o código que gerencia os pontos de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="9b816-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="9b816-120">Substitua o código de Program.cs pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b816-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="9b816-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b816-121">Next steps</span></span>
<span data-ttu-id="9b816-122">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="9b816-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9b816-123">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="9b816-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

