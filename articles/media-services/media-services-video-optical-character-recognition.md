---
title: Digitalizar o texto com o OCR do Azure Media Analytics | Microsoft Docs
description: "O OCR (reconhecimento óptico de caracteres) da Análise de Mídia do Azure permite que você converta o conteúdo de texto de arquivos de vídeo em texto digital editável e pesquisável.  Isso permite que você automatize a extração de metadados significativos do sinal de vídeo de sua mídia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 43f5b3a9bbec243e668c79702045094fcfedbdda
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="2ffd8-104">Usar a Análise de Mídia do Azure para converter o conteúdo de texto em arquivos de vídeo em texto digital</span><span class="sxs-lookup"><span data-stu-id="2ffd8-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="2ffd8-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2ffd8-105">Overview</span></span>
<span data-ttu-id="2ffd8-106">Se for necessário extrair o conteúdo de texto de seus arquivos de vídeo e gerar um texto digital editável e pesquisável, você deverá usar o OCR (reconhecimento óptico de caracteres) da Análise de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="2ffd8-107">Esse Processador de Mídia do Azure detecta o conteúdo de texto em seus arquivos de vídeo e gera arquivos de texto para seu uso.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="2ffd8-108">O OCR permite que você automatize a extração de metadados significativos do sinal de vídeo de sua mídia.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="2ffd8-109">Quando usado em conjunto com um mecanismo de pesquisa, você pode facilmente indexar sua mídia por texto e melhorar a capacidade de descoberta do seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="2ffd8-110">Isso é extremamente útil em vídeo altamente textual, como uma gravação de vídeo ou captura de tela de uma apresentação de slides.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="2ffd8-111">O Processador de Mídia OCR do Azure é otimizado para texto digital.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="2ffd8-112">O processador de mídia de **OCR de Mídia do Azure** atualmente está em Preview.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="2ffd8-113">Este tópico fornece detalhes sobre o **OCR de Mídia do Azure** e mostra como usá-lo com o SDK dos Serviços de Mídia para .NET.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-113">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="2ffd8-114">Para obter informações e exemplos adicionais, consulte [este blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="2ffd8-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="2ffd8-115">Arquivos de entrada de OCR</span><span class="sxs-lookup"><span data-stu-id="2ffd8-115">OCR input files</span></span>
<span data-ttu-id="2ffd8-116">Arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-116">Video files.</span></span> <span data-ttu-id="2ffd8-117">Atualmente, há suporte para os seguintes formatos: MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="2ffd8-118">Configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="2ffd8-118">Task configuration</span></span>
<span data-ttu-id="2ffd8-119">Configuração de tarefa (predefinição).</span><span class="sxs-lookup"><span data-stu-id="2ffd8-119">Task configuration (preset).</span></span> <span data-ttu-id="2ffd8-120">Ao criar uma tarefa com o **OCR de Mídia do Azure**, é necessário especificar uma predefinição de configuração usando JSON ou XML.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="2ffd8-121">O mecanismo de OCR demora apenas uma região de imagem com 40 pixels mínimos ao máximo 32.000 pixels como uma entrada válida na altura e na largura.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="2ffd8-122">Descrições de atributos</span><span class="sxs-lookup"><span data-stu-id="2ffd8-122">Attribute descriptions</span></span>
| <span data-ttu-id="2ffd8-123">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="2ffd8-123">Attribute name</span></span> | <span data-ttu-id="2ffd8-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ffd8-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="2ffd8-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="2ffd8-125">AdvancedOutput</span></span>| <span data-ttu-id="2ffd8-126">Se você definir AdvancedOutput como true, a saída JSON conterá dados posicionais para cada palavra (além de frases e regiões).</span><span class="sxs-lookup"><span data-stu-id="2ffd8-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="2ffd8-127">Se você não quiser ver esses detalhes, defina o sinalizador como false.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="2ffd8-128">O valor padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-128">The default value is false.</span></span> <span data-ttu-id="2ffd8-129">Para saber mais, confira [este blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="2ffd8-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="2ffd8-130">idioma</span><span class="sxs-lookup"><span data-stu-id="2ffd8-130">Language</span></span> |<span data-ttu-id="2ffd8-131">(opcional) descreve o idioma do texto a ser procurado.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="2ffd8-132">Um dos seguintes: AutoDetect (padrão), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="2ffd8-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="2ffd8-133">TextOrientation</span></span> |<span data-ttu-id="2ffd8-134">(opcional) descreve a orientação do texto a ser procurado.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="2ffd8-135">"Left" significa que a parte superior de todas as letras apontam para a esquerda.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="2ffd8-136">O texto padrão (como aquele que pode ser encontrado em um livro), tem a orientação “Up”.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="2ffd8-137">Um dos seguintes: AutoDetect (padrão), Up, Right, Down, Left.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="2ffd8-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="2ffd8-138">TimeInterval</span></span> |<span data-ttu-id="2ffd8-139">(opcional) descreve a taxa de amostragem.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="2ffd8-140">O padrão é a cada 1/2 segundo.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="2ffd8-141">Formato JSON – HH:mm:ss.SSS (padrão 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="2ffd8-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="2ffd8-142">Formato XML: duração primitiva do W3C XSD (padrão PT0.5)</span><span class="sxs-lookup"><span data-stu-id="2ffd8-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="2ffd8-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="2ffd8-143">DetectRegions</span></span> |<span data-ttu-id="2ffd8-144">(opcional) Uma matriz de objetos DetectRegion especificando regiões dentro do quadro de vídeo para detectar o texto.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="2ffd8-145">Um objeto DetectRegion é composto pelos quatro seguintes valores inteiros:</span><span class="sxs-lookup"><span data-stu-id="2ffd8-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="2ffd8-146">Left: pixels a partir da margem esquerda</span><span class="sxs-lookup"><span data-stu-id="2ffd8-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="2ffd8-147">Top: pixels a partir da margem superior</span><span class="sxs-lookup"><span data-stu-id="2ffd8-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="2ffd8-148">Width: altura da região em pixels</span><span class="sxs-lookup"><span data-stu-id="2ffd8-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="2ffd8-149">Height: altura da região em pixels</span><span class="sxs-lookup"><span data-stu-id="2ffd8-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="2ffd8-150">Exemplo de predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="2ffd8-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="2ffd8-151">Exemplo de predefinição XML</span><span class="sxs-lookup"><span data-stu-id="2ffd8-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="2ffd8-152">Arquivos de saída de OCR</span><span class="sxs-lookup"><span data-stu-id="2ffd8-152">OCR output files</span></span>
<span data-ttu-id="2ffd8-153">A saída do processador de mídia de OCR é um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="2ffd8-154">Elementos do arquivo JSON de saída</span><span class="sxs-lookup"><span data-stu-id="2ffd8-154">Elements of the output JSON file</span></span>
<span data-ttu-id="2ffd8-155">A saída de OCR de vídeo fornece dados segmentados por tempo sobre os caracteres encontrados no vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="2ffd8-156">Você pode usar atributos como idioma ou orientação para se concentrar exatamente nas palavras em que está interessado em analisar.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="2ffd8-157">A saída contém os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="2ffd8-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="2ffd8-158">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ffd8-158">Element</span></span> | <span data-ttu-id="2ffd8-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="2ffd8-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ffd8-160">Escala de tempo</span><span class="sxs-lookup"><span data-stu-id="2ffd8-160">Timescale</span></span> |<span data-ttu-id="2ffd8-161">"Tiques" por segundo do vídeo</span><span class="sxs-lookup"><span data-stu-id="2ffd8-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="2ffd8-162">Deslocamento</span><span class="sxs-lookup"><span data-stu-id="2ffd8-162">Offset</span></span> |<span data-ttu-id="2ffd8-163">diferença de tempo para carimbos de data/hora.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-163">time offset for timestamps.</span></span> <span data-ttu-id="2ffd8-164">Na versão 1.0 das APIs de Vídeo, sempre será 0.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="2ffd8-165">Taxa de quadros</span><span class="sxs-lookup"><span data-stu-id="2ffd8-165">Framerate</span></span> |<span data-ttu-id="2ffd8-166">Quadros por segundo do vídeo</span><span class="sxs-lookup"><span data-stu-id="2ffd8-166">Frames per second of the video</span></span> |
| <span data-ttu-id="2ffd8-167">width</span><span class="sxs-lookup"><span data-stu-id="2ffd8-167">width</span></span> |<span data-ttu-id="2ffd8-168">largura do vídeo em pixels</span><span class="sxs-lookup"><span data-stu-id="2ffd8-168">width of the video in pixels</span></span> |
| <span data-ttu-id="2ffd8-169">height</span><span class="sxs-lookup"><span data-stu-id="2ffd8-169">height</span></span> |<span data-ttu-id="2ffd8-170">altura do vídeo em pixels</span><span class="sxs-lookup"><span data-stu-id="2ffd8-170">height of the video in pixels</span></span> |
| <span data-ttu-id="2ffd8-171">Fragmentos</span><span class="sxs-lookup"><span data-stu-id="2ffd8-171">Fragments</span></span> |<span data-ttu-id="2ffd8-172">matriz de partes com base em tempo do vídeo nas quais os metadados estão em bloco</span><span class="sxs-lookup"><span data-stu-id="2ffd8-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="2ffd8-173">iniciar</span><span class="sxs-lookup"><span data-stu-id="2ffd8-173">start</span></span> |<span data-ttu-id="2ffd8-174">hora de início de um fragmento em "tiques"</span><span class="sxs-lookup"><span data-stu-id="2ffd8-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="2ffd8-175">duration</span><span class="sxs-lookup"><span data-stu-id="2ffd8-175">duration</span></span> |<span data-ttu-id="2ffd8-176">duração de um fragmento em "tiques"</span><span class="sxs-lookup"><span data-stu-id="2ffd8-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="2ffd8-177">intervalo</span><span class="sxs-lookup"><span data-stu-id="2ffd8-177">interval</span></span> |<span data-ttu-id="2ffd8-178">intervalo de cada evento dentro do fragmento determinado</span><span class="sxs-lookup"><span data-stu-id="2ffd8-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="2ffd8-179">events</span><span class="sxs-lookup"><span data-stu-id="2ffd8-179">events</span></span> |<span data-ttu-id="2ffd8-180">matriz que contém regiões</span><span class="sxs-lookup"><span data-stu-id="2ffd8-180">array containing regions</span></span> |
| <span data-ttu-id="2ffd8-181">region</span><span class="sxs-lookup"><span data-stu-id="2ffd8-181">region</span></span> |<span data-ttu-id="2ffd8-182">objeto representando palavras ou frases detectadas</span><span class="sxs-lookup"><span data-stu-id="2ffd8-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="2ffd8-183">Linguagem</span><span class="sxs-lookup"><span data-stu-id="2ffd8-183">language</span></span> |<span data-ttu-id="2ffd8-184">idioma do texto detectado dentro de uma região</span><span class="sxs-lookup"><span data-stu-id="2ffd8-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="2ffd8-185">orientation</span><span class="sxs-lookup"><span data-stu-id="2ffd8-185">orientation</span></span> |<span data-ttu-id="2ffd8-186">orientação do texto detectado dentro de uma região</span><span class="sxs-lookup"><span data-stu-id="2ffd8-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="2ffd8-187">lines</span><span class="sxs-lookup"><span data-stu-id="2ffd8-187">lines</span></span> |<span data-ttu-id="2ffd8-188">matriz de linhas de texto detectadas em uma região</span><span class="sxs-lookup"><span data-stu-id="2ffd8-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="2ffd8-189">texto</span><span class="sxs-lookup"><span data-stu-id="2ffd8-189">text</span></span> |<span data-ttu-id="2ffd8-190">o texto real</span><span class="sxs-lookup"><span data-stu-id="2ffd8-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="2ffd8-191">Exemplo de saída JSON</span><span class="sxs-lookup"><span data-stu-id="2ffd8-191">JSON output example</span></span>
<span data-ttu-id="2ffd8-192">O exemplo de saída a seguir contém as informações gerais de vídeo e vários fragmentos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="2ffd8-193">Em cada fragmento de vídeo, ele contém todas as regiões que são detectadas pelo MP de OCR com o idioma e sua orientação de texto.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-193">In every video fragment, it contains every region which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="2ffd8-194">A região também contém todas as linhas de palavras nessa região com texto da linha, posição da linha e todas as informações de palavra (conteúdo, posição e confiança da palavra) nesta linha.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="2ffd8-195">A seguir está um exemplo e coloquei alguns comentários embutidos.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-195">The following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="2ffd8-196">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="2ffd8-196">.NET sample code</span></span>

<span data-ttu-id="2ffd8-197">O programa a seguir mostra como:</span><span class="sxs-lookup"><span data-stu-id="2ffd8-197">The following program shows how to:</span></span>

1. <span data-ttu-id="2ffd8-198">Criar um ativo e carregar um arquivo de mídia nesse ativo.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="2ffd8-199">Crie um trabalho com um arquivo de configuração/predefinição de OCR.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="2ffd8-200">Baixe os arquivos JSON de saída.</span><span class="sxs-lookup"><span data-stu-id="2ffd8-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2ffd8-201">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ffd8-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2ffd8-202">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2ffd8-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="2ffd8-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2ffd8-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
    {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run the OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference to Azure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="2ffd8-204">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="2ffd8-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2ffd8-205">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="2ffd8-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="2ffd8-206">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="2ffd8-206">Related links</span></span>
[<span data-ttu-id="2ffd8-207">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="2ffd8-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

