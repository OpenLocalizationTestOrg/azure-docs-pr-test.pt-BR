---
title: "Edição facial com o Azure Media Analytics | Microsoft Docs"
description: "Este tópico demonstra como editar rostos com o Azure Media Analytics."
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
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="a075c-103">Edição facial com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="a075c-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="a075c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a075c-104">Overview</span></span>
<span data-ttu-id="a075c-105">**Azure Media Redactor** é um MP (processador de mídia) do [Azure Media Analytics](media-services-analytics-overview.md) que oferece edição facial escalonável na nuvem.</span><span class="sxs-lookup"><span data-stu-id="a075c-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="a075c-106">A edição facial permite que você modifique seu vídeo para desfocar rostos de pessoas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="a075c-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="a075c-107">Você pode querer usar o serviço de edição facial em cenários de segurança pública e de notícias veiculadas.</span><span class="sxs-lookup"><span data-stu-id="a075c-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="a075c-108">Alguns minutos de vídeo com vários rostos podem levar horas para serem editados manualmente, mas, com esse serviço, o processo de edição facial exigirá apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="a075c-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="a075c-109">Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-redactor/)blog.</span><span class="sxs-lookup"><span data-stu-id="a075c-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="a075c-110">Este tópico fornece detalhes sobre o **Azure Media Redactor** e mostra como usá-lo com o SDK dos Serviços de Mídia para .NET.</span><span class="sxs-lookup"><span data-stu-id="a075c-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="a075c-111">No momento, o MP do **Azure Media Redactor** está em versão de Visualização.</span><span class="sxs-lookup"><span data-stu-id="a075c-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="a075c-112">Ele está disponível em todas as regiões públicas do Azure, bem como em data centers do Governo dos EUA e da China.</span><span class="sxs-lookup"><span data-stu-id="a075c-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="a075c-113">Esta visualização está disponível gratuitamente no momento.</span><span class="sxs-lookup"><span data-stu-id="a075c-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="a075c-114">Modos de edição facial</span><span class="sxs-lookup"><span data-stu-id="a075c-114">Face redaction modes</span></span>
<span data-ttu-id="a075c-115">A edição facial trabalha detectando rostos em cada quadro de vídeo e controlando o objeto de rosto para frente e para trás no tempo, para que a mesma pessoa possa ser desfocada também de outros ângulos.</span><span class="sxs-lookup"><span data-stu-id="a075c-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="a075c-116">O processo de edição automatizada é muito complexo e nem sempre produz 100% do resultado desejado. Portanto, o Media Analytics oferece duas maneiras de modificar o resultado final.</span><span class="sxs-lookup"><span data-stu-id="a075c-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="a075c-117">Além de um modo totalmente automatizado, há um fluxo de trabalho de duas etapas que permite a seleção de rostos e a desmarcação de rostos selecionados usando uma lista de IDs.</span><span class="sxs-lookup"><span data-stu-id="a075c-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="a075c-118">Além disso, para fazer ajustes avulsos por quadro, o MP usa um arquivo de metadados no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a075c-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="a075c-119">Esse fluxo de trabalho é dividido nos modos **Analisar** e **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a075c-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="a075c-120">Você pode combinar os dois modos em uma única passagem que executa ambas as tarefas em um mesmo trabalho. Esse modo é chamado **Combinado**.</span><span class="sxs-lookup"><span data-stu-id="a075c-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="a075c-121">Modo Combinado</span><span class="sxs-lookup"><span data-stu-id="a075c-121">Combined mode</span></span>
<span data-ttu-id="a075c-122">Esse procedimento produzirá um mp4 editado automaticamente sem qualquer entrada manual.</span><span class="sxs-lookup"><span data-stu-id="a075c-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="a075c-123">Estágio</span><span class="sxs-lookup"><span data-stu-id="a075c-123">Stage</span></span> | <span data-ttu-id="a075c-124">Nome do Arquivo</span><span class="sxs-lookup"><span data-stu-id="a075c-124">File Name</span></span> | <span data-ttu-id="a075c-125">Observações</span><span class="sxs-lookup"><span data-stu-id="a075c-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a075c-126">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-126">Input asset</span></span> |<span data-ttu-id="a075c-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="a075c-127">foo.bar</span></span> |<span data-ttu-id="a075c-128">Vídeo em formato WMV, MOV ou MP4</span><span class="sxs-lookup"><span data-stu-id="a075c-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="a075c-129">Configuração de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-129">Input config</span></span> |<span data-ttu-id="a075c-130">Predefinição de configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="a075c-130">Job configuration preset</span></span> |<span data-ttu-id="a075c-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="a075c-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="a075c-132">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="a075c-132">Output asset</span></span> |<span data-ttu-id="a075c-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="a075c-133">foo_redacted.mp4</span></span> |<span data-ttu-id="a075c-134">Vídeo com desfoque aplicado</span><span class="sxs-lookup"><span data-stu-id="a075c-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="a075c-135">Exemplo de entrada:</span><span class="sxs-lookup"><span data-stu-id="a075c-135">Input example:</span></span>
[<span data-ttu-id="a075c-136">veja este vídeo</span><span class="sxs-lookup"><span data-stu-id="a075c-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="a075c-137">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="a075c-137">Output example:</span></span>
[<span data-ttu-id="a075c-138">veja este vídeo</span><span class="sxs-lookup"><span data-stu-id="a075c-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="a075c-139">Modo Analisar</span><span class="sxs-lookup"><span data-stu-id="a075c-139">Analyze mode</span></span>
<span data-ttu-id="a075c-140">A etapa **Analisar** do fluxo de trabalho de duas etapas utiliza uma entrada de vídeo e produz um arquivo JSON com a localização dos rostos, e imagens jpg de cada rosto detectado.</span><span class="sxs-lookup"><span data-stu-id="a075c-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="a075c-141">Estágio</span><span class="sxs-lookup"><span data-stu-id="a075c-141">Stage</span></span> | <span data-ttu-id="a075c-142">Nome do Arquivo</span><span class="sxs-lookup"><span data-stu-id="a075c-142">File Name</span></span> | <span data-ttu-id="a075c-143">Observações</span><span class="sxs-lookup"><span data-stu-id="a075c-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a075c-144">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-144">Input asset</span></span> |<span data-ttu-id="a075c-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="a075c-145">foo.bar</span></span> |<span data-ttu-id="a075c-146">Vídeo em formato WMV, MPV ou MP4</span><span class="sxs-lookup"><span data-stu-id="a075c-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="a075c-147">Configuração de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-147">Input config</span></span> |<span data-ttu-id="a075c-148">Predefinição de configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="a075c-148">Job configuration preset</span></span> |<span data-ttu-id="a075c-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="a075c-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="a075c-150">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="a075c-150">Output asset</span></span> |<span data-ttu-id="a075c-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="a075c-151">foo_annotations.json</span></span> |<span data-ttu-id="a075c-152">Dados de anotação da localização dos rostos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a075c-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="a075c-153">Isso pode ser editado pelo usuário para modificar as caixas delimitadoras de desfoque.</span><span class="sxs-lookup"><span data-stu-id="a075c-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="a075c-154">Confira o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="a075c-154">See sample below.</span></span> |
| <span data-ttu-id="a075c-155">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="a075c-155">Output asset</span></span> |<span data-ttu-id="a075c-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="a075c-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="a075c-157">Um jpg cortado de cada rosto detectado, em que o número indica o labelId do rosto</span><span class="sxs-lookup"><span data-stu-id="a075c-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="a075c-158">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="a075c-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="a075c-159">Modo de edição</span><span class="sxs-lookup"><span data-stu-id="a075c-159">Redact mode</span></span>
<span data-ttu-id="a075c-160">A segunda etapa do fluxo de trabalho tem um grande número de entradas que precisam ser combinadas em um único ativo.</span><span class="sxs-lookup"><span data-stu-id="a075c-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="a075c-161">Isso inclui uma lista de IDs a serem desfocados, o vídeo original e o JSON de anotações.</span><span class="sxs-lookup"><span data-stu-id="a075c-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="a075c-162">Esse modo usa as anotações para aplicar desfoque ao vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="a075c-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="a075c-163">O resultado da etapa Analisar não inclui o vídeo original.</span><span class="sxs-lookup"><span data-stu-id="a075c-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="a075c-164">O vídeo precisa ser carregado no ativo de entrada para a tarefa do modo Editar e selecionado como o arquivo primário.</span><span class="sxs-lookup"><span data-stu-id="a075c-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="a075c-165">Estágio</span><span class="sxs-lookup"><span data-stu-id="a075c-165">Stage</span></span> | <span data-ttu-id="a075c-166">Nome do Arquivo</span><span class="sxs-lookup"><span data-stu-id="a075c-166">File Name</span></span> | <span data-ttu-id="a075c-167">Observações</span><span class="sxs-lookup"><span data-stu-id="a075c-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a075c-168">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-168">Input asset</span></span> |<span data-ttu-id="a075c-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="a075c-169">foo.bar</span></span> |<span data-ttu-id="a075c-170">Vídeo em formato WMV, MPV ou MP4.</span><span class="sxs-lookup"><span data-stu-id="a075c-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="a075c-171">O mesmo vídeo da etapa 1.</span><span class="sxs-lookup"><span data-stu-id="a075c-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="a075c-172">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-172">Input asset</span></span> |<span data-ttu-id="a075c-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="a075c-173">foo_annotations.json</span></span> |<span data-ttu-id="a075c-174">arquivo de metadados de anotações da fase 1, com modificações opcionais.</span><span class="sxs-lookup"><span data-stu-id="a075c-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="a075c-175">Ativo de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-175">Input asset</span></span> |<span data-ttu-id="a075c-176">foo_IDList.txt (opcional)</span><span class="sxs-lookup"><span data-stu-id="a075c-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="a075c-177">Nova lista opcional separada por linhas de IDs de rostos para editar.</span><span class="sxs-lookup"><span data-stu-id="a075c-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="a075c-178">Se deixado em branco, todas as faces são desfocadas.</span><span class="sxs-lookup"><span data-stu-id="a075c-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="a075c-179">Configuração de entrada</span><span class="sxs-lookup"><span data-stu-id="a075c-179">Input config</span></span> |<span data-ttu-id="a075c-180">Predefinição de configuração de tarefa</span><span class="sxs-lookup"><span data-stu-id="a075c-180">Job configuration preset</span></span> |<span data-ttu-id="a075c-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="a075c-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="a075c-182">Ativo de saída</span><span class="sxs-lookup"><span data-stu-id="a075c-182">Output asset</span></span> |<span data-ttu-id="a075c-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="a075c-183">foo_redacted.mp4</span></span> |<span data-ttu-id="a075c-184">Vídeo com desfoque aplicado com base nas anotações</span><span class="sxs-lookup"><span data-stu-id="a075c-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="a075c-185">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="a075c-185">Example output</span></span>
<span data-ttu-id="a075c-186">É a saída de uma IDList com uma ID selecionada.</span><span class="sxs-lookup"><span data-stu-id="a075c-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="a075c-187">veja este vídeo</span><span class="sxs-lookup"><span data-stu-id="a075c-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="a075c-188">foo_IDList.txt de exemplo</span><span class="sxs-lookup"><span data-stu-id="a075c-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="a075c-189">Tipos de desfoque</span><span class="sxs-lookup"><span data-stu-id="a075c-189">Blur types</span></span>

<span data-ttu-id="a075c-190">No modo **Combinado** ou **Redação**, há cinco modos de desfoque diferentes à sua escolha por meio da configuração de entrada JSON: **Baixo**, **Med**, **Alto**, **Depurar** e **Preto**.</span><span class="sxs-lookup"><span data-stu-id="a075c-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="a075c-191">Por padrão, **Med** é usado.</span><span class="sxs-lookup"><span data-stu-id="a075c-191">By default **Med** is used.</span></span>

<span data-ttu-id="a075c-192">Encontre exemplos dos tipos de desfoque abaixo.</span><span class="sxs-lookup"><span data-stu-id="a075c-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="a075c-193">Exemplo de JSON:</span><span class="sxs-lookup"><span data-stu-id="a075c-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="a075c-194">Baixo</span><span class="sxs-lookup"><span data-stu-id="a075c-194">Low</span></span>

![Baixo](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="a075c-196">Med</span><span class="sxs-lookup"><span data-stu-id="a075c-196">Med</span></span>

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="a075c-198">Alto</span><span class="sxs-lookup"><span data-stu-id="a075c-198">High</span></span>

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="a075c-200">Depurar</span><span class="sxs-lookup"><span data-stu-id="a075c-200">Debug</span></span>

![Depurar](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="a075c-202">Preto</span><span class="sxs-lookup"><span data-stu-id="a075c-202">Black</span></span>

![Preto](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="a075c-204">Elementos do arquivo JSON de saída</span><span class="sxs-lookup"><span data-stu-id="a075c-204">Elements of the output JSON file</span></span>

<span data-ttu-id="a075c-205">O MP de edição fornece detecção facial e acompanhamento de alta precisão local de até 64 rostos humanos em um quadro de vídeo.</span><span class="sxs-lookup"><span data-stu-id="a075c-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="a075c-206">Faces frontais fornecem os melhores resultados, enquanto as faces laterais e faces pequenas (menores ou iguais a 24x24 pixels) têm resultados menos precisos.</span><span class="sxs-lookup"><span data-stu-id="a075c-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="a075c-207">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="a075c-207">.NET sample code</span></span>

<span data-ttu-id="a075c-208">O programa a seguir mostra como:</span><span class="sxs-lookup"><span data-stu-id="a075c-208">The following program shows how to:</span></span>

1. <span data-ttu-id="a075c-209">Criar um ativo e carregar um arquivo de mídia nesse ativo.</span><span class="sxs-lookup"><span data-stu-id="a075c-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="a075c-210">Criar um trabalho com uma tarefa de edição facial baseada em um arquivo de configuração que contém a predefinição de JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="a075c-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="a075c-211">Baixe os arquivos JSON de saída.</span><span class="sxs-lookup"><span data-stu-id="a075c-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a075c-212">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a075c-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a075c-213">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a075c-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="a075c-214">Exemplo</span><span class="sxs-lookup"><span data-stu-id="a075c-214">Example</span></span>

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

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="a075c-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a075c-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a075c-216">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a075c-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="a075c-217">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="a075c-217">Related links</span></span>
[<span data-ttu-id="a075c-218">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="a075c-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="a075c-219">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="a075c-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

