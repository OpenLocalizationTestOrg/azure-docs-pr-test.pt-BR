---
title: "aaaConfigure Olá NewTek TriCaster codificador toosend uma transmissão ao vivo de taxa de bits única | Microsoft Docs"
description: "Este tópico mostra como Olá tooconfigure Tricaster canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo."
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
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="6c6b8-103">Use Olá NewTek TriCaster codificador toosend uma transmissão ao vivo de taxa de bits única</span><span class="sxs-lookup"><span data-stu-id="6c6b8-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c6b8-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="6c6b8-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="6c6b8-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="6c6b8-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="6c6b8-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="6c6b8-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="6c6b8-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="6c6b8-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="6c6b8-108">Este tópico mostra como Olá tooconfigure [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) canais ao vivo codificador toosend uma taxa de bits única fluxo tooAMS que são habilitados para codificação ao vivo.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="6c6b8-109">Para obter mais informações, consulte [trabalhando com canais que é habilitado tooPerform Live codificação com o Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="6c6b8-110">Este tutorial mostra como toomanage Azure Media Services (AMS) com a ferramenta Gerenciador de serviços na mídia do Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="6c6b8-111">Essa ferramenta é executada apenas em PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="6c6b8-112">Se você estiver usando o Mac ou Linux, use Olá toocreate portal do Azure [canais](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programas](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6c6b8-113">Quando usar Tricaster para envio em uma contribuição feed tooAMS canais que são habilitados para codificação ao vivo, pode haver problemas de áudio/vídeo em seu evento ao vivo se você usar determinados recursos do Tricaster, como Recortar entre feeds de rápida ou alternância de slates .</span><span class="sxs-lookup"><span data-stu-id="6c6b8-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="6c6b8-114">Olá AMS equipe está trabalhando para corrigir esses problemas, até lá, é recomendável não toouse esses recursos.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="6c6b8-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6c6b8-115">Prerequisites</span></span>
* [<span data-ttu-id="6c6b8-116">Criar uma conta dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="6c6b8-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="6c6b8-117">Verifique se há um Ponto de Extremidade de Streaming em execução.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="6c6b8-118">Para obter mais informações, veja [Gerenciar Pontos de Extremidade de Transmissão em uma conta de Serviços de Mídia](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="6c6b8-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="6c6b8-119">Instale a versão mais recente Olá de saudação [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="6c6b8-120">Inicie a ferramenta hello e conecte-se a conta tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="6c6b8-121">Dicas</span><span class="sxs-lookup"><span data-stu-id="6c6b8-121">Tips</span></span>
* <span data-ttu-id="6c6b8-122">Sempre que possível, use uma conexão de Internet com fio.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="6c6b8-123">Uma boa regra prática ao determinar os requisitos de largura de banda é toodouble Olá streaming taxas de bits.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="6c6b8-124">Embora não seja um requisito obrigatório, ela ajuda a reduzir o impacto de saudação do congestionamento da rede.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="6c6b8-125">Ao usar codificadores baseados em software, feche todos os programas desnecessários.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="6c6b8-126">Criar um canal</span><span class="sxs-lookup"><span data-stu-id="6c6b8-126">Create a channel</span></span>
1. <span data-ttu-id="6c6b8-127">Na ferramenta AMSE hello, navegar toohello **Live** guia e clique com o botão direito na área de canal hello.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="6c6b8-128">Selecione **Criar canal...**</span><span class="sxs-lookup"><span data-stu-id="6c6b8-128">Select **Create channel…**</span></span> <span data-ttu-id="6c6b8-129">no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="6c6b8-131">Especifique um nome de canal, Olá campo de descrição é opcional.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="6c6b8-132">Em configurações de canal, selecione **padrão** para Olá opção codificação ao vivo, com hello entrada do protocolo definido muito**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="6c6b8-133">Você pode deixar todas as outras configurações como estão.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="6c6b8-134">Verifique se Olá **início Olá novo canal agora** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="6c6b8-135">Clique em **Criar Canal**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="6c6b8-137">canal Olá pode levar até 20 minutos toostart.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="6c6b8-138">Enquanto o canal Olá é iniciado, você pode [configurar codificador Olá](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c6b8-139">Lembre-se de que a cobrança começa assim que o Canal entra em um estado pronto.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="6c6b8-140">Para obter mais informações, veja [Estados do canal](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="6c6b8-141"><a id=configure_tricaster_rtmp></a>Configurar Olá NewTek TriCaster codificador</span><span class="sxs-lookup"><span data-stu-id="6c6b8-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="6c6b8-142">Neste tutorial Olá seguintes configurações de saída são usadas.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="6c6b8-143">Olá restante desta seção descreve etapas de configuração em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="6c6b8-144">**Vídeo**:</span><span class="sxs-lookup"><span data-stu-id="6c6b8-144">**Video**:</span></span>

* <span data-ttu-id="6c6b8-145">Codec: H.264</span><span class="sxs-lookup"><span data-stu-id="6c6b8-145">Codec: H.264</span></span>
* <span data-ttu-id="6c6b8-146">Perfil: Alto (nível 4.0)</span><span class="sxs-lookup"><span data-stu-id="6c6b8-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="6c6b8-147">Taxa de bits: 5.000 kbps</span><span class="sxs-lookup"><span data-stu-id="6c6b8-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="6c6b8-148">Quadro-chave: 2 segundos (60 segundos)</span><span class="sxs-lookup"><span data-stu-id="6c6b8-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="6c6b8-149">Taxa de quadros: 30</span><span class="sxs-lookup"><span data-stu-id="6c6b8-149">Frame Rate: 30</span></span>

<span data-ttu-id="6c6b8-150">**Áudio**:</span><span class="sxs-lookup"><span data-stu-id="6c6b8-150">**Audio**:</span></span>

* <span data-ttu-id="6c6b8-151">Codec: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="6c6b8-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="6c6b8-152">Taxa de bits: 192 kbps</span><span class="sxs-lookup"><span data-stu-id="6c6b8-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="6c6b8-153">Taxa de amostragem: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="6c6b8-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="6c6b8-154">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="6c6b8-154">Configuration steps</span></span>
1. <span data-ttu-id="6c6b8-155">Crie um novo projeto do **NewTek TriCaster** dependendo de qual fonte de entrada de vídeo está sendo usada.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="6c6b8-156">Uma vez no projeto, localize Olá **fluxo** botão e, em seguida, clique em Olá engrenagem ícone próximo tooit tooaccess Olá fluxo configuração menu.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="6c6b8-158">Depois que o menu de saudação for aberto, clique em **novo** sob o título de Conexão hello.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="6c6b8-159">Quando solicitado para o tipo de conexão hello, selecione **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="6c6b8-161">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-161">Click **OK**.</span></span>
5. <span data-ttu-id="6c6b8-162">Um perfil de FMLE agora pode ser importado clicando Olá seta do menu suspenso em **perfil Streaming** e navegar muito**procurar**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="6c6b8-164">Navegue toowhere Olá configurado FMLE perfil foi salvo.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="6c6b8-165">Selecione-o e pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="6c6b8-166">Quando o perfil de saudação é carregado, continue toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="6c6b8-167">Obter URL de entrada do canal de saudação em ordem tooassign-toohello Tricaster **ponto de extremidade de RTMP**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="6c6b8-168">Navegue ferramenta AMSE toohello back e verificar o status de conclusão de canal hello.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="6c6b8-169">Depois que o estado Olá mudou de **iniciando** muito**executando**, você pode obter a URL de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="6c6b8-170">Quando estiver executando o canal Olá, clique direito no nome do canal hello, navegue para baixo toohover **copiar a URL de entrada tooclipboard** e, em seguida, selecione **URL de entrada primária**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="6c6b8-172">Colar essas informações no hello **local** campo em **Flash Server** no projeto de Tricaster hello.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="6c6b8-173">Também atribuir um nome de fluxo em Olá **identificação do fluxo** campo.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="6c6b8-174">Se as informações de fluxo foi adicionadas o perfil FMLE toohello, ele também pode ser importado toothis seção clicando **importar configurações**, navegando toohello salvada FMLE perfil e clicando em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="6c6b8-175">campos de Flash Server relevantes Olá devem preencher com informações de saudação do FMLE.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="6c6b8-177">Quando terminar, clique em **Okey** na parte inferior da saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="6c6b8-178">Quando entradas de áudio e vídeo em Olá Tricaster estiverem prontas, iniciar streaming tooAMS clicando Olá **fluxo** botão.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="6c6b8-180">Antes de clicar em **fluxo**, você **deve** Certifique-se de que o canal de saudação está pronto.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="6c6b8-181">Além disso, certifique-se de não tooleave Olá canal em um estado pronto sem uma entrada contribuição feed por mais de > 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="6c6b8-182">Reprodução de teste</span><span class="sxs-lookup"><span data-stu-id="6c6b8-182">Test playback</span></span>
<span data-ttu-id="6c6b8-183">Navegue ferramenta AMSE toohello e clique com botão direito Olá canal toobe testado.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="6c6b8-184">No menu de hello, passe o mouse sobre **Olá reprodução visualização** e selecione **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="6c6b8-185">Se o fluxo de saudação aparece no player hello, codificador Olá foi tooAMS tooconnect configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="6c6b8-186">Se um erro é recebido, canal Olá precisará toobe redefinição e codificador configurações ajustadas.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="6c6b8-187">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="6c6b8-188">Criar um programa</span><span class="sxs-lookup"><span data-stu-id="6c6b8-188">Create a program</span></span>
1. <span data-ttu-id="6c6b8-189">Depois que a reprodução do canal for confirmada, crie um programa.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="6c6b8-190">Em Olá **Live** guia na ferramenta AMSE hello, clique com o botão direito na área de programa hello e selecione **criar um novo programa**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="6c6b8-192">Nomeie o programa hello e, se necessário, ajuste Olá **duração da janela de arquivo** (os horários de too4 padrões).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="6c6b8-193">Você também pode especificar um local de armazenamento ou deixe como saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="6c6b8-194">Verificar Olá **início Olá programa agora** caixa.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="6c6b8-195">Clique em **Criar Programa**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="6c6b8-196">A criação do programa leva menos tempo do que a criação do canal.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="6c6b8-197">Depois que o programa de hello está sendo executado, confirme a reprodução clique direito programa hello e navegando muito**reprodução Olá programas** e, em seguida, selecionando **com o Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="6c6b8-198">Depois de confirmar, clique com botão direito programa hello novamente e selecionar **copiar Olá URL de saída tooClipboard** (ou recuperar essas informações do hello **informações e configurações de programa** opção no menu de saudação).</span><span class="sxs-lookup"><span data-stu-id="6c6b8-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="6c6b8-199">Olá está agora pronto toobe inserido em um player ou público tooan distribuída ao vivo de exibição.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="6c6b8-200">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="6c6b8-200">Troubleshooting</span></span>
<span data-ttu-id="6c6b8-201">Consulte Olá [de solução de problemas](media-services-troubleshooting-live-streaming.md) tópico para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="6c6b8-202">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="6c6b8-202">Next step</span></span>
<span data-ttu-id="6c6b8-203">Revise os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="6c6b8-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c6b8-204">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6c6b8-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
