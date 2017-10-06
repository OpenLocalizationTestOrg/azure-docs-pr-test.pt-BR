---
title: "texto aaaDigitize com OCR de análise de mídia do Azure | Microsoft Docs"
description: "OCR de análise de mídia do Azure (reconhecimento óptico de caracteres) permite que você tooconvert o conteúdo de texto em arquivos de vídeo em texto digital editável e pesquisável.  Isso permite a extração de saudação tooautomate de metadados significativo de sinal de vídeo de saudação da sua mídia."
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
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="9a9a5-104">Usar o conteúdo de texto de tooconvert de análise de mídia do Azure em arquivos de vídeo em texto digital</span><span class="sxs-lookup"><span data-stu-id="9a9a5-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="9a9a5-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9a9a5-105">Overview</span></span>
<span data-ttu-id="9a9a5-106">Se você precisa texto tooextract conteúdo de seus arquivos de vídeo e gerar um texto editável, pesquisável digital, você deve usar OCR de análise de mídia do Azure (reconhecimento óptico de caracteres).</span><span class="sxs-lookup"><span data-stu-id="9a9a5-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="9a9a5-107">Esse Processador de Mídia do Azure detecta o conteúdo de texto em seus arquivos de vídeo e gera arquivos de texto para seu uso.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="9a9a5-108">OCR permite que você tooautomate Olá extração de metadados significativo de sinal de vídeo de saudação da sua mídia.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="9a9a5-109">Quando usado em conjunto com um mecanismo de pesquisa, pode facilmente sua mídia de índice de texto e aumentar a capacidade de descoberta de saudação do seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="9a9a5-110">Isso é extremamente útil em vídeo altamente textual, como uma gravação de vídeo ou captura de tela de uma apresentação de slides.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="9a9a5-111">Olá processador de mídia do Azure OCR é otimizado para texto digital.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="9a9a5-112">Olá **OCR de mídia do Azure** processador de mídia está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="9a9a5-113">Este tópico fornece detalhes sobre **OCR de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="9a9a5-114">Para obter informações e exemplos adicionais, consulte [este blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="9a9a5-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="9a9a5-115">Arquivos de entrada de OCR</span><span class="sxs-lookup"><span data-stu-id="9a9a5-115">OCR input files</span></span>
<span data-ttu-id="9a9a5-116">Arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-116">Video files.</span></span> <span data-ttu-id="9a9a5-117">Atualmente, a saudação formatos a seguir têm suporte: MOV, MP4 e WMV.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="9a9a5-118">Configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="9a9a5-118">Task configuration</span></span>
<span data-ttu-id="9a9a5-119">Configuração de tarefa (predefinição).</span><span class="sxs-lookup"><span data-stu-id="9a9a5-119">Task configuration (preset).</span></span> <span data-ttu-id="9a9a5-120">Ao criar uma tarefa com o **OCR de Mídia do Azure**, é necessário especificar uma predefinição de configuração usando JSON ou XML.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="9a9a5-121">o mecanismo de OCR Olá tem apenas uma região da imagem com pixels de toomaximum 32000 40 pixels mínima como uma entrada válida em ambos os altura/largura.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="9a9a5-122">Descrições de atributos</span><span class="sxs-lookup"><span data-stu-id="9a9a5-122">Attribute descriptions</span></span>
| <span data-ttu-id="9a9a5-123">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9a9a5-123">Attribute name</span></span> | <span data-ttu-id="9a9a5-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="9a9a5-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="9a9a5-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="9a9a5-125">AdvancedOutput</span></span>| <span data-ttu-id="9a9a5-126">Se você definir AdvancedOutput tootrue, a saída JSON de saudação conterá dados posicionais para cada palavra única (em adição toophrases e regiões).</span><span class="sxs-lookup"><span data-stu-id="9a9a5-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="9a9a5-127">Se você não quiser toosee esses detalhes, defina Olá sinalizador toofalse.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="9a9a5-128">valor padrão de saudação é false.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-128">hello default value is false.</span></span> <span data-ttu-id="9a9a5-129">Para saber mais, confira [este blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="9a9a5-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="9a9a5-130">idioma</span><span class="sxs-lookup"><span data-stu-id="9a9a5-130">Language</span></span> |<span data-ttu-id="9a9a5-131">(opcional) descreve a linguagem de saudação do texto para o qual toolook.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="9a9a5-132">Um dos seguintes Olá: detecção automática (padrão), árabe, ChineseSimplified, chinês tradicional, dinamarquês tcheco, holandês, inglês, finlandês, francês, alemão, grego, húngaro, italiano, japonês, coreano, norueguês, polonês, português, romeno, russo, SerbianCyrillic, SerbianLatin, eslovaco, espanhol, sueco, turco.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="9a9a5-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="9a9a5-133">TextOrientation</span></span> |<span data-ttu-id="9a9a5-134">(opcional) descreve a orientação de saudação do texto para o qual toolook.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="9a9a5-135">"Esquerda" significa que Olá superior de todas as letras é apontada para a esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="9a9a5-136">O texto padrão (como aquele que pode ser encontrado em um livro), tem a orientação “Up”.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="9a9a5-137">Um dos seguintes Olá: detecção automática (padrão), para cima, à direita, à esquerda.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="9a9a5-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="9a9a5-138">TimeInterval</span></span> |<span data-ttu-id="9a9a5-139">(opcional) descreve a taxa de amostragem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="9a9a5-140">O padrão é a cada 1/2 segundo.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="9a9a5-141">Formato JSON – HH:mm:ss.SSS (padrão 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="9a9a5-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="9a9a5-142">Formato XML: duração primitiva do W3C XSD (padrão PT0.5)</span><span class="sxs-lookup"><span data-stu-id="9a9a5-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="9a9a5-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="9a9a5-143">DetectRegions</span></span> |<span data-ttu-id="9a9a5-144">(opcional) Uma matriz de objetos DetectRegion especificando regiões dentro de quadros do vídeo Olá na qual o texto toodetect.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="9a9a5-145">Um objeto DetectRegion é composto de saudação quatro valores de inteiro a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a9a5-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="9a9a5-146">Esquerda – pixels da margem esquerda Olá</span><span class="sxs-lookup"><span data-stu-id="9a9a5-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="9a9a5-147">Principais – pixels da margem superior Olá</span><span class="sxs-lookup"><span data-stu-id="9a9a5-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="9a9a5-148">Largura – largura da região de saudação em pixels</span><span class="sxs-lookup"><span data-stu-id="9a9a5-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="9a9a5-149">Altura – altura da região de saudação em pixels</span><span class="sxs-lookup"><span data-stu-id="9a9a5-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="9a9a5-150">Exemplo de predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="9a9a5-150">JSON preset example</span></span>

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


#### <a name="xml-preset-example"></a><span data-ttu-id="9a9a5-151">Exemplo de predefinição XML</span><span class="sxs-lookup"><span data-stu-id="9a9a5-151">XML preset example</span></span>
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

## <a name="ocr-output-files"></a><span data-ttu-id="9a9a5-152">Arquivos de saída de OCR</span><span class="sxs-lookup"><span data-stu-id="9a9a5-152">OCR output files</span></span>
<span data-ttu-id="9a9a5-153">saída de saudação do processador de mídia Olá OCR é um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="9a9a5-154">Elementos Olá JSON do arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="9a9a5-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="9a9a5-155">saída de vídeo OCR Hello fornece dados segmentados de tempo em caracteres hello encontrados no vídeo.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="9a9a5-156">Você pode usar atributos como o idioma ou orientação toohone no exatamente palavras Olá que você está interessado na análise.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="9a9a5-157">saída de Hello contém Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="9a9a5-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="9a9a5-158">Elemento</span><span class="sxs-lookup"><span data-stu-id="9a9a5-158">Element</span></span> | <span data-ttu-id="9a9a5-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="9a9a5-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9a9a5-160">Escala de tempo</span><span class="sxs-lookup"><span data-stu-id="9a9a5-160">Timescale</span></span> |<span data-ttu-id="9a9a5-161">"tiques" por segundo de vídeo Olá</span><span class="sxs-lookup"><span data-stu-id="9a9a5-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="9a9a5-162">Deslocamento</span><span class="sxs-lookup"><span data-stu-id="9a9a5-162">Offset</span></span> |<span data-ttu-id="9a9a5-163">diferença de tempo para carimbos de data/hora.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-163">time offset for timestamps.</span></span> <span data-ttu-id="9a9a5-164">Na versão 1.0 das APIs de Vídeo, sempre será 0.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="9a9a5-165">Taxa de quadros</span><span class="sxs-lookup"><span data-stu-id="9a9a5-165">Framerate</span></span> |<span data-ttu-id="9a9a5-166">Quadros por segundo do hello vídeo</span><span class="sxs-lookup"><span data-stu-id="9a9a5-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="9a9a5-167">width</span><span class="sxs-lookup"><span data-stu-id="9a9a5-167">width</span></span> |<span data-ttu-id="9a9a5-168">largura da saudação vídeo em pixels</span><span class="sxs-lookup"><span data-stu-id="9a9a5-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="9a9a5-169">height</span><span class="sxs-lookup"><span data-stu-id="9a9a5-169">height</span></span> |<span data-ttu-id="9a9a5-170">altura do vídeo em pixels da saudação</span><span class="sxs-lookup"><span data-stu-id="9a9a5-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="9a9a5-171">Fragmentos</span><span class="sxs-lookup"><span data-stu-id="9a9a5-171">Fragments</span></span> |<span data-ttu-id="9a9a5-172">matriz de blocos com base em tempo de vídeo no qual Olá metadados está em bloco</span><span class="sxs-lookup"><span data-stu-id="9a9a5-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="9a9a5-173">iniciar</span><span class="sxs-lookup"><span data-stu-id="9a9a5-173">start</span></span> |<span data-ttu-id="9a9a5-174">hora de início de um fragmento em "tiques"</span><span class="sxs-lookup"><span data-stu-id="9a9a5-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="9a9a5-175">duration</span><span class="sxs-lookup"><span data-stu-id="9a9a5-175">duration</span></span> |<span data-ttu-id="9a9a5-176">duração de um fragmento em "tiques"</span><span class="sxs-lookup"><span data-stu-id="9a9a5-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="9a9a5-177">intervalo</span><span class="sxs-lookup"><span data-stu-id="9a9a5-177">interval</span></span> |<span data-ttu-id="9a9a5-178">intervalo de cada evento no hello determinado por fragmento</span><span class="sxs-lookup"><span data-stu-id="9a9a5-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="9a9a5-179">events</span><span class="sxs-lookup"><span data-stu-id="9a9a5-179">events</span></span> |<span data-ttu-id="9a9a5-180">matriz que contém regiões</span><span class="sxs-lookup"><span data-stu-id="9a9a5-180">array containing regions</span></span> |
| <span data-ttu-id="9a9a5-181">region</span><span class="sxs-lookup"><span data-stu-id="9a9a5-181">region</span></span> |<span data-ttu-id="9a9a5-182">objeto representando palavras ou frases detectadas</span><span class="sxs-lookup"><span data-stu-id="9a9a5-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="9a9a5-183">Linguagem</span><span class="sxs-lookup"><span data-stu-id="9a9a5-183">language</span></span> |<span data-ttu-id="9a9a5-184">idioma do texto de saudação detectado dentro de uma região</span><span class="sxs-lookup"><span data-stu-id="9a9a5-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="9a9a5-185">orientation</span><span class="sxs-lookup"><span data-stu-id="9a9a5-185">orientation</span></span> |<span data-ttu-id="9a9a5-186">orientação do texto de saudação detectado dentro de uma região</span><span class="sxs-lookup"><span data-stu-id="9a9a5-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="9a9a5-187">lines</span><span class="sxs-lookup"><span data-stu-id="9a9a5-187">lines</span></span> |<span data-ttu-id="9a9a5-188">matriz de linhas de texto detectadas em uma região</span><span class="sxs-lookup"><span data-stu-id="9a9a5-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="9a9a5-189">texto</span><span class="sxs-lookup"><span data-stu-id="9a9a5-189">text</span></span> |<span data-ttu-id="9a9a5-190">texto real da saudação</span><span class="sxs-lookup"><span data-stu-id="9a9a5-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="9a9a5-191">Exemplo de saída JSON</span><span class="sxs-lookup"><span data-stu-id="9a9a5-191">JSON output example</span></span>
<span data-ttu-id="9a9a5-192">Olá saída exemplo a seguir contém informações gerais de vídeo hello e vários fragmentos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="9a9a5-193">Em cada fragmento do vídeo, ele contém todas as regiões que é detectada pelo OCR MP com idioma hello e sua orientação de texto.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="9a9a5-194">região Olá também contém todas as linhas word nesta região com o texto da linha hello, posição da linha hello e todas as informações de palavra (conteúdo do word, posição e confiança) nesta linha.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="9a9a5-195">Olá seguinte é um exemplo e coloquei embutido alguns comentários.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-195">hello following is an example, and I put some comments inline.</span></span>

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
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
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

## <a name="net-sample-code"></a><span data-ttu-id="9a9a5-196">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="9a9a5-196">.NET sample code</span></span>

<span data-ttu-id="9a9a5-197">a seguir Olá programa mostra como:</span><span class="sxs-lookup"><span data-stu-id="9a9a5-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="9a9a5-198">Criar um ativo e carregar um arquivo de mídia no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="9a9a5-199">Crie um trabalho com um arquivo de configuração/predefinição de OCR.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="9a9a5-200">Baixe os arquivos de saída do JSON hello.</span><span class="sxs-lookup"><span data-stu-id="9a9a5-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9a9a5-201">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a9a5-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="9a9a5-202">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9a9a5-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="9a9a5-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="9a9a5-203">Example</span></span>

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
            // Read values from hello App.config file.
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="9a9a5-204">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="9a9a5-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9a9a5-205">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="9a9a5-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="9a9a5-206">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="9a9a5-206">Related links</span></span>
[<span data-ttu-id="9a9a5-207">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="9a9a5-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

