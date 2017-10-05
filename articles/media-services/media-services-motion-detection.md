---
title: Detectar movimentos com o Azure Media Analytics | Microsoft Docs
description: "O MP (processador de mídia) Azure Media Motion Detector permite a identificação eficiente de seções de interesse em um vídeo longo e rotineiro."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="dafb7-103">Detectar movimentos com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="dafb7-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="dafb7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dafb7-104">Overview</span></span>
<span data-ttu-id="dafb7-105">O MP (processador de mídia) **Azure Media Motion Detector** permite a identificação eficiente de seções de interesse em um vídeo longo e rotineiro.</span><span class="sxs-lookup"><span data-stu-id="dafb7-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="dafb7-106">A detecção de movimento pode ser usada em sequências de imagens estáticas para identificar seções do vídeo onde ocorrem movimentos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="dafb7-107">Ela gera um arquivo JSON contendo metadados com carimbos de hora e a região delimitadora onde o evento ocorreu.</span><span class="sxs-lookup"><span data-stu-id="dafb7-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="dafb7-108">Essa tecnologia, destinada à segurança de feeds de vídeo, é capaz de categorizar o movimento em eventos relevantes e falsos positivos, como mudanças de iluminação e sombras.</span><span class="sxs-lookup"><span data-stu-id="dafb7-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="dafb7-109">Isso permite a geração de alertas de segurança por meio de feeds da câmera, sem gerar incontáveis eventos irrelevantes, além de permitir também a extração de momentos de interesse dos vídeos de vigilância extremamente longos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="dafb7-110">No momento, o MP **Azure Media Motion Detector** está em versão de Visualização.</span><span class="sxs-lookup"><span data-stu-id="dafb7-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="dafb7-111">Este tópico fornece detalhes sobre o **Azure Media Motion Detector** e mostra como usá-lo com o SDK dos Serviços de Mídia para .NET</span><span class="sxs-lookup"><span data-stu-id="dafb7-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="dafb7-112">Arquivos de entrada do Motion Detector</span><span class="sxs-lookup"><span data-stu-id="dafb7-112">Motion Detector input files</span></span>
<span data-ttu-id="dafb7-113">Arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-113">Video files.</span></span> <span data-ttu-id="dafb7-114">Atualmente, há suporte para os seguintes formatos: MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="dafb7-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="dafb7-115">Configuração de tarefa (predefinição)</span><span class="sxs-lookup"><span data-stu-id="dafb7-115">Task configuration (preset)</span></span>
<span data-ttu-id="dafb7-116">Quando você criar uma tarefa com o **Azure Media Motion Detector**, deverá especificar uma predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="dafb7-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="dafb7-117">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="dafb7-117">Parameters</span></span>
<span data-ttu-id="dafb7-118">Você pode usar os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="dafb7-118">You can use the following parameters:</span></span>

