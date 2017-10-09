---
title: "aaaDetect movimentos com análise de mídia do Azure | Microsoft Docs"
description: "Olá habilita de processador (MP) do Detector de movimento de mídia do Azure media tooefficiently você identificar seções de interesse em um vídeo de outra forma longa e sem problemas."
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="98d9f-103">Detectar movimentos com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="98d9f-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="98d9f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="98d9f-104">Overview</span></span>
<span data-ttu-id="98d9f-105">Olá **Detector de movimento de mídia do Azure** habilita (MP) do processador de mídia tooefficiently você identificar seções de interesse em um vídeo de outra forma longa e sem problemas.</span><span class="sxs-lookup"><span data-stu-id="98d9f-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="98d9f-106">Detecção de movimento pode ser usada em câmera estático filmagens tooidentify seções de vídeo Olá onde ocorre a animação.</span><span class="sxs-lookup"><span data-stu-id="98d9f-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="98d9f-107">Ele gera um arquivo JSON que contém um metadados com carimbos de hora e hello delimitadora região em que ocorreu o evento hello.</span><span class="sxs-lookup"><span data-stu-id="98d9f-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="98d9f-108">Destinado a feeds de vídeo de segurança, essa tecnologia é capaz de toocategorize movimento em eventos relevantes e falsos positivos, como alterações de iluminação e sombras.</span><span class="sxs-lookup"><span data-stu-id="98d9f-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="98d9f-109">Isso permite toogenerate alertas de segurança de feeds de câmera sem recebam eventos irrelevantes infinito, enquanto estiver sendo momentos tooextract capaz de interesse de vídeos de vigilância muito longos.</span><span class="sxs-lookup"><span data-stu-id="98d9f-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="98d9f-110">Olá **Detector de movimento de mídia do Azure** MP está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="98d9f-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="98d9f-111">Este tópico fornece detalhes sobre **Detector de movimento de mídia do Azure** e mostra como toouse com o SDK do Media Services para .NET</span><span class="sxs-lookup"><span data-stu-id="98d9f-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="98d9f-112">Arquivos de entrada do Motion Detector</span><span class="sxs-lookup"><span data-stu-id="98d9f-112">Motion Detector input files</span></span>
<span data-ttu-id="98d9f-113">Arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="98d9f-113">Video files.</span></span> <span data-ttu-id="98d9f-114">Atualmente, a saudação formatos a seguir têm suporte: MOV, MP4 e WMV.</span><span class="sxs-lookup"><span data-stu-id="98d9f-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="98d9f-115">Configuração de tarefa (predefinição)</span><span class="sxs-lookup"><span data-stu-id="98d9f-115">Task configuration (preset)</span></span>
<span data-ttu-id="98d9f-116">Quando você criar uma tarefa com o **Azure Media Motion Detector**, deverá especificar uma predefinição de configuração.</span><span class="sxs-lookup"><span data-stu-id="98d9f-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="98d9f-117">parâmetros</span><span class="sxs-lookup"><span data-stu-id="98d9f-117">Parameters</span></span>
<span data-ttu-id="98d9f-118">Você pode usar o hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="98d9f-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="98d9f-119">Nome</span><span class="sxs-lookup"><span data-stu-id="98d9f-119">Name</span></span> | <span data-ttu-id="98d9f-120">Opções</span><span class="sxs-lookup"><span data-stu-id="98d9f-120">Options</span></span> | <span data-ttu-id="98d9f-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="98d9f-121">Description</span></span> | <span data-ttu-id="98d9f-122">Padrão</span><span class="sxs-lookup"><span data-stu-id="98d9f-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98d9f-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="98d9f-123">sensitivityLevel</span></span> |<span data-ttu-id="98d9f-124">Cadeia de caracteres: 'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="98d9f-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="98d9f-125">Define a sensibilidade de saudação nível no qual movimentos é relatado.</span><span class="sxs-lookup"><span data-stu-id="98d9f-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="98d9f-126">Ajuste esta quantidade tooadjust de falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="98d9f-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="98d9f-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="98d9f-127">'medium'</span></span> |
| <span data-ttu-id="98d9f-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="98d9f-128">frameSamplingValue</span></span> |<span data-ttu-id="98d9f-129">Número inteiro positivo</span><span class="sxs-lookup"><span data-stu-id="98d9f-129">Positive integer</span></span> |<span data-ttu-id="98d9f-130">Define a frequência de saudação no qual o algoritmo é executado.</span><span class="sxs-lookup"><span data-stu-id="98d9f-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="98d9f-131">1 equivale a cada quadro, 2 significa a cada dois quadros e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="98d9f-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="98d9f-132">1</span><span class="sxs-lookup"><span data-stu-id="98d9f-132">1</span></span> |
| <span data-ttu-id="98d9f-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="98d9f-133">detectLightChange</span></span> |<span data-ttu-id="98d9f-134">Booliano: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="98d9f-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="98d9f-135">Define se alterações leves são relatadas nos resultados da saudação</span><span class="sxs-lookup"><span data-stu-id="98d9f-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="98d9f-136">'False'</span><span class="sxs-lookup"><span data-stu-id="98d9f-136">'False'</span></span> |
| <span data-ttu-id="98d9f-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="98d9f-137">mergeTimeThreshold</span></span> |<span data-ttu-id="98d9f-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="98d9f-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="98d9f-139">Exemplo: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="98d9f-139">Example: 00:00:03</span></span> |<span data-ttu-id="98d9f-140">Especifica a janela de tempo de saudação entre os eventos de movimento onde 2 eventos serão combinados e relatados como 1.</span><span class="sxs-lookup"><span data-stu-id="98d9f-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="98d9f-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="98d9f-141">00:00:00</span></span> |
| <span data-ttu-id="98d9f-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="98d9f-142">detectionZones</span></span> |<span data-ttu-id="98d9f-143">Uma matriz de zonas de detecção:</span><span class="sxs-lookup"><span data-stu-id="98d9f-143">An array of detection zones:</span></span><br/><span data-ttu-id="98d9f-144">- A Zona de Detecção é uma matriz de três ou mais pontos</span><span class="sxs-lookup"><span data-stu-id="98d9f-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="98d9f-145">-Ponto é um x e y coordenada de too1 0.</span><span class="sxs-lookup"><span data-stu-id="98d9f-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="98d9f-146">Descreve a lista de saudação de detecção poligonal zonas toobe usado.</span><span class="sxs-lookup"><span data-stu-id="98d9f-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="98d9f-147">Resultados serão relatados com zonas hello como uma ID, com hello primeiro sendo 'id': 0</span><span class="sxs-lookup"><span data-stu-id="98d9f-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="98d9f-148">Zona única que abrange toda a estrutura hello.</span><span class="sxs-lookup"><span data-stu-id="98d9f-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="98d9f-149">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="98d9f-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="98d9f-150">Arquivos de saída do Motion Detector</span><span class="sxs-lookup"><span data-stu-id="98d9f-150">Motion Detector output files</span></span>
<span data-ttu-id="98d9f-151">Um trabalho de detecção de movimento retornará um arquivo JSON Olá ativo de saída que descreve os alertas de movimento hello e suas categorias, dentro de saudação vídeo.</span><span class="sxs-lookup"><span data-stu-id="98d9f-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="98d9f-152">arquivo de saudação conterá informações sobre tempo de saudação e a duração da animação detectada no vídeo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d9f-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="98d9f-153">Olá API do Detector de movimento fornece indicadores quando existem objetos em movimento em um plano fixo vídeo (por exemplo, um vídeo de inspeção).</span><span class="sxs-lookup"><span data-stu-id="98d9f-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="98d9f-154">Olá Detector de movimento é treinado tooreduce falsos alarmes, iluminação e as alterações de sombra.</span><span class="sxs-lookup"><span data-stu-id="98d9f-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="98d9f-155">Limitações atuais dos algoritmos de saudação incluem vídeos de visão da noite, semitransparentes objetos e objetos pequenos.</span><span class="sxs-lookup"><span data-stu-id="98d9f-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="98d9f-156"><a id="output_elements"></a>Elementos Olá JSON do arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="98d9f-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="98d9f-157">Na versão mais recente do hello, formato da saída JSON de saudação foi alterado e pode representar uma alteração significativa para alguns clientes.</span><span class="sxs-lookup"><span data-stu-id="98d9f-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="98d9f-158">Olá tabela a seguir descreve os elementos Olá JSON do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="98d9f-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="98d9f-159">Elemento</span><span class="sxs-lookup"><span data-stu-id="98d9f-159">Element</span></span> | <span data-ttu-id="98d9f-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="98d9f-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98d9f-161">Versão</span><span class="sxs-lookup"><span data-stu-id="98d9f-161">Version</span></span> |<span data-ttu-id="98d9f-162">Isso se refere a versão toohello de saudação API de vídeo.</span><span class="sxs-lookup"><span data-stu-id="98d9f-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="98d9f-163">versão atual do Hello é 2.</span><span class="sxs-lookup"><span data-stu-id="98d9f-163">hello current version is 2.</span></span> |
| <span data-ttu-id="98d9f-164">Escala de tempo</span><span class="sxs-lookup"><span data-stu-id="98d9f-164">Timescale</span></span> |<span data-ttu-id="98d9f-165">"Tiques" por segundo de vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="98d9f-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="98d9f-166">Deslocamento</span><span class="sxs-lookup"><span data-stu-id="98d9f-166">Offset</span></span> |<span data-ttu-id="98d9f-167">deslocamento de horário de saudação de carimbos de hora em "tiques".</span><span class="sxs-lookup"><span data-stu-id="98d9f-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="98d9f-168">Na versão 1.0 das APIs de Vídeo, sempre será 0.</span><span class="sxs-lookup"><span data-stu-id="98d9f-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="98d9f-169">Em cenários futuro para os quais oferecemos suporte, esse valor poderá ser alterado.</span><span class="sxs-lookup"><span data-stu-id="98d9f-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="98d9f-170">Taxa de quadros</span><span class="sxs-lookup"><span data-stu-id="98d9f-170">Framerate</span></span> |<span data-ttu-id="98d9f-171">Quadros por segundo do hello vídeo.</span><span class="sxs-lookup"><span data-stu-id="98d9f-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="98d9f-172">Largura, Altura</span><span class="sxs-lookup"><span data-stu-id="98d9f-172">Width, Height</span></span> |<span data-ttu-id="98d9f-173">Refere-se toohello largura e altura da saudação vídeo em pixels.</span><span class="sxs-lookup"><span data-stu-id="98d9f-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="98d9f-174">Iniciar</span><span class="sxs-lookup"><span data-stu-id="98d9f-174">Start</span></span> |<span data-ttu-id="98d9f-175">Olá iniciar carimbo de hora "tiques".</span><span class="sxs-lookup"><span data-stu-id="98d9f-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="98d9f-176">Duration</span><span class="sxs-lookup"><span data-stu-id="98d9f-176">Duration</span></span> |<span data-ttu-id="98d9f-177">comprimento de saudação do evento hello, em "tiques".</span><span class="sxs-lookup"><span data-stu-id="98d9f-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="98d9f-178">Intervalo</span><span class="sxs-lookup"><span data-stu-id="98d9f-178">Interval</span></span> |<span data-ttu-id="98d9f-179">intervalo de saudação de cada entrada no evento hello, em "tiques".</span><span class="sxs-lookup"><span data-stu-id="98d9f-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="98d9f-180">Eventos</span><span class="sxs-lookup"><span data-stu-id="98d9f-180">Events</span></span> |<span data-ttu-id="98d9f-181">Cada fragmento do evento contém movimento Olá detectado dentro desse tempo de duração.</span><span class="sxs-lookup"><span data-stu-id="98d9f-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="98d9f-182">Tipo</span><span class="sxs-lookup"><span data-stu-id="98d9f-182">Type</span></span> |<span data-ttu-id="98d9f-183">Na versão atual do hello, isso é sempre '2' para o movimento genérico.</span><span class="sxs-lookup"><span data-stu-id="98d9f-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="98d9f-184">Este rótulo fornece toocategorize movimento por vídeo APIs Olá flexibilidade em versões futuras.</span><span class="sxs-lookup"><span data-stu-id="98d9f-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="98d9f-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="98d9f-185">RegionID</span></span> |<span data-ttu-id="98d9f-186">Conforme explicado acima, isso sempre será 0 nesta versão.</span><span class="sxs-lookup"><span data-stu-id="98d9f-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="98d9f-187">Este rótulo fornece movimento por vídeo API Olá flexibilidade toofind em várias regiões em versões futuras.</span><span class="sxs-lookup"><span data-stu-id="98d9f-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="98d9f-188">Regiões</span><span class="sxs-lookup"><span data-stu-id="98d9f-188">Regions</span></span> |<span data-ttu-id="98d9f-189">Refere-se a área de toohello no vídeo onde você se preocupa movimento.</span><span class="sxs-lookup"><span data-stu-id="98d9f-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="98d9f-190">-"id" representa a área da região hello – nesta versão há apenas um, ID de 0.</span><span class="sxs-lookup"><span data-stu-id="98d9f-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="98d9f-191">-"type" representa a forma de saudação da região Olá importantes para você por movimento.</span><span class="sxs-lookup"><span data-stu-id="98d9f-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="98d9f-192">Atualmente, "retângulo" e "polígono" têm suporte.</span><span class="sxs-lookup"><span data-stu-id="98d9f-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="98d9f-193">Se você especificou "retângulo", a região Olá tem dimensões em X, Y, largura e altura.</span><span class="sxs-lookup"><span data-stu-id="98d9f-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="98d9f-194">Hello X e Y coordenadas representam as coordenadas XY Olá superior esquerdo da região de saudação em uma escala normalizada de 0.0 too1.0.</span><span class="sxs-lookup"><span data-stu-id="98d9f-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="98d9f-195">altura e largura de saudação representam o tamanho de saudação da região de saudação em uma escala normalizada de too1.0 0.0.</span><span class="sxs-lookup"><span data-stu-id="98d9f-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="98d9f-196">Na versão atual do hello, X, Y, largura e altura sempre são corrigidas em 0, 0 e 1, 1.</span><span class="sxs-lookup"><span data-stu-id="98d9f-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="98d9f-197">Se você especificou "polígono", a região Olá tem dimensões em pontos.</span><span class="sxs-lookup"><span data-stu-id="98d9f-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="98d9f-198">Fragmentos</span><span class="sxs-lookup"><span data-stu-id="98d9f-198">Fragments</span></span> |<span data-ttu-id="98d9f-199">Olá metadados está em bloco para cima em diferentes segmentos de chamadas de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="98d9f-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="98d9f-200">Cada fragmento contém um início, uma duração, um número de intervalo e evento(s).</span><span class="sxs-lookup"><span data-stu-id="98d9f-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="98d9f-201">Um fragmento sem eventos significa que nenhum movimento foi detectado durante essa hora de início e duração.</span><span class="sxs-lookup"><span data-stu-id="98d9f-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="98d9f-202">Colchetes []</span><span class="sxs-lookup"><span data-stu-id="98d9f-202">Brackets []</span></span> |<span data-ttu-id="98d9f-203">Cada colchete representa um intervalo em eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d9f-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="98d9f-204">Colchetes vazios para esse intervalo significam que nenhum movimento foi detectado.</span><span class="sxs-lookup"><span data-stu-id="98d9f-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="98d9f-205">locais</span><span class="sxs-lookup"><span data-stu-id="98d9f-205">locations</span></span> |<span data-ttu-id="98d9f-206">Essa nova entrada em eventos lista local de saudação onde ocorreu o movimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d9f-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="98d9f-207">Isso é mais específico que zonas de detecção de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d9f-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="98d9f-208">a seguir Olá é um exemplo de saída JSON</span><span class="sxs-lookup"><span data-stu-id="98d9f-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="98d9f-209">Limitações</span><span class="sxs-lookup"><span data-stu-id="98d9f-209">Limitations</span></span>
* <span data-ttu-id="98d9f-210">formatos de vídeo entrada Hello com suporte incluem MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="98d9f-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="98d9f-211">A detecção de movimento é otimizada para vídeos estáticos em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="98d9f-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="98d9f-212">algoritmo de saudação se concentra na redução alarmes falsos, como alterações de iluminação e sombras.</span><span class="sxs-lookup"><span data-stu-id="98d9f-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="98d9f-213">Alguns movimento não pode ser detectado devido tootechnical desafios; Por exemplo, vídeos de visão da noite, semitransparentes objetos e objetos pequenos.</span><span class="sxs-lookup"><span data-stu-id="98d9f-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="98d9f-214">Código de exemplo do .NET</span><span class="sxs-lookup"><span data-stu-id="98d9f-214">.NET sample code</span></span>

<span data-ttu-id="98d9f-215">a seguir Olá programa mostra como:</span><span class="sxs-lookup"><span data-stu-id="98d9f-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="98d9f-216">Criar um ativo e carregar um arquivo de mídia no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="98d9f-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="98d9f-217">Crie um trabalho com uma tarefa de detecção de movimento por vídeo com base em um arquivo de configuração que contém Olá predefinição json a seguir.</span><span class="sxs-lookup"><span data-stu-id="98d9f-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="98d9f-218">Baixe os arquivos de saída do JSON hello.</span><span class="sxs-lookup"><span data-stu-id="98d9f-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="98d9f-219">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98d9f-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="98d9f-220">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="98d9f-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="98d9f-221">Exemplo</span><span class="sxs-lookup"><span data-stu-id="98d9f-221">Example</span></span>


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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="98d9f-222">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="98d9f-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="98d9f-223">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="98d9f-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="98d9f-224">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="98d9f-224">Related links</span></span>
[<span data-ttu-id="98d9f-225">Blog do Detector de movimento dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="98d9f-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="98d9f-226">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="98d9f-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="98d9f-227">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="98d9f-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

