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
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="2cf26-105">Usar o Azure Media Encoder padrão tooauto-gerar uma escada de taxa de bits</span><span class="sxs-lookup"><span data-stu-id="2cf26-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="2cf26-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2cf26-106">Overview</span></span>

<span data-ttu-id="2cf26-107">Este tópico mostra como toouse codificador de mídia padrão (MES) tooauto-gerar uma escada de taxa de bits (pares de resolução de taxa de bits) com base na resolução de entrada hello e taxa de bits.</span><span class="sxs-lookup"><span data-stu-id="2cf26-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="2cf26-108">Olá gerado automaticamente predefinição nunca excederá taxas de bits e a resolução de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="2cf26-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="2cf26-109">Por exemplo, se for de entrada hello 720p em 3 Mbps, a saída será permanecem 720p na melhor das hipóteses e iniciará a taxas inferior a 3 Mbps.</span><span class="sxs-lookup"><span data-stu-id="2cf26-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="2cf26-110">Codificar para Streaming Somente</span><span class="sxs-lookup"><span data-stu-id="2cf26-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="2cf26-111">Se sua intenção for tooencode sua fonte de vídeo somente para streaming, em seguida, é recomendável usar hello "Streaming adaptável" predefinição ao criar uma tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="2cf26-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="2cf26-112">Ao usar o hello **Streaming adaptável** predefinidos, codificador MES Olá inteligente limitar Escada uma taxa de bits.</span><span class="sxs-lookup"><span data-stu-id="2cf26-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="2cf26-113">No entanto, não será capaz de toocontrol Olá codificação custos, desde que o serviço de saudação determina quantos toouse de camadas e em qual resolução.</span><span class="sxs-lookup"><span data-stu-id="2cf26-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="2cf26-114">Você pode ver exemplos de camadas de saída produzidos pelo MES como resultado de codificação com hello **Streaming adaptável** predefinição final Olá deste tópico.</span><span class="sxs-lookup"><span data-stu-id="2cf26-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="2cf26-115">saudação de saída ativo conterá arquivos MP4 onde áudio e vídeo não são intercalados.</span><span class="sxs-lookup"><span data-stu-id="2cf26-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="2cf26-116">Codificação para download progressivo e streaming</span><span class="sxs-lookup"><span data-stu-id="2cf26-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="2cf26-117">Se sua intenção for tooencode o vídeo de origem de streaming, bem como arquivos MP4 com tooproduce para download progressivo, em seguida, é recomendável usar hello "Conteúdo adaptável várias taxas de bits MP4" predefinição ao criar uma tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="2cf26-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="2cf26-118">Ao usar o hello **conteúdo adaptável MP4 de taxas de bits múltiplas** predefinidos, codificador MES Olá aplicará Olá mesma lógica de codificação, como acima, mas agora Olá ativo de saída conterá MP4 arquivos onde áudio e vídeo são intercalados.</span><span class="sxs-lookup"><span data-stu-id="2cf26-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="2cf26-119">Você pode usar um desses arquivos MP4 (por exemplo, Olá versão mais alta taxa de bits) como um arquivo de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="2cf26-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="2cf26-120"><a id="encoding_with_dotnet"></a>Codificação com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="2cf26-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="2cf26-121">saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2cf26-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="2cf26-122">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="2cf26-122">Create an encoding job.</span></span>
- <span data-ttu-id="2cf26-123">Obtém um codificador de mídia codificador padrão de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="2cf26-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="2cf26-124">Adicionar um trabalho toohello codificação e especificar Olá toouse **Streaming adaptável** predefinido.</span><span class="sxs-lookup"><span data-stu-id="2cf26-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="2cf26-125">Crie um ativo de saída que conterá o ativo de saudação codificado.</span><span class="sxs-lookup"><span data-stu-id="2cf26-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="2cf26-126">Adicione o andamento do trabalho um evento manipulador toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="2cf26-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="2cf26-127">Envie trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2cf26-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2cf26-128">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2cf26-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2cf26-129">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2cf26-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="2cf26-130">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2cf26-130">Example</span></span>

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

