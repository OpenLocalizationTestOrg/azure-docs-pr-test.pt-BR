---
title: "fluxo de aaaLive com codificadores locais usando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de criação de um canal que está configurado para uma entrega de passagem."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="4fc8f-103">Como tooperform a transmissão ao vivo com local codificadores usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4fc8f-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fc8f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4fc8f-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="4fc8f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4fc8f-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="4fc8f-106">REST</span><span class="sxs-lookup"><span data-stu-id="4fc8f-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="4fc8f-107">Este tutorial orienta você pelas etapas de saudação do uso de saudação toocreate portal do Azure uma **Channel** que está configurado para uma entrega de passagem.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4fc8f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4fc8f-108">Prerequisites</span></span>
<span data-ttu-id="4fc8f-109">Olá seguem tutorial de saudação toocomplete necessária:</span><span class="sxs-lookup"><span data-stu-id="4fc8f-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="4fc8f-110">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-110">An Azure account.</span></span> <span data-ttu-id="4fc8f-111">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="4fc8f-112">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-112">A Media Services account.</span></span> <span data-ttu-id="4fc8f-113">toocreate uma conta de serviços de mídia, consulte [como tooCreate uma conta do Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="4fc8f-114">Uma Webcam.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-114">A webcam.</span></span> <span data-ttu-id="4fc8f-115">Por exemplo, [Codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="4fc8f-116">É altamente recomendável Olá tooreview artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fc8f-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="4fc8f-117">Suporte RTMP dos Serviços de Mídia do Azure e Codificadores Ativos.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="4fc8f-118">Visão geral da transmissão ao vivo usando os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="4fc8f-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="4fc8f-119">Transmissão ao vivo com codificadores locais que criam fluxos com múltiplas taxas de bits</span><span class="sxs-lookup"><span data-stu-id="4fc8f-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="4fc8f-120"><a id="scenario"></a>Cenário comum de streaming ao vivo</span><span class="sxs-lookup"><span data-stu-id="4fc8f-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="4fc8f-121">Olá, etapas a seguir descrevem tarefas envolvidas na criação comuns aplicativos de transmissão ao vivo que usam canais que são configurados para entrega de passagem.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="4fc8f-122">Este tutorial mostra como toocreate e gerenciar um canal de passagem e eventos ao vivo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="4fc8f-123">Certifique-se de saudação streaming do qual você deseja que o conteúdo de toostream de ponto de extremidade está em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="4fc8f-124">Conecte um computador de tooa de câmera de vídeo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="4fc8f-125">Inicie e configure um codificador ao vivo local que gere um fluxo RTMP com múltiplas taxas de bits ou MP4 Fragmentado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="4fc8f-126">Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="4fc8f-127">Essa etapa também pode ser realizada após a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="4fc8f-128">Crie e inicie um Canal de passagem.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="4fc8f-129">URL de ingestão recuperar Olá canal.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="4fc8f-130">URL de ingestão Olá é usado pelo Olá codificador ao vivo toosend Olá fluxo toohello canal.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="4fc8f-131">Recupere a URL de visualização do canal hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="4fc8f-132">Use este tooverify URL que o canal está recebendo corretamente transmissão ao vivo hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="4fc8f-133">Crie um evento ao vivo/programa.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="4fc8f-134">Quando usar hello portal do Azure, criar um evento ao vivo também cria um ativo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="4fc8f-135">Inicie programa da evento hello quando você estiver pronto toostart transmissão e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="4fc8f-136">Opcionalmente, o codificador ao vivo Olá pode ser sinalizado toostart um anúncio.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="4fc8f-137">anúncio de saudação é inserido no fluxo de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="4fc8f-138">Pare Olá evento/programa sempre que quiser toostop streaming e arquivamento evento hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="4fc8f-139">Excluir o programa da evento hello (e opcionalmente exclua o ativo de saudação).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="4fc8f-140">Examine [transmissão ao vivo com codificadores locais que criam fluxos de várias taxas de bits](media-services-live-streaming-with-onprem-encoders.md) toolearn sobre conceitos e considerações relacionadas streaming toolive com codificadores locais e canais de passagem.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="4fc8f-141">erros e tooview notificações</span><span class="sxs-lookup"><span data-stu-id="4fc8f-141">tooview notifications and errors</span></span>
<span data-ttu-id="4fc8f-142">Se você quiser tooview notificações e os erros produzidos por Olá portal do Azure, clique no ícone de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Notificações](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="4fc8f-144">Criar e iniciar canais de passagem e eventos</span><span class="sxs-lookup"><span data-stu-id="4fc8f-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="4fc8f-145">Um canal é associado a eventos/programas que permitem a publicação de saudação toocontrol e armazenamento de segmentos em uma transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="4fc8f-146">Os canais gerenciam os eventos.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-146">Channels manage events.</span></span> 

<span data-ttu-id="4fc8f-147">Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para programa hello por configuração Olá **janela de arquivo** comprimento.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="4fc8f-148">Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="4fc8f-149">Duração da janela de arquivo também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="4fc8f-150">Eventos podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="4fc8f-151">Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="4fc8f-152">Cada evento está associado um ativo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-152">Each event is associated with an asset.</span></span> <span data-ttu-id="4fc8f-153">evento de saudação toopublish, você deve criar um localizador OnDemand para ativo Olá associado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="4fc8f-154">Ter esse localizador permite toobuild uma URL de streaming que pode fornecer tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="4fc8f-155">Um canal dá suporte para até toothree em execução simultaneamente eventos para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="4fc8f-156">Isso permite que você toopublish e arquivamento diferentes partes de um evento, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="4fc8f-157">Por exemplo, o requisito de negócios é tooarchive 6 horas de um programa, mas toobroadcast apenas últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="4fc8f-158">tooaccomplish isso, você precisa toocreate dois programas em execução simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="4fc8f-159">Um programa está definido tooarchive 6 horas do evento Olá mas Olá programa não será publicado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="4fc8f-160">Olá outro programa é tooarchive conjunto por 10 minutos e esse programa é publicado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="4fc8f-161">Você não deve reutilizar os eventos existentes ao vivo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-161">You should not reuse existing live events.</span></span> <span data-ttu-id="4fc8f-162">Em vez disso, crie e inicie um novo evento para cada evento.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="4fc8f-163">Inicie o evento hello quando você estiver pronto toostart transmissão e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="4fc8f-164">Pare o programa de saudação sempre que quiser toostop streaming e arquivamento evento hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="4fc8f-165">conteúdo toodelete arquivado, parar e excluir o evento hello e exclua ativo associado hello.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="4fc8f-166">Um ativo não pode ser excluído se ele é usado por um evento; evento Olá deve ser excluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="4fc8f-167">Mesmo depois de parar e excluir o evento hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="4fc8f-168">Se você deseja tooretain Olá arquivado conteúdo, mas não tem disponível para streaming, exclua Olá localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="4fc8f-169">toouse de saudação portal toocreate um canal</span><span class="sxs-lookup"><span data-stu-id="4fc8f-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="4fc8f-170">Esta seção mostra como Olá toouse **criação rápida** opção toocreate um canal de passagem.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="4fc8f-171">Para obter mais detalhes sobre os canais de passagem, veja [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="4fc8f-172">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="4fc8f-173">Em Olá **configurações** janela, clique em **transmissão ao vivo**.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Introdução](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="4fc8f-175">Olá **transmissão ao vivo** janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="4fc8f-176">Clique em **criação rápida** toocreate um canal de passagem com hello RTMP de protocolo de ingestão.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="4fc8f-177">Olá **criar um novo canal** janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="4fc8f-178">Dê um nome de canal novo hello e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="4fc8f-179">Isso cria um canal de passagem com hello protocolo de ingestão RTMP.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="4fc8f-180">Criar eventos</span><span class="sxs-lookup"><span data-stu-id="4fc8f-180">Create events</span></span>
1. <span data-ttu-id="4fc8f-181">Selecione um toowhich de canal que você deseja tooadd um evento.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="4fc8f-182">Pressione o botão **Evento ao Vivo** .</span><span class="sxs-lookup"><span data-stu-id="4fc8f-182">Press **Live Event** button.</span></span>

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="4fc8f-184">Obter URLs de ingestão</span><span class="sxs-lookup"><span data-stu-id="4fc8f-184">Get ingest URLs</span></span>
<span data-ttu-id="4fc8f-185">Depois que o canal de saudação é criado, você pode obter URLs que você fornecerá o codificador ao vivo toohello de ingestão.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="4fc8f-186">codificador de saudação usa tooinput essas URLs uma transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Criado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="4fc8f-188">Evento de saudação de inspeção</span><span class="sxs-lookup"><span data-stu-id="4fc8f-188">Watch hello event</span></span>
<span data-ttu-id="4fc8f-189">evento de saudação toowatch, clique em **inspecionar** Olá Olá do Azure do portal ou Copiar URL de streaming e usar um player de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Criado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="4fc8f-191">Evento ao vivo automaticamente obter conteúdo de demanda tooon convertido quando parado.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="4fc8f-192">Limpar</span><span class="sxs-lookup"><span data-stu-id="4fc8f-192">Clean up</span></span>
<span data-ttu-id="4fc8f-193">Para obter mais detalhes sobre os canais de passagem, veja [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="4fc8f-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="4fc8f-194">Um canal pode ser interrompido somente quando todos os eventos/programas no canal Olá foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="4fc8f-195">Depois que o canal de saudação for interrompido, ele não incorrerá em todos os encargos.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="4fc8f-196">Quando você precisar toostart-lo novamente, ele terá hello mesma URL de ingestão para que você não precise tooreconfigure seu codificador.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="4fc8f-197">Um canal pode ser excluído somente quando todos os eventos ao vivo no canal Olá tem sido excluídos.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="4fc8f-198">Exibir conteúdo arquivado</span><span class="sxs-lookup"><span data-stu-id="4fc8f-198">View archived content</span></span>
<span data-ttu-id="4fc8f-199">Mesmo depois de parar e excluir o evento hello, Olá usuários seria capaz de toostream seu conteúdo arquivado como um vídeo sob demanda, para desde que você não excluir Olá ativo.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="4fc8f-200">Um ativo não pode ser excluído se ele é usado por um evento; evento Olá deve ser excluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="4fc8f-201">Selecione de seus ativos, toomanage **configuração** e clique em **ativos**.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Ativos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="4fc8f-203">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="4fc8f-203">Next step</span></span>
<span data-ttu-id="4fc8f-204">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="4fc8f-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fc8f-205">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4fc8f-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

