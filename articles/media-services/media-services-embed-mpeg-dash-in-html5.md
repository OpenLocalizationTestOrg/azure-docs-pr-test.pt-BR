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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="f55da-103">Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js</span><span class="sxs-lookup"><span data-stu-id="f55da-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="f55da-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f55da-104">Overview</span></span>
<span data-ttu-id="f55da-105">MPEG DASH é um padrão ISO para Olá adaptive streaming de conteúdo de vídeo, que oferece benefícios significativos para os usuários que desejarem toodeliver adaptável, de alta qualidade de streaming de vídeo saída.</span><span class="sxs-lookup"><span data-stu-id="f55da-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="f55da-106">Com MPEG-DASH, o fluxo de vídeo Olá removerá automaticamente definição inferior tooa quando Olá rede fica congestionada.</span><span class="sxs-lookup"><span data-stu-id="f55da-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="f55da-107">Isso reduz a probabilidade de saudação do Visualizador de saudação vendo um vídeo "pausado" enquanto o player Olá Olá de baixa seguida alguns tooplay segundos (também conhecido como buffer).</span><span class="sxs-lookup"><span data-stu-id="f55da-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="f55da-108">Que reduz o congestionamento da rede, o player de vídeo Olá por sua vez retornará tooa fluxo de qualidade superior.</span><span class="sxs-lookup"><span data-stu-id="f55da-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="f55da-109">Essa capacidade tooadapt Olá largura de banda necessária também resulta em uma hora de início rápida para vídeo.</span><span class="sxs-lookup"><span data-stu-id="f55da-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="f55da-110">Que significa que Olá primeiros segundos pode ser executada em um segmento de qualidade inferior fast para download e, em seguida, migrar tooa alta qualidade quando conteúdo suficiente foi armazenada em buffer.</span><span class="sxs-lookup"><span data-stu-id="f55da-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="f55da-111">O dash.js é um player de vídeo MPEG-DASH de software livre escrito em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f55da-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="f55da-112">Sua meta é tooprovide um player robusto e de plataforma cruzada que pode ser livremente reutilizado em aplicativos que exigem reprodução de vídeo.</span><span class="sxs-lookup"><span data-stu-id="f55da-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="f55da-113">Ele fornece reprodução de MPEG-DASH em qualquer navegador que dá suporte a saudação W3C Media Source Extensions (MSE) hoje que é Chrome, Microsoft Edge e o IE11 (outros navegadores indicaram sua intenção toosupport MSE).</span><span class="sxs-lookup"><span data-stu-id="f55da-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="f55da-114">Para obter mais informações sobre o DASH.js, js consulte repositório dash.js do hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="f55da-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="f55da-115">Criando um player de vídeo de streaming com base no navegador</span><span class="sxs-lookup"><span data-stu-id="f55da-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="f55da-116">toocreate uma página da web simples que exibe um player de vídeo com hello esperado controla como um reproduzir, pausar, retroceder etc., você precisará:</span><span class="sxs-lookup"><span data-stu-id="f55da-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="f55da-117">Criar uma página HTML</span><span class="sxs-lookup"><span data-stu-id="f55da-117">Create an HTML page</span></span>
2. <span data-ttu-id="f55da-118">Adicionar a marca de vídeo Olá</span><span class="sxs-lookup"><span data-stu-id="f55da-118">Add hello video tag</span></span>
3. <span data-ttu-id="f55da-119">Adicionar Olá dash.js jogador</span><span class="sxs-lookup"><span data-stu-id="f55da-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="f55da-120">Inicializar o player Olá</span><span class="sxs-lookup"><span data-stu-id="f55da-120">Initialize hello player</span></span>
5. <span data-ttu-id="f55da-121">Adicionar estilo CSS</span><span class="sxs-lookup"><span data-stu-id="f55da-121">Add some CSS style</span></span>
6. <span data-ttu-id="f55da-122">Exibir os resultados em um navegador que implementa MSE Olá</span><span class="sxs-lookup"><span data-stu-id="f55da-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="f55da-123">Inicializando player de saudação pode ser concluída em apenas algumas linhas de código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f55da-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="f55da-124">Usando o dash.js, realmente é que o vídeo MPEG-DASH de tooembed simples em seus aplicativos baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="f55da-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="f55da-125">Criando Olá página HTML</span><span class="sxs-lookup"><span data-stu-id="f55da-125">Creating hello HTML Page</span></span>
<span data-ttu-id="f55da-126">Olá primeira etapa é página toocreate uma HTML padrão que contém a saudação **vídeo** elemento, salve esse arquivo como basicPlayer.html, como Olá exemplo a seguir ilustra:</span><span class="sxs-lookup"><span data-stu-id="f55da-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="f55da-127">Adicionando Olá DASH.js Player</span><span class="sxs-lookup"><span data-stu-id="f55da-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="f55da-128">aplicativo tooadd hello dash.js referência implementação toohello, você precisará toograb arquivo de dash.all.js Olá da versão Olá 1.0 dash.js projeto.</span><span class="sxs-lookup"><span data-stu-id="f55da-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="f55da-129">Isso deve ser salvo na pasta de JavaScript de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55da-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="f55da-130">Esse arquivo é um arquivo de conveniência que reúne todos os códigos de dash.js necessário Olá em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="f55da-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="f55da-131">Se você tiver uma olhada em torno do repositório de dash.js Olá, você encontrar hello arquivos individuais, testar o código e muito mais, mas se você quiser toodo é dash.js de uso e arquivo de dash.all.js Olá é o que você precisa.</span><span class="sxs-lookup"><span data-stu-id="f55da-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="f55da-132">aplicativos de tooyour do player tooadd Olá dash.js, adicione uma seção de cabeçalho de toohello de marca de script de basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="f55da-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="f55da-133">Em seguida, crie um player de saudação do função tooinitialize quando Olá página for carregada.</span><span class="sxs-lookup"><span data-stu-id="f55da-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="f55da-134">Adicione Olá script a seguir após a linha hello em que você carregar dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="f55da-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

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

