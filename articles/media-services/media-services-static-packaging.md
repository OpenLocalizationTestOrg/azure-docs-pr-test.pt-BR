---
title: "tarefas de empacotamento estático aaaUsing Azure Media Packager tooaccomplish | Microsoft Docs"
description: "Este tópico mostra várias tarefas que são realizadas com o Azure Media Packager."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0582628e-a525-4a78-90ac-9f7fc1cd909f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 64e8ba217bcd3074f5819ac3b74d2969432db5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-media-packager-tooaccomplish-static-packaging-tasks"></a><span data-ttu-id="9a785-103">Usando tarefas de empacotamento estático do Azure Media Packager tooaccomplish</span><span class="sxs-lookup"><span data-stu-id="9a785-103">Using Azure Media Packager tooaccomplish static packaging tasks</span></span>
> [!NOTE]
> <span data-ttu-id="9a785-104">fim de saudação da data de vida para o Microsoft Azure Media Packager e Microsoft Azure Media Encryptor foi estendido tooMarch 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="9a785-104">hello end of life date for Microsoft Azure Media Packager and Microsoft Azure Media Encryptor has been extended tooMarch 1, 2017.</span></span> <span data-ttu-id="9a785-105">Antes dessa data, as funcionalidades de saudação desses processadores serão adicionadas tooMedia codificador padrão (MES).</span><span class="sxs-lookup"><span data-stu-id="9a785-105">Before that date, hello functionalities of these processors will be added tooMedia Encoder Standard (MES).</span></span> <span data-ttu-id="9a785-106">Os clientes serão fornecidos com instruções sobre como toomigrate tooMES de trabalhos de toosend seus fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9a785-106">Customers will be provided with instructions on how toomigrate their workflows toosend Jobs tooMES.</span></span> <span data-ttu-id="9a785-107">Os recursos de criptografia e de conversão de formato também poderão ser disponibilizados por meio do empacotamento dinâmico e da criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="9a785-107">Format conversion and encryption capabilities may also be available through dynamic packaging and dynamic encryption.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="9a785-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9a785-108">Overview</span></span>
<span data-ttu-id="9a785-109">Em ordem toodeliver digital Olá da internet, você deve compactar vídeo sobre Olá mídia.</span><span class="sxs-lookup"><span data-stu-id="9a785-109">In order toodeliver digital video over hello internet you must compress hello media.</span></span> <span data-ttu-id="9a785-110">Arquivos de vídeo digital são muito grandes e pode ser muito grande toodeliver sobre Olá internet ou para toodisplay de dispositivos de seus clientes corretamente.</span><span class="sxs-lookup"><span data-stu-id="9a785-110">Digital video files are quite large and may be too big toodeliver over hello internet or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="9a785-111">Codificação é o processo de saudação de compactação de vídeo e áudio para que os clientes possam exibir sua mídia.</span><span class="sxs-lookup"><span data-stu-id="9a785-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span> <span data-ttu-id="9a785-112">Quando um vídeo tiver sido codificado, ele poderá ser colocado em contêineres de arquivo diferentes.</span><span class="sxs-lookup"><span data-stu-id="9a785-112">Once a video has been encoded it can be placed into different file containers.</span></span> <span data-ttu-id="9a785-113">processo de saudação de inserir mídia codificada em um contêiner é chamado de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="9a785-113">hello process of placing encoded media into a container is called packaging.</span></span> <span data-ttu-id="9a785-114">Por exemplo, você pode colocar um arquivo MP4 e convertê-la em conteúdo HLS ou Smooth Streaming usando hello Azure Media Packager.</span><span class="sxs-lookup"><span data-stu-id="9a785-114">For example, you can take an MP4 file and convert it into Smooth Streaming or HLS content by using hello Azure Media Packager.</span></span> 

<span data-ttu-id="9a785-115">O Serviços de Mídia oferece suporte ao empacotamento dinâmico e estático.</span><span class="sxs-lookup"><span data-stu-id="9a785-115">Media Services supports dynamic and static packaging.</span></span> <span data-ttu-id="9a785-116">Ao usar o empacotamento estático, você deve toocreate uma cópia do conteúdo em cada formato necessário para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="9a785-116">When using static packaging you need toocreate a copy of your content in each format required by your customers.</span></span> <span data-ttu-id="9a785-117">Com o empacotamento dinâmico, tudo o que você precisa é toocreate um ativo que contenha um conjunto de arquivos MP4 ou Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="9a785-117">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 or Smooth Streaming files.</span></span> <span data-ttu-id="9a785-118">Em seguida, com base no formato de saudação especificado no manifesto de saudação ou solicitação de fragmento, Olá sob demanda de Streaming server irá garantir que os usuários recebam fluxo Olá no protocolo de saudação que escolheram.</span><span class="sxs-lookup"><span data-stu-id="9a785-118">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that your users receive hello stream in hello protocol they have chosen.</span></span> <span data-ttu-id="9a785-119">Como resultado, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="9a785-119">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

