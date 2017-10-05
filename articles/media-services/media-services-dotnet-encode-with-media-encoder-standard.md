---
title: Codificar um ativo com o Media Encoder Standard usando o .NET | Microsoft Docs
description: "Este tópico mostra como usar o .NET para codificar um ativo com o Codificador de Mídia Padrão."
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
ms.openlocfilehash: 929592368501c54277748bf46b2160c9058db3fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="4d5de-103">Codificar um ativo com o Codificador de Mídia Padrão usando o .NET</span><span class="sxs-lookup"><span data-stu-id="4d5de-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="4d5de-104">Os trabalhos de codificação são uma das operações de processamento mais comuns nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="4d5de-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="4d5de-105">Você cria trabalhos de codificação para converter arquivos de mídia de uma codificação para outra.</span><span class="sxs-lookup"><span data-stu-id="4d5de-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="4d5de-106">Ao codificar, você pode usar o codificador de mídia integrado dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="4d5de-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="4d5de-107">Você também pode usar um codificador fornecido por um parceiro de Serviços de Mídia. Os codificadores de terceiros estão disponíveis por meio do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4d5de-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="4d5de-108">Este tópico mostra como usar o .NET para codificar seus ativos com o MES (Codificador de Mídia Padrão).</span><span class="sxs-lookup"><span data-stu-id="4d5de-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="4d5de-109">O Codificador de Mídia Padrão é configurado usando um dos codificadores predefinidos descritos [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4d5de-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="4d5de-110">Convém sempre codificar arquivos de origem em um conjunto de MP4 de taxa de bits adaptável e, em seguida, converter o conjunto para o formato desejado usando o [Empacotamento Dinâmico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d5de-110">It is recommended to always encode your source files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="4d5de-111">Se seu ativo de saída tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="4d5de-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="4d5de-112">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4d5de-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4d5de-113">O MES produz um arquivo de saída com um nome que contém os primeiros 32 caracteres do nome do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="4d5de-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="4d5de-114">O nome é baseado no que é especificado no arquivo de predefinição.</span><span class="sxs-lookup"><span data-stu-id="4d5de-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="4d5de-115">Por exemplo, "FileName": "{Basename}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="4d5de-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="4d5de-116">{Basename} é substituído pelos primeiros 32 caracteres do nome do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="4d5de-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="4d5de-117">Formatos de MES</span><span class="sxs-lookup"><span data-stu-id="4d5de-117">MES Formats</span></span>
[<span data-ttu-id="4d5de-118">Formatos e codecs</span><span class="sxs-lookup"><span data-stu-id="4d5de-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="4d5de-119">Predefinições de MES</span><span class="sxs-lookup"><span data-stu-id="4d5de-119">MES Presets</span></span>
<span data-ttu-id="4d5de-120">O Codificador de Mídia Padrão é configurado usando um dos codificadores predefinidos descritos [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4d5de-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="4d5de-121">Metadados de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="4d5de-121">Input and output metadata</span></span>
<span data-ttu-id="4d5de-122">Ao codificar um ativo (ou ativos) de entrada usando MES, você obtém um ativo de saída na conclusão bem-sucedida da tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="4d5de-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="4d5de-123">O ativo de saída contém vídeo, áudio, miniaturas, manifesto, etc., com base na predefinição de codificação utilizada.</span><span class="sxs-lookup"><span data-stu-id="4d5de-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="4d5de-124">O ativo de saída também contém um arquivo com metadados sobre o ativo de entrada.</span><span class="sxs-lookup"><span data-stu-id="4d5de-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="4d5de-125">O nome do arquivo XML de metadados tem o seguinte formato: <asset_id>_metadata.xml (por exemplo, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), em que <asset_id> é o valor de AssetId do ativo de entrada.</span><span class="sxs-lookup"><span data-stu-id="4d5de-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="4d5de-126">O esquema desse XML de metadados de entrada é descrito [aqui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4d5de-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="4d5de-127">O ativo de saída também contém um arquivo com metadados sobre o ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="4d5de-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="4d5de-128">O nome do arquivo XML de metadados tem o seguinte formato: <nome_arquivo_origem>_manifest.xml (por exemplo, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="4d5de-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="4d5de-129">O esquema desse XML de metadados de saída é descrito [aqui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4d5de-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="4d5de-130">Se desejar examinar qualquer um dos dois arquivos de metadados, você poderá criar um localizador SAS e baixe o arquivo em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="4d5de-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="4d5de-131">É possível encontrar um exemplo de como criar um localizador SAS e baixar um arquivo usando as Extensões do SDK do .NET para os Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="4d5de-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="4d5de-132">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="4d5de-132">Download sample</span></span>
<span data-ttu-id="4d5de-133">É possível obter e executar uma amostra que explica como codificar com o MES [aqui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="4d5de-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="4d5de-134">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="4d5de-134">.NET sample code</span></span>

<span data-ttu-id="4d5de-135">O exemplo de código a seguir usa o SDK .NET dos Serviços de Mídia para executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="4d5de-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="4d5de-136">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="4d5de-136">Create an encoding job.</span></span>
* <span data-ttu-id="4d5de-137">Obtenha uma referência para o Codificador de Mídia Padrão.</span><span class="sxs-lookup"><span data-stu-id="4d5de-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="4d5de-138">Especifique para usar a predefinição [Transmissão Adaptável](media-services-autogen-bitrate-ladder-with-mes.md).</span><span class="sxs-lookup"><span data-stu-id="4d5de-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="4d5de-139">Adicione uma única tarefa de codificação para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="4d5de-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="4d5de-140">Especifique o ativo de entrada a ser codificado.</span><span class="sxs-lookup"><span data-stu-id="4d5de-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="4d5de-141">Crie um ativo de saída que conterá o ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="4d5de-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="4d5de-142">Adicione um manipulador de eventos para verificar o progresso do trabalho.</span><span class="sxs-lookup"><span data-stu-id="4d5de-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="4d5de-143">Enviar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="4d5de-143">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4d5de-144">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d5de-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4d5de-145">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4d5de-145">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4d5de-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4d5de-146">Example</span></span> 

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

                    // Create a task with the encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4d5de-147">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4d5de-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4d5de-148">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4d5de-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4d5de-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d5de-149">Next steps</span></span>
<span data-ttu-id="4d5de-150">[Como gerar miniatura usando o Media Encoder Standard com o .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Visão geral de codificação dos Serviços de Mídia](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="4d5de-150">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

