---
title: "aaaDetect Face e emoção com análise de mídia do Azure | Microsoft Docs"
description: "Este tópico demonstra como toodetect faces e emoções com análise de mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="922a9-103">Detectar a face e a emoção com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="922a9-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="922a9-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="922a9-104">Overview</span></span>
<span data-ttu-id="922a9-105">Olá **Detector de Face de mídia do Azure** processador de mídia (MP) permite que você toocount, acompanhar movimentos e até mesmo a participação do medidor público e reação via expressões faciais.</span><span class="sxs-lookup"><span data-stu-id="922a9-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="922a9-106">Este serviço contém dois recursos:</span><span class="sxs-lookup"><span data-stu-id="922a9-106">This service contains two features:</span></span> 

* <span data-ttu-id="922a9-107">**Detecção facial**</span><span class="sxs-lookup"><span data-stu-id="922a9-107">**Face detection**</span></span>
  
    <span data-ttu-id="922a9-108">A detecção facial localiza e acompanha as faces humanas em um vídeo.</span><span class="sxs-lookup"><span data-stu-id="922a9-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="922a9-109">Várias faces podem ser detectadas e posteriormente ser controladas à medida que se movimentam, com metadados de hora e o local de saudação retornados em um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="922a9-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="922a9-110">Durante o rastreamento, ele tentará toogive um toohello ID consistente mesmo enfrentam enquanto pessoa Olá é mover-se na tela, mesmo se eles são obstruídos ou deixam brevemente quadro hello.</span><span class="sxs-lookup"><span data-stu-id="922a9-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="922a9-111">Esse serviço não realiza reconhecimento facial.</span><span class="sxs-lookup"><span data-stu-id="922a9-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="922a9-112">Uma pessoa que sai do quadro de saudação ou se torna obstruída para muito tempo será fornecida uma nova ID quando elas retornam.</span><span class="sxs-lookup"><span data-stu-id="922a9-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="922a9-113">**Detecção de emoções**</span><span class="sxs-lookup"><span data-stu-id="922a9-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="922a9-114">Detecção de emoção é um componente opcional do hello processador de mídia de detecção de rosto que retorna análise em vários atributos emocionais de faces Olá detectadas, inclusive felicidade, tristeza, medo, irritação e muito mais.</span><span class="sxs-lookup"><span data-stu-id="922a9-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="922a9-115">Olá **Detector de Face de mídia do Azure** MP está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="922a9-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="922a9-116">Este tópico fornece detalhes sobre **Detector de Face de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET.</span><span class="sxs-lookup"><span data-stu-id="922a9-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="922a9-117">Arquivos de entrada do Face Detector</span><span class="sxs-lookup"><span data-stu-id="922a9-117">Face Detector input files</span></span>
