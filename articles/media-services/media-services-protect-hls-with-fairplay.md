---
title: "aaaProtect de conteúdo HLS com o Microsoft PlayReady ou Apple FairPlay - Azure | Microsoft Docs"
description: "Este tópico fornece uma visão geral e mostra como toouse Azure Media Services toodynamically criptografar conteúdo HTTP Live Streaming (HLS) com FairPlay da Apple. Ele também mostra toouse Olá Media Services licenciar toodeliver do serviço de entrega tooclients de licenças FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="0347b-104">Proteger o conteúdo do HLS com o Apple FairPlay ou Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="0347b-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="0347b-105">Habilita de serviços de mídia do Azure toodynamically você criptografar seu conteúdo HTTP Live Streaming (HLS) usando Olá formatos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0347b-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="0347b-106">**Chave de limpeza do envelope AES-128**</span><span class="sxs-lookup"><span data-stu-id="0347b-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="0347b-107">Olá parte inteira é criptografado usando Olá **CBC AES-128** modo.</span><span class="sxs-lookup"><span data-stu-id="0347b-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="0347b-108">descriptografia de saudação do fluxo de saudação é suportada pelo player OS X e iOS nativamente.</span><span class="sxs-lookup"><span data-stu-id="0347b-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="0347b-109">Para saber mais, confira [Uso da criptografia dinâmica AES-128 e serviço de distribuição de chaves](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="0347b-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="0347b-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="0347b-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="0347b-111">Olá individual vídeo e áudio exemplos são criptografados usando Olá **CBC AES-128** modo.</span><span class="sxs-lookup"><span data-stu-id="0347b-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="0347b-112">**Streaming de FairPlay** (FPS) está integrado ao Olá sistemas operacionais de dispositivos com suporte nativo no iOS e Apple TV.</span><span class="sxs-lookup"><span data-stu-id="0347b-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="0347b-113">Safari nos X permite FPS usando o suporte à interface de extensões de mídia criptografados (EME) hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="0347b-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="0347b-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="0347b-115">Olá, imagem a seguir mostra Olá **HLS + FairPlay ou PlayReady criptografia dinâmica** fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0347b-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagrama do fluxo de trabalho de criptografia dinâmica](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="0347b-117">Este tópico demonstra como toouse os serviços de mídia toodynamically criptografar o conteúdo HLS com FairPlay da Apple.</span><span class="sxs-lookup"><span data-stu-id="0347b-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="0347b-118">Ele também mostra toouse Olá Media Services licenciar toodeliver do serviço de entrega tooclients de licenças FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0347b-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="0347b-119">Se também desejar tooencrypt o HLS conteúdo com PlayReady, você precisa toocreate uma chave de conteúdo comum e associá-lo com seu ativo.</span><span class="sxs-lookup"><span data-stu-id="0347b-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="0347b-120">Você também precisa política de autorização tooconfigure Olá da chave de conteúdo, conforme descrito em [criptografia comum dinâmica do PlayReady usando](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="0347b-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="0347b-121">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="0347b-121">Requirements and considerations</span></span>

<span data-ttu-id="0347b-122">a seguir Olá é necessária ao usar os serviços de mídia toodeliver que HLS criptografado com FairPlay e toodeliver FairPlay licenças:</span><span class="sxs-lookup"><span data-stu-id="0347b-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="0347b-123">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0347b-123">An Azure account.</span></span> <span data-ttu-id="0347b-124">Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0347b-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="0347b-125">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="0347b-125">A Media Services account.</span></span> <span data-ttu-id="0347b-126">toocreate um, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0347b-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="0347b-127">Inscreva-se no [Programa de Desenvolvimento da Apple](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="0347b-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="0347b-128">Apple requer saudação do hello proprietário do conteúdo tooobtain [pacote de implantação](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="0347b-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="0347b-129">Estado que você já implementou módulo de segurança de chave (KSM) com os serviços de mídia, e que você está solicitando o pacote FPS final hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="0347b-130">Há instruções Olá FPS final toogenerate certificação do pacote e obter Olá chave de segredo do aplicativo (SOLICITAR).</span><span class="sxs-lookup"><span data-stu-id="0347b-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="0347b-131">Use o peça tooconfigure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0347b-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="0347b-132">SDK do .NET dos Serviços de Mídia do Azure na versão **3.6.0** ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0347b-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="0347b-133">Olá coisas a seguir deve ser definido no lado de distribuição de chaves dos serviços de mídia:</span><span class="sxs-lookup"><span data-stu-id="0347b-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="0347b-134">**Certificado do aplicativo (AC)**: Este é um arquivo. pfx que contém a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="0347b-135">Você cria esse arquivo e o criptografa com uma senha.</span><span class="sxs-lookup"><span data-stu-id="0347b-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="0347b-136">Quando você configurar uma política de distribuição de chaves, você deve fornecer esse arquivo. pfx hello e a senha no formato Base64.</span><span class="sxs-lookup"><span data-stu-id="0347b-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="0347b-137">Olá, as etapas a seguir descreve como toogenerate um certificado. pfx do arquivo para FairPlay:</span><span class="sxs-lookup"><span data-stu-id="0347b-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="0347b-138">Instale o OpenSSL de https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="0347b-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="0347b-139">Vá toohello pasta onde estão os certificados de FairPlay hello e outros arquivos fornecidos pela Apple.</span><span class="sxs-lookup"><span data-stu-id="0347b-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="0347b-140">Execute Olá comando a seguir na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="0347b-141">Isso converte hello. cer tooa. PEM arquivo.</span><span class="sxs-lookup"><span data-stu-id="0347b-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="0347b-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="0347b-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="0347b-143">Execute Olá comando a seguir na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="0347b-144">Isso converte hello. PEM tooa. pfx arquivo com a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="0347b-145">senha Olá para o arquivo. pfx de hello, em seguida, é solicitada pelo OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="0347b-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="0347b-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="0347b-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="0347b-147">**Senha do certificado do aplicativo**: senha Olá para criar o arquivo. pfx de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="0347b-148">**ID da senha de aplicativo Cert**: você deve carregar senha hello, semelhante toohow carregar outras chaves de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="0347b-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="0347b-149">Saudação de uso **ContentKeyType.FairPlayPfxPassword** Olá de tooget valor de enum ID de serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="0347b-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="0347b-150">Este é o que precisam toouse dentro de opção de política de distribuição de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="0347b-151">**iv**: é um valor aleatório de 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="0347b-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="0347b-152">Ele deve corresponder Olá iv na política de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="0347b-153">Gerar Olá iv e colocá-la em dois lugares: política de distribuição Olá ativo e opção de política de distribuição de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="0347b-154">**Peça**: essa chave é recebida quando você gerar certificação Olá usando o portal do desenvolvedor Apple Olá.</span><span class="sxs-lookup"><span data-stu-id="0347b-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="0347b-155">Cada equipe de desenvolvimento receberá uma ASK exclusiva.</span><span class="sxs-lookup"><span data-stu-id="0347b-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="0347b-156">Salvar uma cópia do hello peça e armazená-lo em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="0347b-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="0347b-157">Você precisará tooconfigure peça como FairPlayAsk tooMedia serviços mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0347b-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="0347b-158">**ID da ASK**: essa ID é obtida quando você faz upload da ASK nos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="0347b-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="0347b-159">Você deve carregar peça usando Olá **ContentKeyType.FairPlayAsk** valor de enumeração.</span><span class="sxs-lookup"><span data-stu-id="0347b-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="0347b-160">Como resultado de Olá Olá ID de serviços de mídia será retornado e isso é o que deve ser usado ao configurar a opção de política de distribuição de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="0347b-161">Olá itens a seguir devem ser definidos por saudação do lado do cliente FPS:</span><span class="sxs-lookup"><span data-stu-id="0347b-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="0347b-162">**Certificado do aplicativo (AC)**: Este é um arquivo de.cer/.der que contém a chave pública do hello, sistema operacional no qual Olá usa tooencrypt alguns carga.</span><span class="sxs-lookup"><span data-stu-id="0347b-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="0347b-163">Serviços de mídia precisa tooknow sobre ele porque ela é necessária pelo player hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="0347b-164">serviço de distribuição de chaves Olá descriptografa usando a chave privada correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="0347b-165">tooplay um fluxo criptografado FairPlay, obter uma peça real primeiro e, em seguida, gerar um certificado real.</span><span class="sxs-lookup"><span data-stu-id="0347b-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="0347b-166">Esse processo cria três partes:</span><span class="sxs-lookup"><span data-stu-id="0347b-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="0347b-167">arquivo .der</span><span class="sxs-lookup"><span data-stu-id="0347b-167">.der file</span></span>
  * <span data-ttu-id="0347b-168">arquivo .pfx</span><span class="sxs-lookup"><span data-stu-id="0347b-168">.pfx file</span></span>
  * <span data-ttu-id="0347b-169">senha para. Olá pfx</span><span class="sxs-lookup"><span data-stu-id="0347b-169">password for hello .pfx</span></span>

<span data-ttu-id="0347b-170">os seguintes clientes Hello suportam HLS com **CBC AES-128** criptografia: Safari nos X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="0347b-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="0347b-171">Configurar a criptografia dinâmica do FairPlay e os serviços de distribuição de licenças</span><span class="sxs-lookup"><span data-stu-id="0347b-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="0347b-172">Olá seguem etapas gerais para proteger seus ativos com FairPlay usando o serviço de entrega de licença de serviços de mídia Olá e também com o uso de criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="0347b-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="0347b-173">Criar um ativo e carregar arquivos no ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="0347b-174">Codifica o ativo de saudação que contenha Olá arquivo toohello taxa de bits adaptável que MP4 definido.</span><span class="sxs-lookup"><span data-stu-id="0347b-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="0347b-175">Criar uma chave de conteúdo e associá-lo com ativo Olá codificado.</span><span class="sxs-lookup"><span data-stu-id="0347b-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="0347b-176">Configure a política de autorização da chave de saudação conteúdo.</span><span class="sxs-lookup"><span data-stu-id="0347b-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="0347b-177">Especifique Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="0347b-177">Specify hello following:</span></span>

   * <span data-ttu-id="0347b-178">método de entrega da saudação (nesse caso, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="0347b-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="0347b-179">a configuração de opções de política do FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0347b-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="0347b-180">Para obter detalhes sobre como tooconfigure FairPlay, consulte Olá **ConfigureFairPlayPolicyOptions()** método no exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="0347b-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0347b-181">Normalmente, você desejaria tooconfigure FairPlay política opções apenas uma vez, porque você terá apenas um conjunto de uma certificação e uma peça.</span><span class="sxs-lookup"><span data-stu-id="0347b-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="0347b-182">Restrições (abertas ou token).</span><span class="sxs-lookup"><span data-stu-id="0347b-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="0347b-183">Informações específicas toohello entrega de chave tipo que define como chave Olá é entregue toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="0347b-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="0347b-184">Configure a política de distribuição de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="0347b-185">configuração de política de distribuição de saudação inclui:</span><span class="sxs-lookup"><span data-stu-id="0347b-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="0347b-186">protocolo de entrega da saudação (HLS).</span><span class="sxs-lookup"><span data-stu-id="0347b-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="0347b-187">tipo de saudação de criptografia dinâmica (criptografia CBC comum).</span><span class="sxs-lookup"><span data-stu-id="0347b-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="0347b-188">Olá URL de aquisição de licença.</span><span class="sxs-lookup"><span data-stu-id="0347b-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0347b-189">Se você quiser toodeliver um fluxo que é criptografado com FairPlay e outro sistema de gerenciamento de direitos digitais (DRM), você tem políticas de entrega separada tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="0347b-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="0347b-190">Um tooconfigure IAssetDeliveryPolicy Streaming adaptável dinâmico sobre HTTP (traço) com o Common Encryption (CENC) (PlayReady + Widevine) e Smooth com PlayReady</span><span class="sxs-lookup"><span data-stu-id="0347b-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="0347b-191">Outro IAssetDeliveryPolicy tooconfigure FairPlay para HLS</span><span class="sxs-lookup"><span data-stu-id="0347b-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="0347b-192">Crie um tooget de localizador OnDemand uma URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="0347b-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="0347b-193">Usar a distribuição de chaves do FairPlay para aplicativos de player</span><span class="sxs-lookup"><span data-stu-id="0347b-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="0347b-194">Você pode desenvolver aplicativos player usando o SDK do iOS hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="0347b-195">toobe capaz de tooplay FairPlay conteúdo, você tem protocolo de intercâmbio de licença tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="0347b-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="0347b-196">Esse protocolo não é especificado pela Apple.</span><span class="sxs-lookup"><span data-stu-id="0347b-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="0347b-197">É o aplicativo tooeach como entrega de chave toosend solicitações.</span><span class="sxs-lookup"><span data-stu-id="0347b-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="0347b-198">Olá serviço de entrega de chave do Media Services FairPlay espera Olá SPC toocome como uma mensagem de post codificados www-form-url, em Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="0347b-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="0347b-199">Player de mídia do Azure não dá suporte a reprodução FairPlay imediato saudação.</span><span class="sxs-lookup"><span data-stu-id="0347b-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="0347b-200">tooget FairPlay reprodução no MAC OS X, obter reprodutor da amostra de saudação do hello conta de desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="0347b-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="0347b-201">URLs de streaming</span><span class="sxs-lookup"><span data-stu-id="0347b-201">Streaming URLs</span></span>
<span data-ttu-id="0347b-202">Se seu ativo foi criptografado com DRM de mais de um, você deve usar uma marca de criptografia na URL de streaming de saudação: (formato = 'm3u8-aapl', criptografia = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="0347b-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="0347b-203">Olá considerações a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="0347b-203">hello following considerations apply:</span></span>

* <span data-ttu-id="0347b-204">Pode ser especificado apenas zero ou um tipo de criptografia.</span><span class="sxs-lookup"><span data-stu-id="0347b-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="0347b-205">tipo de criptografia de saudação não tem toobe especificado na URL de saudação se apenas uma criptografia foi aplicada toohello ativo.</span><span class="sxs-lookup"><span data-stu-id="0347b-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="0347b-206">tipo de criptografia Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0347b-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="0347b-207">Olá seguintes tipos de criptografia pode ser especificada:</span><span class="sxs-lookup"><span data-stu-id="0347b-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="0347b-208">**cenc**: criptografia comum (PlayReady ou Widevine)</span><span class="sxs-lookup"><span data-stu-id="0347b-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="0347b-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="0347b-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="0347b-210">**cbc**: criptografia de envelope AES</span><span class="sxs-lookup"><span data-stu-id="0347b-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0347b-211">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0347b-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="0347b-212">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0347b-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="0347b-213">Adicionar Olá elementos a seguir muito**appSettings** definido no seu arquivo App. config:</span><span class="sxs-lookup"><span data-stu-id="0347b-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="0347b-214">Exemplo</span><span class="sxs-lookup"><span data-stu-id="0347b-214">Example</span></span>

<span data-ttu-id="0347b-215">saudação de exemplo a seguir demonstra Olá capacidade toouse toodeliver de serviços de mídia seu conteúdo criptografado com FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0347b-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="0347b-216">Essa funcionalidade foi introduzida no hello Azure Media Services SDK para .NET versão 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="0347b-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="0347b-217">Substitua o código de saudação no arquivo Program.cs pelo código Olá mostrado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="0347b-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="0347b-218">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0347b-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0347b-219">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="0347b-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0347b-220">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="0347b-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="0347b-221">Certifique-se de que variáveis de tooupdate toopoint toofolders onde se encontram os arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="0347b-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="0347b-222">Próximas etapas: roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="0347b-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0347b-223">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="0347b-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
