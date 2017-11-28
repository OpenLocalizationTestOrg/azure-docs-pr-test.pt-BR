---
title: "Configurar o codificador Elemental Live para enviar uma transmissão ativa de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como configurar o codificador Elemental Live para enviar uma transmissão de taxa de bits única para os canais do AMS que estão habilitados para a codificação ativa."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="40ce5-103">Usar o codificador Elemental Live para enviar uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="40ce5-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40ce5-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="40ce5-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="40ce5-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="40ce5-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="40ce5-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="40ce5-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="40ce5-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="40ce5-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="40ce5-108">Este tópico mostra como configurar o codificador [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) para enviar uma transmissão de taxa de bits única para os canais do AMS que estão habilitados para a codificação ativa.</span><span class="sxs-lookup"><span data-stu-id="40ce5-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="40ce5-109">Para obter mais informações, consulte [trabalhando com canais habilitados a executar codificação ativa com os Serviços de Mídia do Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="40ce5-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="40ce5-110">Este tutorial mostra como gerenciar o AMS (Serviços de Mídia do Azure) com a ferramenta AMSE (Gerenciador de Serviços de Mídia da Azure).</span><span class="sxs-lookup"><span data-stu-id="40ce5-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="40ce5-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="40ce5-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="40ce5-112">Se você estiver no Mac ou Linux, use o portal do Azure para criar [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="40ce5-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40ce5-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="40ce5-113">Prerequisites</span></span>
* <span data-ttu-id="40ce5-114">Deve ter um conhecimento prático de uso da interface Web do Elemental Live para criar eventos ativos.</span><span class="sxs-lookup"><span data-stu-id="40ce5-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="40ce5-115">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="40ce5-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="40ce5-116">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="40ce5-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="40ce5-117">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="40ce5-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="40ce5-118">Instale a versão mais recente da ferramenta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="40ce5-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="40ce5-119">Inicie a ferramenta e conecte-se à sua conta do AMS.</span><span class="sxs-lookup"><span data-stu-id="40ce5-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="40ce5-120">Dicas</span><span class="sxs-lookup"><span data-stu-id="40ce5-120">Tips</span></span>
* <span data-ttu-id="40ce5-121">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="40ce5-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="40ce5-122">Uma boa regra geral ao determinar os requisitos de largura de banda é dobrar as taxas de bits de transmissão.</span><span class="sxs-lookup"><span data-stu-id="40ce5-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="40ce5-123">Embora isso não seja um requisito obrigatório, isso ajuda a reduzir o impacto do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="40ce5-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="40ce5-124">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="40ce5-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="40ce5-125">Elemental Live com ingestão de RTP</span><span class="sxs-lookup"><span data-stu-id="40ce5-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="40ce5-126">Esta seção mostra como configurar um codificador Elemental Live que faz uma transmissão ao vivo de taxa de bits única através de RTP.</span><span class="sxs-lookup"><span data-stu-id="40ce5-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="40ce5-127">Para saber mais, consulte [Fluxo MPEG TS por RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="40ce5-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="40ce5-128">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="40ce5-128">Create a channel</span></span>

1. <span data-ttu-id="40ce5-129">Na ferramenta AMSE, navegue até a guia **Ao Vivo** e clique com o botão direito do mouse na área de canais.</span><span class="sxs-lookup"><span data-stu-id="40ce5-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="40ce5-130">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="40ce5-130">Select **Create channel…**</span></span> <span data-ttu-id="40ce5-131">no menu.</span><span class="sxs-lookup"><span data-stu-id="40ce5-131">from the menu.</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="40ce5-133">Especifique um nome de canal; o campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="40ce5-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="40ce5-134">Em Configurações de Canal, selecione **Padrão** para a opção de Codificação Ativa, com o Protocolo de Entrada definido como **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="40ce5-135">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="40ce5-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="40ce5-136">Verifique se a opção **Iniciar o novo canal agora** está marcada.</span><span class="sxs-lookup"><span data-stu-id="40ce5-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="40ce5-137">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-137">Click **Create Channel**.</span></span>

   ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="40ce5-139">O canal pode levar até 20 minutos para ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="40ce5-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="40ce5-140">Enquanto o canal é iniciado, você pode [configurar o codificador](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="40ce5-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40ce5-141">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="40ce5-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="40ce5-142">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="40ce5-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="40ce5-143"><a id=configure_elemental_rtp></a>Configurar o codificador do Elemental Live</span><span class="sxs-lookup"><span data-stu-id="40ce5-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="40ce5-144">Neste tutorial, são usadas as configurações de saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="40ce5-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="40ce5-145">O restante desta seção descreve as etapas de configuração mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="40ce5-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="40ce5-146">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="40ce5-146">**Video**:</span></span>

* <span data-ttu-id="40ce5-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="40ce5-147">Codec: H.264</span></span>
* <span data-ttu-id="40ce5-148">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="40ce5-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="40ce5-149">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="40ce5-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="40ce5-150">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="40ce5-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="40ce5-151">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="40ce5-151">Frame Rate: 30</span></span>

<span data-ttu-id="40ce5-152">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="40ce5-152">**Audio**:</span></span>

* <span data-ttu-id="40ce5-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="40ce5-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="40ce5-154">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="40ce5-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="40ce5-155">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="40ce5-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="40ce5-156">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="40ce5-156">Configuration steps</span></span>
1. <span data-ttu-id="40ce5-157">Navegue até a interface Web **Elemental Live** e configure o codificador para transmissão **UDP/TS**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="40ce5-158">Depois de criar um novo evento, role para baixo até os grupos de saída e adicione o grupo de saída **UDP/TS** .</span><span class="sxs-lookup"><span data-stu-id="40ce5-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="40ce5-159">Crie uma nova saída selecionando **Nova Transmissão** e clicando em **Adicionar Saída**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="40ce5-161">É recomendável que o evento Elementar tenha o código de tempo definido como "Relógio do Sistema" para ajudar o codificador a reconectar em caso de falha na transmissão.</span><span class="sxs-lookup"><span data-stu-id="40ce5-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="40ce5-162">Agora que a Saída foi criada, clique em **Adicionar Transmissão**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="40ce5-163">As configurações de saída agora podem ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="40ce5-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="40ce5-164">Role para baixo até a “Transmissão 1” que você acabou de criar, clique na guia **Vídeo** à esquerda e expanda a seção de configurações **Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="40ce5-166">Embora o Elemental Live tenha uma ampla variedade possibilidades de personalização disponíveis, as configurações a seguir são recomendadas para a introdução ao streaming para AMS.</span><span class="sxs-lookup"><span data-stu-id="40ce5-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="40ce5-167">Resolução: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="40ce5-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="40ce5-168">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="40ce5-168">Framerate: 30</span></span>
   * <span data-ttu-id="40ce5-169">Tamanho de GOP: 60 quadros</span><span class="sxs-lookup"><span data-stu-id="40ce5-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="40ce5-170">Modo de entrelaçamento: Progressivo</span><span class="sxs-lookup"><span data-stu-id="40ce5-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="40ce5-171">Taxa de bits: 5000000 bits/s (Isso pode ser ajustado baseado nas limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="40ce5-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="40ce5-173">Obter URL de entrada do canal.</span><span class="sxs-lookup"><span data-stu-id="40ce5-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="40ce5-174">Navegue de volta para a ferramenta AMSE e verifique o status de conclusão do canal.</span><span class="sxs-lookup"><span data-stu-id="40ce5-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="40ce5-175">Depois do Estado ser alterado de **Iniciando** para **Executando**, você poderá obter a URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="40ce5-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="40ce5-176">Quando o canal estiver em execução, clique com o botão direito no nome dele, navegue até parar sobre **Copiar URL de entrada para área de transferência**, em seguida, selecione **URL da Entrada Principal**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="40ce5-178">Cole essas informações no campo **Destino Principal** do Elementar.</span><span class="sxs-lookup"><span data-stu-id="40ce5-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="40ce5-179">Todas as outras configurações podem permanecer como o padrão.</span><span class="sxs-lookup"><span data-stu-id="40ce5-179">All other settings can remain the default.</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="40ce5-181">Para redundância adicional, repita essas etapas com a URL de entrada secundária, criando uma guia separada de "Saída" para Streaming de UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="40ce5-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="40ce5-182">Clique em **Criar** (se um novo evento foi criado) ou **Atualizar** (se estiver editando um evento já existente) e inicie o codificador.</span><span class="sxs-lookup"><span data-stu-id="40ce5-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40ce5-183">Antes de clicar em **Iniciar** na interface Web do Elemental Live, é **necessário** verificar se o Canal está pronto.</span><span class="sxs-lookup"><span data-stu-id="40ce5-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="40ce5-184">Além disso, lembre-se de não deixar o Canal em um estado pronto sem um evento por mais de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="40ce5-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="40ce5-185">Após a transmissão estar em execução por 30 segundos, navegue de volta até a ferramenta AMSE e reproduza o teste.</span><span class="sxs-lookup"><span data-stu-id="40ce5-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="40ce5-186">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="40ce5-186">Test playback</span></span>

<span data-ttu-id="40ce5-187">Navegue até a ferramenta AMSE e clique com botão direito do mouse no canal a ser testado.</span><span class="sxs-lookup"><span data-stu-id="40ce5-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="40ce5-188">No menu, passe o mouse sobre **Reproduzir a Visualização** e selecione **Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="40ce5-189">Se a transmissão for exibida no player, isso significa que o codificador foi corretamente configurado para se conectar ao AMS.</span><span class="sxs-lookup"><span data-stu-id="40ce5-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="40ce5-190">Se um erro for recebido, será necessário redefinir o canal e ajustar as configurações do codificador.</span><span class="sxs-lookup"><span data-stu-id="40ce5-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="40ce5-191">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="40ce5-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="40ce5-192">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="40ce5-192">Create a program</span></span>
1. <span data-ttu-id="40ce5-193">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="40ce5-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="40ce5-194">Na guia **Ativo** na ferramenta AMSE, clique com o botão direito na área do programa e selecione **Criar Novo Programa**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="40ce5-196">Nomeie o programa e, se necessário, ajuste a **Duração da Janela de Arquivo** (cujo padrão é de 4 horas).</span><span class="sxs-lookup"><span data-stu-id="40ce5-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="40ce5-197">Você também pode especificar um local de armazenamento ou deixar como o padrão.</span><span class="sxs-lookup"><span data-stu-id="40ce5-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="40ce5-198">Marque a caixa **Iniciar o Programa agora** .</span><span class="sxs-lookup"><span data-stu-id="40ce5-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="40ce5-199">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="40ce5-200">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="40ce5-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="40ce5-201">Quando o programa estiver em execução, confirme a reprodução clicando com o botão direito do programa e navegando até **Reproduzi o(s) programa(s)**, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="40ce5-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="40ce5-202">Depois de confirmar, clique novamente com botão direito no programa e selecione **Copie a URL de Saída para Área de Transferência** (ou recupere essas informações na opção **Informações e configurações do programa** do menu).</span><span class="sxs-lookup"><span data-stu-id="40ce5-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="40ce5-203">A transmissão agora está pronta para ser inserida em um player ou distribuída para um público para a exibição ao vivo.</span><span class="sxs-lookup"><span data-stu-id="40ce5-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="40ce5-204">solução de problemas</span><span class="sxs-lookup"><span data-stu-id="40ce5-204">Troubleshooting</span></span>
<span data-ttu-id="40ce5-205">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="40ce5-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="40ce5-206">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="40ce5-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="40ce5-207">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="40ce5-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