| <span data-ttu-id="dafb7-119">Nome</span><span class="sxs-lookup"><span data-stu-id="dafb7-119">Name</span></span> | <span data-ttu-id="dafb7-120">Opções</span><span class="sxs-lookup"><span data-stu-id="dafb7-120">Options</span></span> | <span data-ttu-id="dafb7-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="dafb7-121">Description</span></span> | <span data-ttu-id="dafb7-122">Padrão</span><span class="sxs-lookup"><span data-stu-id="dafb7-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dafb7-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="dafb7-123">sensitivityLevel</span></span> |<span data-ttu-id="dafb7-124">Cadeia de caracteres: 'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="dafb7-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="dafb7-125">Define o nível de sensibilidade para relatar os movimentos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="dafb7-126">Ajuste para ajustar a quantidade de falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="dafb7-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="dafb7-127">'medium'</span></span> |
| <span data-ttu-id="dafb7-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="dafb7-128">frameSamplingValue</span></span> |<span data-ttu-id="dafb7-129">Número inteiro positivo</span><span class="sxs-lookup"><span data-stu-id="dafb7-129">Positive integer</span></span> |<span data-ttu-id="dafb7-130">Define a frequência na qual o algoritmo é executado.</span><span class="sxs-lookup"><span data-stu-id="dafb7-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="dafb7-131">1 equivale a cada quadro, 2 significa a cada dois quadros e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="dafb7-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="dafb7-132">1</span><span class="sxs-lookup"><span data-stu-id="dafb7-132">1</span></span> |
| <span data-ttu-id="dafb7-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="dafb7-133">detectLightChange</span></span> |<span data-ttu-id="dafb7-134">Booliano: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="dafb7-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="dafb7-135">Define se as mudanças leves são relatadas nos resultados</span><span class="sxs-lookup"><span data-stu-id="dafb7-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="dafb7-136">'False'</span><span class="sxs-lookup"><span data-stu-id="dafb7-136">'False'</span></span> |
| <span data-ttu-id="dafb7-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="dafb7-137">mergeTimeThreshold</span></span> |<span data-ttu-id="dafb7-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="dafb7-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="dafb7-139">Exemplo: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="dafb7-139">Example: 00:00:03</span></span> |<span data-ttu-id="dafb7-140">Especifica a janela de tempo entre eventos de movimento, em que dois eventos serão combinados e relatados como um.</span><span class="sxs-lookup"><span data-stu-id="dafb7-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="dafb7-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="dafb7-141">00:00:00</span></span> |
| <span data-ttu-id="dafb7-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="dafb7-142">detectionZones</span></span> |<span data-ttu-id="dafb7-143">Uma matriz de zonas de detecção:</span><span class="sxs-lookup"><span data-stu-id="dafb7-143">An array of detection zones:</span></span><br/><span data-ttu-id="dafb7-144">- A Zona de Detecção é uma matriz de três ou mais pontos</span><span class="sxs-lookup"><span data-stu-id="dafb7-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="dafb7-145">- Ponto é uma coordenada x e y de 0 a 1.</span><span class="sxs-lookup"><span data-stu-id="dafb7-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="dafb7-146">Descreve a lista de zonas de detecção em forma de polígono a ser usada.</span><span class="sxs-lookup"><span data-stu-id="dafb7-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="dafb7-147">Os resultados serão informados com as zonas como uma ID, com o primeiro sendo 'id': 0</span><span class="sxs-lookup"><span data-stu-id="dafb7-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="dafb7-148">Zona única que abrange todo o quadro.</span><span class="sxs-lookup"><span data-stu-id="dafb7-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="dafb7-149">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="dafb7-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="dafb7-150">Arquivos de saída do Motion Detector</span><span class="sxs-lookup"><span data-stu-id="dafb7-150">Motion Detector output files</span></span>
<span data-ttu-id="dafb7-151">Um trabalho de detecção de movimento retornará um arquivo JSON no ativo de saída, que descreve os alertas de movimento, e suas categorias, no vídeo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="dafb7-152">O arquivo conterá informações sobre a hora e a duração do movimento detectado no vídeo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="dafb7-153">A API do Motion Detector fornecerá indicadores quando houver objetos em movimento em um vídeo fixo em segundo plano (por exemplo, um vídeo de vigilância).</span><span class="sxs-lookup"><span data-stu-id="dafb7-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="dafb7-154">O Motion Detector é treinado para reduzir alarmes falsos, como mudanças de iluminação e de sombra.</span><span class="sxs-lookup"><span data-stu-id="dafb7-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="dafb7-155">As limitações atuais dos algoritmos incluem vídeos de visão noturna, objetos semitransparentes e objetos pequenos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="dafb7-156"><a id="output_elements"></a>Elementos do arquivo JSON de saída</span><span class="sxs-lookup"><span data-stu-id="dafb7-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="dafb7-157">Na versão mais recente, o formato JSON de saída foi alterado e pode representar uma alteração significativa para alguns clientes.</span><span class="sxs-lookup"><span data-stu-id="dafb7-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="dafb7-158">A tabela a seguir descreve os elementos do arquivo JSON de saída:</span><span class="sxs-lookup"><span data-stu-id="dafb7-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="dafb7-159">Elemento</span><span class="sxs-lookup"><span data-stu-id="dafb7-159">Element</span></span> | <span data-ttu-id="dafb7-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="dafb7-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dafb7-161">Versão</span><span class="sxs-lookup"><span data-stu-id="dafb7-161">Version</span></span> |<span data-ttu-id="dafb7-162">Refere-se à versão da API de Vídeo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="dafb7-163">A versão atual é 2.</span><span class="sxs-lookup"><span data-stu-id="dafb7-163">The current version is 2.</span></span> |
| <span data-ttu-id="dafb7-164">Escala de tempo</span><span class="sxs-lookup"><span data-stu-id="dafb7-164">Timescale</span></span> |<span data-ttu-id="dafb7-165">"Tiques" por segundo do vídeo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="dafb7-166">Deslocamento</span><span class="sxs-lookup"><span data-stu-id="dafb7-166">Offset</span></span> |<span data-ttu-id="dafb7-167">A diferença de tempo para carimbos de hora em “tiques”.</span><span class="sxs-lookup"><span data-stu-id="dafb7-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="dafb7-168">Na versão 1.0 das APIs de Vídeo, sempre será 0.</span><span class="sxs-lookup"><span data-stu-id="dafb7-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="dafb7-169">Em cenários futuro para os quais oferecemos suporte, esse valor poderá ser alterado.</span><span class="sxs-lookup"><span data-stu-id="dafb7-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="dafb7-170">Taxa de quadros</span><span class="sxs-lookup"><span data-stu-id="dafb7-170">Framerate</span></span> |<span data-ttu-id="dafb7-171">Quadros por segundo do vídeo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="dafb7-172">Largura, Altura</span><span class="sxs-lookup"><span data-stu-id="dafb7-172">Width, Height</span></span> |<span data-ttu-id="dafb7-173">Refere-se à largura e à altura do vídeo em pixels.</span><span class="sxs-lookup"><span data-stu-id="dafb7-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="dafb7-174">Iniciar</span><span class="sxs-lookup"><span data-stu-id="dafb7-174">Start</span></span> |<span data-ttu-id="dafb7-175">O carimbo de hora inicial em "tiques".</span><span class="sxs-lookup"><span data-stu-id="dafb7-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="dafb7-176">Duração</span><span class="sxs-lookup"><span data-stu-id="dafb7-176">Duration</span></span> |<span data-ttu-id="dafb7-177">A duração do evento, em "tiques".</span><span class="sxs-lookup"><span data-stu-id="dafb7-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="dafb7-178">Intervalo</span><span class="sxs-lookup"><span data-stu-id="dafb7-178">Interval</span></span> |<span data-ttu-id="dafb7-179">O intervalo de cada entrada no evento, em "tiques".</span><span class="sxs-lookup"><span data-stu-id="dafb7-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="dafb7-180">Eventos</span><span class="sxs-lookup"><span data-stu-id="dafb7-180">Events</span></span> |<span data-ttu-id="dafb7-181">Cada fragmento de evento contém o movimento detectado dentro dessa duração.</span><span class="sxs-lookup"><span data-stu-id="dafb7-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="dafb7-182">Tipo</span><span class="sxs-lookup"><span data-stu-id="dafb7-182">Type</span></span> |<span data-ttu-id="dafb7-183">Na versão atual, essa opção sempre será “2” para movimentos genéricos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="dafb7-184">Esse rótulo dá a flexibilidade às APIs de Vídeo para categorizar o movimento em futuras versões.</span><span class="sxs-lookup"><span data-stu-id="dafb7-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="dafb7-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="dafb7-185">RegionID</span></span> |<span data-ttu-id="dafb7-186">Conforme explicado acima, isso sempre será 0 nesta versão.</span><span class="sxs-lookup"><span data-stu-id="dafb7-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="dafb7-187">Esse rótulo oferece à API de Vídeo a flexibilidade de encontrar o movimento em várias regiões em versões futuras.</span><span class="sxs-lookup"><span data-stu-id="dafb7-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="dafb7-188">Regiões</span><span class="sxs-lookup"><span data-stu-id="dafb7-188">Regions</span></span> |<span data-ttu-id="dafb7-189">Refere-se à área no vídeo onde você se preocupa com movimento.</span><span class="sxs-lookup"><span data-stu-id="dafb7-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="dafb7-190">-"id" representa a área de região – nesta versão há apenas uma, ID 0.</span><span class="sxs-lookup"><span data-stu-id="dafb7-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="dafb7-191">-"type" representa a forma da região em que você se preocupa com o movimento.</span><span class="sxs-lookup"><span data-stu-id="dafb7-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="dafb7-192">Atualmente, "retângulo" e "polígono" têm suporte.</span><span class="sxs-lookup"><span data-stu-id="dafb7-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="dafb7-193">Se você tiver especificado "retângulo", a região terá dimensões em X, Y, largura e altura.</span><span class="sxs-lookup"><span data-stu-id="dafb7-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="dafb7-194">As coordenadas X e Y representam as coordenadas XY do lado superior esquerdo da região em uma escala normalizada de 0,0 a 1,0.</span><span class="sxs-lookup"><span data-stu-id="dafb7-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="dafb7-195">A largura e a altura representam o tamanho da região em uma escala normalizada de 0,0 a 1,0.</span><span class="sxs-lookup"><span data-stu-id="dafb7-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="dafb7-196">Na versão atual, X, Y, largura e altura são sempre fixos em 0, 0 e 1, 1.</span><span class="sxs-lookup"><span data-stu-id="dafb7-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="dafb7-197">Se você tiver especificado "polígono", a região terá dimensões em pontos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="dafb7-198">Fragmentos</span><span class="sxs-lookup"><span data-stu-id="dafb7-198">Fragments</span></span> |<span data-ttu-id="dafb7-199">Os metadados são agrupados em segmentos diferentes, chamados fragmentos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="dafb7-200">Cada fragmento contém um início, uma duração, um número de intervalo e evento(s).</span><span class="sxs-lookup"><span data-stu-id="dafb7-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="dafb7-201">Um fragmento sem eventos significa que nenhum movimento foi detectado durante essa hora de início e duração.</span><span class="sxs-lookup"><span data-stu-id="dafb7-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="dafb7-202">Colchetes []</span><span class="sxs-lookup"><span data-stu-id="dafb7-202">Brackets []</span></span> |<span data-ttu-id="dafb7-203">Cada colchete representa um intervalo no evento.</span><span class="sxs-lookup"><span data-stu-id="dafb7-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="dafb7-204">Colchetes vazios para esse intervalo significam que nenhum movimento foi detectado.</span><span class="sxs-lookup"><span data-stu-id="dafb7-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="dafb7-205">locais</span><span class="sxs-lookup"><span data-stu-id="dafb7-205">locations</span></span> |<span data-ttu-id="dafb7-206">Essa nova entrada em eventos lista o local onde ocorreu o movimento.</span><span class="sxs-lookup"><span data-stu-id="dafb7-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="dafb7-207">Isso é mais específico do que as zonas de detecção.</span><span class="sxs-lookup"><span data-stu-id="dafb7-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="dafb7-208">Este é um exemplo de saída JSON</span><span class="sxs-lookup"><span data-stu-id="dafb7-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="dafb7-209">Limitações</span><span class="sxs-lookup"><span data-stu-id="dafb7-209">Limitations</span></span>
* <span data-ttu-id="dafb7-210">Os formatos de vídeo de entrada com suporte incluem MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="dafb7-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="dafb7-211">A detecção de movimento é otimizada para vídeos estáticos em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="dafb7-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="dafb7-212">O algoritmo se concentra na redução de alarmes falsos, como mudanças de iluminação e sombras.</span><span class="sxs-lookup"><span data-stu-id="dafb7-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="dafb7-213">Talvez algum movimento não seja detectado devido a desafios técnicos; por exemplo, vídeos de visão noturna, objetos semitransparentes e objetos pequenos.</span><span class="sxs-lookup"><span data-stu-id="dafb7-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="dafb7-214">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="dafb7-214">.NET sample code</span></span>

<span data-ttu-id="dafb7-215">O programa a seguir mostra como:</span><span class="sxs-lookup"><span data-stu-id="dafb7-215">The following program shows how to:</span></span>

1. <span data-ttu-id="dafb7-216">Criar um ativo e carregar um arquivo de mídia nesse ativo.</span><span class="sxs-lookup"><span data-stu-id="dafb7-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="dafb7-217">Crie um trabalho com uma tarefa de detecção de movimento em vídeo baseada em um arquivo de configuração que contém a predefinição de JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="dafb7-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="dafb7-218">Baixe os arquivos JSON de saída.</span><span class="sxs-lookup"><span data-stu-id="dafb7-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="dafb7-219">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dafb7-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="dafb7-220">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="dafb7-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="dafb7-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="dafb7-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="dafb7-222">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="dafb7-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dafb7-223">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="dafb7-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="dafb7-224">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="dafb7-224">Related links</span></span>
[<span data-ttu-id="dafb7-225">Blog do Detector de movimento dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="dafb7-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="dafb7-226">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="dafb7-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="dafb7-227">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="dafb7-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

