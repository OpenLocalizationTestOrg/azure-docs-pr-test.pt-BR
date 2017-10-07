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
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a><span data-ttu-id="79a81-104">Codificação avançada com fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="79a81-104">Advanced encoding with Media Encoder Premium Workflow</span></span>
> [!NOTE]
> <span data-ttu-id="79a81-105">O processador de mídia do Fluxo de Trabalho do Media Encoder Premium analisado neste tópico não está disponível na China.</span><span class="sxs-lookup"><span data-stu-id="79a81-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span>
>
>

<span data-ttu-id="79a81-106">Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="79a81-106">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="overview"></a><span data-ttu-id="79a81-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="79a81-107">Overview</span></span>
<span data-ttu-id="79a81-108">Serviços de mídia do Microsoft Azure está introduzindo Olá **o fluxo de trabalho do Media Encoder Premium** processador de mídia.</span><span class="sxs-lookup"><span data-stu-id="79a81-108">Microsoft Azure Media Services is introducing hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="79a81-109">Esse processador oferece recursos avançados de codificação para seus fluxos de trabalho premium sob demanda.</span><span class="sxs-lookup"><span data-stu-id="79a81-109">This processor offers advance encoding capabilities for your premium on-demand workflows.</span></span>

<span data-ttu-id="79a81-110">Olá, tópicos a seguir descrevem os detalhes relacionados muito**o fluxo de trabalho do Media Encoder Premium**:</span><span class="sxs-lookup"><span data-stu-id="79a81-110">hello following topics outline details related too**Media Encoder Premium Workflow**:</span></span>

* <span data-ttu-id="79a81-111">[Formatos suportados por Olá o fluxo de trabalho do Media Encoder Premium](media-services-premium-workflow-encoder-formats.md) – discute os codecs com suporte e formatos de arquivo hello **o fluxo de trabalho do Media Encoder Premium**.</span><span class="sxs-lookup"><span data-stu-id="79a81-111">[Formats Supported by hello Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md) – Discusses hello file formats and codecs supported by **Media Encoder Premium Workflow**.</span></span>
* <span data-ttu-id="79a81-112">[Visão geral e a comparação do Azure em codificadores de mídia de demanda](media-services-encode-asset.md) compara Olá recursos de codificação de **o fluxo de trabalho do Media Encoder Premium** e **codificador de mídia padrão**.</span><span class="sxs-lookup"><span data-stu-id="79a81-112">[Overview and comparison of Azure on demand media encoders](media-services-encode-asset.md) compares hello encoding capabilities of **Media Encoder Premium Workflow** and **Media Encoder Standard**.</span></span>

<span data-ttu-id="79a81-113">Este tópico demonstra como tooencode com **o fluxo de trabalho do Media Encoder Premium** usando .NET.</span><span class="sxs-lookup"><span data-stu-id="79a81-113">This topic demonstrates how tooencode with **Media Encoder Premium Workflow** using .NET.</span></span>

<span data-ttu-id="79a81-114">Codificação de tarefas para Olá **o fluxo de trabalho do Media Encoder Premium** requerem um arquivo de configuração separado, chamado de arquivo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="79a81-114">Encoding tasks for hello **Media Encoder Premium Workflow** require a separate configuration file, called a Workflow file.</span></span> <span data-ttu-id="79a81-115">Esses arquivos têm uma extensão de .workflow e são criados usando Olá [Designer de fluxo de trabalho](media-services-workflow-designer.md) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="79a81-115">These files have a .workflow extension and are created using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

<span data-ttu-id="79a81-116">Você também pode obter padrão Olá arquivos de fluxo de trabalho [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span><span class="sxs-lookup"><span data-stu-id="79a81-116">You can also get hello default workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows).</span></span> <span data-ttu-id="79a81-117">pasta Olá também contém a descrição de saudação desses arquivos.</span><span class="sxs-lookup"><span data-stu-id="79a81-117">hello folder also contains hello description of these files.</span></span>

