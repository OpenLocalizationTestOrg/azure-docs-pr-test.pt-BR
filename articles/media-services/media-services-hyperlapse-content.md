---
title: "Arquivos de mídia do Hyperlapse com o Azure Media Hyperlapse | Microsoft Docs"
description: "O Azure Media Hyperlapse cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação. Este tópico mostra como usar o indexador de mídia."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="24851-104">Arquivos de mídia Hyperlapse com o Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="24851-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="24851-105">O Azure Media Hyperlapse é uma MP (mídia de processador) que cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação.</span><span class="sxs-lookup"><span data-stu-id="24851-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="24851-106">O equivalente baseado em nuvem do [Hyperlapse Pro da Microsoft Research para a área de trabalho e do Hyperlapse Mobile baseado em celular](http://aka.ms/hyperlapse), o Microsoft Hyperlapse para os Serviços de Mídia do Azure utiliza a escala em massa da plataforma de Processamento de Mídia dos Serviços de Mídia do Azure para dimensionar horizontalmente e executar em paralelo o processamento em massa do Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="24851-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24851-107">O Microsoft Hyperlapse foi projetado para funcionar melhor em conteúdo de primeira pessoa com uma câmera em movimento.</span><span class="sxs-lookup"><span data-stu-id="24851-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="24851-108">Embora a filmagem de imagens com câmera fotográfica ainda possa funcionar, o desempenho e a qualidade do Processador de Mídia do Azure Media Hyperlapse não podem ser garantidos para outros tipos de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="24851-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="24851-109">Para saber mais sobre o Microsoft Hyperlapse para os Serviços de Mídia do Azure e ver alguns vídeos de exemplo, confira a [postagem de blog introdutória](http://aka.ms/azurehyperlapseblog) da visualização pública.</span><span class="sxs-lookup"><span data-stu-id="24851-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="24851-110">Um trabalho do Azure Media Hyperlapse utiliza como entrada um arquivo de ativo MP4, MOV ou WMV junto com um arquivo de configuração que especifica quais quadros de vídeo devem ser de lapso de tempo e com qual velocidade (por exemplo, os primeiros 10.000 quadros em 2x).</span><span class="sxs-lookup"><span data-stu-id="24851-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="24851-111">A saída é uma representação estabilizada e de lapso de tempo do vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="24851-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="24851-112">Para as atualizações mais recentes do Azure Media Hyperlapse, consulte [blogs dos serviços de mídia](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="24851-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="24851-113">Hyperlapse de um ativo</span><span class="sxs-lookup"><span data-stu-id="24851-113">Hyperlapse an asset</span></span>
<span data-ttu-id="24851-114">Primeiro, você precisará carregar o arquivo de entrada desejado nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="24851-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="24851-115">Para saber mais sobre os conceitos envolvidos no carregamento e gerenciamento de conteúdo, leia o [artigo sobre gerenciamento de conteúdo](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="24851-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="24851-116"><a id="configuration"></a>Predefinição de configuração para Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="24851-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="24851-117">Quando o conteúdo estiver em sua conta de Serviços de Mídia, você precisará construir a predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="24851-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="24851-118">A tabela a seguir explica os campos especificados pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="24851-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="24851-119">Campo</span><span class="sxs-lookup"><span data-stu-id="24851-119">Field</span></span> | <span data-ttu-id="24851-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="24851-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24851-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="24851-121">StartFrame</span></span> |<span data-ttu-id="24851-122">O quadro no qual o processamento do Microsoft Hyperlapse deve começar.</span><span class="sxs-lookup"><span data-stu-id="24851-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="24851-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="24851-123">NumFrames</span></span> |<span data-ttu-id="24851-124">O número de quadros a serem processados</span><span class="sxs-lookup"><span data-stu-id="24851-124">The number of frames to process</span></span> |
| <span data-ttu-id="24851-125">Velocidade</span><span class="sxs-lookup"><span data-stu-id="24851-125">Speed</span></span> |<span data-ttu-id="24851-126">O fator de acordo com o qual acelerar o vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="24851-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="24851-127">A seguir há um exemplo de um arquivo de configuração compatível em XML e JSON:</span><span class="sxs-lookup"><span data-stu-id="24851-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="24851-128">**Predefinição XML:**</span><span class="sxs-lookup"><span data-stu-id="24851-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="24851-129">**Predefinição JSON:**</span><span class="sxs-lookup"><span data-stu-id="24851-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <span data-ttu-id="24851-130"><a id="sample_code"></a> Microsoft Hyperlapse com o SDK do .NET AMS</span><span class="sxs-lookup"><span data-stu-id="24851-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="24851-131">O método a seguir carrega um arquivo de mídia como um ativo e cria um trabalho com o Processador de Mídia do Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="24851-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="24851-132">Você já deve ter um CloudMediaContext no escopo com o nome "contexto" para que esse código funcione.</span><span class="sxs-lookup"><span data-stu-id="24851-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="24851-133">Para saber mais sobre isso, leia o [artigo sobre gerenciamento de conteúdo](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="24851-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="24851-134">O argumento de cadeia de caracteres "hyperConfig" deve ser uma configuração compatível predefinida em JSON ou XML, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="24851-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
            progressJobTask.Wait();

            // If job state is Error, the event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                Console.WriteLine(string.Format("Error: {0}. {1}",
                                                error.Code,
                                                error.Message));  
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <span data-ttu-id="24851-135"><a id="file_types"></a>Tipos de arquivo com suporte</span><span class="sxs-lookup"><span data-stu-id="24851-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="24851-136">MP4</span><span class="sxs-lookup"><span data-stu-id="24851-136">MP4</span></span>
* <span data-ttu-id="24851-137">MOV</span><span class="sxs-lookup"><span data-stu-id="24851-137">MOV</span></span>
* <span data-ttu-id="24851-138">WMV</span><span class="sxs-lookup"><span data-stu-id="24851-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="24851-139">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="24851-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24851-140">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="24851-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="24851-141">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="24851-141">Related links</span></span>
[<span data-ttu-id="24851-142">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="24851-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="24851-143">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="24851-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

