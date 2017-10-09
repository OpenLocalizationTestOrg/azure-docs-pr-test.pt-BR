---
title: "aaaConfigure Olá Live elementar codificador toosend uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como tooconfigure Olá Live elementar codificador toosend um canais de tooAMS de fluxo de taxa de bits única que são habilitados para codificação ao vivo."
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
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="27cd3-103">Use Olá Live elementar codificador toosend uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="27cd3-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27cd3-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="27cd3-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="27cd3-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="27cd3-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="27cd3-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="27cd3-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="27cd3-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="27cd3-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="27cd3-108">Este tópico mostra como Olá tooconfigure [Live elementar](http://www.elementaltechnologies.com/products/elemental-live) codificador toosend tooAMS canais que são habilitados para codificação ao vivo de fluxo de uma taxa de bits única.</span><span class="sxs-lookup"><span data-stu-id="27cd3-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="27cd3-109">Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="27cd3-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="27cd3-110">Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="27cd3-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="27cd3-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="27cd3-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="27cd3-112">Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="27cd3-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27cd3-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27cd3-113">Prerequisites</span></span>
* <span data-ttu-id="27cd3-114">Deve ter um conhecimento prático do usando o Live elementar web interface toocreate eventos ao vivo.</span><span class="sxs-lookup"><span data-stu-id="27cd3-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="27cd3-115">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="27cd3-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="27cd3-116">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="27cd3-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="27cd3-117">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="27cd3-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="27cd3-118">Instale a versão mais recente Olá de saudação [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="27cd3-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="27cd3-119">Inicie a ferramenta hello e conecte-se a conta tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="27cd3-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="27cd3-120">Dicas</span><span class="sxs-lookup"><span data-stu-id="27cd3-120">Tips</span></span>
* <span data-ttu-id="27cd3-121">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="27cd3-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="27cd3-122">Uma boa regra prática ao determinar os requisitos de largura de banda é toodouble Olá streaming taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="27cd3-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="27cd3-123">Embora não seja um requisito obrigatório, ela ajuda a reduzir o impacto de saudação do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="27cd3-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="27cd3-124">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="27cd3-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="27cd3-125">Elemental Live com ingestão de RTP</span><span class="sxs-lookup"><span data-stu-id="27cd3-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="27cd3-126">Esta seção mostra como tooconfigure Olá elementar codificador ao vivo que envia uma taxa de bits única fluxo ao vivo sobre RTP.</span><span class="sxs-lookup"><span data-stu-id="27cd3-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="27cd3-127">Para saber mais, consulte [Fluxo MPEG TS por RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="27cd3-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="27cd3-128">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="27cd3-128">Create a channel</span></span>

1. <span data-ttu-id="27cd3-129">Na ferramenta AMSE hello, navegar toohello **Live** guia e clique com o botão direito na área de canal hello.</span><span class="sxs-lookup"><span data-stu-id="27cd3-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="27cd3-130">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="27cd3-130">Select **Create channel…**</span></span> <span data-ttu-id="27cd3-131">no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="27cd3-131">from hello menu.</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="27cd3-133">Especifique um nome de canal, Olá campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="27cd3-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="27cd3-134">Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="27cd3-135">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="27cd3-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="27cd3-136">Verifique se Olá **início Olá novo canal agora** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="27cd3-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="27cd3-137">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-137">Click **Create Channel**.</span></span>

   ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="27cd3-139">canal Olá pode levar até 20 minutos toostart.</span><span class="sxs-lookup"><span data-stu-id="27cd3-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="27cd3-140">Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="27cd3-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27cd3-141">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="27cd3-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="27cd3-142">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="27cd3-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="27cd3-143"><a id=configure_elemental_rtp></a>Configurar Olá Live elementar codificador</span><span class="sxs-lookup"><span data-stu-id="27cd3-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="27cd3-144">Neste tutorial Olá seguintes configurações de saída são usadas.</span><span class="sxs-lookup"><span data-stu-id="27cd3-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="27cd3-145">Olá restante desta seção descreve etapas de configuração em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="27cd3-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="27cd3-146">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="27cd3-146">**Video**:</span></span>

* <span data-ttu-id="27cd3-147">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="27cd3-147">Codec: H.264</span></span>
* <span data-ttu-id="27cd3-148">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="27cd3-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="27cd3-149">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="27cd3-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="27cd3-150">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="27cd3-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="27cd3-151">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="27cd3-151">Frame Rate: 30</span></span>

<span data-ttu-id="27cd3-152">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="27cd3-152">**Audio**:</span></span>

* <span data-ttu-id="27cd3-153">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="27cd3-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="27cd3-154">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="27cd3-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="27cd3-155">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="27cd3-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="27cd3-156">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="27cd3-156">Configuration steps</span></span>
1. <span data-ttu-id="27cd3-157">Navegue toohello **Live elementar** interface da web e configurar o codificador Olá para **UDP/TS** streaming.</span><span class="sxs-lookup"><span data-stu-id="27cd3-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="27cd3-158">Depois de criar um novo evento, role para baixo toohello saída grupos e adicionar Olá **UDP/TS** grupo de saídas.</span><span class="sxs-lookup"><span data-stu-id="27cd3-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="27cd3-159">Crie uma nova saída selecionando **Nova Transmissão** e clicando em **Adicionar Saída**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="27cd3-161">É recomendável evento elementar Olá tem código de tempo de saudação definido muito codificador de saudação do "relógio do sistema" toohelp reconectar-se no caso de saudação de uma falha de fluxo.</span><span class="sxs-lookup"><span data-stu-id="27cd3-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="27cd3-162">Agora que hello saída foi criada, clique em **adicionar fluxo**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="27cd3-163">configurações de saída de Hello agora podem ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="27cd3-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="27cd3-164">Role para baixo toohello "Fluxo 1" que acabou de criar, clique em Olá **vídeo** guia Olá esquerda e expanda Olá **avançado** seção de configurações.</span><span class="sxs-lookup"><span data-stu-id="27cd3-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="27cd3-166">Enquanto Live elementar tem uma ampla gama de personalização disponíveis, hello configurações a seguir são recomendadas para começar a trabalhar com o streaming tooAMS.</span><span class="sxs-lookup"><span data-stu-id="27cd3-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="27cd3-167">Resolução: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="27cd3-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="27cd3-168">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="27cd3-168">Framerate: 30</span></span>
   * <span data-ttu-id="27cd3-169">Tamanho de GOP: 60 quadros</span><span class="sxs-lookup"><span data-stu-id="27cd3-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="27cd3-170">Modo de entrelaçamento: Progressivo</span><span class="sxs-lookup"><span data-stu-id="27cd3-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="27cd3-171">Taxa de bits: 5000000 bits/s (Isso pode ser ajustado baseado nas limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="27cd3-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="27cd3-173">Obter URL de entrada do canal de saudação.</span><span class="sxs-lookup"><span data-stu-id="27cd3-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="27cd3-174">Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello.</span><span class="sxs-lookup"><span data-stu-id="27cd3-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="27cd3-175">Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="27cd3-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="27cd3-176">Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="27cd3-178">Colar essas informações no hello **destino principal** campo de saudação Elemental.</span><span class="sxs-lookup"><span data-stu-id="27cd3-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="27cd3-179">Todas as outras configurações podem permanecer padrão hello.</span><span class="sxs-lookup"><span data-stu-id="27cd3-179">All other settings can remain hello default.</span></span>

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="27cd3-181">Para redundância adicional, repita essas etapas com hello secundário URL de entrada criando uma guia de "Saída" separada para Streaming de UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="27cd3-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="27cd3-182">Clique em **criar** (se um novo evento foi criado) ou **atualização** (se estiver editando um evento já existente) e, em seguida, continue toostart codificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="27cd3-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27cd3-183">Antes de clicar em **iniciar** na interface de web Live elementar hello, você **deve** Certifique-se de que o canal de saudação está pronto.</span><span class="sxs-lookup"><span data-stu-id="27cd3-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="27cd3-184">Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem um evento por mais de > 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="27cd3-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="27cd3-185">Após execução de fluxo de saudação de 30 segundos, navegue para reprodução de teste e a ferramenta AMSE toohello back.</span><span class="sxs-lookup"><span data-stu-id="27cd3-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="27cd3-186">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="27cd3-186">Test playback</span></span>

<span data-ttu-id="27cd3-187">Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado.</span><span class="sxs-lookup"><span data-stu-id="27cd3-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="27cd3-188">No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="27cd3-189">Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="27cd3-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="27cd3-190">Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas.</span><span class="sxs-lookup"><span data-stu-id="27cd3-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="27cd3-191">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="27cd3-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="27cd3-192">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="27cd3-192">Create a program</span></span>
1. <span data-ttu-id="27cd3-193">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="27cd3-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="27cd3-194">Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elementares](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="27cd3-196">Nomeie o programa hello e, se necessário, ajuste Olá **duração da janela de arquivo** (os horários de too4 padrões).</span><span class="sxs-lookup"><span data-stu-id="27cd3-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="27cd3-197">Você também pode especificar um local de armazenamento ou deixe como saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="27cd3-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="27cd3-198">Verificar Olá **início Olá programa agora** caixa.</span><span class="sxs-lookup"><span data-stu-id="27cd3-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="27cd3-199">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="27cd3-200">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="27cd3-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="27cd3-201">Depois que o programa de hello está sendo executado, confirme a reprodução clique direito programa hello e navegando muito**reprodução Olá programas** e, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="27cd3-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="27cd3-202">Depois de confirmar, clique com botão direito programa hello novamente e selecionar **copiar Olá URL de saída tooClipboard** (ou recuperar essas informações do hello **informações e configurações de programa** opção no menu de saudação).</span><span class="sxs-lookup"><span data-stu-id="27cd3-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="27cd3-203">Olá está agora pronto toobe inserido em um player ou público tooan distribuída ao vivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="27cd3-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="27cd3-204">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="27cd3-204">Troubleshooting</span></span>
<span data-ttu-id="27cd3-205">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="27cd3-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="27cd3-206">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="27cd3-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="27cd3-207">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="27cd3-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
