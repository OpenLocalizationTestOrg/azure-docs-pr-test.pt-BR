---
title: "Configurando as políticas de proteção de conteúdo com o portal do Azure | Microsoft Docs"
description: "Este artigo demonstra como usar o portal do Azure para configurar as políticas de proteção de conteúdo. O artigo também mostra como habilitar a criptografia dinâmica para seus ativos."
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
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="d961d-104">Configurando as políticas de proteção de conteúdo com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d961d-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="d961d-105">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d961d-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d961d-106">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d961d-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="d961d-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d961d-107">Overview</span></span>
<span data-ttu-id="d961d-108">Os Serviços de Mídia do Microsoft Azure (AMS) permitem proteger a mídia do momento em que ela deixa o computador e durante o armazenamento, processamento e entrega.</span><span class="sxs-lookup"><span data-stu-id="d961d-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="d961d-109">Os Serviços de Mídia permitem entregar o conteúdo criptografado dinamicamente com a criptografia AES (usando chaves de criptografia de 128 bits) e a CENC (criptografia comum) usando o PlayReady e/ou Widevine DRM e Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="d961d-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="d961d-110">O AMS fornece um serviço para entregar as licenças DRM e as chaves de limpeza AES aos clientes autorizados.</span><span class="sxs-lookup"><span data-stu-id="d961d-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="d961d-111">O portal do Azure permite que você crie uma **política de autorização de chave/licença** para todos os tipos de criptografias.</span><span class="sxs-lookup"><span data-stu-id="d961d-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="d961d-112">Este artigo demonstra como configurar as políticas de proteção de conteúdo com o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d961d-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="d961d-113">O artigo também mostra como aplicar a criptografia dinâmica em seus ativos.</span><span class="sxs-lookup"><span data-stu-id="d961d-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="d961d-114">Se você usou o portal clássico do Azure para criar políticas de proteção, as políticas poderão não aparecer no [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d961d-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d961d-115">No entanto, todas as antigas políticas ainda existirão.</span><span class="sxs-lookup"><span data-stu-id="d961d-115">However, all the old polices still exist.</span></span> <span data-ttu-id="d961d-116">Você pode examiná-las usando o SDK do .NET dos Serviços de Mídia do Azure ou a ferramenta [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) (para ver as políticas, clique com o botão direito no ativo -> Exibir informações (F4) -> clique na guia Chaves de conteúdo -> clique na chave).</span><span class="sxs-lookup"><span data-stu-id="d961d-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="d961d-117">Se você quiser criptografar seu ativo usando as novas políticas, configure-as com o portal do Azure, clique em Salvar e reaplique a criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="d961d-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="d961d-118">Iniciar a configuração da proteção de conteúdo</span><span class="sxs-lookup"><span data-stu-id="d961d-118">Start configuring content protection</span></span>
<span data-ttu-id="d961d-119">Para usar o portal para começar a configurar a proteção de conteúdo, global para sua conta AMS, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d961d-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="d961d-120">No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="d961d-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d961d-121">Selecione **Configurações** > **Proteção de conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="d961d-121">Select **Settings** > **Content protection**.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="d961d-123">política de autorização de chave/licença</span><span class="sxs-lookup"><span data-stu-id="d961d-123">Key/license authorization policy</span></span>
<span data-ttu-id="d961d-124">O AMS oferece várias maneiras de autenticar os usuários que fazem solicitações de licença ou chave.</span><span class="sxs-lookup"><span data-stu-id="d961d-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="d961d-125">A política de autorização da chave de conteúdo deve ser configurada por você e atendida pelo cliente para que a chave/licença seja entregue ao cliente.</span><span class="sxs-lookup"><span data-stu-id="d961d-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="d961d-126">A política de autorização de chave de conteúdo pode ter uma ou mais restrições de autorização: **aberta** ou **de token**.</span><span class="sxs-lookup"><span data-stu-id="d961d-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="d961d-127">O portal do Azure permite que você crie uma **política de autorização de chave/licença** para todos os tipos de criptografias.</span><span class="sxs-lookup"><span data-stu-id="d961d-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="d961d-128">Aberto</span><span class="sxs-lookup"><span data-stu-id="d961d-128">Open</span></span>
<span data-ttu-id="d961d-129">Restrição aberta significa que o sistema entregará a chave para qualquer pessoa que fizer uma solicitação de chave.</span><span class="sxs-lookup"><span data-stu-id="d961d-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="d961d-130">Essa restrição pode ser útil para o teste.</span><span class="sxs-lookup"><span data-stu-id="d961d-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="d961d-131">restrição</span><span class="sxs-lookup"><span data-stu-id="d961d-131">Token</span></span>
<span data-ttu-id="d961d-132">A política restrita do token deve ser acompanhada por um token emitido por um Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="d961d-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="d961d-133">Os serviços de mídia oferecem suporte a tokens no formato Simple Web Tokens (SWT) e no formato JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="d961d-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="d961d-134">Os serviços de mídia não fornecem Secure Token Services.</span><span class="sxs-lookup"><span data-stu-id="d961d-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="d961d-135">Você pode criar um STS personalizado ou usar o Microsoft Azure ACS para emitir tokens.</span><span class="sxs-lookup"><span data-stu-id="d961d-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="d961d-136">O STS deve ser configurado para criar um token assinado com as a chave especificada e declarações de emissão que você especificou na configuração de restrição do token.</span><span class="sxs-lookup"><span data-stu-id="d961d-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="d961d-137">O serviço de distribuição de chaves dos Serviços de Mídia retornará a chave de criptografia para o cliente se o token for válido e as declarações no token corresponderem àquelas configuradas para a chave (ou licença).</span><span class="sxs-lookup"><span data-stu-id="d961d-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="d961d-138">Ao configurar a política restrita do token, você deve especificar os parâmetros da chave de verificação primária, do emissor e do público-alvo.</span><span class="sxs-lookup"><span data-stu-id="d961d-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="d961d-139">A chave de verificação primária contém a chave que o token foi assinado, o emissor é o serviço de token seguro que emite o token.</span><span class="sxs-lookup"><span data-stu-id="d961d-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="d961d-140">A audiência (às vezes chamada de escopo) descreve a intenção do token ou o recurso que o token autoriza o acesso.</span><span class="sxs-lookup"><span data-stu-id="d961d-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="d961d-141">O serviço de distribuição de chaves dos serviços de mídia valida que esses valores no token correspondem aos valores no modelo.</span><span class="sxs-lookup"><span data-stu-id="d961d-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="d961d-143">Modelo de direitos do PlayReady</span><span class="sxs-lookup"><span data-stu-id="d961d-143">PlayReady rights template</span></span>
<span data-ttu-id="d961d-144">Para obter informações detalhadas sobre o modelo de direitos do PlayReady, consulte [Visão Geral do Modelo de Licença do PlayReady dos Serviços de Mídia](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d961d-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="d961d-145">Não persistente</span><span class="sxs-lookup"><span data-stu-id="d961d-145">Non persistent</span></span>
<span data-ttu-id="d961d-146">Se você configurar a licença como não persistente, ela só será mantida na memória enquanto o player estiver usando a licença.</span><span class="sxs-lookup"><span data-stu-id="d961d-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="d961d-148">Persistente</span><span class="sxs-lookup"><span data-stu-id="d961d-148">Persistent</span></span>
<span data-ttu-id="d961d-149">Se você configurar a licença como persistente, ela será salva no armazenamento persistente no cliente.</span><span class="sxs-lookup"><span data-stu-id="d961d-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="d961d-151">Modelo de direitos do Widevine</span><span class="sxs-lookup"><span data-stu-id="d961d-151">Widevine rights template</span></span>
<span data-ttu-id="d961d-152">Para obter informações detalhadas sobre o modelo de direitos do Widevine, consulte [Visão Geral do Modelo de Licença do Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d961d-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="d961d-153">Basic</span><span class="sxs-lookup"><span data-stu-id="d961d-153">Basic</span></span>
<span data-ttu-id="d961d-154">Quando você selecionar **Básico**, o modelo será criado com todos os valores padrões.</span><span class="sxs-lookup"><span data-stu-id="d961d-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="d961d-155">Avançado</span><span class="sxs-lookup"><span data-stu-id="d961d-155">Advanced</span></span>
<span data-ttu-id="d961d-156">Para obter uma explicação detalhada sobre a opção avançada das configurações do Widevine, consulte [este](media-services-widevine-license-template-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="d961d-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="d961d-158">Configuração do FairPlay</span><span class="sxs-lookup"><span data-stu-id="d961d-158">FairPlay configuration</span></span>
<span data-ttu-id="d961d-159">Para habilitar a criptografia do FairPlay, você precisa fornecer o Certificado do Aplicativo e a Chave de Segredo do Aplicativo (ASK) com a opção Configuração do FairPlay.</span><span class="sxs-lookup"><span data-stu-id="d961d-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="d961d-160">Para obter informações detalhadas sobre a configuração e os requisitos do FairPlay, consulte [este](media-services-protect-hls-with-fairplay.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d961d-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="d961d-162">Aplique a criptografia dinâmica em seu ativo</span><span class="sxs-lookup"><span data-stu-id="d961d-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="d961d-163">Para aproveitar a criptografia dinâmica, você precisa codificar o arquivo de origem em um conjunto de arquivos MP4 de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="d961d-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="d961d-164">Selecionar o ativo que você deseja criptografar</span><span class="sxs-lookup"><span data-stu-id="d961d-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="d961d-165">Para ver todos os seus ativos, selecione **Configurações** > **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="d961d-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="d961d-167">Criptografar com AES ou DRM</span><span class="sxs-lookup"><span data-stu-id="d961d-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="d961d-168">Depois de pressionar **Criptografar** em um ativo, você verá duas opções: **AES** ou **DRM**.</span><span class="sxs-lookup"><span data-stu-id="d961d-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="d961d-169">AES</span><span class="sxs-lookup"><span data-stu-id="d961d-169">AES</span></span>
<span data-ttu-id="d961d-170">A criptografia da chave de limpeza do AES será habilitada em todos os protocolos de streaming: Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="d961d-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="d961d-172">DRM</span><span class="sxs-lookup"><span data-stu-id="d961d-172">DRM</span></span>
<span data-ttu-id="d961d-173">Quando você selecionar a guia DRM, verá diferentes opções de políticas de proteção de conteúdo (que você deve ter configurado agora) + um conjunto de protocolos de streaming.</span><span class="sxs-lookup"><span data-stu-id="d961d-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="d961d-174">**PlayReady e Widevine com o MPEG-DASH** - irão criptografar dinamicamente seu fluxo MPEG DASH com os DRMs do PlayReady e do Widevine.</span><span class="sxs-lookup"><span data-stu-id="d961d-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="d961d-175">**PlayReady e Widevine com o MPEG-DASH+ FairPlay com HLS** - irão criptografar dinamicamente seu fluxo MPEG DASH com os DRMs do PlayReady e do Widevine.</span><span class="sxs-lookup"><span data-stu-id="d961d-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="d961d-176">Também irão criptografar seus fluxos HLS com o FairPlay.</span><span class="sxs-lookup"><span data-stu-id="d961d-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="d961d-177">**PlayReady somente com Smooth Streaming, HLS e MPEG-DASH** - irão criptografar dinamicamente o Smooth Streaming, HLS e fluxos MPEG-DASH com o DRM do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="d961d-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="d961d-178">**Widevine apenas com MPEG-DASH** - irá criptografar dinamicamente seu MPEG-DASH com o DRM do Widevine.</span><span class="sxs-lookup"><span data-stu-id="d961d-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="d961d-179">**FairPlay apenas com HLS** - irá criptografar dinamicamente seu fluxo HLS com o FairPlay.</span><span class="sxs-lookup"><span data-stu-id="d961d-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="d961d-180">Para habilitar a criptografia do FairPlay, você precisa fornecer o Certificado do Aplicativo e a Chave de Segredo do Aplicativo (ASK) com a opção Configuração do FairPlay da folha de configurações Proteção de Conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d961d-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="d961d-182">Após fazer a seleção da criptografia, pressione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d961d-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="d961d-183">Se você pretende executar um HLS criptografado para AES no Safari, visite [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="d961d-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d961d-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d961d-184">Next steps</span></span>
<span data-ttu-id="d961d-185">Examine os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="d961d-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d961d-186">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="d961d-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

