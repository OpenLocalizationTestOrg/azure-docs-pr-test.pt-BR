---
title: "Tutoriais avançados do fluxo de trabalho do Codificador de Mídia Premium"
description: "Este documento contém instruções passo a passo que mostram como executar tarefas avançadas com o Fluxo de trabalho do Codificador de Mídia Premium e também como criar fluxos de trabalho complexos com o Designer de Fluxo de Trabalho."
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
ms.openlocfilehash: 565497bd5a35e3c4d69d29512307cf3ca2364bdd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="39ba9-103">Tutoriais avançados do fluxo de trabalho do Codificador de Mídia Premium</span><span class="sxs-lookup"><span data-stu-id="39ba9-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="39ba9-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="39ba9-104">Overview</span></span>
<span data-ttu-id="39ba9-105">Este documento contém instruções passo a passo que mostram como personalizar fluxos de trabalho com o **Designer de Fluxo de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="39ba9-105">This document contains walkthroughs that show how to customize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="39ba9-106">Encontre os arquivos de fluxo de trabalho [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="39ba9-106">You can find the actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="39ba9-107">SUMÁRIO</span><span class="sxs-lookup"><span data-stu-id="39ba9-107">TOC</span></span>
<span data-ttu-id="39ba9-108">Os tópicos a seguir serão abordados:</span><span class="sxs-lookup"><span data-stu-id="39ba9-108">The following topics are covered:</span></span>

* [<span data-ttu-id="39ba9-109">Codificando MXF em um MP4 de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="39ba9-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="39ba9-110">Iniciando um novo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="39ba9-111">Usando a Entrada do Arquivo de Mídia</span><span class="sxs-lookup"><span data-stu-id="39ba9-111">Using the Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="39ba9-112">Inspecionando fluxos de mídia</span><span class="sxs-lookup"><span data-stu-id="39ba9-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="39ba9-113">Adicionando um codificador de vídeo para geração de arquivo .MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="39ba9-114">Codificando o fluxo de áudio</span><span class="sxs-lookup"><span data-stu-id="39ba9-114">Encoding the audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="39ba9-115">Multiplexando fluxos de áudio e de vídeo em um contêiner MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="39ba9-116">Gravando o arquivo MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-116">Writing the MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="39ba9-117">Criando um Ativo dos Serviços de Mídia do arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="39ba9-117">Creating a Media Services Asset from the output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="39ba9-118">Testar o fluxo de trabalho concluído localmente</span><span class="sxs-lookup"><span data-stu-id="39ba9-118">Test the finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="39ba9-119">Codificando MXF em MP4s com várias taxas bits - empacotamento dinâmico habilitado</span><span class="sxs-lookup"><span data-stu-id="39ba9-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="39ba9-120">Adicionando uma ou mais saídas MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="39ba9-121">Configurando os nomes de saída do arquivo</span><span class="sxs-lookup"><span data-stu-id="39ba9-121">Configuring the file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="39ba9-122">Adicionando uma Trilha de Áudio separada</span><span class="sxs-lookup"><span data-stu-id="39ba9-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="39ba9-123">Adicionando o arquivo SMIL .ISM</span><span class="sxs-lookup"><span data-stu-id="39ba9-123">Adding the .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="39ba9-124">Codificando MXF em MP4 com várias taxas de bit - plano gráfico aprimorado</span><span class="sxs-lookup"><span data-stu-id="39ba9-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="39ba9-125">Visão geral do fluxo de trabalho para aprimoramento</span><span class="sxs-lookup"><span data-stu-id="39ba9-125">Workflow overview to enhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="39ba9-126">Convenções de nomenclatura do arquivo</span><span class="sxs-lookup"><span data-stu-id="39ba9-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="39ba9-127">Publicando as propriedades do componente na raiz do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-127">Publishing component properties onto the workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="39ba9-128">Faça com que os nomes de arquivo de saída gerados dependam dos valores de propriedade publicados</span><span class="sxs-lookup"><span data-stu-id="39ba9-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="39ba9-129">Adicionando miniaturas à saída MP4 com várias taxas de bit</span><span class="sxs-lookup"><span data-stu-id="39ba9-129">Adding thumbnails to multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="39ba9-130">Visão geral do fluxo de trabalho para adição de miniaturas</span><span class="sxs-lookup"><span data-stu-id="39ba9-130">Workflow overview to add thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="39ba9-131">Adicionando codificação JPG</span><span class="sxs-lookup"><span data-stu-id="39ba9-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="39ba9-132">Lidando com a conversão de espaço de cor</span><span class="sxs-lookup"><span data-stu-id="39ba9-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="39ba9-133">Gravando as miniaturas</span><span class="sxs-lookup"><span data-stu-id="39ba9-133">Writing the thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="39ba9-134">Detectando erros em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="39ba9-135">Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="39ba9-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="39ba9-136">Corte baseado em tempo da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="39ba9-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="39ba9-137">Visão geral do fluxo de trabalho para começar a adição do corte</span><span class="sxs-lookup"><span data-stu-id="39ba9-137">Workflow overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="39ba9-138">Usando o corte de fluxo</span><span class="sxs-lookup"><span data-stu-id="39ba9-138">Using the Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="39ba9-139">Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="39ba9-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="39ba9-140">Introdução ao componente com script</span><span class="sxs-lookup"><span data-stu-id="39ba9-140">Introducing the Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="39ba9-141">Criando scripts em um fluxo de trabalho: hello world</span><span class="sxs-lookup"><span data-stu-id="39ba9-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="39ba9-142">Corte baseado em quadro da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="39ba9-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="39ba9-143">Visão geral do plano gráfico para começar a adição do corte</span><span class="sxs-lookup"><span data-stu-id="39ba9-143">Blueprint overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="39ba9-144">Como usar o XML da lista de clipes</span><span class="sxs-lookup"><span data-stu-id="39ba9-144">Using the Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="39ba9-145">Modificando a lista de clipes de um componente com script</span><span class="sxs-lookup"><span data-stu-id="39ba9-145">Modifying the clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="39ba9-146">Adicionando uma propriedade de conveniência ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="39ba9-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="39ba9-147"><a id="MXF_to_MP4"></a>Codificando MXF em um MP4 de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="39ba9-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="39ba9-148">Neste passo a passo, criaremos um arquivo MP4 de taxa de bits única com áudio codificado em AAC-HE a partir de um arquivo de entrada .MXF.</span><span class="sxs-lookup"><span data-stu-id="39ba9-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="39ba9-149"><a id="MXF_to_MP4_start_new"></a>Iniciando um novo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="39ba9-150">Abra o Designer de Fluxo de Trabalho e selecione "Arquivo" - "Novo Espaço de Trabalho" - "Transcodificar Esquema"</span><span class="sxs-lookup"><span data-stu-id="39ba9-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="39ba9-151">O novo fluxo de trabalho mostrará três elementos:</span><span class="sxs-lookup"><span data-stu-id="39ba9-151">The new workflow will show 3 elements:</span></span>

* <span data-ttu-id="39ba9-152">Arquivo de Origem Principal</span><span class="sxs-lookup"><span data-stu-id="39ba9-152">Primary Source File</span></span>
* <span data-ttu-id="39ba9-153">XML da Lista de Clipes</span><span class="sxs-lookup"><span data-stu-id="39ba9-153">Clip List XML</span></span>
* <span data-ttu-id="39ba9-154">Arquivo/Ativo de Saída</span><span class="sxs-lookup"><span data-stu-id="39ba9-154">Output File/Asset</span></span>  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="39ba9-156">*Novo fluxo de trabalho de codificação*</span><span class="sxs-lookup"><span data-stu-id="39ba9-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="39ba9-157"><a id="MXF_to_MP4_with_file_input"></a>Usando a Entrada do Arquivo de Mídia</span><span class="sxs-lookup"><span data-stu-id="39ba9-157"><a id="MXF_to_MP4_with_file_input"></a>Using the Media File Input</span></span>
<span data-ttu-id="39ba9-158">Para aceitar nosso arquivo de mídia de entrada, é necessário começar com a adição de um componente de Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="39ba9-158">In order to accept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="39ba9-159">Para adicionar um componente ao fluxo de trabalho, procure-o na caixa de pesquisa do Repositório e arraste a entrada desejada até o painel do designer.</span><span class="sxs-lookup"><span data-stu-id="39ba9-159">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span> <span data-ttu-id="39ba9-160">Faça isso com a Entrada do Arquivo de Mídia e conecte o componente de Arquivo de Origem Principal ao pino de entrada Nome de arquivo na Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="39ba9-160">Do this for the Media File Input and connect the Primary Source File component to the Filename input pin from the Media File Input.</span></span>

![Entrada do Arquivo de Mídia conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="39ba9-162">*Entrada do Arquivo de Mídia conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-162">*Connected Media File Input*</span></span>

<span data-ttu-id="39ba9-163">Antes de podermos fazer mais do que isso, precisaremos indicar ao designer de fluxo de trabalho qual arquivo de exemplo desejamos usar para criar nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-163">Before we can do much else, we'll first need to indicate to the workflow designer what sample file we'd like to use to design our workflow with.</span></span> <span data-ttu-id="39ba9-164">Para fazer isso, clique no plano de fundo do painel do designer e procure pela propriedade do Arquivo de Origem Principal no painel de propriedades do lado direito.</span><span class="sxs-lookup"><span data-stu-id="39ba9-164">To do so, click the designer pane background and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="39ba9-165">Clique no ícone de pasta e selecione o arquivo com o qual deseja testar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-165">Click the folder icon and select the desired file to test the workflow with.</span></span> <span data-ttu-id="39ba9-166">Assim que isso for feito, o componente de Entrada do Arquivo de Mídia inspecionará o arquivo e preencherá seus pinos de saída para refletir o arquivo inspecionado por ele.</span><span class="sxs-lookup"><span data-stu-id="39ba9-166">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file it inspected.</span></span>

![Entrada do Arquivo de Mídia preenchida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="39ba9-168">*Entrada do Arquivo de Mídia preenchida*</span><span class="sxs-lookup"><span data-stu-id="39ba9-168">*Populated Media File Input*</span></span>

<span data-ttu-id="39ba9-169">Embora isso especifique com qual entrada queremos trabalhar, não informa ainda para onde a saída codificada deve ir.</span><span class="sxs-lookup"><span data-stu-id="39ba9-169">While this specifies with what input we'd like to work with, it doesn't tell yet where the encoded output should go to.</span></span> <span data-ttu-id="39ba9-170">Assim como o Arquivo de Origem Principal foi configurado, configure a propriedade da Variável da pasta de saída, logo abaixo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-170">Similar to how the Primary Source File was configured, now configure the Output Folder Variable property, just below it.</span></span>

![Propriedades de Entrada e Saída configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="39ba9-172">*Propriedades de Entrada e Saída configuradas*</span><span class="sxs-lookup"><span data-stu-id="39ba9-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="39ba9-173"><a id="MXF_to_MP4_streams"></a>Inspecionando fluxos de mídia</span><span class="sxs-lookup"><span data-stu-id="39ba9-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="39ba9-174">Com frequência, convém saber como é o fluxo que percorre o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-174">Often it's desired to know how the stream looks like that flows through the workflow.</span></span> <span data-ttu-id="39ba9-175">Para inspecionar um fluxo em qualquer ponto do fluxo de trabalho, basta clicar em um pino de saída ou de entrada em qualquer um dos componentes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-175">To inspect a stream at any point in the workflow, just click an output or input pin on any of the components.</span></span> <span data-ttu-id="39ba9-176">Nesse caso, tente clicar no pino de saída Vídeo Descompactado em nossa Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="39ba9-176">In this case, try clicking on the Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="39ba9-177">Uma caixa de diálogo será aberta permitindo a inspeção do vídeo de saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-177">A dialog will open up that allows to inspect the outbound video.</span></span>

![Inspeção do pino de saída Vídeo Descompactado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="39ba9-179">*Inspeção do pino de saída Vídeo Descompactado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-179">*Inspecting the Uncompressed Video output pin*</span></span>

<span data-ttu-id="39ba9-180">Em nosso caso, ele nos informa, por exemplo, que estamos lidando com uma entrada de 1920 x 1080 a 24 quadros por segundo em uma amostragem de 4:2:2 de um vídeo de quase 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="39ba9-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="39ba9-181"><a id="MXF_to_MP4_file_generation"></a>Adicionando um codificador de vídeo para geração de arquivo .MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="39ba9-182">Observe que, agora, um pino de saída Vídeo Descompactado e vários pinos de saída Áudio Descompactados estão disponíveis para uso em nossa Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="39ba9-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="39ba9-183">Para codificar o vídeo de entrada, precisamos de um componente de codificação - nesse caso, para geração de arquivos .MP4.</span><span class="sxs-lookup"><span data-stu-id="39ba9-183">In order to encode the inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="39ba9-184">Para codificar o fluxo de vídeo para H.264, adicione o componente do Codificador de Vídeo AVC à superfície do designer.</span><span class="sxs-lookup"><span data-stu-id="39ba9-184">To encode the video stream to H.264, add the AVC Video Encoder component to the designer surface.</span></span> <span data-ttu-id="39ba9-185">Esse componente recebe um fluxo de vídeo descompactado como entrada e fornece um fluxo de vídeo compactado AVC em seu pino de saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Codificador AVC desconectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="39ba9-187">*Codificador AVC desconectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="39ba9-188">Suas propriedades determinam como a codificação ocorre exatamente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-188">Its properties determine how the encoding exactly happens.</span></span> <span data-ttu-id="39ba9-189">Vamos analisar algumas das configurações mais importantes:</span><span class="sxs-lookup"><span data-stu-id="39ba9-189">Let's have a look at some of the more important settings:</span></span>

* <span data-ttu-id="39ba9-190">Largura da Saída e Altura da Saída: determinam a resolução do vídeo codificado.</span><span class="sxs-lookup"><span data-stu-id="39ba9-190">Output width and Output height: these determine the resolution of the encoded video.</span></span> <span data-ttu-id="39ba9-191">Em nosso caso, usaremos 640 x 360</span><span class="sxs-lookup"><span data-stu-id="39ba9-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="39ba9-192">Taxa de Quadros: quando definida como passagem, adotará a taxa de quadros de origem, mas é possível substituir isso.</span><span class="sxs-lookup"><span data-stu-id="39ba9-192">Frame Rate: when set to passthrough it will just adopt the source frame rate, it's possible to override this though.</span></span> <span data-ttu-id="39ba9-193">Observe que essa conversão de taxa de quadros não tem compensação de movimento.</span><span class="sxs-lookup"><span data-stu-id="39ba9-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="39ba9-194">Perfil e Nível: determinam o perfil e o nível do AVC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-194">Profile and Level: these determine the AVC profile and level.</span></span> <span data-ttu-id="39ba9-195">Para saber mais sobre os diferentes níveis e perfis de forma conveniente, clique no ícone de interrogação no componente do Codificador de vídeo AVC e a página de Ajuda mostrará mais detalhes sobre cada um dos níveis.</span><span class="sxs-lookup"><span data-stu-id="39ba9-195">To conveniently get more information about the different levels and profiles, click the question mark icon on the AVC Video Encoder component and the help page will show more detail about each of the levels.</span></span> <span data-ttu-id="39ba9-196">Em nosso exemplo, usaremos Perfil Principal no nível 3.2 (o padrão).</span><span class="sxs-lookup"><span data-stu-id="39ba9-196">For our sample, let's go with Main Profile at level 3.2 (the default).</span></span>
* <span data-ttu-id="39ba9-197">Modo de Controle de Taxa e Taxa de bits (kbps): em nosso cenário, optamos por uma saída de taxa de bits constante (CBR) de 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="39ba9-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="39ba9-198">Formato de Vídeo: trata-se da VUI (Informação de Uso do Vídeo) gravada no fluxo H.264 (informações que podem ser usadas por um decodificador para melhorar a exibição, mas que não são essenciais para decodificar corretamente):</span><span class="sxs-lookup"><span data-stu-id="39ba9-198">Video Format: this is about the VUI (Video Usability Information) that gets written into the H.264 stream (side information that might be used by a decoder to enhance the display but not essential to correctly decode):</span></span>
* <span data-ttu-id="39ba9-199">NTSC (normalmente para os Estados Unidos ou o Japão, usando 30 qps)</span><span class="sxs-lookup"><span data-stu-id="39ba9-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="39ba9-200">PAL (normalmente para a Europa, usando 25 qps)</span><span class="sxs-lookup"><span data-stu-id="39ba9-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="39ba9-201">Modo de Tamanho de GOP: configuraremos o Tamanho de GOP Fixo para nossos objetivos com um Intervalo de Chave de dois segundos com GOPs Fechados.</span><span class="sxs-lookup"><span data-stu-id="39ba9-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="39ba9-202">Isso garante a compatibilidade com o empacotamento dinâmico fornecido pelos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba9-202">This ensures compatibility with the dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="39ba9-203">Para alimentar nosso codificador de AVC, conecte o pino de saída Vídeo Descompactado do componente de Entrada de arquivo de mídia ao pino de entrada Vídeo Descompactado do codificador de AVC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-203">To feed our AVC encoder, connect the Uncompressed Video output pin from the Media File Input component to the Uncompressed Video input pin from the AVC encoder.</span></span>

![Codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="39ba9-205">*Codificador Principal de AVC conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="39ba9-206"><a id="MXF_to_MP4_audio"></a>Codificando o fluxo de áudio</span><span class="sxs-lookup"><span data-stu-id="39ba9-206"><a id="MXF_to_MP4_audio"></a>Encoding the audio stream</span></span>
<span data-ttu-id="39ba9-207">Neste ponto, codificamos o vídeo, mas o fluxo de áudio descompactado original ainda precisa ser compactado.</span><span class="sxs-lookup"><span data-stu-id="39ba9-207">At this point, we have encoded video but the original uncompressed audio stream still needs to be compressed.</span></span> <span data-ttu-id="39ba9-208">Para isso, usaremos a codificação AAC do componente Codificador AAC (Dolby).</span><span class="sxs-lookup"><span data-stu-id="39ba9-208">For this we'll go with AAC encoding by the AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="39ba9-209">Adicione-o ao fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-209">Add it to the workflow.</span></span>

![Codificador AVC desconectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="39ba9-211">*Codificador AAC desconectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="39ba9-212">Agora há uma incompatibilidade: há apenas um pino de entrada áudio descompactado no Codificador AAC, enquanto é bem provável que a Entrada do Arquivo de Mídia tenha fluxos de áudio descompactados diferentes disponíveis: um para o canal de áudio esquerdo e outro para o direito.</span><span class="sxs-lookup"><span data-stu-id="39ba9-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from the AAC Encoder while more than likely the Media File Input will have two different uncompressed audio stream available: one for the left audio channel and one for the right.</span></span> <span data-ttu-id="39ba9-213">(Se você estiver lidando com som surround, serão seis canais). Portanto, não é possível conectar diretamente o áudio da origem da Entrada do arquivo de mídia no codificador de áudio AAC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible to directly connect the audio from the Media File Input source into the AAC audio encoder.</span></span> <span data-ttu-id="39ba9-214">O componente AAC espera um chamado fluxo de áudio chamado "intercalado": um único fluxo que possui os canais esquerdo e direito intercalados entre si.</span><span class="sxs-lookup"><span data-stu-id="39ba9-214">The AAC component expects a so-called "interleaved" audio stream: a single stream that has both the left and the right channels interleaved with each other.</span></span> <span data-ttu-id="39ba9-215">Quando soubermos de nosso arquivo de mídia de origem quais faixas de áudio estão em determinada posição na origem, poderemos gerar esse fluxo de áudio intercalado com as posições de alto-falante corretamente atribuídas para os lados esquerdo e direito.</span><span class="sxs-lookup"><span data-stu-id="39ba9-215">Once we know from our source media file which audio tracks are on what position in the source, we can generate such interleaved audio stream with the correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="39ba9-216">Primeiro, convém gerar um fluxo intercalado dos canais de áudio de origem exigidos.</span><span class="sxs-lookup"><span data-stu-id="39ba9-216">First one will want to generated an interleaved stream from the required source audio channels.</span></span> <span data-ttu-id="39ba9-217">O componente Intercalador do Fluxo de Áudio tratará disso para nós.</span><span class="sxs-lookup"><span data-stu-id="39ba9-217">The Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="39ba9-218">Adicione-o ao fluxo de trabalho e conecte as saídas de áudio da Entrada do Arquivo de Mídia nele.</span><span class="sxs-lookup"><span data-stu-id="39ba9-218">Add it to the workflow and connect the audio outputs from the Media File Input into it.</span></span>

![Intercalador do fluxo de áudio conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="39ba9-220">*Intercalador do fluxo de áudio conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="39ba9-221">Agora que temos um fluxo de áudio intercalado, ainda não especificamos a qual local devemos atribuir as posições esquerda ou direita do alto-falante.</span><span class="sxs-lookup"><span data-stu-id="39ba9-221">Now that we have an interleaved audio stream, we still didn't specify where to assign the left or right speaker positions to.</span></span> <span data-ttu-id="39ba9-222">Para especificar isso, podemos usar o Atribuidor de posição de alto-falante.</span><span class="sxs-lookup"><span data-stu-id="39ba9-222">In order to specify this, we can leverage the Speaker Position Assigner.</span></span>

![Adicionando um Atribuidor de Posição do Alto-falante](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="39ba9-224">*Adicionando um Atribuidor de Posição do Alto-falante*</span><span class="sxs-lookup"><span data-stu-id="39ba9-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="39ba9-225">Configure o Atribuidor de Posição de Alto-falante para uso com um fluxo de entrada estéreo por meio de um Filtro de Predefinição do Codificador "Personalizado" e da Predefinição de Canal chamada "2.0 (L, R)".</span><span class="sxs-lookup"><span data-stu-id="39ba9-225">Configure the Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and the Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="39ba9-226">(Isso atribuirá a posição do alto-falante esquerdo ao canal 1, e a posição do alto-falante direito ao canal 2).</span><span class="sxs-lookup"><span data-stu-id="39ba9-226">(This will assign the left speaker position to channel 1 and the right speaker position to channel 2.)</span></span>

<span data-ttu-id="39ba9-227">Conecte a saída do Atribuidor de Posição do Alto-falante à entrada do Codificador AAC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-227">Connect the output of the Speaker Position Assigner to the input of the AAC Encoder.</span></span> <span data-ttu-id="39ba9-228">Em seguida, instrua o Codificador AAC a trabalhar com uma Predefinição de Canal "2.0 (L, R)", para que ele saiba lidar com o áudio estéreo como uma entrada.</span><span class="sxs-lookup"><span data-stu-id="39ba9-228">Then, tell the AAC Encoder to work with a "2.0 (L,R)" Channel Preset, so it knows to deal with stereo audio as input.</span></span>

### <span data-ttu-id="39ba9-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexando fluxos de áudio e de vídeo em um contêiner MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="39ba9-230">Com base em nosso fluxo de vídeo codificado em AVC e em nosso fluxo de áudio codificado em AAC, podemos capturar ambos em um contêiner .MP4.</span><span class="sxs-lookup"><span data-stu-id="39ba9-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="39ba9-231">O processo de mistura de fluxos diferentes em um único fluxo é chamado de "multiplexação" (ou "muxing").</span><span class="sxs-lookup"><span data-stu-id="39ba9-231">The process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="39ba9-232">Nesse caso, estamos intercalando os fluxos de áudio e de vídeo em um único pacote .MP4 coerente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-232">In this case we're interleaving the audio and the video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="39ba9-233">O componente que coordena isso para um contêiner .MP4 é chamado de Multiplexador ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="39ba9-233">The component that coordinates this for an .MP4 container is called the ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="39ba9-234">Adicione esse componente à superfície do designer e conecte o Codificador de vídeo AVC e o Codificador AAC às suas entradas.</span><span class="sxs-lookup"><span data-stu-id="39ba9-234">Add one to the designer surface and connect both the AVC Video Encoder and the AAC Encoder to its inputs.</span></span>

![Multiplexador MPEG4 conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="39ba9-236">*Multiplexador MPEG4 conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="39ba9-237"><a id="MXF_to_MP4_writing_mp4"></a>Gravando o arquivo MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing the MP4 file</span></span>
<span data-ttu-id="39ba9-238">O componente Saída do Arquivo é usado durante a gravação de um arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-238">When writing an output file, the File Output component is used.</span></span> <span data-ttu-id="39ba9-239">Podemos conectá-lo à saída do Multiplexador ISO MPEG-4 para que sua saída seja gravada em disco.</span><span class="sxs-lookup"><span data-stu-id="39ba9-239">We can connect this to the output of the ISO MPEG-4 Multiplexer so that its output gets written to disk.</span></span> <span data-ttu-id="39ba9-240">Para fazer isso, conecte o pino de saída Contêiner (MPEG-4) ao pino de entrada Gravação do Arquivo de Saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-240">To do this, connect the Container (MPEG-4) output pin to the Write input pin of the File Output.</span></span>

![Saída do arquivo conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="39ba9-242">*Saída do arquivo conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-242">*Connected File Output*</span></span>

<span data-ttu-id="39ba9-243">O nome do arquivo que será usado é determinado pela propriedade Arquivo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-243">The filename that will be used is determined by the File property.</span></span> <span data-ttu-id="39ba9-244">Embora essa propriedade possa ser codificada para um determinado valor, convém defini-la por meio de uma expressão.</span><span class="sxs-lookup"><span data-stu-id="39ba9-244">While that property can be hardcoded to a given value, most likely one will want to set it through an expression instead.</span></span>

<span data-ttu-id="39ba9-245">Para que o fluxo de trabalho determine automaticamente a propriedade de nome do Arquivo de saída a partir de uma expressão, clique no botão ao lado do Nome do arquivo (ao lado do ícone de pasta).</span><span class="sxs-lookup"><span data-stu-id="39ba9-245">To have the workflow automatically determine the output File name property from an expression, click the buton next to the File name (next to the folder icon).</span></span> <span data-ttu-id="39ba9-246">No menu suspenso, selecione "Expressão".</span><span class="sxs-lookup"><span data-stu-id="39ba9-246">From the drop down menu then select "Expression".</span></span> <span data-ttu-id="39ba9-247">Isso abrirá o editor de expressão.</span><span class="sxs-lookup"><span data-stu-id="39ba9-247">This will bring up the expression editor.</span></span> <span data-ttu-id="39ba9-248">Primeiro, limpe o conteúdo do editor.</span><span class="sxs-lookup"><span data-stu-id="39ba9-248">Clear the contents of the editor first.</span></span>

![Editor de expressão vazio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="39ba9-250">*Editor de expressão vazio*</span><span class="sxs-lookup"><span data-stu-id="39ba9-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="39ba9-251">O editor de expressão permite a inserção de qualquer valor literal, combinado com uma ou mais variáveis.</span><span class="sxs-lookup"><span data-stu-id="39ba9-251">The expression editor allows to enter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="39ba9-252">As variáveis começam com um sinal de cifrão.</span><span class="sxs-lookup"><span data-stu-id="39ba9-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="39ba9-253">Quando você pressiona a tecla $, o editor mostra uma caixa suspensa com as variáveis disponíveis para sua escolha.</span><span class="sxs-lookup"><span data-stu-id="39ba9-253">As you hit the $ key, the editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="39ba9-254">Em nosso caso, usaremos uma combinação da variável do diretório de saída e da variável básica de nome do arquivo de entrada:</span><span class="sxs-lookup"><span data-stu-id="39ba9-254">In our case we'll use a combination of the output directory variable and the base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Editor de expressão preenchido](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="39ba9-256">*Editor de expressão preenchido*</span><span class="sxs-lookup"><span data-stu-id="39ba9-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="39ba9-257">Para ver um arquivo de saída de seu trabalho de codificação no Azure, você deve fornecer um valor no editor de expressão.</span><span class="sxs-lookup"><span data-stu-id="39ba9-257">In order to see see an output file of your encoding job in Azure, you must provide a value in the expression editor.</span></span>
>
>

<span data-ttu-id="39ba9-258">Quando você confirma a expressão clicando em ok, a janela de propriedade mostra para que valor a propriedade Arquivo é resolvida neste momento.</span><span class="sxs-lookup"><span data-stu-id="39ba9-258">When you confirm the expression by hitting ok, the property window will preview to what value the File property resolves at this point in time.</span></span>

![Diretório de saída de resolução da Expressão do Arquivo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="39ba9-260">*Diretório de saída de resolução da Expressão do Arquivo*</span><span class="sxs-lookup"><span data-stu-id="39ba9-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="39ba9-261"><a id="MXF_to_MP4_asset_from_output"></a>Criando um Ativo dos Serviços de Mídia do arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="39ba9-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from the output file</span></span>
<span data-ttu-id="39ba9-262">Embora tenhamos escrito um arquivo de saída MP4, ainda precisamos indicar que este arquivo pertence ao ativo de saída que os Serviços de Mídia gerarão como resultado da execução deste fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-262">While we have written an MP4 output file, we still need to indicate that this file belongs to the output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="39ba9-263">Para essa finalidade, usamos o nó Arquivo/Ativo de Saída na tela do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-263">To this end, the Output File/Asset node on the workflow canvas is used.</span></span> <span data-ttu-id="39ba9-264">Todos os arquivos recebidos nesse nó farão parte do ativo resultante dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba9-264">All incoming files into this node will make part of the resulting Azure Media Services asset.</span></span>

<span data-ttu-id="39ba9-265">Conecte o componente Saída do Arquivo ao componente Arquivo/Ativo de Saída para concluir o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-265">Connect the File Output component to the Output File/Asset component to finish the workflow.</span></span>

![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="39ba9-267">*Fluxo de trabalho concluído*</span><span class="sxs-lookup"><span data-stu-id="39ba9-267">*Finished Workflow*</span></span>

### <span data-ttu-id="39ba9-268"><a id="MXF_to_MP4_test"></a>Testar o fluxo de trabalho concluído localmente</span><span class="sxs-lookup"><span data-stu-id="39ba9-268"><a id="MXF_to_MP4_test"></a>Test the finished workflow locally</span></span>
<span data-ttu-id="39ba9-269">Para testar o fluxo de trabalho localmente, pressione o botão Executar na barra de ferramentas superior.</span><span class="sxs-lookup"><span data-stu-id="39ba9-269">To test the workflow locally, hit the play button in the toolbar at the top.</span></span> <span data-ttu-id="39ba9-270">Após a conclusão da execução do fluxo de trabalho, inspecione a saída gerada na pasta de saída configurada.</span><span class="sxs-lookup"><span data-stu-id="39ba9-270">When the workflow finished executing, inspect the output generated in the configured output folder.</span></span> <span data-ttu-id="39ba9-271">Você verá o arquivo de saída MP4 concluído que foi codificado a partir do arquivo de origem de entrada MXF.</span><span class="sxs-lookup"><span data-stu-id="39ba9-271">You'll see the finished MP4 output file that was encoded from the MXF input source file.</span></span>

## <span data-ttu-id="39ba9-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codificação do MXF em MP4 - empacotamento dinâmico com várias taxas bits habilitado</span><span class="sxs-lookup"><span data-stu-id="39ba9-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="39ba9-273">Neste passo a passo, criaremos um conjunto de arquivos MP4 com várias taxas de bits e áudio codificado em AAC a partir de um único arquivo de entrada .MXF.</span><span class="sxs-lookup"><span data-stu-id="39ba9-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="39ba9-274">Quando houver o desejo por uma saída de ativo com várias taxas de bit para uso junto com os recursos de Empacotamento dinâmico oferecidos pelos Serviços de Mídia do Azure, será necessário gerar vários arquivos MP4 alinhados com GOP de cada taxa de bits e resolução diferentes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-274">When a multi-bitrate asset output is desired for use in combination with the Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need to be generated.</span></span> <span data-ttu-id="39ba9-275">Para fazer isso, o passo a passo [Codificação do MXF em um MP4 de taxa de bits única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) fornece um bom ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="39ba9-275">To do so, the [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Como iniciar o fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="39ba9-277">*Como iniciar o fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="39ba9-277">*Starting Workflow*</span></span>

### <span data-ttu-id="39ba9-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adicionando uma ou mais saídas MP4</span><span class="sxs-lookup"><span data-stu-id="39ba9-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="39ba9-279">Cada arquivo MP4 em nosso ativo resultante dos Serviços de Mídia do Azure oferecerá suporte a uma taxa de bits e resolução diferentes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="39ba9-280">Vamos adicionar um ou mais arquivos de saída MP4 ao fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-280">Let's add one or more MP4 output files to the workflow.</span></span>

<span data-ttu-id="39ba9-281">Para termos certeza de que todos os nossos codificadores de vídeo foram criados com as mesmas configurações, é mais conveniente duplicar o Codificador de vídeo AVC já existente e configurar outra combinação de resolução e taxa de bits (vamos adicionar uma de 960 x 540 a 25 quadros por segundo a 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="39ba9-281">To make sure we have all our video encoders created with the same settings, it's most convenient to duplicate the already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="39ba9-282">Para duplicar o codificador existente, copie e cole-o na superfície do designer.</span><span class="sxs-lookup"><span data-stu-id="39ba9-282">To duplicate the existing encoder, copy paste it on the designer surface.</span></span>

<span data-ttu-id="39ba9-283">Conecte o pino de saída Vídeo Descompactado da Entrada do Arquivo de Mídia ao nosso novo componente AVC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-283">Connect the Uncompressed Video output pin of the Media File Input into our new AVC component.</span></span>

![Segundo codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="39ba9-285">*Segundo codificador AVC conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="39ba9-286">Agora, adapte a configuração de nosso novo codificador AVC para a saída 960 x 540 a 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="39ba9-286">Now adapt the configuration for our new AVC encoder to output 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="39ba9-287">(Use as propriedades "Largura de saída", "Altura de saída" e "Taxa de bits (kbps)" para isso).</span><span class="sxs-lookup"><span data-stu-id="39ba9-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="39ba9-288">Considerando que queremos usar o ativo resultante junto com o empacotamento dinâmico dos Serviços de Mídia do Azure, o ponto de extremidade de streaming precisa ser capaz de gerar a partir dos fragmentos MP4/DASH HLS/Fragmentados desses arquivos MP4, que são exatamente alinhados entre si de uma maneira que os clientes que alternam entre taxas de bits diferentes obtenham uma experiência de vídeo e áudio contínua e suave.</span><span class="sxs-lookup"><span data-stu-id="39ba9-288">Given we want to use the resulting asset together with Azure Media Services' dynamic packaging, the streaming endpoint needs to be capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned to each other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="39ba9-289">Para fazer isso acontecer, precisamos garantir que o tamanho do GOP ("grupo de imagens") dos dois arquivos MP4 seja definido como dois segundos nas propriedades dos codificadores AVC, o que pode ser feito da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="39ba9-289">To make that happen, we need to ensure that, in the properties of both AVC encoders the GOP ("group of pictures") size for both MP4 files is set to 2 seconds, which can be done by:</span></span>

* <span data-ttu-id="39ba9-290">Definindo o Modo de Tamanho do GOP como o tamanho GOP Fixo e</span><span class="sxs-lookup"><span data-stu-id="39ba9-290">setting the GOP Size Mode to Fixed GOP size and</span></span>
* <span data-ttu-id="39ba9-291">O Intervalo de Quadro Principal como dois segundos.</span><span class="sxs-lookup"><span data-stu-id="39ba9-291">the Key Frame Interval to two seconds.</span></span>
* <span data-ttu-id="39ba9-292">Além disso, defina o Controle IDR do GOP como GOP Fechado a fim de garantir que todos os GOPs fiquem ativos sem dependências</span><span class="sxs-lookup"><span data-stu-id="39ba9-292">also set the GOP IDR Control to Closed GOP to ensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="39ba9-293">Para facilitar a compreensão de nosso o fluxo de trabalho, renomeie o primeiro codificador AVC como "Codificador de Vídeo AVC 640 x 360 1200 kbps" e o segundo codificador AVC como"Codificador de Vídeo AVC 960 x 540 2500 kbps".</span><span class="sxs-lookup"><span data-stu-id="39ba9-293">To make our workflow convenient to understand, rename the first AVC encoder to "AVC Video Encoder 640x360 1200kbps" and the second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="39ba9-294">Agora, adicione um segundo Multiplexador ISO MPEG-4 e uma segunda Saída de arquivo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="39ba9-295">Conecte o multiplexador ao novo codificador AVC e certifique-se de que sua saída seja direcionada para o Arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-295">Connect the multiplexer to the new AVC encoder and make sure its output is directed into the File Output.</span></span> <span data-ttu-id="39ba9-296">Conecte também a saída do codificador de áudio AAC à entrada do novo multiplexador.</span><span class="sxs-lookup"><span data-stu-id="39ba9-296">Then also connect the AAC audio encoder output to the new multiplexer's input.</span></span> <span data-ttu-id="39ba9-297">A Saída do arquivo, por sua vez, pode ser conectada ao nó Arquivo/Ativo de Saída a fim de adicioná-la ao Ativo dos Serviços de Mídia que será criado.</span><span class="sxs-lookup"><span data-stu-id="39ba9-297">The File Output in turn can then be connected to the Output File/Asset node to add it to the Media Services Asset that will be created.</span></span>

![Segundo Muxer e Saída do arquivo conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="39ba9-299">*Segundo Muxer e Saída do arquivo conectado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="39ba9-300">Para manter a compatibilidade com o empacotamento dinâmico dos Serviços de Mídia do Azure, configure Modo de Partes do multiplexador para contagem ou duração de GOP e defina os GOPs por parte como 1.</span><span class="sxs-lookup"><span data-stu-id="39ba9-300">For compatibility with Azure Media Services dynamic packaging, configure the multiplexer's Chunk Mode to GOP count or duration and set the GOPs per chunk to 1.</span></span> <span data-ttu-id="39ba9-301">(Esse deve ser o padrão).</span><span class="sxs-lookup"><span data-stu-id="39ba9-301">(This should be the default.)</span></span>

![Modos de parte do muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="39ba9-303">*Modos de parte do muxer*</span><span class="sxs-lookup"><span data-stu-id="39ba9-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="39ba9-304">Observação: convém repetir esse processo para qualquer outra combinação de resolução e taxa de bits que você deseja adicionar à saída do ativo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-304">Note: you may want to repeat this process for any other bitrate and resolution combinations you want to have added to the asset output.</span></span>

### <span data-ttu-id="39ba9-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configurando os nomes de saída do arquivo</span><span class="sxs-lookup"><span data-stu-id="39ba9-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring the file output names</span></span>
<span data-ttu-id="39ba9-306">Mais de um arquivo foi adicionado ao ativo de saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-306">We have more than one single file added to the output asset.</span></span> <span data-ttu-id="39ba9-307">Com isso, é necessário se certificar de que os nomes de arquivo de cada um dos arquivos de saída sejam diferentes uns dos outros, e talvez até mesmo aplicar uma convenção de nomenclatura de arquivo para que fique claro, a partir do nome do arquivo, com o você está lidando.</span><span class="sxs-lookup"><span data-stu-id="39ba9-307">This provides a need to make sure the filenames for each of the output files are different from each other and maybe even apply a file-naming convention so it becomes clear from the file name what you're dealing with.</span></span>

<span data-ttu-id="39ba9-308">A nomenclatura de saída do arquivo pode ser controlada por meio de expressões no designer.</span><span class="sxs-lookup"><span data-stu-id="39ba9-308">File output naming can be controlled through expressions in the designer.</span></span> <span data-ttu-id="39ba9-309">Abra o painel de propriedades de um dos componentes de Saída do arquivo, e abra o editor de expressão para a propriedade Arquivo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-309">Open the property pane for one of the File Output components and open the expression editor for the File property.</span></span> <span data-ttu-id="39ba9-310">Nosso primeiro arquivo de saída foi configurado por meio da seguinte expressão (consulte o tutorial para ir de um [MXF para uma saída MP4 taxa de bits única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="39ba9-310">Our first output file was configured through the following expression (see the tutorial for going from [MXF to a single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="39ba9-311">Isso significa que nosso nome de arquivo é determinado por duas variáveis: o diretório de saída para gravação e o nome base do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="39ba9-311">This means that our filename is determined by two variables: the output directory to write in and the source file base name.</span></span> <span data-ttu-id="39ba9-312">O primeiro é exposto como uma propriedade na raiz do fluxo de trabalho, e o último é determinado pelo arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="39ba9-312">The former is exposed as a property on the workflow root and the latter is determined by the incoming file.</span></span> <span data-ttu-id="39ba9-313">Observe que o diretório de saída é usado para teste local; essa propriedade será substituída pelo mecanismo de fluxo de trabalho, quando o fluxo de trabalho for executado pelo processador de mídia baseado em nuvem nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba9-313">Note that the output directory is what you use for local testing; this property will be overridden by the workflow engine when the workflow is executed by the cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="39ba9-314">Para atribuir aos nossos dois arquivos de saída uma nomenclatura de saída consistente, altere a primeira expressão de nomenclatura de arquivo para:</span><span class="sxs-lookup"><span data-stu-id="39ba9-314">To give both our output files a consistent output naming, change the first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="39ba9-315">e a segunda para:</span><span class="sxs-lookup"><span data-stu-id="39ba9-315">and the second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="39ba9-316">Execute uma execução de teste intermediária para se certificar de que os dois arquivos de saída MP4 foram gerados corretamente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-316">Execute an intermediate test run to make sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="39ba9-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adicionando uma Trilha de Áudio separada</span><span class="sxs-lookup"><span data-stu-id="39ba9-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="39ba9-318">Como veremos posteriormente ao gerarmos um arquivo .ism para acompanhar nossos arquivos de saída MP4, também precisaremos de um arquivo MP4 somente de áudio como a trilha de áudio para nosso streaming adaptável.</span><span class="sxs-lookup"><span data-stu-id="39ba9-318">As we'll see later when we generate an .ism file to go with our MP4 output files, we will also require a audio-only MP4 file as the audio track for our adaptive streaming.</span></span> <span data-ttu-id="39ba9-319">Para criar esse arquivo, adicione outro muxer ao fluxo de trabalho (Multiplexador ISO-MPEG-4) e conecte o pino de saída do codificador AAC ao seu pino de entrada para a Trilha 1.</span><span class="sxs-lookup"><span data-stu-id="39ba9-319">To create this file, add an additional muxer to the workflow (ISO-MPEG-4 Multiplexer) and connect the AAC encoder's output pin with its input pin for Track 1.</span></span>

![Muxer de áudio adicionado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="39ba9-321">*Muxer de áudio adicionado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="39ba9-322">Crie um terceiro componente de Saída do arquivo para mostrar o fluxo de saída do muxer e configurar a expressão de nomenclatura do arquivo como:</span><span class="sxs-lookup"><span data-stu-id="39ba9-322">Create a third File Output component to output the outbound stream from the muxer and configure the file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Criação de Saída do arquivo pelo muxer de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="39ba9-324">*Criação de Saída do arquivo pelo muxer de áudio*</span><span class="sxs-lookup"><span data-stu-id="39ba9-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="39ba9-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adicionando o arquivo SMIL .ISM</span><span class="sxs-lookup"><span data-stu-id="39ba9-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding the .ISM SMIL File</span></span>
<span data-ttu-id="39ba9-326">Para o empacotamento dinâmico funcionar junto com os dois arquivos MP4 (e com o MP4 somente de áudio) em nosso ativo dos Serviços de Mídia, também precisamos de um arquivo de manifesto (também chamado de arquivo "SMIL": Linguagem de integração de multimídia sincronizada).</span><span class="sxs-lookup"><span data-stu-id="39ba9-326">For the dynamic packaging to work in combination with both MP4 files (and the audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="39ba9-327">Esse arquivo indica aos Serviços de Mídia do Azure quais são os arquivos MP4 que estão disponíveis para empacotamento dinâmico e quais deles devem ser considerados para o streaming de áudio.</span><span class="sxs-lookup"><span data-stu-id="39ba9-327">This file indicates to Azure Media Services what MP4 files are available for dynamic packaging and which of those to consider for the audio streaming.</span></span> <span data-ttu-id="39ba9-328">Um arquivo de manifesto típico para um conjunto de MP4s com um único fluxo de áudio tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="39ba9-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

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

<span data-ttu-id="39ba9-329">O arquivo .ism contém uma instrução switch, uma referência a cada um dos arquivos de vídeo MP4 individuais e também uma (ou mais) referências de arquivo de áudio para um MP4 que contém apenas o áudio.</span><span class="sxs-lookup"><span data-stu-id="39ba9-329">The .ism file contains within a switch statement, a reference to each of the individual MP4 video files and in addition to those also one (or more) audio file references to an MP4 that only contains the audio.</span></span>

<span data-ttu-id="39ba9-330">A geração do arquivo de manifesto para nosso conjunto de MP4s pode ser realizada por meio de um componente chamado de "Gravador de Manifesto AMS".</span><span class="sxs-lookup"><span data-stu-id="39ba9-330">Generating the manifest file for our set of MP4's can be done through a component called the "AMS Manifest Writer".</span></span> <span data-ttu-id="39ba9-331">Para usá-lo, arraste-o para a superfície e conecte os pinos de saída "Gravação Concluída" dos três componentes de Saída de arquivo com a entrada do Gravador de Manifesto AMS.</span><span class="sxs-lookup"><span data-stu-id="39ba9-331">To use it, drag it onto the surface and connect the "Write Complete" output pins from the three File Output components to the AMS Manifest Writer input.</span></span> <span data-ttu-id="39ba9-332">Em seguida, conecte a saída do Gravador de Manifesto AMS ao Arquivo/Ativo de Saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-332">Then make sure to connect the output of the AMS Manifest Writer to the Output File/Asset.</span></span>

<span data-ttu-id="39ba9-333">Assim como nossos outros componentes de saída do arquivo, configure o nome de saída do arquivo .ism com uma expressão:</span><span class="sxs-lookup"><span data-stu-id="39ba9-333">As with our other file output components, configure the .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="39ba9-334">Nosso fluxo de trabalho concluído é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="39ba9-334">Our finished workflow looks like the below:</span></span>

![Fluxo de trabalho concluído de MXF para MP4 com várias taxas de bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="39ba9-336">*Fluxo de trabalho concluído de MXF para MP4 com várias taxas de bit*</span><span class="sxs-lookup"><span data-stu-id="39ba9-336">*Finished MXF to multibitrate MP4 workflow*</span></span>

## <span data-ttu-id="39ba9-337"><a id="MXF_to__multibitrate_MP4"></a>Codificando MXF em MP4 com várias taxas de bit - plano gráfico aprimorado</span><span class="sxs-lookup"><span data-stu-id="39ba9-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="39ba9-338">No [passo a passo do fluxo de trabalho anterior](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) vimos como um único ativo de entrada MXF pode ser convertido em um ativo de saída com arquivos MP4 com várias taxas de bits, um arquivo MP4 somente áudio e um arquivo de manifesto para uso em conjunto com o empacotamento dinâmico dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba9-338">In the [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="39ba9-339">Este passo a passo mostrará como alguns dos aspectos podem ser aprimorados e tornados mais convenientes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-339">This walkthrough will show how some of the aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="39ba9-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Visão geral do fluxo de trabalho para aprimoramento</span><span class="sxs-lookup"><span data-stu-id="39ba9-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview to enhance</span></span>
![Fluxo de trabalho de MP4 com várias taxas de bit para aprimoramento](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="39ba9-342">*Fluxo de trabalho de MP4 com várias taxas de bit para aprimoramento*</span><span class="sxs-lookup"><span data-stu-id="39ba9-342">*Multibitrate MP4 workflow to enhance*</span></span>

### <span data-ttu-id="39ba9-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenções de nomenclatura do arquivo</span><span class="sxs-lookup"><span data-stu-id="39ba9-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="39ba9-344">No fluxo de trabalho anterior especificamos uma expressão simples como base para a geração de nomes de arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-344">In the previous workflow we specified a simple expression as the basis for generating output file names.</span></span> <span data-ttu-id="39ba9-345">No entanto, temos algumas duplicações: todos os componentes individuais do arquivo de saída especificaram essa expressão.</span><span class="sxs-lookup"><span data-stu-id="39ba9-345">We have some duplication though: all of the the individual output file components specified such expression.</span></span>

<span data-ttu-id="39ba9-346">Por exemplo, nosso componente de saída de arquivo para o primeiro arquivo de vídeo está configurado com esta expressão:</span><span class="sxs-lookup"><span data-stu-id="39ba9-346">For example, our file output component for the first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="39ba9-347">Enquanto no segundo vídeo de saída, temos uma expressão como esta:</span><span class="sxs-lookup"><span data-stu-id="39ba9-347">While for the second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="39ba9-348">Não seria mais claro, menos propenso a erros e mais conveniente se pudéssemos remover algumas essas duplicações e tornar as coisas mais configuráveis?</span><span class="sxs-lookup"><span data-stu-id="39ba9-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="39ba9-349">Felizmente, podemos fazer isso: os recursos de expressão do designer em combinação com a capacidade de criar propriedades personalizadas na raiz de nosso fluxo de trabalho nos proporcionará um pouco mais de conveniência.</span><span class="sxs-lookup"><span data-stu-id="39ba9-349">Luckily we can: the designer's expression capabilities in combination with the ability to create custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="39ba9-350">Vamos supor que obteremos a configuração de nome do arquivo com base nas taxas de bits dos arquivos MP4 individuais.</span><span class="sxs-lookup"><span data-stu-id="39ba9-350">Let's assume we'll drive filename configuration from the bitrates of the individual MP4 files.</span></span> <span data-ttu-id="39ba9-351">Nosso objetivo é configurar essas taxas de bit em um local central (na raiz de nosso gráfico), de onde poderão ser acessadas para configurar e realizar a geração de nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-351">These bitrates we'll aim to configure in one central place (on the root of our graph), from where they'll be accessed to configure and drive file name generation.</span></span> <span data-ttu-id="39ba9-352">Para fazer isso, começamos publicando a propriedade de taxa de bits a partir dos dois codificadores AVC até a raiz de nosso fluxo de trabalho, de modo que fique acessível a partir da raiz e dos codificadores AVC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-352">To do this, we start by publishing the bitrate property from both AVC encoders to the root of our workflow, so that it becomes accessible from both the root as well as from the AVC encoders.</span></span> <span data-ttu-id="39ba9-353">(Mesmo se for exibido em dois pontos diferentes, haverá apenas um valor subjacente).</span><span class="sxs-lookup"><span data-stu-id="39ba9-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="39ba9-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publicando as propriedades do componente na raiz do fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto the workflow root</span></span>
<span data-ttu-id="39ba9-355">Abra o primeiro codificador AVC, vá até a propriedade Taxa de bits (kbps) e, no menu suspenso, selecione Publicar.</span><span class="sxs-lookup"><span data-stu-id="39ba9-355">Open the first AVC encoder, go to the Bitrate (kbps) property and from the dropdown choose Publish.</span></span>

![Publicando a propriedade de taxa de bits](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="39ba9-357">*Publicando a propriedade de taxa de bits*</span><span class="sxs-lookup"><span data-stu-id="39ba9-357">*Publishing the bitrate property*</span></span>

<span data-ttu-id="39ba9-358">Configure a caixa de diálogo Publicar para publicar a raiz do nosso gráfico de fluxo de trabalho, com o nome publicado de "video1bitrate" e um nome de exibição legível de "Taxa de Bits do Vídeo 1".</span><span class="sxs-lookup"><span data-stu-id="39ba9-358">Configure the publish dialog to publish to the root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="39ba9-359">Configure um nome do grupo personalizado chamado "Taxas de Bits de Streaming" e toque em Publicar.</span><span class="sxs-lookup"><span data-stu-id="39ba9-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Publicando a propriedade de taxa de bits](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="39ba9-361">*Caixa de diálogo de publicação para a propriedade de taxa de bits*</span><span class="sxs-lookup"><span data-stu-id="39ba9-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="39ba9-362">Repita o mesmo para a propriedade de taxa de bits do segundo codificador AVC e nomeie-o como "video2bitrate" com um nome de exibição de "Taxas de Bits do Vídeo 2", no mesmo grupo personalizado "Taxas de Bits de Streaming".</span><span class="sxs-lookup"><span data-stu-id="39ba9-362">Repeat the same for the bitrate property of the second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in the same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="39ba9-363">Se agora inspecionarmos as propriedades raiz do fluxo de trabalho, veremos nosso grupo personalizado com as duas propriedades publicados em exibição.</span><span class="sxs-lookup"><span data-stu-id="39ba9-363">If we now inspect the workflow root properties, we'll see our custom group with the two published properties show up.</span></span> <span data-ttu-id="39ba9-364">Ambas refletem o valor de suas respectivas taxas de bits do codificador AVC.</span><span class="sxs-lookup"><span data-stu-id="39ba9-364">Both are reflecting the value of their respective AVC encoder bitrate.</span></span>

![Propriedades de taxa de bits publicadas na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="39ba9-366">Sempre que quisermos acessar essas propriedades a partir do código ou de uma expressão, poderemos fazer isso da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="39ba9-366">Whenever we want to access these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="39ba9-367">no código embutido de um componente logo abaixo da raiz: node.getPropertyAsString('../video1bitrate',null)</span><span class="sxs-lookup"><span data-stu-id="39ba9-367">from inline code from a component right below the root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="39ba9-368">em uma expressão: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="39ba9-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="39ba9-369">Vamos concluir o grupo "Taxas de Bits de Streaming" publicando também a taxa de bits de nossa trilha de áudio.</span><span class="sxs-lookup"><span data-stu-id="39ba9-369">Let's complete the "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="39ba9-370">Nas propriedades do Codificador AAC, procure pela configuração de Taxa de bits e selecione Publicar no menu suspenso ao lado dela.</span><span class="sxs-lookup"><span data-stu-id="39ba9-370">Within the properties of the AAC Encoder, search for the Bitrate setting and select Publish from the dropdown next to it.</span></span> <span data-ttu-id="39ba9-371">Publique na raiz do gráfico com o nome "audio1bitrate" e exiba o nome "Taxa de Bits do Áudio 1" em nosso grupo personalizado "Taxas de Bits de Streaming".</span><span class="sxs-lookup"><span data-stu-id="39ba9-371">Publish to the root of the graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Caixa de diálogo de publicação para a taxa de bits de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="39ba9-373">*Caixa de diálogo de publicação para a taxa de bits de áudio*</span><span class="sxs-lookup"><span data-stu-id="39ba9-373">*Publishing dialog for audio bitrate*</span></span>

![Propriedades de áudio e vídeos resultantes na raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="39ba9-375">*Propriedades de áudio e vídeos resultantes na raiz*</span><span class="sxs-lookup"><span data-stu-id="39ba9-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="39ba9-376">Observe que a alteração de qualquer um desses três valores também reconfigura e altera os valores nos respectivos componentes aos quais estão vinculados (e dos quais foram publicados).</span><span class="sxs-lookup"><span data-stu-id="39ba9-376">Note that changing any of those three values also re-configures and changes the values on the respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="39ba9-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Faça com que os nomes de arquivo de saída gerados dependam dos valores de propriedade publicados</span><span class="sxs-lookup"><span data-stu-id="39ba9-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="39ba9-378">Em vez de codificar nossos nomes de arquivo gerados, podemos mudar nossa expressão de nome de arquivo em cada um dos componentes de Arquivo de saída, a fim de depender das propriedades de taxa de bits que acabamos de publicar na raiz do gráfico.</span><span class="sxs-lookup"><span data-stu-id="39ba9-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of the File Output components to rely on the bitrate properties we just published on the graph root.</span></span> <span data-ttu-id="39ba9-379">Começando com nossa primeira saída de arquivo, encontre a propriedade Arquivo e edite a expressão da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="39ba9-379">Starting with our first file output, find the File property and edit the expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="39ba9-380">Os parâmetros diferentes nessa expressão podem ser acessados e inseridos pressionando o sinal de cifrão no teclado enquanto estiver na janela de expressão.</span><span class="sxs-lookup"><span data-stu-id="39ba9-380">The different parameters in this expression can be accessed and entered by hitting the dollar sign on the keyboard while in the expression window.</span></span> <span data-ttu-id="39ba9-381">Um dos parâmetros disponíveis é nossa propriedade video1bitrate que publicamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-381">One of the available parameters is our video1bitrate property which we published earlier.</span></span>

![Acessando parâmetros dentro de uma expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="39ba9-383">*Acessando parâmetros dentro de uma expressão*</span><span class="sxs-lookup"><span data-stu-id="39ba9-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="39ba9-384">Faça o mesmo para a saída de arquivo de nosso segundo vídeo:</span><span class="sxs-lookup"><span data-stu-id="39ba9-384">Do the same for the file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="39ba9-385">e para a saída do arquivo somente de áudio:</span><span class="sxs-lookup"><span data-stu-id="39ba9-385">and for the audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="39ba9-386">Se agora alterarmos a taxa de bits de qualquer um dos arquivos de áudio ou de vídeo, o respectivo codificador será reconfigurado e a convenção de nomenclatura de arquivos com base na taxa de bits será respeitada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-386">If we now change the bitrate for any of the video or audio files, the respective encoder will be reconfigured and the bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="39ba9-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adicionando miniaturas à saída MP4 com várias taxas de bit</span><span class="sxs-lookup"><span data-stu-id="39ba9-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails to multibitrate MP4 output</span></span>
<span data-ttu-id="39ba9-388">Começando em um fluxo de trabalho que gera [uma saída MP4 com várias taxas de bit a partir de uma entrada MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), agora vamos analisar como adicionar miniaturas à saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails to the output.</span></span>

### <span data-ttu-id="39ba9-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Visão geral do fluxo de trabalho para adição de miniaturas</span><span class="sxs-lookup"><span data-stu-id="39ba9-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview to add thumbnails to</span></span>
![Fluxo de trabalho de MP4 com várias taxas de bit para começar](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="39ba9-391">*Fluxo de trabalho de MP4 com várias taxas de bit para começar*</span><span class="sxs-lookup"><span data-stu-id="39ba9-391">*Multibitrate MP4 workflow to start from*</span></span>

### <span data-ttu-id="39ba9-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adicionando codificação JPG</span><span class="sxs-lookup"><span data-stu-id="39ba9-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="39ba9-393">A essência de nossa geração de miniaturas será o componente Codificador de JPG, capaz de gerar arquivos JPG.</span><span class="sxs-lookup"><span data-stu-id="39ba9-393">The heart of our thumbnail generation will be the JPG Encoder component, able to output JPG files.</span></span>

![Codificador de JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="39ba9-395">*Codificador de JPG*</span><span class="sxs-lookup"><span data-stu-id="39ba9-395">*JPG Encoder*</span></span>

<span data-ttu-id="39ba9-396">No entanto, não podemos conectar diretamente nosso fluxo de Vídeo Descompactado da Entrada do Arquivo de Mídia para o codificador de JPG.</span><span class="sxs-lookup"><span data-stu-id="39ba9-396">We cannot however directly connect our Uncompressed Video stream from the Media File Input into the JPG encoder.</span></span> <span data-ttu-id="39ba9-397">Em vez disso, ele espera receber quadros individuais.</span><span class="sxs-lookup"><span data-stu-id="39ba9-397">Instead, it expects to be handed individual frames.</span></span> <span data-ttu-id="39ba9-398">Isso podemos fazer por meio do componente Portão de quadro do vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-398">This, we can do through the Video Frame Gate component.</span></span>

![Conectando um portão de quadro ao codificador de JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="39ba9-400">*Conectando um portão de quadro ao codificador de JPG*</span><span class="sxs-lookup"><span data-stu-id="39ba9-400">*Connecting a frame gate to the JPG encoder*</span></span>

<span data-ttu-id="39ba9-401">O portão de quadro permite, uma vez a cada vários segundos ou quadros, a passagem de um quadro de vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-401">The frame gate once every so many seconds or frames allows a video frame to pass.</span></span> <span data-ttu-id="39ba9-402">O intervalo e o deslocamento de tempo com base no qual isso ocorre pode ser configurado nas propriedades.</span><span class="sxs-lookup"><span data-stu-id="39ba9-402">The interval and the time offset with which this happens is configurable in the properties.</span></span>

![Propriedades do Portão de Quadro do Vídeo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="39ba9-404">*Propriedades do Portão de Quadro do Vídeo*</span><span class="sxs-lookup"><span data-stu-id="39ba9-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="39ba9-405">Vamos criar uma miniatura a cada minuto definindo o modo como Tempo (segundos) e o Intervalo como 60.</span><span class="sxs-lookup"><span data-stu-id="39ba9-405">Let's create a thumbnail every minute by setting the mode to Time (seconds) and the Interval to 60.</span></span>

### <span data-ttu-id="39ba9-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Lidando com a conversão de espaço de cor</span><span class="sxs-lookup"><span data-stu-id="39ba9-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="39ba9-407">Embora pareça lógico que os pinos de Vídeo Descompactado do portão de quadro e a Entrada do Arquivo de Mídia possam ser conectados agora, receberíamos um aviso se fizéssemos isso.</span><span class="sxs-lookup"><span data-stu-id="39ba9-407">While it would seem logical both Uncompressed Video pins of the frame gate and the Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Erro no espaço de cor de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="39ba9-409">*Erro no espaço de cor de entrada*</span><span class="sxs-lookup"><span data-stu-id="39ba9-409">*Input color space error*</span></span>

<span data-ttu-id="39ba9-410">Isso ocorre por que a maneira com a qual as informações de cores são representadas em nosso fluxo original bruto de vídeo descompactado, provenientes de nosso MXF, é diferente do esperado pelo Codificador de JPG.</span><span class="sxs-lookup"><span data-stu-id="39ba9-410">This is because the way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what the JPG Encoder is expecting.</span></span> <span data-ttu-id="39ba9-411">Mais especificamente, algo chamado "espaço de cores" de "RGB" ou "Escala de cinza" é esperado.</span><span class="sxs-lookup"><span data-stu-id="39ba9-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected to flow in.</span></span> <span data-ttu-id="39ba9-412">Isso significa que o fluxo de vídeo de entrada do Portão de Quadro do Vídeo precisará ter uma conversão aplicada com relação a seu espaço de cores.</span><span class="sxs-lookup"><span data-stu-id="39ba9-412">This means that the Video Frame Gate's inbound video stream will need to have a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="39ba9-413">Arraste o Conversor de Espaço de Cor - Intel até o fluxo de trabalho e conecte-o ao nosso portão de quadro.</span><span class="sxs-lookup"><span data-stu-id="39ba9-413">Drag onto the workflow the Color Space Converter - Intel and connect it to our frame gate.</span></span>

![Conexão de um Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="39ba9-415">*Conexão de um Conversor de Espaço de Cor*</span><span class="sxs-lookup"><span data-stu-id="39ba9-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="39ba9-416">Na janela Propriedades, selecione a entrada BGR 24 na lista de Predefinições.</span><span class="sxs-lookup"><span data-stu-id="39ba9-416">In the properties window, pick the BGR 24 entry from the Preset list.</span></span>

### <span data-ttu-id="39ba9-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Gravando as miniaturas</span><span class="sxs-lookup"><span data-stu-id="39ba9-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing the thumbnails</span></span>
<span data-ttu-id="39ba9-418">Diferente do nossos vídeos MP4, o componente do Codificador de JPG produzirá mais de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-418">Different from our MP4 video's, the JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="39ba9-419">Para lidar com isso, é possível usar um componente de Gravador de arquivo JPG de Pesquisa de cena: ele usará as miniaturas JPG recebidas e as gravará, com cada nome de arquivo recebendo como sufixo um número diferente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-419">In order to deal with this, a Scene Search JPG File Writer component can be used: it will take the incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="39ba9-420">(O número normalmente indicando o número de segundos/unidades no fluxo do qual a miniatura foi extraída).</span><span class="sxs-lookup"><span data-stu-id="39ba9-420">(The number typically indicating the number of seconds/units in the stream which the thumbnail was drawn from.)</span></span>

![Apresentação do Gravador de arquivo JPG de Pesquisa de cena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="39ba9-422">*Apresentação do Gravador de arquivo JPG de Pesquisa de cena*</span><span class="sxs-lookup"><span data-stu-id="39ba9-422">*Introducing the Scene Search JPG File Writer*</span></span>

<span data-ttu-id="39ba9-423">Configure a propriedade Caminho da pasta de saída com a expressão: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="39ba9-423">Configure the Output Folder Path property with the expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="39ba9-424">e a propriedade Prefixo de nome de arquivo com:</span><span class="sxs-lookup"><span data-stu-id="39ba9-424">and the Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="39ba9-425">O prefixo determinará como os arquivos de miniatura estão sendo chamados.</span><span class="sxs-lookup"><span data-stu-id="39ba9-425">The prefix will determine how the thumbnail files are being named.</span></span> <span data-ttu-id="39ba9-426">Eles receberão um sufixo com um número indicando a posição da miniatura no fluxo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-426">They will be suffixed with a number indicating the thumb's position in the stream.</span></span>

![Propriedades do Gravador de arquivo JPG de Pesquisa de cena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="39ba9-428">*Propriedades do Gravador de arquivo JPG de Pesquisa de cena*</span><span class="sxs-lookup"><span data-stu-id="39ba9-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="39ba9-429">Conecte o Gravador de arquivo JPG de Pesquisa de Cena ao nó Arquivo/Ativo de Saída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-429">Connect the Scene Search JPG File Writer to the Output File/Asset node.</span></span>

### <span data-ttu-id="39ba9-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detectando erros em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="39ba9-431">Conecte a entrada do conversor de espaço de cor à saída de vídeo descompactado bruto.</span><span class="sxs-lookup"><span data-stu-id="39ba9-431">Connect the input of the color space converter to the raw uncompressed video output.</span></span> <span data-ttu-id="39ba9-432">Agora execute um teste local no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-432">Now perform a local test run for the workflow.</span></span> <span data-ttu-id="39ba9-433">Há uma boa chance de a execução do fluxo de trabalho parar de repente e indicar com um contorno vermelho no componente que encontrou um erro:</span><span class="sxs-lookup"><span data-stu-id="39ba9-433">There's a good chance the workflow will suddenly stop executing and indicate with a red outline on the component that encountered an error:</span></span>

![Erro no Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="39ba9-435">*Erro no Conversor de Espaço de Cor*</span><span class="sxs-lookup"><span data-stu-id="39ba9-435">*Color Space Converter error*</span></span>

<span data-ttu-id="39ba9-436">Clique no pequeno ícone "E" vermelho no canto superior direito do componente Conversor de Espaço de Cor para ver o motivo pelo qual a tentativa de codificação falhou.</span><span class="sxs-lookup"><span data-stu-id="39ba9-436">Click the little red "E" icon in the top right corner of the Color Space Converter component to see what's the reason the encoding attempt failed.</span></span>

![Caixa de diálogo do erro no Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="39ba9-438">*Caixa de diálogo do erro no Conversor de Espaço de Cor*</span><span class="sxs-lookup"><span data-stu-id="39ba9-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="39ba9-439">Na verdade, como você pode ver, o padrão do espaço de cor recebido para o conversor de espaço de cor deve ser rec601 para nossa conversão solicitada de YUV para RGB.</span><span class="sxs-lookup"><span data-stu-id="39ba9-439">It turns out, as you can see, that the incoming color space standard for the color space converter has to be rec601 for our requested conversion of YUV to RGB.</span></span> <span data-ttu-id="39ba9-440">Aparentemente, nosso fluxo não indica que é rec601.</span><span class="sxs-lookup"><span data-stu-id="39ba9-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="39ba9-441">(Rec 601 é um padrão de codificação de sinais de vídeo analógicos entrelaçados no formato de vídeo digital.</span><span class="sxs-lookup"><span data-stu-id="39ba9-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="39ba9-442">Ele especifica uma região ativa cobrindo 720 amostras de luminosidade e 360 exemplos de crominância por linha.</span><span class="sxs-lookup"><span data-stu-id="39ba9-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="39ba9-443">O sistema de codificação de cores é conhecido como YCbCr 4:2:2).</span><span class="sxs-lookup"><span data-stu-id="39ba9-443">The color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="39ba9-444">Para corrigir isso, indicaremos nos metadados de nosso fluxo que estamos lidando com conteúdo rec601.</span><span class="sxs-lookup"><span data-stu-id="39ba9-444">To fix this, we'll indicate on the metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="39ba9-445">Para fazer isso, usaremos um componente Atualizador de tipo de dados de vídeo, que colocaremos entre nossa origem bruta e o componente de conversão de espaço de cor.</span><span class="sxs-lookup"><span data-stu-id="39ba9-445">To do so we'll use a Video Data Type Updater component, which we'll put in between our raw source and the color space conversion component.</span></span> <span data-ttu-id="39ba9-446">Esse atualizador de tipo de dados permite a atualização manual de determinadas propriedades de tipo de dados de vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-446">This data type updater allows for the manual update of certain video data type properties.</span></span> <span data-ttu-id="39ba9-447">Configure-o para indicar um Padrão de espaço de cor de "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="39ba9-447">Configure it to indicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="39ba9-448">Isso fará com que o Atualizador de Tipo de Dados do Vídeo marque o fluxo com o espaço de cores "Rec 601", caso ainda não exista um espaço de cores definido.</span><span class="sxs-lookup"><span data-stu-id="39ba9-448">This will cause the Video Data Type Updater to tag the stream with the "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="39ba9-449">(Ele não substituirá os metadados existentes, a menos que a caixa de seleção Substituir tenha sido marcada).</span><span class="sxs-lookup"><span data-stu-id="39ba9-449">(It will not override any existing metadata, unless the Override checkbox was checked.)</span></span>

![Atualizando o padrão de espaço de cores com o Atualizador de tipo de dados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="39ba9-451">*Atualizando o padrão de espaço de cores com o Atualizador de tipo de dados*</span><span class="sxs-lookup"><span data-stu-id="39ba9-451">*Updating Color Space Standard on the Data Type Updater*</span></span>

### <span data-ttu-id="39ba9-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="39ba9-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="39ba9-453">Agora que nosso fluxo de trabalho foi concluído, realize outro teste de execução para vê-lo passar.</span><span class="sxs-lookup"><span data-stu-id="39ba9-453">Now that our our workflow is finished, do another test run to see it pass.</span></span>

![Fluxo de trabalho concluído para várias saídas mp4 com miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="39ba9-455">*Fluxo de trabalho concluído para várias saídas mp4 com miniaturas*</span><span class="sxs-lookup"><span data-stu-id="39ba9-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="39ba9-456"><a id="time_based_trim"></a>Corte baseado em tempo da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="39ba9-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="39ba9-457">Começando em um fluxo de trabalho que gera [uma saída MP4 com várias taxas de bit a partir de uma entrada MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), agora vamos analisar como cortar o vídeo de origem com base em carimbos de data e hora.</span><span class="sxs-lookup"><span data-stu-id="39ba9-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on time-stamps.</span></span>

### <span data-ttu-id="39ba9-458"><a id="time_based_trim_start"></a>Visão geral do fluxo de trabalho para começar a adição do corte</span><span class="sxs-lookup"><span data-stu-id="39ba9-458"><a id="time_based_trim_start"></a>Workflow overview to start adding trimming to</span></span>
![Iniciando o fluxo de trabalho para adição do corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="39ba9-460">*Iniciando o fluxo de trabalho para adição do corte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-460">*Starting workflow to add trimming to*</span></span>

### <span data-ttu-id="39ba9-461"><a id="time_based_trim_use_stream_trimmer"></a>Usando o corte de fluxo</span><span class="sxs-lookup"><span data-stu-id="39ba9-461"><a id="time_based_trim_use_stream_trimmer"></a>Using the Stream Trimmer</span></span>
<span data-ttu-id="39ba9-462">O componente Corte de Fluxo permite cortar o início e o final de um fluxo de entrada com base em informações de tempo (segundos, minutos...). O corte não oferece suporte ao corte baseado em quadros.</span><span class="sxs-lookup"><span data-stu-id="39ba9-462">The Stream Trimmer component allows to trim the beginning and ending of an input stream base on timing information (seconds, minutes, ...). The trimmer does not support frame-based trimming.</span></span>

![Corte de fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="39ba9-464">*Corte de fluxo*</span><span class="sxs-lookup"><span data-stu-id="39ba9-464">*Stream Trimmer*</span></span>

<span data-ttu-id="39ba9-465">Em vez de vincular diretamente os codificadores AVC e o atribuidor de posição de alto-falante à Entrada do Arquivo de Mídia, colocaremos entre eles o corte de fluxo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-465">Instead of linking the AVC encoders and speaker position assigner to the Media File Input directly, we'll put in between those the stream trimmer.</span></span> <span data-ttu-id="39ba9-466">(Um para o sinal de vídeo e outro para o sinal de áudio intercalado).</span><span class="sxs-lookup"><span data-stu-id="39ba9-466">(One for the video signal and one for the interleaved audio signal.)</span></span>

![Como colocar o Corte de fluxo entre eles](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="39ba9-468">*Como colocar o Corte de fluxo entre eles*</span><span class="sxs-lookup"><span data-stu-id="39ba9-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="39ba9-469">Vamos configurar o corte para processarmos apenas o vídeo e o áudio entre 15 e 60 segundos do vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-469">Let's configure the trimmer so that we will only process video and audio between 15 seconds and 60 seconds in the video.</span></span>

<span data-ttu-id="39ba9-470">Acesse as propriedades do Corte de fluxo de vídeo e configure as propriedades de Hora de início (15 s) e Hora de término (60 s).</span><span class="sxs-lookup"><span data-stu-id="39ba9-470">Go to the properties of the Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="39ba9-471">Para termos certeza de que o corte de áudio e de vídeo estará sempre configurado com os mesmos valores de início e de término, os publicaremos na raiz do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-471">To make sure both our audio and video trimmer are always configured to the same start and end values, we will publish those to the root of the workflow.</span></span>

![Publicar a propriedade de hora de início do Corte de Fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="39ba9-473">*Publicar a propriedade de hora de início do Corte de Fluxo*</span><span class="sxs-lookup"><span data-stu-id="39ba9-473">*Publish start time property from Stream Trimmer*</span></span>

![Publicar o diálogo da propriedade para a hora de início](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="39ba9-475">*Publicar o diálogo da propriedade para a hora de início*</span><span class="sxs-lookup"><span data-stu-id="39ba9-475">*Publish property dialog for start time*</span></span>

![Publicar o diálogo da propriedade para a hora de término](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="39ba9-477">*Publicar o diálogo da propriedade para a hora de término*</span><span class="sxs-lookup"><span data-stu-id="39ba9-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="39ba9-478">Se agora inspecionarmos a raiz de nosso fluxo de trabalho, as duas propriedades estarão claramente em exibição e poderão ser configuradas a partir daí.</span><span class="sxs-lookup"><span data-stu-id="39ba9-478">If we now inspect the root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Propriedades publicadas disponíveis na raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="39ba9-480">*Propriedades publicadas disponíveis na raiz*</span><span class="sxs-lookup"><span data-stu-id="39ba9-480">*Published properties available on root*</span></span>

<span data-ttu-id="39ba9-481">Agora, abra as propriedades de corte do corte de áudio e configure os horários de início e de término com uma expressão que faça referência às propriedades publicadas na raiz de nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-481">Now open the trimming properties from the audio trimmer and configure both start and end times with an expression that refers to the published properties on the root of our workflow.</span></span>

<span data-ttu-id="39ba9-482">Para a hora de início do corte de áudio:</span><span class="sxs-lookup"><span data-stu-id="39ba9-482">For the audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="39ba9-483">e para a hora de término:</span><span class="sxs-lookup"><span data-stu-id="39ba9-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="39ba9-484"><a id="time_based_trim_finish"></a>Fluxo de trabalho concluído</span><span class="sxs-lookup"><span data-stu-id="39ba9-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="39ba9-486">*Fluxo de trabalho concluído*</span><span class="sxs-lookup"><span data-stu-id="39ba9-486">*Finished Workflow*</span></span>

## <span data-ttu-id="39ba9-487"><a id="scripting"></a>Introdução ao componente com script</span><span class="sxs-lookup"><span data-stu-id="39ba9-487"><a id="scripting"></a>Introducing the Scripted Component</span></span>
<span data-ttu-id="39ba9-488">Os componentes com script podem executar scripts aleatórios durante as fases de execução de nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-488">Scripted Components can execute arbitrary scripts during the execution phases of our workflow.</span></span> <span data-ttu-id="39ba9-489">Há quatro scripts diferentes que podem ser executados, cada um com características específicas e seus próprios lugares no ciclo de vida do fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="39ba9-489">There are four different scripts that can be executed, each with specific characteristics and their own place in the workflow life-cycle:</span></span>

* <span data-ttu-id="39ba9-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="39ba9-490">**commandScript**</span></span>
* <span data-ttu-id="39ba9-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="39ba9-491">**realizeScript**</span></span>
* <span data-ttu-id="39ba9-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="39ba9-492">**processInputScript**</span></span>
* <span data-ttu-id="39ba9-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="39ba9-493">**lifeCycleScript**</span></span>

<span data-ttu-id="39ba9-494">A documentação do Componente com Script mostra mais detalhes sobre cada um dos scripts acima.</span><span class="sxs-lookup"><span data-stu-id="39ba9-494">The documentation of the Scripted Component goes in more detail for each of the above.</span></span> <span data-ttu-id="39ba9-495">Na [seção a seguir](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), o componente com script **realizeScript** é usado para construir dinamicamente um xml de lista de clipes quando o fluxo de trabalho é iniciado.</span><span class="sxs-lookup"><span data-stu-id="39ba9-495">In [the following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), the **realizeScript** scripting component is used to construct a cliplist xml on the fly when the workflow starts.</span></span> <span data-ttu-id="39ba9-496">Esse script é chamado durante a configuração do componente, que ocorre apenas uma vez em seu ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="39ba9-496">This script is called during the component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="39ba9-497"><a id="scripting_hello_world"></a>Criando scripts em um fluxo de trabalho: hello world</span><span class="sxs-lookup"><span data-stu-id="39ba9-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="39ba9-498">Arraste um Componente com Script para a superfície do designer e renomeie-o (por exemplo, "DefinirXMLDeListaDeClipes").</span><span class="sxs-lookup"><span data-stu-id="39ba9-498">Drag a Scripted Component onto the designer surface and rename it (for example, "SetClipListXML").</span></span>

![Adicionando um Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="39ba9-500">*Adicionando um Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="39ba9-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="39ba9-501">Quando você inspeciona as propriedades do Componente com Script, os quatro tipos diferentes de script são exibidos, cada um configurável para outro script.</span><span class="sxs-lookup"><span data-stu-id="39ba9-501">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![Propriedades do Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="39ba9-503">*Propriedades do Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="39ba9-503">*Scripted Component properties*</span></span>

<span data-ttu-id="39ba9-504">Limpe o processInputScript e abra o editor para o realizeScript.</span><span class="sxs-lookup"><span data-stu-id="39ba9-504">Clear the processInputScript and open the editor for the realizeScript.</span></span> <span data-ttu-id="39ba9-505">Agora, estamos configurados e prontos para começar a criar scripts.</span><span class="sxs-lookup"><span data-stu-id="39ba9-505">Now we're set up and ready to start scripting.</span></span>

<span data-ttu-id="39ba9-506">Os scripts são escritos em Groovy, uma linguagem de script compilada dinamicamente para a plataforma Java que mantém a compatibilidade com Java.</span><span class="sxs-lookup"><span data-stu-id="39ba9-506">Scripts are written in Groovy, a dynamically compiled scripting language for the Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="39ba9-507">Na verdade, grande parte do código Java é um código Groovy válido.</span><span class="sxs-lookup"><span data-stu-id="39ba9-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="39ba9-508">Vamos escrever um script Groovy simples de olá, mundo no contexto de nosso realizeScript.</span><span class="sxs-lookup"><span data-stu-id="39ba9-508">Let's write a simple hello world groovy script in the context of our realizeScript.</span></span> <span data-ttu-id="39ba9-509">Digite o seguinte no editor:</span><span class="sxs-lookup"><span data-stu-id="39ba9-509">Enter the following in the editor:</span></span>

    node.log("hello world");

<span data-ttu-id="39ba9-510">Agora, realize um teste local.</span><span class="sxs-lookup"><span data-stu-id="39ba9-510">Now execute a local test run.</span></span> <span data-ttu-id="39ba9-511">Após essa execução, inspecione a propriedade Logs (por meio da guia Sistema no Componente com Script).</span><span class="sxs-lookup"><span data-stu-id="39ba9-511">After this run, inspect (through the System tab on the Scripted Component) the Logs property.</span></span>

![Saída do log de Hello world](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="39ba9-513">*Saída do log de Hello world*</span><span class="sxs-lookup"><span data-stu-id="39ba9-513">*Hello world log output*</span></span>

<span data-ttu-id="39ba9-514">O objeto do nó no qual chamamos o método faz referência ao nosso "nó" atual, ou ao componente no qual estivermos gerando o script.</span><span class="sxs-lookup"><span data-stu-id="39ba9-514">The node object we call the log method on, refers to our current "node" or the component we're scripting within.</span></span> <span data-ttu-id="39ba9-515">Assim, cada componente tem a capacidade de gerar dados de log, disponíveis na guia Sistema. Nesse caso, mostramos a cadeia de caracteres literal "hello world".</span><span class="sxs-lookup"><span data-stu-id="39ba9-515">Every component as such has the ability to output logging data, available through the system tab. In this case, we output the string literal "hello world".</span></span> <span data-ttu-id="39ba9-516">É importante entender aqui que essa pode ser uma ferramenta de depuração valiosa, fornecendo informações sobre o que o script está realmente fazendo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-516">Important to understand here is that this can prove to be an invaluable debugging tool, providing you with insight on what the script is actually doing.</span></span>

<span data-ttu-id="39ba9-517">De dentro de nosso ambiente de script, também temos acesso às propriedades de outros componentes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-517">From within our scripting environment, we also have access to properties on other components.</span></span> <span data-ttu-id="39ba9-518">Tente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="39ba9-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up to other nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="39ba9-519">Nossa janela de log mostrará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="39ba9-519">Our log window will show us the following:</span></span>

![Saída de log para acessar os caminhos do nó](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="39ba9-521">*Saída de log para acessar os caminhos do nó*</span><span class="sxs-lookup"><span data-stu-id="39ba9-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="39ba9-522"><a id="frame_based_trim"></a>Corte baseado em quadro da saída MP4 com várias taxas de bits</span><span class="sxs-lookup"><span data-stu-id="39ba9-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="39ba9-523">Começando em um fluxo de trabalho que gera [uma saída MP4 com várias taxas de bit a partir de uma entrada MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), agora vamos analisar como cortar o vídeo de origem com base em contagens de quadro.</span><span class="sxs-lookup"><span data-stu-id="39ba9-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on frame counts.</span></span>

### <span data-ttu-id="39ba9-524"><a id="frame_based_trim_start"></a>Visão geral do plano gráfico para começar a adição do corte</span><span class="sxs-lookup"><span data-stu-id="39ba9-524"><a id="frame_based_trim_start"></a>Blueprint overview to start adding trimming to</span></span>
![Fluxo de trabalho para começar a adição do corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="39ba9-526">*Fluxo de trabalho para começar a adição do corte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-526">*Workflow to start adding trimming to*</span></span>

### <span data-ttu-id="39ba9-527"><a id="frame_based_trim_clip_list"></a>Como usar o XML da lista de clipes</span><span class="sxs-lookup"><span data-stu-id="39ba9-527"><a id="frame_based_trim_clip_list"></a>Using the Clip List XML</span></span>
<span data-ttu-id="39ba9-528">Em todos os tutoriais de fluxo de trabalho anteriores, usamos o componente de Entrada do Arquivo de Mídia como nossa fonte de entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-528">In all previous workflow tutorials, we used the Media File Input component as our video input source.</span></span> <span data-ttu-id="39ba9-529">No entanto, para este cenário específico, usaremos o componente de Origem da Lista de Clipes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-529">For this specific scenario though, we'll be using the Clip List Source component instead.</span></span> <span data-ttu-id="39ba9-530">Observe que essa não é a melhor maneira de trabalhar; use a Origem da Lista de Clipes apenas quando houver um motivo para isso (como no caso abaixo, onde estamos usando os recursos de corte de lista de clipes).</span><span class="sxs-lookup"><span data-stu-id="39ba9-530">Note that this should not be the preferred way of working; only use the Clip List Source when there's a real reason to do so (like in the below case, where we're making use of the clip list trimming capabilities).</span></span>

<span data-ttu-id="39ba9-531">Para alternar de nossa Entrada do Arquivo de Mídia para a Origem de lista de clipes, arraste o componente Origem de lista de clipes para a superfície de design e conecte o pino XML da lista de clipes ao nó XML da lista de clipe do designer de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-531">To switch from our Media File Input to the Clip List Source, drag the Clip List Source component onto the design surface and connect the Clip List XML pin to the Clip List XML node of the workflow designer.</span></span> <span data-ttu-id="39ba9-532">Isso deve preencher a Origem da Lista de Clipes com os pinos de saída, de acordo com o nosso vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="39ba9-532">This should populate the Clip List Source with output pins, according to our input video.</span></span> <span data-ttu-id="39ba9-533">Agora conecte os pinos de Vídeo Descompactado e Áudio Descompactados da Origem da Lista de Clipes aos respectivos Codificadores AVC e Intercalador de fluxo de áudio.</span><span class="sxs-lookup"><span data-stu-id="39ba9-533">Now connect the Uncompressed Video and Uncompressed Audio pins from the the Clip List Source to the respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="39ba9-534">Agora remova a Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="39ba9-534">Now remove the Media File Input.</span></span>

![A Entrada do Arquivo de Mídia foi substituída pela Origem da Lista de Clipes](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="39ba9-536">*A Entrada do Arquivo de Mídia foi substituída pela Origem da Lista de Clipes*</span><span class="sxs-lookup"><span data-stu-id="39ba9-536">*Replaced the Media File Input with the Clip List Source*</span></span>

<span data-ttu-id="39ba9-537">O componente Origem da Lista de Clipes recebe como entrada um "XML de lista de clipes".</span><span class="sxs-lookup"><span data-stu-id="39ba9-537">The Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="39ba9-538">Ao selecionar o arquivo de origem para testar localmente, esse xml de lista de clipes é preenchido automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="39ba9-538">When selecting the source file to test with locally, this clip list xml is auto-populated for you.</span></span>

![Propriedade XML de lista de clipes preenchida automaticamente](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="39ba9-540">*Propriedade XML de lista de clipes preenchida automaticamente*</span><span class="sxs-lookup"><span data-stu-id="39ba9-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="39ba9-541">Analisando um pouco mais de perto o xml, ele se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="39ba9-541">Looking a bit closer to the xml, this is how it looks like:</span></span>

![Diálogo Editar lista de clipes](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="39ba9-543">*Diálogo Editar lista de clipes*</span><span class="sxs-lookup"><span data-stu-id="39ba9-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="39ba9-544">No entanto, isso não reflete os recursos do xml da lista de clipes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-544">This however does not reflect the capabilities of the clip list xml.</span></span> <span data-ttu-id="39ba9-545">Uma opção que temos é adicionar um elemento "Corte" à origem do áudio e do vídeo, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="39ba9-545">One option we have is to add a "Trim" element under both the video and audio source, like this:</span></span>

![Adicionando um elemento de corte à lista de clipes](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="39ba9-547">*Adicionando um elemento de corte à lista de clipes*</span><span class="sxs-lookup"><span data-stu-id="39ba9-547">*Adding a trim element to the clip list*</span></span>

<span data-ttu-id="39ba9-548">Se você modificar o xml da lista de clipes da forma indicada acima e executar um teste local, você verá o vídeo corretamente cortado entre 10 e 20 segundos do vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-548">If you modify the clip list xml like this above and perform a local test run, you'll see the video correctly been trimmed between 10 and 20 seconds in the video.</span></span>

<span data-ttu-id="39ba9-549">Ao contrário do que acontece quando você realiza uma execução local, esse mesmo xml de lista de clipes não teria o mesmo efeito quando aplicado em um fluxo de trabalho executado nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="39ba9-549">Contrary to what happens when you do a local run though, this very same cliplist xml would not have the same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="39ba9-550">Quando o Codificador Premium do Azure é iniciado, o xml de lista de clipes é gerado periodicamente com base no arquivo de entrada recebido pelo trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="39ba9-550">When Azure Premium Encoder starts, the cliplist xml is generated every time again, based on the input file the encoding job was given.</span></span> <span data-ttu-id="39ba9-551">Isso significa que qualquer alteração feita no xml seria infelizmente substituída.</span><span class="sxs-lookup"><span data-stu-id="39ba9-551">This means that any changes we do on the xml would unfortunately be overridden.</span></span>

<span data-ttu-id="39ba9-552">Para combater a limpeza do xml de lista de clipes quando um trabalho de codificação é iniciado, podemos gerar isso novamente de forma dinâmica logo após o início de nosso fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="39ba9-552">To counter the cliplist xml being wiped when an encoding job is started, we can re-generate it on the fly just after the start of our workflow.</span></span> <span data-ttu-id="39ba9-553">Essas ações personalizadas podem ser realizadas por meio do que é chamado de "Componente de script".</span><span class="sxs-lookup"><span data-stu-id="39ba9-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="39ba9-554">Para saber mais, confira [Introdução ao Componente com Script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="39ba9-554">For more information, see [Introducing the Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="39ba9-555">Arraste um Componente com Script para a superfície do designer e renomeie-o como "DefinirXMLDeListaDeClipes".</span><span class="sxs-lookup"><span data-stu-id="39ba9-555">Drag a Scripted Component onto the designer surface and rename it to "SetClipListXML".</span></span>

![Adicionando um Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="39ba9-557">*Adicionando um Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="39ba9-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="39ba9-558">Quando você inspeciona as propriedades do Componente com Script, os quatro tipos diferentes de script são exibidos, cada um configurável para outro script.</span><span class="sxs-lookup"><span data-stu-id="39ba9-558">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![Propriedades do Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="39ba9-560">*Propriedades do Componente com Script*</span><span class="sxs-lookup"><span data-stu-id="39ba9-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="39ba9-561"><a id="frame_based_trim_modify_clip_list"></a>Modificando a lista de clipes de um componente com script</span><span class="sxs-lookup"><span data-stu-id="39ba9-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying the clip list from a Scripted Component</span></span>
<span data-ttu-id="39ba9-562">Antes de podermos reescrever o xml de lista de clipes gerado durante a inicialização do fluxo de trabalho, precisaremos de acesso à propriedade e ao conteúdo do xml de lista de clipes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-562">Before we can re-write the cliplist xml that is generated during workflow startup, we'll need to have access to the cliplist xml property and contents.</span></span> <span data-ttu-id="39ba9-563">Podemos fazer isso da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="39ba9-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clipes recebida registrada em log](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="39ba9-565">*Lista de clipes recebida registrada em log*</span><span class="sxs-lookup"><span data-stu-id="39ba9-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="39ba9-566">Primeiro, precisamos de um meio para determinar em quais pontos queremos cortar o vídeo.</span><span class="sxs-lookup"><span data-stu-id="39ba9-566">First we need a way to determine from which point till which point we want to trim the video.</span></span> <span data-ttu-id="39ba9-567">Para tornar isso conveniente para o usuário menos técnico do fluxo de trabalho, publique duas propriedades na raiz do gráfico.</span><span class="sxs-lookup"><span data-stu-id="39ba9-567">To make this convenient to the less-technical user of the workflow, publish two properties to the root of the graph.</span></span> <span data-ttu-id="39ba9-568">Para fazer isso, clique com o botão direito do mouse na superfície do designer e selecione "Adicionar Propriedade":</span><span class="sxs-lookup"><span data-stu-id="39ba9-568">To do this, right click the designer surface and select "Add Property":</span></span>

* <span data-ttu-id="39ba9-569">Primeira propriedade: "ClippingTimeStart" do tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="39ba9-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="39ba9-570">Segunda propriedade: "ClippingTimeEnd" do tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="39ba9-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Adicionar o diálogo Propriedade à hora de início de corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="39ba9-572">*Adicionar o diálogo Propriedade à hora de início de corte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-572">*Add Property dialog for clipping start time*</span></span>

![Propriedades da hora de corte publicadas na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="39ba9-574">*Propriedades da hora de corte publicadas na raiz do fluxo de trabalho*</span><span class="sxs-lookup"><span data-stu-id="39ba9-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="39ba9-575">Configure as duas propriedades com um valor adequado:</span><span class="sxs-lookup"><span data-stu-id="39ba9-575">Configure both properties to a suitable value:</span></span>

![Configurar as propriedades de início de término do corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="39ba9-577">*Configurar as propriedades de início de término do corte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-577">*Configure the clipping start and end properties*</span></span>

<span data-ttu-id="39ba9-578">Agora, em nosso script, podemos acessar as duas propriedades, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="39ba9-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Janela do log mostrando o início e o término do corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="39ba9-580">*Janela do log mostrando o início e o término do corte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="39ba9-581">Vamos analisar as cadeias de código de tempo com uma forma de uso mais conveniente, usando uma expressão regular simples:</span><span class="sxs-lookup"><span data-stu-id="39ba9-581">Let's parse the timecode strings into a more convenient to use form, using a simple regular expression:</span></span>

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Janela do log com a saúda do código de tempo analisado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="39ba9-583">*Janela do log com a saúda do código de tempo analisado*</span><span class="sxs-lookup"><span data-stu-id="39ba9-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="39ba9-584">Com essas informações em mãos, podemos modificar o xml de lista de clipes para refletir as horas de início e de término para o corte preciso de quadro desejado do filme.</span><span class="sxs-lookup"><span data-stu-id="39ba9-584">With this information at hand, we can now modify the cliplist xml to reflect the start and end times for the desired frame-accurate clipping of the movie.</span></span>

![Código de script para adicionar elementos de corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="39ba9-586">*Código de script para adicionar elementos de corte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-586">*Script code to add trim elements*</span></span>

<span data-ttu-id="39ba9-587">Isso foi feito por meio de operações de manipulação de cadeia de caracteres normais.</span><span class="sxs-lookup"><span data-stu-id="39ba9-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="39ba9-588">O xml da lista de clipes modificado resultante é gravado novamente na propriedade clipListXML na raiz do fluxo de trabalho por meio do método "setProperty".</span><span class="sxs-lookup"><span data-stu-id="39ba9-588">The resulting modified clip list xml is written back to the clipListXML property on the workflow root through the "setProperty" method.</span></span> <span data-ttu-id="39ba9-589">A janela de log, após a execução de outro teste, nos mostraria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="39ba9-589">The log window after another test run would show us the following:</span></span>

![Registrando em log a lista de clipes resultante](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="39ba9-591">*Registrando em log a lista de clipes resultante*</span><span class="sxs-lookup"><span data-stu-id="39ba9-591">*Logging the resulting clip list*</span></span>

<span data-ttu-id="39ba9-592">Faça um teste de execução para ver como os fluxos de áudio e de vídeo foram cortados.</span><span class="sxs-lookup"><span data-stu-id="39ba9-592">Do a test-run to see how the video and audio streams have been clipped.</span></span> <span data-ttu-id="39ba9-593">Como você fará mais de um teste de execução com valores diferentes para os pontos de corte, perceberá que eles não serão levados em consideração!</span><span class="sxs-lookup"><span data-stu-id="39ba9-593">As you'll do more than one test-run with different values for the trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="39ba9-594">O motivo para isso é que o designer, ao contrário do tempo de execução do Azure, NÃO substitui o xml de lista de clipes em cada execução.</span><span class="sxs-lookup"><span data-stu-id="39ba9-594">The reason for this is that the designer, unlike the Azure runtime, does NOT override the cliplist xml every run.</span></span> <span data-ttu-id="39ba9-595">Isso significa que apenas a primeira vez em que você definir os pontos de entrada e saída causará uma transformação do xml. Em todas as outras vezes, nossa cláusula de proteção (if(clipListXML.indexOf("<trim>") == -1)) impedirá que o fluxo de trabalho adicione outro elemento de corte quando já houver um presente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-595">This means that only the very first time you have set the in and out points, will cause the xml to transform, all the other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent the workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="39ba9-596">Para tornar o teste local do fluxo de trabalho mais conveniente, é melhor adicionarmos algum código de manutenção que verifica se um elemento de corte já está presente.</span><span class="sxs-lookup"><span data-stu-id="39ba9-596">To make our workflow convenient to test locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="39ba9-597">Em caso positivo, podemos removê-lo antes de continuar por meio da modificação do xml com os novos valores.</span><span class="sxs-lookup"><span data-stu-id="39ba9-597">If so, we can remove it before continuing by modifying the xml with the new values.</span></span> <span data-ttu-id="39ba9-598">Em vez de usar manipulações de cadeia de caracteres simples, provavelmente será mais seguro fazer isso por meio da análise do modelo de objeto xml real.</span><span class="sxs-lookup"><span data-stu-id="39ba9-598">Rather than using plain string manipulations, it's probably safer to do this through real xml object model parsing.</span></span>

<span data-ttu-id="39ba9-599">Antes de podermos adicionar esse código, precisamos adicionar algumas instruções de importação ao início do nosso script:</span><span class="sxs-lookup"><span data-stu-id="39ba9-599">Before we can add such code though, we'll need to add a number of import statements at the start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="39ba9-600">Depois disso, podemos adicionar o código de limpeza necessário:</span><span class="sxs-lookup"><span data-stu-id="39ba9-600">After this, we can add the required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from the clip list xml by parsing the xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
     //delete the trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="39ba9-601">Esse código fica logo acima do ponto no qual podemos adicionar os elementos de corte ao xml da lista de clipes.</span><span class="sxs-lookup"><span data-stu-id="39ba9-601">This code goes just above the point at which we add the trim elements to the cliplist xml.</span></span>

<span data-ttu-id="39ba9-602">Neste ponto, podemos executar e modificar nosso fluxo de trabalho o quanto quisermos enquanto as alterações são aplicadas sempre.</span><span class="sxs-lookup"><span data-stu-id="39ba9-602">At this point, we can run and modify our workflow as much as we want while having the changes applied ever time.</span></span>    

### <span data-ttu-id="39ba9-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adicionando uma propriedade de conveniência ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="39ba9-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="39ba9-604">Como você não quer que o corte ocorra sempre, vamos finalizar nosso fluxo de trabalho adicionando um sinalizador booliano conveniente que indica se queremos ou não permitir o corte/recorte.</span><span class="sxs-lookup"><span data-stu-id="39ba9-604">As you might not always want trimming to happen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want to enable trimming / clipping.</span></span>

<span data-ttu-id="39ba9-605">Assim como antes, publique uma nova propriedade na raiz de nosso fluxo de trabalho chamada "ClippingEnabled" do tipo "BOOLEAN".</span><span class="sxs-lookup"><span data-stu-id="39ba9-605">Just as before, publish a new property to the root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Propriedade publicada para habilitar o recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="39ba9-607">*Propriedade publicada para habilitar o recorte*</span><span class="sxs-lookup"><span data-stu-id="39ba9-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="39ba9-608">Com a cláusula de proteção simples abaixo, podemos verificar se o corte é necessário e decidir se nossa lista de clipes precisa ser modificada ou não.</span><span class="sxs-lookup"><span data-stu-id="39ba9-608">With the below simple guard clause, we can check if trimming is required and decide if our clip list as such needs to be modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="39ba9-609"><a id="code"></a>Código completo</span><span class="sxs-lookup"><span data-stu-id="39ba9-609"><a id="code"></a>Complete code</span></span>
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

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from the clip list xml by parsing the xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
    //delete the trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
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

    //add trim elements to cliplist xml
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


## <a name="also-see"></a><span data-ttu-id="39ba9-610">Consulte também</span><span class="sxs-lookup"><span data-stu-id="39ba9-610">Also see</span></span>
[<span data-ttu-id="39ba9-611">Apresentando a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="39ba9-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="39ba9-612">Como usar a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="39ba9-612">How to Use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="39ba9-613">Codificando conteúdo sob demanda com os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="39ba9-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="39ba9-614">Codecs e formatos de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="39ba9-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="39ba9-615">Exemplos de arquivos de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="39ba9-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="39ba9-616">Ferramenta do Explorador dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="39ba9-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="39ba9-617">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="39ba9-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="39ba9-618">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="39ba9-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
