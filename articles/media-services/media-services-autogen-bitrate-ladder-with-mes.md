---
title: "tooauto Azure Media Encoder padrão aaaUse-gerar uma taxa de bits Escada | Microsoft Docs"
description: "Este tópico mostra como toouse codificador de mídia padrão (MES) tooauto-gerar uma escada de taxa de bits com base na resolução de entrada hello e taxa de bits. taxa de bits e resolução de entrada hello nunca serão excedidos. Por exemplo, se for de entrada hello 720p em 3 Mbps, a saída será permanecem 720p na melhor das hipóteses e iniciará a taxas inferior a 3 Mbps."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Usar o Azure Media Encoder padrão tooauto-gerar uma escada de taxa de bits

## <a name="overview"></a>Visão geral

Este tópico mostra como toouse codificador de mídia padrão (MES) tooauto-gerar uma escada de taxa de bits (pares de resolução de taxa de bits) com base na resolução de entrada hello e taxa de bits. Olá gerado automaticamente predefinição nunca excederá taxas de bits e a resolução de saudação de entrada. Por exemplo, se for de entrada hello 720p em 3 Mbps, a saída será permanecem 720p na melhor das hipóteses e iniciará a taxas inferior a 3 Mbps.

### <a name="encoding-for-streaming-only"></a>Codificar para Streaming Somente

Se sua intenção for tooencode sua fonte de vídeo somente para streaming, em seguida, é recomendável usar hello "Streaming adaptável" predefinição ao criar uma tarefa de codificação. Ao usar o hello **Streaming adaptável** predefinidos, codificador MES Olá inteligente limitar Escada uma taxa de bits. No entanto, não será capaz de toocontrol Olá codificação custos, desde que o serviço de saudação determina quantos toouse de camadas e em qual resolução. Você pode ver exemplos de camadas de saída produzidos pelo MES como resultado de codificação com hello **Streaming adaptável** predefinição final Olá deste tópico. saudação de saída ativo conterá arquivos MP4 onde áudio e vídeo não são intercalados.

### <a name="encoding-for-streaming-and-progressive-download"></a>Codificação para download progressivo e streaming

Se sua intenção for tooencode o vídeo de origem de streaming, bem como arquivos MP4 com tooproduce para download progressivo, em seguida, é recomendável usar hello "Conteúdo adaptável várias taxas de bits MP4" predefinição ao criar uma tarefa de codificação. Ao usar o hello **conteúdo adaptável MP4 de taxas de bits múltiplas** predefinidos, codificador MES Olá aplicará Olá mesma lógica de codificação, como acima, mas agora Olá ativo de saída conterá MP4 arquivos onde áudio e vídeo são intercalados. Você pode usar um desses arquivos MP4 (por exemplo, Olá versão mais alta taxa de bits) como um arquivo de download progressivo.

## <a id="encoding_with_dotnet"></a>Codificação com o SDK do .NET dos Serviços de Mídia

saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:

- Crie um trabalho de codificação.
- Obtém um codificador de mídia codificador padrão de toohello de referência.
- Adicionar um trabalho toohello codificação e especificar Olá toouse **Streaming adaptável** predefinido. 
- Crie um ativo de saída que conterá o ativo de saudação codificado.
- Adicione o andamento do trabalho um evento manipulador toocheck hello.
- Envie trabalho de saudação.

#### <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemplo

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }
        private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
            default:
                break;
            }
        }
        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
        }
    }

## <a id="output"></a>Saída

Esta seção mostra três exemplos de camadas de saída produzidos pelo MES como resultado de codificação com hello **Streaming adaptável** predefinido. 

### <a name="example-1"></a>Exemplo 1
Fonte com altura "1080" e taxa de quadros "29.970" produz seis camadas de vídeo:

|Camada|Altura|Largura|Taxa de bits (Kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>Exemplo 2
Fonte com altura "720" e taxa de quadros "23.970" produz cinco camadas de vídeo:

|Camada|Altura|Largura|Taxa de bits (Kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>Exemplo 3
Fonte com altura "360" e taxa de quadros "29.970" produz três camadas de vídeo:

|Camada|Altura|Largura|Taxa de bits (Kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Visão geral da codificação de serviços de mídia](media-services-encode-asset.md)

