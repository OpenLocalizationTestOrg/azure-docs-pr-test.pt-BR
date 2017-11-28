---
title: "Transmissão ao vivo com codificadores locais usando o portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você nas etapas de criação de um Canal que esteja configurado para uma entrega de passagem."
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
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="a27b5-103">Como executar uma transmissão ao vivo com codificadores locais usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a27b5-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a27b5-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a27b5-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="a27b5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a27b5-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="a27b5-106">REST</span><span class="sxs-lookup"><span data-stu-id="a27b5-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="a27b5-107">Este tutorial orienta você nas etapas de como usar o portal do Azure para criar um **Canal** que é configurado para uma entrega de passagem.</span><span class="sxs-lookup"><span data-stu-id="a27b5-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a27b5-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a27b5-108">Prerequisites</span></span>
<span data-ttu-id="a27b5-109">Os itens a seguir são necessários para concluir o tutorial:</span><span class="sxs-lookup"><span data-stu-id="a27b5-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="a27b5-110">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a27b5-110">An Azure account.</span></span> <span data-ttu-id="a27b5-111">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a27b5-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="a27b5-112">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="a27b5-112">A Media Services account.</span></span> <span data-ttu-id="a27b5-113">Para criar uma conta de Serviços de Mídia, consulte [Como criar uma conta de Serviços de Mídia](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a27b5-114">Uma Webcam.</span><span class="sxs-lookup"><span data-stu-id="a27b5-114">A webcam.</span></span> <span data-ttu-id="a27b5-115">Por exemplo, [Codificador Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="a27b5-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="a27b5-116">É recomendável revisar os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="a27b5-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="a27b5-117">Suporte RTMP dos Serviços de Mídia do Azure e Codificadores Ativos.</span><span class="sxs-lookup"><span data-stu-id="a27b5-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="a27b5-118">Visão geral da transmissão ao vivo usando os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="a27b5-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="a27b5-119">Transmissão ao vivo com codificadores locais que criam fluxos com múltiplas taxas de bits</span><span class="sxs-lookup"><span data-stu-id="a27b5-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="a27b5-120"><a id="scenario"></a>Cenário comum de streaming ao vivo</span><span class="sxs-lookup"><span data-stu-id="a27b5-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="a27b5-121">As etapas a seguir descrevem as tarefas envolvidas na criação de aplicativos comuns de transmissão ao vivo que usam canais configurados para entrega de passagem.</span><span class="sxs-lookup"><span data-stu-id="a27b5-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="a27b5-122">Este tutorial mostra como criar e gerenciar um canal de passagem e eventos ao vivo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="a27b5-123">Verifique se o ponto de extremidade de streaming do qual você deseja transmitir nosso conteúdo está no estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="a27b5-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="a27b5-124">Conecte uma câmera de vídeo a um computador.</span><span class="sxs-lookup"><span data-stu-id="a27b5-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="a27b5-125">Inicie e configure um codificador ao vivo local que gere um fluxo RTMP com múltiplas taxas de bits ou MP4 Fragmentado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="a27b5-126">Para obter mais informações, consulte [Suporte RTMP dos Serviços de Mídia do Azure e Codificadores ao Vivo](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="a27b5-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="a27b5-127">Essa etapa também pode ser realizada após a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="a27b5-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="a27b5-128">Crie e inicie um Canal de passagem.</span><span class="sxs-lookup"><span data-stu-id="a27b5-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="a27b5-129">Recupere a URL de ingestão do canal.</span><span class="sxs-lookup"><span data-stu-id="a27b5-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="a27b5-130">A URL de ingestão é usada pelo codificador ao vivo para enviar o fluxo para o canal.</span><span class="sxs-lookup"><span data-stu-id="a27b5-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="a27b5-131">Recupere a URL de visualização do canal.</span><span class="sxs-lookup"><span data-stu-id="a27b5-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="a27b5-132">Use essa URL para verificar se o canal está recebendo corretamente o fluxo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="a27b5-133">Crie um evento ao vivo/programa.</span><span class="sxs-lookup"><span data-stu-id="a27b5-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="a27b5-134">Ao usar o portal do Azure, a criação de um evento ao vivo também cria um ativo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="a27b5-135">Inicie o evento/programa quando estiver pronto para iniciar a transmissão e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="a27b5-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="a27b5-136">Opcionalmente, o codificador ao vivo pode ser sinalizado para iniciar um anúncio.</span><span class="sxs-lookup"><span data-stu-id="a27b5-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="a27b5-137">O anúncio é inserido no fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="a27b5-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="a27b5-138">Interrompa o evento/programa sempre que você quiser parar a transmissão e o arquivamento do evento.</span><span class="sxs-lookup"><span data-stu-id="a27b5-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="a27b5-139">Exclua o evento/programa (e, opcionalmente, exclua o ativo).</span><span class="sxs-lookup"><span data-stu-id="a27b5-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="a27b5-140">Examine a [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md) para saber mais sobre os conceitos e considerações relacionados à transmissão ao vivo com codificadores locais e canais de passagem.</span><span class="sxs-lookup"><span data-stu-id="a27b5-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="a27b5-141">Para exibir notificações e erros</span><span class="sxs-lookup"><span data-stu-id="a27b5-141">To view notifications and errors</span></span>
<span data-ttu-id="a27b5-142">Se você quiser exibir as notificações e erros produzidos pelo portal do Azure, clique no ícone Notificação.</span><span class="sxs-lookup"><span data-stu-id="a27b5-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Notificações](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="a27b5-144">Criar e iniciar canais de passagem e eventos</span><span class="sxs-lookup"><span data-stu-id="a27b5-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="a27b5-145">Um canal é associado a eventos/programas que permitem que você controle a publicação e o armazenamento de segmentos em um fluxo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="a27b5-146">Os canais gerenciam os eventos.</span><span class="sxs-lookup"><span data-stu-id="a27b5-146">Channels manage events.</span></span> 

<span data-ttu-id="a27b5-147">Você pode especificar o número de horas pelo qual você deseja manter o conteúdo gravado para o programa, definindo a duração da **Janela de Arquivo** .</span><span class="sxs-lookup"><span data-stu-id="a27b5-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="a27b5-148">Esse valor pode ser definido entre um mínimo de 5 minutos e um máximo de 25 horas.</span><span class="sxs-lookup"><span data-stu-id="a27b5-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="a27b5-149">A duração da janela de arquivo também determina que a quantidade máxima de tempo que os clientes podem pesquisar na posição atual em tempo real.</span><span class="sxs-lookup"><span data-stu-id="a27b5-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="a27b5-150">Os eventos podem ser executados no período de tempo especificado, mas o conteúdo que ficar para trás no comprimento da janela será continuamente descartado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="a27b5-151">Esse valor desta propriedade também determina por quanto tempo os manifestos do cliente podem crescer.</span><span class="sxs-lookup"><span data-stu-id="a27b5-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="a27b5-152">Cada evento está associado um ativo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-152">Each event is associated with an asset.</span></span> <span data-ttu-id="a27b5-153">Para publicar o evento, você precisa criar um localizador OnDemand para o ativo associado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="a27b5-154">Ter esse localizador permitirá que você crie uma URL de transmissão que você pode fornecer aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="a27b5-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="a27b5-155">Um canal dá suporte a até três eventos em execução simultânea para que você possa criar diversos arquivos no mesmo fluxo de entrada.</span><span class="sxs-lookup"><span data-stu-id="a27b5-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="a27b5-156">Isso permite que você publique e arquive diferentes partes de um evento, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="a27b5-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="a27b5-157">Por exemplo, o requisito de negócios é arquivar 6 horas de um programa, mas transmitir apenas os últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a27b5-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="a27b5-158">Para fazer isso, você precisa criar dois programas em execução simultânea.</span><span class="sxs-lookup"><span data-stu-id="a27b5-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="a27b5-159">Um programa é definido para arquivar 6 horas do evento, mas o programa não é publicado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="a27b5-160">Outro programa é definido para 10 minutos e esse programa é publicado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="a27b5-161">Você não deve reutilizar os eventos existentes ao vivo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-161">You should not reuse existing live events.</span></span> <span data-ttu-id="a27b5-162">Em vez disso, crie e inicie um novo evento para cada evento.</span><span class="sxs-lookup"><span data-stu-id="a27b5-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="a27b5-163">Inicie o evento quando estiver pronto para começar a transmissão e o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="a27b5-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="a27b5-164">Interrompa o programa sempre que você deseja parar o streaming e o arquivamento do evento.</span><span class="sxs-lookup"><span data-stu-id="a27b5-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="a27b5-165">Para excluir o conteúdo arquivado, interrompa e exclua o evento, em seguida, exclua o ativo associado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="a27b5-166">Não será possível excluir um ativo se este for usado por um evento; o evento deve ser excluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="a27b5-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="a27b5-167">Mesmo depois de você parar e excluir o evento, os usuários poderão transmitir seu conteúdo arquivado como vídeo por demanda enquanto você não excluir o ativo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="a27b5-168">Se desejar manter o conteúdo arquivado mas ele não está disponível para streaming, exclua o localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="a27b5-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="a27b5-169">Para usar o portal para criar um canal</span><span class="sxs-lookup"><span data-stu-id="a27b5-169">To use the portal to create a channel</span></span>
<span data-ttu-id="a27b5-170">Esta seção mostra como usar a opção **Criação Rápida** para criar um canal de passagem.</span><span class="sxs-lookup"><span data-stu-id="a27b5-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="a27b5-171">Para obter mais detalhes sobre os canais de passagem, veja [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="a27b5-172">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="a27b5-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a27b5-173">Na janela **Configurações**, clique em **Transmissão ao vivo**.</span><span class="sxs-lookup"><span data-stu-id="a27b5-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Introdução](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="a27b5-175">A janela **Transmissão ao vivo** é exibida.</span><span class="sxs-lookup"><span data-stu-id="a27b5-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="a27b5-176">Clique em **Criação Rápida** para criar um canal de passagem com o protocolo de ingestão RTMP.</span><span class="sxs-lookup"><span data-stu-id="a27b5-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="a27b5-177">A janela **CRIAR UM NOVO CANAL** é exibida.</span><span class="sxs-lookup"><span data-stu-id="a27b5-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="a27b5-178">Nomeie o novo canal e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a27b5-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="a27b5-179">Isso cria um canal de passagem com o protocolo de ingestão RTMP.</span><span class="sxs-lookup"><span data-stu-id="a27b5-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="a27b5-180">Criar eventos</span><span class="sxs-lookup"><span data-stu-id="a27b5-180">Create events</span></span>
1. <span data-ttu-id="a27b5-181">Selecione um canal para o qual você deseja adicionar um evento.</span><span class="sxs-lookup"><span data-stu-id="a27b5-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="a27b5-182">Pressione o botão **Evento ao Vivo** .</span><span class="sxs-lookup"><span data-stu-id="a27b5-182">Press **Live Event** button.</span></span>

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="a27b5-184">Obter URLs de ingestão</span><span class="sxs-lookup"><span data-stu-id="a27b5-184">Get ingest URLs</span></span>
<span data-ttu-id="a27b5-185">Depois que o canal é criado, você pode obter URLs de ingestão que você fornecerá ao codificador ao vivo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="a27b5-186">O codificador usa essas URLs para gerar entrada de um fluxo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-186">The encoder uses these URLs to input a live stream.</span></span>

![Criado](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="a27b5-188">Assistir ao evento</span><span class="sxs-lookup"><span data-stu-id="a27b5-188">Watch the event</span></span>
<span data-ttu-id="a27b5-189">Para assistir o evento, clique em **Assistir** no portal do Azure ou copie a URL de transmissão e use um player de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="a27b5-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Criado](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="a27b5-191">O evento ao vivo é convertido automaticamente no conteúdo sob demanda quando estiver parado.</span><span class="sxs-lookup"><span data-stu-id="a27b5-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a27b5-192">Limpar</span><span class="sxs-lookup"><span data-stu-id="a27b5-192">Clean up</span></span>
<span data-ttu-id="a27b5-193">Para obter mais detalhes sobre os canais de passagem, veja [Transmissão ao vivo com codificadores locais que criam fluxos de múltiplas taxas de bits](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="a27b5-194">Um canal pode ser interrompido somente quando todos os eventos/programas nele foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="a27b5-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="a27b5-195">Depois que o canal estiver parado, ele não incorrerá em nenhum encargo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="a27b5-196">Quando for necessário iniciá-lo novamente ele terá a mesma URL de ingestão, portanto, você não precisará reconfigurar seu codificador.</span><span class="sxs-lookup"><span data-stu-id="a27b5-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="a27b5-197">Um canal pode ser excluído somente quando todos os eventos ao vivo nele foram excluídos.</span><span class="sxs-lookup"><span data-stu-id="a27b5-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="a27b5-198">Exibir conteúdo arquivado</span><span class="sxs-lookup"><span data-stu-id="a27b5-198">View archived content</span></span>
<span data-ttu-id="a27b5-199">Mesmo depois de você parar e excluir o evento, os usuários poderão transmitir seu conteúdo arquivado como vídeo por demanda enquanto você não excluir o ativo.</span><span class="sxs-lookup"><span data-stu-id="a27b5-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="a27b5-200">Não será possível excluir um ativo se este for usado por um evento; o evento deve ser excluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="a27b5-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="a27b5-201">Para gerenciar os ativos, selecione **Configuração** e clique em **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="a27b5-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![Ativos](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="a27b5-203">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="a27b5-203">Next step</span></span>
<span data-ttu-id="a27b5-204">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="a27b5-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a27b5-205">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a27b5-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

