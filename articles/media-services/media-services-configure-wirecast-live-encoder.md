---
title: "Configurar o codificador Telestream Wirecast para enviar uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como configurar o codificador ativo Wirecast para enviar uma transmissão de taxa de bits única para os canais do AMS que estão habilitados para a codificação ativa. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="1f0fb-103">Usar o codificador Wirecast para enviar uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="1f0fb-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f0fb-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="1f0fb-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="1f0fb-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="1f0fb-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="1f0fb-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="1f0fb-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="1f0fb-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="1f0fb-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="1f0fb-108">Este tópico mostra como configurar o codificador ativo [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) para enviar uma transmissão de taxa de bits única para os canais do AMS que estão habilitados para a codificação ativa.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="1f0fb-109">Para obter mais informações, consulte [Trabalhando com canais habilitados para executar codificação ao vivo com os Serviços de Mídia do Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="1f0fb-110">Este tutorial mostra como gerenciar o AMS (Serviços de Mídia do Azure) com a ferramenta AMSE (Gerenciador de Serviços de Mídia da Azure).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="1f0fb-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="1f0fb-112">Se você estiver no Mac ou Linux, use o portal do Azure para criar [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f0fb-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f0fb-113">Prerequisites</span></span>
* [<span data-ttu-id="1f0fb-114">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="1f0fb-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="1f0fb-115">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="1f0fb-116">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="1f0fb-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="1f0fb-117">Instale a versão mais recente da ferramenta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="1f0fb-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="1f0fb-118">Inicie a ferramenta e conecte-se à sua conta do AMS.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="1f0fb-119">Dicas</span><span class="sxs-lookup"><span data-stu-id="1f0fb-119">Tips</span></span>
* <span data-ttu-id="1f0fb-120">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="1f0fb-121">Uma boa regra geral ao determinar os requisitos de largura de banda é dobrar as taxas de bits de transmissão.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="1f0fb-122">Embora isso não seja um requisito obrigatório, isso ajuda a reduzir o impacto do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="1f0fb-123">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="1f0fb-124">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="1f0fb-124">Create a channel</span></span>
1. <span data-ttu-id="1f0fb-125">Na ferramenta AMSE, navegue até a guia **Ao Vivo** e clique com o botão direito do mouse na área de canais.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="1f0fb-126">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="1f0fb-126">Select **Create channel…**</span></span> <span data-ttu-id="1f0fb-127">no menu.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-127">from the menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="1f0fb-129">Especifique um nome de canal; o campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="1f0fb-130">Nas Configurações do Canal, selecione **Standard** para a opção Codificação Ativa, com o Protocolo de Entrada definido para **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="1f0fb-131">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="1f0fb-132">Verifique se a opção **Iniciar o novo canal agora** está marcada.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="1f0fb-133">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="1f0fb-135">O canal pode levar até 20 minutos para ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="1f0fb-136">Enquanto o canal é iniciado, você pode [configurar o codificador](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f0fb-137">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="1f0fb-138">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="1f0fb-139"><a id=configure_wirecast_rtmp></a>Configurar o codificador do Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="1f0fb-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="1f0fb-140">Neste tutorial, são usadas as configurações de saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="1f0fb-141">O restante desta seção descreve as etapas de configuração mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="1f0fb-142">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="1f0fb-142">**Video**:</span></span>

* <span data-ttu-id="1f0fb-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="1f0fb-143">Codec: H.264</span></span>
* <span data-ttu-id="1f0fb-144">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="1f0fb-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="1f0fb-145">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="1f0fb-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="1f0fb-146">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="1f0fb-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="1f0fb-147">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="1f0fb-147">Frame Rate: 30</span></span>

<span data-ttu-id="1f0fb-148">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="1f0fb-148">**Audio**:</span></span>

* <span data-ttu-id="1f0fb-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="1f0fb-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="1f0fb-150">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="1f0fb-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="1f0fb-151">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="1f0fb-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="1f0fb-152">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="1f0fb-152">Configuration steps</span></span>
1. <span data-ttu-id="1f0fb-153">Abra o aplicativo do Telestream Wirecast no computador que está sendo usado e configure a transmissão RTMP.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="1f0fb-154">Configure a saída navegando até a guia **Saída** e selecionando **Configurações de Saída...**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="1f0fb-155">Certifique-se de que o **Destino de Saída** está definido como **Servidor RTMP**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="1f0fb-156">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-156">Click **OK**.</span></span>
4. <span data-ttu-id="1f0fb-157">Na página de configurações, defina o campo **Destino** como **Serviços de Mídia do Azure**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="1f0fb-158">O perfil de Codificação é pré-selecionado para **Azure H.264 720p 16:9 (1280x720)**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="1f0fb-159">Para personalizar essas configurações, selecione o ícone de engrenagem à direita da lista suspensa e escolha **Nova Predefinição**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="1f0fb-161">Configure as predefinições do codificador.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-161">Configure encoder presets.</span></span>

    <span data-ttu-id="1f0fb-162">Nomeie a predefinição e verifique as seguintes configurações recomendadas:</span><span class="sxs-lookup"><span data-stu-id="1f0fb-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="1f0fb-163">**Vídeo**</span><span class="sxs-lookup"><span data-stu-id="1f0fb-163">**Video**</span></span>

   * <span data-ttu-id="1f0fb-164">Codificador: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="1f0fb-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="1f0fb-165">Quadros por segundo: 30</span><span class="sxs-lookup"><span data-stu-id="1f0fb-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="1f0fb-166">Taxa de bits média: 5.000 kbits/s (Pode ser ajustada com base nas limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="1f0fb-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="1f0fb-167">Perfil: Principal</span><span class="sxs-lookup"><span data-stu-id="1f0fb-167">Profile: Main</span></span>
   * <span data-ttu-id="1f0fb-168">Quadro chave: a cada 60 quadros</span><span class="sxs-lookup"><span data-stu-id="1f0fb-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="1f0fb-169">**Áudio**</span><span class="sxs-lookup"><span data-stu-id="1f0fb-169">**Audio**</span></span>

   * <span data-ttu-id="1f0fb-170">Taxa de bits de destino: 192 kbits/s</span><span class="sxs-lookup"><span data-stu-id="1f0fb-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="1f0fb-171">Taxa de amostragem: 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="1f0fb-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="1f0fb-173">Pressione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-173">Press **Save**.</span></span>

    <span data-ttu-id="1f0fb-174">O campo Codificação agora tem o perfil recém-criado disponível para seleção.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="1f0fb-175">Certifique-se de selecionar o novo perfil.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="1f0fb-176">Obtenha a URL de entrada do canal para atribuí-la ao **Ponto de extremidade RTMP**do Wirecast.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="1f0fb-177">Navegue de volta para a ferramenta AMSE e verifique o status de conclusão do canal.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="1f0fb-178">Depois do Estado ser alterado de **Iniciando** para **Executando**, você poderá obter a URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="1f0fb-179">Quando o canal estiver em execução, clique com o botão direito no nome dele, navegue até parar sobre **Copiar URL de entrada para área de transferência**, em seguida, selecione **URL da Entrada Principal**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="1f0fb-181">Na janela **Configurações de Saída** do Wirecast, cole essas informações no campo **Endereço** da seção de saída e atribua um nome de transmissão.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="1f0fb-183">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-183">Select **OK**.</span></span>
2. <span data-ttu-id="1f0fb-184">Na tela principal do **Wirecast**, confirme se as fontes de entrada de áudio e vídeo estão prontas e pressione **Transmissão** no canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="1f0fb-186">Antes de clicar em **Transmissão**, você **deve** assegurar que o Canal está pronto.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="1f0fb-187">Além disso, lembre-se de não deixar o Canal em um estado pronto sem um feed de contribuição de entrada por mais de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="1f0fb-188">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="1f0fb-188">Test playback</span></span>

<span data-ttu-id="1f0fb-189">Navegue até a ferramenta AMSE e clique com botão direito do mouse no canal a ser testado.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="1f0fb-190">No menu, passe o mouse sobre **Reproduzir a Visualização** e selecione **Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="1f0fb-191">Se a transmissão for exibida no player, isso significa que o codificador foi corretamente configurado para se conectar ao AMS.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="1f0fb-192">Se um erro for recebido, será necessário redefinir o canal e ajustar as configurações do codificador.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="1f0fb-193">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="1f0fb-194">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="1f0fb-194">Create a program</span></span>
1. <span data-ttu-id="1f0fb-195">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="1f0fb-196">Na guia **Ativo** na ferramenta AMSE, clique com o botão direito na área do programa e selecione **Criar Novo Programa**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="1f0fb-198">Nomeie o programa e, se necessário, ajuste a **Duração da Janela de Arquivo** (cujo padrão é de 4 horas).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="1f0fb-199">Você também pode especificar um local de armazenamento ou deixar como o padrão.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="1f0fb-200">Marque a caixa **Iniciar o Programa agora** .</span><span class="sxs-lookup"><span data-stu-id="1f0fb-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="1f0fb-201">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="1f0fb-202">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="1f0fb-203">Quando o programa estiver em execução, confirme a reprodução clicando com o botão direito do programa e navegando até **Reproduzi o(s) programa(s)**, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="1f0fb-204">Depois de confirmar, clique novamente com botão direito no programa e selecione **Copie a URL de Saída para Área de Transferência** (ou recupere essas informações na opção **Informações e configurações do programa** do menu).</span><span class="sxs-lookup"><span data-stu-id="1f0fb-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="1f0fb-205">A transmissão agora está pronta para ser inserida em um player ou distribuída para um público para a exibição ao vivo.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="1f0fb-206">solução de problemas</span><span class="sxs-lookup"><span data-stu-id="1f0fb-206">Troubleshooting</span></span>
<span data-ttu-id="1f0fb-207">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="1f0fb-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1f0fb-208">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="1f0fb-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1f0fb-209">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="1f0fb-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