<span data-ttu-id="922a9-118">Arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="922a9-118">Video files.</span></span> <span data-ttu-id="922a9-119">Atualmente, a saudação formatos a seguir têm suporte: MOV, MP4 e WMV.</span><span class="sxs-lookup"><span data-stu-id="922a9-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="922a9-120">Arquivos de saída do Face Detector</span><span class="sxs-lookup"><span data-stu-id="922a9-120">Face Detector output files</span></span>
<span data-ttu-id="922a9-121">API de controle e detecção de face Olá fornece controle que pode detectar o too64 as faces humana em um vídeo e detecção de local de face de alta precisão.</span><span class="sxs-lookup"><span data-stu-id="922a9-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="922a9-122">Faces frontais fornecem Olá obter melhores resultados, enquanto as faces lado e faces pequenas (menor que ou igual a too24x24 pixels) pode não ser tão precisas.</span><span class="sxs-lookup"><span data-stu-id="922a9-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="922a9-123">Olá faces detectadas e controladas são retornadas pelas coordenadas (esquerda, superior, largura e altura) que indica o local de saudação de faces na imagem de saudação em pixels, bem como uma face ID numérica que indica Olá controle dessa pessoa.</span><span class="sxs-lookup"><span data-stu-id="922a9-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="922a9-124">Números de identificação de face são propensas a tooreset em circunstâncias quando face frontal Olá for perdido ou sobreposta no quadro hello, resultando em algumas pessoas ser atribuídas a várias IDs.</span><span class="sxs-lookup"><span data-stu-id="922a9-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="922a9-125"><a id="output_elements"></a>Elementos Olá JSON do arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="922a9-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="922a9-126">Detector de face usa técnicas de fragmentação (onde Olá metadados podem ser dividido em partes com base em hora e você pode baixar apenas o que é necessário) e segmentação (onde os eventos de saudação são divididos caso eles obtêm muito grandes).</span><span class="sxs-lookup"><span data-stu-id="922a9-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="922a9-127">Alguns cálculos simples podem ajudá-lo a transformar dados hello.</span><span class="sxs-lookup"><span data-stu-id="922a9-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="922a9-128">Por exemplo, se um evento tiver começado em 6300 (tiques), com uma escala de tempo de 2997 (tiques/s) e uma taxa de quadros de 29,97 (quadros/s), então:</span><span class="sxs-lookup"><span data-stu-id="922a9-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="922a9-129">Início/Escala de tempo = 2,1 segundos</span><span class="sxs-lookup"><span data-stu-id="922a9-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="922a9-130">Segundos x taxa de quadros = 63 quadros</span><span class="sxs-lookup"><span data-stu-id="922a9-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="922a9-131">Exemplo de entrada e saída da detecção facial</span><span class="sxs-lookup"><span data-stu-id="922a9-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="922a9-132">Vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="922a9-132">Input video</span></span>
[<span data-ttu-id="922a9-133">Vídeo de Entrada</span><span class="sxs-lookup"><span data-stu-id="922a9-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="922a9-134">Configuração de tarefa (predefinição)</span><span class="sxs-lookup"><span data-stu-id="922a9-134">Task configuration (preset)</span></span>
<span data-ttu-id="922a9-135">Ao criar uma tarefa com o **Azure Media Face Detector**, é necessário especificar uma predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="922a9-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="922a9-136">Olá predefinição de configuração a seguir é apenas para detecção de rosto.</span><span class="sxs-lookup"><span data-stu-id="922a9-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="922a9-137">Descrições de atributos</span><span class="sxs-lookup"><span data-stu-id="922a9-137">Attribute descriptions</span></span>
| <span data-ttu-id="922a9-138">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="922a9-138">Attribute name</span></span> | <span data-ttu-id="922a9-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="922a9-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="922a9-140">Mode</span><span class="sxs-lookup"><span data-stu-id="922a9-140">Mode</span></span> |<span data-ttu-id="922a9-141">Mais rápido: maior velocidade de processamento, mas menos precisão (padrão).</span><span class="sxs-lookup"><span data-stu-id="922a9-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="922a9-142">Saída em JSON</span><span class="sxs-lookup"><span data-stu-id="922a9-142">JSON output</span></span>
<span data-ttu-id="922a9-143">saudação de exemplo da saída JSON a seguir foi truncada.</span><span class="sxs-lookup"><span data-stu-id="922a9-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="922a9-144">Exemplo de entrada e saída da detecção de emoção</span><span class="sxs-lookup"><span data-stu-id="922a9-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="922a9-145">Vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="922a9-145">Input video</span></span>
[<span data-ttu-id="922a9-146">Vídeo de Entrada</span><span class="sxs-lookup"><span data-stu-id="922a9-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="922a9-147">Configuração de tarefa (predefinição)</span><span class="sxs-lookup"><span data-stu-id="922a9-147">Task configuration (preset)</span></span>
<span data-ttu-id="922a9-148">Ao criar uma tarefa com o **Azure Media Face Detector**, é necessário especificar uma predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="922a9-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="922a9-149">Olá predefinição de configuração a seguir especifica toocreate que JSON com base na detecção de emoção hello.</span><span class="sxs-lookup"><span data-stu-id="922a9-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="922a9-150">Descrições de atributos</span><span class="sxs-lookup"><span data-stu-id="922a9-150">Attribute descriptions</span></span>
| <span data-ttu-id="922a9-151">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="922a9-151">Attribute name</span></span> | <span data-ttu-id="922a9-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="922a9-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="922a9-153">Modo</span><span class="sxs-lookup"><span data-stu-id="922a9-153">Mode</span></span> |<span data-ttu-id="922a9-154">Faces: somente detecção facial.</span><span class="sxs-lookup"><span data-stu-id="922a9-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="922a9-155">PerFaceEmotion: retornar emoção independentemente de cada detecção facial.</span><span class="sxs-lookup"><span data-stu-id="922a9-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="922a9-156">AggregateEmotion: retorna uma média dos valores de emoção para todas as faces no quadro.</span><span class="sxs-lookup"><span data-stu-id="922a9-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="922a9-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="922a9-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="922a9-158">Use se o modo AggregateEmotion for selecionado.</span><span class="sxs-lookup"><span data-stu-id="922a9-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="922a9-159">Especifica o comprimento de saudação do vídeo tooproduce usado cada resultado da agregação, em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="922a9-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="922a9-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="922a9-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="922a9-161">Use se o modo AggregateEmotion for selecionado.</span><span class="sxs-lookup"><span data-stu-id="922a9-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="922a9-162">Especifica com resultados de agregação de tooproduce que frequência.</span><span class="sxs-lookup"><span data-stu-id="922a9-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="922a9-163">Padrões de agregação</span><span class="sxs-lookup"><span data-stu-id="922a9-163">Aggregate defaults</span></span>
<span data-ttu-id="922a9-164">Abaixo são recomendados para a janela de agregação hello e as configurações de intervalo.</span><span class="sxs-lookup"><span data-stu-id="922a9-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="922a9-165">AggregateEmotionWindowMs deve ser maior que AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="922a9-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="922a9-166">Padrões</span><span class="sxs-lookup"><span data-stu-id="922a9-166">Defaults(s)</span></span> | <span data-ttu-id="922a9-167">Mín.</span><span class="sxs-lookup"><span data-stu-id="922a9-167">Min(s)</span></span> | <span data-ttu-id="922a9-168">Máx.</span><span class="sxs-lookup"><span data-stu-id="922a9-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="922a9-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="922a9-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="922a9-170">0,5</span><span class="sxs-lookup"><span data-stu-id="922a9-170">0.5</span></span> |<span data-ttu-id="922a9-171">2</span><span class="sxs-lookup"><span data-stu-id="922a9-171">2</span></span> |<span data-ttu-id="922a9-172">0,25</span><span class="sxs-lookup"><span data-stu-id="922a9-172">0.25</span></span>|
| <span data-ttu-id="922a9-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="922a9-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="922a9-174">0,5</span><span class="sxs-lookup"><span data-stu-id="922a9-174">0.5</span></span> |<span data-ttu-id="922a9-175">1</span><span class="sxs-lookup"><span data-stu-id="922a9-175">1</span></span> |<span data-ttu-id="922a9-176">0,25</span><span class="sxs-lookup"><span data-stu-id="922a9-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="922a9-177">Saída em JSON</span><span class="sxs-lookup"><span data-stu-id="922a9-177">JSON output</span></span>
<span data-ttu-id="922a9-178">Saída em JSON para agregação de emoção (truncada):</span><span class="sxs-lookup"><span data-stu-id="922a9-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="922a9-179">Limitações</span><span class="sxs-lookup"><span data-stu-id="922a9-179">Limitations</span></span>
* <span data-ttu-id="922a9-180">formatos de vídeo entrada Hello com suporte incluem MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="922a9-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="922a9-181">intervalo de tamanho de face detectáveis Olá é 24 x 24 pixels de too2048x2048.</span><span class="sxs-lookup"><span data-stu-id="922a9-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="922a9-182">Olá faces fora desse intervalo não serão detectadas.</span><span class="sxs-lookup"><span data-stu-id="922a9-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="922a9-183">Para cada vídeo, o número máximo de saudação de faces retornado é 64.</span><span class="sxs-lookup"><span data-stu-id="922a9-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="922a9-184">Algumas faces podem não ser detectadas devido tootechnical desafios; Por exemplo, é muito grandes ângulos de face (pose head) e oclusão grande.</span><span class="sxs-lookup"><span data-stu-id="922a9-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="922a9-185">Faces frontais e próximo frontal tem os melhores resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="922a9-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="922a9-186">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="922a9-186">.NET sample code</span></span>

<span data-ttu-id="922a9-187">a seguir Olá programa mostra como:</span><span class="sxs-lookup"><span data-stu-id="922a9-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="922a9-188">Criar um ativo e carregar um arquivo de mídia no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="922a9-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="922a9-189">Crie um trabalho com uma tarefa de detecção de rosto com base em um arquivo de configuração que contém Olá predefinição json a seguir.</span><span class="sxs-lookup"><span data-stu-id="922a9-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="922a9-190">Baixe os arquivos de saída do JSON hello.</span><span class="sxs-lookup"><span data-stu-id="922a9-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="922a9-191">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="922a9-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="922a9-192">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="922a9-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="922a9-193">Exemplo</span><span class="sxs-lookup"><span data-stu-id="922a9-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="922a9-194">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="922a9-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="922a9-195">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="922a9-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="922a9-196">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="922a9-196">Related links</span></span>
[<span data-ttu-id="922a9-197">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="922a9-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="922a9-198">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="922a9-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

