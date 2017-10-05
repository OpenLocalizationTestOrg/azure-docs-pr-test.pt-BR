---
title: "Usar o Codificador de Mídia do Azure Standard para gerar automaticamente uma escada de taxa de bits | Microsoft Docs"
description: "Este tópico mostra como usar o Media Encoder Standard (MES) para gerar automaticamente uma escada de taxa de bits com base na resolução de entrada e na taxa de bits. A resolução de entrada e a taxa de bits nunca serão excedidas. Por exemplo, se a entrada for 720p em 3Mbps, a saída continuará 720p na melhor das hipóteses e iniciará com taxas menores que 3Mbps."
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
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="e2e8e-105">Usar o Codificador de Mídia do Azure Standard para gerar automaticamente uma escada de taxa de bits</span><span class="sxs-lookup"><span data-stu-id="e2e8e-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="e2e8e-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e2e8e-106">Overview</span></span>

<span data-ttu-id="e2e8e-107">Este tópico mostra como usar o Media Encoder Standard (MES) para gerar automaticamente uma escada de taxa de bits (pares de resolução de taxa de bits) com base na resolução de entrada e na taxa de bits.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="e2e8e-108">A predefinição gerada automaticamente nunca excederá a resolução de entrada e a taxa de bits.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="e2e8e-109">Por exemplo, se a entrada for 720p em 3Mbps, a saída continuará 720p na melhor das hipóteses e iniciará com taxas menores que 3Mbps.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="e2e8e-110">Codificar para Streaming Somente</span><span class="sxs-lookup"><span data-stu-id="e2e8e-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="e2e8e-111">Se sua intenção for codificar o vídeo de origem somente para streaming, é recomendável usar a predefinição "Streaming adaptável" ao criar uma tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-111">If your intent is to encode your source video only for streaming, then you shoud use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="e2e8e-112">Ao usar a predefinição do **Streaming Adaptável**, o codificador MES protegerá, de forma inteligente, uma escada de taxa de bits.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="e2e8e-113">No entanto, não será possível controlar os custos de codificação, já que o serviço determina quantas camadas usar e em qual resolução.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="e2e8e-114">Você pode ver exemplos das camadas de saída produzidas por MES como resultado de codificação com a predefinição do **Streaming Adaptável** no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this topic.</span></span> <span data-ttu-id="e2e8e-115">O Ativo de saída conterá arquivos MP4 onde áudio e vídeo não são intercalados.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-115">The output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="e2e8e-116">Codificação para download progressivo e streaming</span><span class="sxs-lookup"><span data-stu-id="e2e8e-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="e2e8e-117">Se sua intenção for codificar o vídeo de origem de streaming, bem como para produzir arquivos MP4 para download progressivo, é recomendável usar a predefinição "conteúdo adaptável várias taxas de bits MP4" ao criar uma tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you shoud use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="e2e8e-118">Ao usar a predefinição **MP4 de Taxa de Bits Múltiplas Adaptável a Conteúdo**, o codificador MES aplicará a mesma lógica de codificação como acima, mas agora, o ativo de saída conterá arquivos MP4 onde áudio e vídeo são intercalados.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder will apply the same encoding logic as above, but now the output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="e2e8e-119">Você pode usar um desses arquivos MP4 (por exemplo, a versão de taxa de bits mais alta) como um arquivo de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="e2e8e-120"><a id="encoding_with_dotnet"></a>Codificação com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="e2e8e-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="e2e8e-121">O exemplo de código a seguir usa o SDK .NET dos Serviços de Mídia para executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="e2e8e-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="e2e8e-122">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-122">Create an encoding job.</span></span>
- <span data-ttu-id="e2e8e-123">Obtenha uma referência para o Codificador de Mídia Padrão.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="e2e8e-124">Adicione uma tarefa de codificação ao trabalho e especifique para usar a predefinição do **Streaming Adaptável**.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="e2e8e-125">Crie um ativo de saída que conterá o ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-125">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="e2e8e-126">Adicione um manipulador de eventos para verificar o progresso do trabalho.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="e2e8e-127">Enviar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e2e8e-128">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2e8e-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e2e8e-129">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e2e8e-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e2e8e-130">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e2e8e-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
    {
        class Program
        {
        // Read values from the App.config file.
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

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

## <span data-ttu-id="e2e8e-131"><a id="output"></a>Saída</span><span class="sxs-lookup"><span data-stu-id="e2e8e-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="e2e8e-132">Esta seção exibe três exemplos de camadas de saída produzidas por MES como resultado de codificação com a predefinição do **Streaming Adaptável**.</span><span class="sxs-lookup"><span data-stu-id="e2e8e-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="e2e8e-133">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="e2e8e-133">Example 1</span></span>
<span data-ttu-id="e2e8e-134">Fonte com altura "1080" e taxa de quadros "29.970" produz seis camadas de vídeo:</span><span class="sxs-lookup"><span data-stu-id="e2e8e-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="e2e8e-135">Camada</span><span class="sxs-lookup"><span data-stu-id="e2e8e-135">Layer</span></span>|<span data-ttu-id="e2e8e-136">Altura</span><span class="sxs-lookup"><span data-stu-id="e2e8e-136">Height</span></span>|<span data-ttu-id="e2e8e-137">Largura</span><span class="sxs-lookup"><span data-stu-id="e2e8e-137">Width</span></span>|<span data-ttu-id="e2e8e-138">Taxa de bits (Kbps)</span><span class="sxs-lookup"><span data-stu-id="e2e8e-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="e2e8e-139">1</span><span class="sxs-lookup"><span data-stu-id="e2e8e-139">1</span></span>|<span data-ttu-id="e2e8e-140">1080</span><span class="sxs-lookup"><span data-stu-id="e2e8e-140">1080</span></span>|<span data-ttu-id="e2e8e-141">1920</span><span class="sxs-lookup"><span data-stu-id="e2e8e-141">1920</span></span>|<span data-ttu-id="e2e8e-142">6780</span><span class="sxs-lookup"><span data-stu-id="e2e8e-142">6780</span></span>|
|<span data-ttu-id="e2e8e-143">2</span><span class="sxs-lookup"><span data-stu-id="e2e8e-143">2</span></span>|<span data-ttu-id="e2e8e-144">720</span><span class="sxs-lookup"><span data-stu-id="e2e8e-144">720</span></span>|<span data-ttu-id="e2e8e-145">1280</span><span class="sxs-lookup"><span data-stu-id="e2e8e-145">1280</span></span>|<span data-ttu-id="e2e8e-146">3520</span><span class="sxs-lookup"><span data-stu-id="e2e8e-146">3520</span></span>|
|<span data-ttu-id="e2e8e-147">3</span><span class="sxs-lookup"><span data-stu-id="e2e8e-147">3</span></span>|<span data-ttu-id="e2e8e-148">540</span><span class="sxs-lookup"><span data-stu-id="e2e8e-148">540</span></span>|<span data-ttu-id="e2e8e-149">960</span><span class="sxs-lookup"><span data-stu-id="e2e8e-149">960</span></span>|<span data-ttu-id="e2e8e-150">2210</span><span class="sxs-lookup"><span data-stu-id="e2e8e-150">2210</span></span>|
|<span data-ttu-id="e2e8e-151">4</span><span class="sxs-lookup"><span data-stu-id="e2e8e-151">4</span></span>|<span data-ttu-id="e2e8e-152">360</span><span class="sxs-lookup"><span data-stu-id="e2e8e-152">360</span></span>|<span data-ttu-id="e2e8e-153">640</span><span class="sxs-lookup"><span data-stu-id="e2e8e-153">640</span></span>|<span data-ttu-id="e2e8e-154">1150</span><span class="sxs-lookup"><span data-stu-id="e2e8e-154">1150</span></span>|
|<span data-ttu-id="e2e8e-155">5</span><span class="sxs-lookup"><span data-stu-id="e2e8e-155">5</span></span>|<span data-ttu-id="e2e8e-156">270</span><span class="sxs-lookup"><span data-stu-id="e2e8e-156">270</span></span>|<span data-ttu-id="e2e8e-157">480</span><span class="sxs-lookup"><span data-stu-id="e2e8e-157">480</span></span>|<span data-ttu-id="e2e8e-158">720</span><span class="sxs-lookup"><span data-stu-id="e2e8e-158">720</span></span>|
|<span data-ttu-id="e2e8e-159">6</span><span class="sxs-lookup"><span data-stu-id="e2e8e-159">6</span></span>|<span data-ttu-id="e2e8e-160">180</span><span class="sxs-lookup"><span data-stu-id="e2e8e-160">180</span></span>|<span data-ttu-id="e2e8e-161">320</span><span class="sxs-lookup"><span data-stu-id="e2e8e-161">320</span></span>|<span data-ttu-id="e2e8e-162">380</span><span class="sxs-lookup"><span data-stu-id="e2e8e-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="e2e8e-163">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="e2e8e-163">Example 2</span></span>
<span data-ttu-id="e2e8e-164">Fonte com altura "720" e taxa de quadros "23.970" produz cinco camadas de vídeo:</span><span class="sxs-lookup"><span data-stu-id="e2e8e-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="e2e8e-165">Camada</span><span class="sxs-lookup"><span data-stu-id="e2e8e-165">Layer</span></span>|<span data-ttu-id="e2e8e-166">Altura</span><span class="sxs-lookup"><span data-stu-id="e2e8e-166">Height</span></span>|<span data-ttu-id="e2e8e-167">Largura</span><span class="sxs-lookup"><span data-stu-id="e2e8e-167">Width</span></span>|<span data-ttu-id="e2e8e-168">Taxa de bits (Kbps)</span><span class="sxs-lookup"><span data-stu-id="e2e8e-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="e2e8e-169">1</span><span class="sxs-lookup"><span data-stu-id="e2e8e-169">1</span></span>|<span data-ttu-id="e2e8e-170">720</span><span class="sxs-lookup"><span data-stu-id="e2e8e-170">720</span></span>|<span data-ttu-id="e2e8e-171">1280</span><span class="sxs-lookup"><span data-stu-id="e2e8e-171">1280</span></span>|<span data-ttu-id="e2e8e-172">2940</span><span class="sxs-lookup"><span data-stu-id="e2e8e-172">2940</span></span>|
|<span data-ttu-id="e2e8e-173">2</span><span class="sxs-lookup"><span data-stu-id="e2e8e-173">2</span></span>|<span data-ttu-id="e2e8e-174">540</span><span class="sxs-lookup"><span data-stu-id="e2e8e-174">540</span></span>|<span data-ttu-id="e2e8e-175">960</span><span class="sxs-lookup"><span data-stu-id="e2e8e-175">960</span></span>|<span data-ttu-id="e2e8e-176">1850</span><span class="sxs-lookup"><span data-stu-id="e2e8e-176">1850</span></span>|
|<span data-ttu-id="e2e8e-177">3</span><span class="sxs-lookup"><span data-stu-id="e2e8e-177">3</span></span>|<span data-ttu-id="e2e8e-178">360</span><span class="sxs-lookup"><span data-stu-id="e2e8e-178">360</span></span>|<span data-ttu-id="e2e8e-179">640</span><span class="sxs-lookup"><span data-stu-id="e2e8e-179">640</span></span>|<span data-ttu-id="e2e8e-180">960</span><span class="sxs-lookup"><span data-stu-id="e2e8e-180">960</span></span>|
|<span data-ttu-id="e2e8e-181">4</span><span class="sxs-lookup"><span data-stu-id="e2e8e-181">4</span></span>|<span data-ttu-id="e2e8e-182">270</span><span class="sxs-lookup"><span data-stu-id="e2e8e-182">270</span></span>|<span data-ttu-id="e2e8e-183">480</span><span class="sxs-lookup"><span data-stu-id="e2e8e-183">480</span></span>|<span data-ttu-id="e2e8e-184">600</span><span class="sxs-lookup"><span data-stu-id="e2e8e-184">600</span></span>|
|<span data-ttu-id="e2e8e-185">5</span><span class="sxs-lookup"><span data-stu-id="e2e8e-185">5</span></span>|<span data-ttu-id="e2e8e-186">180</span><span class="sxs-lookup"><span data-stu-id="e2e8e-186">180</span></span>|<span data-ttu-id="e2e8e-187">320</span><span class="sxs-lookup"><span data-stu-id="e2e8e-187">320</span></span>|<span data-ttu-id="e2e8e-188">320</span><span class="sxs-lookup"><span data-stu-id="e2e8e-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="e2e8e-189">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="e2e8e-189">Example 3</span></span>
<span data-ttu-id="e2e8e-190">Fonte com altura "360" e taxa de quadros "29.970" produz três camadas de vídeo:</span><span class="sxs-lookup"><span data-stu-id="e2e8e-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="e2e8e-191">Camada</span><span class="sxs-lookup"><span data-stu-id="e2e8e-191">Layer</span></span>|<span data-ttu-id="e2e8e-192">Altura</span><span class="sxs-lookup"><span data-stu-id="e2e8e-192">Height</span></span>|<span data-ttu-id="e2e8e-193">Largura</span><span class="sxs-lookup"><span data-stu-id="e2e8e-193">Width</span></span>|<span data-ttu-id="e2e8e-194">Taxa de bits (Kbps)</span><span class="sxs-lookup"><span data-stu-id="e2e8e-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="e2e8e-195">1</span><span class="sxs-lookup"><span data-stu-id="e2e8e-195">1</span></span>|<span data-ttu-id="e2e8e-196">360</span><span class="sxs-lookup"><span data-stu-id="e2e8e-196">360</span></span>|<span data-ttu-id="e2e8e-197">640</span><span class="sxs-lookup"><span data-stu-id="e2e8e-197">640</span></span>|<span data-ttu-id="e2e8e-198">700</span><span class="sxs-lookup"><span data-stu-id="e2e8e-198">700</span></span>|
|<span data-ttu-id="e2e8e-199">2</span><span class="sxs-lookup"><span data-stu-id="e2e8e-199">2</span></span>|<span data-ttu-id="e2e8e-200">270</span><span class="sxs-lookup"><span data-stu-id="e2e8e-200">270</span></span>|<span data-ttu-id="e2e8e-201">480</span><span class="sxs-lookup"><span data-stu-id="e2e8e-201">480</span></span>|<span data-ttu-id="e2e8e-202">440</span><span class="sxs-lookup"><span data-stu-id="e2e8e-202">440</span></span>|
|<span data-ttu-id="e2e8e-203">3</span><span class="sxs-lookup"><span data-stu-id="e2e8e-203">3</span></span>|<span data-ttu-id="e2e8e-204">180</span><span class="sxs-lookup"><span data-stu-id="e2e8e-204">180</span></span>|<span data-ttu-id="e2e8e-205">320</span><span class="sxs-lookup"><span data-stu-id="e2e8e-205">320</span></span>|<span data-ttu-id="e2e8e-206">230</span><span class="sxs-lookup"><span data-stu-id="e2e8e-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="e2e8e-207">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="e2e8e-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e2e8e-208">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="e2e8e-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e2e8e-209">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e2e8e-209">See Also</span></span>
[<span data-ttu-id="e2e8e-210">Visão geral da codificação de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="e2e8e-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

