---
title: "aaaSmooth plug-in de Streaming para Olá Open Source Media Framework"
description: "Saiba como toouse Olá plug-in do Azure Media Services Smooth Streaming para Olá Adobe Open Source Media Framework."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="ff4f1-103">Como o tooUse hello Microsoft Smooth Streaming plug-in para Olá Adobe Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="ff4f1-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="ff4f1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ff4f1-104">Overview</span></span>
<span data-ttu-id="ff4f1-105">Olá plug-in Microsoft Smooth Streaming para Open Source Media Framework 2.0 (SS para OSMF) estende os recursos de padrão de saudação de OSMF e adiciona toonew de reprodução de conteúdo Microsoft Smooth Streaming e OSMF existente players.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="ff4f1-106">Olá plug-in também adiciona Smooth Streaming reprodução tooStrobe de recursos Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="ff4f1-107">O SS para OSMF inclui duas versões do plug-in:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="ff4f1-108">Plug-in do Static Smooth Streaming para OSMF (.swc)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="ff4f1-109">Plug-in do Dynamic Smooth Streaming para OSMF (.swf)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="ff4f1-110">Este documento assume que o leitor de saudação tenha um conhecimento prático geral de OSMF e OSMF plug-ins. Para obter mais informações sobre OSMF, consulte documentação Olá em Olá [site oficial do OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="ff4f1-111">Plug-in do Smooth Streaming para OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="ff4f1-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="ff4f1-112">Olá plug-in dá suporte ao carregamento e a reprodução de conteúdo de Smooth Streaming sob demanda com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="ff4f1-113">Reprodução de Smooth Streaming sob demanda (reproduzir, pausar, buscar, parar)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="ff4f1-114">Reprodução de Smooth Streaming ao vivo (reproduzir)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="ff4f1-115">Funções de DVR ao vivo (pausar, buscar, reprodução de DVR, Go-to-Live)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="ff4f1-116">Suporte para codecs de vídeo - H.264</span><span class="sxs-lookup"><span data-stu-id="ff4f1-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="ff4f1-117">Suporte para codecs de áudio - AAC</span><span class="sxs-lookup"><span data-stu-id="ff4f1-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="ff4f1-118">Comutação de vários idiomas de áudio com as APIs internas do OSMF</span><span class="sxs-lookup"><span data-stu-id="ff4f1-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="ff4f1-119">Seleção da qualidade de reprodução máxima com as APIs internas do OSMF</span><span class="sxs-lookup"><span data-stu-id="ff4f1-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="ff4f1-120">Legendas codificadas sidecar com o plug-in de legendas do OSMF</span><span class="sxs-lookup"><span data-stu-id="ff4f1-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="ff4f1-121">Adobe&reg; Flash&reg; Player 11.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="ff4f1-122">Essa versão dá suporte apenas ao OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="ff4f1-123">Recursos com suporte e problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="ff4f1-123">Supported features and known issues</span></span>
<span data-ttu-id="ff4f1-124">Para obter uma lista completa de recursos com suporte, recursos sem suporte e problemas conhecidos, consulte muito[neste documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="ff4f1-125">Saudação de carregamento de plug-in</span><span class="sxs-lookup"><span data-stu-id="ff4f1-125">Loading hello Plugin</span></span>
<span data-ttu-id="ff4f1-126">Os plug-ins do OSMF podem ser carregados estaticamente (em tempo de compilação) ou dinamicamente (em tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="ff4f1-127">Olá Smooth Streaming plug-in para download OSMF inclui versões dinâmicas e estáticas.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="ff4f1-128">Carregamento estático: tooload estaticamente, um arquivo de biblioteca estática (SWC) é necessário.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="ff4f1-129">Estáticos plug-ins são adicionados como referência toohello projetos e mesclagem de saída final de saudação do arquivo em tempo de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="ff4f1-130">Carregamento dinâmico: tooload dinamicamente, pré-compilado (SWF) é necessário um arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="ff4f1-131">Plug-ins dinâmicos são carregadas no tempo de execução de saudação e não incluídos na saída do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="ff4f1-132">(Saída compilada) Os plug-ins dinâmicos podem ser carregados usando os protocolos HTTP e FILE.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="ff4f1-133">Para obter mais informações sobre carregamento estático e dinâmico, consulte oficial Olá [página de plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="ff4f1-134">SS para carregamento dinâmico de OSMF</span><span class="sxs-lookup"><span data-stu-id="ff4f1-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="ff4f1-135">trecho de código Olá abaixo mostra como tooload hello SS plugin para OSMF estaticamente e reproduzir um vídeo básico usando a classe de OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="ff4f1-136">Antes de incluir Olá SS para o código OSMF, verifique se a referência de projeto de saudação inclui plug-in de estático hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="ff4f1-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="ff4f1-137">Carregamento dinâmico de SS para OSMF</span><span class="sxs-lookup"><span data-stu-id="ff4f1-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="ff4f1-138">trecho de código Olá abaixo mostra como tooload hello SS plugin para OSMF dinamicamente e reproduzir um vídeo básico usando a classe de OSMF MediaFactory hello.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="ff4f1-139">Antes de incluir Olá SS para o código OSMF, copie a pasta de projeto de toohello do hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dinâmico de plug-in se você quiser tooload usando o protocolo de arquivo, ou copiar em um servidor web para carga HTTP.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="ff4f1-140">Não há nenhum tooinclude necessidade "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" hello referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="ff4f1-141">pacote {</span><span class="sxs-lookup"><span data-stu-id="ff4f1-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="ff4f1-142">}</span><span class="sxs-lookup"><span data-stu-id="ff4f1-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="ff4f1-143">Strobe Media Playback com hello ODMF SS dinâmico plug-in</span><span class="sxs-lookup"><span data-stu-id="ff4f1-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="ff4f1-144">Olá Smooth Streaming para plug-in OSMF dinâmico é compatível com [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="ff4f1-145">Você pode usar o hello SS para OSMF plug-in tooadd Smooth Streaming reprodução de conteúdo tooSMP.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="ff4f1-146">toodo, cópia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" em um servidor web para carga HTTP usando Olá seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="ff4f1-147">Procurar Olá [página de instalação Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="ff4f1-148">Origem de Smooth Streaming tooa do conjunto de saudação src, (por exemplo, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="ff4f1-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="ff4f1-149">Fazer alterações de configuração de saudação desejada e clique em visualização e atualização.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="ff4f1-150">**Observação** o servidor web de conteúdo precisa de um crossdomain.xml válido.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="ff4f1-151">Copie e cole Olá código tooa página HTML simples usando seu editor de texto favorito, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="ff4f1-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="ff4f1-152">Adicionar o Streaming do Smooth OSMF plug-in toohello código de inserção e salvar.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="ff4f1-153">Salve a página HTML e publicar tooa web server.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="ff4f1-154">Procurar toohello publicado página da web usando o Flash favorito&reg; Player habilitado o navegador da Internet (Internet Explorer, Chrome, Firefox, etc).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="ff4f1-155">Aproveite o conteúdo de Smooth Streaming no Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="ff4f1-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="ff4f1-156">Para obter mais informações sobre o desenvolvimento de OSMF geral, consulte oficial Olá [página de desenvolvimento de OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="ff4f1-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ff4f1-157">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ff4f1-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ff4f1-158">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ff4f1-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ff4f1-159">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ff4f1-159">See Also</span></span>
[<span data-ttu-id="ff4f1-160">plug-in Microsoft Adaptive Streaming para atualização OSMF</span><span class="sxs-lookup"><span data-stu-id="ff4f1-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

