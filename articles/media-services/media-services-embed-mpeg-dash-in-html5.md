---
title: "Inserindo um vídeo de Streaming Adaptável MPEG-DASH em um Aplicativo HTML5 com DASH.js | Microsoft Docs"
description: "Este tópico demonstra como inserir um Vídeo de Streaming Adaptável MPEG-DASH em um Aplicativo HTML5 com DASH.js."
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="6df1b-103">Inserindo um vídeo de streaming adaptável MPEG-DASH em um aplicativo HTML5 com DASH.js</span><span class="sxs-lookup"><span data-stu-id="6df1b-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="6df1b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6df1b-104">Overview</span></span>
<span data-ttu-id="6df1b-105">O MPEG-DASH é um padrão ISO para streaming adaptável de conteúdo de vídeo, que oferece benefícios significativos para quem deseja fornecer saída de streaming de vídeo adaptável de alta qualidade.</span><span class="sxs-lookup"><span data-stu-id="6df1b-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="6df1b-106">Com o MPEG-DASH, o fluxo de vídeo cairá automaticamente para uma definição inferior quando a rede ficar congestionada.</span><span class="sxs-lookup"><span data-stu-id="6df1b-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="6df1b-107">Dessa maneira, é menor a probabilidade de o vídeo ser pausado enquanto o player baixa os próximos segundos a serem reproduzidos (também conhecido como buffer).</span><span class="sxs-lookup"><span data-stu-id="6df1b-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="6df1b-108">À medida que o congestionamento de rede é reduzido, o player de vídeo retorna para um fluxo de qualidade mais alta.</span><span class="sxs-lookup"><span data-stu-id="6df1b-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="6df1b-109">Essa capacidade de adaptação da largura de banda necessária também resulta em um tempo de início mais rápido do vídeo.</span><span class="sxs-lookup"><span data-stu-id="6df1b-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="6df1b-110">Isso significa que os primeiros segundos podem ser reproduzidos em um segmento de qualidade inferior para rápido download e, em seguida, o vídeo passará a ter uma qualidade mais alta assim que conteúdo suficiente tiver sido armazenado em buffer.</span><span class="sxs-lookup"><span data-stu-id="6df1b-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="6df1b-111">O dash.js é um player de vídeo MPEG-DASH de software livre escrito em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6df1b-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="6df1b-112">Seu objetivo é fornecer um player robusto de plataforma cruzada que pode ser reutilizado livremente em aplicativos que exigem reprodução de vídeo.</span><span class="sxs-lookup"><span data-stu-id="6df1b-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="6df1b-113">Ele fornece reprodução de MPEG-DASH em qualquer navegador que dê suporte ao MSE (Media Source Extensions) da W3C, que hoje são o Chrome, o Microsoft Edge e o IE11 (outros navegadores demonstraram intenção de dar suporte ao MSE).</span><span class="sxs-lookup"><span data-stu-id="6df1b-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="6df1b-114">Para obter mais informações sobre o DASH.js, consulte o repositório do dash.js do GitHub.</span><span class="sxs-lookup"><span data-stu-id="6df1b-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="6df1b-115">Criando um player de vídeo de streaming com base no navegador</span><span class="sxs-lookup"><span data-stu-id="6df1b-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="6df1b-116">Para criar uma página da Web simples que exiba um player de vídeo com os controles esperados, como reproduzir, pausar, retroceder, etc., você precisará:</span><span class="sxs-lookup"><span data-stu-id="6df1b-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="6df1b-117">Criar uma página HTML</span><span class="sxs-lookup"><span data-stu-id="6df1b-117">Create an HTML page</span></span>
2. <span data-ttu-id="6df1b-118">Adicionar a marca de vídeo</span><span class="sxs-lookup"><span data-stu-id="6df1b-118">Add the video tag</span></span>
3. <span data-ttu-id="6df1b-119">Adicionar o player dash.js</span><span class="sxs-lookup"><span data-stu-id="6df1b-119">Add the dash.js player</span></span>
4. <span data-ttu-id="6df1b-120">Inicializar o player</span><span class="sxs-lookup"><span data-stu-id="6df1b-120">Initialize the player</span></span>
5. <span data-ttu-id="6df1b-121">Adicionar estilo CSS</span><span class="sxs-lookup"><span data-stu-id="6df1b-121">Add some CSS style</span></span>
6. <span data-ttu-id="6df1b-122">Exibir os resultados em um navegador que implemente o MSE</span><span class="sxs-lookup"><span data-stu-id="6df1b-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="6df1b-123">A inicialização do player pode ser concluída em algumas linhas de código do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6df1b-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="6df1b-124">Usando o dash.js, é realmente simples inserir vídeo MPEG-DASH em seus aplicativos baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="6df1b-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="6df1b-125">Criando uma página HTML</span><span class="sxs-lookup"><span data-stu-id="6df1b-125">Creating the HTML Page</span></span>
<span data-ttu-id="6df1b-126">A primeira etapa é criar uma página padrão HTML contendo o elemento **video**, salvar esse arquivo como basicPlayer.html, como ilustrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6df1b-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="6df1b-127">Adicionando o player DASH.js</span><span class="sxs-lookup"><span data-stu-id="6df1b-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="6df1b-128">Para adicionar a implementação de referência do dash.js ao aplicativo, você precisará obter o arquivo dash.all.js da versão 1.0 do projeto dash.js.</span><span class="sxs-lookup"><span data-stu-id="6df1b-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="6df1b-129">O arquivo deve ser salvo na pasta JavaScript do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6df1b-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="6df1b-130">Esse arquivo é um arquivo de conveniência que reúne todo o código dash.js necessário em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="6df1b-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="6df1b-131">Ao explorar o repositório do dash.js, você encontrará os arquivos individuais, o código de teste e muito mais, mas se tudo o que você quer é usar o dash.js, o arquivo dash.all.js é do que você precisa.</span><span class="sxs-lookup"><span data-stu-id="6df1b-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="6df1b-132">Para adicionar o player dash.js aos seus aplicativos, adicione uma marca de script à seção de cabeçalho do basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="6df1b-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="6df1b-133">Em seguida, crie uma função para inicializar o player quando a página for carregada.</span><span class="sxs-lookup"><span data-stu-id="6df1b-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="6df1b-134">Adicione o seguinte script após a linha na qual você carregou o dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="6df1b-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="6df1b-135">Primeiramente, essa função cria um DashContext.</span><span class="sxs-lookup"><span data-stu-id="6df1b-135">This function first creates a DashContext.</span></span> <span data-ttu-id="6df1b-136">Ele é usado para configurar o aplicativo para um ambiente de tempo de execução específico.</span><span class="sxs-lookup"><span data-stu-id="6df1b-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="6df1b-137">De um ponto de vista técnico, ele define as classes que a estrutura de injeção de dependência deve usar ao construir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6df1b-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="6df1b-138">Na maioria dos casos, você usará o Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="6df1b-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="6df1b-139">Em seguida, instancie a classe primária da estrutura dash.js, o MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="6df1b-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="6df1b-140">Essa classe contém os principais métodos necessários, como reproduzir e pausar, gerencia a relação com o elemento de vídeo e também gerencia a interpretação do arquivo MPD (Media Presentation Description) que descreve o vídeo a ser reproduzido.</span><span class="sxs-lookup"><span data-stu-id="6df1b-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="6df1b-141">A função startup() da classe MediaPlayer é chamada para garantir que o player esteja pronto para reproduzir o vídeo.</span><span class="sxs-lookup"><span data-stu-id="6df1b-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="6df1b-142">Entre outras coisas, essa função garante que todas as classes necessárias (conforme definido pelo contexto) tenham sido carregadas.</span><span class="sxs-lookup"><span data-stu-id="6df1b-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="6df1b-143">Assim que o vídeo estiver pronto, você poderá anexar o elemento de vídeo a ele usando a função attachView().</span><span class="sxs-lookup"><span data-stu-id="6df1b-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="6df1b-144">Isso permite que o MediaPlayer injete o fluxo de vídeo no elemento e também controle a reprodução conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="6df1b-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="6df1b-145">Passe a URL do arquivo MPD para o MediaPlayer de modo que este saiba sobre o vídeo que vai reproduzir. A função setupVideo() que acabou de ser criada precisará ser executada assim que a página tiver sido completamente carregada.</span><span class="sxs-lookup"><span data-stu-id="6df1b-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="6df1b-146">Faça isso usando o evento onload do elemento body.</span><span class="sxs-lookup"><span data-stu-id="6df1b-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="6df1b-147">Altere o elemento <body> para:</span><span class="sxs-lookup"><span data-stu-id="6df1b-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="6df1b-148">Por fim, defina o tamanho do elemento de vídeo usando CSS.</span><span class="sxs-lookup"><span data-stu-id="6df1b-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="6df1b-149">Em um ambiente de streaming adaptável, isso é importante principalmente porque o tamanho do vídeo que está sendo reproduzido pode mudar conforme a reprodução se adapta às condições em constante mudança da rede.</span><span class="sxs-lookup"><span data-stu-id="6df1b-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="6df1b-150">Nesta simples demonstração, basta forçar o elemento de vídeo a ser 80% da janela do navegador disponível adicionando o seguinte CSS à seção de cabeçalho da página:</span><span class="sxs-lookup"><span data-stu-id="6df1b-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="6df1b-151">Reproduzindo um vídeo</span><span class="sxs-lookup"><span data-stu-id="6df1b-151">Playing a Video</span></span>
<span data-ttu-id="6df1b-152">Para reproduzir um vídeo, aponte o navegador no arquivo basicPlayback.html e clique em Reproduzir no player de vídeo exibido.</span><span class="sxs-lookup"><span data-stu-id="6df1b-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6df1b-153">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="6df1b-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6df1b-154">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6df1b-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6df1b-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6df1b-155">See Also</span></span>
[<span data-ttu-id="6df1b-156">Desenvolver aplicativos de player de vídeo</span><span class="sxs-lookup"><span data-stu-id="6df1b-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="6df1b-157">Repositório do dash.js do GitHub</span><span class="sxs-lookup"><span data-stu-id="6df1b-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

