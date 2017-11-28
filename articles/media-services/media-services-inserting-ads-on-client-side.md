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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="d5e78-103">Inserção de anúncios no lado do cliente Olá</span><span class="sxs-lookup"><span data-stu-id="d5e78-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="d5e78-104">Este tópico contém informações sobre como tooinsert vários tipos de anúncios no lado do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="d5e78-105">Para obter informações sobre o suporte a legendagem oculta e anúncios em vídeos de transmissão ao vivo, consulte [Padrões de legendagem oculta e inserção de anúncios com suporte](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="d5e78-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="d5e78-106">Atualmente, o Azure Media Player não dá suporte a anúncios.</span><span class="sxs-lookup"><span data-stu-id="d5e78-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="d5e78-107"><a id="insert_ads_into_media"></a>Inserir anúncios em sua mídia</span><span class="sxs-lookup"><span data-stu-id="d5e78-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="d5e78-108">Serviços de mídia do Azure fornece suporte para inserção de anúncios por meio de saudação plataforma de mídia do Windows: estruturas de Player.</span><span class="sxs-lookup"><span data-stu-id="d5e78-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="d5e78-109">As estruturas de player com suporte a anúncios estão disponíveis para dispositivos com Windows 8, Silverlight, Windows Phone 8 e iOS.</span><span class="sxs-lookup"><span data-stu-id="d5e78-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="d5e78-110">Cada estrutura de player contém um código de exemplo que mostra como tooimplement um aplicativo de player. Há três tipos diferentes de anúncios, que você pode inserir em sua lista de mídia:.</span><span class="sxs-lookup"><span data-stu-id="d5e78-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="d5e78-111">**Linear** – completo anúncios de quadro que pausam o vídeo principal hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="d5e78-112">**Não lineares** – anúncios de sobreposição que são exibidos como reprodução do vídeo principal Olá, geralmente um logotipo ou outra imagem estática colocada no player de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="d5e78-113">**Complementar** – anúncios que são exibidos fora do player hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="d5e78-114">Anúncios podem ser inseridos em qualquer ponto na linha do tempo do vídeo principal hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="d5e78-115">Você deve informar o player hello quando tooplay Olá ad e qual tooplay de anúncios.</span><span class="sxs-lookup"><span data-stu-id="d5e78-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="d5e78-116">Isso é feito usando um conjunto de arquivos padrão baseados em XML: VAST (Video Ad Service Template), VMAP (Digital Video Multiple Ad Playlist), MAST (Media Abstract Sequencing Template) e VPAID (Digital Video Player Ad Interface Definition).</span><span class="sxs-lookup"><span data-stu-id="d5e78-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="d5e78-117">Os arquivos VAST especificam quais toodisplay anúncios.</span><span class="sxs-lookup"><span data-stu-id="d5e78-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="d5e78-118">Arquivos VMAP especificam quando tooplay diversos anúncios e contêm XML VAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="d5e78-119">Os arquivos MAST são outra anúncios de toosequence de forma que também podem conter XML VAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="d5e78-120">Os arquivos VPAID definem uma interface entre o player de vídeo hello e ad hello ou servidor do ad.</span><span class="sxs-lookup"><span data-stu-id="d5e78-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="d5e78-121">Cada estrutura do player funciona de maneira diferente e cada uma será abordada em seu próprio tópico.</span><span class="sxs-lookup"><span data-stu-id="d5e78-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="d5e78-122">Este tópico descreverá Olá mecanismos básicos usados tooinsert anúncios. Aplicativos de player de vídeo solicitarem anúncios de um servidor do ad.</span><span class="sxs-lookup"><span data-stu-id="d5e78-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="d5e78-123">servidor do ad Olá pode responder de várias maneiras:</span><span class="sxs-lookup"><span data-stu-id="d5e78-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="d5e78-124">Retornar um arquivo VAST</span><span class="sxs-lookup"><span data-stu-id="d5e78-124">Return a VAST file</span></span>
* <span data-ttu-id="d5e78-125">Retornar um arquivo VMAP (com VAST incorporado)</span><span class="sxs-lookup"><span data-stu-id="d5e78-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="d5e78-126">Retornar um arquivo MAST (com VAST incorporado)</span><span class="sxs-lookup"><span data-stu-id="d5e78-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="d5e78-127">Retornar um arquivo VAST com anúncios VPAID</span><span class="sxs-lookup"><span data-stu-id="d5e78-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="d5e78-128">Usando um arquivo (VAST) de modelo do serviço de anúncio de vídeo</span><span class="sxs-lookup"><span data-stu-id="d5e78-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="d5e78-129">Um arquivo VAST Especifica quais anúncios toodisplay.</span><span class="sxs-lookup"><span data-stu-id="d5e78-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="d5e78-130">Olá XML a seguir é um exemplo de um arquivo grande para um anúncio linear:</span><span class="sxs-lookup"><span data-stu-id="d5e78-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="d5e78-131">anúncio linear Olá é descrito por hello <**Linear**> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="d5e78-132">Especifica a duração de saudação do ad Olá, eventos de rastreamento, clique no, clique em controle e um número de **MediaFile** elementos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="d5e78-133">Eventos de rastreamento são especificados em hello <**TrackingEvents**> elemento e permitir um tootrack de servidor de ad vários eventos que ocorrem durante a visualização ad hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="d5e78-134">Nesse caso, Olá início, ponto médio, conclusão e expanda eventos serão rastreados.</span><span class="sxs-lookup"><span data-stu-id="d5e78-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="d5e78-135">Olá início do evento ocorre quando a saudação anúncio é exibido.</span><span class="sxs-lookup"><span data-stu-id="d5e78-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="d5e78-136">evento de ponto médio de saudação ocorre quando pelo menos 50% da linha de tempo do ad Olá foi exibida.</span><span class="sxs-lookup"><span data-stu-id="d5e78-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="d5e78-137">evento de conclusão de Olá ocorre quando ad Olá ficou toohello final.</span><span class="sxs-lookup"><span data-stu-id="d5e78-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="d5e78-138">evento de expansão Olá ocorre quando o usuário Olá expande a tela de toofull hello player de vídeo.</span><span class="sxs-lookup"><span data-stu-id="d5e78-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="d5e78-139">Os clickthroughs são especificados com um <**ClickThrough**> elemento dentro de um <**VideoClicks**> elemento e especifica um toodisplay de recurso do URI tooa quando o usuário Olá clica no ad hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="d5e78-140">Rastreamento de cliques é especificado em uma <**rastreamento de cliques**> elemento, também em hello <**VideoClicks**> elemento e especifica um recurso de rastreamento para Olá player toorequest quando Olá usuário clica em em Olá ad.hello <**MediaFile**> especificam informações sobre uma codificação específica de um anúncio.</span><span class="sxs-lookup"><span data-stu-id="d5e78-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="d5e78-141">Quando há mais de um <**MediaFile**> elemento, o player de vídeo Olá pode escolher Olá melhor codificação para a plataforma de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="d5e78-142">Os anúncios lineares podem ser exibidos na ordem especificada.</span><span class="sxs-lookup"><span data-stu-id="d5e78-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="d5e78-143">toodo isso, adicione adicionais <Ad> elementos toohello VAST de arquivo e especificar ordem hello usando o atributo de sequência de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="d5e78-144">saudação de exemplo a seguir ilustra isso:</span><span class="sxs-lookup"><span data-stu-id="d5e78-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="d5e78-145">Anúncios não lineares também são especificados em um elemento de <Creative>.</span><span class="sxs-lookup"><span data-stu-id="d5e78-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="d5e78-146">Olá mostrado no exemplo a seguir um <Creative> elemento que descreve um anúncio não linear.</span><span class="sxs-lookup"><span data-stu-id="d5e78-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="d5e78-147">Olá <**NonLinearAds**> elemento pode conter um ou mais <**não lineares**> elementos, cada um deles pode descrever um anúncio não linear.</span><span class="sxs-lookup"><span data-stu-id="d5e78-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="d5e78-148">Olá <**não lineares**> elemento Especifica o recurso Olá para o anúncio não linear hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="d5e78-149">Olá recurso pode ser um <**StaticResouce**>, um <**IFrameResource**>, ou um <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="d5e78-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="d5e78-150"> <**StaticResource**> descreve um recurso não HTML e define um atributo creativeType que especifica como o recurso de saudação é exibido:</span><span class="sxs-lookup"><span data-stu-id="d5e78-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="d5e78-151">Imagem/gif, imagem/jpeg, imagem/png – o recurso de saudação é exibido em uma marca HTML <**img**> marca.</span><span class="sxs-lookup"><span data-stu-id="d5e78-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="d5e78-152">Aplicativo/x-javascript – recursos de saudação é exibido em um HTML <**script**> marca.</span><span class="sxs-lookup"><span data-stu-id="d5e78-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="d5e78-153">Application/x-shockwave-flash – recursos Olá é exibido em um player Flash.</span><span class="sxs-lookup"><span data-stu-id="d5e78-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="d5e78-154">**IFrameResource** descreve um recurso HTML que pode ser exibido em um IFrame.</span><span class="sxs-lookup"><span data-stu-id="d5e78-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="d5e78-155">**HTMLResource** descreve um trecho de código HTML que pode ser inserido em uma página da Web.</span><span class="sxs-lookup"><span data-stu-id="d5e78-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="d5e78-156">**TrackingEvents** especificar eventos de rastreamento e Olá URI toorequest quando ocorre o evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="d5e78-157">No hello exemplo eventos acceptInvitation e collapse são rastreados.</span><span class="sxs-lookup"><span data-stu-id="d5e78-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="d5e78-158">Para obter mais informações sobre Olá **NonLinearAds** elemento e seus filhos, consulte IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="d5e78-159">Observe que Olá **TrackingEvents** elemento está localizado em Olá **NonLinearAds** elemento, em vez da saudação **não lineares** elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="d5e78-160">Anúncios complementares são definidos dentro de um elemento de <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="d5e78-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="d5e78-161">Olá <CompanionAds> elemento pode conter um ou mais <Companion> elementos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="d5e78-162">Cada <Companion> elemento descreve um anúncio complementar e pode conter um <StaticResource>, <IFrameResource>, ou <HTMLResource> que são especificados em Olá mesma maneira que um anúncio não linear.</span><span class="sxs-lookup"><span data-stu-id="d5e78-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="d5e78-163">Um arquivo grande pode conter diversos anúncios complementares e aplicativo de player hello pode escolher Olá toodisplay de anúncio mais apropriado.</span><span class="sxs-lookup"><span data-stu-id="d5e78-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="d5e78-164">Para saber mais sobre VAST, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="d5e78-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="d5e78-165">Usando um arquivo VMAP (Digital Video Multiple Ad Playlist)</span><span class="sxs-lookup"><span data-stu-id="d5e78-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="d5e78-166">Um arquivo VMAP permite que você toospecify quando intervalos de anúncios acontecem, quanto tempo cada quebra é, quantos anúncios podem ser exibidos durante um intervalo e quais tipos de anúncios podem ser exibidos durante um intervalo.</span><span class="sxs-lookup"><span data-stu-id="d5e78-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="d5e78-167">Olá a seguir um exemplo de arquivo VMAP que define um único intervalo de anúncio:</span><span class="sxs-lookup"><span data-stu-id="d5e78-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="d5e78-168">Um arquivo VMAP começa com um elemento de <VMAP> que contém um ou mais elementos de <AdBreak>, cada um definindo um intervalo de anúncio.</span><span class="sxs-lookup"><span data-stu-id="d5e78-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="d5e78-169">Cada intervalo de anúncio especifica um tipo de intervalo, ID de intervalo e deslocamento de tempo.</span><span class="sxs-lookup"><span data-stu-id="d5e78-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="d5e78-170">atributo do Hello breakType Especifica o tipo de saudação de anúncio que pode ser reproduzido durante o intervalo de saudação: linear, não linear ou exibição.</span><span class="sxs-lookup"><span data-stu-id="d5e78-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="d5e78-171">Exibir anúncios anúncios complementares de tooVAST do mapa.</span><span class="sxs-lookup"><span data-stu-id="d5e78-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="d5e78-172">Mais de um tipo de anúncio pode ser especificado em uma lista separada por vírgulas (sem espaços).</span><span class="sxs-lookup"><span data-stu-id="d5e78-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="d5e78-173">Olá breakID é um identificador opcional para o ad hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="d5e78-174">Olá timeOffset Especifica quando o anúncio de saudação deve ser exibido.</span><span class="sxs-lookup"><span data-stu-id="d5e78-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="d5e78-175">Ele pode ser especificado em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5e78-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="d5e78-176">Tempo – em formato hh:mm:ss ou hh:mm:ss.mmm em que .mmm são milissegundos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="d5e78-177">valor deste atributo Olá Especifica o tempo de saudação do início de saudação do início de toohello Olá vídeo da linha do tempo de intervalo de anúncio de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="d5e78-178">Porcentagem – em formato % n onde n é o percentual de saudação do tooplay de vídeo da linha do tempo de saudação antes de reproduzir ad Olá</span><span class="sxs-lookup"><span data-stu-id="d5e78-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="d5e78-179">Início/fim – Especifica que um anúncio deve ser exibido antes ou depois de vídeo Olá foram exibido</span><span class="sxs-lookup"><span data-stu-id="d5e78-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="d5e78-180">Posição – Especifica a ordem de saudação do ad quebras quando tempo Olá Olá ad quebras de é desconhecido, como na transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="d5e78-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="d5e78-181">ordem de saudação de cada intervalo de anúncio é especificada no formato de saudação #n onde n é um inteiro de 1 ou maior.</span><span class="sxs-lookup"><span data-stu-id="d5e78-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="d5e78-182">1 significa Olá anúncio deve ser reproduzido na primeira oportunidade de hello, 2 significa ad Olá deve ser reproduzido na segunda oportunidade de saudação e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d5e78-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="d5e78-183">Em hello <**AdBreak**> elemento pode ser um <**AdSource**> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="d5e78-184">Olá <**AdSource**> elemento contém Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="d5e78-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="d5e78-185">ID – Especifica um identificador para a origem do ad Olá</span><span class="sxs-lookup"><span data-stu-id="d5e78-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="d5e78-186">allowMultipleAds – um valor booleano que especifica se anúncios múltiplos podem ser exibidos durante o intervalo de anúncio Olá</span><span class="sxs-lookup"><span data-stu-id="d5e78-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="d5e78-187">followRedirects – um valor booleano opcional que especifica se o player de vídeo Olá deve usar redirecionamentos dentro de uma resposta de anúncio</span><span class="sxs-lookup"><span data-stu-id="d5e78-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="d5e78-188">Olá <**AdSource**> elemento fornece player Olá uma resposta embutida de anúncio ou uma resposta de anúncio de tooan de referência.</span><span class="sxs-lookup"><span data-stu-id="d5e78-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="d5e78-189">Ele pode conter uma saudação elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5e78-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="d5e78-190"><VASTAdData>indica que uma resposta de anúncio VAST está inserida no arquivo VMAP de saudação</span><span class="sxs-lookup"><span data-stu-id="d5e78-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="d5e78-191"><AdTagURI> um URI que faz referência a uma resposta de anúncio de outro sistema</span><span class="sxs-lookup"><span data-stu-id="d5e78-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="d5e78-192"><CustomAdData> -uma cadeia de caracteres arbitrária que representa uma resposta não VAST</span><span class="sxs-lookup"><span data-stu-id="d5e78-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="d5e78-193">Neste exemplo, uma resposta embutida de anúncio é especificada com um elemento <VASTAdData> que contém uma resposta de anúncio VAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="d5e78-194">Para obter mais informações sobre Olá outros elementos, consulte [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="d5e78-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="d5e78-195">Olá <**AdBreak**> elemento também pode conter um <**TrackingEvents**> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="d5e78-196">Olá <**TrackingEvents**> elemento permite iniciar de saudação tootrack ou final de um intervalo de anúncio ou se ocorreu um erro durante o intervalo de anúncio Olá.</span><span class="sxs-lookup"><span data-stu-id="d5e78-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="d5e78-197">Olá <**TrackingEvents**> elemento contém um ou mais <**controle**> elementos, cada um deles especifica um evento de rastreamento e um URI de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="d5e78-198">Olá possíveis eventos de rastreamento são:</span><span class="sxs-lookup"><span data-stu-id="d5e78-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="d5e78-199">breakStart – rastreia a partir de um intervalo de anúncio Olá</span><span class="sxs-lookup"><span data-stu-id="d5e78-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="d5e78-200">breakEnd – acompanhar Olá conclusão de um intervalo de anúncio</span><span class="sxs-lookup"><span data-stu-id="d5e78-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="d5e78-201">Error – rastreia um erro que ocorreu durante o intervalo de anúncio Olá</span><span class="sxs-lookup"><span data-stu-id="d5e78-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="d5e78-202">saudação de exemplo a seguir mostra um arquivo VMAP que especifica os eventos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="d5e78-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="d5e78-203">Para obter mais informações sobre hello <**TrackingEvents**> elemento e seus filhos, consulte http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="d5e78-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="d5e78-204">Usando um arquivo MAST (Media Abstract Sequencing Template)</span><span class="sxs-lookup"><span data-stu-id="d5e78-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="d5e78-205">Um arquivo MAST permite que você toospecify gatilhos que definem quando um anúncio é exibido.</span><span class="sxs-lookup"><span data-stu-id="d5e78-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="d5e78-206">a seguir Olá é um arquivo MAST de exemplo que contém acionadores para um anúncio de roll pre, um anúncio Mid-roll e um POST-roll.</span><span class="sxs-lookup"><span data-stu-id="d5e78-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="d5e78-207">Um arquivo MAST começa com um elemento **MAST** que contém um elemento **triggers**.</span><span class="sxs-lookup"><span data-stu-id="d5e78-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="d5e78-208">Olá <triggers> elemento contém um ou mais **gatilho** elementos que definem quando um anúncio deve ser reproduzido.</span><span class="sxs-lookup"><span data-stu-id="d5e78-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="d5e78-209">Olá **gatilho** elemento contém um **startConditions** elemento que especificam quando um anúncio deve começar tooplay.</span><span class="sxs-lookup"><span data-stu-id="d5e78-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="d5e78-210">Olá **startConditions** elemento contém um ou mais <condition> elementos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="d5e78-211">Quando cada <condition> avalia tootrue um acionador é iniciado ou revogado dependendo se Olá <condition> está dentro de um **startConditions** ou **endConditions** elemento respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d5e78-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="d5e78-212">Quando vários <condition> elementos estão presentes, elas são tratadas como um implícito ou, qualquer condição avaliada tootrue fará com que a saudação gatilho tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="d5e78-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="d5e78-213">Os elementos <condition> podem ser aninhados.</span><span class="sxs-lookup"><span data-stu-id="d5e78-213"><condition> elements can be nested.</span></span> <span data-ttu-id="d5e78-214">Quando filho <condition> elementos são predefinidos, elas são tratadas como um implícito e, todas as condições devem ser avaliadas tootrue para Olá gatilho tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="d5e78-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="d5e78-215">Olá <condition> elemento contém Olá atributos que definem a condição de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5e78-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="d5e78-216">**tipo** – Especifica o tipo de saudação de condição, evento ou propriedade</span><span class="sxs-lookup"><span data-stu-id="d5e78-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="d5e78-217">**nome** – hello nome da saudação toobe propriedade ou evento usado durante a avaliação</span><span class="sxs-lookup"><span data-stu-id="d5e78-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="d5e78-218">**valor** – Olá o valor de uma propriedade será avaliada</span><span class="sxs-lookup"><span data-stu-id="d5e78-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="d5e78-219">**operador** – Olá toouse operação durante a avaliação: EQ (igual), NEQ (não igual), GTR (maior), GEQ (maior ou igual), LT (menor que), LEQ (menor ou igual), MOD (módulo)</span><span class="sxs-lookup"><span data-stu-id="d5e78-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="d5e78-220">**endConditions** também contêm elementos <condition>.</span><span class="sxs-lookup"><span data-stu-id="d5e78-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="d5e78-221">Quando a condição for avaliada gatilho de saudação tootrue é reset.hello <trigger> também contém um <sources> elemento que contém um ou mais <source> elementos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="d5e78-222">Olá <source> elementos definem resposta de anúncio de toohello Olá URI e o tipo de saudação de resposta de anúncio.</span><span class="sxs-lookup"><span data-stu-id="d5e78-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="d5e78-223">Neste exemplo, um URI for fornecido resposta VAST tooa.</span><span class="sxs-lookup"><span data-stu-id="d5e78-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="d5e78-224">Usando a VPAID (Video Player-Ad Interface Definition)</span><span class="sxs-lookup"><span data-stu-id="d5e78-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="d5e78-225">VPAID é uma API para habilitar o anúncio executável unidades toocommunicate com um player de vídeo.</span><span class="sxs-lookup"><span data-stu-id="d5e78-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="d5e78-226">Isso permite experiências de anúncios altamente interativos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="d5e78-227">Olá usuário pode interagir com ad hello e ad Olá pode responder tooactions tomadas pelo Visualizador de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="d5e78-228">Por exemplo, um anúncio pode exibir botões que permitem Olá usuário tooview obter mais informações ou uma versão mais longa do anúncio de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="d5e78-229">player de vídeo Olá deve oferecer suporte à saudação API VPAID e anúncio executável Olá deve implementar Olá API.</span><span class="sxs-lookup"><span data-stu-id="d5e78-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="d5e78-230">Quando um player solicita um anúncio de um servidor de saudação do servidor ad pode responder com uma resposta VAST que contém um anúncio vpaid.</span><span class="sxs-lookup"><span data-stu-id="d5e78-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="d5e78-231">Um anúncio executável é criado no código que deve ser executado em um ambiente de tempo de execução como Adobe Flash ™ ou JavaScript, que pode ser executado em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="d5e78-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="d5e78-232">Quando um servidor de anúncios retorna uma resposta VAST que contém um anúncio vpaid, Olá o valor do atributo apiFramework Olá Olá <MediaFile> elemento deve ser "VPAID".</span><span class="sxs-lookup"><span data-stu-id="d5e78-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="d5e78-233">Esse atributo especifica que o ad Olá contido é um anúncio vpaid executável.</span><span class="sxs-lookup"><span data-stu-id="d5e78-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="d5e78-234">o atributo de tipo Hello deve ser definido toohello tipo MIME da saudação executável, como "application/x-shockwave-flash" ou "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="d5e78-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="d5e78-235">Olá, trecho XML a seguir mostra Olá <MediaFile> elemento de uma resposta VAST que contém um anúncio vpaid executável.</span><span class="sxs-lookup"><span data-stu-id="d5e78-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="d5e78-236">Um anúncio executável pode ser inicializado usando Olá <AdParameters> elemento dentro do hello <Linear> ou <NonLinear> elementos em uma resposta VAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="d5e78-237">Para obter mais informações sobre Olá <AdParameters> elemento, consulte [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="d5e78-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="d5e78-238">Para obter mais informações sobre Olá API VPAID, consulte [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="d5e78-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="d5e78-239">Implementação de um player no Windows ou Windows Phone 8 com suporte a anúncios</span><span class="sxs-lookup"><span data-stu-id="d5e78-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="d5e78-240">Olá Microsoft Media Platform: estrutura de Player para Windows 8 e Windows Phone 8 contém uma coleção de aplicativos de exemplo que mostram como tooimplement um aplicativo de player de vídeo usando Olá do framework.</span><span class="sxs-lookup"><span data-stu-id="d5e78-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="d5e78-241">Você pode baixar exemplos de estrutura de Player e Olá Olá de [estrutura de Player para Windows 8 e Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="d5e78-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="d5e78-242">Quando você abre Olá Microsoft.PlayerFramework.Xaml.Samples solução, você verá um número de pastas no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="d5e78-243">pasta de anúncios Olá contém toocreating relevantes de código de exemplo do hello um player de vídeo com suporte do ad.</span><span class="sxs-lookup"><span data-stu-id="d5e78-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="d5e78-244">Interior Olá publicidade pasta é um número de XAML/cs arquivos cada um dos quais mostrar como tooinsert anúncios de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="d5e78-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="d5e78-245">Olá lista a seguir descreve cada:</span><span class="sxs-lookup"><span data-stu-id="d5e78-245">hello following list describes each:</span></span>

* <span data-ttu-id="d5e78-246">AdPodPage.xaml mostra como toodisplay um ad pod.</span><span class="sxs-lookup"><span data-stu-id="d5e78-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="d5e78-247">AdSchedulingPage.xaml mostra como tooschedule anúncios.</span><span class="sxs-lookup"><span data-stu-id="d5e78-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="d5e78-248">FreeWheelPage.xaml mostra como toouse Olá FreeWheel plug-in tooschedule anúncios.</span><span class="sxs-lookup"><span data-stu-id="d5e78-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="d5e78-249">MastPage.xaml mostra como tooschedule anúncios com um arquivo MAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="d5e78-250">Programmaticadpage. XAML mostra como tooprogrammatically agendar anúncios em um vídeo.</span><span class="sxs-lookup"><span data-stu-id="d5e78-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="d5e78-251">ScheduleClipPage.xaml mostra como tooschedule um anúncio sem um arquivo grande.</span><span class="sxs-lookup"><span data-stu-id="d5e78-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="d5e78-252">VastLinearCompanionPage.xaml mostra como tooinsert linear e complementar ad.</span><span class="sxs-lookup"><span data-stu-id="d5e78-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="d5e78-253">VastNonLinearPage.xaml mostra como tooinsert um anúncio não linear.</span><span class="sxs-lookup"><span data-stu-id="d5e78-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="d5e78-254">VmapPage.xaml mostra como toospecify anúncios com um arquivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="d5e78-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="d5e78-255">Cada um desses exemplos usa a classe de Media Player de saudação definido pela estrutura de player hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="d5e78-256">A maioria dos exemplos usam plugins que adicionam suporte para vários formatos de resposta de anúncio.</span><span class="sxs-lookup"><span data-stu-id="d5e78-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="d5e78-257">exemplo do Hello ProgrammaticAdPage interage programaticamente com uma instância do Media Player.</span><span class="sxs-lookup"><span data-stu-id="d5e78-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="d5e78-258">Exemplo do AdPodPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-258">AdPodPage Sample</span></span>
<span data-ttu-id="d5e78-259">Este exemplo usa Olá AdSchedulerPlugin toodefine quando toodisplay um anúncio.</span><span class="sxs-lookup"><span data-stu-id="d5e78-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="d5e78-260">Neste exemplo, um anúncio Mid-roll é agendado toobe reproduzida depois de 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="d5e78-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="d5e78-261">pod ad de saudação (um grupo de anúncios toodisplay em ordem) é especificado em um arquivo VAST retornado de um servidor de anúncios.</span><span class="sxs-lookup"><span data-stu-id="d5e78-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="d5e78-262">Olá URI toohello grande arquivo é especificado em Olá <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="d5e78-263">Para obter mais informações sobre Olá AdSchedulerPlugin, consulte [anúncios no hello estrutura de Player no Windows 8 e Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="d5e78-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="d5e78-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-264">AdSchedulingPage</span></span>
<span data-ttu-id="d5e78-265">Este exemplo também usa Olá AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="d5e78-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="d5e78-266">Ele agenda três anúncios, um anúncio pre-roll, um anúncio mid-roll e um anúncio post-roll.</span><span class="sxs-lookup"><span data-stu-id="d5e78-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="d5e78-267">Olá URI toohello VAST de cada anúncio é especificado em um <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="d5e78-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-268">FreeWheelPage</span></span>
<span data-ttu-id="d5e78-269">Este exemplo usa Olá FreeWheelPlugin que especifica um atributo de origem que especifica um URI que arquivo SmartXML tooa de pontos que especifica o conteúdo do ad, bem como informações de agendamento do ad.</span><span class="sxs-lookup"><span data-stu-id="d5e78-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="d5e78-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-270">MastPage</span></span>
<span data-ttu-id="d5e78-271">Este exemplo usa Olá MastSchedulerPlugin que permite que você toouse um arquivo MAST.</span><span class="sxs-lookup"><span data-stu-id="d5e78-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="d5e78-272">atributo de origem de saudação especifica o local de saudação do arquivo MAST de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="d5e78-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="d5e78-274">Este exemplo interage programaticamente com hello Media Player.</span><span class="sxs-lookup"><span data-stu-id="d5e78-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="d5e78-275">arquivo programmaticadpage. XAML de saudação instancia Olá Media Player:</span><span class="sxs-lookup"><span data-stu-id="d5e78-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="d5e78-276">arquivo de ProgrammaticAdPage.xaml.cs Olá cria um AdHandlerPlugin, adiciona um toospecify TimelineMarker quando um anúncio deve ser exibido e, em seguida, adiciona um manipulador de evento de MarkerReached Olá que carrega um RemoteAdSource especificando um arquivo grande do URI tooa e, em seguida, executa anúncio de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5e78-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="d5e78-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-277">ScheduleClipPage</span></span>
<span data-ttu-id="d5e78-278">Este exemplo usa Olá AdSchedulerPlugin tooschedule um anúncio Mid-roll, especificando um arquivo. wmv que contém ad hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="d5e78-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="d5e78-280">Este exemplo ilustra como toouse Olá AdSchedulerPlugin tooschedule um anúncio linear Mid-roll com um anúncio complementar.</span><span class="sxs-lookup"><span data-stu-id="d5e78-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="d5e78-281">Olá <RemoteAdSource> elemento Especifica o local de saudação do arquivo VAST hello.</span><span class="sxs-lookup"><span data-stu-id="d5e78-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="d5e78-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="d5e78-283">Este exemplo usa Olá AdSchedulerPlugin tooschedule linear e um anúncio não linear.</span><span class="sxs-lookup"><span data-stu-id="d5e78-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="d5e78-284">Olá local do arquivo VAST é especificado com hello <RemoteAdSource> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="d5e78-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="d5e78-285">VMAPPage</span></span>
<span data-ttu-id="d5e78-286">Este exemplo usa os anúncios de tooschedule VmapSchedulerPlugin hello usando um arquivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="d5e78-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="d5e78-287">arquivo do Hello URI toohello VMAP é especificado no atributo de origem de saudação do hello <VmapSchedulerPlugin> elemento.</span><span class="sxs-lookup"><span data-stu-id="d5e78-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="d5e78-288">Implementando um iOS Video Player com suporte para anúncios</span><span class="sxs-lookup"><span data-stu-id="d5e78-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="d5e78-289">Olá Microsoft Media Platform: estrutura de Player para iOS contém uma coleção de aplicativos de exemplo que mostram como tooimplement um aplicativo de player de vídeo usando Olá do framework.</span><span class="sxs-lookup"><span data-stu-id="d5e78-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="d5e78-290">Você pode baixar exemplos de estrutura de Player e Olá Olá de [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="d5e78-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="d5e78-291">Olá, página github tem um link de tooa Wiki que contém informações adicionais sobre a estrutura de player hello e um exemplo do player Introdução toohello: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="d5e78-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="d5e78-292">Agendando anúncios com VMAP</span><span class="sxs-lookup"><span data-stu-id="d5e78-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="d5e78-293">Olá mostrado no exemplo a seguir como tooschedule anúncios usando um arquivo VMAP.</span><span class="sxs-lookup"><span data-stu-id="d5e78-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="d5e78-294">Agendando anúncios com VAST</span><span class="sxs-lookup"><span data-stu-id="d5e78-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="d5e78-295">saudação de exemplo a seguir mostra como tooschedule um anúncio VAST de associação tardia.</span><span class="sxs-lookup"><span data-stu-id="d5e78-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="d5e78-296">saudação de exemplo a seguir mostra como tooschedule um anúncio VAST de associação antecipada.</span><span class="sxs-lookup"><span data-stu-id="d5e78-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="d5e78-297">Exemplo: 4 agenda um antecipado Olá associação anúncio VAST //Download VAST arquivo caso (! [ framework.adResolver downloadManifest: & manifesto withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="d5e78-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="d5e78-298">saudação de exemplo a seguir mostra como tooinsert um anúncio usando aproximada Recortar RCE (edição)</span><span class="sxs-lookup"><span data-stu-id="d5e78-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="d5e78-299">Olá exemplo a seguir mostra como tooschedule um ad pod.</span><span class="sxs-lookup"><span data-stu-id="d5e78-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="d5e78-300">Olá mostrado no exemplo a seguir como tooschedule um não-Mid-roll sticky.</span><span class="sxs-lookup"><span data-stu-id="d5e78-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="d5e78-301">Um não-sticky é reproduzido apenas uma vez, independentemente de qualquer busca Olá visualizador executa.</span><span class="sxs-lookup"><span data-stu-id="d5e78-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="d5e78-302">Olá mostrado no exemplo a seguir como tooschedule um anúncio Mid-roll sticky.</span><span class="sxs-lookup"><span data-stu-id="d5e78-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="d5e78-303">Um anúncio sticky será exibido cada vez Olá especificadas ponto na linha do tempo de saudação vídeo seja alcançado.</span><span class="sxs-lookup"><span data-stu-id="d5e78-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="d5e78-304">saudação de exemplo a seguir mostra como tooschedule um POST-roll.</span><span class="sxs-lookup"><span data-stu-id="d5e78-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="d5e78-305">saudação de exemplo a seguir mostra como tooschedule um anúncio Pre-roll.</span><span class="sxs-lookup"><span data-stu-id="d5e78-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="d5e78-306">saudação de exemplo a seguir mostra como tooschedule um Mid-roll sobreposição de ad.</span><span class="sxs-lookup"><span data-stu-id="d5e78-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="d5e78-307">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="d5e78-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d5e78-308">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="d5e78-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d5e78-309">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d5e78-309">See Also</span></span>
[<span data-ttu-id="d5e78-310">Desenvolver aplicativos de player de vídeo</span><span class="sxs-lookup"><span data-stu-id="d5e78-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

