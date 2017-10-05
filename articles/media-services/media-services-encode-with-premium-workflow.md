---
title: "Codificação avançada com o Fluxo de Trabalho do Media Encoder Premium | Microsoft Docs"
description: "Saiba como codificar com fluxo de trabalho do Media Encoder Premium. Os exemplos de código são escritos em C# e usam a SDK dos Serviços de Mídia para .NET."
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
ms.openlocfilehash: 2b03853bf07e05c07fd730d5e8a8563963887921
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="8d868-104">Codificação avançada com fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="8d868-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="8d868-105">O processador de mídia do Fluxo de Trabalho do Media Encoder Premium analisado neste tópico não está disponível na China.</span><span class="sxs-lookup"><span data-stu-id="8d868-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="8d868-106">Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="8d868-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="8d868-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8d868-107">Overview</span></span>
<span data-ttu-id="8d868-108">Os Serviços de Mídia do Microsoft Azure estão apresentando o processador de mídia do **Fluxo de trabalho do Codificador de Mídia Premium** .</span><span class="sxs-lookup"><span data-stu-id="8d868-108">Microsoft Azure Media Services is introducing the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="8d868-109">Esse processador oferece recursos avançados de codificação para seus fluxos de trabalho premium sob demanda.</span><span class="sxs-lookup"><span data-stu-id="8d868-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="8d868-110">Os tópicos a seguir descrevem os detalhes relacionados ao **Fluxo de Trabalho do Media Encoder Premium**:</span><span class="sxs-lookup"><span data-stu-id="8d868-110">The following topics outline details related to **Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="8d868-111">[Formatos suportados pelo Fluxo de trabalho do Media Encoder Premium](media-services-premium-workflow-encoder-formats.md) – Discute os formatos de arquivo e codecs com suporte do **Fluxo de trabalho do Media Encoder Premium**.</span><span class="sxs-lookup"><span data-stu-id="8d868-111">[Formats Supported by the Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses the file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="8d868-112">[Visão geral e comparação dos codificadores de mídia sob demanda do Azure](media-services-encode-asset.md) compara os recursos de codificação do **Fluxo de Trabalho do Media Encoder Premium** e do **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="8d868-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares the encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="8d868-113">Este tópico demonstra como codificar com o **Fluxo de Trabalho do Media Encoder Premium** usando o .NET.</span><span class="sxs-lookup"><span data-stu-id="8d868-113">This topic demonstrates how to encode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="8d868-114">As tarefas de codificação para o **Fluxo de trabalho do Media Encoder Premium** exigem um arquivo de configuração separado, chamado de arquivo de Fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d868-114">Encoding tasks for the **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="8d868-115">Esses arquivos têm uma extensão .workflow e são criados usando a ferramenta [Designer de Fluxo de Trabalho](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="8d868-115">These files have a .workflow extension and are created using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="8d868-116">Você também pode obter os arquivos de fluxo de trabalho padrão [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="8d868-116">You can also get the default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="8d868-117">A pasta também contém a descrição desses arquivos.</span><span class="sxs-lookup"><span data-stu-id="8d868-117">The folder also contains the description of these files.</span></span>

<span data-ttu-id="8d868-118">Os arquivos de fluxo de trabalho devem ser carregados para sua conta de serviços de mídia como um ativo e esse ativo deve ser passado para a tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="8d868-118">The workflow files need to be uploaded to your Media Services account as an Asset, and this Asset should be passed in to the encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8d868-119">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d868-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="8d868-120">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8d868-120">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="8d868-121">Exemplo de codificação</span><span class="sxs-lookup"><span data-stu-id="8d868-121">Encoding example</span></span>

<span data-ttu-id="8d868-122">O exemplo a seguir demonstra como codificar com o **Fluxo de trabalho do Media Encoder Premium**.</span><span class="sxs-lookup"><span data-stu-id="8d868-122">The following example demonstrates how to encode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="8d868-123">As seguintes etapas são executadas:</span><span class="sxs-lookup"><span data-stu-id="8d868-123">The following steps are performed:</span></span>

1. <span data-ttu-id="8d868-124">Criar um ativo e carregar um arquivo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d868-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="8d868-125">Criar um ativo e carregar um arquivo de mídia de origem.</span><span class="sxs-lookup"><span data-stu-id="8d868-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="8d868-126">Obtenha o processador de mídia "Fluxo de trabalho do Media Encoder Premium".</span><span class="sxs-lookup"><span data-stu-id="8d868-126">Get the "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="8d868-127">Criar um trabalho e uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="8d868-127">Create a job and a task.</span></span>

    <span data-ttu-id="8d868-128">Na maioria dos casos, a cadeia de caracteres de configuração para a tarefa está vazia (como no exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="8d868-128">In most cases, the configuration string for the task is empty (like in the following example).</span></span> <span data-ttu-id="8d868-129">Há alguns cenários avançados (que exigem que você defina propriedades de tempo de execução dinamicamente) em que você forneceria uma cadeia de caracteres XML para a tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="8d868-129">There are some advanced scenarios (that require you to to set runtime properties dynamically) in which case you would provide an XML string to the encoding task.</span></span> <span data-ttu-id="8d868-130">Exemplos desses cenários são: criação de uma sobreposição, união de mídia paralela ou sequencial, colocação de legenda.</span><span class="sxs-lookup"><span data-stu-id="8d868-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="8d868-131">Adicionar dois ativos de entrada à tarefa.</span><span class="sxs-lookup"><span data-stu-id="8d868-131">Add two input assets to the task.</span></span>

    1. <span data-ttu-id="8d868-132">1º – o ativo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d868-132">1st – the workflow asset.</span></span>
    2. <span data-ttu-id="8d868-133">2º – o ativo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="8d868-133">2nd – the video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8d868-134">O ativo de fluxo de trabalho deve ser adicionado à tarefa antes do ativo de mídia.</span><span class="sxs-lookup"><span data-stu-id="8d868-134">The workflow asset must be added to the task before the media asset.</span></span>
   <span data-ttu-id="8d868-135">A cadeia de caracteres de configuração para essa tarefa deve estar vazia.</span><span class="sxs-lookup"><span data-stu-id="8d868-135">The configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="8d868-136">Envie o trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="8d868-136">Submit the encoding job.</span></span>

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
                    // Get a media processor reference, and pass to it the name of the
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with the encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset to contain the results of the job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means the output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use the following event handler to check job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch the job.
                    job.Submit();

                    // Check job execution and wait for job to finish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error the event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due to job error.");
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

<span data-ttu-id="8d868-137">Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="8d868-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8d868-138">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="8d868-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8d868-139">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="8d868-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