<span data-ttu-id="f55da-135">Primeiramente, essa função cria um DashContext.</span><span class="sxs-lookup"><span data-stu-id="f55da-135">This function first creates a DashContext.</span></span> <span data-ttu-id="f55da-136">Este é o aplicativo hello de tooconfigure usado para um ambiente de tempo de execução específico.</span><span class="sxs-lookup"><span data-stu-id="f55da-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="f55da-137">Do ponto de vista técnico, ele define Olá classes que Olá estrutura de injeção de dependência devem usar ao construir o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f55da-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="f55da-138">Na maioria dos casos, você usará o Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="f55da-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="f55da-139">Em seguida, instanciar a classe principal de Olá do framework de dash.js hello, Media Player.</span><span class="sxs-lookup"><span data-stu-id="f55da-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="f55da-140">Essa classe contém core Olá métodos necessários, como reproduzir e pausam, gerencia Olá relação com o elemento de vídeo hello e também gerenciam a interpretação de saudação do arquivo de descrição de apresentação de mídia (MPD) Olá que descreve Olá toobe vídeo reproduzida.</span><span class="sxs-lookup"><span data-stu-id="f55da-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="f55da-141">função de Startup Hello de saudação MediaPlayer classe é chamada tooensure pelo player hello está pronto tooplay de vídeo.</span><span class="sxs-lookup"><span data-stu-id="f55da-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="f55da-142">Entre outras coisas esta função garante que todas as classes necessárias de saudação (conforme definido pelo contexto de saudação) tenham sido carregadas.</span><span class="sxs-lookup"><span data-stu-id="f55da-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="f55da-143">Depois que o player Olá estiver pronto, você pode anexar Olá tooit de elemento de vídeo usando a função de attachView() hello.</span><span class="sxs-lookup"><span data-stu-id="f55da-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="f55da-144">Isso permite que o fluxo de vídeo de Olá Olá Media Player tooinject no elemento de saudação e também controlar a reprodução conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f55da-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="f55da-145">Passar a URL de saudação do hello MPD arquivo toohello Media Player para que ele saiba sobre Olá vídeo é esperado tooplay.hello setupVideo() função recém-criado será necessário toobe executado depois que a página Olá totalmente carregada.</span><span class="sxs-lookup"><span data-stu-id="f55da-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="f55da-146">Faça isso usando o evento onload de saudação do elemento de corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55da-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="f55da-147">Altere o elemento <body> para:</span><span class="sxs-lookup"><span data-stu-id="f55da-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="f55da-148">Finalmente, defina o tamanho de saudação do elemento de vídeo hello usando CSS.</span><span class="sxs-lookup"><span data-stu-id="f55da-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="f55da-149">Em um ambiente de streaming adaptável, isso é especialmente importante porque o tamanho de saudação do hello vídeo que está sendo reproduzida pode mudar conforme reprodução adapta toochanging condições da rede.</span><span class="sxs-lookup"><span data-stu-id="f55da-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="f55da-150">Nesta demonstração simples simplesmente force Olá elemento video toobe 80% da janela de navegador Olá adicionando Olá CSS toohello principal seção da página de saudação seguinte:</span><span class="sxs-lookup"><span data-stu-id="f55da-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="f55da-151">Reproduzindo um vídeo</span><span class="sxs-lookup"><span data-stu-id="f55da-151">Playing a Video</span></span>
<span data-ttu-id="f55da-152">tooplay um vídeo, aponte o navegador no arquivo de basicPlayback.html hello e clique em executar no player de vídeo Olá exibido.</span><span class="sxs-lookup"><span data-stu-id="f55da-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f55da-153">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="f55da-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f55da-154">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="f55da-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f55da-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f55da-155">See Also</span></span>
[<span data-ttu-id="f55da-156">Desenvolver aplicativos de player de vídeo</span><span class="sxs-lookup"><span data-stu-id="f55da-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="f55da-157">Repositório do dash.js do GitHub</span><span class="sxs-lookup"><span data-stu-id="f55da-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

