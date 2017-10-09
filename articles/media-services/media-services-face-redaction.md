---
title: "as faces aaaRedact com análise de mídia do Azure | Microsoft Docs"
description: "Este tópico demonstra como tooredact faces com análise de mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="95543-103">Edição facial com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="95543-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="95543-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="95543-104">Overview</span></span>
<span data-ttu-id="95543-105">**Redactor de mídia do Azure** é um [análise de mídia do Azure](media-services-analytics-overview.md) processador de mídia (MP) que oferece redação face escalonável na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="95543-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="95543-106">Redação da face permite que você toomodify o vídeo em faces de tooblur de ordem de pessoas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="95543-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="95543-107">Talvez você queira serviço de redação de face toouse Olá em cenários de segurança e mídia públicos.</span><span class="sxs-lookup"><span data-stu-id="95543-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="95543-108">Alguns minutos do que contém várias faces podem levar horas tooredact manualmente, mas com esta face de saudação do serviço redação processo requer apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="95543-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="95543-109">Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-redactor/)blog.</span><span class="sxs-lookup"><span data-stu-id="95543-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="95543-110">Este tópico fornece detalhes sobre **Redactor de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="95543-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="95543-111">Olá **Redactor de mídia do Azure** MP está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="95543-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="95543-112">Ele está disponível em todas as regiões públicas do Azure, bem como em data centers do Governo dos EUA e da China.</span><span class="sxs-lookup"><span data-stu-id="95543-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="95543-113">Esta visualização está disponível gratuitamente no momento.</span><span class="sxs-lookup"><span data-stu-id="95543-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="95543-114">Modos de edição facial</span><span class="sxs-lookup"><span data-stu-id="95543-114">Face redaction modes</span></span>
<span data-ttu-id="95543-115">Redação facial funciona Detectando as faces em cada quadro de vídeo e controle face Olá objeto ambos frente e para trás no tempo, para que hello mesma pessoa pode ser indefinida de outros ângulos também.</span><span class="sxs-lookup"><span data-stu-id="95543-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="95543-116">Olá processo automatizado de redação é muito complexo e não produzir sempre 100% de saída desejada, por esse motivo, que análise de mídia oferece duas maneiras saída final de saudação toomodify.</span><span class="sxs-lookup"><span data-stu-id="95543-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="95543-117">No modo totalmente automático de tooa de adição, há um fluxo de trabalho de dois passos que permite Olá seleção de/de-selection de faces encontradas por meio de uma lista de IDs.</span><span class="sxs-lookup"><span data-stu-id="95543-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="95543-118">Além disso, toomake arbitrário por saudação ajustes de quadro MP usa um arquivo de metadados no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="95543-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="95543-119">Esse fluxo de trabalho é dividido nos modos **Analisar** e **Editar**.</span><span class="sxs-lookup"><span data-stu-id="95543-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="95543-120">Você pode combinar dois modos de saudação em uma única passagem que executa ambas as tarefas em um trabalho; Esse modo é chamado **combinada**.</span><span class="sxs-lookup"><span data-stu-id="95543-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="95543-121">Modo Combinado</span><span class="sxs-lookup"><span data-stu-id="95543-121">Combined mode</span></span>
<span data-ttu-id="95543-122">Esse procedimento produzirá um mp4 editado automaticamente sem qualquer entrada manual.</span><span class="sxs-lookup"><span data-stu-id="95543-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="95543-123">Estágio</span><span class="sxs-lookup"><span data-stu-id="95543-123">Stage</span></span> | <span data-ttu-id="95543-124">Nome do Arquivo</span><span class="sxs-lookup"><span data-stu-id="95543-124">File Name</span></span> | <span data-ttu-id="95543-125">Observações</span><span class="sxs-lookup"><span data-stu-id="95543-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95543-126">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-126">Input asset</span></span> |<span data-ttu-id="95543-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="95543-127">foo.bar</span></span> |<span data-ttu-id="95543-128">Vídeo em formato WMV, MOV ou MP4</span><span class="sxs-lookup"><span data-stu-id="95543-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="95543-129">Configuração de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-129">Input config</span></span> |<span data-ttu-id="95543-130">Predefinição de configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="95543-130">Job configuration preset</span></span> |<span data-ttu-id="95543-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="95543-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="95543-132">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="95543-132">Output asset</span></span> |<span data-ttu-id="95543-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="95543-133">foo_redacted.mp4</span></span> |<span data-ttu-id="95543-134">Vídeo com desfoque aplicado</span><span class="sxs-lookup"><span data-stu-id="95543-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="95543-135">Exemplo de entrada:</span><span class="sxs-lookup"><span data-stu-id="95543-135">Input example:</span></span>
[<span data-ttu-id="95543-136">veja este vídeo</span><span class="sxs-lookup"><span data-stu-id="95543-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="95543-137">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="95543-137">Output example:</span></span>
[<span data-ttu-id="95543-138">veja este vídeo</span><span class="sxs-lookup"><span data-stu-id="95543-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="95543-139">Modo Analisar</span><span class="sxs-lookup"><span data-stu-id="95543-139">Analyze mode</span></span>
<span data-ttu-id="95543-140">Olá **analisar** passagem de fluxo de trabalho de dois passos Olá utiliza uma entrada de vídeo e produz um arquivo JSON de locais de face e jpg imagens de cada detectado face.</span><span class="sxs-lookup"><span data-stu-id="95543-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="95543-141">Estágio</span><span class="sxs-lookup"><span data-stu-id="95543-141">Stage</span></span> | <span data-ttu-id="95543-142">Nome do Arquivo</span><span class="sxs-lookup"><span data-stu-id="95543-142">File Name</span></span> | <span data-ttu-id="95543-143">Observações</span><span class="sxs-lookup"><span data-stu-id="95543-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95543-144">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-144">Input asset</span></span> |<span data-ttu-id="95543-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="95543-145">foo.bar</span></span> |<span data-ttu-id="95543-146">Vídeo em formato WMV, MPV ou MP4</span><span class="sxs-lookup"><span data-stu-id="95543-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="95543-147">Configuração de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-147">Input config</span></span> |<span data-ttu-id="95543-148">Predefinição de configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="95543-148">Job configuration preset</span></span> |<span data-ttu-id="95543-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="95543-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="95543-150">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="95543-150">Output asset</span></span> |<span data-ttu-id="95543-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="95543-151">foo_annotations.json</span></span> |<span data-ttu-id="95543-152">Dados de anotação da localização dos rostos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="95543-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="95543-153">Isso pode ser editado por obscurecendo no saudação do toomodify de usuário Olá caixas delimitadoras.</span><span class="sxs-lookup"><span data-stu-id="95543-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="95543-154">Confira o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="95543-154">See sample below.</span></span> |
| <span data-ttu-id="95543-155">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="95543-155">Output asset</span></span> |<span data-ttu-id="95543-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="95543-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="95543-157">Jpg cortada de cada detectado face, onde o número de saudação indica labelId Olá da face Olá</span><span class="sxs-lookup"><span data-stu-id="95543-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="95543-158">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="95543-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="95543-159">Modo de edição</span><span class="sxs-lookup"><span data-stu-id="95543-159">Redact mode</span></span>
<span data-ttu-id="95543-160">segundo de aprovação de fluxo de trabalho Olá Olá entra em um grande número de entradas que devem ser combinados em um único ativo.</span><span class="sxs-lookup"><span data-stu-id="95543-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="95543-161">Isso inclui uma lista de IDs tooblur vídeo original hello e anotações Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="95543-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="95543-162">Esse modo usa Olá anotações tooapply obscurecendo no vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="95543-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="95543-163">Hello saída da passagem de analisar Olá não incluir vídeo original hello.</span><span class="sxs-lookup"><span data-stu-id="95543-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="95543-164">Olá vídeo precisa toobe carregado no ativo de entrada hello para tarefas de modo Redact hello e marcada como arquivo principal hello.</span><span class="sxs-lookup"><span data-stu-id="95543-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="95543-165">Estágio</span><span class="sxs-lookup"><span data-stu-id="95543-165">Stage</span></span> | <span data-ttu-id="95543-166">Nome do Arquivo</span><span class="sxs-lookup"><span data-stu-id="95543-166">File Name</span></span> | <span data-ttu-id="95543-167">Observações</span><span class="sxs-lookup"><span data-stu-id="95543-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="95543-168">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-168">Input asset</span></span> |<span data-ttu-id="95543-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="95543-169">foo.bar</span></span> |<span data-ttu-id="95543-170">Vídeo em formato WMV, MPV ou MP4.</span><span class="sxs-lookup"><span data-stu-id="95543-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="95543-171">O mesmo vídeo da etapa 1.</span><span class="sxs-lookup"><span data-stu-id="95543-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="95543-172">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-172">Input asset</span></span> |<span data-ttu-id="95543-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="95543-173">foo_annotations.json</span></span> |<span data-ttu-id="95543-174">arquivo de metadados de anotações da fase 1, com modificações opcionais.</span><span class="sxs-lookup"><span data-stu-id="95543-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="95543-175">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-175">Input asset</span></span> |<span data-ttu-id="95543-176">foo_IDList.txt (opcional)</span><span class="sxs-lookup"><span data-stu-id="95543-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="95543-177">Nova linha opcional lista separada de face tooredact IDs.</span><span class="sxs-lookup"><span data-stu-id="95543-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="95543-178">Se deixado em branco, todas as faces são desfocadas.</span><span class="sxs-lookup"><span data-stu-id="95543-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="95543-179">Configuração de entrada</span><span class="sxs-lookup"><span data-stu-id="95543-179">Input config</span></span> |<span data-ttu-id="95543-180">Predefinição de configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="95543-180">Job configuration preset</span></span> |<span data-ttu-id="95543-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="95543-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="95543-182">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="95543-182">Output asset</span></span> |<span data-ttu-id="95543-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="95543-183">foo_redacted.mp4</span></span> |<span data-ttu-id="95543-184">Vídeo com desfoque aplicado com base nas anotações</span><span class="sxs-lookup"><span data-stu-id="95543-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="95543-185">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="95543-185">Example output</span></span>
<span data-ttu-id="95543-186">Esta é a saída de saudação de um IDList com uma ID de selecionada.</span><span class="sxs-lookup"><span data-stu-id="95543-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="95543-187">veja este vídeo</span><span class="sxs-lookup"><span data-stu-id="95543-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="95543-188">foo_IDList.txt de exemplo</span><span class="sxs-lookup"><span data-stu-id="95543-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="95543-189">Tipos de desfoque</span><span class="sxs-lookup"><span data-stu-id="95543-189">Blur types</span></span>

<span data-ttu-id="95543-190">Em Olá **combinada** ou **Redact** modo, há 5 modos de desfoque diferentes, você pode escolher por meio da configuração de entrada hello JSON: **baixo**, **Med**, **Alta**, **depurar**, e **preto**.</span><span class="sxs-lookup"><span data-stu-id="95543-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="95543-191">Por padrão, **Med** é usado.</span><span class="sxs-lookup"><span data-stu-id="95543-191">By default **Med** is used.</span></span>

<span data-ttu-id="95543-192">Você pode encontrar exemplos de saudação desfoque tipos abaixo.</span><span class="sxs-lookup"><span data-stu-id="95543-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="95543-193">Exemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="95543-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="95543-194">Baixo</span><span class="sxs-lookup"><span data-stu-id="95543-194">Low</span></span>

![Baixo](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="95543-196">Med</span><span class="sxs-lookup"><span data-stu-id="95543-196">Med</span></span>

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="95543-198">Alto</span><span class="sxs-lookup"><span data-stu-id="95543-198">High</span></span>

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="95543-200">Depurar</span><span class="sxs-lookup"><span data-stu-id="95543-200">Debug</span></span>

![Depurar](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="95543-202">Preto</span><span class="sxs-lookup"><span data-stu-id="95543-202">Black</span></span>

![Preto](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="95543-204">Elementos Olá JSON do arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="95543-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="95543-205">Olá MP de redação fornece controle que pode detectar o too64 as faces humana em um quadro de vídeo e detecção de local de face de alta precisão.</span><span class="sxs-lookup"><span data-stu-id="95543-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="95543-206">Faces frontais fornecem Olá obter melhores resultados, enquanto as faces lado e faces pequenas (menor que ou igual a too24x24 pixels) são um desafio.</span><span class="sxs-lookup"><span data-stu-id="95543-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="95543-207">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="95543-207">.NET sample code</span></span>

<span data-ttu-id="95543-208">a seguir Olá programa mostra como:</span><span class="sxs-lookup"><span data-stu-id="95543-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="95543-209">Criar um ativo e carregar um arquivo de mídia no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95543-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="95543-210">Crie um trabalho com uma tarefa de redação de face com base em um arquivo de configuração que contém Olá predefinição json a seguir.</span><span class="sxs-lookup"><span data-stu-id="95543-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="95543-211">Baixe os arquivos de saída do JSON hello.</span><span class="sxs-lookup"><span data-stu-id="95543-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="95543-212">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95543-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="95543-213">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="95543-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="95543-214">Exemplo</span><span class="sxs-lookup"><span data-stu-id="95543-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="95543-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95543-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="95543-216">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="95543-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="95543-217">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="95543-217">Related links</span></span>
[<span data-ttu-id="95543-218">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="95543-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="95543-219">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="95543-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

