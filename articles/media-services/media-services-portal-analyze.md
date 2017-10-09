---
title: "aaaAnalyze sua mídia usando Olá portal do Azure | Microsoft Docs"
description: "Este tópico discute como tooprocess Olá de mídia com processadores de mídia de análise de mídia (MPs) usando o portal do Azure."
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
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="907a9-103">Analisar sua mídia usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="907a9-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="907a9-104">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="907a9-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="907a9-105">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="907a9-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="907a9-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="907a9-106">Overview</span></span>
<span data-ttu-id="907a9-107">Análise de serviços de mídia do Azure é uma coleção de componentes de visão e fala (em escala empresarial, conformidade, segurança e alcance global) que facilitam para organizações e empresas tooderive de informações práticas de seus arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="907a9-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="907a9-108">Para maiores detalhes da Análise de Serviços de Mídia do Azure consulte [esse](media-services-analytics-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="907a9-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="907a9-109">Este tópico discute como tooprocess Olá de mídia com processadores de mídia de análise de mídia (MPs) usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="907a9-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="907a9-110">Os MPs da Análise de Mídia produzem arquivos MP4 ou arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="907a9-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="907a9-111">Se um processador de mídia produziu um arquivo MP4, você pode baixar progressivamente arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="907a9-112">Se um processador de mídia produziu um arquivo JSON, você pode baixar o arquivo de saudação do hello armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="907a9-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="907a9-113">Escolha um ativo que você deseja tooanalyze</span><span class="sxs-lookup"><span data-stu-id="907a9-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="907a9-114">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="907a9-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="907a9-115">Em Olá **configurações** janela, selecione **ativos**.</span><span class="sxs-lookup"><span data-stu-id="907a9-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="907a9-116">.</span><span class="sxs-lookup"><span data-stu-id="907a9-116">.</span></span>
    <span data-ttu-id="907a9-117">![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="907a9-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="907a9-118">Ativo Olá selecione que você gostaria de saudação tooanalyze e pressione **analisar** botão.</span><span class="sxs-lookup"><span data-stu-id="907a9-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="907a9-120">Em Olá **ativo de mídia do processo com análise de mídia** janela, processador Olá select.</span><span class="sxs-lookup"><span data-stu-id="907a9-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="907a9-121">restante de saudação do artigo Olá explica por que e como toouse cada processador.</span><span class="sxs-lookup"><span data-stu-id="907a9-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="907a9-122">Pressione **criar** toohello iniciar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="907a9-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="907a9-123">Indexador de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="907a9-123">Azure Media Indexer</span></span>
<span data-ttu-id="907a9-124">Olá **Azure Media Indexer** processador de mídia permite que você toomake arquivos de mídia e conteúdo pesquisável, bem como gerar faixas de legendas fechadas.</span><span class="sxs-lookup"><span data-stu-id="907a9-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="907a9-125">Esta seção fornece alguns detalhes sobre as opções que você pode especificar para esse MP.</span><span class="sxs-lookup"><span data-stu-id="907a9-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="907a9-127">idioma</span><span class="sxs-lookup"><span data-stu-id="907a9-127">Language</span></span>
<span data-ttu-id="907a9-128">Olá toobe de linguagem natural reconhecido no arquivo de multimídia hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="907a9-129">Por exemplo, inglês ou espanhol.</span><span class="sxs-lookup"><span data-stu-id="907a9-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="907a9-130">Legendas</span><span class="sxs-lookup"><span data-stu-id="907a9-130">Captions</span></span>
<span data-ttu-id="907a9-131">Você pode escolher um formato de legenda que será gerado do seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="907a9-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="907a9-132">Um trabalho de indexação pode gerar arquivos de legenda codificada Olá formatos a seguir:</span><span class="sxs-lookup"><span data-stu-id="907a9-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="907a9-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="907a9-133">**SAMI**</span></span>
* <span data-ttu-id="907a9-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="907a9-134">**TTML**</span></span>
* <span data-ttu-id="907a9-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="907a9-135">**WebVTT**</span></span>

<span data-ttu-id="907a9-136">Arquivos fechados de legenda (CC) nos seguintes formatos podem ser usados toomake áudio e vídeo arquivos toopeople acessível com deficiência auditiva.</span><span class="sxs-lookup"><span data-stu-id="907a9-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="907a9-137">Arquivo AIB</span><span class="sxs-lookup"><span data-stu-id="907a9-137">AIB file</span></span>
<span data-ttu-id="907a9-138">Selecione esta opção se você seria como arquivo de Blob de índice de áudio toogenerate Olá para uso com hello IFilter personalizadas de servidor SQL.</span><span class="sxs-lookup"><span data-stu-id="907a9-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="907a9-139">Para saber mais, confira [este](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="907a9-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="907a9-140">Palavras-chave</span><span class="sxs-lookup"><span data-stu-id="907a9-140">Keywords</span></span>
<span data-ttu-id="907a9-141">Selecione esta opção se você gostaria que toogenerate um arquivo XML de palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="907a9-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="907a9-142">Este arquivo contém palavras-chave extraídas do conteúdo de fala hello, com frequência e a informação de deslocamento.</span><span class="sxs-lookup"><span data-stu-id="907a9-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="907a9-143">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="907a9-143">Job name</span></span>
<span data-ttu-id="907a9-144">Um nome amigável que permite identificar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="907a9-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="907a9-145">[Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="907a9-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="907a9-146">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="907a9-146">Output file</span></span>
<span data-ttu-id="907a9-147">Um nome amigável que permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="907a9-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="907a9-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="907a9-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="907a9-149">O Azure Media Hyperlapse é um MP que cria vídeos suaves de lapso de tempo de conteúdo de primeira pessoa ou de uma câmera de ação.</span><span class="sxs-lookup"><span data-stu-id="907a9-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="907a9-150">Para obter mais informações, consulte [este](media-services-hyperlapse-content.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="907a9-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="907a9-151">Esta seção fornece alguns detalhes sobre as opções que você pode especificar para esse MP.</span><span class="sxs-lookup"><span data-stu-id="907a9-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="907a9-153">Velocidade</span><span class="sxs-lookup"><span data-stu-id="907a9-153">Speed</span></span>
<span data-ttu-id="907a9-154">Especifique a velocidade de saudação com qual toospeed o vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="907a9-155">saída de Hello é uma representação estabilizar e tempo decorrido de vídeo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="907a9-156">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="907a9-156">Job name</span></span>
<span data-ttu-id="907a9-157">Um nome amigável que permite identificar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="907a9-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="907a9-158">[Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="907a9-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="907a9-159">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="907a9-159">Output file</span></span>
<span data-ttu-id="907a9-160">Um nome amigável que permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="907a9-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="907a9-161">Detector de Rostos em Mídias do Azure</span><span class="sxs-lookup"><span data-stu-id="907a9-161">Azure Media Face Detector</span></span>
<span data-ttu-id="907a9-162">Olá **Detector de Face de mídia do Azure** processador de mídia (MP) permite que você toocount, acompanhar movimentos e até mesmo a participação do medidor público e reação via expressões faciais.</span><span class="sxs-lookup"><span data-stu-id="907a9-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="907a9-163">Este serviço contém dois recursos:</span><span class="sxs-lookup"><span data-stu-id="907a9-163">This service contains two features:</span></span> 

* <span data-ttu-id="907a9-164">**Detecção facial**</span><span class="sxs-lookup"><span data-stu-id="907a9-164">**Face detection**</span></span>
  
    <span data-ttu-id="907a9-165">A detecção facial localiza e acompanha as faces humanas em um vídeo.</span><span class="sxs-lookup"><span data-stu-id="907a9-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="907a9-166">Várias faces podem ser detectadas e posteriormente ser controladas à medida que se movimentam, com metadados de hora e o local de saudação retornados em um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="907a9-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="907a9-167">Durante o rastreamento, ele tentará toogive um toohello ID consistente mesmo enfrentam enquanto pessoa Olá é mover-se na tela, mesmo se eles são obstruídos ou deixam brevemente quadro hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="907a9-168">Esses serviços não realizam o reconhecimento facial.</span><span class="sxs-lookup"><span data-stu-id="907a9-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="907a9-169">Uma pessoa que sai do quadro de saudação ou se torna obstruída para muito tempo será fornecida uma nova ID quando elas retornam.</span><span class="sxs-lookup"><span data-stu-id="907a9-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="907a9-170">**Detecção de emoções**</span><span class="sxs-lookup"><span data-stu-id="907a9-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="907a9-171">Detecção de emoção é um componente opcional do hello processador de mídia de detecção de rosto que retorna análise em vários atributos emocionais de faces Olá detectadas, inclusive felicidade, tristeza, medo, irritação e muito mais.</span><span class="sxs-lookup"><span data-stu-id="907a9-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="907a9-173">Modo de detecção</span><span class="sxs-lookup"><span data-stu-id="907a9-173">Detection mode</span></span>
<span data-ttu-id="907a9-174">Uma saudação modos a seguir pode ser usada pelo processador de saudação:</span><span class="sxs-lookup"><span data-stu-id="907a9-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="907a9-175">detecção facial</span><span class="sxs-lookup"><span data-stu-id="907a9-175">face detection</span></span>
* <span data-ttu-id="907a9-176">detecção de emoções faciais</span><span class="sxs-lookup"><span data-stu-id="907a9-176">per face emotion detection</span></span>
* <span data-ttu-id="907a9-177">detecção de emoção de agregada</span><span class="sxs-lookup"><span data-stu-id="907a9-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="907a9-178">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="907a9-178">Job name</span></span>
<span data-ttu-id="907a9-179">Um nome amigável que permite identificar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="907a9-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="907a9-180">[Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="907a9-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="907a9-181">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="907a9-181">Output file</span></span>
<span data-ttu-id="907a9-182">Um nome amigável que permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="907a9-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="907a9-183">Detector de Movimento em Mídias do Azure</span><span class="sxs-lookup"><span data-stu-id="907a9-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="907a9-184">Olá **Detector de movimento de mídia do Azure** habilita (MP) do processador de mídia tooefficiently você identificar seções de interesse em um vídeo de outra forma longa e sem problemas.</span><span class="sxs-lookup"><span data-stu-id="907a9-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="907a9-185">Detecção de movimento pode ser usada em câmera estático filmagens tooidentify seções de vídeo Olá onde ocorre a animação.</span><span class="sxs-lookup"><span data-stu-id="907a9-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="907a9-186">Ele gera um arquivo JSON que contém um metadados com carimbos de hora e hello delimitadora região em que ocorreu o evento hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="907a9-187">Destinado a feeds de vídeo de segurança, essa tecnologia é capaz de toocategorize movimento em eventos relevantes e falsos positivos, como alterações de iluminação e sombras.</span><span class="sxs-lookup"><span data-stu-id="907a9-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="907a9-188">Isso permite toogenerate alertas de segurança de feeds de câmera sem recebam eventos irrelevantes infinito, enquanto estiver sendo momentos tooextract capaz de interesse de vídeos de vigilância muito longos.</span><span class="sxs-lookup"><span data-stu-id="907a9-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="907a9-190">Miniaturas de Vídeo de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="907a9-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="907a9-191">Este processador pode ajudá-lo a criar resumos dos vídeos longos selecionando automaticamente trechos interessantes de vídeo de origem hello.</span><span class="sxs-lookup"><span data-stu-id="907a9-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="907a9-192">Isso é útil quando você deseja tooprovide uma visão rápida do que tooexpect em um vídeo longo.</span><span class="sxs-lookup"><span data-stu-id="907a9-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="907a9-193">Para obter informações detalhadas e exemplos, consulte [tooCreate de uso do Azure Media Video miniaturas um resumo de vídeo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="907a9-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Analisar vídeos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="907a9-195">Nome do trabalho</span><span class="sxs-lookup"><span data-stu-id="907a9-195">Job name</span></span>
<span data-ttu-id="907a9-196">Um nome amigável que permite identificar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="907a9-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="907a9-197">[Isso](media-services-portal-check-job-progress.md) artigo descreve como você pode monitorar o andamento de saudação de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="907a9-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="907a9-198">Arquivo de saída</span><span class="sxs-lookup"><span data-stu-id="907a9-198">Output file</span></span>
<span data-ttu-id="907a9-199">Um nome amigável que permite identificar Olá conteúdo de saída.</span><span class="sxs-lookup"><span data-stu-id="907a9-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="907a9-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="907a9-200">Next steps</span></span>
<span data-ttu-id="907a9-201">Exibir os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="907a9-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="907a9-202">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="907a9-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

