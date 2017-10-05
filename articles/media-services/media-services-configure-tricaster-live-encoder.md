---
title: "Configurar o codificador NewTek TriCaster para enviar uma transmissão ativa da taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como configurar o codificador ativo TriCaster para enviar uma transmissão de taxa de bits única para os canais do AMS que estão habilitados para codificação ativa."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="11e15-103">Usar o codificador NewTek TriCaster para enviar uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="11e15-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11e15-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="11e15-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="11e15-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="11e15-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="11e15-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="11e15-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="11e15-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="11e15-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="11e15-108">Este tópico mostra como configurar o codificador ativo [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) para enviar uma transmissão de taxa de bits única para os canais do AMS que estão habilitados para codificação ativa.</span><span class="sxs-lookup"><span data-stu-id="11e15-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="11e15-109">Para obter mais informações, consulte [Trabalhando com canais habilitados para executar codificação ao vivo com os Serviços de Mídia do Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="11e15-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="11e15-110">Este tutorial mostra como gerenciar o AMS (Serviços de Mídia do Azure) com a ferramenta AMSE (Gerenciador de Serviços de Mídia da Azure).</span><span class="sxs-lookup"><span data-stu-id="11e15-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="11e15-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="11e15-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="11e15-112">Se você estiver no Mac ou Linux, use o portal do Azure para criar [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="11e15-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11e15-113">Ao usar o Tricaster para o envio de um feed de contribuição aos canais AMS habilitados para codificação ativa, pode haver problemas de áudio/vídeo no evento ao vivo, caso você use determinados recursos do Tricaster, como corte rápido entre feeds ou alternância de/para imagens fixas.</span><span class="sxs-lookup"><span data-stu-id="11e15-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="11e15-114">A equipe do AMS está trabalhando para corrigir esses problemas; até lá, não é recomendável usar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="11e15-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="11e15-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="11e15-115">Prerequisites</span></span>
* [<span data-ttu-id="11e15-116">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="11e15-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="11e15-117">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="11e15-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="11e15-118">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="11e15-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="11e15-119">Instale a versão mais recente da ferramenta [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="11e15-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="11e15-120">Inicie a ferramenta e conecte-se à sua conta do AMS.</span><span class="sxs-lookup"><span data-stu-id="11e15-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="11e15-121">Dicas</span><span class="sxs-lookup"><span data-stu-id="11e15-121">Tips</span></span>
* <span data-ttu-id="11e15-122">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="11e15-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="11e15-123">Uma boa regra geral ao determinar os requisitos de largura de banda é dobrar as taxas de bits de transmissão.</span><span class="sxs-lookup"><span data-stu-id="11e15-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="11e15-124">Embora isso não seja um requisito obrigatório, isso ajuda a reduzir o impacto do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="11e15-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="11e15-125">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="11e15-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="11e15-126">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="11e15-126">Create a channel</span></span>
1. <span data-ttu-id="11e15-127">Na ferramenta AMSE, navegue até a guia **Ao Vivo** e clique com o botão direito do mouse na área de canais.</span><span class="sxs-lookup"><span data-stu-id="11e15-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="11e15-128">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="11e15-128">Select **Create channel…**</span></span> <span data-ttu-id="11e15-129">no menu.</span><span class="sxs-lookup"><span data-stu-id="11e15-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="11e15-131">Especifique um nome de canal; o campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="11e15-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="11e15-132">Nas Configurações do Canal, selecione **Standard** para a opção Codificação Ativa, com o Protocolo de Entrada definido para **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="11e15-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="11e15-133">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="11e15-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="11e15-134">Verifique se a opção **Iniciar o novo canal agora** está marcada.</span><span class="sxs-lookup"><span data-stu-id="11e15-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="11e15-135">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="11e15-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="11e15-137">O canal pode levar até 20 minutos para ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="11e15-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="11e15-138">Enquanto o canal é iniciado, você pode [configurar o codificador](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="11e15-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11e15-139">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="11e15-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="11e15-140">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="11e15-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="11e15-141"><a id=configure_tricaster_rtmp></a>Configurar o codificador do NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="11e15-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="11e15-142">Neste tutorial, são usadas as configurações de saída abaixo.</span><span class="sxs-lookup"><span data-stu-id="11e15-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="11e15-143">O restante desta seção descreve as etapas de configuração mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="11e15-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="11e15-144">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="11e15-144">**Video**:</span></span>

* <span data-ttu-id="11e15-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="11e15-145">Codec: H.264</span></span>
* <span data-ttu-id="11e15-146">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="11e15-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="11e15-147">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="11e15-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="11e15-148">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="11e15-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="11e15-149">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="11e15-149">Frame Rate: 30</span></span>

<span data-ttu-id="11e15-150">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="11e15-150">**Audio**:</span></span>

* <span data-ttu-id="11e15-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="11e15-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="11e15-152">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="11e15-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="11e15-153">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="11e15-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="11e15-154">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="11e15-154">Configuration steps</span></span>
1. <span data-ttu-id="11e15-155">Crie um novo projeto do **NewTek TriCaster** dependendo de qual fonte de entrada de vídeo está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="11e15-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="11e15-156">Depois de entrar nesse projeto, encontre o botão **Transmissão** e clique no ícone de engrenagem ao lado dele para acessar o menu de configuração da transmissão.</span><span class="sxs-lookup"><span data-stu-id="11e15-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="11e15-158">Depois de abrir o menu, clique em **Novo** no título Conexão.</span><span class="sxs-lookup"><span data-stu-id="11e15-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="11e15-159">Quando solicitado para selecionar o tipo de conexão, selecione **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="11e15-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="11e15-161">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="11e15-161">Click **OK**.</span></span>
5. <span data-ttu-id="11e15-162">Um perfil FMLE agora pode ser importado clicando na seta suspensa no **Perfil de Streaming** e navegando até **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="11e15-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="11e15-164">Navegue até onde o perfil FMLE configurado foi salvo.</span><span class="sxs-lookup"><span data-stu-id="11e15-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="11e15-165">Selecione-o e pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="11e15-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="11e15-166">Uma vez que o perfil foi carregado, vá para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="11e15-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="11e15-167">Obtenha a URL de entrada do canal para atribuí-la ao **Ponto de extremidade RTMP**do Tricaster.</span><span class="sxs-lookup"><span data-stu-id="11e15-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="11e15-168">Navegue de volta para a ferramenta AMSE e verifique o status de conclusão do canal.</span><span class="sxs-lookup"><span data-stu-id="11e15-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="11e15-169">Depois do Estado ser alterado de **Iniciando** para **Executando**, você poderá obter a URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="11e15-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="11e15-170">Quando o canal estiver em execução, clique com o botão direito no nome dele, navegue até parar sobre **Copiar URL de entrada para área de transferência**, em seguida, selecione **URL da Entrada Principal**.</span><span class="sxs-lookup"><span data-stu-id="11e15-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="11e15-172">Cole essas informações no campo **Local** sob **Flash Server** dentro do projeto Tricaster.</span><span class="sxs-lookup"><span data-stu-id="11e15-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="11e15-173">Atribua também um nome de transmissão no campo **ID da transmissão** .</span><span class="sxs-lookup"><span data-stu-id="11e15-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="11e15-174">Se as informações do fluxo forem adicionadas ao perfil FMLE, ele também poderá ser importado para esta seção clicando em **Importar Configurações**, navegando até o perfil FMLE salvo e clicando em **OK**.</span><span class="sxs-lookup"><span data-stu-id="11e15-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="11e15-175">Os campos relevantes do Flash Server devem preencher as informações do FMLE.</span><span class="sxs-lookup"><span data-stu-id="11e15-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="11e15-177">Quando terminar, clique em **OK** na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="11e15-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="11e15-178">Quando as entradas de áudio e vídeo no Tricaster estiverem prontas, comece a transmissão para o AMS clicando no botão **Transmissão** .</span><span class="sxs-lookup"><span data-stu-id="11e15-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="11e15-180">Antes de clicar em **Transmissão**, você **deve** assegurar que o Canal está pronto.</span><span class="sxs-lookup"><span data-stu-id="11e15-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="11e15-181">Além disso, lembre-se de não deixar o Canal em um estado pronto sem um feed de contribuição de entrada por mais de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="11e15-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="11e15-182">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="11e15-182">Test playback</span></span>
<span data-ttu-id="11e15-183">Navegue até a ferramenta AMSE e clique com botão direito do mouse no canal a ser testado.</span><span class="sxs-lookup"><span data-stu-id="11e15-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="11e15-184">No menu, passe o mouse sobre **Reproduzir a Visualização** e selecione **Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="11e15-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="11e15-185">Se a transmissão for exibida no player, isso significa que o codificador foi corretamente configurado para se conectar ao AMS.</span><span class="sxs-lookup"><span data-stu-id="11e15-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="11e15-186">Se um erro for recebido, será necessário redefinir o canal e ajustar as configurações do codificador.</span><span class="sxs-lookup"><span data-stu-id="11e15-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="11e15-187">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="11e15-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="11e15-188">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="11e15-188">Create a program</span></span>
1. <span data-ttu-id="11e15-189">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="11e15-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="11e15-190">Na guia **Ativo** na ferramenta AMSE, clique com o botão direito na área do programa e selecione **Criar Novo Programa**.</span><span class="sxs-lookup"><span data-stu-id="11e15-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="11e15-192">Nomeie o programa e, se necessário, ajuste a **Duração da Janela de Arquivo** (cujo padrão é de 4 horas).</span><span class="sxs-lookup"><span data-stu-id="11e15-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="11e15-193">Você também pode especificar um local de armazenamento ou deixar como o padrão.</span><span class="sxs-lookup"><span data-stu-id="11e15-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="11e15-194">Marque a caixa **Iniciar o Programa agora** .</span><span class="sxs-lookup"><span data-stu-id="11e15-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="11e15-195">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="11e15-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="11e15-196">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="11e15-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="11e15-197">Quando o programa estiver em execução, confirme a reprodução clicando com o botão direito do programa e navegando até **Reproduzi o(s) programa(s)**, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="11e15-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="11e15-198">Depois de confirmar, clique novamente com botão direito no programa e selecione **Copie a URL de Saída para Área de Transferência** (ou recupere essas informações na opção **Informações e configurações do programa** do menu).</span><span class="sxs-lookup"><span data-stu-id="11e15-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="11e15-199">A transmissão agora está pronta para ser inserida em um player ou distribuída para um público para a exibição ao vivo.</span><span class="sxs-lookup"><span data-stu-id="11e15-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="11e15-200">solução de problemas</span><span class="sxs-lookup"><span data-stu-id="11e15-200">Troubleshooting</span></span>
<span data-ttu-id="11e15-201">Veja o tópico [solução de problemas](media-services-troubleshooting-live-streaming.md) para obter orientações.</span><span class="sxs-lookup"><span data-stu-id="11e15-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="11e15-202">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="11e15-202">Next step</span></span>
<span data-ttu-id="11e15-203">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="11e15-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11e15-204">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="11e15-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
