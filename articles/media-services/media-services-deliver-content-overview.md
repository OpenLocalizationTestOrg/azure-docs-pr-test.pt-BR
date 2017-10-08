---
title: "toocustomers conteúdo aaaDelivering | Microsoft Docs"
description: "Este tópico fornece uma visão geral do que está envolvido no fornecimento de conteúdo com os Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Entregar conteúdo toocustomers
Quando você está oferecendo seu toocustomers conteúdo de streaming ou vídeo sob demanda, sua meta é toodeliver toovarious de vídeo de alta qualidade dispositivos sob condições de rede diferente.

tooachieve essa meta, você pode:

* Codifica o fluxo de vídeo de taxa de bits múltipla (taxa de bits adaptável) do fluxo tooa. Isso cuidará da qualidade e das condições de rede.
* Usar serviços de mídia do Microsoft Azure [empacotamento dinâmico](media-services-dynamic-packaging-overview.md) toodynamically empacotar novamente seu fluxo em protocolos diferentes. Isso se encarregará da transmissão em diferentes dispositivos. Serviços de mídia oferece suporte à entrega de saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming e MPEG-DASH.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

Este artigo apresenta uma visão geral de conceitos importantes de distribuição de conteúdo.

toocheck problemas conhecidos, consulte [problemas conhecidos](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>Empacotamento dinâmico
Com o empacotamento dinâmico Olá que Media Services fornece, que você pode distribuir o conteúdo de taxa de bits adaptável MP4 ou Smooth Streaming codificados em formatos suportados pelo Media Services (MPEG-DASH, HLS, Smooth Streaming) de fluxo contínuo sem ter que toore-pacote Esses formatos de streaming. É recomendável distribuir conteúdo com empacotamento dinâmico.

tootake proveito do empacotamento dinâmico, você precisará de tooencode seu arquivo de mezanino (origem) em um conjunto de arquivos MP4 com taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.

Com o empacotamento dinâmico, você pode armazenar e paga pelos arquivos Olá no formato de armazenamento único. Serviços de mídia criará e enviará a resposta apropriada hello, com base em suas solicitações.

O empacotamento dinâmico está disponível para pontos de extremidade de streaming Standard e Premium. 

Para saber mais, confira [Empacotamento dinâmico](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Filtros e manifestos dinâmicos
Você pode definir filtros para seus ativos com os Serviços de Mídia. Esses filtros são regras de servidor que ajudar seus clientes a fazer coisas como reproduzir uma seção específica de um vídeo ou especificar um subconjunto de representações de áudio e vídeo que pode lidar com o dispositivo do cliente (em vez de todas as representações de saudação que estão associadas com ativo Olá ). A filtragem é obtida por meio de *manifestos dinâmicos* que são criados quando o cliente solicita toostream um vídeo com base em um ou mais especificados filtros.

Para obter mais informações, consulte [Filtros e manifestos dinâmicos](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Localizadores
tooprovide o usuário com uma URL que pode ser usado toostream ou baixar o conteúdo, é necessário primeiro toopublish seu ativo, criando um localizador. Um localizador fornece uma saudação tooaccess de ponto de entrada arquivos contidos em um ativo. Os Serviços de Mídia oferecem suporte a dois tipos de localizadores:

* Localizadores OnDemandOrigin. Eles são usados toostream mídia (por exemplo, MPEG-DASH, HLS ou Smooth Streaming) ou download progressivo de arquivos.
* Localizadores de URL por SAS (Assinatura de Acesso Compartilhado). Esses são usados toodownload mídia arquivos tooyour local computador.

Um *política de acesso* é usado toodefine permissões hello (como leitura, gravação e lista) e a duração para o qual um cliente tem acesso para um determinado ativo. Observe que a permissão de lista de saudação (Accesspermissions) não deve ser usado na criação de um localizador Ondemandorigin.

Os localizadores têm datas de validade. Olá portal do Azure define uma data de expiração 100 anos em Olá futura para os localizadores.

> [!NOTE]
> Se você usou os localizadores do hello toocreate portal do Azure antes de março de 2015, os localizadores foram definidos tooexpire depois de dois anos.
> 
> 

tooupdate uma data de expiração em um localizador, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs. Observe que quando você atualizar a data de expiração de saudação de um localizador SAS, Olá URL é alterado.

Os localizadores não são projetados toomanage o controle de acesso por usuário. Você pode conceder acesso de diferente usuários tooindividual de direitos usando soluções de gerenciamento de direitos digitais (DRM). Para obter mais informações, consulte [Protegendo mídia](http://msdn.microsoft.com/library/azure/dn282272.aspx).

Quando você cria um localizador, pode haver um atraso de 30 segundos devido a processos de armazenamento e a propagação de toorequired no armazenamento do Azure.

## <a name="adaptive-streaming"></a>Streaming adaptável
Tecnologias de taxa de bits adaptável permitem que os aplicativos de player de vídeo toodetermine condições da rede e selecionem várias taxas de bits. Ao diminuir a comunicação de rede, o cliente de saudação pode selecionar uma taxa de bits mais baixa para que reprodução possa continuar com a qualidade de vídeo inferior. Como melhorarem a condições da rede, o cliente de Olá pode alternar tooa maior taxa de bits com melhor qualidade de vídeo. Serviços de mídia do Azure oferece suporte a saudação seguintes tecnologias de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming e MPEG-DASH.

usuários de tooprovide com URLs de streaming, você primeiro deve criar um localizador OnDemandOrigin. Toostream criando Olá fornece localizador Olá ativo de toohello caminho base que contém o conteúdo de saudação desejado. No entanto, toostream capaz de toobe esse conteúdo, você precisa toomodify esse caminho ainda mais. tooconstruct um toohello URL completa, o arquivo de manifesto de streaming, você deverá concatenar o caminho do localizador de saudação do valor e hello (filename.ism) o nome do arquivo de manifesto. Em seguida, anexe **/manifesto** e um caminho de localizador de toohello formato apropriado (se necessário).

> [!NOTE]
> Você também pode transmitir seu conteúdo por uma conexão SSL. toodo isso, verifique se suas URLs de streaming começam com HTTPS. Observe que, atualmente, o AMS não dá suporte ao SSL com domínios personalizados.  
> 


Só é possível transmitir sobre SSL se saudação do qual você distribuir o conteúdo do ponto de extremidade de streaming foi criada após 10 de setembro de 2014. Se suas URLs de streaming se basearem na Olá criados após 10 de setembro de 2014, os pontos de extremidade de streaming Olá URL contém "streaming.mediaservices.windows.net". As URLs de streaming que contêm "origin.mediaservices.windows.net" (formato antigo do hello) não dão suporte a SSL. Se a URL estiver no formato antigo hello e desejar toostream capaz de toobe sobre SSL, crie um novo ponto de extremidade de streaming. Use URLs com base em Olá novo streaming toostream de ponto de extremidade seu conteúdo sobre SSL.

## <a name="streaming-url-formats"></a>Formatos de URL de streaming
### <a name="mpeg-dash-format"></a>Formato MPEG-DASH
{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Formato Apple HTTP Live Streaming (HLS) V4
{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Formato Apple HTTP Live Streaming (HLS) V3
{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Formato HLS (Apple HTTP Live Streaming) com filtro somente áudio
Por padrão, as faixas de áudio são incluídas no manifesto de HLS de saudação. Isso é necessário na certificação da Apple Store para redes de celular. Nesse caso, se um cliente não tem suficiente largura de banda ou se estiver conectado por uma conexão 2G, reprodução alterna somente tooaudio. Isso ajuda a tookeep conteúdo de streaming sem buffer, mas não há nenhum vídeo. Em alguns cenários, o buffer do player pode ser preferível a somente áudio. Se você quiser acompanhar de somente de áudio Olá tooremove, adicionar **somente de áudio = false** toohello URL.

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

Para saber mais, confira [Dynamic Manifest Composition support and HLS output additional features (Suporte à Composição de Manifesto Dinâmico e recursos adicionais da saída de HLS)](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).

### <a name="smooth-streaming-format"></a>Formato Smooth Streaming
{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest

Exemplo:

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>Manifesto do Smooth Streaming 2.0 (manifesto herdado)
Por padrão, o formato do manifesto Smooth Streaming contém marca de repetição de saudação (r-tag). No entanto, alguns players não dão suporte a saudação r-tag. Os clientes com essas players podem usar um formato que desabilita Olá r-tag:

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Download progressivo
Com o download progressivo, você pode iniciar a reprodução de mídia antes do download do arquivo inteiro hello. Você não pode baixar progressivamente arquivos .ism* (ismv, isma, ismt ou ismc).

tooprogressively baixar conteúdo, use o tipo de OnDemandOrigin de saudação do localizador. Olá, exemplo a seguir mostra Olá URL com base no hello OnDemandOrigin tipo de localizador:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

Você deve descriptografar qualquer ativos criptografados de armazenamento que você deseja toostream do serviço de origem Olá para download progressivo.

## <a name="download"></a>Baixar
toodownload seu dispositivo de cliente tooa conteúdo, você deve criar um localizador SAS. Olá SAS localizador oferece a você acesso toohello contêiner de armazenamento do Azure onde o arquivo está localizado. URL de download do toobuild hello, você tem nome de arquivo hello tooembed entre o host de saudação e a assinatura SAS.

Olá, exemplo a seguir mostra Olá URL com base no localizador SAS hello:

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

Olá considerações a seguir se aplicam:

* Você deve descriptografar qualquer ativos criptografados de armazenamento que você deseja toostream do serviço de origem Olá para download progressivo.
* Um download que não foi concluído em 12 horas, falhará.

## <a name="streaming-endpoints"></a>Pontos de extremidade de streaming

Um ponto de extremidade de streaming representa um serviço de streaming que pode entregar conteúdo diretamente a mais de tooa cliente player aplicativo ou tooa fornecimento de conteúdo CDN (rede) para distribuição. fluxo de saída de saudação de um serviço de ponto de extremidade de streaming pode ser uma transmissão ao vivo ou um ativo de vídeo sob demanda em sua conta de serviços de mídia. Há dois tipos de ponto de extremidade de streaming, **Standard** e **Premium**. Para saber mais, confira [Streaming endpoints overview](media-services-streaming-endpoints-overview.md) (Visão geral dos pontos de extremidade de streaming).

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

## <a name="known-issues"></a>Problemas conhecidos
### <a name="changes-toosmooth-streaming-manifest-version"></a>Versão do manifesto de Streaming alterações tooSmooth
Antes de saudação versão do serviço de julho de 2016 - o ao manifesto ativos produzidos pelo codificador de mídia padrão, o fluxo de trabalho do Media Encoder Premium ou hello Azure Media Encoder anteriores foram transmitidos usando o empacotamento dinâmico - Olá Smooth Streaming retornado atenderiam tooversion 2.0. Na versão 2.0, durações de fragmento de saudação não usar marcas de repetir os chamados ('r') de saudação. Por exemplo:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

Em Olá versão do serviço de julho de 2016, o manifesto de Smooth Streaming Olá gerado segue tooversion 2.2, com durações de fragmento usando marcas de repetição. Por exemplo:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Alguns dos clientes herdados de Smooth Streaming do hello podem não oferecer suporte a marcas de repetição hello e falharão manifesto de saudação tooload. toomitigate esse problema, você pode usar o parâmetro de formato do manifesto herdado hello **(format = fmp4-v20)** ou atualizar o cliente toohello versão mais recente, que oferece suporte a marcas de repetição. Para obter mais informações, confira [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Tópicos relacionados
[Atualizar localizadores dos Serviços de Mídia depois de implantar chaves de armazenamento](media-services-roll-storage-access-keys.md)

