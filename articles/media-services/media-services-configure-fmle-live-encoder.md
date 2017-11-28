---
title: "aaaConfigure Olá FMLE codificador toosend uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como tooconfigure Olá Flash Media ao vivo codificador (FMLE) codificador toosend um canais de tooAMS de fluxo de taxa de bits única que são habilitados para codificação ao vivo."
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
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="0561a-103">Use Olá FMLE codificador toosend uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="0561a-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0561a-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="0561a-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="0561a-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="0561a-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="0561a-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="0561a-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="0561a-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="0561a-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="0561a-108">Este tópico mostra como Olá tooconfigure [Flash Live o codificador de mídia](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) codificador toosend tooAMS canais que são habilitados para codificação ao vivo de fluxo de uma taxa de bits única.</span><span class="sxs-lookup"><span data-stu-id="0561a-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="0561a-109">Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="0561a-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="0561a-110">Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="0561a-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="0561a-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="0561a-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="0561a-112">Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="0561a-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="0561a-113">Observe que este tutorial descreve como usar o AAC.</span><span class="sxs-lookup"><span data-stu-id="0561a-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="0561a-114">No entanto, por padrão, o FMLE dá suporte ao AAC.</span><span class="sxs-lookup"><span data-stu-id="0561a-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="0561a-115">Você precisaria toopurchase um plug-in para codificação AAC por exemplo, MainConcept: [AAC plug-in](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="0561a-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0561a-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0561a-116">Prerequisites</span></span>
* [<span data-ttu-id="0561a-117">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="0561a-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="0561a-118">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="0561a-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="0561a-119">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="0561a-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="0561a-120">Instale a versão mais recente Olá de saudação [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="0561a-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="0561a-121">Inicie a ferramenta hello e conecte-se a conta tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="0561a-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="0561a-122">Dicas</span><span class="sxs-lookup"><span data-stu-id="0561a-122">Tips</span></span>
* <span data-ttu-id="0561a-123">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="0561a-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="0561a-124">Uma boa regra prática ao determinar os requisitos de largura de banda é toodouble Olá streaming taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="0561a-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="0561a-125">Embora não seja um requisito obrigatório, ela ajuda a reduzir o impacto de saudação do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="0561a-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="0561a-126">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="0561a-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="0561a-127">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="0561a-127">Create a channel</span></span>
1. <span data-ttu-id="0561a-128">Na ferramenta AMSE hello, navegar toohello **Live** guia e clique com o botão direito na área de canal hello.</span><span class="sxs-lookup"><span data-stu-id="0561a-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="0561a-129">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="0561a-129">Select **Create channel…**</span></span> <span data-ttu-id="0561a-130">no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="0561a-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="0561a-132">Especifique um nome de canal, Olá campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="0561a-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="0561a-133">Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="0561a-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="0561a-134">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="0561a-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="0561a-135">Verifique se Olá **início Olá novo canal agora** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="0561a-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="0561a-136">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="0561a-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="0561a-138">canal Olá pode levar até 20 minutos toostart.</span><span class="sxs-lookup"><span data-stu-id="0561a-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="0561a-139">Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="0561a-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0561a-140">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="0561a-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="0561a-141">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="0561a-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="0561a-142"><a id=configure_fmle_rtmp></a>Configurar Olá FMLE codificador</span><span class="sxs-lookup"><span data-stu-id="0561a-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="0561a-143">Neste tutorial Olá seguintes configurações de saída são usadas.</span><span class="sxs-lookup"><span data-stu-id="0561a-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="0561a-144">Olá restante desta seção descreve etapas de configuração em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="0561a-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="0561a-145">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="0561a-145">**Video**:</span></span>

* <span data-ttu-id="0561a-146">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="0561a-146">Codec: H.264</span></span>
* <span data-ttu-id="0561a-147">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="0561a-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="0561a-148">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="0561a-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="0561a-149">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="0561a-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="0561a-150">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="0561a-150">Frame Rate: 30</span></span>

<span data-ttu-id="0561a-151">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="0561a-151">**Audio**:</span></span>

* <span data-ttu-id="0561a-152">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="0561a-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="0561a-153">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="0561a-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="0561a-154">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="0561a-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="0561a-155">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="0561a-155">Configuration steps</span></span>
1. <span data-ttu-id="0561a-156">Navegue toohello que interface Flash Live codificador de mídia (FMLE) na máquina hello está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="0561a-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="0561a-157">interface Olá é uma página principal de configurações.</span><span class="sxs-lookup"><span data-stu-id="0561a-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="0561a-158">Por favor, tome nota das recomendadas a seguir Olá configurações tooget iniciado com o streaming usando FMLE.</span><span class="sxs-lookup"><span data-stu-id="0561a-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="0561a-159">Formato: Taxa de quadros H. 264: 30,00</span><span class="sxs-lookup"><span data-stu-id="0561a-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="0561a-160">Tamanho de entrada: 1280x720</span><span class="sxs-lookup"><span data-stu-id="0561a-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="0561a-161">Taxa de bits: 5000 kbits/s (pode ser ajustada com base nas limitações de rede)</span><span class="sxs-lookup"><span data-stu-id="0561a-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="0561a-163">Quando usar entrelaçada fontes, por favor, marca de seleção hello "Desentrelaçar" opção</span><span class="sxs-lookup"><span data-stu-id="0561a-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="0561a-164">Selecione Olá chave inglesa ícone próximo tooFormat, essas configurações adicionais que devem ser:</span><span class="sxs-lookup"><span data-stu-id="0561a-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="0561a-165">Perfil: Principal</span><span class="sxs-lookup"><span data-stu-id="0561a-165">Profile: Main</span></span>
   * <span data-ttu-id="0561a-166">Nível: 4.0</span><span class="sxs-lookup"><span data-stu-id="0561a-166">Level: 4.0</span></span>
   * <span data-ttu-id="0561a-167">Frequência de quadro-chave: 2 segundos</span><span class="sxs-lookup"><span data-stu-id="0561a-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="0561a-169">Saudação de conjunto de configuração de áudio importante a seguir:</span><span class="sxs-lookup"><span data-stu-id="0561a-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="0561a-170">Formato: AAC</span><span class="sxs-lookup"><span data-stu-id="0561a-170">Format: AAC</span></span>
   * <span data-ttu-id="0561a-171">Taxa de exemplo: 44100 kHz</span><span class="sxs-lookup"><span data-stu-id="0561a-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="0561a-172">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="0561a-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="0561a-174">Obter URL de entrada do canal de saudação em ordem tooassign-toohello FMLE **ponto de extremidade de RTMP**.</span><span class="sxs-lookup"><span data-stu-id="0561a-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="0561a-175">Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello.</span><span class="sxs-lookup"><span data-stu-id="0561a-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="0561a-176">Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="0561a-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="0561a-177">Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.</span><span class="sxs-lookup"><span data-stu-id="0561a-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="0561a-179">Colar essas informações no hello **FMS URL** campo da seção de saída de hello e atribua um nome de fluxo.</span><span class="sxs-lookup"><span data-stu-id="0561a-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="0561a-181">Para redundância adicional, repita essas etapas com hello secundário URL de entrada.</span><span class="sxs-lookup"><span data-stu-id="0561a-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="0561a-182">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="0561a-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0561a-183">Antes de clicar em **conectar**, você **deve** Certifique-se de que o canal de saudação está pronto.</span><span class="sxs-lookup"><span data-stu-id="0561a-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="0561a-184">Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem uma entrada contribuição feed por mais de > 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="0561a-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="0561a-185">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="0561a-185">Test playback</span></span>

<span data-ttu-id="0561a-186">Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado.</span><span class="sxs-lookup"><span data-stu-id="0561a-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="0561a-187">No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="0561a-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="0561a-188">Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="0561a-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="0561a-189">Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas.</span><span class="sxs-lookup"><span data-stu-id="0561a-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="0561a-190">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="0561a-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="0561a-191">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="0561a-191">Create a program</span></span>
1. <span data-ttu-id="0561a-192">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="0561a-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="0561a-193">Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.</span><span class="sxs-lookup"><span data-stu-id="0561a-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="0561a-195">Nomeie o programa hello e, se necessário, ajuste Olá **duração da janela de arquivo** (os horários de too4 padrões).</span><span class="sxs-lookup"><span data-stu-id="0561a-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="0561a-196">Você também pode especificar um local de armazenamento ou deixe como saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="0561a-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="0561a-197">Verificar Olá **início Olá programa agora** caixa.</span><span class="sxs-lookup"><span data-stu-id="0561a-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="0561a-198">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="0561a-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="0561a-199">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="0561a-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="0561a-200">Depois que o programa de hello está sendo executado, confirme a reprodução clique direito programa hello e navegando muito**reprodução Olá programas** e, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="0561a-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="0561a-201">Depois de confirmar, clique com botão direito programa hello novamente e selecionar **copiar Olá URL de saída tooClipboard** (ou recuperar essas informações do hello **informações e configurações de programa** opção no menu de saudação).</span><span class="sxs-lookup"><span data-stu-id="0561a-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="0561a-202">Olá está agora pronto toobe inserido em um player ou público tooan distribuída ao vivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="0561a-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="0561a-203">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="0561a-203">Troubleshooting</span></span>
<span data-ttu-id="0561a-204">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="0561a-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0561a-205">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="0561a-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0561a-206">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="0561a-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
