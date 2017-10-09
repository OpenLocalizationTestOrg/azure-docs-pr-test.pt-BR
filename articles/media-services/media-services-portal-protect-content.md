---
title: "políticas de proteção de conteúdo aaaConfiguring usando Olá portal do Azure | Microsoft Docs"
description: "Este artigo demonstra como toouse Olá políticas de proteção de conteúdo tooconfigure portal do Azure. Olá artigo também mostra como a criptografia dinâmica tooenable para seus ativos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="ab7cd-104">Configurando políticas de proteção de conteúdo usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ab7cd-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="ab7cd-105">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="ab7cd-106">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="ab7cd-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ab7cd-107">Overview</span></span>
<span data-ttu-id="ab7cd-108">Microsoft Azure Media Services (AMS) permite que você toosecure sua mídia do tempo de saudação deixa o computador por meio de armazenamento, processamento e entrega.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="ab7cd-109">Serviços de mídia permitem toodeliver seu conteúdo criptografado dinamicamente com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits), criptografia comum (CENC) usando PlayReady e/ou Widevine DRM e FairPlay da Apple.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="ab7cd-110">AMS fornece um serviço para distribuir licenças do DRM e clientes de tooauthorized chaves não criptografada AES.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="ab7cd-111">Hello portal do Azure permite que você toocreate um **diretiva de autorização de chave/licença** para todos os tipos de criptografia.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="ab7cd-112">Este artigo demonstra como tooconfigure conteúdo políticas de proteção com hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="ab7cd-113">Olá artigo também mostra como ativos de tooyour tooapply criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="ab7cd-114">Se você usou as políticas de proteção do hello toocreate de portal clássico do Azure, as políticas de saudação podem não aparecer no hello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="ab7cd-115">No entanto, todos os Olá antigo políticas ainda existe.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="ab7cd-116">Você pode examiná-los usando Olá SDK do Azure Media Services .NET ou hello [Azure-Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) ferramenta (políticas de saudação toosee, com o botão direito no ativo de saudação -> exibição informações (F4) -> clique na guia -> chaves de conteúdo Clique na chave de saudação).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="ab7cd-117">Se você quiser tooencrypt seu ativo usando as novas políticas, configurá-los com hello portal do Azure, clique em Salvar e reaplicar criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="ab7cd-118">Iniciar a configuração da proteção de conteúdo</span><span class="sxs-lookup"><span data-stu-id="ab7cd-118">Start configuring content protection</span></span>
<span data-ttu-id="ab7cd-119">toouse Olá portal toostart, configurando a proteção de conteúdo, conta tooyour global AMS, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab7cd-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="ab7cd-120">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="ab7cd-121">Selecione **Configurações** > **Proteção de conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-121">Select **Settings** > **Content protection**.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="ab7cd-123">política de autorização de chave/licença</span><span class="sxs-lookup"><span data-stu-id="ab7cd-123">Key/license authorization policy</span></span>
<span data-ttu-id="ab7cd-124">O AMS oferece várias maneiras de autenticar os usuários que fazem solicitações de licença ou chave.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="ab7cd-125">política de autorização da chave de conteúdo Olá deve ser configurada por você e cumprida pelo cliente para Olá chave ou a licença toobe toohello delived cliente.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="ab7cd-126">Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: **abrir** ou **token** restrição.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="ab7cd-127">Hello portal do Azure permite que você toocreate um **diretiva de autorização de chave/licença** para todos os tipos de criptografia.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="ab7cd-128">Aberto</span><span class="sxs-lookup"><span data-stu-id="ab7cd-128">Open</span></span>
<span data-ttu-id="ab7cd-129">Restrição aberta significa que o sistema de saudação distribuirá Olá tooanyone chave que faz uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="ab7cd-130">Essa restrição pode ser útil para o teste.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="ab7cd-131">Token</span><span class="sxs-lookup"><span data-stu-id="ab7cd-131">Token</span></span>
<span data-ttu-id="ab7cd-132">política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="ab7cd-133">Serviços de mídia oferece suporte a tokens no formato do Simple Web Tokens (SWT) hello e JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="ab7cd-134">Os serviços de mídia não fornecem Secure Token Services.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="ab7cd-135">Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="ab7cd-136">Olá STS deve ser configurado toocreate um token assinado com hello especificado chave e emitir declarações que você especificou na configuração de restrição de token hello.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="ab7cd-137">Serviços de mídia Olá serviço de entrega de chave retornará Olá solicitado hello e chave (ou licença) cliente toohello se Olá token for válido declarações em Olá token correspondam às configuradas para chave hello (ou licença).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="ab7cd-138">Ao configurar a política de restrição de token do hello, você deve especificar parâmetros de público-alvo, emissor e chave de verificação primária hello.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="ab7cd-139">chave de verificação primária Olá contém Olá chave que Olá token foi assinado com, o emissor é Olá serviço de token seguro que emite o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="ab7cd-140">público Hello (às vezes chamado de escopo) descreve a intenção de saudação do token de saudação ou token de saudação do recurso de saudação autoriza o acesso ao.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="ab7cd-141">Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="ab7cd-143">Modelo de direitos do PlayReady</span><span class="sxs-lookup"><span data-stu-id="ab7cd-143">PlayReady rights template</span></span>
<span data-ttu-id="ab7cd-144">Para obter informações detalhadas sobre o modelo de direitos Olá PlayReady, consulte [visão geral do modelo de licença do Media Services PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="ab7cd-145">Não persistente</span><span class="sxs-lookup"><span data-stu-id="ab7cd-145">Non persistent</span></span>
<span data-ttu-id="ab7cd-146">Se você configurar a licença como não persistente, ele só é mantido na memória enquanto player hello está usando a licença de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="ab7cd-148">Persistente</span><span class="sxs-lookup"><span data-stu-id="ab7cd-148">Persistent</span></span>
<span data-ttu-id="ab7cd-149">Se você configurar a licença hello como persistente, ele será salvo no armazenamento persistente no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="ab7cd-151">Modelo de direitos do Widevine</span><span class="sxs-lookup"><span data-stu-id="ab7cd-151">Widevine rights template</span></span>
<span data-ttu-id="ab7cd-152">Para obter informações detalhadas sobre o modelo de direitos de Widevine hello, consulte [visão geral do modelo de licença Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="ab7cd-153">Basic</span><span class="sxs-lookup"><span data-stu-id="ab7cd-153">Basic</span></span>
<span data-ttu-id="ab7cd-154">Quando você seleciona **básica**, Olá modelo será criado com todos os valores padrões.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="ab7cd-155">Avançado</span><span class="sxs-lookup"><span data-stu-id="ab7cd-155">Advanced</span></span>
<span data-ttu-id="ab7cd-156">Para obter uma explicação detalhada sobre a opção avançada das configurações do Widevine, consulte [este](media-services-widevine-license-template-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="ab7cd-158">Configuração do FairPlay</span><span class="sxs-lookup"><span data-stu-id="ab7cd-158">FairPlay configuration</span></span>
<span data-ttu-id="ab7cd-159">tooenable FairPlay criptografia, necessárias tooprovide Olá certificado do aplicativo e a chave de segredo do aplicativo (SOLICITAR) por meio de saudação opção de configuração FairPlay.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="ab7cd-160">Para obter informações detalhadas sobre a configuração e os requisitos do FairPlay, consulte [este](media-services-protect-hls-with-fairplay.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="ab7cd-162">Aplicar o ativo de tooyour criptografia dinâmica</span><span class="sxs-lookup"><span data-stu-id="ab7cd-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="ab7cd-163">tootake vantagem da criptografia dinâmica, você precisa de tooencode seu arquivo de origem em um conjunto de arquivos MP4 com taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="ab7cd-164">Selecione um ativo que você deseja tooencrypt</span><span class="sxs-lookup"><span data-stu-id="ab7cd-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="ab7cd-165">Selecione de todos os seus ativos, toosee **configurações** > **ativos**.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="ab7cd-167">Criptografar com AES ou DRM</span><span class="sxs-lookup"><span data-stu-id="ab7cd-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="ab7cd-168">Depois de pressionar **Criptografar** em um ativo, você verá duas opções: **AES** ou **DRM**.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="ab7cd-169">AES</span><span class="sxs-lookup"><span data-stu-id="ab7cd-169">AES</span></span>
<span data-ttu-id="ab7cd-170">A criptografia da chave de limpeza do AES será habilitada em todos os protocolos de streaming: Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="ab7cd-172">DRM</span><span class="sxs-lookup"><span data-stu-id="ab7cd-172">DRM</span></span>
<span data-ttu-id="ab7cd-173">Quando você seleciona Olá DRM guia, você verá diferentes opções de políticas de proteção de conteúdo (que você deve ter configurado agora) + um conjunto de protocolos de streaming.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="ab7cd-174">**PlayReady e Widevine com o MPEG-DASH** - irão criptografar dinamicamente seu fluxo MPEG DASH com os DRMs do PlayReady e do Widevine.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="ab7cd-175">**PlayReady e Widevine com o MPEG-DASH+ FairPlay com HLS** - irão criptografar dinamicamente seu fluxo MPEG DASH com os DRMs do PlayReady e do Widevine.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="ab7cd-176">Também irão criptografar seus fluxos HLS com o FairPlay.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="ab7cd-177">**PlayReady somente com Smooth Streaming, HLS e MPEG-DASH** - irão criptografar dinamicamente o Smooth Streaming, HLS e fluxos MPEG-DASH com o DRM do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="ab7cd-178">**Widevine apenas com MPEG-DASH** - irá criptografar dinamicamente seu MPEG-DASH com o DRM do Widevine.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="ab7cd-179">**FairPlay apenas com HLS** - irá criptografar dinamicamente seu fluxo HLS com o FairPlay.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="ab7cd-180">tooenable FairPlay criptografia, necessárias tooprovide Olá certificado do aplicativo e a chave de segredo do aplicativo (SOLICITAR) por meio de saudação opção de configuração de FairPlay da folha de configurações de proteção de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="ab7cd-182">Depois de fazer a seleção de criptografia hello, pressione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="ab7cd-183">Se você estiver planejando tooplay um AES criptografado HLS no Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="ab7cd-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab7cd-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab7cd-184">Next steps</span></span>
<span data-ttu-id="ab7cd-185">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="ab7cd-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ab7cd-186">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ab7cd-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

