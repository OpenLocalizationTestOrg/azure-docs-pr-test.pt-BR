---
title: "Proteger o conteúdo do HLS com o Microsoft PlayReady ou o Apple FairPlay | Microsoft Docs"
description: "Este tópico fornece uma visão geral e mostra como usar os Serviços de Mídia do Azure para criptografar de forma dinâmica o seu conteúdo de HLS (HTTP Live Streaming) com o FairPlay da Apple. Ele também mostra como usar o serviço de distribuição de licença dos Serviços de Mídia para entregar licenças do FairPlay aos clientes."
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
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="98bec-104">Proteger o conteúdo do HLS com o Apple FairPlay ou Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="98bec-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="98bec-105">Os Serviços de Mídia do Azure permitem que você criptografe seu conteúdo de HLS (HTTP Live Streaming) de maneira dinâmica, usando os seguintes formatos:</span><span class="sxs-lookup"><span data-stu-id="98bec-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="98bec-106">**Chave de limpeza do envelope AES-128**</span><span class="sxs-lookup"><span data-stu-id="98bec-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="98bec-107">A parte inteira é criptografada usando o modo **AES-128 CBC**.</span><span class="sxs-lookup"><span data-stu-id="98bec-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="98bec-108">A descriptografia da transmissão tem suporte nativo do iOS e player OSX.</span><span class="sxs-lookup"><span data-stu-id="98bec-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="98bec-109">Para saber mais, confira [Uso da criptografia dinâmica AES-128 e serviço de distribuição de chaves](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="98bec-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="98bec-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="98bec-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="98bec-111">Os exemplos de áudio e vídeo individuais são criptografados usando o modo **AES-128 CBC**.</span><span class="sxs-lookup"><span data-stu-id="98bec-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="98bec-112">**FPS** (FairPlay Streaming) é integrado aos sistemas operacionais de dispositivos, com suporte nativo no iOS e na Apple TV.</span><span class="sxs-lookup"><span data-stu-id="98bec-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="98bec-113">O Safari no OS X habilita o FPS usando o suporte à interface EME (Extensões de Mídia Criptografada).</span><span class="sxs-lookup"><span data-stu-id="98bec-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="98bec-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="98bec-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="98bec-115">A imagem a seguir mostra o fluxo de trabalho da **criptografia dinâmica do HLS + FairPlay ou PlayReady**.</span><span class="sxs-lookup"><span data-stu-id="98bec-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagrama do fluxo de trabalho de criptografia dinâmica](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="98bec-117">Este tópico demonstra como usar os Serviços de Mídia para criptografar de forma dinâmica o conteúdo de HLS com o Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="98bec-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="98bec-118">Ele também mostra como usar o serviço de distribuição de licença dos Serviços de Mídia para entregar licenças do FairPlay aos clientes.</span><span class="sxs-lookup"><span data-stu-id="98bec-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="98bec-119">Se quiser criptografar o conteúdo do HLS com o PlayReady, você precisará criar uma chave de conteúdo comum e associá-la ao seu ativo.</span><span class="sxs-lookup"><span data-stu-id="98bec-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="98bec-120">Você também precisa configurar a política de autorização da chave de conteúdo, como descrito em [Uso da criptografia comum dinâmica PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="98bec-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="98bec-121">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="98bec-121">Requirements and considerations</span></span>

<span data-ttu-id="98bec-122">Veja a seguir o que é necessário ao usar os Serviços de Mídia para distribuir HLS criptografado com o FairPlay e distribuir licenças do FairPlay:</span><span class="sxs-lookup"><span data-stu-id="98bec-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="98bec-123">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="98bec-123">An Azure account.</span></span> <span data-ttu-id="98bec-124">Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="98bec-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="98bec-125">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="98bec-125">A Media Services account.</span></span> <span data-ttu-id="98bec-126">Para criar uma, confira [Criar uma conta dos Serviços de Mídia do Azure usando o portal do Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="98bec-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="98bec-127">Inscreva-se no [Programa de Desenvolvimento da Apple](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="98bec-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="98bec-128">A Apple exige que o proprietário do conteúdo obtenha o [pacote de implantação](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="98bec-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="98bec-129">Declare que você já implementou o KSM (Módulo de Segurança de Chave) com os Serviços de Mídia e que está solicitando o pacote final do FPS.</span><span class="sxs-lookup"><span data-stu-id="98bec-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="98bec-130">Há instruções no pacote final do FPS para gerar certificação e obter a ASK (Chave de Segredo do Aplicativo).</span><span class="sxs-lookup"><span data-stu-id="98bec-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="98bec-131">Você usa a ASK para configurar o FairPlay.</span><span class="sxs-lookup"><span data-stu-id="98bec-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="98bec-132">SDK do .NET dos Serviços de Mídia do Azure na versão **3.6.0** ou posterior.</span><span class="sxs-lookup"><span data-stu-id="98bec-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="98bec-133">Os seguintes itens devem ser definidos no lado de distribuição de chaves dos Serviços de Mídia:</span><span class="sxs-lookup"><span data-stu-id="98bec-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="98bec-134">**AC (Certificado do Aplicativo)**: trata-se de um arquivo .pfx que contém a chave privada.</span><span class="sxs-lookup"><span data-stu-id="98bec-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="98bec-135">Você cria esse arquivo e o criptografa com uma senha.</span><span class="sxs-lookup"><span data-stu-id="98bec-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="98bec-136">Ao configurar a política de distribuição de chaves, você deve fornecer a senha e o .pfx no formato Base64.</span><span class="sxs-lookup"><span data-stu-id="98bec-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="98bec-137">As etapas a seguir descrevem como gerar um arquivo de certificado .pfx para FairPlay:</span><span class="sxs-lookup"><span data-stu-id="98bec-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="98bec-138">Instale o OpenSSL de https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="98bec-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="98bec-139">Vá para a pasta onde se encontram o certificado FairPlay e outros arquivos enviados pela Apple.</span><span class="sxs-lookup"><span data-stu-id="98bec-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="98bec-140">Execute o comando a seguir na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="98bec-140">Run the following command from the command line.</span></span> <span data-ttu-id="98bec-141">Isso converte o arquivo .cer em um arquivo .pem.</span><span class="sxs-lookup"><span data-stu-id="98bec-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="98bec-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="98bec-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="98bec-143">Execute o comando a seguir na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="98bec-143">Run the following command from the command line.</span></span> <span data-ttu-id="98bec-144">Isso converte o arquivo .pem em um arquivo .pfx com a chave privada.</span><span class="sxs-lookup"><span data-stu-id="98bec-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="98bec-145">A senha para o arquivo .pfx é solicitada pelo OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="98bec-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="98bec-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="98bec-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="98bec-147">**Senha do Certificado do Aplicativo**: a senha para a criação do arquivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="98bec-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="98bec-148">**ID da senha do Certificado do Aplicativo**: você deve fazer upload da senha, de maneira semelhante a como faz upload de outras chaves dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="98bec-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="98bec-149">Use o valor de enumeração **ContentKeyType.FairPlayPfxPassword** para obter a ID dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="98bec-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="98bec-150">É necessário usá-la na opção de política de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="98bec-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="98bec-151">**iv**: é um valor aleatório de 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="98bec-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="98bec-152">Ele deve corresponder ao iv na política de distribuição de ativos.</span><span class="sxs-lookup"><span data-stu-id="98bec-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="98bec-153">Você gera o iv e o coloca em dois locais: na política de distribuição de ativos e na opção de política de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="98bec-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="98bec-154">**ASK**: essa chave é recebida quando você gera a certificação usando o portal do Desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="98bec-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="98bec-155">Cada equipe de desenvolvimento receberá uma ASK exclusiva.</span><span class="sxs-lookup"><span data-stu-id="98bec-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="98bec-156">Salve uma cópia da ASK e armazene-a em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="98bec-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="98bec-157">Você precisará configurar a ASK como FairPlayAsk nos Serviços de Mídia posteriormente.</span><span class="sxs-lookup"><span data-stu-id="98bec-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="98bec-158">**ID da ASK**: essa ID é obtida quando você faz upload da ASK nos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="98bec-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="98bec-159">Você deve fazer upload da ASK usando o valor de enumeração **ContentKeyType.FairPlayAsk**.</span><span class="sxs-lookup"><span data-stu-id="98bec-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="98bec-160">Como resultado, a ID dos Serviços de Mídia é retornada, que deve ser usada na configuração da opção de política de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="98bec-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="98bec-161">Os seguintes itens devem ser definidos pelo lado do cliente FPS:</span><span class="sxs-lookup"><span data-stu-id="98bec-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="98bec-162">**AC (Certificado do Aplicativo)**: trata-se de um arquivo .cer/.der que contém a chave pública que o sistema operacional usa para criptografar conteúdo.</span><span class="sxs-lookup"><span data-stu-id="98bec-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="98bec-163">Os Serviços de Mídia precisam ter conhecimento sobre ele, uma vez que ele é exibido pelo player.</span><span class="sxs-lookup"><span data-stu-id="98bec-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="98bec-164">O serviço de distribuição de chaves descriptografa-o usando a chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="98bec-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="98bec-165">Para reproduzir uma transmissão criptografada do FairPlay, obtenha a ASK real primeiro e, em seguida, gere um certificado real.</span><span class="sxs-lookup"><span data-stu-id="98bec-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="98bec-166">Esse processo cria três partes:</span><span class="sxs-lookup"><span data-stu-id="98bec-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="98bec-167">arquivo .der</span><span class="sxs-lookup"><span data-stu-id="98bec-167">.der file</span></span>
  * <span data-ttu-id="98bec-168">arquivo .pfx</span><span class="sxs-lookup"><span data-stu-id="98bec-168">.pfx file</span></span>
  * <span data-ttu-id="98bec-169">senha do .pfx</span><span class="sxs-lookup"><span data-stu-id="98bec-169">password for the .pfx</span></span>

<span data-ttu-id="98bec-170">Os clientes a seguir dão suporte ao HLS com a criptografia **AES-128 CBC**: Safari no OS X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="98bec-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="98bec-171">Configurar a criptografia dinâmica do FairPlay e os serviços de distribuição de licenças</span><span class="sxs-lookup"><span data-stu-id="98bec-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="98bec-172">Veja a seguir as etapas gerais para proteger seus ativos com o FairPlay usando o serviço de distribuição de licenças dos Serviços de Mídia e também usando a criptografia dinâmica.</span><span class="sxs-lookup"><span data-stu-id="98bec-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="98bec-173">Crie um ativo e faça upload dos arquivos no ativo.</span><span class="sxs-lookup"><span data-stu-id="98bec-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="98bec-174">Codifique o ativo que contém o arquivo para o conjunto de MP4 da taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="98bec-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="98bec-175">Crie uma chave de conteúdo e associe-a ao ativo codificado.</span><span class="sxs-lookup"><span data-stu-id="98bec-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="98bec-176">Configurar a política de autorização da chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="98bec-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="98bec-177">Especifique o seguinte:</span><span class="sxs-lookup"><span data-stu-id="98bec-177">Specify the following:</span></span>

   * <span data-ttu-id="98bec-178">O método de entrega (nesse caso, o FairPlay).</span><span class="sxs-lookup"><span data-stu-id="98bec-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="98bec-179">a configuração de opções de política do FairPlay.</span><span class="sxs-lookup"><span data-stu-id="98bec-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="98bec-180">Para obter detalhes sobre como configurar o FairPlay, confira o método **ConfigureFairPlayPolicyOptions()** no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="98bec-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98bec-181">Normalmente, convém configurar as opções de política do FairPlay apenas uma vez, visto que você terá apenas um conjunto de uma certificação e uma ASK.</span><span class="sxs-lookup"><span data-stu-id="98bec-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="98bec-182">Restrições (abertas ou token).</span><span class="sxs-lookup"><span data-stu-id="98bec-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="98bec-183">Informações específicas sobre o tipo de distribuição de chaves que define como a chave é fornecida ao cliente.</span><span class="sxs-lookup"><span data-stu-id="98bec-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="98bec-184">Configure a política de distribuição de ativos.</span><span class="sxs-lookup"><span data-stu-id="98bec-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="98bec-185">A configuração da política de entrega inclui:</span><span class="sxs-lookup"><span data-stu-id="98bec-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="98bec-186">O protocolo de entrega (HLS).</span><span class="sxs-lookup"><span data-stu-id="98bec-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="98bec-187">O tipo de criptografia dinâmica (criptografia CBC comum).</span><span class="sxs-lookup"><span data-stu-id="98bec-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="98bec-188">A URL de aquisição de licença.</span><span class="sxs-lookup"><span data-stu-id="98bec-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98bec-189">Se quiser fazer uma transmissão que seja criptografada com o FairPlay e outro sistema DRM (Gerenciamento de Direitos Digitais), você precisará configurar políticas de entrega separadas:</span><span class="sxs-lookup"><span data-stu-id="98bec-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="98bec-190">Uma IAssetDeliveryPolicy para configurar DASH (Transmissão Adaptável Dinâmica por HTTP) com CENC (Criptografia Comum) (PlayReady + Widevine) e Smooth com PlayReady</span><span class="sxs-lookup"><span data-stu-id="98bec-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="98bec-191">Outro IAssetDeliveryPolicy para configurar o FairPlay para o HLS</span><span class="sxs-lookup"><span data-stu-id="98bec-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="98bec-192">Criar um localizador OnDemand para obter uma URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="98bec-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="98bec-193">Usar a distribuição de chaves do FairPlay para aplicativos de player</span><span class="sxs-lookup"><span data-stu-id="98bec-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="98bec-194">Você pode desenvolver aplicativos player usando o SDK do iOS.</span><span class="sxs-lookup"><span data-stu-id="98bec-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="98bec-195">Para poder reproduzir conteúdo do FairPlay, você precisa implementar o protocolo de troca de licenças.</span><span class="sxs-lookup"><span data-stu-id="98bec-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="98bec-196">Esse protocolo não é especificado pela Apple.</span><span class="sxs-lookup"><span data-stu-id="98bec-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="98bec-197">Depende de cada aplicativo o modo de enviar solicitações de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="98bec-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="98bec-198">O serviço de distribuição de chaves do FairPlay nos Serviços de Mídia espera que o SPC seja recebido como um mensagem de postagem codificada www-form-url da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="98bec-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="98bec-199">O Player de Mídia do Azure não dá suporte para a reprodução do FairPlay pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="98bec-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="98bec-200">Para ter a reprodução do FairPlay no MAC OS X, obtenha o player de exemplo na conta de desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="98bec-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="98bec-201">URLs de streaming</span><span class="sxs-lookup"><span data-stu-id="98bec-201">Streaming URLs</span></span>
<span data-ttu-id="98bec-202">Se o ativo foi criptografado com mais de um DRM, você deve usar uma marcação de criptografia na URL de streaming: (formato='m3u8-aapl' criptografia='xxx').</span><span class="sxs-lookup"><span data-stu-id="98bec-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="98bec-203">As seguintes considerações se aplicam:</span><span class="sxs-lookup"><span data-stu-id="98bec-203">The following considerations apply:</span></span>

* <span data-ttu-id="98bec-204">Pode ser especificado apenas zero ou um tipo de criptografia.</span><span class="sxs-lookup"><span data-stu-id="98bec-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="98bec-205">O tipo de criptografia não precisa ser especificado na URL se apenas uma criptografia foi aplicada no ativo.</span><span class="sxs-lookup"><span data-stu-id="98bec-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="98bec-206">O tipo de criptografia não diferencia letras maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="98bec-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="98bec-207">Os seguintes tipos de criptografia podem ser especificados:</span><span class="sxs-lookup"><span data-stu-id="98bec-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="98bec-208">**cenc**: criptografia comum (PlayReady ou Widevine)</span><span class="sxs-lookup"><span data-stu-id="98bec-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="98bec-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="98bec-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="98bec-210">**cbc**: criptografia de envelope AES</span><span class="sxs-lookup"><span data-stu-id="98bec-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="98bec-211">Criar e configurar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98bec-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="98bec-212">Configure seu ambiente de desenvolvimento e preencha o arquivo de configuração app.config com as informações de conexão, conforme descrito em [Desenvolvimento de Serviços de Mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="98bec-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="98bec-213">Adicione os seguintes elementos para **appSettings** definidos no seu arquivo app.config:</span><span class="sxs-lookup"><span data-stu-id="98bec-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="98bec-214">Exemplo</span><span class="sxs-lookup"><span data-stu-id="98bec-214">Example</span></span>

<span data-ttu-id="98bec-215">O exemplo a seguir demonstra a capacidade de usar os Serviços de Mídia para distribuir conteúdo criptografado com o FairPlay.</span><span class="sxs-lookup"><span data-stu-id="98bec-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="98bec-216">Essa funcionalidade foi introduzida no SDK dos Serviços de Mídia do Azure para a versão 3.6.0 do .NET.</span><span class="sxs-lookup"><span data-stu-id="98bec-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="98bec-217">Substitua o código no seu arquivo Program.cs pelo código mostrado nesta seção.</span><span class="sxs-lookup"><span data-stu-id="98bec-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="98bec-218">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="98bec-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="98bec-219">Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento).</span><span class="sxs-lookup"><span data-stu-id="98bec-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="98bec-220">Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="98bec-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="98bec-221">Certifique-se de atualizar as variáveis para que indiquem as pastas onde estão localizados os arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="98bec-221">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
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

            // Associate the key with the asset.
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

            // Associate the content key authorization policy with the content key.
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

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="98bec-222">Próximas etapas: roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="98bec-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="98bec-223">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="98bec-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
