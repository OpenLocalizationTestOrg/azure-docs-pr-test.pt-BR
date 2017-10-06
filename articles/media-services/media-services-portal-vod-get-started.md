---
title: "aaaGet iniciado com fornecendo VoD usando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação da implementação de um serviço básico de fornecimento de conteúdo de vídeo sob demanda (VoD) com o aplicativo de serviços de mídia do Azure (AMS) usando Olá portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="2da8a-103">Introdução ao fornecimento de conteúdo sob demanda usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2da8a-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="2da8a-104">Este tutorial orienta você pelas etapas de saudação da implementação de um serviço básico de fornecimento de conteúdo de vídeo sob demanda (VoD) com o aplicativo de serviços de mídia do Azure (AMS) usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2da8a-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2da8a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2da8a-105">Prerequisites</span></span>
<span data-ttu-id="2da8a-106">Olá seguem tutorial de saudação toocomplete necessária:</span><span class="sxs-lookup"><span data-stu-id="2da8a-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="2da8a-107">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="2da8a-107">An Azure account.</span></span> <span data-ttu-id="2da8a-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2da8a-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="2da8a-109">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="2da8a-109">A Media Services account.</span></span> <span data-ttu-id="2da8a-110">toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="2da8a-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="2da8a-111">Este tutorial inclui Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2da8a-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="2da8a-112">Iniciar ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="2da8a-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="2da8a-113">Carregar um arquivo de vídeo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-113">Upload a video file.</span></span>
3. <span data-ttu-id="2da8a-114">Codifica o arquivo de origem de saudação em um conjunto de arquivos MP4 com taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="2da8a-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="2da8a-115">Publica ativo hello e get streaming e URLs de download progressivo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="2da8a-116">Reproduzir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="2da8a-117">Iniciar pontos de extremidade de streaming</span><span class="sxs-lookup"><span data-stu-id="2da8a-117">Start streaming endpoints</span></span> 

<span data-ttu-id="2da8a-118">Ao trabalhar com o Azure Media Services, um dos cenários mais comuns de saudação está entregando vídeo por meio de streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="2da8a-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="2da8a-119">Serviços de mídia fornecem empacotamento dinâmico, que permite que você toodeliver sua taxa de bits adaptável MP4 codificados conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, sem a necessidade de toostore pacote predefinido versões de cada um desses formatos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="2da8a-120">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="2da8a-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="2da8a-121">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="2da8a-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="2da8a-122">toostart Olá ponto de extremidade de streaming, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2da8a-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="2da8a-123">Faça logon em Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2da8a-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2da8a-124">Na janela de configurações de saudação, clique em pontos de extremidade de Streaming.</span><span class="sxs-lookup"><span data-stu-id="2da8a-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="2da8a-125">Clique em padrão Olá ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="2da8a-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="2da8a-126">saudação padrão detalhes do ponto de EXTREMIDADE de STREAMING de janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="2da8a-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="2da8a-127">Clique o ícone de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="2da8a-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="2da8a-128">Clique em Olá toosave de botão de salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="2da8a-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="2da8a-129">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="2da8a-129">Upload files</span></span>
<span data-ttu-id="2da8a-130">toostream vídeos usando serviços de mídia do Azure, você precisa de vídeos de origem do tooupload hello, codificá-los em várias taxas de bits e publicar resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2da8a-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="2da8a-131">primeira etapa de saudação é abordada nesta seção.</span><span class="sxs-lookup"><span data-stu-id="2da8a-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="2da8a-132">Em Olá **configuração** janela, clique em **ativos**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Carregar arquivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="2da8a-134">Clique em Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="2da8a-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="2da8a-135">Olá **carregar um ativo de vídeo** janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="2da8a-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2da8a-136">Não há nenhuma limitação de tamanho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="2da8a-137">Procurar vídeo toohello desejado no seu computador, selecioná-la e Okey de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="2da8a-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="2da8a-138">Olá upload é iniciado e você pode ver o progresso de saudação em nome do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2da8a-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="2da8a-139">Após a conclusão do carregamento de saudação, você ver novo ativo de saudação listado no hello **ativos** janela.</span><span class="sxs-lookup"><span data-stu-id="2da8a-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="2da8a-140">Codificar ativos</span><span class="sxs-lookup"><span data-stu-id="2da8a-140">Encode assets</span></span>

