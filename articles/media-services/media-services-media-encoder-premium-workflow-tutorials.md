---
title: "tutoriais de fluxo de trabalho Premium de codificador de mídia aaaAvanced"
description: "Este documento contém instruções passo a passo que mostram como tooperform avançado tarefas de fluxo de trabalho Premium de codificador de mídia e também como toocreate fluxos de trabalho complexos com o Designer de fluxo de trabalho."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="5f5b4-103">Tutoriais avançados do fluxo de trabalho do Codificador de Mídia Premium</span><span class="sxs-lookup"><span data-stu-id="5f5b4-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="5f5b4-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5f5b4-104">Overview</span></span>
<span data-ttu-id="5f5b4-105">Este documento contém instruções passo a passo que mostram como fluxos de trabalho toocustomize com **Designer de fluxo de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="5f5b4-106">Você pode encontrar os arquivos de fluxo de trabalho real Olá [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="5f5b4-107">SUMÁRIO</span><span class="sxs-lookup"><span data-stu-id="5f5b4-107">TOC</span></span>
<span data-ttu-id="5f5b4-108">Olá seguintes tópicos é abordado:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="5f5b4-109">Codificando MXF em um MP4 de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="5f5b4-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="5f5b4-110">Iniciando um novo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="5f5b4-111">Usando Olá entrada de arquivo de mídia</span><span class="sxs-lookup"><span data-stu-id="5f5b4-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="5f5b4-112">Inspecionando fluxos de mídia</span><span class="sxs-lookup"><span data-stu-id="5f5b4-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="5f5b4-113">Adicionando um codificador de vídeo para geração de arquivo .MP4</span><span class="sxs-lookup"><span data-stu-id="5f5b4-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="5f5b4-114">Fluxo de áudio Olá codificação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="5f5b4-115">Multiplexando fluxos de áudio e de vídeo em um contêiner MP4</span><span class="sxs-lookup"><span data-stu-id="5f5b4-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="5f5b4-116">Gravar o arquivo MP4 de saudação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="5f5b4-117">Criar um ativo de serviços de mídia do arquivo de saída Olá</span><span class="sxs-lookup"><span data-stu-id="5f5b4-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="5f5b4-118">Saudação de teste terminar o fluxo de trabalho localmente</span><span class="sxs-lookup"><span data-stu-id="5f5b4-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="5f5b4-119">Codificando MXF em MP4s com várias taxas bits - empacotamento dinâmico habilitado</span><span class="sxs-lookup"><span data-stu-id="5f5b4-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="5f5b4-120">Adicionando uma ou mais saídas MP4</span><span class="sxs-lookup"><span data-stu-id="5f5b4-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="5f5b4-121">Configurar nomes de saída do arquivo hello</span><span class="sxs-lookup"><span data-stu-id="5f5b4-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="5f5b4-122">Adicionando uma Trilha de Áudio separada</span><span class="sxs-lookup"><span data-stu-id="5f5b4-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="5f5b4-123">Adicionando hello. Arquivo SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="5f5b4-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="5f5b4-124">Codificando MXF em MP4 com várias taxas de bit - plano gráfico aprimorado</span><span class="sxs-lookup"><span data-stu-id="5f5b4-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="5f5b4-125">Tooenhance de visão geral do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="5f5b4-126">Convenções de nomenclatura do arquivo</span><span class="sxs-lookup"><span data-stu-id="5f5b4-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="5f5b4-127">Propriedades de componente na raiz de fluxo de trabalho de saudação de publicação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="5f5b4-128">Faça com que os nomes de arquivo de saída gerados dependam dos valores de propriedade publicados</span><span class="sxs-lookup"><span data-stu-id="5f5b4-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="5f5b4-129">Adicionando a saída de MP4 toomultibitrate miniaturas</span><span class="sxs-lookup"><span data-stu-id="5f5b4-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="5f5b4-130">Miniaturas de tooadd de visão geral do fluxo de trabalho para</span><span class="sxs-lookup"><span data-stu-id="5f5b4-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="5f5b4-131">Adicionando codificação JPG</span><span class="sxs-lookup"><span data-stu-id="5f5b4-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="5f5b4-132">Lidando com a conversão de espaço de cor</span><span class="sxs-lookup"><span data-stu-id="5f5b4-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="5f5b4-133">Miniaturas de saudação de gravação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="5f5b4-134">Detectando erros em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="5f5b4-135">Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="5f5b4-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="5f5b4-136">Corte baseado em tempo da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="5f5b4-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="5f5b4-137">Toostart de visão geral do fluxo de trabalho adicionando restrições para</span><span class="sxs-lookup"><span data-stu-id="5f5b4-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="5f5b4-138">Usando Olá filtro de fluxo</span><span class="sxs-lookup"><span data-stu-id="5f5b4-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="5f5b4-139">Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="5f5b4-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="5f5b4-140">Apresentando o hello componente script</span><span class="sxs-lookup"><span data-stu-id="5f5b4-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="5f5b4-141">Criando scripts em um fluxo de trabalho: hello world</span><span class="sxs-lookup"><span data-stu-id="5f5b4-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="5f5b4-142">Corte baseado em quadro da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="5f5b4-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="5f5b4-143">Plano gráfico toostart visão geral sobre a adição de corte para</span><span class="sxs-lookup"><span data-stu-id="5f5b4-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="5f5b4-144">Usando Olá Clip lista XML</span><span class="sxs-lookup"><span data-stu-id="5f5b4-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="5f5b4-145">Modificando a lista de saudação do clipe de um componente script</span><span class="sxs-lookup"><span data-stu-id="5f5b4-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="5f5b4-146">Adicionando uma propriedade de conveniência ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="5f5b4-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="5f5b4-147"><a id="MXF_to_MP4"></a>Codificando MXF em um MP4 de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="5f5b4-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="5f5b4-148">Neste passo a passo, criaremos um arquivo MP4 de taxa de bits única com áudio codificado em AAC-HE a partir de um arquivo de entrada .MXF.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="5f5b4-149"><a id="MXF_to_MP4_start_new"></a>Iniciando um novo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="5f5b4-150">Abra o Designer de Fluxo de Trabalho e selecione "Arquivo" - "Novo Espaço de Trabalho" - "Transcodificar Esquema"</span><span class="sxs-lookup"><span data-stu-id="5f5b4-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="5f5b4-151">Olá novo fluxo de trabalho mostrará 3 elementos:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="5f5b4-152">Arquivo de Origem Principal</span><span class="sxs-lookup"><span data-stu-id="5f5b4-152">Primary Source File</span></span>
* <span data-ttu-id="5f5b4-153">XML da Lista de Clipes</span><span class="sxs-lookup"><span data-stu-id="5f5b4-153">Clip List XML</span></span>
* <span data-ttu-id="5f5b4-154">Arquivo/Ativo de Saída</span><span class="sxs-lookup"><span data-stu-id="5f5b4-154">Output File/Asset</span></span>  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="5f5b4-156">*Novo fluxo de trabalho de codificação*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="5f5b4-157"><a id="MXF_to_MP4_with_file_input"></a>Usando Olá entrada de arquivo de mídia</span><span class="sxs-lookup"><span data-stu-id="5f5b4-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="5f5b4-158">Em ordem tooaccept nosso arquivo de mídia de entrada, uma começa com a adição de um componente de entrada de arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="5f5b4-159">tooadd um fluxo de trabalho toohello de componente, procure-a na caixa de pesquisa de repositório hello e arrastar entrada hello desejado no painel de designer do hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="5f5b4-160">Faça isso para Olá entrada de arquivo de mídia e conecte Olá arquivo fonte primário componente toohello Filename pino de entrada de saudação entrada de arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Entrada do Arquivo de Mídia conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="5f5b4-162">*Entrada do Arquivo de Mídia conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-162">*Connected Media File Input*</span></span>

<span data-ttu-id="5f5b4-163">Para que possa fazer muito mais do que, primeiro precisaremos designer de fluxo de trabalho toohello tooindicate o arquivo de exemplo gostaríamos toouse toodesign nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="5f5b4-164">toodo assim, clique em segundo plano do painel designer hello e procure a propriedade de arquivo de origem primário Olá no painel de propriedade direito hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="5f5b4-165">Clique no ícone de pasta hello e selecione Olá desejado arquivo tootest Olá fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="5f5b4-166">Assim que isso for feito, o componente de entrada de arquivo de mídia Olá inspecionar o arquivo hello e preencher sua saída pins tooreflect Olá arquivo, que ele inspecionado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Entrada do Arquivo de Mídia preenchida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="5f5b4-168">*Entrada do Arquivo de Mídia preenchida*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-168">*Populated Media File Input*</span></span>

<span data-ttu-id="5f5b4-169">Enquanto isso Especifica com qual entrada que gostaríamos toowork com, ela não informa ainda em que a saída de hello codificado deve ir para.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="5f5b4-170">Semelhante Olá toohow principal arquivo de origem foi configurado, configure Olá propriedade da variável de pasta de saída, logo abaixo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Propriedades de Entrada e Saída configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="5f5b4-172">*Propriedades de Entrada e Saída configuradas*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="5f5b4-173"><a id="MXF_to_MP4_streams"></a>Inspecionando fluxos de mídia</span><span class="sxs-lookup"><span data-stu-id="5f5b4-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="5f5b4-174">Geralmente é preferível tooknow fluxo Olá aparência desse flui pelo fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="5f5b4-175">tooinspect um fluxo em qualquer ponto no fluxo de trabalho hello, basta clicar uma saída ou entrada de pin em qualquer um dos componentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="5f5b4-176">Nesse caso, tente clicar em Olá pino de saída de vídeo descompactado da nossa entrada de arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="5f5b4-177">Uma caixa de diálogo será aberta que permite que o vídeo de saída de hello tooinspect.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Inspecionando pino de saída de vídeo descompactado Olá](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="5f5b4-179">*Inspecionando pino de saída de vídeo descompactado Olá*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="5f5b4-180">Em nosso caso, ele nos informa, por exemplo, que estamos lidando com uma entrada de 1920 x 1080 a 24 quadros por segundo em uma amostragem de 4:2:2 de um vídeo de quase 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="5f5b4-181"><a id="MXF_to_MP4_file_generation"></a>Adicionando um codificador de vídeo para geração de arquivo .MP4</span><span class="sxs-lookup"><span data-stu-id="5f5b4-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="5f5b4-182">Observe que, agora, um pino de saída Vídeo Descompactado e vários pinos de saída Áudio Descompactados estão disponíveis para uso em nossa Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="5f5b4-183">Em ordem tooencode Olá vídeo de entrada, precisamos de um componente de codificação - nesse caso para gerar. Arquivos MP4.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="5f5b4-184">tooencode Olá tooH.264 do fluxo de vídeo, adicione a superfície do designer de toohello Olá AVC codificador de vídeo componente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="5f5b4-185">Esse componente recebe um fluxo de vídeo descompactado como entrada e fornece um fluxo de vídeo compactado AVC em seu pino de saída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Codificador AVC desconectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="5f5b4-187">*Codificador AVC desconectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="5f5b4-188">Suas propriedades determinam como exatamente Olá codificação acontece.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="5f5b4-189">Vamos dar uma olhada em algumas Olá configurações mais importantes:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="5f5b4-190">Largura de saída e a altura de saída: esses determinam a resolução de saudação do vídeo Olá codificado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="5f5b4-191">Em nosso caso, usaremos 640 x 360</span><span class="sxs-lookup"><span data-stu-id="5f5b4-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="5f5b4-192">Taxa de quadros: quando toopassthrough conjunto será apenas adotar a taxa de quadros de origem Olá, é possível toooverride esta aqui.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="5f5b4-193">Observe que essa conversão de taxa de quadros não tem compensação de movimento.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="5f5b4-194">Nível e perfil: eles determinam perfil Olá AVC e nível.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="5f5b4-195">tooconveniently obter mais informações sobre Olá diferentes níveis e os perfis, clique em ícone de ponto de interrogação Olá no componente de codificador de vídeo AVC hello e página de ajuda de saudação mostrará mais detalhes sobre cada um dos níveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="5f5b4-196">Em nosso exemplo, vamos Escolher perfil principal no nível 3.2 (padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="5f5b4-197">Modo de Controle de Taxa e Taxa de bits (kbps): em nosso cenário, optamos por uma saída de taxa de bits constante (CBR) de 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="5f5b4-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="5f5b4-198">Formato de vídeo: trata-se Olá VUI (informações de uso do vídeo) que é gravado no fluxo de h. 264 hello (informações sobre o que pode ser usado por uma exibição de saudação do decodificador tooenhance, mas não essencial toocorrectly decodificar):</span><span class="sxs-lookup"><span data-stu-id="5f5b4-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="5f5b4-199">NTSC (normalmente para os Estados Unidos ou o Japão, usando 30 qps)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="5f5b4-200">PAL (normalmente para a Europa, usando 25 qps)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="5f5b4-201">Modo de Tamanho de GOP: configuraremos o Tamanho de GOP Fixo para nossos objetivos com um Intervalo de Chave de dois segundos com GOPs Fechados.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="5f5b4-202">Isso assegura a compatibilidade com hello que fornece serviços de mídia do empacotamento dinâmico do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="5f5b4-203">toofeed nossa codificador AVC, conectar pino de saída de vídeo descompactado saudação do hello entrada de arquivo de mídia componente toohello vídeo descompactado pino de entrada do codificador Olá AVC.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="5f5b4-205">*Codificador Principal de AVC conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="5f5b4-206"><a id="MXF_to_MP4_audio"></a>Fluxo de áudio Olá codificação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="5f5b4-207">Neste ponto, podemos ter codificado vídeo mas fluxo de áudio descompactados original Olá ainda precisa toobe compactado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="5f5b4-208">Para isso vamos com AAC codificação por Olá componente AAC codificador (Dolby).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="5f5b4-209">Adicione-o fluxo de trabalho toohello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-209">Add it toohello workflow.</span></span>

![Codificador AVC desconectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="5f5b4-211">*Codificador AAC desconectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="5f5b4-212">Agora há uma incompatibilidade: há apenas um único descompactado áudio entrado pin de saudação AAC codificador enquanto mais do que provavelmente Olá entrada de arquivo de mídia terá dois descompactados disponíveis de fluxo de áudio: uma para Olá deixado canal de áudio e outro para Olá Certo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="5f5b4-213">(Se você estiver lidando com som surround, serão seis canais). Portanto, não é possível toodirectly conecte áudio Olá da fonte de entrada de arquivo de mídia Olá codificador de áudio Olá AAC.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="5f5b4-214">componente AAC Hello espera um fluxo de áudio chamado "intercalado": um único fluxo que tem ambos Olá esquerda e hello canais corretos intercalados entre si.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="5f5b4-215">Já sabemos do nosso arquivo de mídia de origem que faixas de áudio em qual posição na origem hello, podemos gerar esse fluxo de áudio Intercalado com hello corretamente recebem posições locutor para a esquerda e direita.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="5f5b4-216">Primeiro um desejará toogenerated um fluxo intercalado de canais de áudio de origem Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="5f5b4-217">componente de Interleaver de fluxo de áudio de saudação tratará isso para nós.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="5f5b4-218">Adicioná-lo toohello de fluxo de trabalho e se conectar a saídas de áudio de saudação do hello entrada de arquivo de mídia para ele.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Intercalador do fluxo de áudio conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="5f5b4-220">*Intercalador do fluxo de áudio conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="5f5b4-221">Agora que temos um fluxo de áudio intercalado, ainda não especificamos onde tooassign Olá esquerdo ou direito dos alto-falantes posições à.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="5f5b4-222">Em ordem toospecify isso, podemos aproveitar Olá locutor cedente de posição.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Adicionando um Atribuidor de Posição do Alto-falante](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="5f5b4-224">*Adicionando um Atribuidor de Posição do Alto-falante*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="5f5b4-225">Configurar Olá locutor posição cedente para uso com um fluxo de entrada estéreo por meio de um filtro de predefinição de codificador de "Custom" e Olá canal predefinido chamado "2.0 (L, R)".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="5f5b4-226">(Isso atribuirá Olá locutor esquerdo posição toochannel 1 e Olá locutor certa posição toochannel 2.)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="5f5b4-227">Conecte a saída de saudação do toohello entrada locutor posição cedente Olá Olá AAC codificador.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="5f5b4-228">Em seguida, conte-Olá AAC codificador toowork com um "2.0 (L, R)" canal predefinidos, para que ele saiba toodeal com áudio estéreo como entrada.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="5f5b4-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexando fluxos de áudio e de vídeo em um contêiner MP4</span><span class="sxs-lookup"><span data-stu-id="5f5b4-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="5f5b4-230">Com base em nosso fluxo de vídeo codificado em AVC e em nosso fluxo de áudio codificado em AAC, podemos capturar ambos em um contêiner .MP4.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="5f5b4-231">processo de saudação de combinação de fluxos diferentes em uma única é chamado de "multiplexação" (ou "muxing").</span><span class="sxs-lookup"><span data-stu-id="5f5b4-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="5f5b4-232">Nesse caso, está intercalação hello e Olá vídeo fluxos de áudio em uma única coerente. Pacote de MP4.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="5f5b4-233">componente de saudação que coordena isso para um. Olá multiplexador ISO MPEG-4 é chamado de contêiner MP4.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="5f5b4-234">Adicione uma superfície de designer toohello e conecte Olá AVC codificador de vídeo e entradas de tooits AAC codificador hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Multiplexador MPEG4 conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="5f5b4-236">*Multiplexador MPEG4 conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="5f5b4-237"><a id="MXF_to_MP4_writing_mp4"></a>Gravar o arquivo MP4 de saudação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="5f5b4-238">Ao gravar um arquivo de saída, o componente de saída de arquivo hello é usado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="5f5b4-239">Podemos pode se conectar esta saída toohello de saudação multiplexador ISO MPEG-4 para que a saída é gravada toodisk.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="5f5b4-240">toodo, conectar Olá contêiner (MPEG-4) pin toohello gravação entrado pino de saída de hello arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Saída do arquivo conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="5f5b4-242">*Saída do arquivo conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-242">*Connected File Output*</span></span>

<span data-ttu-id="5f5b4-243">Olá nome do arquivo que será usado é determinado pelo Olá propriedade de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="5f5b4-244">Enquanto essa propriedade pode ser codificado tooa valor, um provavelmente desejarão tooset-lo por meio de uma expressão em vez disso.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="5f5b4-245">fluxo de trabalho toohave Olá determinar automaticamente a saída de hello arquivo de propriedade de nome de uma expressão, clique em Olá botão próximo toohello nome de arquivo (ícone de pasta próximo toohello).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="5f5b4-246">No hello menu suspenso e selecione "Expressão".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="5f5b4-247">Isso abrirá o editor de expressão hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="5f5b4-248">Limpe o conteúdo de saudação do editor de saudação primeiro.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-248">Clear hello contents of hello editor first.</span></span>

![Editor de expressão vazio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="5f5b4-250">*Editor de expressão vazio*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="5f5b4-251">editor de expressão Olá permite tooenter qualquer valor literal, combinado com uma ou mais variáveis.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="5f5b4-252">As variáveis começam com um sinal de cifrão.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="5f5b4-253">Conforme você pressionar a tecla de $ de hello, editor de saudação mostrará uma caixa suspensa com uma opção de variáveis disponíveis.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="5f5b4-254">Em nosso caso, usaremos uma combinação de variável de diretório de saída de hello e variável de nome de arquivo base de entrada hello:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Editor de expressão preenchido](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="5f5b4-256">*Editor de expressão preenchido*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="5f5b4-257">Em ordem toosee ver um arquivo de saída do seu trabalho de codificação no Azure, você deve fornecer um valor no editor de expressão hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="5f5b4-258">Quando você confirmar expressão Olá atingindo okey, janela de propriedade Olá visualizará toowhat valor Olá arquivo propriedade resolve neste momento.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![Diretório de saída de resolução da Expressão do Arquivo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="5f5b4-260">*Diretório de saída de resolução da Expressão do Arquivo*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="5f5b4-261"><a id="MXF_to_MP4_asset_from_output"></a>Criar um ativo de serviços de mídia do arquivo de saída Olá</span><span class="sxs-lookup"><span data-stu-id="5f5b4-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="5f5b4-262">Enquanto estamos foram gravadas, um arquivo de saída de MP4, ainda precisamos tooindicate este arquivo pertence toohello ativo quais serviços de mídia irá gerar como resultado da execução deste fluxo de trabalho de saída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="5f5b4-263">toothis final, o nó de arquivo/ativo de saída Olá na tela de fluxo de trabalho de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="5f5b4-264">Todos os arquivos de entrada para esse nó se tornará parte do hello resultante do Azure Media Services ativo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="5f5b4-265">Conecte-se Olá saída de arquivo componente toohello ativo/arquivo de saída componente toofinish Olá fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="5f5b4-267">*Fluxo de trabalho concluído*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-267">*Finished Workflow*</span></span>

### <span data-ttu-id="5f5b4-268"><a id="MXF_to_MP4_test"></a>Saudação de teste terminar o fluxo de trabalho localmente</span><span class="sxs-lookup"><span data-stu-id="5f5b4-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="5f5b4-269">tootest Olá fluxo de trabalho localmente, pressione o botão de reprodução de Olá na barra de ferramentas de saudação na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="5f5b4-270">Quando o fluxo de trabalho Olá terminar a execução, inspecione saída Olá gerada na pasta de saída de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="5f5b4-271">Você verá Olá terminar o arquivo de saída de MP4 que foi codificado Olá MXF entrada do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="5f5b4-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codificação do MXF em MP4 - empacotamento dinâmico com várias taxas bits habilitado</span><span class="sxs-lookup"><span data-stu-id="5f5b4-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="5f5b4-273">Neste passo a passo, criaremos um conjunto de arquivos MP4 com várias taxas de bits e áudio codificado em AAC a partir de um único arquivo de entrada .MXF.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="5f5b4-274">Quando uma saída de ativo de múltiplas taxas de bits for desejada para uso em combinação com recursos de empacotamento dinâmico Olá oferecidos pelo Azure Media Services, vários arquivos MP4 com alinhamento GOP de cada uma taxa de bits diferente e a resolução precisará toobe gerado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="5f5b4-275">Assim, Olá toodo [MXF codificação em uma taxa de bits única MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) passo a passo fornece um bom ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Como iniciar o fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="5f5b4-277">*Como iniciar o fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-277">*Starting Workflow*</span></span>

### <span data-ttu-id="5f5b4-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adicionando uma ou mais saídas MP4</span><span class="sxs-lookup"><span data-stu-id="5f5b4-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="5f5b4-279">Cada arquivo MP4 em nosso ativo resultante dos Serviços de Mídia do Azure oferecerá suporte a uma taxa de bits e resolução diferentes.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="5f5b4-280">Vamos adicionar um ou mais MP4 saída arquivos toohello fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="5f5b4-281">toomake-se de que temos todos os codificadores de vídeos criados com Olá mesmas configurações, é mais conveniente tooduplicate Olá codificador de vídeo AVC já existente e configure outra combinação de resolução e taxa de bits (vamos adicionar um 960 x 540 25 quadros por segundo 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="5f5b4-282">codificador existente do tooduplicate hello, cópia colá-lo na superfície de designer hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="5f5b4-283">Conecte-se Olá pino de saída de vídeo descompactado da saudação entrada de arquivo de mídia em nosso novo componente AVC.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Segundo codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="5f5b4-285">*Segundo codificador AVC conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="5f5b4-286">Agora adapte configuração Olá para toooutput de codificador AVC nosso novo 960 x 540 a 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="5f5b4-287">(Use as propriedades "Largura de saída", "Altura de saída" e "Taxa de bits (kbps)" para isso).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="5f5b4-288">Considerando que desejamos toouse ativo resultante do hello junto com o empacotamento dinâmico do Azure Media Services, Olá ponto de extremidade de streaming necessidades toobe capaz de gerar desses arquivos MP4 fragmentos HLS/fragmentado MP4/DASH que são exatamente alinhado tooeach outro de forma que os clientes que estiver alternando entre diferentes taxas de bits obtém uma único smooth contínua áudio e vídeo experiência.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="5f5b4-289">toomake que acontecem, precisamos tooensure que, nas propriedades de saudação do codificadores AVC está definido Olá tamanho GOP ("grupo de imagens") para os dois arquivos MP4 too2 segundos, que podem ser feitos por:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="5f5b4-290">Definindo o tamanho de GOP Olá GOP tamanho modo tooFixed e</span><span class="sxs-lookup"><span data-stu-id="5f5b4-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="5f5b4-291">segundos de tootwo de intervalo de quadro chave Hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="5f5b4-292">também definir Olá GOP IDR controle tooClosed GOP tooensure GOP todos está aguardando em seus próprios sem dependências</span><span class="sxs-lookup"><span data-stu-id="5f5b4-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="5f5b4-293">toomake nossa toounderstand conveniente de fluxo de trabalho, renomear o codificador de AVC primeiro Olá muito "codificador de vídeo AVC 640x360 1200kbps" e Olá codificador do segundo AVC "codificador de vídeo AVC 960 x 540 kbps 2500".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="5f5b4-294">Agora, adicione um segundo Multiplexador ISO MPEG-4 e uma segunda Saída de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="5f5b4-295">Conecte Olá multiplexador toohello novo AVC codificador e verifique se que a saída é direcionada para Olá saída de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="5f5b4-296">Também se conectar Olá AAC codificador de áudio saída toohello nova entrada da multiplexador.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="5f5b4-297">Olá saída de arquivo por sua vez pode ser conectado toohello ativo/arquivo de saída nó tooadd-toohello ativo de serviços de mídia que será criado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Segundo Muxer e Saída do arquivo conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="5f5b4-299">*Segundo Muxer e Saída do arquivo conectado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="5f5b4-300">Para compatibilidade com o empacotamento dinâmico dos serviços de mídia do Azure, configure a contagem de tooGOP de modo de bloco de saudação do multiplexador ou duração e defina Olá GOPs por too1 parte.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="5f5b4-301">(Isso deve ser o padrão de hello.)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-301">(This should be hello default.)</span></span>

![Modos de parte do muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="5f5b4-303">*Modos de parte do muxer*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="5f5b4-304">Observação: talvez você queira toorepeat esse processo para qualquer taxa de bits e resolução de combinações de toohave adicionado toohello saída de ativo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="5f5b4-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configurar nomes de saída do arquivo hello</span><span class="sxs-lookup"><span data-stu-id="5f5b4-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="5f5b4-306">Temos mais de um ativo de saída de arquivo único adicionado toohello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="5f5b4-307">Isso fornece uma saudação-se de necessidade toomake nomes de arquivos para cada Olá saída arquivos são diferentes uns dos outros e talvez até mesmo se aplica uma convenção de nomenclatura de arquivo portanto fica claro saudação do nome de arquivo que você está lidando com.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="5f5b4-308">Nomenclatura de arquivos de saída pode ser controlado por meio de expressões no designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="5f5b4-309">Abrir o painel de propriedade Olá para um dos componentes de saída de arquivo hello e abrir editor de expressão de saudação do hello propriedade de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="5f5b4-310">Nosso primeiro arquivo de saída foi configurado por meio de saudação expressão a seguir (consulte o tutorial Olá para indo de [taxa de bits única saída MP4 do MXF tooa](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="5f5b4-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="5f5b4-311">Isso significa que nossa filename é determinada por duas variáveis: Olá saída toowrite directory no e hello nome base do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="5f5b4-312">antiga Olá é exposta como uma propriedade na raiz de fluxo de trabalho hello e Olá esta última é determinada pelo arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="5f5b4-313">Observe que esse diretório de saída Olá é usada para teste local. Essa propriedade será substituída pelo mecanismo de fluxo de trabalho hello quando o fluxo de trabalho de saudação é executado pelo processador de mídia com base em nuvem Olá nos serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="5f5b4-314">toogive ambos os arquivos de nossa saída uma saída consistente de nomenclatura, alteração Olá primeiro arquivo nomenclatura expressão para:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="5f5b4-315">e o segundo Olá para:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="5f5b4-316">Execução de um teste intermediário toomake-se de que ambos os arquivos de saída de MP4 gerados corretamente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="5f5b4-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adicionando uma Trilha de Áudio separada</span><span class="sxs-lookup"><span data-stu-id="5f5b4-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="5f5b4-318">Como veremos mais tarde quando geramos uma toogo de arquivo. ISM com os arquivos de saída de MP4, nós também exigirá um arquivo MP4 somente de áudio como faixa de áudio Olá para nosso streaming adaptável.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="5f5b4-319">toocreate esse arquivo, adicione um fluxo de trabalho do muxer adicionais toohello (ISO-MPEG-4 multiplexador) e conecte-se o pino de saída do codificador do hello AAC com seu pin de entrada para acompanhar 1.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Muxer de áudio adicionado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="5f5b4-321">*Muxer de áudio adicionado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="5f5b4-322">Criar um fluxo de saída do arquivo de saída componente toooutput Olá terceiro de saudação muxer e configure a expressão de nomenclatura de arquivo hello como:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Criação de Saída do arquivo pelo muxer de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="5f5b4-324">*Criação de Saída do arquivo pelo muxer de áudio*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="5f5b4-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adicionando hello. Arquivo SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="5f5b4-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="5f5b4-326">Para toowork de empacotamento dinâmico Olá em combinação com os dois MP4 arquivos (e Olá somente de áudio MP4) em nosso ativo do Media Services, também é necessário um arquivo de manifesto (também chamado de arquivo "SMIL": linguagem de integração de multimídia sincronizada).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="5f5b4-327">Esse arquivo indica tooAzure Media Services quais arquivos MP4 estão disponíveis para empacotamento dinâmico e que esses tooconsider para streaming de áudio hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="5f5b4-328">Um arquivo de manifesto típico para um conjunto de MP4s com um único fluxo de áudio tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="5f5b4-329">arquivo. ISM de saudação contém dentro de uma instrução switch, tooeach uma referência de arquivos individuais de vídeo de MP4 hello e além de arquivo de áudio toothose também uma (ou mais) faz referência a tooan MP4 que contém apenas o áudio hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="5f5b4-330">Gerar arquivo de manifesto de saudação para nosso conjunto de MP4 pode ser feito por meio de um componente chamado hello "AMS manifesto gravador".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="5f5b4-331">toouse, arraste-o para a superfície de saudação e conecte-se o hello "De gravação concluído" pinos de saída de hello três arquivos de saída componentes toohello AMS gravador de manifesto de entrada.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="5f5b4-332">Certifique-se de que tooconnect Olá saída Olá AMS manifesto gravador toohello ativo/arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="5f5b4-333">Assim como acontece com os outros componentes de saída de arquivo, configure o nome de saída de arquivo hello. ISM com uma expressão:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="5f5b4-334">Nosso fluxo de trabalho concluído é semelhante a saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-334">Our finished workflow looks like hello below:</span></span>

![Fluxo de trabalho MP4 toomultibitrate de terminar de MXF](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="5f5b4-336">*Fluxo de trabalho MP4 toomultibitrate de terminar de MXF*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="5f5b4-337"><a id="MXF_to__multibitrate_MP4"></a>Codificando MXF em MP4 com várias taxas de bit - plano gráfico aprimorado</span><span class="sxs-lookup"><span data-stu-id="5f5b4-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="5f5b4-338">Em Olá [passo a passo de fluxo de trabalho anterior](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) que vimos como um único ativo de entrada MXF pode ser convertido em um ativo de saída com arquivos MP4 com múltiplas taxas de bits, um arquivo MP4 somente de áudio e um arquivo de manifesto para uso em conjunto com a mídia do Azure Serviços de empacotamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="5f5b4-339">Este passo a passo mostrará como alguns aspectos de saudação podem ser aprimorados e torna mais conveniente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="5f5b4-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance de visão geral do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 tooenhance de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="5f5b4-342">*Multibitrate MP4 tooenhance de fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="5f5b4-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenções de nomenclatura do arquivo</span><span class="sxs-lookup"><span data-stu-id="5f5b4-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="5f5b4-344">Fluxo de trabalho anterior Olá especificamos uma expressão simples como base Olá para gerar nomes de arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="5f5b4-345">Temos alguns duplicação embora: todos os componentes de arquivo de saída individuais Olá Olá essa expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="5f5b4-346">Por exemplo, nosso componente de saída de arquivo para o arquivo de vídeo primeiro Olá é configurado com esta expressão:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="5f5b4-347">Tempo para Olá segunda saída de vídeo, temos uma expressão como:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="5f5b4-348">Não seria mais claro, menos propenso a erros e mais conveniente se pudéssemos remover algumas essas duplicações e tornar as coisas mais configuráveis?</span><span class="sxs-lookup"><span data-stu-id="5f5b4-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="5f5b4-349">Felizmente, podemos: recursos de expressão do designer de saudação em combinação com propriedades personalizadas da saudação capacidade toocreate em nosso raiz de fluxo de trabalho fornece uma camada adicional de conveniência.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="5f5b4-350">Vamos supor que estamos será unidade de configuração de nome de arquivo do hello taxas de bits de arquivos MP4 individuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="5f5b4-351">Essas taxas de bits, irá visar tooconfigure em um centro colocar (em raiz de saudação do nosso gráfico), de onde eles serão acessada geração de nome de arquivo de tooconfigure e a unidade.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="5f5b4-352">toodo isso, vamos começar com a publicação de propriedade de taxa de bits Olá de ambos os raiz de toohello AVC codificadores de nosso fluxo de trabalho para que ele se tornará acessível de ambos os raiz hello, bem como codificadores Olá AVC.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="5f5b4-353">(Mesmo se for exibido em dois pontos diferentes, haverá apenas um valor subjacente).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="5f5b4-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Propriedades de componente na raiz de fluxo de trabalho de saudação de publicação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="5f5b4-355">Abra o codificador de AVC primeiro hello, vá toohello propriedade de taxa de bits (kbps) e na lista suspensa de saudação selecione publicar.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Propriedade de taxa de bits Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="5f5b4-357">*Propriedade de taxa de bits Olá publicação*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="5f5b4-358">Configurar Olá publicar diálogo toopublish toohello raiz do nosso gráfico de fluxo de trabalho, com um nome publicado de "video1bitrate" e um nome de exibição legível de "Taxa de bits do vídeo 1".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="5f5b4-359">Configure um nome do grupo personalizado chamado "Taxas de Bits de Streaming" e toque em Publicar.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Propriedade de taxa de bits Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="5f5b4-361">*Caixa de diálogo de publicação para a propriedade de taxa de bits*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="5f5b4-362">Olá repetição mesmo para a propriedade de taxa de bits de saudação do hello segundo codificador AVC e nomeie-o "video2bitrate" com um nome de exibição de "Taxa de bits do vídeo 2", no hello mesma personalizado de grupo "Streaming taxas de bits".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="5f5b4-363">Se nós agora inspecionar as propriedades de fluxo de trabalho raiz hello, veremos nosso grupo personalizado com hello aparecem duas propriedades publicadas.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="5f5b4-364">Ambos são refletir o valor de saudação de seu respectiva AVC codificador de taxa de bits.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Propriedades de taxa de bits publicadas na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="5f5b4-366">Sempre que desejamos tooaccess essas propriedades de código ou de uma expressão, podemos fazer isso como este:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="5f5b4-367">no código embutido de um componente logo abaixo raiz Olá: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="5f5b4-368">em uma expressão: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="5f5b4-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="5f5b4-369">Vamos concluir o grupo de "Streaming taxas de bits" hello publicando nosso faixa de áudio de taxa de bits nele também.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="5f5b4-370">Em Propriedades Olá Olá AAC codificador, procure a configuração de taxa de bits de saudação e selecione publicar na Olá suspensa próxima tooit.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="5f5b4-371">Publicar toohello raiz do gráfico de saudação com nome "audio1bitrate" e exibir o nome "Taxa de bits de áudio 1" em nosso grupo personalizado "Streaming taxas de bits".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Caixa de diálogo de publicação para a taxa de bits de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="5f5b4-373">*Caixa de diálogo de publicação para a taxa de bits de áudio*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-373">*Publishing dialog for audio bitrate*</span></span>

![Propriedades de áudio e vídeos resultantes na raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="5f5b4-375">*Propriedades de áudio e vídeos resultantes na raiz*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="5f5b4-376">Observe que a alteração de qualquer um desses três valores também configura novamente e alterações Olá componentes do respectivos Olá são vinculados com valores (e, quando publicados do).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="5f5b4-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Faça com que os nomes de arquivo de saída gerados dependam dos valores de propriedade publicados</span><span class="sxs-lookup"><span data-stu-id="5f5b4-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="5f5b4-378">Em vez de codificar os nomes de arquivo gerado, podemos agora alterar nossa expressão de nome de arquivo em cada um dos toorely de componentes de saída de arquivo hello nas propriedades de taxa de bits Olá que acabou de ser publicados na raiz do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="5f5b4-379">Começando com nossa primeira saída de arquivo, localizar a propriedade de arquivo hello e editar a expressão hello como este:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="5f5b4-380">parâmetros diferentes de saudação nesta expressão podem ser acessados e inseridos ao atingir o sinal de cifrão Olá teclado Olá enquanto estiver na janela de expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="5f5b4-381">Um dos parâmetros disponíveis Olá é nossa propriedade video1bitrate que são publicados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Acessando parâmetros dentro de uma expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="5f5b4-383">*Acessando parâmetros dentro de uma expressão*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="5f5b4-384">Olá mesmo para saída de arquivo hello para nosso vídeo segundo:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="5f5b4-385">e para a saída de arquivo somente de áudio hello:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="5f5b4-386">Se alterarmos agora Olá a taxa de bits para qualquer um dos arquivos de áudio ou vídeo hello, codificador do respectivos Olá será reconfigurado e convenção de nomes de arquivos com base em taxas de bits hello será cumprida automático.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="5f5b4-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adicionando a saída de MP4 toomultibitrate miniaturas</span><span class="sxs-lookup"><span data-stu-id="5f5b4-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="5f5b4-388">A partir de um fluxo de trabalho que gera [uma saída como MP4 de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), podemos agora verá em Adicionar saída de toohello de miniaturas.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="5f5b4-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Miniaturas de tooadd de visão geral do fluxo de trabalho para</span><span class="sxs-lookup"><span data-stu-id="5f5b4-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Multibitrate MP4 toostart de fluxo de trabalho do](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="5f5b4-391">*Multibitrate MP4 toostart de fluxo de trabalho do*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="5f5b4-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adicionando codificação JPG</span><span class="sxs-lookup"><span data-stu-id="5f5b4-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="5f5b4-393">núcleo de saudação do nosso geração de miniaturas serão componente de codificador de JPG hello, toooutput capaz de arquivos. JPG.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![Codificador de JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="5f5b4-395">*Codificador de JPG*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-395">*JPG Encoder*</span></span>

<span data-ttu-id="5f5b4-396">No entanto diretamente não foi possível conectar nosso fluxo de vídeo descompactado da saudação entrada de arquivo de mídia no codificador JPG hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="5f5b4-397">Em vez disso, ele espera toobe entregue quadros individuais.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="5f5b4-398">Isso, podemos fazer através do componente de entrada do quadro de vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-398">This, we can do through hello Video Frame Gate component.</span></span>

![Conectar-se um codificador JPG quadro portão toohello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="5f5b4-400">*Conectar-se um codificador JPG quadro portão toohello*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="5f5b4-401">Portão de quadro Hello quando cada tantos segundos ou quadros permite toopass um quadro de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="5f5b4-402">tempo de intervalo e hello de saudação deslocamento com que isso ocorre é configurável nas propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Propriedades do Portão de Quadro do Vídeo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="5f5b4-404">*Propriedades do Portão de Quadro do Vídeo*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="5f5b4-405">Vamos criar uma miniatura de cada minuto, definindo Olá modo tooTime (segundos) e Olá too60 de intervalo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="5f5b4-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Lidando com a conversão de espaço de cor</span><span class="sxs-lookup"><span data-stu-id="5f5b4-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="5f5b4-407">Embora seria parecer lógico pins de vídeo descompactado do portão de quadro hello e hello entrada de arquivo de mídia agora podem ser conectados, obteremos um aviso se fazer isso.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Erro no espaço de cor de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="5f5b4-409">*Erro no espaço de cor de entrada*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-409">*Input color space error*</span></span>

<span data-ttu-id="5f5b4-410">Isso ocorre porque a forma Olá no qual cor informações são representadas em nosso original bruto descompactado fluxo de vídeo, provenientes de nosso MXF é diferente do que Olá codificador de JPG está esperando.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="5f5b4-411">Mais especificamente, uma chamada "espaço de cores" de "RGB" ou "Cinza" é esperado tooflow no.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="5f5b4-412">Isso significa que o fluxo de vídeo de entrada do que Olá vídeo quadro portão precisará toohave uma conversão aplicada primeiro sobre o seu espaço de cor.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="5f5b4-413">Arraste a saudação de fluxo de trabalho Olá conversor de espaço de cor - Intel e conectá-lo tooour portão de quadro.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Conexão de um Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="5f5b4-415">*Conexão de um Conversor de Espaço de Cor*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="5f5b4-416">Na janela de propriedades hello, escolha entrada hello BGR 24 Olá predefinição de lista.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="5f5b4-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniaturas de saudação de gravação</span><span class="sxs-lookup"><span data-stu-id="5f5b4-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="5f5b4-418">Diferente do nosso vídeo de MP4, Olá codificador de JPG componente resultará em mais de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="5f5b4-419">Em ordem toodeal com isso, um componente de cena pesquisa JPG arquivo gravador pode ser usado: ele se miniaturas JPG entradas hello e gravar, cada nome de arquivo que está sendo o sufixo por um número diferente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="5f5b4-420">(número de saudação normalmente indicando o número de saudação de segundos/unidades no fluxo de saudação que Olá miniatura foi obtido de.)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Olá apresentando o gravador de arquivo JPG cena pesquisa](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="5f5b4-422">*Olá apresentando o gravador de arquivo JPG cena pesquisa*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="5f5b4-423">Configurar a propriedade do caminho da pasta de saída de hello com expressão Olá: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="5f5b4-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="5f5b4-424">e Olá a propriedade com o prefixo de nome de arquivo:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="5f5b4-425">prefixo de saudação determinará como arquivos em miniatura Olá estão sendo nomeados.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="5f5b4-426">Eles serão ser sufixo com um número indicando Olá posição da miniatura no fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Propriedades do Gravador de arquivo JPG de Pesquisa de cena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="5f5b4-428">*Propriedades do Gravador de arquivo JPG de Pesquisa de cena*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="5f5b4-429">Conecte-se nó do hello o gravador de arquivo JPG cena pesquisa toohello ativo/arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="5f5b4-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detectando erros em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="5f5b4-431">Conecte-se a entrada Olá Olá cor espaço conversor toohello bruto descompactados saída de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="5f5b4-432">Agora, execute um teste local para o fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="5f5b4-433">Há um fluxo de trabalho de Olá boas chances de repente parará a execução e indicar com um contorno vermelho no componente de saudação que encontrou um erro:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Erro no Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="5f5b4-435">*Erro no Conversor de Espaço de Cor*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-435">*Color Space Converter error*</span></span>

<span data-ttu-id="5f5b4-436">Clique em ícone de "E" hello pouco vermelha no canto superior direito de saudação do hello conversor de espaço de cor componente toosee o que é o motivo de saudação Falha na tentativa de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Caixa de diálogo do erro no Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="5f5b4-438">*Caixa de diálogo do erro no Conversor de Espaço de Cor*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="5f5b4-439">Na verdade, como você pode ver, Olá entrada espaço de cor padrão para o conversor de espaço de cor Olá tem rec601 toobe para nossa conversão solicitada de YUV tooRGB.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="5f5b4-440">Aparentemente, nosso fluxo não indica que é rec601.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="5f5b4-441">(Rec 601 é um padrão de codificação de sinais de vídeo analógicos entrelaçados no formato de vídeo digital.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="5f5b4-442">Ele especifica uma região ativa cobrindo 720 amostras de luminosidade e 360 exemplos de crominância por linha.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="5f5b4-443">cor Olá codificação sistema é conhecido como YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="5f5b4-444">toofix isso, será indicamos nos metadados de saudação do nosso fluxo que estamos lidando com conteúdo rec601.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="5f5b4-445">toodo, então, vamos usar um componente do atualizador de tipo de dados de vídeo, colocaremos entre nossos bruto fonte e hello cor espaço componente de conversão.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="5f5b4-446">Esse atualizador de tipo de dados permite atualização manual de saudação de certos dados vídeos propriedades de tipo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="5f5b4-447">Configurá-lo tooindicate um padrão de espaço de cor de "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="5f5b4-448">Isso fará com que fluxo de Olá Olá atualizador de tipo de dados de vídeo tootag com espaço de cor hello "Rec 601" se não houver nenhum espaço de cor foi definido.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="5f5b4-449">(Ela não substituirá todos os metadados existentes, a menos que a caixa de seleção de substituição de saudação foi verificada.)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Atualizando o espaço de cor padrão em Olá atualizador de tipo de dados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="5f5b4-451">*Atualizando o espaço de cor padrão em Olá atualizador de tipo de dados*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="5f5b4-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="5f5b4-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="5f5b4-453">Agora que nossa nosso fluxo de trabalho for concluído, faça outra toosee de execução de teste passar por ele.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Fluxo de trabalho concluído para várias saídas mp4 com miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="5f5b4-455">*Fluxo de trabalho concluído para várias saídas mp4 com miniaturas*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="5f5b4-456"><a id="time_based_trim"></a>Corte baseado em tempo da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="5f5b4-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="5f5b4-457">A partir de um fluxo de trabalho que gera [uma saída como MP4 de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), podemos agora verá para cortar o vídeo de origem de saudação com base em carimbos de data / hora.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="5f5b4-458"><a id="time_based_trim_start"></a>Toostart de visão geral do fluxo de trabalho adicionando restrições para</span><span class="sxs-lookup"><span data-stu-id="5f5b4-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Iniciar a remoção de tooadd de fluxo de trabalho para](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="5f5b4-460">*Iniciar a remoção de tooadd de fluxo de trabalho para*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="5f5b4-461"><a id="time_based_trim_use_stream_trimmer"></a>Usando Olá filtro de fluxo</span><span class="sxs-lookup"><span data-stu-id="5f5b4-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="5f5b4-462">componente de filtro de fluxo Olá permite a partir de saudação tootrim e final de um fluxo de entrada se basear em informações de tempo (em segundos, minutos,...). filtro de saudação não oferece suporte a quadros de corte.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Corte de fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="5f5b4-464">*Corte de fluxo*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-464">*Stream Trimmer*</span></span>

<span data-ttu-id="5f5b4-465">Em vez de vincular codificadores Olá AVC e alto-falantes posição cedente toohello entrada do arquivo de mídia diretamente, colocaremos entre esses filtro de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="5f5b4-466">(Uma para o sinal de vídeo hello e outro para o sinal de áudio intercaladas hello.)</span><span class="sxs-lookup"><span data-stu-id="5f5b4-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Como colocar o Corte de fluxo entre eles](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="5f5b4-468">*Como colocar o Corte de fluxo entre eles*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="5f5b4-469">Vamos configurar filtro de saudação para que somente Processaremos vídeo e áudio entre 15 e 60 segundos no vídeo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="5f5b4-470">Vá toohello propriedades de filtro de fluxo de vídeo de hello e configurar as propriedades de hora de término (60 s) e hora de início (15 anos).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="5f5b4-471">toomake se ambos os nossos filtro de áudio e vídeo está sempre toohello configurado mesmo começar e terminar valores, publicaremos esses raiz toohello de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Publicar a propriedade de hora de início do Corte de Fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="5f5b4-473">*Publicar a propriedade de hora de início do Corte de Fluxo*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-473">*Publish start time property from Stream Trimmer*</span></span>

![Publicar o diálogo da propriedade para a hora de início](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="5f5b4-475">*Publicar o diálogo da propriedade para a hora de início*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-475">*Publish property dialog for start time*</span></span>

![Publicar o diálogo da propriedade para a hora de término](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="5f5b4-477">*Publicar o diálogo da propriedade para a hora de término*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="5f5b4-478">Se nós agora inspecionar raiz de saudação do nosso fluxo de trabalho, ambas as propriedades será claramente exibido e configuráveis a partir daí.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Propriedades publicadas disponíveis na raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="5f5b4-480">*Propriedades publicadas disponíveis na raiz*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-480">*Published properties available on root*</span></span>

<span data-ttu-id="5f5b4-481">Abrir as propriedades de corte de saudação do filtro de áudio Olá agora e configurar horários de início e de término com uma expressão que se refere a toohello publicado propriedades na raiz de saudação do nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="5f5b4-482">Para a hora de início de corte de áudio hello:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="5f5b4-483">e para a hora de término:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="5f5b4-484"><a id="time_based_trim_finish"></a>Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="5f5b4-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="5f5b4-486">*Fluxo de trabalho concluído*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-486">*Finished Workflow*</span></span>

## <span data-ttu-id="5f5b4-487"><a id="scripting"></a>Apresentando o hello componente script</span><span class="sxs-lookup"><span data-stu-id="5f5b4-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="5f5b4-488">Componentes de script podem executar scripts arbitrários durante as fases de execução de saudação do nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="5f5b4-489">Há quatro scripts diferentes que podem ser executados, cada um com características específicas e seu próprios lugar no ciclo de vida do fluxo de trabalho hello:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="5f5b4-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="5f5b4-490">**commandScript**</span></span>
* <span data-ttu-id="5f5b4-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="5f5b4-491">**realizeScript**</span></span>
* <span data-ttu-id="5f5b4-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="5f5b4-492">**processInputScript**</span></span>
* <span data-ttu-id="5f5b4-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="5f5b4-493">**lifeCycleScript**</span></span>

<span data-ttu-id="5f5b4-494">documentação de saudação do hello componente script vai em mais detalhes para cada Olá acima.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="5f5b4-495">Em [Olá seguinte seção](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), Olá **realizeScript** componente script é usado tooconstruct um xml cliplist imediatamente hello quando Olá será iniciado.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="5f5b4-496">Esse script é chamado durante a instalação do componente hello, que ocorre apenas uma vez no ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="5f5b4-497"><a id="scripting_hello_world"></a>Criando scripts em um fluxo de trabalho: hello world</span><span class="sxs-lookup"><span data-stu-id="5f5b4-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="5f5b4-498">Arraste um componente script a superfície do designer hello e renomeá-lo (por exemplo, "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="5f5b4-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Adicionando um Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="5f5b4-500">*Adicionando um Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="5f5b4-501">Quando você inspecionar as propriedades de saudação do hello componente script, Olá quatro tipos diferentes de script serão mostrados, cada script diferentes tooa configurável.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propriedades do Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="5f5b4-503">*Propriedades do Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-503">*Scripted Component properties*</span></span>

<span data-ttu-id="5f5b4-504">Limpe Olá processInputScript e abrir editor de saudação do hello realizeScript.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="5f5b4-505">Agora estão configurados e pronto toostart de script.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="5f5b4-506">Os scripts são escritos em Groovy, uma linguagem de script compilada dinamicamente para plataforma Java Olá que mantém a compatibilidade com Java.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="5f5b4-507">Na verdade, grande parte do código Java é um código Groovy válido.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="5f5b4-508">Vamos escrever um script groovy do simples hello world no contexto de saudação do nosso realizeScript.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="5f5b4-509">Insira o seguinte Olá no editor de saudação:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="5f5b4-510">Agora, realize um teste local.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-510">Now execute a local test run.</span></span> <span data-ttu-id="5f5b4-511">Após essa execução inspecionar (por meio da guia sistema Olá Olá componente script) Olá propriedade Logs.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Saída do log de Hello world](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="5f5b4-513">*Saída do log de Hello world*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-513">*Hello world log output*</span></span>

<span data-ttu-id="5f5b4-514">objeto de nó de Hello, podemos chamar o método de log hello, refere-se tooour atual "nó" ou componente Olá nós estiver scrip em.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="5f5b4-515">Assim, cada componente tem Olá capacidade toooutput registrando dados, disponíveis por meio da guia de sistema de saudação. Nesse caso, estamos saída Olá literal de cadeia de caracteres "Olá, mundo".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="5f5b4-516">Toounderstand importante aqui é que isso pode ser toobe uma ferramenta de depuração inestimável, oferecendo informações sobre o script hello está realmente fazer.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="5f5b4-517">De dentro de nosso ambiente de script, também temos acesso tooproperties em outros componentes.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="5f5b4-518">Tente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="5f5b4-519">Nossa janela de log nos mostrará Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-519">Our log window will show us hello following:</span></span>

![Saída de log para acessar os caminhos do nó](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="5f5b4-521">*Saída de log para acessar os caminhos do nó*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="5f5b4-522"><a id="frame_based_trim"></a>Corte baseado em quadro da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="5f5b4-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="5f5b4-523">A partir de um fluxo de trabalho que gera [uma saída como MP4 de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), podemos agora verá para cortar o vídeo de origem de saudação com base na contagem de quadros.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="5f5b4-524"><a id="frame_based_trim_start"></a>Plano gráfico toostart visão geral sobre a adição de corte para</span><span class="sxs-lookup"><span data-stu-id="5f5b4-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Fluxo de trabalho toostart adicionando restrições para](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="5f5b4-526">*Fluxo de trabalho toostart adicionando restrições para*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="5f5b4-527"><a id="frame_based_trim_clip_list"></a>Usando Olá Clip lista XML</span><span class="sxs-lookup"><span data-stu-id="5f5b4-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="5f5b4-528">Todos os tutoriais de fluxo de trabalho anterior, usamos o componente de entrada de arquivo de mídia hello como nossa fonte de entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="5f5b4-529">Para este cenário específico, usaremos componente de origem da lista de clipe Olá em vez disso.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="5f5b4-530">Observe que isso não deve ser a forma preferida de saudação do trabalho; usar somente Olá Clip fonte da lista quando houver um motivo real toodo assim (como no hello abaixo caso, em que estamos fazendo uso dos recursos de fragmentação de lista de clipe Olá).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="5f5b4-531">tooswitch do nosso toohello de entrada de arquivo de mídia Clip fonte da lista, arraste o componente de origem da lista de clipe Olá na superfície de design de saudação e conecte-se Olá Clip lista XML pin toohello Clip lista XML do designer de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="5f5b4-532">Isso deve preencher Olá Clip fonte da lista com os pins de saída, de acordo com o vídeo de entrada tooour.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="5f5b4-533">Agora conectar os pins não compactado de áudio e vídeo descompactado Olá de Olá Olá Clip lista origem toohello respectivos AVC codificadores e Interleaver de fluxo de áudio.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="5f5b4-534">Agora remova Olá entrada de arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-534">Now remove hello Media File Input.</span></span>

![Substituído Olá entrada de arquivo de mídia com hello clipe de lista de origem](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="5f5b4-536">*Substituído Olá entrada de arquivo de mídia com hello clipe de lista de origem*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="5f5b4-537">componente de origem da lista de clipe Olá toma como entrada um XML de lista"Clip".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="5f5b4-538">Ao selecionar Olá tootest de arquivo de origem com localmente, esse xml de lista de clipe é preenchido automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Propriedade XML de lista de clipes preenchida automaticamente](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="5f5b4-540">*Propriedade XML de lista de clipes preenchida automaticamente*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="5f5b4-541">Procurando mais detalhadamente xml de toohello, isso é como ele se parece com:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Diálogo Editar lista de clipes](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="5f5b4-543">*Diálogo Editar lista de clipes*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="5f5b4-544">No entanto, isso não refletem recursos Olá Olá clip lista XML.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="5f5b4-545">Uma opção que temos é tooadd um elemento "Trim" em Olá vídeo e áudio fonte, como este:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Adicionando uma lista de clipe toohello elemento trim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="5f5b4-547">*Adicionando uma lista de clipe toohello elemento trim*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="5f5b4-548">Se você modificar o xml de lista de clipe hello como acima e executar um teste local, você verá o vídeo Olá corretamente foi cortado entre 10 e 20 segundos no vídeo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="5f5b4-549">Toowhat contrary acontece quando você fizer uma execução local, embora, esse xml cliplist mesmo não teria Olá mesmo efeito quando aplicado a um fluxo de trabalho é executado no Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="5f5b4-550">Quando é iniciado do codificador do Azure Premium, Olá cliplist xml é gerado sempre que novamente, com base em codificação de saudação de arquivo de entrada hello trabalho foi atribuído.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="5f5b4-551">Isso significa que qualquer alteração que fazemos no xml de saudação Infelizmente poderia ser substituída.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="5f5b4-552">toocounter Olá cliplist xml ser apagado quando um trabalho de codificação é iniciado, podemos novamente gerar-Olá imediatamente após o início de saudação do nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="5f5b4-553">Essas ações personalizadas podem ser realizadas por meio do que é chamado de "Componente de script".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="5f5b4-554">Para obter mais informações, consulte [Introducing Olá componente script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="5f5b4-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="5f5b4-555">Arraste um componente script a superfície do designer hello e renomeá-lo muito "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Adicionando um Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="5f5b4-557">*Adicionando um Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="5f5b4-558">Quando você inspecionar as propriedades de saudação do hello componente script, Olá quatro tipos diferentes de script serão mostrados, cada script diferentes tooa configurável.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propriedades do Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="5f5b4-560">*Propriedades do Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="5f5b4-561"><a id="frame_based_trim_modify_clip_list"></a>Modificando a lista de saudação do clipe de um componente script</span><span class="sxs-lookup"><span data-stu-id="5f5b4-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="5f5b4-562">Antes de novamente, podemos gravar Olá cliplist xml que é gerado durante a inicialização do fluxo de trabalho, precisaremos conteúdo e a propriedade do toohave acesso toohello cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="5f5b4-563">Podemos fazer isso da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clipes recebida registrada em log](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="5f5b4-565">*Lista de clipes recebida registrada em log*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="5f5b4-566">Primeiro, precisamos toodetermine uma maneira de qual ponto até o ponto em que desejamos tootrim Olá vídeo.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="5f5b4-567">toomake esse usuário de menos técnico toohello conveniente de fluxo de trabalho Olá publicar raiz de toohello duas propriedades do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="5f5b4-568">toodo isso, clique com botão direito superfície do designer hello e selecione "Adicionar propriedade":</span><span class="sxs-lookup"><span data-stu-id="5f5b4-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="5f5b4-569">Primeira propriedade: "ClippingTimeStart" do tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="5f5b4-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="5f5b4-570">Segunda propriedade: "ClippingTimeEnd" do tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="5f5b4-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Adicionar o diálogo Propriedade à hora de início de corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="5f5b4-572">*Adicionar o diálogo Propriedade à hora de início de corte*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-572">*Add Property dialog for clipping start time*</span></span>

![Propriedades da hora de corte publicadas na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="5f5b4-574">*Propriedades da hora de corte publicadas na raiz do fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="5f5b4-575">Configure ambos os valor adequado de tooa propriedades:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-575">Configure both properties tooa suitable value:</span></span>

![Configurar Olá propriedades de início e término de recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="5f5b4-577">*Configurar Olá propriedades de início e término de recorte*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="5f5b4-578">Agora, em nosso script, podemos acessar as duas propriedades, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Janela do log mostrando o início e o término do corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="5f5b4-580">*Janela do log mostrando o início e o término do corte*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="5f5b4-581">Vamos analisar cadeias de caracteres de código de tempo de saudação em um formulário toouse mais conveniente, usando uma expressão regular simple:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Janela do log com a saúda do código de tempo analisado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="5f5b4-583">*Janela do log com a saúda do código de tempo analisado*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="5f5b4-584">Com essas informações à mão, agora podemos modificar início de Olá Olá cliplist xml tooreflect e horários de término para Olá desejado recorte precisas de quadro do filme hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Elementos de corte script código tooadd](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="5f5b4-586">*Elementos de corte script código tooadd*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="5f5b4-587">Isso foi feito por meio de operações de manipulação de cadeia de caracteres normais.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="5f5b4-588">xml de lista de clipe modificado resultante Hello será gravado toohello clipListXML propriedade na raiz de fluxo de trabalho Olá por meio do método "setProperty" hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="5f5b4-589">janela de log Olá após a execução de outro teste nos mostrariam Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-589">hello log window after another test run would show us hello following:</span></span>

![Lista de clipe resultante Olá registro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="5f5b4-591">*Lista de clipe resultante Olá registro*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="5f5b4-592">Faça um toosee de execução de teste como fluxos de áudio e vídeo de saudação tem sido cortados.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="5f5b4-593">Como você fará mais de uma execução de teste com valores diferentes para pontos de corte hello, você observará que aqueles serão não levadas em conta porém!</span><span class="sxs-lookup"><span data-stu-id="5f5b4-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="5f5b4-594">motivo Olá é designer hello, ao contrário de saudação do Azure em tempo de execução, faz não substituição Olá cliplist xml cada execução.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="5f5b4-595">Isso significa que somente hello primeira vez que você definiu hello e pontos, fará com que Olá xml tootransform, todos Olá outras vezes, a cláusula de proteção (se (clipListXML.indexOf ("<trim>") = = -1)) impedirá o fluxo de trabalho de saudação de adicionar outro trim elemento quando já há uma presente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="5f5b4-596">toomake nosso fluxo de trabalho conveniente tootest localmente, é melhor adicionar algum código de manutenção de casa que verifica se um elemento de corte já estiver presente.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="5f5b4-597">Nesse caso, estamos pode removê-lo antes de continuar modificando Olá xml com os novos valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="5f5b4-598">Em vez de usar manipulações de cadeia de caracteres simples, é mais seguro provavelmente toodo isso por meio do objeto xml real do modelo de análise.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="5f5b4-599">Antes que possamos adicionar esse código no entanto, vamos precisar tooadd que um número de instruções de importação no hello início do nosso script primeiro:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="5f5b4-600">Depois disso, podemos adicionar Olá necessário código de limpeza:</span><span class="sxs-lookup"><span data-stu-id="5f5b4-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="5f5b4-601">Esse código vai acima ponto Olá em que adicionamos Olá elementos trim toohello cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="5f5b4-602">Neste ponto, podemos executar e modificar nosso fluxo de trabalho como tempo quanto queremos tendo alterações Olá aplicadas nunca.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="5f5b4-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adicionando uma propriedade de conveniência ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="5f5b4-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="5f5b4-604">Como você pode não querer sempre toohappen corte, vamos finalizar nosso fluxo de trabalho adicionando um conveniente sinalizador booliano que indica se deseja ou não podemos tooenable cortar / recorte.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="5f5b4-605">Assim como antes, publicar uma nova raiz de toohello de propriedade de nosso fluxo de trabalho chamado "ClippingEnabled" do tipo "Booleano".</span><span class="sxs-lookup"><span data-stu-id="5f5b4-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Propriedade publicada para habilitar o recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="5f5b4-607">*Propriedade publicada para habilitar o recorte*</span><span class="sxs-lookup"><span data-stu-id="5f5b4-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="5f5b4-608">Com hello abaixo cláusula de guarda simples, podemos verificar se a fragmentação é necessária e decidir se nossa lista de clipe como tal precisa toobe modificado ou não.</span><span class="sxs-lookup"><span data-stu-id="5f5b4-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="5f5b4-609"><a id="code"></a>Código completo</span><span class="sxs-lookup"><span data-stu-id="5f5b4-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="5f5b4-610">Consulte também</span><span class="sxs-lookup"><span data-stu-id="5f5b4-610">Also see</span></span>
[<span data-ttu-id="5f5b4-611">Apresentando a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="5f5b4-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="5f5b4-612">Como tooUse Premium de codificação no Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="5f5b4-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="5f5b4-613">Codificando conteúdo sob demanda com os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="5f5b4-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="5f5b4-614">Codecs e formatos de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="5f5b4-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="5f5b4-615">Exemplos de arquivos de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f5b4-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="5f5b4-616">Ferramenta do Explorador dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="5f5b4-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="5f5b4-617">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="5f5b4-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5f5b4-618">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="5f5b4-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
