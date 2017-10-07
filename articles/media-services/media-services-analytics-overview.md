---
title: "aaaMedia análise na plataforma de serviços de mídia Olá | Microsoft Docs"
description: "Visão geral da versão prévia pública da Análise de Mídia, uma coleção de serviços de fala e de pesquisa visual computacional de nível empresarial, de conformidade, segurança e alcance global"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="8a6a6-103">Análise de mídia na plataforma de serviços de mídia Olá</span><span class="sxs-lookup"><span data-stu-id="8a6a6-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="8a6a6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8a6a6-104">Overview</span></span>
<span data-ttu-id="8a6a6-105">Mais organizações estão usando o vídeo como Olá preferencial tootrain médio seus funcionários, envolver seus clientes e funções de negócios do documento.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="8a6a6-106">Fornece uma maneira toostore, de computação em nuvem de fluxo e acessar esses arquivos de mídia grandes.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="8a6a6-107">Mas à medida que aumenta a biblioteca de uma empresa de conteúdo de vídeo, precisa de uma forma igualmente eficaz de extração de informações de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="8a6a6-108">tooaddress essa necessidade crescente, os serviços de mídia do Azure oferece a análise de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="8a6a6-109">Análise de mídia é uma coleção de componentes de fala e visão que torna mais fácil para as organizações e empresas tooderive de informações práticas de seus arquivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="8a6a6-110">Construído usando componentes de plataforma Olá principais serviços de mídia, análise de mídia pode lidar com processamento em escala em um dia de mídia.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="8a6a6-111">Com a Análise de Mídia, os desenvolvedores podem trazer rapidamente funcionalidades de vídeo avançadas para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="8a6a6-112">Ele fornece os ambientes corporativos escala hello, conformidade, segurança e alcance global exigido por organizações de grandes porte.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="8a6a6-113">Olá diagrama a seguir mostra a análise de mídia e outras partes principais da plataforma de serviços de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![Fluxo de trabalho VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="8a6a6-115">O processador de mídia da Análise de Mídia produz arquivos MP4 ou arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="8a6a6-116">Se um processador de mídia produz um arquivo MP4, você pode baixar progressivamente arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="8a6a6-117">Se um processador de mídia produz um arquivo JSON, você pode baixar o arquivo de saudação do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="8a6a6-118">Serviços de Análise de Mídia</span><span class="sxs-lookup"><span data-stu-id="8a6a6-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="8a6a6-119">Indexador</span><span class="sxs-lookup"><span data-stu-id="8a6a6-119">Indexer</span></span>
<span data-ttu-id="8a6a6-120">Com o Azure Media Indexer, você pode tornar o conteúdo pesquisável e gerar faixas de legendagem.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="8a6a6-121">Versão anterior do toohello comparados, visualização de 2 do indexador de mídia do Azure tem mais ampla e indexação mais rápida de linguagem suporte.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="8a6a6-122">Dentre os idiomas com suporte estão: inglês, espanhol, francês, alemão, italiano, chinês, português e árabe.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="8a6a6-123">Para obter informações detalhadas e exemplos, consulte [Processar vídeos com o Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="8a6a6-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="8a6a6-124">Hyperlapse</span></span>
<span data-ttu-id="8a6a6-125">Microsoft Hyperlapse combina os vídeos lapso de tempo de capacidade rápidos e consumo de toocreate de seu conteúdo de forma longa e estabilização de vídeo.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="8a6a6-126">Além de criar vídeo lapso de tempo, você pode usar Hyperlapse toocreate estáveis vídeos de vídeos shaky capturados por meio de telefones celulares e câmeras.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="8a6a6-127">Para ver informações detalhadas e exemplos, consulte [Arquivos de Mídia do Hyperlapse com o Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="8a6a6-128">Detector de Movimento</span><span class="sxs-lookup"><span data-stu-id="8a6a6-128">Motion Detector</span></span>
<span data-ttu-id="8a6a6-129">Você pode usar o movimento do Detector de movimento toodetect em um vídeo com planos de fundo estáticos.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="8a6a6-130">Isso torna possível toocheck para falsos positivos em eventos de movimento detectados pelo câmeras de vigilância.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="8a6a6-131">Para obter informações detalhadas e exemplos, consulte [Detecção de movimento para Análise de Mídia do Azure](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="8a6a6-132">Detector Facial</span><span class="sxs-lookup"><span data-stu-id="8a6a6-132">Face Detector</span></span>
<span data-ttu-id="8a6a6-133">Usando o Face Detector, é possível detectar as faces das pessoas e suas emoções, incluindo felicidade, tristeza e surpresa.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="8a6a6-134">Isso tem várias aplicações úteis na indústria, descritas abaixo, incluindo agregar e analisar reações de pessoas participando de um evento.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="8a6a6-135">Para obter informações detalhadas e exemplos, consulte [Detecção facial e de emoções da Análise de Mídia do Azure](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="8a6a6-136">Resumo de vídeo</span><span class="sxs-lookup"><span data-stu-id="8a6a6-136">Video summarization</span></span>
<span data-ttu-id="8a6a6-137">Resumo de vídeo pode ajudá-lo a criar resumos dos vídeos longos selecionando automaticamente trechos interessantes de vídeo de origem hello.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="8a6a6-138">Essa capacidade é útil quando você deseja tooprovide uma visão rápida do que tooexpect em um vídeo longo.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="8a6a6-139">Para obter informações detalhadas e exemplos, consulte [resumo de vídeo do uso do Azure Media vídeo miniaturas toocreate](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="8a6a6-140">Reconhecimento de caractere óptico</span><span class="sxs-lookup"><span data-stu-id="8a6a6-140">Optical character recognition</span></span>
<span data-ttu-id="8a6a6-141">O OCR (reconhecimento óptico de caracteres) de Mídia do Azure permite que você converta o conteúdo de texto de arquivos de vídeo em texto digital editável e pesquisável.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="8a6a6-142">Em seguida, você pode automatizar extração Olá de metadados significativo de sinal de vídeo de saudação da sua mídia.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="8a6a6-143">Edição facial escalonável</span><span class="sxs-lookup"><span data-stu-id="8a6a6-143">Scalable face redaction</span></span>
<span data-ttu-id="8a6a6-144">Redactor de mídia do Azure é um processador de mídia de análise de mídia que oferece redação face escalonável na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="8a6a6-145">Usando face redação, você pode modificar seu vídeo tooblur as faces de pessoas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="8a6a6-146">Talvez você queira toouse o serviço de redação Olá face na mídia ou a segurança pública está envolvida.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="8a6a6-147">Alguns minutos do que contém várias faces podem levar horas tooredact manualmente, mas com esse serviço, redação face leva apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="8a6a6-148">Para obter mais informações, consulte Olá [redigir faces com análise de mídia do Azure](media-services-face-redaction.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="8a6a6-149">Cenários comuns</span><span class="sxs-lookup"><span data-stu-id="8a6a6-149">Common scenarios</span></span>
<span data-ttu-id="8a6a6-150">A Análise de Mídia pode ajudar as organizações e empresas a obter novas informações de vídeos e gerenciar grandes volumes de conteúdo de vídeo com mais eficácia.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="8a6a6-151">Veja os diversos cenários a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a6a6-151">Here are several scenarios:</span></span>

* <span data-ttu-id="8a6a6-152">**Call centers**.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-152">**Call centers**.</span></span> <span data-ttu-id="8a6a6-153">Mesmo com o surgimento de saudação de mídia social, call centers de clientes ainda facilitam um grande percentual de transações de atendimento ao cliente.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="8a6a6-154">Codificado nesses dados de áudio é uma grande quantidade de informações do cliente que podem ser analisados tooachieve maior satisfação do cliente.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="8a6a6-155">Usando o Indexador de Mídia, as organizações podem extrair texto e criar índices de pesquisa e painéis.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="8a6a6-156">Em seguida, elas podem extrair inteligência sobre reclamações comuns, fontes de reclamações e outros dados relevantes.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="8a6a6-157">**Moderação de conteúdo gerado pelo usuário**.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-157">**User-generated content moderation**.</span></span> <span data-ttu-id="8a6a6-158">De departamentos de toopolice de tomadas de mídia, muitas organizações têm portais público que aceitam mídia gerado pelo usuário, como imagens e vídeos.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="8a6a6-159">volume de saudação de conteúdo pode ter picos toounexpected eventos de vencimento.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="8a6a6-160">Nesses cenários, é difícil tooconduct revisões de manual eficaz de conteúdo para conveniência.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="8a6a6-161">Os clientes podem depender Olá toofocus de moderação de conteúdo do serviço no conteúdo apropriado.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="8a6a6-162">**Vigilância**.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-162">**Surveillance**.</span></span> <span data-ttu-id="8a6a6-163">Com hello crescimento em uso de câmeras IP é fornecido um inventário crescente de vídeo de vigilância.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="8a6a6-164">Revisar manualmente o vídeo de vigilância é toohuman intensiva e propensas a erro em tempo.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="8a6a6-165">Análise de mídia fornece serviços, como detecção de movimento, detecção de rosto e processo de saudação do Hyperlapse toomake de revisão, gerenciamento e criação de derivados.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="8a6a6-166">Processadores de mídia da Análise de Mídia</span><span class="sxs-lookup"><span data-stu-id="8a6a6-166">Media Analytics media processors</span></span>
<span data-ttu-id="8a6a6-167">Esta seção lista processadores de mídia de análise de mídia de saudação e mostra como toouse .NET ou REST tooget um objeto de processador (MP) de mídia.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="8a6a6-168">Nomes dos MP</span><span class="sxs-lookup"><span data-stu-id="8a6a6-168">MP names</span></span>
* <span data-ttu-id="8a6a6-169">Preview do Indexador de Mídia do Azure 2</span><span class="sxs-lookup"><span data-stu-id="8a6a6-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="8a6a6-170">Indexador de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="8a6a6-170">Azure Media Indexer</span></span>
* <span data-ttu-id="8a6a6-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="8a6a6-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="8a6a6-172">Detector de Rostos em Mídias do Azure</span><span class="sxs-lookup"><span data-stu-id="8a6a6-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="8a6a6-173">Detector de Movimento em Mídias do Azure</span><span class="sxs-lookup"><span data-stu-id="8a6a6-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="8a6a6-174">Miniaturas de Vídeo de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="8a6a6-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="8a6a6-175">OCR de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="8a6a6-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="8a6a6-176">.NET</span><span class="sxs-lookup"><span data-stu-id="8a6a6-176">.NET</span></span>
<span data-ttu-id="8a6a6-177">Olá após a função usa um de saudação especificado MP nomes e retorna um objeto de pacote de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="8a6a6-178">REST</span><span class="sxs-lookup"><span data-stu-id="8a6a6-178">REST</span></span>
<span data-ttu-id="8a6a6-179">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="8a6a6-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="8a6a6-180">Resposta:</span><span class="sxs-lookup"><span data-stu-id="8a6a6-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="8a6a6-181">Demonstrações</span><span class="sxs-lookup"><span data-stu-id="8a6a6-181">Demos</span></span>
<span data-ttu-id="8a6a6-182">Consulte [Demonstrações da Análise de Mídia do Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a6a6-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a6a6-183">Next steps</span></span>
<span data-ttu-id="8a6a6-184">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="8a6a6-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8a6a6-185">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="8a6a6-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="8a6a6-186">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="8a6a6-186">Related articles</span></span>
<span data-ttu-id="8a6a6-187">Consulte o [Comunicado da análise dos Serviços de Mídia](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="8a6a6-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