<span data-ttu-id="2da8a-141">Ao trabalhar com um dos cenários mais comuns de saudação está entregando uma taxa de bits adaptável streaming tooyour clientes de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="2da8a-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="2da8a-142">Serviços de mídia oferece suporte a saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="2da8a-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="2da8a-143">tooprepare vídeos para streaming de taxa de bits adaptável, você precisa tooencode sua fonte de vídeo em arquivos de várias taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="2da8a-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="2da8a-144">Você deve usar o hello **codificador de mídia padrão** tooencode codificador seus vídeos.</span><span class="sxs-lookup"><span data-stu-id="2da8a-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="2da8a-145">Serviços de mídia também fornecem empacotamento dinâmico, que permite que você toodeliver seus MP4s de múltiplas taxas de bits nos seguintes formatos de streaming de saudação: MPEG DASH, HLS, Smooth Streaming, sem a necessidade de toorepackage nesses formatos de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="2da8a-146">Com o empacotamento dinâmico, você só precisa toostore e pagamento para arquivos de saudação em único formato de armazenamento e os serviços de mídia cria e serve a resposta apropriada hello, com base nas solicitações de um cliente.</span><span class="sxs-lookup"><span data-stu-id="2da8a-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="2da8a-147">tootake proveito do empacotamento dinâmico, você precisa de tooencode seu arquivo de origem em um conjunto de arquivos MP4 com múltiplas taxas de bits (etapas de codificação Olá são demonstradas posteriormente nesta seção).</span><span class="sxs-lookup"><span data-stu-id="2da8a-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="2da8a-148">toouse Olá portal tooencode</span><span class="sxs-lookup"><span data-stu-id="2da8a-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="2da8a-149">Esta seção descreve Olá etapas tooencode seu conteúdo com o codificador de mídia padrão.</span><span class="sxs-lookup"><span data-stu-id="2da8a-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="2da8a-150">Em Olá **configurações** janela, selecione **ativos**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="2da8a-151">Em Olá **ativos** janela, ativo Olá selecione que você gostaria que tooencode.</span><span class="sxs-lookup"><span data-stu-id="2da8a-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="2da8a-152">Olá pressione **Encode** botão.</span><span class="sxs-lookup"><span data-stu-id="2da8a-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="2da8a-153">Em Olá **codificar um ativo** janela, processador "Padrão de codificador de mídia" hello select e uma predefinição.</span><span class="sxs-lookup"><span data-stu-id="2da8a-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="2da8a-154">Para saber mais sobre as predefinições, confira [Gerar automaticamente uma escada de taxa de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de tarefa para MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2da8a-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="2da8a-155">Se você planejar toocontrol quais predefinição de codificação é usada, lembre-se disso: é importante tooselect Olá predefinição mais apropriado para o vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="2da8a-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="2da8a-156">Por exemplo, se você souber o vídeo de entrada com uma resolução de 1920 x 1080 pixels, você pode usar hello "H264 taxas de bits múltiplas 1080p" predefinido.</span><span class="sxs-lookup"><span data-stu-id="2da8a-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="2da8a-157">Se você tiver um vídeo de baixa resolução (640 x 360), não deverá usar a predefinição "H264 Múltiplas Taxas de Bits 1080p".</span><span class="sxs-lookup"><span data-stu-id="2da8a-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="2da8a-158">Para facilitar o gerenciamento, você tem uma opção da edição nome Olá Olá ativo de saída e o nome de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2da8a-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificar ativos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="2da8a-160">Pressione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="2da8a-161">Monitorar o andamento do trabalho de codificação</span><span class="sxs-lookup"><span data-stu-id="2da8a-161">Monitor encoding job progress</span></span>
<span data-ttu-id="2da8a-162">progresso de saudação toomonitor de saudação codificação de trabalho, clique em **configurações** (na parte superior de saudação da página de saudação) e, em seguida, selecione **trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Trabalhos](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="2da8a-164">Publicar conteúdo</span><span class="sxs-lookup"><span data-stu-id="2da8a-164">Publish content</span></span>
<span data-ttu-id="2da8a-165">tooprovide o usuário com uma URL que pode ser usado toostream ou baixar o conteúdo, você primeiro precisa muito "Publicar" seu ativo, criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="2da8a-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="2da8a-166">Os localizadores fornecem acesso toofiles contidos em Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="2da8a-167">Os Serviços de Mídia oferecem suporte a dois tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="2da8a-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="2da8a-168">Transmitindo os localizadores (OnDemandOrigin), usados para streaming adaptável (por exemplo, toostream MPEG DASH, HLS ou Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="2da8a-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="2da8a-169">toocreate um localizador de transmissão seu ativo deve conter um arquivo. ISM.</span><span class="sxs-lookup"><span data-stu-id="2da8a-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="2da8a-170">Localizadores progressivos (SAS), usados para a entrega de vídeo por meio do download progressivo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="2da8a-171">Uma URL de streaming tem Olá formato a seguir e você pode usá-lo tooplay ativos do Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2da8a-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="2da8a-172">Acrescentar toobuild uma URL de streaming de HLS (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="2da8a-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="2da8a-173">Acrescentar toobuild um MPEG DASH URL de streaming (formato = mpd-tempo-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="2da8a-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="2da8a-174">Uma URL SAS tem Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="2da8a-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="2da8a-175">Se você usou os localizadores de portal toocreate Olá antes de março de 2015, os localizadores com uma data de validade de dois anos foram criados.</span><span class="sxs-lookup"><span data-stu-id="2da8a-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="2da8a-176">tooupdate uma data de expiração em um localizador, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) ou [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span><span class="sxs-lookup"><span data-stu-id="2da8a-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="2da8a-177">Quando você atualizar a data de expiração de saudação de um localizador SAS, Olá URL é alterado.</span><span class="sxs-lookup"><span data-stu-id="2da8a-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="2da8a-178">toouse de saudação portal toopublish um ativo</span><span class="sxs-lookup"><span data-stu-id="2da8a-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="2da8a-179">toouse de saudação portal toopublish um ativo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2da8a-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="2da8a-180">Selecione **Configurações** > **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="2da8a-181">Selecione Olá ativo que você deseja toopublish.</span><span class="sxs-lookup"><span data-stu-id="2da8a-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="2da8a-182">Clique em Olá **publicar** botão.</span><span class="sxs-lookup"><span data-stu-id="2da8a-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="2da8a-183">Selecione o tipo de localizador de saudação.</span><span class="sxs-lookup"><span data-stu-id="2da8a-183">Select hello locator type.</span></span>
5. <span data-ttu-id="2da8a-184">Pressione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-184">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="2da8a-186">Olá URL é adicionado a lista toohello de **publicado URLs**.</span><span class="sxs-lookup"><span data-stu-id="2da8a-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="2da8a-187">Reproduzir conteúdo do portal de saudação</span><span class="sxs-lookup"><span data-stu-id="2da8a-187">Play content from hello portal</span></span>
<span data-ttu-id="2da8a-188">Olá, portal do Azure fornece um player de conteúdo que você pode usar tootest o vídeo.</span><span class="sxs-lookup"><span data-stu-id="2da8a-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="2da8a-189">Clique em vídeo Olá desejado e clique em Olá **reproduzir** botão.</span><span class="sxs-lookup"><span data-stu-id="2da8a-189">Click hello desired video and then click hello **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="2da8a-191">Algumas considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="2da8a-191">Some considerations apply:</span></span>

* <span data-ttu-id="2da8a-192">toobegin streaming, iniciar execução Olá **padrão** ponto de extremidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="2da8a-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="2da8a-193">Certifique-se de saudação vídeo foi publicada.</span><span class="sxs-lookup"><span data-stu-id="2da8a-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="2da8a-194">Isso **Media player** reproduz do ponto de extremidade de streaming de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2da8a-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="2da8a-195">Se você quiser tooplay de não-padrão streaming de ponto de extremidade, clique toocopy Olá URL e use outro player.</span><span class="sxs-lookup"><span data-stu-id="2da8a-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="2da8a-196">Por exemplo, o [Player dos Serviços de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="2da8a-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2da8a-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2da8a-197">Next steps</span></span>
<span data-ttu-id="2da8a-198">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="2da8a-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2da8a-199">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="2da8a-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