> [!NOTE]
> <span data-ttu-id="9a785-120">É recomendável toouse [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a785-120">It is recommended toouse [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>
> 
> 

<span data-ttu-id="9a785-121">No entanto, existem alguns cenários que exigem o empacotamento estático:</span><span class="sxs-lookup"><span data-stu-id="9a785-121">However, there are some scenarios that require static packaging:</span></span> 

* <span data-ttu-id="9a785-122">Validando MP4s com taxa de bits adaptável codificados com codificadores externos (por exemplo, usando codificadores de terceiros).</span><span class="sxs-lookup"><span data-stu-id="9a785-122">Validating adaptive bitrate MP4s encoded with external encoders (for example, using third party encoders).</span></span>

<span data-ttu-id="9a785-123">Você também pode usar o hello tooperform de empacotamento estático tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a785-123">You can also use static packaging tooperform hello following tasks.</span></span> <span data-ttu-id="9a785-124">No entanto, é recomendável criptografia dinâmica toouse.</span><span class="sxs-lookup"><span data-stu-id="9a785-124">However it is recommended toouse dynamic encryption.</span></span>

* <span data-ttu-id="9a785-125">Usando a criptografia estática tooprotect seu Smooth e MPEG DASH com PlayReady</span><span class="sxs-lookup"><span data-stu-id="9a785-125">Using static encryption tooprotect your Smooth and MPEG DASH with PlayReady</span></span>
* <span data-ttu-id="9a785-126">Usando a criptografia estática tooprotect HLSv3 com AES-128</span><span class="sxs-lookup"><span data-stu-id="9a785-126">Using static encryption tooprotect HLSv3 with AES-128</span></span>
* <span data-ttu-id="9a785-127">Usando a criptografia estática tooprotect HLSv3 com PlayReady</span><span class="sxs-lookup"><span data-stu-id="9a785-127">Using static encryption tooprotect HLSv3 with PlayReady</span></span>

## <a name="validating-adaptive-bitrate-mp4s-encoded-with-external-encoders"></a><span data-ttu-id="9a785-128">Validando MP4s com taxa de bits adaptável codificados com codificadores externos</span><span class="sxs-lookup"><span data-stu-id="9a785-128">Validating Adaptive Bitrate MP4s Encoded with External Encoders</span></span>
<span data-ttu-id="9a785-129">Se você quiser toouse um conjunto de arquivos MP4 com taxa de bits adaptável (múltiplas taxas de bits) que não foram codificados com codificadores de serviços de mídia, você deverá validar seus arquivos antes de continuar o processamento.</span><span class="sxs-lookup"><span data-stu-id="9a785-129">If you want toouse a set of adaptive bitrate (multi-bitrate) MP4 files that were not encoded with Media Services' encoders, you should validate your files before further processing.</span></span> <span data-ttu-id="9a785-130">Olá Media Services Packager pode validar um ativo que contém um conjunto de arquivos MP4 e verificar se o ativo de saudação pode ser empacotado tooSmooth Streaming ou HLS.</span><span class="sxs-lookup"><span data-stu-id="9a785-130">hello Media Services Packager can validate an asset that contains a set of MP4 files and check whether hello asset can be packaged tooSmooth Streaming or HLS.</span></span> <span data-ttu-id="9a785-131">Se a tarefa de validação de saudação falhar, trabalho Olá que estava processando tarefa Olá será concluída com um erro.</span><span class="sxs-lookup"><span data-stu-id="9a785-131">If hello validation task fails, hello job that was processing hello task will complete with an error.</span></span> <span data-ttu-id="9a785-132">Olá XML que define Olá predefinido para uma tarefa de validação Olá pode ser encontrada no hello [predefinição de tarefa para o Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="9a785-132">hello XML that defines hello preset for hello validation task can be found in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

> [!NOTE]
> <span data-ttu-id="9a785-133">Use tooproduce codificador de mídia padrão hello ou Olá Media Services Packager toovalidate seu conteúdo em problemas de ordem de tempo de execução tooavoid.</span><span class="sxs-lookup"><span data-stu-id="9a785-133">Use hello Media Encoder Standard tooproduce or hello Media Services Packager toovalidate your content in order tooavoid runtime issues.</span></span> <span data-ttu-id="9a785-134">Se o servidor de Streaming sob demanda de saudação não é capaz de tooparse sua fonte de arquivos em tempo de execução, você receberá o erro de HTTP 1.1 "415 Tipo de mídia não suportado".</span><span class="sxs-lookup"><span data-stu-id="9a785-134">If hello On-Demand Streaming server is not able tooparse your source files at runtime, you will receive HTTP 1.1 error “415 Unsupported Media Type”.</span></span> <span data-ttu-id="9a785-135">Seus arquivos de origem repetidamente causando Olá servidor toofail tooparse afeta o desempenho do servidor de Streaming sob demanda de saudação e pode reduzir Olá largura de banda disponível tooserving outras solicitações.</span><span class="sxs-lookup"><span data-stu-id="9a785-135">Repeatedly causing hello server toofail tooparse your source files affects performance of hello On-Demand Streaming server and may reduce hello bandwidth available tooserving other requests.</span></span> <span data-ttu-id="9a785-136">Serviços de mídia do Azure oferece um contrato de nível de serviço (SLA) em seus serviços de Streaming sob demanda; No entanto, esse SLA não poderá ser mantida se o servidor de saudação é usado de forma incorreta Olá forma descrita acima.</span><span class="sxs-lookup"><span data-stu-id="9a785-136">Azure Media Services offers a Service Level Agreement (SLA) on its On-Demand Streaming services; however, this SLA cannot be honored if hello server is misused in hello fashion described above.</span></span>
> 
> 

<span data-ttu-id="9a785-137">Esta seção mostra como tooprocess Olá tarefa de validação.</span><span class="sxs-lookup"><span data-stu-id="9a785-137">This section shows how tooprocess hello validation task.</span></span> <span data-ttu-id="9a785-138">Ele também mostra como toosee Olá a mensagem de erro de status e Olá Olá do trabalho do que é concluído com JobStatus.Error.</span><span class="sxs-lookup"><span data-stu-id="9a785-138">It also shows how toosee hello status and hello error message of hello job that completes with JobStatus.Error.</span></span>

<span data-ttu-id="9a785-139">toovalidate seu MP4 arquivos com o Media Services Packager, você deve criar seu próprio arquivo de manifesto (. ISM) e carregá-lo junto com os arquivos de origem Olá no hello conta do Media Services.</span><span class="sxs-lookup"><span data-stu-id="9a785-139">toovalidate your MP4 files with Media Services Packager, you must create your own manifest (.ism) file and upload it together with hello source files into hello Media Services account.</span></span> <span data-ttu-id="9a785-140">Abaixo está um exemplo de arquivo do hello. ISM produzido pelo codificador de mídia padrão da saudação.</span><span class="sxs-lookup"><span data-stu-id="9a785-140">Below is a sample of hello .ism file produced by hello Media Encoder Standard.</span></span> <span data-ttu-id="9a785-141">nomes de arquivo Hello diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9a785-141">hello file names are case sensitive.</span></span> <span data-ttu-id="9a785-142">Além disso, certifique-se de que o texto de saudação no arquivo do hello. ISM está codificado com UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9a785-142">Also, make sure hello text in hello .ism file is encoded with UTF-8.</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
    <!-- Tells hello server that these input files are MP4s – specific tooDynamic Packaging -->
        <meta name="formats" content="mp4" /> 
      </head>
      <body>
        <switch>
          <video src="BigBuckBunny_1000.mp4" />
          <video src="BigBuckBunny_1500.mp4" />
          <video src="BigBuckBunny_2250.mp4" />
          <video src="BigBuckBunny_3400.mp4" />
          <video src="BigBuckBunny_400.mp4" />
          <video src="BigBuckBunny_650.mp4" />
          <audio src="BigBuckBunny_400.mp4" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="9a785-143">Uma vez que Olá taxa de bits adaptável que MP4 conjunto que você pode aproveitar o empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="9a785-143">Once you have hello adaptive bitrate MP4 set you can take advantage of Dynamic Packaging.</span></span> <span data-ttu-id="9a785-144">O empacotamento dinâmico permite fluxos toodeliver Olá especificado protocolo sem necessidade de empacotamento adicional.</span><span class="sxs-lookup"><span data-stu-id="9a785-144">Dynamic Packaging allows you toodeliver streams in hello specified protocol without further packaging.</span></span> <span data-ttu-id="9a785-145">Para saber mais, consulte [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a785-145">For more information, see [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="9a785-146">Olá seguindo o exemplo de código usa extensões de SDK .NET do serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a785-146">hello following code sample uses Azure Media Services .NET SDK Extensions.</span></span>  <span data-ttu-id="9a785-147">Certifique-se de que tooupdate Olá código toopoint toohello pasta na qual seus arquivos MP4 de entrada e o arquivo. ISM estão localizados.</span><span class="sxs-lookup"><span data-stu-id="9a785-147">Make sure tooupdate hello code toopoint toohello folder where your input MP4 files and .ism file are located.</span></span> <span data-ttu-id="9a785-148">E também toowhere sua MediaPackager_ValidateTask.xml arquivo está localizado.</span><span class="sxs-lookup"><span data-stu-id="9a785-148">And also toowhere your MediaPackager_ValidateTask.xml file is located.</span></span> <span data-ttu-id="9a785-149">Esse arquivo XML é definido no tópico [Predefinição de Tarefa para o Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9a785-149">This XML file is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Xml.Linq;

    namespace MediaServicesStaticPackaging
    {
        class Program
        {
            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            // hello MultibitrateMP4Files folder should also
            // contain hello .ism manifest file.
            private static readonly string _multibitrateMP4s =
                Path.Combine(_mediaFiles, @"MultibitrateMP4Files");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Ingest a set of multibitrate MP4s.
                //
                // Use hello SDK extension method toocreate a new asset by 
                // uploading files from a local directory.
                IAsset multibitrateMP4sAsset = _context.Assets.CreateFromFolder(
                    _multibitrateMP4s,
                    AssetCreationOptions.None,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                // Use Azure Media Packager toovalidate hello files.
                IAsset validatedMP4s =
                    ValidateMultibitrateMP4s(multibitrateMP4sAsset);

                // Publish hello asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    validatedMP4s,
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                                     // Get hello streaming URLs.
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(validatedMP4s.GetSmoothStreamingUri().ToString());
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(validatedMP4s.GetMpegDashUri().ToString());
                Console.WriteLine("HLS URL:");
                Console.WriteLine(validatedMP4s.GetHlsUri().ToString());
            }

            public static IAsset ValidateMultibitrateMP4s(IAsset multibitrateMP4sAsset)
            {
                // Set .ism as a primary file 
                // in a multibitrate MP4 set.
                SetISMFileAsPrimary(multibitrateMP4sAsset);

                // Create a new job.
                IJob job = _context.Jobs.Create("MP4 validation and converstion tooSmooth Stream job.");

                // Read hello task configuration data into a string. 
                string configMp4Validation = File.ReadAllText(Path.Combine(
                        _configurationXMLFiles,
                        "MediaPackager_ValidateTask.xml"));

                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Create a task with hello conversion details, using hello configuration data. 
                ITask task = job.Tasks.AddNew("Mp4 Validation Task",
                    processor,
                    configMp4Validation,
                    TaskOptions.None);

                // Specify hello input asset toobe validated.
                task.InputAssets.Add(multibitrateMP4sAsset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted). 
                task.OutputAssets.AddNew("Validated output asset",
                        AssetCreationOptions.None);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // If hello validation task fails and job completes with JobState.Error,
                // display hello error message and throw an exception.
                if (job.State == JobState.Error)
                {
                    Console.WriteLine("  Job ID: " + job.Id);
                    Console.WriteLine("  Name: " + job.Name);
                    Console.WriteLine("  State: " + job.State);

                    foreach (var jobTask in job.Tasks)
                    {
                        Console.WriteLine("  Task Id: " + jobTask.Id);
                        Console.WriteLine("  Name: " + jobTask.Name);
                        Console.WriteLine("  Progress: " + jobTask.Progress);
                        Console.WriteLine("  Configuration: " + jobTask.Configuration);
                        Console.WriteLine("  Running time: " + jobTask.RunningDuration);
                        if (jobTask.ErrorDetails != null)
                        {
                            foreach (var errordetail in jobTask.ErrorDetails)
                            {

                                Console.WriteLine("  Error Message:" + errordetail.Message);
                                Console.WriteLine("  Error Code:" + errordetail.Code);
                            }
                        }
                    }
                    throw new Exception("hello specified multi-bitrate MP4 set is not valid.");
                }


                return job.OutputMediaAssets[0];
            }

            static void SetISMFileAsPrimary(IAsset asset)
            {
                var ismAssetFiles = asset.AssetFiles.ToList().
                    Where(f => f.Name.EndsWith(".ism", StringComparison.OrdinalIgnoreCase)).ToArray();

                // hello following code assigns hello first .ism file as hello primary file in hello asset.
                // An asset should have one .ism file.  
                ismAssetFiles.First().IsPrimary = true;
                ismAssetFiles.First().Update();
            }
        }
    }

## <a name="using-static-encryption-tooprotect-your-smooth-and-mpeg-dash-with-playready"></a><span data-ttu-id="9a785-150">Usando a criptografia estática tooProtect seu Smooth e MPEG DASH com PlayReady</span><span class="sxs-lookup"><span data-stu-id="9a785-150">Using Static Encryption tooProtect your Smooth and MPEG DASH with PlayReady</span></span>
<span data-ttu-id="9a785-151">Se você quiser tooprotect seu conteúdo com PlayReady, você tem a opção de usar [criptografia dinâmica](media-services-protect-with-drm.md) (Olá opção recomendada) ou criptografia estática (conforme descrito nesta seção).</span><span class="sxs-lookup"><span data-stu-id="9a785-151">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

<span data-ttu-id="9a785-152">exemplo Hello nesta seção codifica um arquivo mezanino (neste caso, MP4) em arquivos MP4 de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="9a785-152">hello example in this section encodes a mezzanine file (in this case MP4) into adaptive bitrate MP4 files.</span></span> <span data-ttu-id="9a785-153">Ele então empacota os MP4s como Smooth Streaming e criptografa o Smooth Streaming com o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="9a785-153">It then packages MP4s into Smooth Streaming and then encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="9a785-154">Como resultado, será possível toostream Smooth Streaming ou MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="9a785-154">As a result you are able toostream Smooth Streaming or MPEG DASH.</span></span>

<span data-ttu-id="9a785-155">Os Serviços de Mídia agora fornecem um serviço de distribuição de licenças do Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="9a785-155">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="9a785-156">Olá exemplo neste artigo mostra como serviço de entrega de licença de tooconfigure Olá PlayReady dos serviços de mídia (consulte o método de ConfigureLicenseDeliveryService Olá definido no código de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="9a785-156">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello ConfigureLicenseDeliveryService method defined in hello code below).</span></span> <span data-ttu-id="9a785-157">Para saber mais sobre o serviço de entrega de licença do PlayReady do Serviços de Mídia, consulte [Usando o serviço de entrega de licença e a criptografia dinâmica do PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="9a785-157">For more information about Media Services PlayReady license delivery service, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9a785-158">toodeliver MPEG DASH criptografado com PlayReady, verifique toouse-se de que as opções CENC definindo propriedades de saudação e adjustSubSamples (descrito no hello [predefinidos de tarefa para o Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) tópico) tootrue.</span><span class="sxs-lookup"><span data-stu-id="9a785-158">toodeliver MPEG DASH encrypted with PlayReady, make sure toouse CENC options by setting hello useSencBox and adjustSubSamples properties (described in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic) tootrue.</span></span>  
> 
> 

<span data-ttu-id="9a785-159">Certifique-se de saudação tooupdate pasta de toohello toopoint de código onde se encontra o arquivo MP4 de entrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a785-159">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span>

<span data-ttu-id="9a785-160">E também toowhere seus MediaPackager_MP4ToSmooth.xml e MediaEncryptor_PlayReadyProtection.xml arquivos estão localizados.</span><span class="sxs-lookup"><span data-stu-id="9a785-160">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="9a785-161">MediaPackager_MP4ToSmooth.xml é definido em [predefinidos de tarefa para o Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) e MediaEncryptor_PlayReadyProtection.xml é definido em Olá [predefinidos de tarefa para o Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="9a785-161">MediaPackager_MP4ToSmooth.xml is defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span> 

<span data-ttu-id="9a785-162">exemplo Hello define o método de UpdatePlayReadyConfigurationXMLFile de saudação que você pode usar o arquivo de MediaEncryptor_PlayReadyProtection.xml toodynamically atualização hello.</span><span class="sxs-lookup"><span data-stu-id="9a785-162">hello example defines hello UpdatePlayReadyConfigurationXMLFile method that you can use toodynamically update hello MediaEncryptor_PlayReadyProtection.xml file.</span></span> <span data-ttu-id="9a785-163">Se você tiver a semente chave Olá disponível, você pode usar o hello CommonEncryption.GeneratePlayReadyContentKey método toogenerate Olá chave de conteúdo com base em valores hello keySeedValue e KeyId.</span><span class="sxs-lookup"><span data-stu-id="9a785-163">If you have hello key seed available, you can use hello CommonEncryption.GeneratePlayReadyContentKey method toogenerate hello content key based on hello keySeedValue and KeyId values.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace PlayReadyStaticEncryptAndKeyDeliverySvc
    {
        class Program
        {

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////
                // Load a single MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset =
                    ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);


                // Encrypt your clear Smooth Streaming tooSmooth Streaming with PlayReady.
                IAsset outputAsset = CreateSmoothStreamEncryptedWithPlayReady(clearSmoothStreamAsset);


                // You can use hello http://smf.cloudapp.net/healthmonitor player 
                // tootest hello smoothStreamURL URL.
                string smoothStreamURL = outputAsset.GetSmoothStreamingUri().ToString();
                Console.WriteLine("Smooth Streaming URL:");
                Console.WriteLine(smoothStreamURL);

                // You can use hello http://dashif.org/reference/players/javascript/ player 
                // tootest hello dashURL URL.
                string dashURL = outputAsset.GetMpegDashUri().ToString();
                Console.WriteLine("MPEG DASH URL:");
                Console.WriteLine(dashURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Stream.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains hello Smooth Streaming asset.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts Smooth Stream with PlayReady.
            /// Then creates a Smooth Streaming Url.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateSmoothStreamEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                // Create a job.
                IJob job = _context.Jobs.Create("Encrypt tooPlayReady Smooth Streaming.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare hello encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Stream",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: toodeliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue. 
            /// In this example, MediaEncryptor_PlayReadyProtection.xml contains configuration.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);

                return playreadyAsset;
            }

            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }

            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-aes-128"></a><span data-ttu-id="9a785-164">Usando a criptografia estática tooProtect HLSv3 com AES-128</span><span class="sxs-lookup"><span data-stu-id="9a785-164">Using Static Encryption tooProtect HLSv3 with AES-128</span></span>
<span data-ttu-id="9a785-165">Se você quiser tooencrypt o HLS com AES-128, você tem a opção de usar criptografia dinâmica (Olá opção recomendada) ou criptografia estática (conforme mostrado nesta seção).</span><span class="sxs-lookup"><span data-stu-id="9a785-165">If you want tooencrypt your HLS with AES-128, you have a choice of using dynamic encryption (hello recommended option) or static encryption (as shown in this section).</span></span> <span data-ttu-id="9a785-166">Se você decidir criptografia dinâmica toouse, consulte [usando criptografia dinâmica AES-128 e o serviço de entrega de chave](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="9a785-166">If you decide toouse dynamic encryption, see [Using AES-128 Dynamic Encryption and Key Delivery Service](media-services-protect-with-aes128.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9a785-167">Em ordem tooconvert seu conteúdo em HLS, você deve primeiro converter/codificar o conteúdo em Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9a785-167">In order tooconvert your content into HLS, you must first convert/encode your content into Smooth Streaming.</span></span>
> <span data-ttu-id="9a785-168">Além disso, para Olá HLS tooget criptografado com AES Certifique se tooset Olá seguintes propriedades no arquivo MediaPackager_SmoothToHLS.xml: Olá conjunto criptografar tootrue de propriedade, defina o valor de chave de saudação e Olá keyuri valor toopoint tooyour authentication\ servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="9a785-168">Also, for hello HLS tooget encrypted with AES make sure tooset hello following properties in your MediaPackager_SmoothToHLS.xml file: set hello encrypt property tootrue, set hello key value, and hello keyuri value toopoint tooyour authentication\authorization server.</span></span>
> <span data-ttu-id="9a785-169">Serviços de mídia criará um arquivo de chave e colocá-lo no contêiner de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a785-169">Media Services will create a key file and place it in hello asset container.</span></span> <span data-ttu-id="9a785-170">Você deve copiar o servidor de tooyour Olá /asset-containerguid/*.key arquivos (ou criar seu próprio arquivo de chave) e exclua o arquivo de Key de saudação do contêiner de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a785-170">You should copy hello /asset-containerguid/*.key file tooyour server (or create your own key file) and then delete hello *.key file from hello asset container.</span></span>
> 
> 

<span data-ttu-id="9a785-171">exemplo Hello nesta seção codifica um arquivo mezanino (neste caso, MP4) em como arquivos de MP4 e, em seguida, empacota MP4s em Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9a785-171">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files and then packages MP4s into Smooth Streaming.</span></span> <span data-ttu-id="9a785-172">Ele então empacota o Smooth Streaming em HTTP Live Streaming (HLS) criptografado com a criptografia de fluxo de 128 bits do Padrão de Criptografia Avançada (AES).</span><span class="sxs-lookup"><span data-stu-id="9a785-172">It then packages Smooth Streaming into HTTP Live Streaming (HLS) encrypted with Advanced Encryption Standard (AES) 128-bit stream encryption.</span></span> <span data-ttu-id="9a785-173">Certifique-se de saudação tooupdate pasta de toohello toopoint de código onde se encontra o arquivo MP4 de entrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a785-173">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="9a785-174">E também toowhere seus arquivos de configuração MediaPackager_MP4ToSmooth.xml e MediaPackager_SmoothToHLS.xml estão localizados.</span><span class="sxs-lookup"><span data-stu-id="9a785-174">And also toowhere your MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml configuration files are located.</span></span> <span data-ttu-id="9a785-175">Você pode encontrar a definição Olá para esses arquivos no hello [predefinidos de tarefa para o Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="9a785-175">You can find hello definition for these files in hello [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";

            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName = 
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey = 
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName, 
                                _mediaServicesAccountKey);
                // Use hello cached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Encoding and encrypting assets //////////////////////

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create HLS encrypted with AES.
                IAsset HLSEncryptedWithAESAsset = CreateHLSEncryptedWithAES(clearSmoothStreamAsset);

                // You can use hello following player tootest hello HLS with AES stream.
                // http://apps.microsoft.com/windows/app/3ivx-hls-player/f79ce7d0-2993-4658-bc4e-83dc182a0614 
                string hlsWithAESURL = HLSEncryptedWithAESAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with AES URL:");
                Console.WriteLine(hlsWithAESURL);
            }


            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Encrypts an HLS with AES-128.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithAES(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with AES.");

                // Add task 1 - Package clear Smooth Streaming tooHLS with AES.
                PackageSmoothStreamToHLS(job, clearSmoothStreamAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // hello OutputMediaAssets[0] contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[0],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[0];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });

                return asset;
            }

            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s", 
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles, 
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset = 
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming", 
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }

            /// <summary>
            /// Converts Smooth Streaming tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Streaming asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                // For hello HLS tooget encrypted with AES make sure tooset the
                // encrypt configuration property tootrue.
                //
                // In production, it is recommended toodo hello following:
                //    Set a Key url for your authn/authz server.
                //    Copy hello /asset-containerguid/*.key file tooyour server (or craft a key file for yourself).
                //    Delete *.key from hello asset container.
                //
                string configuration = File.ReadAllText(Path.Combine(_configurationXMLFiles, @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth Streaming tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset = 
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }
        }
    }

## <a name="using-static-encryption-tooprotect-hlsv3-with-playready"></a><span data-ttu-id="9a785-176">Usando a criptografia estática tooProtect HLSv3 com PlayReady</span><span class="sxs-lookup"><span data-stu-id="9a785-176">Using Static Encryption tooProtect HLSv3 with PlayReady</span></span>
<span data-ttu-id="9a785-177">Se você quiser tooprotect seu conteúdo com PlayReady, você tem a opção de usar [criptografia dinâmica](media-services-protect-with-drm.md) (Olá opção recomendada) ou criptografia estática (conforme descrito nesta seção).</span><span class="sxs-lookup"><span data-stu-id="9a785-177">If you want tooprotect your content with PlayReady, you have a choice of using [dynamic encryption](media-services-protect-with-drm.md) (hello recommended option) or static encryption (as described in this section).</span></span>

> [!NOTE]
> <span data-ttu-id="9a785-178">Em ordem tooprotect seu conteúdo usando PlayReady você deve primeiro converter/codificar o conteúdo em um formato de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9a785-178">In order tooprotect your content using PlayReady you must first convert/encode your content into a Smooth Streaming format.</span></span>
> 
> 

<span data-ttu-id="9a785-179">exemplo Hello nesta seção codifica um arquivo mezanino (neste caso, MP4) em arquivos de taxa de bits múltipla MP4.</span><span class="sxs-lookup"><span data-stu-id="9a785-179">hello example in this section encodes a mezzanine file (in this case MP4) into multibitrate MP4 files.</span></span> <span data-ttu-id="9a785-180">Ele então empacota os MP4s no Smooth Streaming e criptografa o Smooth Streaming com o PlayReady.</span><span class="sxs-lookup"><span data-stu-id="9a785-180">It then packages MP4s into Smooth Streaming and encrypts Smooth Streaming with PlayReady.</span></span> <span data-ttu-id="9a785-181">tooproduce HTTP Live Streaming (HLS) criptografado com PlayReady, o ativo PlayReady Smooth Streaming de saudação precisa toobe empacotado como HLS.</span><span class="sxs-lookup"><span data-stu-id="9a785-181">tooproduce HTTP Live Streaming (HLS) encrypted with PlayReady, hello PlayReady Smooth Streaming asset needs toobe packaged into HLS.</span></span> <span data-ttu-id="9a785-182">Este tópico demonstra como tooperform todas essas etapas.</span><span class="sxs-lookup"><span data-stu-id="9a785-182">This topic demonstrates how tooperform all these steps.</span></span>

<span data-ttu-id="9a785-183">Os Serviços de Mídia agora fornecem um serviço de distribuição de licenças do Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="9a785-183">Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="9a785-184">Olá exemplo neste artigo mostra como serviço de entrega de licença de tooconfigure Olá PlayReady dos serviços de mídia (consulte Olá **ConfigureLicenseDeliveryService** método definido no código de saudação abaixo).</span><span class="sxs-lookup"><span data-stu-id="9a785-184">hello example in this article shows how tooconfigure hello Media Services PlayReady license delivery service (see hello **ConfigureLicenseDeliveryService** method defined in hello code below).</span></span> 

<span data-ttu-id="9a785-185">Certifique-se de saudação tooupdate pasta de toohello toopoint de código onde se encontra o arquivo MP4 de entrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a785-185">Make sure tooupdate hello following code toopoint toohello folder where your input MP4 file is located.</span></span> <span data-ttu-id="9a785-186">E também toowhere seus MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml e MediaEncryptor_PlayReadyProtection.xml arquivos estão localizados.</span><span class="sxs-lookup"><span data-stu-id="9a785-186">And also toowhere your MediaPackager_MP4ToSmooth.xml, MediaPackager_SmoothToHLS.xml, and MediaEncryptor_PlayReadyProtection.xml files are located.</span></span> <span data-ttu-id="9a785-187">MediaPackager_MP4ToSmooth.xml e MediaPackager_SmoothToHLS.xml são definidos no [predefinidos de tarefa para o Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) e MediaEncryptor_PlayReadyProtection.xml é definido em Olá [predefinidos de tarefa para o Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="9a785-187">MediaPackager_MP4ToSmooth.xml and MediaPackager_SmoothToHLS.xml are defined in [Task Preset for Azure Media Packager](http://msdn.microsoft.com/library/azure/hh973635.aspx) and MediaEncryptor_PlayReadyProtection.xml is defined in hello [Task Preset for Azure Media Encryptor](http://msdn.microsoft.com/library/azure/hh973610.aspx) topic.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Xml.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace MediaServicesContentProtection
    {
        class Program
        {
            // Paths toosupport files (within hello above base path). You can use 
            // hello provided sample media files from hello "SupportFiles" folder, or 
            // provide paths tooyour own media files below toorun these samples.

            private static readonly string _mediaFiles =
                Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
                Path.Combine(_mediaFiles, @"SingleMP4\BigBuckBunny.mp4");

            // XML Configruation files path.
            private static readonly string _configurationXMLFiles = @"../..\Configurations\";


            private static MediaServicesCredentials _cachedCredentials = null;
            private static CloudMediaContext _context = null;

            // Media Services account information.
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServiceAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServiceAccountKey"];

            static void Main(string[] args)
            {
                // Create and cache hello Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used hello chached credentials toocreate CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

                // Load an MP4 file.
                IAsset asset = IngestSingleMP4File(_singleMP4File, AssetCreationOptions.None);

                // Encode an MP4 file tooa set of multibitrate MP4s.
                // Then, package a set of MP4s tooclear Smooth Streaming.
                IAsset clearSmoothStreamAsset = ConvertMP4ToMultibitrateMP4sToSmoothStreaming(asset);

                // Create a common encryption content key that is used 
                // a) tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
                //    that is used for encryption.
                // b) tooconfigure hello license delivery service and 
                //
                Guid keyId;
                byte[] contentKey;

                IContentKey key = CreateCommonEncryptionKey(out keyId, out contentKey);

                // hello content key authorization policy must be configured by you 
                // and met by hello client in order for hello PlayReady license
                // toobe delivered toohello client. 
                // In this example hello Media Services PlayReady license delivery service is used.
                ConfigureLicenseDeliveryService(key);

                // Get hello Media Services PlayReady license delivery URL.
                // This URL will be assigned toohello licenseAcquisitionUrl property 
                // of hello MediaEncryptor_PlayReadyProtection.xml file.
                Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

                // Update hello MediaEncryptor_PlayReadyProtection.xml file with hello key and URL info.
                UpdatePlayReadyConfigurationXMLFile(keyId, contentKey, acquisitionUrl);

                // Create HLS encrypted with PlayReady.
                IAsset playReadyHLSAsset = CreateHLSEncryptedWithPlayReady(clearSmoothStreamAsset);
                //
                string hlsWithPlayReadyURL = playReadyHLSAsset.GetHlsUri().ToString();
                Console.WriteLine("HLS with PlayReady URL:");
                Console.WriteLine(hlsWithPlayReadyURL);
            }

            /// <summary>
            /// Creates a job with 2 tasks: 
            /// 1 task - encodes a single MP4 toomultibitrate MP4s,
            /// 2 task - packages MP4s tooSmooth Streaming.
            /// </summary>
            /// <returns>hello output asset.</returns>
            public static IAsset ConvertMP4ToMultibitrateMP4sToSmoothStreaming(IAsset asset)
            {
                // Create a new job.
                IJob job = _context.Jobs.Create("Convert MP4 tooSmooth Streaming.");

                // Add task 1 - Encode single MP4 into multibitrate MP4s.
                IAsset MP4sAsset = EncodeSingleMP4IntoMultibitrateMP4sTask(job, asset);
                // Add task 2 - Package a multibitrate MP4 set tooClear Smooth Streaming.
                IAsset packagedAsset = PackageMP4ToSmoothStreamingTask(job, MP4sAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Get hello output asset that contains Smooth Streaming.
                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Create a common encryption content key that is used 
            /// tooset hello key values in hello MediaEncryptor_PlayReadyProtection.xml file
            /// that is used for encryption.
            /// </summary>
            /// <param name="keyId"></param>
            /// <param name="contentKey"></param>
            /// <returns></returns>
            public static IContentKey CreateCommonEncryptionKey(out Guid keyId, out byte[] contentKey)
            {
                keyId = Guid.NewGuid();
                contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
            }

            /// <summary>
            /// Update your configuration .xml file dynamically.
            /// </summary>
            public static void UpdatePlayReadyConfigurationXMLFile(Guid keyId, byte[] keyValue, Uri licenseAcquisitionUrl)
            {
                string xmlFileName = Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml");

                XNamespace xmlns = "http://schemas.microsoft.com/iis/media/v4/TM/TaskDefinition#";

                // Prepare hello encryption task template
                XDocument doc = XDocument.Load(xmlFileName);

                var licenseAcquisitionUrlEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "licenseAcquisitionUrl")
                        .FirstOrDefault();
                var contentKeyEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "contentKey")
                        .FirstOrDefault();
                var keyIdEl = doc
                        .Descendants(xmlns + "property")
                        .Where(p => p.Attribute("name").Value == "keyId")
                        .FirstOrDefault();

                // Update hello "value" property.
                if (licenseAcquisitionUrlEl != null)
                    licenseAcquisitionUrlEl.Attribute("value").SetValue(licenseAcquisitionUrl.ToString());

                if (contentKeyEl != null)
                    contentKeyEl.Attribute("value").SetValue(Convert.ToBase64String(keyValue));

                if (keyIdEl != null)
                    keyIdEl.Attribute("value").SetValue(keyId);

                doc.Save(xmlFileName);
            }

            /// <summary>
            // Encrypts clear Smooth Streaming tooSmooth Streaming with PlayReady.
            // Then, packages hello PlayReady Smooth Streaming tooHLS with PlayReady.
            /// </summary>
            /// <param name="clearSmoothAsset">Asset that contains clear Smooth Streaming.</param>
            /// <returns>hello output asset.</returns>
            public static IAsset CreateHLSEncryptedWithPlayReady(IAsset clearSmoothStreamAsset)
            {
                IJob job = _context.Jobs.Create("Encrypt tooHLS with PlayReady.");

                // Add task 1 - Encrypt Smooth Streaming with PlayReady 
                IAsset encryptedSmoothAsset =
                    EncryptSmoothStreamWithPlayReadyTask(job, clearSmoothStreamAsset);

                // Add task 2 - Package tooHLS with PlayReady.
                PackageSmoothStreamToHLS(job, encryptedSmoothAsset);

                // Submit hello job and wait until it is completed.
                job.Submit();
                job = job.StartExecutionProgressTask(
                    j =>
                    {
                        Console.WriteLine("Job state: {0}", j.State);
                        Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
                    },
                    CancellationToken.None).Result;

                // Since we had two tasks, hello OutputMediaAssets[1]
                // contains hello desired asset.
                _context.Locators.Create(
                    LocatorType.OnDemandOrigin,
                    job.OutputMediaAssets[1],
                    AccessPermissions.Read,
                    TimeSpan.FromDays(30));

                return job.OutputMediaAssets[1];
            }

            /// <summary>
            /// Uploads a single file.
            /// </summary>
            /// <param name="fileDir">hello location of hello files.</param>
            /// <param name="assetCreationOptions">
            ///  You can specify hello following encryption options for hello AssetCreationOptions.
            ///      None:  no encryption.  
            ///      StorageEncrypted: storage encryption. Encrypts a clear input file 
            ///        before it is uploaded tooAzure storage. 
            ///      CommonEncryptionProtected: for Common Encryption Protected (CENC) files. 
            ///        For example, a set of files that are already PlayReady encrypted. 
            ///      EnvelopeEncryptionProtected: for HLS with AES encryption files.
            ///        NOTE: hello files must have been encoded and encrypted by Transform Manager. 
            ///     </param>
            /// <returns>Returns an asset that contains a single file.</returns>
            /// </summary>
            /// <returns></returns>
            private static IAsset IngestSingleMP4File(string fileDir, AssetCreationOptions assetCreationOptions)
            {
                // Use hello SDK extension method toocreate a new asset by 
                // uploading a mezzanine file from a local path.
                IAsset asset = _context.Assets.CreateFromFile(
                    fileDir,
                    assetCreationOptions,
                    (af, p) =>
                    {
                        Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
                    });


                return asset;

            }
            /// <summary>
            /// Creates a task tooencode tooAdaptive Bitrate. 
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncodeSingleMP4IntoMultibitrateMP4sTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Media Encoder Standard.
                IMediaProcessor encoder = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.MediaEncoderStandard);

                ITask adpativeBitrateTask = job.Tasks.AddNew("MP4 tooAdaptive Bitrate Task",
                   encoder,
                   "Adaptive Streaming",
                   TaskOptions.None);

                // Specify hello input Asset
                adpativeBitrateTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset abrAsset = adpativeBitrateTask.OutputAssets.AddNew("Multibitrate MP4s",
                                        AssetCreationOptions.None);

                return abrAsset;
            }

            /// <summary>
            /// Creates a task tooconvert hello MP4 file(s) tooa Smooth Streaming asset.
            /// Adds hello new task tooa job.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset PackageMP4ToSmoothStreamingTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor packager = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Azure Media Packager does not accept string presets, so load xml configuration
                string smoothConfig = File.ReadAllText(Path.Combine(
                            _configurationXMLFiles,
                            "MediaPackager_MP4toSmooth.xml"));

                // Create a new Task tooconvert adaptive bitrate tooSmooth Streaming.
                ITask smoothStreamingTask = job.Tasks.AddNew("MP4 tooSmooth Task",
                   packager,
                   smoothConfig,
                   TaskOptions.None);

                // Specify hello input Asset, which is hello output Asset from hello first task
                smoothStreamingTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.None, which 
                // means hello output asset is in hello clear (unencrypted).
                IAsset smoothOutputAsset =
                    smoothStreamingTask.OutputAssets.AddNew("Clear Smooth Streaming",
                        AssetCreationOptions.None);

                return smoothOutputAsset;
            }


            /// <summary>
            /// Converts Smooth Stream tooHLS.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello Smooth Stream asset.</param>
            /// <returns>hello asset that was packaged tooHLS.</returns>
            private static IAsset PackageSmoothStreamToHLS(IJob job, IAsset smoothStreamAsset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Packager.
                IMediaProcessor processor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaPackager);

                // Read hello configuration data into a string. 
                //
                string configuration = File.ReadAllText(
                            Path.Combine(_configurationXMLFiles,
                                        @"MediaPackager_SmoothToHLS.xml"));

                // Create a task with hello encoding details, using a configuration file.
                ITask task = job.Tasks.AddNew("My Smooth tooHLS Task",
                   processor,
                   configuration,
                   TaskOptions.ProtectedConfiguration);

                // Specify hello input asset toobe encoded.
                task.InputAssets.Add(smoothStreamAsset);

                // Add an output asset toocontain hello results of hello job. 
                IAsset outputAsset =
                    task.OutputAssets.AddNew("HLS asset", AssetCreationOptions.None);


                return outputAsset;
            }

            /// <summary>
            /// Creates a task tooencrypt Smooth Streaming with PlayReady.
            /// Note: Do deliver DASH, make sure tooset hello useSencBox and adjustSubSamples 
            /// configuration properties tootrue.
            /// </summary>
            /// <param name="job">hello job toowhich tooadd hello new task.</param>
            /// <param name="asset">hello input asset.</param>
            /// <returns>hello output asset.</returns>
            private static IAsset EncryptSmoothStreamWithPlayReadyTask(IJob job, IAsset asset)
            {
                // Get hello SDK extension method too get a reference toohello Azure Media Encryptor.
                IMediaProcessor playreadyProcessor = _context.MediaProcessors.GetLatestMediaProcessorByName(
                    MediaProcessorNames.WindowsAzureMediaEncryptor);

                // Read hello configuration XML.
                //
                // Note that hello configuration defined in MediaEncryptor_PlayReadyProtection.xml
                // is using keySeedValue. It is recommended that you do this only for testing 
                // and not in production. For more information, see 
                // http://msdn.microsoft.com/library/windowsazure/dn189154.aspx.
                //
                string configPlayReady = File.ReadAllText(Path.Combine(_configurationXMLFiles,
                                            @"MediaEncryptor_PlayReadyProtection.xml"));

                ITask playreadyTask = job.Tasks.AddNew("My PlayReady Task",
                   playreadyProcessor,
                   configPlayReady,
                   TaskOptions.ProtectedConfiguration);

                playreadyTask.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job. 
                // This output is specified as AssetCreationOptions.CommonEncryptionProtected.
                IAsset playreadyAsset = playreadyTask.OutputAssets.AddNew(
                                                "PlayReady Smooth Streaming",
                                                AssetCreationOptions.CommonEncryptionProtected);


                return playreadyAsset;
            }


            /// <summary>
            /// Configures authorization policy for hello content key. 
            /// </summary>
            /// <param name="contentKey">hello content key.</param>
            static public void ConfigureLicenseDeliveryService(IContentKey contentKey)
            {
                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                    new ContentKeyAuthorizationPolicyRestriction 
                    { 
                        Name = "Open", 
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open, 
                        Requirements = null
                    }
                };

                // Configure PlayReady license template.
                string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                IContentKeyAuthorizationPolicyOption policyOption =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, newLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(policyOption);

                // Associate hello content key authorization policy with hello content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // hello following code configures PlayReady License Template using .NET classes
                // and returns hello XML string.

                PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }
            static private byte[] GetRandomBuffer(int length)
            {
                var returnValue = new byte[length];

                using (var rng =
                    new System.Security.Cryptography.RNGCryptoServiceProvider())
                {
                    rng.GetBytes(returnValue);
                }

                return returnValue;
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="9a785-188">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="9a785-188">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9a785-189">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="9a785-189">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

