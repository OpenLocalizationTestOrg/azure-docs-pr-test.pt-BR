---
title: "aaaEncode um ativo com o codificador de mídia padrão usando o .NET | Microsoft Docs"
description: "Este tópico mostra como toouse .NET tooencode um ativo usando o padrão de codificador de mídia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>Codificar um ativo com o Codificador de Mídia Padrão usando o .NET
Trabalhos de codificação são uma das operações de processamento mais comuns Olá nos serviços de mídia. Criar arquivos de mídia de tooconvert trabalhos codificação de um tooanother de codificação. Ao codificar, você pode usar o hello Media Encoder interno dos serviços de mídia. Você também pode usar um codificador fornecido por um parceiro de serviços de mídia; codificadores de terceiros estão disponíveis por meio de saudação do Azure Marketplace. 

Este tópico mostra como toouse .NET tooencode seus ativos com o Media Encoder padrão (MES). Codificador de mídia padrão é configurado usando uma das predefinições de codificador Olá descritas [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

É recomendável tooalways codificar seus arquivos de origem em uma conjunto de MP4 de taxa de bits adaptável e, em seguida, converter Olá toohello desejado formato de conjunto usando Olá [empacotamento dinâmico](media-services-dynamic-packaging-overview.md). 

Se seu ativo de saída tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos. Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md).

> [!NOTE]
> Produz MES um arquivo de saída com um nome que contenha Olá primeiros 32 caracteres do hello nome de arquivo de entrada. nome Hello baseia-se no que é especificado no arquivo de predefinição hello. Por exemplo, "FileName": "{Basename}_{Index}{Extension}". {Nome base} é substituído pelo Olá primeiros 32 caracteres do nome de arquivo de entrada hello.
> 
> 

### <a name="mes-formats"></a>Formatos de MES
[Formatos e codecs](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>Predefinições de MES
Codificador de mídia padrão é configurado usando uma das predefinições de codificador Olá descritas [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadados de entrada e saída
Ao codificar um ativo de entrada (ou ativos) usando MES, você obtém um ativo de saída em Olá conclusão bem-sucedida do que codificar a tarefa. Olá ativo de saída contém vídeo, áudio, miniaturas, manifesto, etc, com base na predefinição de codificação Olá que você usar.

Olá ativo de saída também contém um arquivo com metadados sobre o ativo de entrada hello. nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: < asset_id > <asset_id>_metadata.XML (por exemplo, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), onde < asset_id > é o valor AssetId de saudação do ativo de entrada hello. Olá esquema de entrada metadados XML descrita [aqui](media-services-input-metadata-schema.md).

Olá ativo de saída também contém um arquivo com metadados sobre o ativo de saída hello. nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: < source_file_name>_manifest.XML > <nome_do_arquivo_de_origem>_manifest.XML (por exemplo, BigBuckBunny_manifest.xml). esquema de saudação desses metadados de saída XML é descrito [aqui](media-services-output-metadata-schema.md).

Se quiser tooexamine qualquer um dos arquivos de metadados de saudação dois, você pode criar um localizador SAS e baixar o computador do local de tooyour do arquivo hello. Você pode encontrar um exemplo de como toocreate um localizador SAS e baixar uma arquivo usando Olá dos serviços de mídia extensões do SDK do .NET.

## <a name="download-sample"></a>Baixar exemplo
Você pode obter e executar um exemplo que mostra como tooencode com MES de [aqui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).

## <a name="net-sample-code"></a>Código de exemplo do .NET

saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:

* Crie um trabalho de codificação.
* Obtém um codificador de mídia codificador padrão de toohello de referência.
* Especificar Olá toouse [Streaming adaptável](media-services-autogen-bitrate-ladder-with-mes.md) predefinido. 
* Adicione um único trabalho de toohello de tarefa de codificação. 
* Especifique a entrada hello toobe ativo codificado.
* Crie um ativo de saída que conterá o ativo de saudação codificado.
* Adicione o andamento do trabalho um evento manipulador toocheck hello.
* Envie trabalho de saudação.

#### <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 

#### <a name="example"></a>Exemplo 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Próximas etapas
[Como toogenerate miniatura usando o codificador de mídia padrão com o .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[codificação visão geral de serviços de mídia](media-services-encode-asset.md)

