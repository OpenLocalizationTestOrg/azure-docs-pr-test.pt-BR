---
title: aaaManage pontos de extremidade com o SDK .NET de streaming. | Microsoft Docs
description: "Este tópico mostra como pontos de extremidade de streaming de toomanage com hello portal do Azure."
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
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="03859-104">Gerenciar pontos de extremidade de streaming com o SDK .NET</span><span class="sxs-lookup"><span data-stu-id="03859-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="03859-105">Verifique se Olá de tooreview [visão geral](media-services-streaming-endpoints-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="03859-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="03859-106">Além disso, revise [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="03859-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="03859-107">código de saudação neste tópico mostra como Olá toodo seguintes tarefas usando Olá SDK do Azure Media Services .NET:</span><span class="sxs-lookup"><span data-stu-id="03859-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="03859-108">Examine o padrão de saudação ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="03859-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="03859-109">Crie ou adicione um novo ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="03859-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="03859-110">Convém toohave vários pontos de extremidade de streaming se você planejar toohave CDNs diferentes ou um CDN e acesso direto.</span><span class="sxs-lookup"><span data-stu-id="03859-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="03859-111">Você será cobrado apenas quando seu ponto de extremidade de streaming estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="03859-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="03859-112">Atualize Olá ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="03859-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="03859-113">Certifique-se de que toocall Olá função Update ().</span><span class="sxs-lookup"><span data-stu-id="03859-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="03859-114">Exclua ponto de extremidade de streaming de saudação.</span><span class="sxs-lookup"><span data-stu-id="03859-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="03859-115">padrão de saudação ponto de extremidade de streaming não pode ser excluído.</span><span class="sxs-lookup"><span data-stu-id="03859-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="03859-116">Para obter informações sobre como tooscale Olá ponto de extremidade de streaming, consulte [isso](media-services-portal-scale-streaming-endpoints.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="03859-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="03859-117">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03859-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="03859-118">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="03859-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="03859-119">Adicionar o código que gerencia os pontos de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="03859-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="03859-120">Substitua o código de saudação em Olá Program.cs com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="03859-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
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


## <a name="next-steps"></a><span data-ttu-id="03859-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03859-121">Next steps</span></span>
<span data-ttu-id="03859-122">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="03859-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="03859-123">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="03859-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

