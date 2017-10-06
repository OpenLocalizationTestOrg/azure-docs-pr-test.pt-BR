---
title: "aaaInserting anúncios no lado do cliente Olá | Microsoft Docs"
description: "Este tópico mostra como tooinsert anúncios Olá do lado do cliente."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Inserção de anúncios no lado do cliente Olá
Este tópico contém informações sobre como tooinsert vários tipos de anúncios no lado do cliente de saudação.

Para obter informações sobre o suporte a legendagem oculta e anúncios em vídeos de transmissão ao vivo, consulte [Padrões de legendagem oculta e inserção de anúncios com suporte](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Atualmente, o Azure Media Player não dá suporte a anúncios.
> 
> 

## <a id="insert_ads_into_media"></a>Inserir anúncios em sua mídia
Serviços de mídia do Azure fornece suporte para inserção de anúncios por meio de saudação plataforma de mídia do Windows: estruturas de Player. As estruturas de player com suporte a anúncios estão disponíveis para dispositivos com Windows 8, Silverlight, Windows Phone 8 e iOS. Cada estrutura de player contém um código de exemplo que mostra como tooimplement um aplicativo de player. Há três tipos diferentes de anúncios, que você pode inserir em sua lista de mídia:.

* **Linear** – completo anúncios de quadro que pausam o vídeo principal hello.
* **Não lineares** – anúncios de sobreposição que são exibidos como reprodução do vídeo principal Olá, geralmente um logotipo ou outra imagem estática colocada no player de saudação.
* **Complementar** – anúncios que são exibidos fora do player hello.

Anúncios podem ser inseridos em qualquer ponto na linha do tempo do vídeo principal hello. Você deve informar o player hello quando tooplay Olá ad e qual tooplay de anúncios. Isso é feito usando um conjunto de arquivos padrão baseados em XML: VAST (Video Ad Service Template), VMAP (Digital Video Multiple Ad Playlist), MAST (Media Abstract Sequencing Template) e VPAID (Digital Video Player Ad Interface Definition). Os arquivos VAST especificam quais toodisplay anúncios. Arquivos VMAP especificam quando tooplay diversos anúncios e contêm XML VAST. Os arquivos MAST são outra anúncios de toosequence de forma que também podem conter XML VAST. Os arquivos VPAID definem uma interface entre o player de vídeo hello e ad hello ou servidor do ad.

Cada estrutura do player funciona de maneira diferente e cada uma será abordada em seu próprio tópico. Este tópico descreverá Olá mecanismos básicos usados tooinsert anúncios. Aplicativos de player de vídeo solicitarem anúncios de um servidor do ad. servidor do ad Olá pode responder de várias maneiras:

* Retornar um arquivo VAST
* Retornar um arquivo VMAP (com VAST incorporado)
* Retornar um arquivo MAST (com VAST incorporado)
* Retornar um arquivo VAST com anúncios VPAID

### <a name="using-a-video-ad-service-template-vast-file"></a>Usando um arquivo (VAST) de modelo do serviço de anúncio de vídeo
Um arquivo VAST Especifica quais anúncios toodisplay. Olá XML a seguir é um exemplo de um arquivo grande para um anúncio linear:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

anúncio linear Olá é descrito por hello <**Linear**> elemento. Especifica a duração de saudação do ad Olá, eventos de rastreamento, clique no, clique em controle e um número de **MediaFile** elementos. Eventos de rastreamento são especificados em hello <**TrackingEvents**> elemento e permitir um tootrack de servidor de ad vários eventos que ocorrem durante a visualização ad hello. Nesse caso, Olá início, ponto médio, conclusão e expanda eventos serão rastreados. Olá início do evento ocorre quando a saudação anúncio é exibido. evento de ponto médio de saudação ocorre quando pelo menos 50% da linha de tempo do ad Olá foi exibida. evento de conclusão de Olá ocorre quando ad Olá ficou toohello final. evento de expansão Olá ocorre quando o usuário Olá expande a tela de toofull hello player de vídeo. Os clickthroughs são especificados com um <**ClickThrough**> elemento dentro de um <**VideoClicks**> elemento e especifica um toodisplay de recurso do URI tooa quando o usuário Olá clica no ad hello. Rastreamento de cliques é especificado em uma <**rastreamento de cliques**> elemento, também em hello <**VideoClicks**> elemento e especifica um recurso de rastreamento para Olá player toorequest quando Olá usuário clica em em Olá ad.hello <**MediaFile**> especificam informações sobre uma codificação específica de um anúncio. Quando há mais de um <**MediaFile**> elemento, o player de vídeo Olá pode escolher Olá melhor codificação para a plataforma de saudação. 

Os anúncios lineares podem ser exibidos na ordem especificada. toodo isso, adicione adicionais <Ad> elementos toohello VAST de arquivo e especificar ordem hello usando o atributo de sequência de saudação. saudação de exemplo a seguir ilustra isso:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

Anúncios não lineares também são especificados em um elemento de <Creative>. Olá mostrado no exemplo a seguir um <Creative> elemento que descreve um anúncio não linear.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


Olá <**NonLinearAds**> elemento pode conter um ou mais <**não lineares**> elementos, cada um deles pode descrever um anúncio não linear. Olá <**não lineares**> elemento Especifica o recurso Olá para o anúncio não linear hello. Olá recurso pode ser um <**StaticResouce**>, um <**IFrameResource**>, ou um <**HTMLResouce**>. <**StaticResource**> descreve um recurso não HTML e define um atributo creativeType que especifica como o recurso de saudação é exibido:

Imagem/gif, imagem/jpeg, imagem/png – o recurso de saudação é exibido em uma marca HTML <**img**> marca.

Aplicativo/x-javascript – recursos de saudação é exibido em um HTML <**script**> marca.

Application/x-shockwave-flash – recursos Olá é exibido em um player Flash.

**IFrameResource** descreve um recurso HTML que pode ser exibido em um IFrame. **HTMLResource** descreve um trecho de código HTML que pode ser inserido em uma página da Web. **TrackingEvents** especificar eventos de rastreamento e Olá URI toorequest quando ocorre o evento de saudação. No hello exemplo eventos acceptInvitation e collapse são rastreados. Para obter mais informações sobre Olá **NonLinearAds** elemento e seus filhos, consulte IAB.NET/VAST. Observe que Olá **TrackingEvents** elemento está localizado em Olá **NonLinearAds** elemento, em vez da saudação **não lineares** elemento.

Anúncios complementares são definidos dentro de um elemento de <CompanionAds>. Olá <CompanionAds> elemento pode conter um ou mais <Companion> elementos. Cada <Companion> elemento descreve um anúncio complementar e pode conter um <StaticResource>, <IFrameResource>, ou <HTMLResource> que são especificados em Olá mesma maneira que um anúncio não linear. Um arquivo grande pode conter diversos anúncios complementares e aplicativo de player hello pode escolher Olá toodisplay de anúncio mais apropriado. Para saber mais sobre VAST, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Usando um arquivo VMAP (Digital Video Multiple Ad Playlist)
Um arquivo VMAP permite que você toospecify quando intervalos de anúncios acontecem, quanto tempo cada quebra é, quantos anúncios podem ser exibidos durante um intervalo e quais tipos de anúncios podem ser exibidos durante um intervalo. Olá a seguir um exemplo de arquivo VMAP que define um único intervalo de anúncio:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Um arquivo VMAP começa com um elemento de <VMAP> que contém um ou mais elementos de <AdBreak>, cada um definindo um intervalo de anúncio. Cada intervalo de anúncio especifica um tipo de intervalo, ID de intervalo e deslocamento de tempo. atributo do Hello breakType Especifica o tipo de saudação de anúncio que pode ser reproduzido durante o intervalo de saudação: linear, não linear ou exibição. Exibir anúncios anúncios complementares de tooVAST do mapa. Mais de um tipo de anúncio pode ser especificado em uma lista separada por vírgulas (sem espaços). Olá breakID é um identificador opcional para o ad hello. Olá timeOffset Especifica quando o anúncio de saudação deve ser exibido. Ele pode ser especificado em uma saudação maneiras a seguir:

1. Tempo – em formato hh:mm:ss ou hh:mm:ss.mmm em que .mmm são milissegundos. valor deste atributo Olá Especifica o tempo de saudação do início de saudação do início de toohello Olá vídeo da linha do tempo de intervalo de anúncio de saudação.
2. Porcentagem – em formato % n onde n é o percentual de saudação do tooplay de vídeo da linha do tempo de saudação antes de reproduzir ad Olá
3. Início/fim – Especifica que um anúncio deve ser exibido antes ou depois de vídeo Olá foram exibido
4. Posição – Especifica a ordem de saudação do ad quebras quando tempo Olá Olá ad quebras de é desconhecido, como na transmissão ao vivo. ordem de saudação de cada intervalo de anúncio é especificada no formato de saudação #n onde n é um inteiro de 1 ou maior. 1 significa Olá anúncio deve ser reproduzido na primeira oportunidade de hello, 2 significa ad Olá deve ser reproduzido na segunda oportunidade de saudação e assim por diante.

Em hello <**AdBreak**> elemento pode ser um <**AdSource**> elemento. Olá <**AdSource**> elemento contém Olá seguintes atributos:

1. ID – Especifica um identificador para a origem do ad Olá
2. allowMultipleAds – um valor booleano que especifica se anúncios múltiplos podem ser exibidos durante o intervalo de anúncio Olá
3. followRedirects – um valor booleano opcional que especifica se o player de vídeo Olá deve usar redirecionamentos dentro de uma resposta de anúncio

Olá <**AdSource**> elemento fornece player Olá uma resposta embutida de anúncio ou uma resposta de anúncio de tooan de referência. Ele pode conter uma saudação elementos a seguir:

* <VASTAdData>indica que uma resposta de anúncio VAST está inserida no arquivo VMAP de saudação
* <AdTagURI> um URI que faz referência a uma resposta de anúncio de outro sistema
* <CustomAdData> -uma cadeia de caracteres arbitrária que representa uma resposta não VAST

Neste exemplo, uma resposta embutida de anúncio é especificada com um elemento <VASTAdData> que contém uma resposta de anúncio VAST. Para obter mais informações sobre Olá outros elementos, consulte [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Olá <**AdBreak**> elemento também pode conter um <**TrackingEvents**> elemento. Olá <**TrackingEvents**> elemento permite iniciar de saudação tootrack ou final de um intervalo de anúncio ou se ocorreu um erro durante o intervalo de anúncio Olá. Olá <**TrackingEvents**> elemento contém um ou mais <**controle**> elementos, cada um deles especifica um evento de rastreamento e um URI de rastreamento. Olá possíveis eventos de rastreamento são:

1. breakStart – rastreia a partir de um intervalo de anúncio Olá
2. breakEnd – acompanhar Olá conclusão de um intervalo de anúncio
3. Error – rastreia um erro que ocorreu durante o intervalo de anúncio Olá

saudação de exemplo a seguir mostra um arquivo VMAP que especifica os eventos de rastreamento

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Para obter mais informações sobre hello <**TrackingEvents**> elemento e seus filhos, consulte http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Usando um arquivo MAST (Media Abstract Sequencing Template)
Um arquivo MAST permite que você toospecify gatilhos que definem quando um anúncio é exibido. a seguir Olá é um arquivo MAST de exemplo que contém acionadores para um anúncio de roll pre, um anúncio Mid-roll e um POST-roll.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



Um arquivo MAST começa com um elemento **MAST** que contém um elemento **triggers**. Olá <triggers> elemento contém um ou mais **gatilho** elementos que definem quando um anúncio deve ser reproduzido. 

Olá **gatilho** elemento contém um **startConditions** elemento que especificam quando um anúncio deve começar tooplay. Olá **startConditions** elemento contém um ou mais <condition> elementos. Quando cada <condition> avalia tootrue um acionador é iniciado ou revogado dependendo se Olá <condition> está dentro de um **startConditions** ou **endConditions** elemento respectivamente. Quando vários <condition> elementos estão presentes, elas são tratadas como um implícito ou, qualquer condição avaliada tootrue fará com que a saudação gatilho tooinitiate. Os elementos <condition> podem ser aninhados. Quando filho <condition> elementos são predefinidos, elas são tratadas como um implícito e, todas as condições devem ser avaliadas tootrue para Olá gatilho tooinitiate. Olá <condition> elemento contém Olá atributos que definem a condição de saudação a seguir: 

1. **tipo** – Especifica o tipo de saudação de condição, evento ou propriedade
2. **nome** – hello nome da saudação toobe propriedade ou evento usado durante a avaliação
3. **valor** – Olá o valor de uma propriedade será avaliada
4. **operador** – Olá toouse operação durante a avaliação: EQ (igual), NEQ (não igual), GTR (maior), GEQ (maior ou igual), LT (menor que), LEQ (menor ou igual), MOD (módulo)

**endConditions** também contêm elementos <condition>. Quando a condição for avaliada gatilho de saudação tootrue é reset.hello <trigger> também contém um <sources> elemento que contém um ou mais <source> elementos. Olá <source> elementos definem resposta de anúncio de toohello Olá URI e o tipo de saudação de resposta de anúncio. Neste exemplo, um URI for fornecido resposta VAST tooa. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Usando a VPAID (Video Player-Ad Interface Definition)
VPAID é uma API para habilitar o anúncio executável unidades toocommunicate com um player de vídeo. Isso permite experiências de anúncios altamente interativos. Olá usuário pode interagir com ad hello e ad Olá pode responder tooactions tomadas pelo Visualizador de saudação. Por exemplo, um anúncio pode exibir botões que permitem Olá usuário tooview obter mais informações ou uma versão mais longa do anúncio de saudação. player de vídeo Olá deve oferecer suporte à saudação API VPAID e anúncio executável Olá deve implementar Olá API. Quando um player solicita um anúncio de um servidor de saudação do servidor ad pode responder com uma resposta VAST que contém um anúncio vpaid.

Um anúncio executável é criado no código que deve ser executado em um ambiente de tempo de execução como Adobe Flash ™ ou JavaScript, que pode ser executado em um navegador da Web. Quando um servidor de anúncios retorna uma resposta VAST que contém um anúncio vpaid, Olá o valor do atributo apiFramework Olá Olá <MediaFile> elemento deve ser "VPAID". Esse atributo especifica que o ad Olá contido é um anúncio vpaid executável. o atributo de tipo Hello deve ser definido toohello tipo MIME da saudação executável, como "application/x-shockwave-flash" ou "application/x-javascript". Olá, trecho XML a seguir mostra Olá <MediaFile> elemento de uma resposta VAST que contém um anúncio vpaid executável. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Um anúncio executável pode ser inicializado usando Olá <AdParameters> elemento dentro do hello <Linear> ou <NonLinear> elementos em uma resposta VAST. Para obter mais informações sobre Olá <AdParameters> elemento, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf). Para obter mais informações sobre Olá API VPAID, consulte [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Implementação de um player no Windows ou Windows Phone 8 com suporte a anúncios
Olá Microsoft Media Platform: estrutura de Player para Windows 8 e Windows Phone 8 contém uma coleção de aplicativos de exemplo que mostram como tooimplement um aplicativo de player de vídeo usando Olá do framework. Você pode baixar exemplos de estrutura de Player e Olá Olá de [estrutura de Player para Windows 8 e Windows Phone 8](https://playerframework.codeplex.com).

Quando você abre Olá Microsoft.PlayerFramework.Xaml.Samples solução, você verá um número de pastas no projeto de saudação. pasta de anúncios Olá contém toocreating relevantes de código de exemplo do hello um player de vídeo com suporte do ad. Interior Olá publicidade pasta é um número de XAML/cs arquivos cada um dos quais mostrar como tooinsert anúncios de maneira diferente. Olá lista a seguir descreve cada:

* AdPodPage.xaml mostra como toodisplay um ad pod.
* AdSchedulingPage.xaml mostra como tooschedule anúncios.
* FreeWheelPage.xaml mostra como toouse Olá FreeWheel plug-in tooschedule anúncios.
* MastPage.xaml mostra como tooschedule anúncios com um arquivo MAST.
* Programmaticadpage. XAML mostra como tooprogrammatically agendar anúncios em um vídeo.
* ScheduleClipPage.xaml mostra como tooschedule um anúncio sem um arquivo grande.
* VastLinearCompanionPage.xaml mostra como tooinsert linear e complementar ad.
* VastNonLinearPage.xaml mostra como tooinsert um anúncio não linear.
* VmapPage.xaml mostra como toospecify anúncios com um arquivo VMAP.

Cada um desses exemplos usa a classe de Media Player de saudação definido pela estrutura de player hello. A maioria dos exemplos usam plugins que adicionam suporte para vários formatos de resposta de anúncio. exemplo do Hello ProgrammaticAdPage interage programaticamente com uma instância do Media Player.

### <a name="adpodpage-sample"></a>Exemplo do AdPodPage
Este exemplo usa Olá AdSchedulerPlugin toodefine quando toodisplay um anúncio. Neste exemplo, um anúncio Mid-roll é agendado toobe reproduzida depois de 5 segundos. pod ad de saudação (um grupo de anúncios toodisplay em ordem) é especificado em um arquivo VAST retornado de um servidor de anúncios. Olá URI toohello grande arquivo é especificado em Olá <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

Para obter mais informações sobre Olá AdSchedulerPlugin, consulte [anúncios no hello estrutura de Player no Windows 8 e Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
Este exemplo também usa Olá AdSchedulerPlugin. Ele agenda três anúncios, um anúncio pre-roll, um anúncio mid-roll e um anúncio post-roll. Olá URI toohello VAST de cada anúncio é especificado em um <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
Este exemplo usa Olá FreeWheelPlugin que especifica um atributo de origem que especifica um URI que arquivo SmartXML tooa de pontos que especifica o conteúdo do ad, bem como informações de agendamento do ad.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
Este exemplo usa Olá MastSchedulerPlugin que permite que você toouse um arquivo MAST. atributo de origem de saudação especifica o local de saudação do arquivo MAST de saudação.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
Este exemplo interage programaticamente com hello Media Player. arquivo programmaticadpage. XAML de saudação instancia Olá Media Player:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

arquivo de ProgrammaticAdPage.xaml.cs Olá cria um AdHandlerPlugin, adiciona um toospecify TimelineMarker quando um anúncio deve ser exibido e, em seguida, adiciona um manipulador de evento de MarkerReached Olá que carrega um RemoteAdSource especificando um arquivo grande do URI tooa e, em seguida, executa anúncio de saudação.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
Este exemplo usa Olá AdSchedulerPlugin tooschedule um anúncio Mid-roll, especificando um arquivo. wmv que contém ad hello.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
Este exemplo ilustra como toouse Olá AdSchedulerPlugin tooschedule um anúncio linear Mid-roll com um anúncio complementar. Olá <RemoteAdSource> elemento Especifica o local de saudação do arquivo VAST hello.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
Este exemplo usa Olá AdSchedulerPlugin tooschedule linear e um anúncio não linear. Olá local do arquivo VAST é especificado com hello <RemoteAdSource> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
Este exemplo usa os anúncios de tooschedule VmapSchedulerPlugin hello usando um arquivo VMAP. arquivo do Hello URI toohello VMAP é especificado no atributo de origem de saudação do hello <VmapSchedulerPlugin> elemento.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Implementando um iOS Video Player com suporte para anúncios
Olá Microsoft Media Platform: estrutura de Player para iOS contém uma coleção de aplicativos de exemplo que mostram como tooimplement um aplicativo de player de vídeo usando Olá do framework. Você pode baixar exemplos de estrutura de Player e Olá Olá de [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). Olá, página github tem um link de tooa Wiki que contém informações adicionais sobre a estrutura de player hello e um exemplo do player Introdução toohello: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>Agendando anúncios com VMAP
Olá mostrado no exemplo a seguir como tooschedule anúncios usando um arquivo VMAP.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>Agendando anúncios com VAST
saudação de exemplo a seguir mostra como tooschedule um anúncio VAST de associação tardia.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   saudação de exemplo a seguir mostra como tooschedule um anúncio VAST de associação antecipada.
Exemplo: 4 agenda um antecipado Olá associação anúncio VAST //Download VAST arquivo caso (! [ framework.adResolver downloadManifest: & manifesto withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

saudação de exemplo a seguir mostra como tooinsert um anúncio usando aproximada Recortar RCE (edição)

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

Olá exemplo a seguir mostra como tooschedule um ad pod.

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Olá mostrado no exemplo a seguir como tooschedule um não-Mid-roll sticky. Um não-sticky é reproduzido apenas uma vez, independentemente de qualquer busca Olá visualizador executa.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Olá mostrado no exemplo a seguir como tooschedule um anúncio Mid-roll sticky. Um anúncio sticky será exibido cada vez Olá especificadas ponto na linha do tempo de saudação vídeo seja alcançado.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


saudação de exemplo a seguir mostra como tooschedule um POST-roll.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

saudação de exemplo a seguir mostra como tooschedule um anúncio Pre-roll.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

saudação de exemplo a seguir mostra como tooschedule um Mid-roll sobreposição de ad.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Desenvolver aplicativos de player de vídeo](media-services-develop-video-players.md)