<span data-ttu-id="79a81-118">arquivos de fluxo de trabalho Olá necessário conta de serviços de mídia tooyour toobe carregado como um ativo, e este ativo deve ser passado toohello tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="79a81-118">hello workflow files need toobe uploaded tooyour Media Services account as an Asset, and this Asset should be passed in toohello encoding Task.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="79a81-119">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79a81-119">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="79a81-120">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="79a81-120">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="encoding-example"></a><span data-ttu-id="79a81-121">Exemplo de codificação</span><span class="sxs-lookup"><span data-stu-id="79a81-121">Encoding example</span></span>

<span data-ttu-id="79a81-122">Olá exemplo a seguir demonstra como tooencode com **o fluxo de trabalho do Media Encoder Premium**.</span><span class="sxs-lookup"><span data-stu-id="79a81-122">hello following example demonstrates how tooencode with **Media Encoder Premium Workflow**.</span></span>

<span data-ttu-id="79a81-123">Olá, as etapas a seguir é executada:</span><span class="sxs-lookup"><span data-stu-id="79a81-123">hello following steps are performed:</span></span>

1. <span data-ttu-id="79a81-124">Criar um ativo e carregar um arquivo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="79a81-124">Create an asset and upload a workflow file.</span></span>
2. <span data-ttu-id="79a81-125">Criar um ativo e carregar um arquivo de mídia de origem.</span><span class="sxs-lookup"><span data-stu-id="79a81-125">Create an asset and upload a source media file.</span></span>
3. <span data-ttu-id="79a81-126">Obtenha o processador de mídia hello "Media Encoder Premium fluxo de trabalho".</span><span class="sxs-lookup"><span data-stu-id="79a81-126">Get hello "Media Encoder Premium Workflow" media processor.</span></span>
4. <span data-ttu-id="79a81-127">Criar um trabalho e uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="79a81-127">Create a job and a task.</span></span>

    <span data-ttu-id="79a81-128">Na maioria dos casos, cadeia de caracteres de configuração de saudação para tarefa hello está vazia (como no exemplo a seguir de saudação).</span><span class="sxs-lookup"><span data-stu-id="79a81-128">In most cases, hello configuration string for hello task is empty (like in hello following example).</span></span> <span data-ttu-id="79a81-129">Existem alguns cenários avançados (que exigem que você tootooset propriedades de tempo de execução dinamicamente) caso em que você forneça uma tarefa de codificação de toohello de cadeia de caracteres XML.</span><span class="sxs-lookup"><span data-stu-id="79a81-129">There are some advanced scenarios (that require you tootooset runtime properties dynamically) in which case you would provide an XML string toohello encoding task.</span></span> <span data-ttu-id="79a81-130">Exemplos desses cenários são: criação de uma sobreposição, união de mídia paralela ou sequencial, colocação de legenda.</span><span class="sxs-lookup"><span data-stu-id="79a81-130">Examples of such scenarios are: creating an overlay, parallel or sequential media stitching, subtitling.</span></span>
5. <span data-ttu-id="79a81-131">Adicione duas tarefas toohello de ativos de entrada.</span><span class="sxs-lookup"><span data-stu-id="79a81-131">Add two input assets toohello task.</span></span>

    1. <span data-ttu-id="79a81-132">1º – ativos de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="79a81-132">1st – hello workflow asset.</span></span>
    2. <span data-ttu-id="79a81-133">2º – ativo de vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="79a81-133">2nd – hello video asset.</span></span>

    >[!NOTE]
    ><span data-ttu-id="79a81-134">ativos de fluxo de trabalho Olá devem ser adicionado toohello tarefa antes de ativos de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="79a81-134">hello workflow asset must be added toohello task before hello media asset.</span></span>
   <span data-ttu-id="79a81-135">cadeia de caracteres de configuração de saudação para essa tarefa deve ficar vazia.</span><span class="sxs-lookup"><span data-stu-id="79a81-135">hello configuration string for this task should be empty.</span></span>
   
6. <span data-ttu-id="79a81-136">Envie trabalho de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="79a81-136">Submit hello encoding job.</span></span>

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

<span data-ttu-id="79a81-137">Para solucionar dúvidas sobre o codificador premium, envie um email para o mepd em Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="79a81-137">For premium encoder questions, email mepd at Microsoft.com.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="79a81-138">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="79a81-138">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="79a81-139">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="79a81-139">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
