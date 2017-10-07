---
title: "codificação de aaaAdvanced com o fluxo de trabalho do Media Encoder Premium | Microsoft Docs"
description: "Saiba como tooencode com fluxo de trabalho Premium de codificador de mídia. Exemplos de código são escritos em c# e usam Olá SDK do Media Services para .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>Codificação avançada com fluxo de trabalho do Media Encoder Premium
> [!NOTE]
> O processador de mídia do Fluxo de Trabalho do Media Encoder Premium analisado neste tópico não está disponível na China.
>
>

Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.

## <a name="overview"></a>Visão geral
Serviços de mídia do Microsoft Azure está introduzindo Olá **o fluxo de trabalho do Media Encoder Premium** processador de mídia. Esse processador oferece recursos avançados de codificação para seus fluxos de trabalho premium sob demanda.

Olá, tópicos a seguir descrevem os detalhes relacionados muito**o fluxo de trabalho do Media Encoder Premium**:

* [Formatos suportados por Olá o fluxo de trabalho do Media Encoder Premium](media-services-premium-workflow-encoder-formats.md) – discute os codecs com suporte e formatos de arquivo hello **o fluxo de trabalho do Media Encoder Premium**.
* [Visão geral e a comparação do Azure em codificadores de mídia de demanda](media-services-encode-asset.md) compara Olá recursos de codificação de **o fluxo de trabalho do Media Encoder Premium** e **codificador de mídia padrão**.

Este tópico demonstra como tooencode com **o fluxo de trabalho do Media Encoder Premium** usando .NET.

Codificação de tarefas para Olá **o fluxo de trabalho do Media Encoder Premium** requerem um arquivo de configuração separado, chamado de arquivo de fluxo de trabalho. Esses arquivos têm uma extensão de .workflow e são criados usando Olá [Designer de fluxo de trabalho](media-services-workflow-designer.md) ferramenta.

Você também pode obter padrão Olá arquivos de fluxo de trabalho [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). pasta Olá também contém a descrição de saudação desses arquivos.

arquivos de fluxo de trabalho Olá necessário conta de serviços de mídia tooyour toobe carregado como um ativo, e este ativo deve ser passado toohello tarefas de codificação.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto do Visual Studio

Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 

## <a name="encoding-example"></a>Exemplo de codificação

Olá exemplo a seguir demonstra como tooencode com **o fluxo de trabalho do Media Encoder Premium**.

Olá, as etapas a seguir é executada:

1. Criar um ativo e carregar um arquivo de fluxo de trabalho.
2. Criar um ativo e carregar um arquivo de mídia de origem.
3. Obtenha o processador de mídia hello "Media Encoder Premium fluxo de trabalho".
4. Criar um trabalho e uma tarefa.

    Na maioria dos casos, cadeia de caracteres de configuração de saudação para tarefa hello está vazia (como no exemplo a seguir de saudação). Existem alguns cenários avançados (que exigem que você tootooset propriedades de tempo de execução dinamicamente) caso em que você forneça uma tarefa de codificação de toohello de cadeia de caracteres XML. Exemplos desses cenários são: criação de uma sobreposição, união de mídia paralela ou sequencial, colocação de legenda.
5. Adicione duas tarefas toohello de ativos de entrada.

    1. 1º – ativos de fluxo de trabalho de saudação.
    2. 2º – ativo de vídeo hello.

    >[!NOTE]
    >ativos de fluxo de trabalho Olá devem ser adicionado toohello tarefa antes de ativos de mídia hello.
   cadeia de caracteres de configuração de saudação para essa tarefa deve ficar vazia.
   
6. Envie trabalho de codificação de saudação.

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
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

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
                }

                static private void StateChanged(object sender, JobStateChangedEventArgs e)
                {
                    Console.WriteLine("Job state changed event:");
                    Console.WriteLine("  Previous state: " + e.PreviousState);
                    Console.WriteLine("  Current state: " + e.CurrentState);

                    switch (e.CurrentState)
                    {
                        case JobState.Finished:
                            Console.WriteLine();
                            Console.WriteLine("Job is finished.");
                            Console.WriteLine();
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
                            // LogJobStop(job.Id);
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

Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
