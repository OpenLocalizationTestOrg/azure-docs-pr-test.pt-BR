---
title: "Configurar o codificador FMLE para enviar uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como configurar o codificador FMLE (Flash Media Live Encoder) para enviar uma transmissão de taxa de bits única para os canais do AMS que são habilitados para codificação ativa."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="5521f-103">Usar o codificador FMLE para enviar uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="5521f-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5521f-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="5521f-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="5521f-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="5521f-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="5521f-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="5521f-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="5521f-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="5521f-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="5521f-108">Este tópico mostra como configurar o codificador [FMLE](http://www.adobe.com/products/flash-media-encoder.html) (Flash Media Live Encoder) para enviar uma transmissão de taxa de bits única para os canais do AMS que são habilitados para codificação ativa.</span><span class="sxs-lookup"><span data-stu-id="5521f-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="5521f-109">Para obter mais informações, consulte [Trabalhando com canais habilitados para executar codificação ao vivo com os Serviços de Mídia do Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="5521f-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="5521f-110">Este tutorial mostra como gerenciar o AMS (Serviços de Mídia do Azure) com a ferramenta AMSE (Gerenciador de Serviços de Mídia da Azure).</span><span class="sxs-lookup"><span data-stu-id="5521f-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="5521f-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="5521f-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="5521f-112">Se você estiver no Mac ou Linux, use o portal do Azure para criar [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="5521f-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="5521f-113">Observe que este tutorial descreve como usar o AAC.</span><span class="sxs-lookup"><span data-stu-id="5521f-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="5521f-114">No entanto, por padrão, o FMLE dá suporte ao AAC.</span><span class="sxs-lookup"><span data-stu-id="5521f-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="5521f-115">Você precisa comprar um plug-in para codificação do AAC como MainConcept: [AAC plug-in](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="5521f-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5521f-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5521f-116">Prerequisites</span></span>
* [<span data-ttu-id="5521f-117">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="5521f-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="5521f-118">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="5521f-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="5521f-119">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="5521f-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="5521f-120">Instale a versão mais recente da ferramenta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="5521f-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="5521f-121">Inicie a ferramenta e conecte-se à sua conta do AMS.</span><span class="sxs-lookup"><span data-stu-id="5521f-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="5521f-122">Dicas</span><span class="sxs-lookup"><span data-stu-id="5521f-122">Tips</span></span>
* <span data-ttu-id="5521f-123">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="5521f-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="5521f-124">Uma boa regra geral ao determinar os requisitos de largura de banda é dobrar as taxas de bits de transmissão.</span><span class="sxs-lookup"><span data-stu-id="5521f-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="5521f-125">Embora isso não seja um requisito obrigatório, isso ajuda a reduzir o impacto do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="5521f-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="5521f-126">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="5521f-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="5521f-127">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="5521f-127">Create a channel</span></span>
1. <span data-ttu-id="5521f-128">Na ferramenta AMSE, navegue até a guia **Ao Vivo** e clique com o botão direito do mouse na área de canais.</span><span class="sxs-lookup"><span data-stu-id="5521f-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="5521f-129">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="5521f-129">Select **Create channel…**</span></span> <span data-ttu-id="5521f-130">no menu.</span><span class="sxs-lookup"><span data-stu-id="5521f-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="5521f-132">Especifique um nome de canal; o campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="5521f-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="5521f-133">Nas Configurações do Canal, selecione **Standard** para a opção Codificação Ativa, com o Protocolo de Entrada definido para **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="5521f-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="5521f-134">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="5521f-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="5521f-135">Verifique se a opção **Iniciar o novo canal agora** está marcada.</span><span class="sxs-lookup"><span data-stu-id="5521f-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="5521f-136">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="5521f-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="5521f-138">O canal pode levar até 20 minutos para ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="5521f-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="5521f-139">Enquanto o canal é iniciado, você pode [configurar o codificador](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="5521f-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5521f-140">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="5521f-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="5521f-141">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="5521f-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="5521f-142"><a id=configure_fmle_rtmp></a>Configurar o codificador FMLE</span><span class="sxs-lookup"><span data-stu-id="5521f-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="5521f-143">Neste tutorial, são usadas as configurações de saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="5521f-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="5521f-144">O restante desta seção descreve as etapas de configuração mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="5521f-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="5521f-145">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="5521f-145">**Video**:</span></span>

* <span data-ttu-id="5521f-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="5521f-146">Codec: H.264</span></span>
* <span data-ttu-id="5521f-147">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="5521f-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="5521f-148">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="5521f-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="5521f-149">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="5521f-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="5521f-150">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="5521f-150">Frame Rate: 30</span></span>

<span data-ttu-id="5521f-151">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="5521f-151">**Audio**:</span></span>

* <span data-ttu-id="5521f-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="5521f-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="5521f-153">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="5521f-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="5521f-154">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="5521f-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="5521f-155">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="5521f-155">Configuration steps</span></span>
1. <span data-ttu-id="5521f-156">Navegue até a interface do Flash Media Live Encoder (FMLE) no computador que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="5521f-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="5521f-157">A interface é uma página principal de configurações.</span><span class="sxs-lookup"><span data-stu-id="5521f-157">The interface is one main page of settings.</span></span> <span data-ttu-id="5521f-158">Por favor, anote as seguintes configurações recomendadas para introdução à transmissão usando FMLE.</span><span class="sxs-lookup"><span data-stu-id="5521f-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="5521f-159">Formato: Taxa de quadros H. 264: 30,00</span><span class="sxs-lookup"><span data-stu-id="5521f-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="5521f-160">Tamanho de entrada: 1280x720</span><span class="sxs-lookup"><span data-stu-id="5521f-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="5521f-161">Taxa de bits: 5000 kbits/s (pode ser ajustada com base nas limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="5521f-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="5521f-163">Quando usar as fontes entrelaçadas desmarque a opção “Desentrelaçar”</span><span class="sxs-lookup"><span data-stu-id="5521f-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="5521f-164">Selecione o ícone de chave inglesa ao lado de Formato, essas configurações adicionais devem ser:</span><span class="sxs-lookup"><span data-stu-id="5521f-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="5521f-165">Perfil: Principal</span><span class="sxs-lookup"><span data-stu-id="5521f-165">Profile: Main</span></span>
   * <span data-ttu-id="5521f-166">Nível: 4.0</span><span class="sxs-lookup"><span data-stu-id="5521f-166">Level: 4.0</span></span>
   * <span data-ttu-id="5521f-167">Frequência de quadro-chave: 2 segundos</span><span class="sxs-lookup"><span data-stu-id="5521f-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="5521f-169">Defina a configuração de áudio importante a seguir:</span><span class="sxs-lookup"><span data-stu-id="5521f-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="5521f-170">Formato: AAC</span><span class="sxs-lookup"><span data-stu-id="5521f-170">Format: AAC</span></span>
   * <span data-ttu-id="5521f-171">Taxa de exemplo: 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="5521f-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="5521f-172">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="5521f-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="5521f-174">Obtenha a URL de entrada do canal para atribuí-la ao **Ponto de extremidade FMLE**do FMLE.</span><span class="sxs-lookup"><span data-stu-id="5521f-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="5521f-175">Navegue de volta para a ferramenta AMSE e verifique o status de conclusão do canal.</span><span class="sxs-lookup"><span data-stu-id="5521f-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="5521f-176">Depois do Estado ser alterado de **Iniciando** para **Executando**, você poderá obter a URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="5521f-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="5521f-177">Quando o canal estiver em execução, clique com o botão direito no nome dele, navegue até parar sobre **Copiar URL de entrada para área de transferência**, em seguida, selecione **URL da Entrada Principal**.</span><span class="sxs-lookup"><span data-stu-id="5521f-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="5521f-179">Cole essas informações no campo **URL do FMS** da seção de saída e atribua um nome de transmissão.</span><span class="sxs-lookup"><span data-stu-id="5521f-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="5521f-181">Para redundância adicional, repita essas etapas com a URL de entrada secundária.</span><span class="sxs-lookup"><span data-stu-id="5521f-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="5521f-182">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="5521f-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5521f-183">Antes de clicar em **Conectar**, é **necessário** verificar se o Canal está pronto.</span><span class="sxs-lookup"><span data-stu-id="5521f-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="5521f-184">Além disso, lembre-se de não deixar o Canal em um estado pronto sem um feed de contribuição de entrada por mais de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="5521f-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="5521f-185">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="5521f-185">Test playback</span></span>

<span data-ttu-id="5521f-186">Navegue até a ferramenta AMSE e clique com botão direito do mouse no canal a ser testado.</span><span class="sxs-lookup"><span data-stu-id="5521f-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="5521f-187">No menu, passe o mouse sobre **Reproduzir a Visualização** e selecione **Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="5521f-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="5521f-188">Se a transmissão for exibida no player, isso significa que o codificador foi corretamente configurado para se conectar ao AMS.</span><span class="sxs-lookup"><span data-stu-id="5521f-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="5521f-189">Se um erro for recebido, será necessário redefinir o canal e ajustar as configurações do codificador.</span><span class="sxs-lookup"><span data-stu-id="5521f-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="5521f-190">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="5521f-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="5521f-191">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="5521f-191">Create a program</span></span>
1. <span data-ttu-id="5521f-192">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="5521f-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="5521f-193">Na guia **Ativo** na ferramenta AMSE, clique com o botão direito na área do programa e selecione **Criar Novo Programa**.</span><span class="sxs-lookup"><span data-stu-id="5521f-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="5521f-195">Nomeie o programa e, se necessário, ajuste a **Duração da Janela de Arquivo** (cujo padrão é de 4 horas).</span><span class="sxs-lookup"><span data-stu-id="5521f-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="5521f-196">Você também pode especificar um local de armazenamento ou deixar como o padrão.</span><span class="sxs-lookup"><span data-stu-id="5521f-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="5521f-197">Marque a caixa **Iniciar o Programa agora** .</span><span class="sxs-lookup"><span data-stu-id="5521f-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="5521f-198">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="5521f-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="5521f-199">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="5521f-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="5521f-200">Quando o programa estiver em execução, confirme a reprodução clicando com o botão direito do programa e navegando até **Reproduzi o(s) programa(s)**, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="5521f-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="5521f-201">Depois de confirmar, clique novamente com botão direito no programa e selecione **Copie a URL de Saída para Área de Transferência** (ou recupere essas informações na opção **Informações e configurações do programa** do menu).</span><span class="sxs-lookup"><span data-stu-id="5521f-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="5521f-202">A transmissão agora está pronta para ser inserida em um player ou distribuída para um público para a exibição ao vivo.</span><span class="sxs-lookup"><span data-stu-id="5521f-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="5521f-203">solução de problemas</span><span class="sxs-lookup"><span data-stu-id="5521f-203">Troubleshooting</span></span>
<span data-ttu-id="5521f-204">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="5521f-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5521f-205">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="5521f-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5521f-206">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="5521f-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
