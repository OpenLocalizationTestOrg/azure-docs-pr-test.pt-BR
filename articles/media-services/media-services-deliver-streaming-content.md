---
title: "conteúdo do Azure Media Services aaaPublish usando .NET | Microsoft Docs"
description: "Saiba como toocreate um localizador que é usado toobuild uma URL de streaming. Exemplos de código são escritos em c# e usam Olá SDK do Media Services para .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="93920-104">Publicar o conteúdo dos Serviços de Mídia do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="93920-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93920-105">REST</span><span class="sxs-lookup"><span data-stu-id="93920-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="93920-106">.NET</span><span class="sxs-lookup"><span data-stu-id="93920-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="93920-107">Portal</span><span class="sxs-lookup"><span data-stu-id="93920-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="93920-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="93920-108">Overview</span></span>
<span data-ttu-id="93920-109">Você pode transmitir um conjunto de MP4 com taxa de bits adaptável ao criar um localizador de streaming sob demanda e criar uma URL de transmissão.</span><span class="sxs-lookup"><span data-stu-id="93920-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="93920-110">Olá [codificar um ativo](media-services-encode-asset.md) tópico mostra como definir tooencode em uma taxa de bits adaptável MP4.</span><span class="sxs-lookup"><span data-stu-id="93920-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="93920-111">Se o seu conteúdo for criptografado, configure a política de entrega de ativos (conforme descrito [neste](media-services-dotnet-configure-asset-delivery-policy.md) tópico) antes de criar um localizador.</span><span class="sxs-lookup"><span data-stu-id="93920-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="93920-112">Você também pode usar um OnDemand localizador toobuild URLs que arquivos tooMP4 ponto que podem ser baixado progressivamente de streaming.</span><span class="sxs-lookup"><span data-stu-id="93920-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="93920-113">Este tópico mostra como toocreate um OnDemand toopublish localizador de streaming seu ativo e construir um Smooth, MPEG DASH e HLS URLs de streaming.</span><span class="sxs-lookup"><span data-stu-id="93920-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="93920-114">Ele também mostra toobuild hot URLs de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="93920-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="93920-115">Criar um localizador de streaming sob demanda</span><span class="sxs-lookup"><span data-stu-id="93920-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="93920-116">toocreate Olá OnDemand localizador de streaming e obter URLs, você precisa toodo Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="93920-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="93920-117">Se o conteúdo de saudação é criptografado, defina uma política de acesso.</span><span class="sxs-lookup"><span data-stu-id="93920-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="93920-118">Criar um localizador de streaming sob demanda.</span><span class="sxs-lookup"><span data-stu-id="93920-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="93920-119">Se você planejar toostream, obter Olá streaming de arquivo de manifesto (. ISM) em ativo hello.</span><span class="sxs-lookup"><span data-stu-id="93920-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="93920-120">Se você planejar tooprogressively download, obter nomes de saudação de arquivos MP4 no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="93920-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="93920-121">Crie arquivo de manifesto de toohello URLs ou arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="93920-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="93920-122">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="93920-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="93920-123">Use Olá a mesma ID de política se você estiver usando sempre Olá mesmo dias / permissões de acesso.</span><span class="sxs-lookup"><span data-stu-id="93920-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="93920-124">Por exemplo, políticas de localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="93920-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="93920-125">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="93920-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="93920-126">Usar o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="93920-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="93920-127">Criar URLs de streaming</span><span class="sxs-lookup"><span data-stu-id="93920-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="93920-128">Olá saídas:</span><span class="sxs-lookup"><span data-stu-id="93920-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="93920-129">Você também pode transmitir seu conteúdo por uma conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="93920-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="93920-130">toodo essa abordagem, verifique se suas URLs de streaming começam com HTTPS.</span><span class="sxs-lookup"><span data-stu-id="93920-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="93920-131">Atualmente, o AMS não dá suporte ao SSL com domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="93920-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="93920-132">Crie URLs de download progressivo</span><span class="sxs-lookup"><span data-stu-id="93920-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="93920-133">Olá saídas:</span><span class="sxs-lookup"><span data-stu-id="93920-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="93920-134">Usam o SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="93920-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="93920-135">Olá código a seguir chama métodos de extensões do SDK do .NET que criar um localizador e geram Olá Smooth Streaming, HLS e MPEG-DASH URLs de streaming adaptável.</span><span class="sxs-lookup"><span data-stu-id="93920-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="93920-136">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="93920-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93920-137">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="93920-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="93920-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93920-138">Next steps</span></span>
* [<span data-ttu-id="93920-139">Baixar ativos</span><span class="sxs-lookup"><span data-stu-id="93920-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="93920-140">Configurar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="93920-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

