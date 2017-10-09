---
title: "aaaFilters e manifestos dinâmicos | Microsoft Docs"
description: "Este tópico descreve como os filtros de toocreate para que seu cliente pode usá-los toostream a seções específicas de um fluxo. Serviços de mídia cria manifestos dinâmico tooarchive este fluxo seletivo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Filtros e manifestos dinâmicos
A partir da versão 2.11, serviços de mídia permitem toodefine filtros para os ativos. Esses filtros são regras de servidor que permitirá que os clientes toochoose toodo coisas como: reprodução apenas uma seção de um vídeo (em vez de execução Olá vídeo inteiro), ou especifique apenas um subconjunto de representações de áudio e vídeo que o dispositivo do cliente pode manipular ( em vez de todas as representações de saudação que estão associados com o ativo de saudação). A filtragem de seus ativos é arquivada por meio de **manifesto dinâmico**s serão criados após o toostream de solicitação do cliente, um vídeo com base no filtro (s) especificado.

Este tópico discute os cenários comuns nos quais usando filtros seria muito útil tooyour tootopics clientes e links que demonstram como toocreate filtros programaticamente (no momento, você pode criar filtros com APIs REST somente).

## <a name="overview"></a>Visão geral
Durante a entrega seu conteúdo toocustomers (fluxo de eventos em tempo real ou vídeo sob demanda) de sua meta é toodeliver dispositivos de vídeo toovarious de alta qualidade em condições de rede diferente. tooachieve essa meta Olá a seguir:

