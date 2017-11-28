---
title: "predefinições de codificador de mídia padrão aaaCustomizing | Microsoft Docs"
description: "Este tópico mostra como tooperform avançados de codificação Personalizando o codificador de mídia padrão predefinições de tarefa. tópico de saudação mostra como toouse SDK do Media Services .NET toocreate uma codificação de tarefas e de trabalho. Ele também mostra como toosupply personalizado predefinições toohello trabalho de codificação."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: fa8c3bef63b0c1ecc88a6b8874ecbff3a8028a57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="4d9e3-105">Personalizando as predefinições do Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="4d9e3-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="4d9e3-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4d9e3-106">Overview</span></span>

<span data-ttu-id="4d9e3-107">Este tópico mostra como tooperform avançado de codificação com mídia codificador padrão (MES) usando um personalizado predefinido.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-107">This topic shows how tooperform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="4d9e3-108">tópico de saudação usa .NET toocreate uma tarefa de codificação e um trabalho que executa essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-108">hello topic uses .NET toocreate an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="4d9e3-109">Neste tópico você verá como toocustomize uma predefinição colocando Olá [H264 várias taxas de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) número Olá predefinidas e redução de camadas.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-109">In this topic you will see how toocustomize a preset by taking hello [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing hello number of layers.</span></span> <span data-ttu-id="4d9e3-110">Olá [predefinições de codificador padrão do personalizando mídia](media-services-advanced-encoding-with-mes.md) tópico demonstra as predefinições personalizadas que podem ser usado tooperform avançado tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-110">hello [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used tooperform advanced encoding tasks.</span></span>

## <span data-ttu-id="4d9e3-111"><a id="customizing_presets"></a> Personalizando uma predefinição do MES</span><span class="sxs-lookup"><span data-stu-id="4d9e3-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="4d9e3-112">Predefinição original</span><span class="sxs-lookup"><span data-stu-id="4d9e3-112">Original preset</span></span>

<span data-ttu-id="4d9e3-113">Salvar Olá JSON definido no hello [H264 várias taxas de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tópico em algum arquivo com extensão. JSON.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-113">Save hello JSON defined in hello [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="4d9e3-114">Por exemplo, **CustomPreset_JSON.json**.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="4d9e3-115">Predefinição personalizada</span><span class="sxs-lookup"><span data-stu-id="4d9e3-115">Customized preset</span></span>

<span data-ttu-id="4d9e3-116">Olá abrir **CustomPreset_JSON.json** de arquivo e remover as três primeiras camadas de **H264Layers** para o arquivo tem esta aparência.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-116">Open hello **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
    

## <span data-ttu-id="4d9e3-117"><a id="encoding_with_dotnet"></a>Codificação com o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4d9e3-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="4d9e3-118">saudação de exemplo de código a seguir usa saudação do SDK do Media Services .NET tooperform tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d9e3-118">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="4d9e3-119">Crie um trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-119">Create an encoding job.</span></span>
- <span data-ttu-id="4d9e3-120">Obtém um codificador de mídia codificador padrão de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-120">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="4d9e3-121">Carregar Olá que JSON personalizado predefinidos que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-121">Load hello custom JSON preset that you created in hello previous section.</span></span> 
  
        // Load hello JSON from hello local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="4d9e3-122">Adicione um trabalho toohello codificação.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-122">Add an encoding task toohello job.</span></span> 
- <span data-ttu-id="4d9e3-123">Especifique a entrada hello toobe ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-123">Specify hello input asset toobe encoded.</span></span>
- <span data-ttu-id="4d9e3-124">Crie um ativo de saída que conterá o ativo de saudação codificado.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-124">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="4d9e3-125">Adicione o andamento do trabalho um evento manipulador toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-125">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="4d9e3-126">Envie trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d9e3-126">Submit hello job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4d9e3-127">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d9e3-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4d9e3-128">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4d9e3-128">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4d9e3-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4d9e3-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using custom presets.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4d9e3-130">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4d9e3-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4d9e3-131">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4d9e3-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4d9e3-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4d9e3-132">See Also</span></span>
[<span data-ttu-id="4d9e3-133">Visão geral da codificação de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="4d9e3-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

