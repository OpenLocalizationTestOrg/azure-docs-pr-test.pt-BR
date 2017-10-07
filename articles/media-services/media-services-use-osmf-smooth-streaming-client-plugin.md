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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>Como o tooUse hello Microsoft Smooth Streaming plug-in para Olá Adobe Open Source Media Framework
## <a name="overview"></a>Visão geral
Olá plug-in Microsoft Smooth Streaming para Open Source Media Framework 2.0 (SS para OSMF) estende os recursos de padrão de saudação de OSMF e adiciona toonew de reprodução de conteúdo Microsoft Smooth Streaming e OSMF existente players. Olá plug-in também adiciona Smooth Streaming reprodução tooStrobe de recursos Media Playback (SMP).

O SS para OSMF inclui duas versões do plug-in:

* Plug-in do Static Smooth Streaming para OSMF (.swc)
* Plug-in do Dynamic Smooth Streaming para OSMF (.swf)

Este documento assume que o leitor de saudação tenha um conhecimento prático geral de OSMF e OSMF plug-ins. Para obter mais informações sobre OSMF, consulte documentação Olá em Olá [site oficial do OSMF](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Plug-in do Smooth Streaming para OSMF 2.0
Olá plug-in dá suporte ao carregamento e a reprodução de conteúdo de Smooth Streaming sob demanda com hello recursos a seguir:

* Reprodução de Smooth Streaming sob demanda (reproduzir, pausar, buscar, parar)
* Reprodução de Smooth Streaming ao vivo (reproduzir)
* Funções de DVR ao vivo (pausar, buscar, reprodução de DVR, Go-to-Live)
* Suporte para codecs de vídeo - H.264
* Suporte para codecs de áudio - AAC
* Comutação de vários idiomas de áudio com as APIs internas do OSMF
* Seleção da qualidade de reprodução máxima com as APIs internas do OSMF
* Legendas codificadas sidecar com o plug-in de legendas do OSMF
* Adobe&reg; Flash&reg; Player 11.4 ou superior.
* Essa versão dá suporte apenas ao OSMF 2.0.

## <a name="supported-features-and-known-issues"></a>Recursos com suporte e problemas conhecidos
Para obter uma lista completa de recursos com suporte, recursos sem suporte e problemas conhecidos, consulte muito[neste documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Saudação de carregamento de plug-in
Os plug-ins do OSMF podem ser carregados estaticamente (em tempo de compilação) ou dinamicamente (em tempo de execução). Olá Smooth Streaming plug-in para download OSMF inclui versões dinâmicas e estáticas.

* Carregamento estático: tooload estaticamente, um arquivo de biblioteca estática (SWC) é necessário. Estáticos plug-ins são adicionados como referência toohello projetos e mesclagem de saída final de saudação do arquivo em tempo de compilação de saudação.
* Carregamento dinâmico: tooload dinamicamente, pré-compilado (SWF) é necessário um arquivo. Plug-ins dinâmicos são carregadas no tempo de execução de saudação e não incluídos na saída do projeto hello. (Saída compilada) Os plug-ins dinâmicos podem ser carregados usando os protocolos HTTP e FILE.

Para obter mais informações sobre carregamento estático e dinâmico, consulte oficial Olá [página de plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>SS para carregamento dinâmico de OSMF
trecho de código Olá abaixo mostra como tooload hello SS plugin para OSMF estaticamente e reproduzir um vídeo básico usando a classe de OSMF MediaFactory. Antes de incluir Olá SS para o código OSMF, verifique se a referência de projeto de saudação inclui plug-in de estático hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".

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


### <a name="ss-for-osmf-dynamic-loading"></a>Carregamento dinâmico de SS para OSMF
trecho de código Olá abaixo mostra como tooload hello SS plugin para OSMF dinamicamente e reproduzir um vídeo básico usando a classe de OSMF MediaFactory hello. Antes de incluir Olá SS para o código OSMF, copie a pasta de projeto de toohello do hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dinâmico de plug-in se você quiser tooload usando o protocolo de arquivo, ou copiar em um servidor web para carga HTTP. Não há nenhum tooinclude necessidade "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" hello referências de projeto.

pacote {

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Strobe Media Playback com hello ODMF SS dinâmico plug-in
Olá Smooth Streaming para plug-in OSMF dinâmico é compatível com [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html). Você pode usar o hello SS para OSMF plug-in tooadd Smooth Streaming reprodução de conteúdo tooSMP. toodo, cópia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" em um servidor web para carga HTTP usando Olá seguindo as etapas:

1. Procurar Olá [página de instalação Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html). 
2. Origem de Smooth Streaming tooa do conjunto de saudação src, (por exemplo, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Fazer alterações de configuração de saudação desejada e clique em visualização e atualização.
   
   **Observação** o servidor web de conteúdo precisa de um crossdomain.xml válido. 
4. Copie e cole Olá código tooa página HTML simples usando seu editor de texto favorito, como no exemplo a seguir de saudação:

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



1. Adicionar o Streaming do Smooth OSMF plug-in toohello código de inserção e salvar.
   
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
2. Salve a página HTML e publicar tooa web server. Procurar toohello publicado página da web usando o Flash favorito&reg; Player habilitado o navegador da Internet (Internet Explorer, Chrome, Firefox, etc).
3. Aproveite o conteúdo de Smooth Streaming no Adobe&reg; Flash&reg; Player.

Para obter mais informações sobre o desenvolvimento de OSMF geral, consulte oficial Olá [página de desenvolvimento de OSMF](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[plug-in Microsoft Adaptive Streaming para atualização OSMF](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

