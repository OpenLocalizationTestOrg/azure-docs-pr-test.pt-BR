---
title: "aaaConfigure Olá toosend de codificador Telestream Wirecast uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como Olá tooconfigure Wirecast canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo. "
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
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="b5827-103">Use Olá Wirecast codificador toosend uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="b5827-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5827-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="b5827-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="b5827-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="b5827-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="b5827-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="b5827-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="b5827-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="b5827-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="b5827-108">Este tópico mostra como Olá tooconfigure [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo.</span><span class="sxs-lookup"><span data-stu-id="b5827-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="b5827-109">Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="b5827-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="b5827-110">Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="b5827-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="b5827-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="b5827-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="b5827-112">Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="b5827-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5827-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b5827-113">Prerequisites</span></span>
* [<span data-ttu-id="b5827-114">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="b5827-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="b5827-115">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="b5827-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="b5827-116">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="b5827-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="b5827-117">Instale a versão mais recente Olá de saudação [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="b5827-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="b5827-118">Inicie a ferramenta hello e conecte-se a conta tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="b5827-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="b5827-119">Dicas</span><span class="sxs-lookup"><span data-stu-id="b5827-119">Tips</span></span>
* <span data-ttu-id="b5827-120">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="b5827-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="b5827-121">Uma boa regra prática ao determinar os requisitos de largura de banda é toodouble Olá streaming taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="b5827-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="b5827-122">Embora não seja um requisito obrigatório, ela ajuda a reduzir o impacto de saudação do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="b5827-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="b5827-123">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="b5827-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="b5827-124">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="b5827-124">Create a channel</span></span>
1. <span data-ttu-id="b5827-125">Na ferramenta AMSE hello, navegar toohello **Live** guia e clique com o botão direito na área de canal hello.</span><span class="sxs-lookup"><span data-stu-id="b5827-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="b5827-126">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="b5827-126">Select **Create channel…**</span></span> <span data-ttu-id="b5827-127">no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5827-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="b5827-129">Especifique um nome de canal, Olá campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="b5827-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="b5827-130">Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="b5827-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="b5827-131">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="b5827-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="b5827-132">Verifique se Olá **início Olá novo canal agora** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="b5827-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="b5827-133">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="b5827-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="b5827-135">canal Olá pode levar até 20 minutos toostart.</span><span class="sxs-lookup"><span data-stu-id="b5827-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="b5827-136">Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="b5827-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5827-137">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="b5827-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="b5827-138">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="b5827-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="b5827-139"><a id=configure_wirecast_rtmp></a>Configurar Olá codificador Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="b5827-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="b5827-140">Neste tutorial Olá seguintes configurações de saída são usadas.</span><span class="sxs-lookup"><span data-stu-id="b5827-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="b5827-141">Olá restante desta seção descreve etapas de configuração em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="b5827-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="b5827-142">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="b5827-142">**Video**:</span></span>

* <span data-ttu-id="b5827-143">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="b5827-143">Codec: H.264</span></span>
* <span data-ttu-id="b5827-144">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="b5827-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="b5827-145">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="b5827-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="b5827-146">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="b5827-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="b5827-147">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="b5827-147">Frame Rate: 30</span></span>

<span data-ttu-id="b5827-148">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="b5827-148">**Audio**:</span></span>

* <span data-ttu-id="b5827-149">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="b5827-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="b5827-150">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="b5827-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="b5827-151">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="b5827-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="b5827-152">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="b5827-152">Configuration steps</span></span>
1. <span data-ttu-id="b5827-153">Abra aplicativo Telestream Wirecast Olá Olá máquina que está sendo usado e configurado para streaming de RTMP.</span><span class="sxs-lookup"><span data-stu-id="b5827-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="b5827-154">Configurar saída de hello navegando toohello **saída** guia e selecionando **configurações de saída...** .</span><span class="sxs-lookup"><span data-stu-id="b5827-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="b5827-155">Verifique se Olá **destino de saída** está definido muito**servidor RTMP**.</span><span class="sxs-lookup"><span data-stu-id="b5827-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="b5827-156">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5827-156">Click **OK**.</span></span>
4. <span data-ttu-id="b5827-157">Na página de configurações do hello, defina Olá **destino** campo toobe **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="b5827-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="b5827-158">Olá perfil de codificação é pré-selecionada muito**Azure h. 264 720 p 16:9 (1280x720)**.</span><span class="sxs-lookup"><span data-stu-id="b5827-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="b5827-159">toocustomize essas configurações, selecione Olá toohello de ícone de engrenagem direito da saudação lista suspensa e, em seguida, escolha **nova predefinição**.</span><span class="sxs-lookup"><span data-stu-id="b5827-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="b5827-161">Configure as predefinições do codificador.</span><span class="sxs-lookup"><span data-stu-id="b5827-161">Configure encoder presets.</span></span>

    <span data-ttu-id="b5827-162">Olá nome predefinido e verificar as configurações recomendada a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="b5827-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="b5827-163">**Vídeo**</span><span class="sxs-lookup"><span data-stu-id="b5827-163">**Video**</span></span>

   * <span data-ttu-id="b5827-164">Codificador: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="b5827-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="b5827-165">Quadros por segundo: 30</span><span class="sxs-lookup"><span data-stu-id="b5827-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="b5827-166">Taxa de bits média: 5.000 kbits/s (Pode ser ajustada com base nas limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="b5827-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="b5827-167">Perfil: Principal</span><span class="sxs-lookup"><span data-stu-id="b5827-167">Profile: Main</span></span>
   * <span data-ttu-id="b5827-168">Quadro chave: a cada 60 quadros</span><span class="sxs-lookup"><span data-stu-id="b5827-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="b5827-169">**Áudio**</span><span class="sxs-lookup"><span data-stu-id="b5827-169">**Audio**</span></span>

   * <span data-ttu-id="b5827-170">Taxa de bits de destino: 192 kbits/s</span><span class="sxs-lookup"><span data-stu-id="b5827-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="b5827-171">Taxa de amostragem: 44,100 kHz</span><span class="sxs-lookup"><span data-stu-id="b5827-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="b5827-173">Pressione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b5827-173">Press **Save**.</span></span>

    <span data-ttu-id="b5827-174">campo de codificação Olá agora tem disponíveis para seleção do perfil de saudação recém-criado.</span><span class="sxs-lookup"><span data-stu-id="b5827-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="b5827-175">Certifique-se de novo perfil de saudação está selecionado.</span><span class="sxs-lookup"><span data-stu-id="b5827-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="b5827-176">Obter URL de entrada do canal de saudação em ordem tooassign-toohello Wirecast **ponto de extremidade de RTMP**.</span><span class="sxs-lookup"><span data-stu-id="b5827-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="b5827-177">Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello.</span><span class="sxs-lookup"><span data-stu-id="b5827-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="b5827-178">Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="b5827-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="b5827-179">Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.</span><span class="sxs-lookup"><span data-stu-id="b5827-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="b5827-181">Em Olá Wirecast **configurações de saída** janela, colar essas informações no hello **endereço** campo da seção de saída de hello e atribua um nome de fluxo.</span><span class="sxs-lookup"><span data-stu-id="b5827-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="b5827-183">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5827-183">Select **OK**.</span></span>
2. <span data-ttu-id="b5827-184">Em Olá principal **Wirecast** , confirme as fontes de entrada de áudio e vídeo estiverem prontos e, em seguida, pressionar **fluxo** no canto superior esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b5827-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="b5827-186">Antes de clicar em **fluxo**, você **deve** Certifique-se de que o canal de saudação está pronto.</span><span class="sxs-lookup"><span data-stu-id="b5827-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="b5827-187">Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem uma entrada contribuição feed por mais de > 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="b5827-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="b5827-188">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="b5827-188">Test playback</span></span>

<span data-ttu-id="b5827-189">Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado.</span><span class="sxs-lookup"><span data-stu-id="b5827-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="b5827-190">No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="b5827-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="b5827-191">Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="b5827-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="b5827-192">Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas.</span><span class="sxs-lookup"><span data-stu-id="b5827-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="b5827-193">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="b5827-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="b5827-194">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="b5827-194">Create a program</span></span>
1. <span data-ttu-id="b5827-195">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="b5827-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="b5827-196">Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.</span><span class="sxs-lookup"><span data-stu-id="b5827-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="b5827-198">Nomeie o programa hello e, se necessário, ajuste Olá **duração da janela de arquivo** (os horários de too4 padrões).</span><span class="sxs-lookup"><span data-stu-id="b5827-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="b5827-199">Você também pode especificar um local de armazenamento ou deixe como saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="b5827-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="b5827-200">Verificar Olá **início Olá programa agora** caixa.</span><span class="sxs-lookup"><span data-stu-id="b5827-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="b5827-201">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="b5827-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="b5827-202">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="b5827-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="b5827-203">Depois que o programa de hello está sendo executado, confirme a reprodução clique direito programa hello e navegando muito**reprodução Olá programas** e, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="b5827-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="b5827-204">Depois de confirmar, clique com botão direito programa hello novamente e selecionar **copiar Olá URL de saída tooClipboard** (ou recuperar essas informações do hello **informações e configurações de programa** opção no menu de saudação).</span><span class="sxs-lookup"><span data-stu-id="b5827-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="b5827-205">Olá está agora pronto toobe inserido em um player ou público tooan distribuída ao vivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="b5827-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="b5827-206">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b5827-206">Troubleshooting</span></span>
<span data-ttu-id="b5827-207">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="b5827-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b5827-208">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="b5827-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b5827-209">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="b5827-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
