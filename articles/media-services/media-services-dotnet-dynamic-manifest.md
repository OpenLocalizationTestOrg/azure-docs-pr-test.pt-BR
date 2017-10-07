---
title: Filtros de aaaCreating com o SDK do Azure Media Services .NET
description: "Este tópico descreve como os filtros de toocreate para que seu cliente pode usá-los toostream a seções específicas de um fluxo. Serviços de mídia cria manifestos dinâmico tooachieve este fluxo seletivo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Criando filtros com o SDK do .NET dos Serviços de Mídia do Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

A partir da versão 2.11, serviços de mídia permitem toodefine filtros para os ativos. Esses filtros são regras de servidor que permitirá que os clientes toochoose toodo coisas como: reprodução apenas uma seção de um vídeo (em vez de execução Olá vídeo inteiro), ou especifique apenas um subconjunto de representações de áudio e vídeo que o dispositivo do cliente pode manipular ( em vez de todas as representações de saudação que estão associados com o ativo de saudação). A filtragem de seus ativos é obtida por meio de **manifesto dinâmico**s serão criados após o toostream de solicitação do cliente, um vídeo com base no filtro (s) especificado.

Para obter mais informações relacionadas toofilters e manifesto dinâmico, consulte [dinâmico manifestos de visão geral do](media-services-dynamic-manifest-overview.md).

Este tópico mostra como toouse toocreate do SDK do Media Services .NET, atualizar e excluir filtros. 

Observe que se você atualizar um filtro, pode demorar até minutos too2 para regras de saudação do toorefresh de ponto de extremidade de streaming. Se conteúdo Olá foi servido usando esse filtro (e armazenado em cache na CDN e proxies caches), esse filtro a atualização pode resultar em falhas de player. É recomendável cache de saudação tooclear depois de atualizar o filtro de saudação. Se essa opção não for possível, considere usar um filtro diferente. 

## <a name="types-used-toocreate-filters"></a>Tipos usados filtros toocreate
tipos seguintes Hello são usados durante a criação de filtros: 

* **IStreamingFilter**.  Esse tipo é baseado na Olá API REST a seguir [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Esse tipo é baseado na Olá API REST a seguir [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Esse tipo é baseado na Olá API REST a seguir [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**. Esses tipos são baseados em Olá seguintes APIs REST [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Criar/atualizar/ler/excluir os filtros globais
Olá código a seguir mostra como toouse .NET toocreate, atualizar, ler e excluir filtros de ativo.

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a>Criar/atualizar/ler/excluir os filtros de ativo
Olá código a seguir mostra como toouse .NET toocreate, atualizar, ler e excluir filtros de ativo.

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a>Criar URLs de streaming que usam filtros
Para obter informações sobre como toopublish e oferecer seus ativos, consulte [visão geral de entrega de conteúdo tooCustomers](media-services-deliver-content-overview.md).

Olá exemplos a seguir mostram como os filtros de tooadd tooyour URLs de streaming.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Streaming Suave**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Visão geral de manifestos dinâmicos](media-services-dynamic-manifest-overview.md)