## <span data-ttu-id="2cf26-131"><a id="output"></a>Saída</span><span class="sxs-lookup"><span data-stu-id="2cf26-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="2cf26-132">Esta seção mostra três exemplos de camadas de saída produzidos pelo MES como resultado de codificação com hello **Streaming adaptável** predefinido.</span><span class="sxs-lookup"><span data-stu-id="2cf26-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="2cf26-133">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="2cf26-133">Example 1</span></span>
<span data-ttu-id="2cf26-134">Fonte com altura "1080" e taxa de quadros "29.970" produz seis camadas de vídeo:</span><span class="sxs-lookup"><span data-stu-id="2cf26-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="2cf26-135">Camada</span><span class="sxs-lookup"><span data-stu-id="2cf26-135">Layer</span></span>|<span data-ttu-id="2cf26-136">Altura</span><span class="sxs-lookup"><span data-stu-id="2cf26-136">Height</span></span>|<span data-ttu-id="2cf26-137">Largura</span><span class="sxs-lookup"><span data-stu-id="2cf26-137">Width</span></span>|<span data-ttu-id="2cf26-138">Taxa de bits (Kbps)</span><span class="sxs-lookup"><span data-stu-id="2cf26-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="2cf26-139">1</span><span class="sxs-lookup"><span data-stu-id="2cf26-139">1</span></span>|<span data-ttu-id="2cf26-140">1080</span><span class="sxs-lookup"><span data-stu-id="2cf26-140">1080</span></span>|<span data-ttu-id="2cf26-141">1920</span><span class="sxs-lookup"><span data-stu-id="2cf26-141">1920</span></span>|<span data-ttu-id="2cf26-142">6780</span><span class="sxs-lookup"><span data-stu-id="2cf26-142">6780</span></span>|
|<span data-ttu-id="2cf26-143">2</span><span class="sxs-lookup"><span data-stu-id="2cf26-143">2</span></span>|<span data-ttu-id="2cf26-144">720</span><span class="sxs-lookup"><span data-stu-id="2cf26-144">720</span></span>|<span data-ttu-id="2cf26-145">1280</span><span class="sxs-lookup"><span data-stu-id="2cf26-145">1280</span></span>|<span data-ttu-id="2cf26-146">3520</span><span class="sxs-lookup"><span data-stu-id="2cf26-146">3520</span></span>|
|<span data-ttu-id="2cf26-147">3</span><span class="sxs-lookup"><span data-stu-id="2cf26-147">3</span></span>|<span data-ttu-id="2cf26-148">540</span><span class="sxs-lookup"><span data-stu-id="2cf26-148">540</span></span>|<span data-ttu-id="2cf26-149">960</span><span class="sxs-lookup"><span data-stu-id="2cf26-149">960</span></span>|<span data-ttu-id="2cf26-150">2210</span><span class="sxs-lookup"><span data-stu-id="2cf26-150">2210</span></span>|
|<span data-ttu-id="2cf26-151">4</span><span class="sxs-lookup"><span data-stu-id="2cf26-151">4</span></span>|<span data-ttu-id="2cf26-152">360</span><span class="sxs-lookup"><span data-stu-id="2cf26-152">360</span></span>|<span data-ttu-id="2cf26-153">640</span><span class="sxs-lookup"><span data-stu-id="2cf26-153">640</span></span>|<span data-ttu-id="2cf26-154">1150</span><span class="sxs-lookup"><span data-stu-id="2cf26-154">1150</span></span>|
|<span data-ttu-id="2cf26-155">5</span><span class="sxs-lookup"><span data-stu-id="2cf26-155">5</span></span>|<span data-ttu-id="2cf26-156">270</span><span class="sxs-lookup"><span data-stu-id="2cf26-156">270</span></span>|<span data-ttu-id="2cf26-157">480</span><span class="sxs-lookup"><span data-stu-id="2cf26-157">480</span></span>|<span data-ttu-id="2cf26-158">720</span><span class="sxs-lookup"><span data-stu-id="2cf26-158">720</span></span>|
|<span data-ttu-id="2cf26-159">6</span><span class="sxs-lookup"><span data-stu-id="2cf26-159">6</span></span>|<span data-ttu-id="2cf26-160">180</span><span class="sxs-lookup"><span data-stu-id="2cf26-160">180</span></span>|<span data-ttu-id="2cf26-161">320</span><span class="sxs-lookup"><span data-stu-id="2cf26-161">320</span></span>|<span data-ttu-id="2cf26-162">380</span><span class="sxs-lookup"><span data-stu-id="2cf26-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="2cf26-163">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="2cf26-163">Example 2</span></span>
<span data-ttu-id="2cf26-164">Fonte com altura "720" e taxa de quadros "23.970" produz cinco camadas de vídeo:</span><span class="sxs-lookup"><span data-stu-id="2cf26-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="2cf26-165">Camada</span><span class="sxs-lookup"><span data-stu-id="2cf26-165">Layer</span></span>|<span data-ttu-id="2cf26-166">Altura</span><span class="sxs-lookup"><span data-stu-id="2cf26-166">Height</span></span>|<span data-ttu-id="2cf26-167">Largura</span><span class="sxs-lookup"><span data-stu-id="2cf26-167">Width</span></span>|<span data-ttu-id="2cf26-168">Taxa de bits (Kbps)</span><span class="sxs-lookup"><span data-stu-id="2cf26-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="2cf26-169">1</span><span class="sxs-lookup"><span data-stu-id="2cf26-169">1</span></span>|<span data-ttu-id="2cf26-170">720</span><span class="sxs-lookup"><span data-stu-id="2cf26-170">720</span></span>|<span data-ttu-id="2cf26-171">1280</span><span class="sxs-lookup"><span data-stu-id="2cf26-171">1280</span></span>|<span data-ttu-id="2cf26-172">2940</span><span class="sxs-lookup"><span data-stu-id="2cf26-172">2940</span></span>|
|<span data-ttu-id="2cf26-173">2</span><span class="sxs-lookup"><span data-stu-id="2cf26-173">2</span></span>|<span data-ttu-id="2cf26-174">540</span><span class="sxs-lookup"><span data-stu-id="2cf26-174">540</span></span>|<span data-ttu-id="2cf26-175">960</span><span class="sxs-lookup"><span data-stu-id="2cf26-175">960</span></span>|<span data-ttu-id="2cf26-176">1850</span><span class="sxs-lookup"><span data-stu-id="2cf26-176">1850</span></span>|
|<span data-ttu-id="2cf26-177">3</span><span class="sxs-lookup"><span data-stu-id="2cf26-177">3</span></span>|<span data-ttu-id="2cf26-178">360</span><span class="sxs-lookup"><span data-stu-id="2cf26-178">360</span></span>|<span data-ttu-id="2cf26-179">640</span><span class="sxs-lookup"><span data-stu-id="2cf26-179">640</span></span>|<span data-ttu-id="2cf26-180">960</span><span class="sxs-lookup"><span data-stu-id="2cf26-180">960</span></span>|
|<span data-ttu-id="2cf26-181">4</span><span class="sxs-lookup"><span data-stu-id="2cf26-181">4</span></span>|<span data-ttu-id="2cf26-182">270</span><span class="sxs-lookup"><span data-stu-id="2cf26-182">270</span></span>|<span data-ttu-id="2cf26-183">480</span><span class="sxs-lookup"><span data-stu-id="2cf26-183">480</span></span>|<span data-ttu-id="2cf26-184">600</span><span class="sxs-lookup"><span data-stu-id="2cf26-184">600</span></span>|
|<span data-ttu-id="2cf26-185">5</span><span class="sxs-lookup"><span data-stu-id="2cf26-185">5</span></span>|<span data-ttu-id="2cf26-186">180</span><span class="sxs-lookup"><span data-stu-id="2cf26-186">180</span></span>|<span data-ttu-id="2cf26-187">320</span><span class="sxs-lookup"><span data-stu-id="2cf26-187">320</span></span>|<span data-ttu-id="2cf26-188">320</span><span class="sxs-lookup"><span data-stu-id="2cf26-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="2cf26-189">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="2cf26-189">Example 3</span></span>
<span data-ttu-id="2cf26-190">Fonte com altura "360" e taxa de quadros "29.970" produz três camadas de vídeo:</span><span class="sxs-lookup"><span data-stu-id="2cf26-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="2cf26-191">Camada</span><span class="sxs-lookup"><span data-stu-id="2cf26-191">Layer</span></span>|<span data-ttu-id="2cf26-192">Altura</span><span class="sxs-lookup"><span data-stu-id="2cf26-192">Height</span></span>|<span data-ttu-id="2cf26-193">Largura</span><span class="sxs-lookup"><span data-stu-id="2cf26-193">Width</span></span>|<span data-ttu-id="2cf26-194">Taxa de bits (Kbps)</span><span class="sxs-lookup"><span data-stu-id="2cf26-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="2cf26-195">1</span><span class="sxs-lookup"><span data-stu-id="2cf26-195">1</span></span>|<span data-ttu-id="2cf26-196">360</span><span class="sxs-lookup"><span data-stu-id="2cf26-196">360</span></span>|<span data-ttu-id="2cf26-197">640</span><span class="sxs-lookup"><span data-stu-id="2cf26-197">640</span></span>|<span data-ttu-id="2cf26-198">700</span><span class="sxs-lookup"><span data-stu-id="2cf26-198">700</span></span>|
|<span data-ttu-id="2cf26-199">2</span><span class="sxs-lookup"><span data-stu-id="2cf26-199">2</span></span>|<span data-ttu-id="2cf26-200">270</span><span class="sxs-lookup"><span data-stu-id="2cf26-200">270</span></span>|<span data-ttu-id="2cf26-201">480</span><span class="sxs-lookup"><span data-stu-id="2cf26-201">480</span></span>|<span data-ttu-id="2cf26-202">440</span><span class="sxs-lookup"><span data-stu-id="2cf26-202">440</span></span>|
|<span data-ttu-id="2cf26-203">3</span><span class="sxs-lookup"><span data-stu-id="2cf26-203">3</span></span>|<span data-ttu-id="2cf26-204">180</span><span class="sxs-lookup"><span data-stu-id="2cf26-204">180</span></span>|<span data-ttu-id="2cf26-205">320</span><span class="sxs-lookup"><span data-stu-id="2cf26-205">320</span></span>|<span data-ttu-id="2cf26-206">230</span><span class="sxs-lookup"><span data-stu-id="2cf26-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="2cf26-207">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="2cf26-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2cf26-208">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="2cf26-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2cf26-209">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2cf26-209">See Also</span></span>
[<span data-ttu-id="2cf26-210">Visão geral da codificação de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="2cf26-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

