---
title: "aaaHyperlapse arquivos de mídia com o Azure Media Hyperlapse | Microsoft Docs"
description: "O Azure Media Hyperlapse cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação. Este tópico mostra como toouse indexador de mídia."
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
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="08035-104">Arquivos de mídia Hyperlapse com o Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="08035-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="08035-105">O Azure Media Hyperlapse é uma MP (mídia de processador) que cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação.</span><span class="sxs-lookup"><span data-stu-id="08035-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="08035-106">Olá baseado em nuvem irmão muito[Microsoft Research desktop Pro do Hyperlapse e baseada em telefone celular do Hyperlapse](http://aka.ms/hyperlapse), Hyperlapse Microsoft para serviços de mídia do Azure utiliza grande escala Olá de saudação de mídia do Azure Media Services Processamento plataforma toohorizontally dimensionar e executar em paralelo em massa o processamento do Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="08035-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08035-107">Microsoft Hyperlapse é projetado toowork melhor sobre o conteúdo da primeira pessoa com uma câmera móvel.</span><span class="sxs-lookup"><span data-stu-id="08035-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="08035-108">Embora filmagens da câmera ainda podem trabalhar, desempenho de saudação e qualidade do processador de mídia do Azure Media Hyperlapse de saudação não podem ser garantidas para outros tipos de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="08035-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="08035-109">toolearn mais sobre o Microsoft Hyperlapse para serviços de mídia do Azure e ver alguns vídeos de exemplo, confira Olá [postagem de blog introdutórias](http://aka.ms/azurehyperlapseblog) da visualização pública hello.</span><span class="sxs-lookup"><span data-stu-id="08035-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="08035-110">Um arquivo de ativo MP4, MOV ou WMV junto com um arquivo de configuração que especifica quais quadros do vídeo devem ser o tempo decorrido e toowhat velocidade de entrada de um trabalho considera como do Azure Media Hyperlapse (por exemplo, primeiro 10.000 quadros em x 2).</span><span class="sxs-lookup"><span data-stu-id="08035-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="08035-111">saída de Hello é uma representação estabilizar e tempo decorrido de vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="08035-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="08035-112">Atualizações mais recentes de Azure Media Hyperlapse hello, consulte [blogs dos serviços de mídia](https://azure.microsoft.com/blog/topics/media-services/).</span><span class="sxs-lookup"><span data-stu-id="08035-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="08035-113">Hyperlapse de um ativo</span><span class="sxs-lookup"><span data-stu-id="08035-113">Hyperlapse an asset</span></span>
<span data-ttu-id="08035-114">Primeiro você precisará tooupload tooAzure o arquivo de entrada desejado dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="08035-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="08035-115">Saiba mais sobre toolearn Olá conceitos envolvidos carregar e gerenciar conteúdo, ler Olá [artigo de gerenciamento de conteúdo](media-services-portal-vod-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="08035-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="08035-116"><a id="configuration"></a>Predefinição de configuração para Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="08035-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="08035-117">Depois que o conteúdo está em sua conta de serviços de mídia, você precisará tooconstruct predefinição de sua configuração.</span><span class="sxs-lookup"><span data-stu-id="08035-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="08035-118">Olá, a tabela a seguir explica campos de saudação especificado pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="08035-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="08035-119">Campo</span><span class="sxs-lookup"><span data-stu-id="08035-119">Field</span></span> | <span data-ttu-id="08035-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="08035-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08035-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="08035-121">StartFrame</span></span> |<span data-ttu-id="08035-122">quadro de saudação após a qual Olá Microsoft Hyperlapse processamento deve começar.</span><span class="sxs-lookup"><span data-stu-id="08035-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="08035-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="08035-123">NumFrames</span></span> |<span data-ttu-id="08035-124">número de saudação de quadros tooprocess</span><span class="sxs-lookup"><span data-stu-id="08035-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="08035-125">Velocidade</span><span class="sxs-lookup"><span data-stu-id="08035-125">Speed</span></span> |<span data-ttu-id="08035-126">fator de saudação com qual toospeed o vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="08035-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="08035-127">a seguir Olá é um exemplo de um arquivo de configuração compatível em XML e JSON:</span><span class="sxs-lookup"><span data-stu-id="08035-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="08035-128">**Predefinição XML:**</span><span class="sxs-lookup"><span data-stu-id="08035-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="08035-129">**Predefinição JSON:**</span><span class="sxs-lookup"><span data-stu-id="08035-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="08035-130"><a id="sample_code"></a>Microsoft Hyperlapse com hello AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="08035-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="08035-131">Olá método a seguir carrega um arquivo de mídia como um ativo e cria um trabalho com hello processador de mídia do Azure Media Hyperlapse.</span><span class="sxs-lookup"><span data-stu-id="08035-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="08035-132">Você já deve ter um CloudMediaContext no escopo com hello "contexto de nome" toowork esse código.</span><span class="sxs-lookup"><span data-stu-id="08035-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="08035-133">toolearn mais sobre isso, Olá leitura [artigo de gerenciamento de conteúdo](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="08035-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="08035-134">argumento de cadeia de caracteres Hello "hyperConfig" é esperado toobe uma configuração compatível predefinida no JSON ou XML, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="08035-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
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

            // If job state is Error, hello event handling
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

### <span data-ttu-id="08035-135"><a id="file_types"></a>Tipos de arquivo com suporte</span><span class="sxs-lookup"><span data-stu-id="08035-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="08035-136">MP4</span><span class="sxs-lookup"><span data-stu-id="08035-136">MP4</span></span>
* <span data-ttu-id="08035-137">MOV</span><span class="sxs-lookup"><span data-stu-id="08035-137">MOV</span></span>
* <span data-ttu-id="08035-138">WMV</span><span class="sxs-lookup"><span data-stu-id="08035-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="08035-139">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="08035-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="08035-140">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="08035-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="08035-141">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="08035-141">Related links</span></span>
[<span data-ttu-id="08035-142">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="08035-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="08035-143">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="08035-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

