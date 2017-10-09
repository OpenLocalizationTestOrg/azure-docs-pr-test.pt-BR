---
title: "aaaEmbedding um vídeo MPEG-DASH Adaptive Streaming em um aplicativo HTML5 com DASH.js | Microsoft Docs"
description: "Este tópico demonstra como tooembed um vídeo MPEG-DASH Adaptive Streaming em um aplicativo HTML5 com DASH.js."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js
## <a name="overview"></a>Visão geral
MPEG DASH é um padrão ISO para Olá adaptive streaming de conteúdo de vídeo, que oferece benefícios significativos para os usuários que desejarem toodeliver adaptável, de alta qualidade de streaming de vídeo saída. Com MPEG-DASH, o fluxo de vídeo Olá removerá automaticamente definição inferior tooa quando Olá rede fica congestionada. Isso reduz a probabilidade de saudação do Visualizador de saudação vendo um vídeo "pausado" enquanto o player Olá Olá de baixa seguida alguns tooplay segundos (também conhecido como buffer). Que reduz o congestionamento da rede, o player de vídeo Olá por sua vez retornará tooa fluxo de qualidade superior. Essa capacidade tooadapt Olá largura de banda necessária também resulta em uma hora de início rápida para vídeo. Que significa que Olá primeiros segundos pode ser executada em um segmento de qualidade inferior fast para download e, em seguida, migrar tooa alta qualidade quando conteúdo suficiente foi armazenada em buffer.

O dash.js é um player de vídeo MPEG-DASH de software livre escrito em JavaScript. Sua meta é tooprovide um player robusto e de plataforma cruzada que pode ser livremente reutilizado em aplicativos que exigem reprodução de vídeo. Ele fornece reprodução de MPEG-DASH em qualquer navegador que dá suporte a saudação W3C Media Source Extensions (MSE) hoje que é Chrome, Microsoft Edge e o IE11 (outros navegadores indicaram sua intenção toosupport MSE). Para obter mais informações sobre o DASH.js, js consulte repositório dash.js do hello GitHub.

## <a name="creating-a-browser-based-streaming-video-player"></a>Criando um player de vídeo de streaming com base no navegador
toocreate uma página da web simples que exibe um player de vídeo com hello esperado controla como um reproduzir, pausar, retroceder etc., você precisará:

1. Criar uma página HTML
2. Adicionar a marca de vídeo Olá
3. Adicionar Olá dash.js jogador
4. Inicializar o player Olá
5. Adicionar estilo CSS
6. Exibir os resultados em um navegador que implementa MSE Olá

Inicializando player de saudação pode ser concluída em apenas algumas linhas de código JavaScript. Usando o dash.js, realmente é que o vídeo MPEG-DASH de tooembed simples em seus aplicativos baseados em navegador.

## <a name="creating-hello-html-page"></a>Criando Olá página HTML
Olá primeira etapa é página toocreate uma HTML padrão que contém a saudação **vídeo** elemento, salve esse arquivo como basicPlayer.html, como Olá exemplo a seguir ilustra:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Adicionando Olá DASH.js Player
aplicativo tooadd hello dash.js referência implementação toohello, você precisará toograb arquivo de dash.all.js Olá da versão Olá 1.0 dash.js projeto. Isso deve ser salvo na pasta de JavaScript de saudação do seu aplicativo. Esse arquivo é um arquivo de conveniência que reúne todos os códigos de dash.js necessário Olá em um único arquivo. Se você tiver uma olhada em torno do repositório de dash.js Olá, você encontrar hello arquivos individuais, testar o código e muito mais, mas se você quiser toodo é dash.js de uso e arquivo de dash.all.js Olá é o que você precisa.

aplicativos de tooyour do player tooadd Olá dash.js, adicione uma seção de cabeçalho de toohello de marca de script de basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Em seguida, crie um player de saudação do função tooinitialize quando Olá página for carregada. Adicione Olá script a seguir após a linha hello em que você carregar dash.all.js:

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

Primeiramente, essa função cria um DashContext. Este é o aplicativo hello de tooconfigure usado para um ambiente de tempo de execução específico. Do ponto de vista técnico, ele define Olá classes que Olá estrutura de injeção de dependência devem usar ao construir o aplicativo hello. Na maioria dos casos, você usará o Dash.di.DashContext.

Em seguida, instanciar a classe principal de Olá do framework de dash.js hello, Media Player. Essa classe contém core Olá métodos necessários, como reproduzir e pausam, gerencia Olá relação com o elemento de vídeo hello e também gerenciam a interpretação de saudação do arquivo de descrição de apresentação de mídia (MPD) Olá que descreve Olá toobe vídeo reproduzida.

função de Startup Hello de saudação MediaPlayer classe é chamada tooensure pelo player hello está pronto tooplay de vídeo. Entre outras coisas esta função garante que todas as classes necessárias de saudação (conforme definido pelo contexto de saudação) tenham sido carregadas. Depois que o player Olá estiver pronto, você pode anexar Olá tooit de elemento de vídeo usando a função de attachView() hello. Isso permite que o fluxo de vídeo de Olá Olá Media Player tooinject no elemento de saudação e também controlar a reprodução conforme necessário.

Passar a URL de saudação do hello MPD arquivo toohello Media Player para que ele saiba sobre Olá vídeo é esperado tooplay.hello setupVideo() função recém-criado será necessário toobe executado depois que a página Olá totalmente carregada. Faça isso usando o evento onload de saudação do elemento de corpo de saudação. Altere o elemento <body> para:

    <body onload="setupVideo()">

Finalmente, defina o tamanho de saudação do elemento de vídeo hello usando CSS. Em um ambiente de streaming adaptável, isso é especialmente importante porque o tamanho de saudação do hello vídeo que está sendo reproduzida pode mudar conforme reprodução adapta toochanging condições da rede. Nesta demonstração simples simplesmente force Olá elemento video toobe 80% da janela de navegador Olá adicionando Olá CSS toohello principal seção da página de saudação seguinte:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Reproduzindo um vídeo
tooplay um vídeo, aponte o navegador no arquivo de basicPlayback.html hello e clique em executar no player de vídeo Olá exibido.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte também
[Desenvolver aplicativos de player de vídeo](media-services-develop-video-players.md)

[Repositório do dash.js do GitHub](https://github.com/Dash-Industry-Forum/dash.js) 

