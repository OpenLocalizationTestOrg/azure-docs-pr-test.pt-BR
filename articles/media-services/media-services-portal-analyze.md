---
title: "Analisar sua mídia usando o Portal do Azure | Microsoft Docs"
description: "Este tópico aborda como processar sua mídia com processadores de mídia (MPs) da Análise de Mídia usando o Portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="5dce1-103">Analisar sua mídia usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5dce1-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="5dce1-104">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dce1-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5dce1-105">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5dce1-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="5dce1-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5dce1-106">Overview</span></span>
<span data-ttu-id="5dce1-107">A Análise dos Serviços de Mídia do Azure é uma coleção de componentes de fala e visão (em escala empresarial, conformidade, segurança e alcance global) que facilitam para as organizações e empresas obterem ideias práticas de seus arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="5dce1-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="5dce1-108">Para maiores detalhes da Análise de Serviços de Mídia do Azure consulte [esse](media-services-analytics-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="5dce1-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="5dce1-109">Este tópico aborda como processar sua mídia com processadores de mídia (MPs) da Análise de Mídia usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dce1-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="5dce1-110">Os MPs da Análise de Mídia produzem arquivos MP4 ou arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="5dce1-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="5dce1-111">Se um processador de mídia produzir um arquivo MP4, você poderá baixar o arquivo progressivamente.</span><span class="sxs-lookup"><span data-stu-id="5dce1-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="5dce1-112">Se um processador de mídia produzir um arquivo JSON, você poderá baixar o arquivo do Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dce1-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="5dce1-113">Escolha um ativo que você deseja analisar</span><span class="sxs-lookup"><span data-stu-id="5dce1-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="5dce1-114">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dce1-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5dce1-115">Na janela **Configurações**, selecione **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="5dce1-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="5dce1-116">.</span><span class="sxs-lookup"><span data-stu-id="5dce1-116">.</span></span>
    <span data-ttu-id="5dce1-117">![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="5dce1-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="5dce1-118">Selecione o ativo que você deseja analisar e pressione o botão **Analisar**.</span><span class="sxs-lookup"><span data-stu-id="5dce1-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="5dce1-120">Na janela **Processar ativo de mídia com Análise de Mídia**, selecione o processador.</span><span class="sxs-lookup"><span data-stu-id="5dce1-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="5dce1-121">O restante do artigo explica porque e como usar cada processador.</span><span class="sxs-lookup"><span data-stu-id="5dce1-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="5dce1-122">Pressione **Criar** para iniciar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="5dce1-123">Indexador de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="5dce1-123">Azure Media Indexer</span></span>
<span data-ttu-id="5dce1-124">O processador de mídia do **Azure Media Indexer** permite tornar conteúdo e arquivos de mídia pesquisáveis, bem como gerar faixas de legendagem oculta.</span><span class="sxs-lookup"><span data-stu-id="5dce1-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="5dce1-125">Esta seção fornece alguns detalhes sobre as opções que você pode especificar para esse MP.</span><span class="sxs-lookup"><span data-stu-id="5dce1-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="5dce1-127">Linguagem</span><span class="sxs-lookup"><span data-stu-id="5dce1-127">Language</span></span>
<span data-ttu-id="5dce1-128">O idioma natural a ser reconhecido no arquivo de multimídia.</span><span class="sxs-lookup"><span data-stu-id="5dce1-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="5dce1-129">Por exemplo, inglês ou espanhol.</span><span class="sxs-lookup"><span data-stu-id="5dce1-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="5dce1-130">Legendas</span><span class="sxs-lookup"><span data-stu-id="5dce1-130">Captions</span></span>
<span data-ttu-id="5dce1-131">Você pode escolher um formato de legenda que será gerado do seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5dce1-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="5dce1-132">Um trabalho de indexação pode gerar arquivos de legenda oculta nos seguintes formatos:</span><span class="sxs-lookup"><span data-stu-id="5dce1-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="5dce1-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="5dce1-133">**SAMI**</span></span>
* <span data-ttu-id="5dce1-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="5dce1-134">**TTML**</span></span>
* <span data-ttu-id="5dce1-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="5dce1-135">**WebVTT**</span></span>

<span data-ttu-id="5dce1-136">Arquivos de CC (Legenda Oculta) nesses formatos podem ser usados para tornar os arquivos de áudio e vídeo acessíveis para pessoas com deficiência auditiva.</span><span class="sxs-lookup"><span data-stu-id="5dce1-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="5dce1-137">Arquivo AIB</span><span class="sxs-lookup"><span data-stu-id="5dce1-137">AIB file</span></span>
<span data-ttu-id="5dce1-138">Selecione esta opção se você deseja gerar o Arquivo de blob de índice de áudio para uso com o IFilter personalizado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5dce1-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="5dce1-139">Para saber mais, confira [este](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="5dce1-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="5dce1-140">Palavras-chave</span><span class="sxs-lookup"><span data-stu-id="5dce1-140">Keywords</span></span>
<span data-ttu-id="5dce1-141">Selecione esta opção se você gostaria de gerar um arquivo XML de palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="5dce1-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="5dce1-142">Esse arquivo contém palavras-chave extraídas do conteúdo de fala, com informações de frequência de compensação.</span><span class="sxs-lookup"><span data-stu-id="5dce1-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="5dce1-143">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="5dce1-143">Job name</span></span>
<span data-ttu-id="5dce1-144">Um nome amigável que permite identificar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="5dce1-145">[Esse](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o progresso de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5dce1-146">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="5dce1-146">Output file</span></span>
<span data-ttu-id="5dce1-147">Um nome amigável que permite identificar o conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="5dce1-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="5dce1-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="5dce1-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="5dce1-149">O Azure Media Hyperlapse é um MP que cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação.</span><span class="sxs-lookup"><span data-stu-id="5dce1-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="5dce1-150">Para obter mais informações, consulte [este](media-services-hyperlapse-content.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="5dce1-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="5dce1-151">Esta seção fornece alguns detalhes sobre as opções que você pode especificar para esse MP.</span><span class="sxs-lookup"><span data-stu-id="5dce1-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="5dce1-153">Velocidade</span><span class="sxs-lookup"><span data-stu-id="5dce1-153">Speed</span></span>
<span data-ttu-id="5dce1-154">Especifique a velocidade com a qual acelerar o vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="5dce1-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="5dce1-155">A saída é uma representação estabilizada e de lapso de tempo do vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="5dce1-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="5dce1-156">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="5dce1-156">Job name</span></span>
<span data-ttu-id="5dce1-157">Um nome amigável que permite identificar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="5dce1-158">[Esse](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o progresso de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5dce1-159">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="5dce1-159">Output file</span></span>
<span data-ttu-id="5dce1-160">Um nome amigável que permite identificar o conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="5dce1-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="5dce1-161">Detector de Rostos em Mídias do Azure</span><span class="sxs-lookup"><span data-stu-id="5dce1-161">Azure Media Face Detector</span></span>
<span data-ttu-id="5dce1-162">O MP (processador de mídia) **Azure Media Face Detector** permite que você conte e acompanhe movimentos, e até mesmo meça a participação e a reação do público por meio de expressões faciais.</span><span class="sxs-lookup"><span data-stu-id="5dce1-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="5dce1-163">Este serviço contém dois recursos:</span><span class="sxs-lookup"><span data-stu-id="5dce1-163">This service contains two features:</span></span> 

* <span data-ttu-id="5dce1-164">**Detecção facial**</span><span class="sxs-lookup"><span data-stu-id="5dce1-164">**Face detection**</span></span>
  
    <span data-ttu-id="5dce1-165">A detecção facial localiza e acompanha as faces humanas em um vídeo.</span><span class="sxs-lookup"><span data-stu-id="5dce1-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="5dce1-166">Várias faces podem ser detectadas e, consequentemente, acompanhadas à medida que se movimentam, com os metadados de hora e local retornados em um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="5dce1-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="5dce1-167">Durante o acompanhamento, esse recurso tentará atribuir uma ID consistente à mesma face enquanto a pessoa se movimenta pela tela, mesmo se for obstruída ou deixar brevemente o quadro.</span><span class="sxs-lookup"><span data-stu-id="5dce1-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5dce1-168">Esses serviços não realizam o reconhecimento facial.</span><span class="sxs-lookup"><span data-stu-id="5dce1-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="5dce1-169">Uma pessoa que sair do enquadramento ou ficar obstruída por muito tempo receberá uma nova ID quando retornar.</span><span class="sxs-lookup"><span data-stu-id="5dce1-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="5dce1-170">**Detecção de emoções**</span><span class="sxs-lookup"><span data-stu-id="5dce1-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="5dce1-171">A Detecção de Emoções é um componente opcional do Face Detection Media Processor que retorna uma análise sobre vários atributos emocionais das faces detectadas, incluindo felicidade, tristeza, medo, irritação e muito mais.</span><span class="sxs-lookup"><span data-stu-id="5dce1-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="5dce1-173">Modo de detecção</span><span class="sxs-lookup"><span data-stu-id="5dce1-173">Detection mode</span></span>
<span data-ttu-id="5dce1-174">Um dos modos a seguir pode ser usado pelo processador:</span><span class="sxs-lookup"><span data-stu-id="5dce1-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="5dce1-175">detecção facial</span><span class="sxs-lookup"><span data-stu-id="5dce1-175">face detection</span></span>
* <span data-ttu-id="5dce1-176">detecção de emoções faciais</span><span class="sxs-lookup"><span data-stu-id="5dce1-176">per face emotion detection</span></span>
* <span data-ttu-id="5dce1-177">detecção de emoção de agregada</span><span class="sxs-lookup"><span data-stu-id="5dce1-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="5dce1-178">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="5dce1-178">Job name</span></span>
<span data-ttu-id="5dce1-179">Um nome amigável que permite identificar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="5dce1-180">[Esse](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o progresso de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5dce1-181">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="5dce1-181">Output file</span></span>
<span data-ttu-id="5dce1-182">Um nome amigável que permite identificar o conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="5dce1-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="5dce1-183">Detector de Movimento em Mídias do Azure</span><span class="sxs-lookup"><span data-stu-id="5dce1-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="5dce1-184">O MP (processador de mídia) **Azure Media Motion Detector** permite a identificação eficiente de seções de interesse em um vídeo longo e rotineiro.</span><span class="sxs-lookup"><span data-stu-id="5dce1-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="5dce1-185">A detecção de movimento pode ser usada em sequências de imagens estáticas para identificar seções do vídeo onde ocorrem movimentos.</span><span class="sxs-lookup"><span data-stu-id="5dce1-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="5dce1-186">Ela gera um arquivo JSON contendo metadados com carimbos de hora e a região delimitadora onde o evento ocorreu.</span><span class="sxs-lookup"><span data-stu-id="5dce1-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="5dce1-187">Essa tecnologia, destinada à segurança de feeds de vídeo, é capaz de categorizar o movimento em eventos relevantes e falsos positivos, como mudanças de iluminação e sombras.</span><span class="sxs-lookup"><span data-stu-id="5dce1-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="5dce1-188">Isso permite a geração de alertas de segurança por meio de feeds da câmera, sem gerar incontáveis eventos irrelevantes, além de permitir também a extração de momentos de interesse dos vídeos de vigilância extremamente longos.</span><span class="sxs-lookup"><span data-stu-id="5dce1-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="5dce1-190">Miniaturas de Vídeo de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="5dce1-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="5dce1-191">Esse processador pode ajudá-lo a criar resumos de vídeos de longa duração com a seleção automática de trechos interessantes do vídeo de origem.</span><span class="sxs-lookup"><span data-stu-id="5dce1-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="5dce1-192">Isso será útil quando você desejar fornecer uma visão geral rápida do que esperar de um vídeo de longa duração.</span><span class="sxs-lookup"><span data-stu-id="5dce1-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="5dce1-193">Para obter informações detalhadas e exemplos, confira [Usar miniaturas de vídeo da Mídia do Azure para criar um resumo de vídeo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="5dce1-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="5dce1-195">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="5dce1-195">Job name</span></span>
<span data-ttu-id="5dce1-196">Um nome amigável que permite identificar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="5dce1-197">[Esse](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o progresso de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="5dce1-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5dce1-198">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="5dce1-198">Output file</span></span>
<span data-ttu-id="5dce1-199">Um nome amigável que permite identificar o conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="5dce1-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5dce1-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dce1-200">Next steps</span></span>
<span data-ttu-id="5dce1-201">Exibir os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="5dce1-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5dce1-202">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="5dce1-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

