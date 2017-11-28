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
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="47ba3-103">Codificar um ativo com o Codificador de Mídia Padrão usando o .NET</span><span class="sxs-lookup"><span data-stu-id="47ba3-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="47ba3-104">Trabalhos de codificação são uma das operações de processamento mais comuns Olá nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="47ba3-104">Encoding jobs are one of hello most common processing operations in Media Services.</span></span> <span data-ttu-id="47ba3-105">Criar arquivos de mídia de tooconvert trabalhos codificação de um tooanother de codificação.</span><span class="sxs-lookup"><span data-stu-id="47ba3-105">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="47ba3-106">Ao codificar, você pode usar o hello Media Encoder interno dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="47ba3-106">When you encode, you can use hello Media Services built-in Media Encoder.</span></span> <span data-ttu-id="47ba3-107">Você também pode usar um codificador fornecido por um parceiro de serviços de mídia; codificadores de terceiros estão disponíveis por meio de saudação do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="47ba3-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through hello Azure Marketplace.</span></span> 

<span data-ttu-id="47ba3-108">Este tópico mostra como toouse .NET tooencode seus ativos com o Media Encoder padrão (MES).</span><span class="sxs-lookup"><span data-stu-id="47ba3-108">This topic shows how toouse .NET tooencode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="47ba3-109">Codificador de mídia padrão é configurado usando uma das predefinições de codificador Olá descritas [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="47ba3-109">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="47ba3-110">É recomendável tooalways codificar seus arquivos de origem em uma conjunto de MP4 de taxa de bits adaptável e, em seguida, converter Olá toohello desejado formato de conjunto usando Olá [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47ba3-110">It is recommended tooalways encode your source files into an adaptive bitrate MP4 set and then convert hello set toohello desired format using hello [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="47ba3-111">Se seu ativo de saída tiver o armazenamento criptografado, você deverá configurar a política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="47ba3-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="47ba3-112">Para obter mais informações, consulte [Configurando a política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="47ba3-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="47ba3-113">Produz MES um arquivo de saída com um nome que contenha Olá primeiros 32 caracteres do hello nome de arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="47ba3-113">MES produces an output file with a name that contains hello first 32 characters of hello input file name.</span></span> <span data-ttu-id="47ba3-114">nome Hello baseia-se no que é especificado no arquivo de predefinição hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-114">hello name is based on what is specified in hello preset file.</span></span> <span data-ttu-id="47ba3-115">Por exemplo, "FileName": "{Basename}_{Index}{Extension}".</span><span class="sxs-lookup"><span data-stu-id="47ba3-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="47ba3-116">{Nome base} é substituído pelo Olá primeiros 32 caracteres do nome de arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-116">{Basename} is replaced by hello first 32 characters of hello input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="47ba3-117">Formatos de MES</span><span class="sxs-lookup"><span data-stu-id="47ba3-117">MES Formats</span></span>
[<span data-ttu-id="47ba3-118">Formatos e codecs</span><span class="sxs-lookup"><span data-stu-id="47ba3-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="47ba3-119">Predefinições de MES</span><span class="sxs-lookup"><span data-stu-id="47ba3-119">MES Presets</span></span>
<span data-ttu-id="47ba3-120">Codificador de mídia padrão é configurado usando uma das predefinições de codificador Olá descritas [aqui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="47ba3-120">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="47ba3-121">Metadados de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="47ba3-121">Input and output metadata</span></span>
<span data-ttu-id="47ba3-122">Ao codificar um ativo de entrada (ou ativos) usando MES, você obtém um ativo de saída em Olá conclusão bem-sucedida do que codificar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="47ba3-122">When you encode an input asset (or assets) using MES, you get an output asset at hello successful completion of that encode task.</span></span> <span data-ttu-id="47ba3-123">Olá ativo de saída contém vídeo, áudio, miniaturas, manifesto, etc, com base na predefinição de codificação Olá que você usar.</span><span class="sxs-lookup"><span data-stu-id="47ba3-123">hello output asset contains video, audio, thumbnails, manifest, etc. based on hello encoding preset you use.</span></span>

<span data-ttu-id="47ba3-124">Olá ativo de saída também contém um arquivo com metadados sobre o ativo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-124">hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="47ba3-125">nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: < asset_id > <asset_id>_metadata.XML (por exemplo, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), onde < asset_id > é o valor AssetId de saudação do ativo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-125">hello name of hello metadata XML file has hello following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is hello AssetId value of hello input asset.</span></span> <span data-ttu-id="47ba3-126">Olá esquema de entrada metadados XML descrita [aqui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="47ba3-126">hello schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="47ba3-127">Olá ativo de saída também contém um arquivo com metadados sobre o ativo de saída hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-127">hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="47ba3-128">nome do arquivo XML de metadados Olá Olá tem Olá formato a seguir: < source_file_name>_manifest.XML > <nome_do_arquivo_de_origem>_manifest.XML (por exemplo, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="47ba3-128">hello name of hello metadata XML file has hello following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="47ba3-129">esquema de saudação desses metadados de saída XML é descrito [aqui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="47ba3-129">hello schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="47ba3-130">Se quiser tooexamine qualquer um dos arquivos de metadados de saudação dois, você pode criar um localizador SAS e baixar o computador do local de tooyour do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-130">If you want tooexamine either of hello two metadata files, you can create a SAS locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="47ba3-131">Você pode encontrar um exemplo de como toocreate um localizador SAS e baixar uma arquivo usando Olá dos serviços de mídia extensões do SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="47ba3-131">You can find an example on how toocreate a SAS locator and download a file Using hello Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="47ba3-132">Baixar exemplo</span><span class="sxs-lookup"><span data-stu-id="47ba3-132">Download sample</span></span>
<span data-ttu-id="47ba3-133">Você pode obter e executar um exemplo que mostra como tooencode com MES de [aqui](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="47ba3-133">You can get and run a sample that shows how tooencode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="47ba3-134">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="47ba3-134">.NET sample code</span></span>

<span data-ttu-id="47ba3-135">saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47ba3-135">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="47ba3-136">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="47ba3-136">Create an encoding job.</span></span>
* <span data-ttu-id="47ba3-137">Obtém um codificador de mídia codificador padrão de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="47ba3-137">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="47ba3-138">Especificar Olá toouse [Streaming adaptável](media-services-autogen-bitrate-ladder-with-mes.md) predefinido.</span><span class="sxs-lookup"><span data-stu-id="47ba3-138">Specify toouse hello [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="47ba3-139">Adicione um único trabalho de toohello de tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="47ba3-139">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="47ba3-140">Especifique a entrada hello toobe ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="47ba3-140">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="47ba3-141">Crie um ativo de saída que conterá o ativo de saudação codificado.</span><span class="sxs-lookup"><span data-stu-id="47ba3-141">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="47ba3-142">Adicione o andamento do trabalho um evento manipulador toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="47ba3-142">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="47ba3-143">Envie trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="47ba3-143">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="47ba3-144">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="47ba3-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="47ba3-145">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="47ba3-145">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="47ba3-146">Exemplo</span><span class="sxs-lookup"><span data-stu-id="47ba3-146">Example</span></span> 

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="47ba3-147">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="47ba3-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="47ba3-148">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="47ba3-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="47ba3-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47ba3-149">Next steps</span></span>
<span data-ttu-id="47ba3-150">[Como toogenerate miniatura usando o codificador de mídia padrão com o .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[codificação visão geral de serviços de mídia](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="47ba3-150">[How toogenerate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