* codificar seu fluxo toomulti taxas de bits ([taxa de bits adaptável](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) (Isso será responsável por condições de rede e qualidade) do fluxo de vídeo e 
* usar os serviços de mídia [empacotamento dinâmico](media-services-dynamic-packaging-overview.md) toodynamically empacotar novamente seu fluxo em protocolos diferentes (Isso será responsável por streaming em diferentes dispositivos). Serviços de mídia oferece suporte à entrega de saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH. 

### <a name="manifest-files"></a>Arquivos de manifesto
Quando você codifica um ativo para streaming de taxa de bits adaptável, um **manifesto** arquivo (lista de reprodução) é criado (arquivo hello é baseado em XML ou texto). Olá **manifesto** inclui metadados de streaming, como: tipo (áudio, vídeo ou texto) de acompanhar, acompanhar o nome, hora de início e término, taxa de bits (qualidades), idiomas de faixa, a janela de apresentação (a janela deslizante de duração fixa), vídeo codec (FourCC). Também instrui fragmento próximo do Olá Olá player tooretrieve fornecendo informações sobre Olá Avançar executável fragmentos de vídeo disponíveis e sua localização. Fragmentos (ou segmentos) são Olá real "partes" de um conteúdo de vídeo.

Aqui está um exemplo desse arquivo de manifesto: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Manifestos dinâmicos
Há [cenários](media-services-dynamic-manifest-overview.md#scenarios) quando o cliente precisa de mais flexibilidade do que o que é descrito no arquivo de manifesto de saudação padrão ativo. Por exemplo:

* Dispositivo específico: entregar somente Olá especificado e/ou de representações especificado faixas de idioma com suporte pelo dispositivo Olá tooplayback usado hello ("representação de filtragem de conteúdo"). 
* Reduza Olá manifesto tooshow um subclipe de um evento ao vivo ("subclipe filtragem").
* Início de corte Olá de um vídeo ("cortar um vídeo").
* Ajuste a janela de apresentação (DVR) na ordem tooprovide um comprimento limitado da janela DVR Olá no player de saudação ("ajustar apresentação janela").

tooachieve essa flexibilidade, ofertas de serviços de mídia **manifestos dinâmico** com base em predefinido [filtros](media-services-dynamic-manifest-overview.md#filters).  Depois de definir filtros Olá, seus clientes podem usá-los toostream uma representação específica ou sub clipes do vídeo. Eles pode especificar filtros no hello URL de streaming. Filtros podem ser a taxa de bits de tooadaptive aplicada protocolos com suporte de streaming [empacotamento dinâmico](media-services-dynamic-packaging-overview.md): Smooth Streaming, MPEG-DASH e HLS. Por exemplo:

URL de MPEG DASH com filtro

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

URL de Smooth Streaming com filtro

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Para obter mais informações sobre como toodeliver o conteúdo e a compilação streaming URLs, consulte [fornecendo visão geral do conteúdo](media-services-deliver-content-overview.md).

> [!NOTE]
> Observe que manifestos dinâmico não alterar ativo hello e Olá manifesto padrão para esse ativo. O cliente pode escolher toorequest um fluxo com ou sem filtros. 
> 
> 

### <a id="filters"></a>Filtros
Há dois tipos de filtros de ativo: 

* Filtros globais (pode ser ativo tooany aplicado em Olá conta do Azure Media Services, tem um tempo de vida da conta de saudação) e 
* Filtros locais (pode ser apenas ativo tooan aplicada com quais Olá filtro foi associado no momento da criação, têm um tempo de vida do ativo de saudação). 

Tipos de filtros globais e locais têm exatamente Olá as mesmas propriedades. Olá principal diferença entre Olá dois é para os cenários que tipo de um servidor de dados é mais adequado. Filtros globais são geralmente adequados para perfis de dispositivo (filtragem de representação) onde filtros locais podem ser usado tootrim um ativo específico.

## <a id="scenarios"></a>Cenários comuns
Como foi mencionado antes, quando entregar seu conteúdo toocustomers (fluxo de eventos em tempo real ou vídeo sob demanda) sua meta é toodeliver um vídeo de alta qualidade toovarious dispositivos em diferentes condições de rede. Além disso, você pode ter outros requisitos que envolvem a filtragem dos ativos e uso de **manifestos dinâmicos**. Olá seções a seguir oferecem uma breve visão geral dos diferentes cenários de filtragem.

* Especifique somente um subconjunto de representações de áudio e vídeo que podem controlar determinados dispositivos (em vez de todas as representações de saudação que estão associadas a ativos de saudação). 
* Reproduzindo apenas uma seção de um vídeo (em vez da saudação reproduzindo vídeo inteiro).
* Ajuste da janela de apresentação de DVR.

## <a name="rendition-filtering"></a>Filtragem de representação
Você pode escolher tooencode os perfis de codificação do toomultiple ativo (linha de base de h. 264, h. 264 alto, AACL, AACH, Dolby Digital Plus) e várias taxas de bits de qualidade. No entanto, nem todos os dispositivos de cliente oferecerão suporte a todos os seus perfis e taxas de bits de todos os seus ativos. Por exemplo, os dispositivos Android antigos oferecem suporte apenas da H.264 linha de base+ AACL. Dispositivo de tooa taxas de bits mais alto que não é possível obter benefícios de saudação de envio, desperdiça o cálculo de largura de banda e o dispositivo. Esse dispositivo deve decodificar todos hello fornecido informações, apenas tooscale-para baixo para exibição.

Com o manifesto dinâmico, você pode criar perfis de dispositivo como móvel, console, HD/SD, etc. e incluir faixas hello e qualidades que você deseja toobe uma parte de cada perfil.

![Exemplo de filtragem de representação][renditions2]

Olá exemplo a seguir, um codificador era usado tooencode um ativo de mezanino em sete representações de vídeo de MP4s de ISO (de 180p too1080p). Olá ativo codificado pode ser dinamicamente empacotado em qualquer um dos seguintes protocolos de transmissão de saudação: MPEG DASH, HLS e Smooth.  Na parte superior de saudação do diagrama hello, Olá HLS manifesto para ativo Olá sem filtros é mostrado (ele contém todas as representações de sete).  Olá inferior esquerda, Olá que HLS manifesto toowhich foi aplicado um filtro chamado "ott" é mostrado. filtro de "ott" Hello Especifica tooremove todas as taxas de bits abaixo de 1 Mbps, resultando na Olá inferior dois níveis de qualidade que estão sendo removidos na resposta de saudação.  Olá parte inferior direita, Olá HLS toowhich manifesto foi aplicado um filtro chamado "móvel" é mostrado. filtro "móvel" Hello Especifica representações tooremove onde hello resolução é maior do que 720p, resultando na Olá duas 1080p reproduções sendo removidas.

![Filtragem de representação][renditions1]

## <a name="removing-language-tracks"></a>Remover faixas de idiomas
Os ativos podem incluir vários idiomas de áudio, como inglês, espanhol, francês etc. Geralmente, gerenciadores de Player SDK saudação padrão de seleção de faixa de áudio e controla o áudio disponível por seleção de usuário. É muito difícil toodevelop tais SDKs do Player, é necessário implementações diferentes em estruturas de player específico do dispositivo. Além disso, em algumas plataformas, APIs de Player são limitados e não incluem o recurso de seleção de áudio em que os usuários não podem selecionar ou alterar a faixa de áudio saudação padrão. Com filtros de ativos, você pode controlar o comportamento de saudação Criando filtros que incluem apenas os idiomas de áudio desejados.

![Filtragem das faixas de idioma][language_filter]

## <a name="trimming-start-of-an-asset"></a>Corte do início de um ativo
Na maioria dos eventos de transmissão ao vivo, operadores executar alguns testes antes do evento real hello. Por exemplo, elas podem incluir um Tablet assim antes do início de saudação do evento Olá: "O programa será iniciado momentaneamente". Se o arquivamento de programa hello, teste Olá slate dados também são arquivados e serão incluídos na apresentação de saudação. No entanto, essas informações não devem ser mostradas toohello clientes. Com o manifesto dinâmico, você pode criar um filtro de hora de início e remover dados indesejado de saudação do manifesto de saudação.

![Corte do início][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Criar subclipes (exibições) de um arquivo ao vivo
Muitos eventos ao vivo são de longa duração e o arquivamento dinâmico pode incluir vários eventos. Depois que as emissoras termina de evento ao vivo Olá seja toobreak backup Olá live arquivamento no início do programa lógico e parar sequências. Em seguida, publica esses programas virtuais separadamente sem post processar arquivo dinâmico Olá e não criar ativos separados (que não obterá o benefício de fragmentos de cache existente Olá no hello CDNs). Exemplos desses programas virtual (sub clipes) são Olá trimestres de um futebol ou jogo basquete innings Olá em bola ou eventos individuais de uma tarde programa Olimpíadas.

Com o manifesto dinâmico, você pode criar filtros usando os horários de início/término e criar modos de exibição virtuais pela parte superior de saudação do seu arquivo em tempo real. 

![Filtro de subclipe][subclip_filter]

Ativos filtrados:

![Esqui][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Ajuste da janela de apresentação (DVR)
Atualmente, os serviços de mídia do Azure oferece arquivamento circular onde duração Olá pode ser configurada entre 5 minutos - 25 horas. Manifesto de filtragem pode ser usado toocreate uma janela DVR sem interrupção pela parte superior de saudação do arquivo hello, sem excluir a mídia. Há muitos cenários em que deseja que as emissoras tooprovide uma janela DVR limitada que move com hello live borda e a saudação mesmo tempo manter uma janela maior de arquivamento. Uma emissora pode toouse Olá dados fora do clipes de toohighlight Olá DVR janela, ou he\she talvez queira tooprovide janelas DVR diferentes para diferentes dispositivos. Por exemplo, a maioria dos dispositivos móveis Olá não lidar com grande windows DVR (você pode ter uma janela DVR de 2 minutos para dispositivos móveis e 1 hora para os clientes de desktop).

![Janela DVR][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Ajustar o LiveBackoff (posição ao vivo)
Manifesto a filtragem pode ser usado tooremove vários segundos da borda de saudação ao vivo de um programa ao vivo. Isso permite que as emissoras apresentação de saudação toowatch na publicação de visualização Olá aponte e criar anúncio pontos de inserção antes de visualizadores de saudação recebam o fluxo de saudação (geralmente feito-off por 30 segundos). As emissoras podem enviar essas estruturas de cliente tootheir anúncios no tempo para que eles tooreceived e processo de informações de saudação antes de oportunidade de anúncio hello.

Além de dar suporte a toohello anúncio, LiveBackoff pode ser usado para ajustar a posição de download ao vivo do cliente para que quando os clientes descompasso e ocorrências borda dinâmico Olá ainda pode obter fragmentos do servidor em vez de obter erros HTTP 404 ou 412.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Combinar várias regras em um único filtro
É possível combinar várias regras de filtragem em um único filtro. Por exemplo, você pode definir um Tablet de tooremove de regra de intervalo de um arquivo em tempo real e também filtrar taxas de bits disponíveis. Para vários final de saudação regras filtragem o resultado é composição hello (interseção) dessas regras.

![várias regras][multiple-rules]

## <a name="create-filters-programmatically"></a>Criar filtros por meio de programa
Olá tópico a seguir discute entidades de serviços de mídia que são toofilters relacionados. tópico de saudação também mostra como tooprogrammatically criar filtros.  

[Criar filtros com APIs REST](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Combinando vários filtros (composição de filtros)
Você também pode combinar vários filtros em uma única URL. 

Olá cenário a seguir demonstra por que você desejaria toocombine filtros:

1. É necessário toofilter suas qualidades de vídeos para dispositivos móveis, como Android ou iPAD (em qualidades de vídeo de toolimit de ordem). tooremove Olá qualidades indesejadas, você deve criar um filtro global que é adequado para perfis de dispositivo. Conforme mencionado acima, os filtros globais podem ser usados para todos os seus ativos em Olá conta sem qualquer outra associação de serviços a mesma mídia. 
2. Você também mudar tootrim Olá início e fim da hora de um ativo. tooachieve isso, crie um filtro de local e definir a hora de início/término hello. 
3. Você deseja toocombine desses filtros (sem combinação seria necessário tooadd qualidade filtragem toohello corte filtro que faz uso de filtro de difícil).

toocombine filtros, você precisa tooset Olá filtro nomes toohello manifesto/lista de reprodução de URL com delimitada por ponto e vírgula. Vamos supor que você tenha um filtro nomeado *MyMobileDevice* que filtra qualidades e você tiver outro chamado *MyStartTime* tooset uma determinada hora de início. Você pode combiná-los assim:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

Você pode combinar os filtros de too3. 

Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.

## <a name="know-issues-and-limitations"></a>Conheça os problemas e limitações
* Manifesto dinâmico opera nos limites do GOP (quadros chave) e, como consequência, o corte tem precisão de GOP. 
* É possível usar o mesmo nome de filtro para os filtros globais e locais. Observe que o filtro local têm maior precedência e substituem os filtros globais.
* Se você atualizar um filtro, pode demorar até minutos too2 para regras de saudação do toorefresh de ponto de extremidade de streaming. Se Olá conteúdo foi servido usando alguns filtros (e armazenado em cache na CDN e proxies caches), esses filtros de atualização pode resultar em falhas de player. É recomendável cache de saudação tooclear depois de atualizar o filtro de saudação. Se essa opção não for possível, considere usar um filtro diferente.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Entregando conteúdo tooCustomers visão geral](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
