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
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a>Arquivos de mídia Hyperlapse com o Azure Media Hyperlapse
O Azure Media Hyperlapse é uma MP (mídia de processador) que cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação.  Olá baseado em nuvem irmão muito[Microsoft Research desktop Pro do Hyperlapse e baseada em telefone celular do Hyperlapse](http://aka.ms/hyperlapse), Hyperlapse Microsoft para serviços de mídia do Azure utiliza grande escala Olá de saudação de mídia do Azure Media Services Processamento plataforma toohorizontally dimensionar e executar em paralelo em massa o processamento do Hyperlapse.

> [!IMPORTANT]
> Microsoft Hyperlapse é projetado toowork melhor sobre o conteúdo da primeira pessoa com uma câmera móvel.  Embora filmagens da câmera ainda podem trabalhar, desempenho de saudação e qualidade do processador de mídia do Azure Media Hyperlapse de saudação não podem ser garantidas para outros tipos de conteúdo.  toolearn mais sobre o Microsoft Hyperlapse para serviços de mídia do Azure e ver alguns vídeos de exemplo, confira Olá [postagem de blog introdutórias](http://aka.ms/azurehyperlapseblog) da visualização pública hello.
> 
> 

Um arquivo de ativo MP4, MOV ou WMV junto com um arquivo de configuração que especifica quais quadros do vídeo devem ser o tempo decorrido e toowhat velocidade de entrada de um trabalho considera como do Azure Media Hyperlapse (por exemplo, primeiro 10.000 quadros em x 2).  saída de Hello é uma representação estabilizar e tempo decorrido de vídeo de entrada hello.

Atualizações mais recentes de Azure Media Hyperlapse hello, consulte [blogs dos serviços de mídia](https://azure.microsoft.com/blog/topics/media-services/).

## <a name="hyperlapse-an-asset"></a>Hyperlapse de um ativo
Primeiro você precisará tooupload tooAzure o arquivo de entrada desejado dos serviços de mídia.  Saiba mais sobre toolearn Olá conceitos envolvidos carregar e gerenciar conteúdo, ler Olá [artigo de gerenciamento de conteúdo](media-services-portal-vod-get-started.md).

### <a id="configuration"></a>Predefinição de configuração para Hyperlapse
Depois que o conteúdo está em sua conta de serviços de mídia, você precisará tooconstruct predefinição de sua configuração.  Olá, a tabela a seguir explica campos de saudação especificado pelo usuário:

| Campo | Descrição |
| --- | --- |
| StartFrame |quadro de saudação após a qual Olá Microsoft Hyperlapse processamento deve começar. |
| NumFrames |número de saudação de quadros tooprocess |
| Velocidade |fator de saudação com qual toospeed o vídeo de entrada hello. |

a seguir Olá é um exemplo de um arquivo de configuração compatível em XML e JSON:

**Predefinição XML:**

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

**Predefinição JSON:**

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

### <a id="sample_code"></a>Microsoft Hyperlapse com hello AMS .NET SDK
Olá método a seguir carrega um arquivo de mídia como um ativo e cria um trabalho com hello processador de mídia do Azure Media Hyperlapse.

> [!NOTE]
> Você já deve ter um CloudMediaContext no escopo com hello "contexto de nome" toowork esse código.  toolearn mais sobre isso, Olá leitura [artigo de gerenciamento de conteúdo](media-services-dotnet-get-started.md).
> 
> [!NOTE]
> argumento de cadeia de caracteres Hello "hyperConfig" é esperado toobe uma configuração compatível predefinida no JSON ou XML, conforme descrito acima.
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

### <a id="file_types"></a>Tipos de arquivo com suporte
* MP4
* MOV
* WMV

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Visão geral do Azure Media Services Analytics](media-services-analytics-overview.md)

[Demonstrações do Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

