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
# <a name="publish-azure-media-services-content-using-net"></a>Publicar o conteúdo dos Serviços de Mídia do Azure usando o .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>Visão geral
Você pode transmitir um conjunto de MP4 com taxa de bits adaptável ao criar um localizador de streaming sob demanda e criar uma URL de transmissão. Olá [codificar um ativo](media-services-encode-asset.md) tópico mostra como definir tooencode em uma taxa de bits adaptável MP4. 

> [!NOTE]
> Se o seu conteúdo for criptografado, configure a política de entrega de ativos (conforme descrito [neste](media-services-dotnet-configure-asset-delivery-policy.md) tópico) antes de criar um localizador. 
> 
> 

Você também pode usar um OnDemand localizador toobuild URLs que arquivos tooMP4 ponto que podem ser baixado progressivamente de streaming.  

Este tópico mostra como toocreate um OnDemand toopublish localizador de streaming seu ativo e construir um Smooth, MPEG DASH e HLS URLs de streaming. Ele também mostra toobuild hot URLs de download progressivo. 

## <a name="create-an-ondemand-streaming-locator"></a>Criar um localizador de streaming sob demanda
toocreate Olá OnDemand localizador de streaming e obter URLs, você precisa toodo Olá coisas a seguir:

1. Se o conteúdo de saudação é criptografado, defina uma política de acesso.
2. Criar um localizador de streaming sob demanda.
3. Se você planejar toostream, obter Olá streaming de arquivo de manifesto (. ISM) em ativo hello. 
   
   Se você planejar tooprogressively download, obter nomes de saudação de arquivos MP4 no ativo de saudação.  
4. Crie arquivo de manifesto de toohello URLs ou arquivos MP4. 


>[!NOTE]
>Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Use Olá a mesma ID de política se você estiver usando sempre Olá mesmo dias / permissões de acesso. Por exemplo, políticas de localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

### <a name="use-media-services-net-sdk"></a>Usar o SDK do .NET dos Serviços de Mídia
Criar URLs de streaming 

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

Olá saídas:

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> Você também pode transmitir seu conteúdo por uma conexão SSL. toodo essa abordagem, verifique se suas URLs de streaming começam com HTTPS. Atualmente, o AMS não dá suporte ao SSL com domínios personalizados.
> 
> 

Crie URLs de download progressivo 

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

Olá saídas:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Usam o SDK do .NET dos Serviços de Mídia
Olá código a seguir chama métodos de extensões do SDK do .NET que criar um localizador e geram Olá Smooth Streaming, HLS e MPEG-DASH URLs de streaming adaptável.

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


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Próximas etapas
* [Baixar ativos](media-services-deliver-asset-download.md)
* [Configurar política de entrega de ativos](media-services-dotnet-configure-asset-delivery-policy.md)

