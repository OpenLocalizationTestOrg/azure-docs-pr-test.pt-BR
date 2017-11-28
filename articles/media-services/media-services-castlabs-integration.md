---
title: "aaaUsing castLabs toodeliver Widevine licenças dos serviços de mídia tooAzure | Microsoft Docs"
description: "Este artigo descreve como você pode usar os serviços de mídia do Azure (AMS) toodeliver um fluxo criptografado dinamicamente pelo AMS com PlayReady e Widevine DRMs. licença do PlayReady Hello proveniente do servidor de licença do PlayReady dos serviços de mídia e licenças Widevine é fornecida pelo servidor de licença castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="96565-104">Usando castLabs toodeliver Widevine licenças tooAzure serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="96565-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96565-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="96565-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="96565-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="96565-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="96565-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="96565-107">Overview</span></span>
<span data-ttu-id="96565-108">Este artigo descreve como você pode usar os serviços de mídia do Azure (AMS) toodeliver um fluxo criptografado dinamicamente pelo AMS com PlayReady e Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="96565-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="96565-109">licença do PlayReady Hello proveniente do servidor de licença do PlayReady dos serviços de mídia e licenças Widevine é entregue por **castLabs** servidor de licença.</span><span class="sxs-lookup"><span data-stu-id="96565-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="96565-110">tooplayback streaming de conteúdo protegido por CENC (PlayReady e/ou Widevine), você pode usar [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="96565-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="96565-111">Consulte o [documento sobre AMP](http://amp.azure.net/libs/amp/latest/docs/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="96565-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="96565-112">Olá diagrama a seguir demonstra uma arquitetura de integração de serviços de mídia do Azure e castLabs alto nível.</span><span class="sxs-lookup"><span data-stu-id="96565-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integração](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="96565-114">Configuração típica do sistema</span><span class="sxs-lookup"><span data-stu-id="96565-114">Typical system set up</span></span>
* <span data-ttu-id="96565-115">O conteúdo de mídia é armazenado em AMS.</span><span class="sxs-lookup"><span data-stu-id="96565-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="96565-116">As IDs de chave de chaves de conteúdo são armazenados em castLabs e AMS.</span><span class="sxs-lookup"><span data-stu-id="96565-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="96565-117">O castLabs e o AMS têm autenticação de token interna.</span><span class="sxs-lookup"><span data-stu-id="96565-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="96565-118">Olá seções a seguir discutem os tokens de autenticação.</span><span class="sxs-lookup"><span data-stu-id="96565-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="96565-119">Quando um cliente solicita o vídeo de saudação toostream, conteúdo de saudação dinamicamente é criptografado com **criptografia comum** (CENC) e empacotado dinamicamente pelo AMS tooSmooth Streaming e traço.</span><span class="sxs-lookup"><span data-stu-id="96565-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="96565-120">Também fornecemos criptografia de fluxo elementar PlayReady M2TS para protocolo de streaming do HLS.</span><span class="sxs-lookup"><span data-stu-id="96565-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="96565-121">A licença do PlayReady é recuperada do servidor de licença do AMS e a licença Widevine é recuperada do servidor de licenças castLabs.</span><span class="sxs-lookup"><span data-stu-id="96565-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="96565-122">Media Player decide quais toofetch de licença com base na capacidade de plataforma de cliente Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96565-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="96565-123">Geração de token de autenticação para obter uma licença</span><span class="sxs-lookup"><span data-stu-id="96565-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="96565-124">CastLabs e AMS suporte JWT (JSON Web Token) formato do token usado tooauthorize uma licença.</span><span class="sxs-lookup"><span data-stu-id="96565-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="96565-125">Token JWT no AMS</span><span class="sxs-lookup"><span data-stu-id="96565-125">JWT token in AMS</span></span>
<span data-ttu-id="96565-126">Olá, a tabela a seguir descreve o token JWT no AMS.</span><span class="sxs-lookup"><span data-stu-id="96565-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="96565-127">Emissor</span><span class="sxs-lookup"><span data-stu-id="96565-127">Issuer</span></span> | <span data-ttu-id="96565-128">Cadeia de caracteres do emissor de saudação escolhida Token STS (serviço seguro)</span><span class="sxs-lookup"><span data-stu-id="96565-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="96565-129">Público-alvo</span><span class="sxs-lookup"><span data-stu-id="96565-129">Audience</span></span> |<span data-ttu-id="96565-130">Cadeia de caracteres de público-alvo de saudação usada STS</span><span class="sxs-lookup"><span data-stu-id="96565-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="96565-131">Declarações</span><span class="sxs-lookup"><span data-stu-id="96565-131">Claims</span></span> |<span data-ttu-id="96565-132">Um conjunto de declarações</span><span class="sxs-lookup"><span data-stu-id="96565-132">A set of claims</span></span> |
| <span data-ttu-id="96565-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="96565-133">NotBefore</span></span> |<span data-ttu-id="96565-134">Iniciar a validade do token Olá</span><span class="sxs-lookup"><span data-stu-id="96565-134">Start validity of hello token</span></span> |
| <span data-ttu-id="96565-135">Expira</span><span class="sxs-lookup"><span data-stu-id="96565-135">Expires</span></span> |<span data-ttu-id="96565-136">Final de validade do token Olá</span><span class="sxs-lookup"><span data-stu-id="96565-136">End validity of hello token</span></span> |
| <span data-ttu-id="96565-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="96565-137">SigningCredentials</span></span> |<span data-ttu-id="96565-138">chave de saudação que é compartilhado entre o servidor de licença do PlayReady, castLabs servidor de licença e STS, poderia ser chave simétrica ou assimétrica.</span><span class="sxs-lookup"><span data-stu-id="96565-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="96565-139">Token JWT no castLabs</span><span class="sxs-lookup"><span data-stu-id="96565-139">JWT token in castLabs</span></span>
<span data-ttu-id="96565-140">Olá, a tabela a seguir descreve o token JWT no castLabs.</span><span class="sxs-lookup"><span data-stu-id="96565-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="96565-141">Nome</span><span class="sxs-lookup"><span data-stu-id="96565-141">Name</span></span> | <span data-ttu-id="96565-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="96565-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="96565-143">optData</span><span class="sxs-lookup"><span data-stu-id="96565-143">optData</span></span> |<span data-ttu-id="96565-144">Uma cadeia de caracteres JSON que contém informações sobre você.</span><span class="sxs-lookup"><span data-stu-id="96565-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="96565-145">crt</span><span class="sxs-lookup"><span data-stu-id="96565-145">crt</span></span> |<span data-ttu-id="96565-146">Uma JSON cadeia de caracteres que contêm informações sobre ativos hello, seus direitos de reprodução e informações de licença.</span><span class="sxs-lookup"><span data-stu-id="96565-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="96565-147">iat</span><span class="sxs-lookup"><span data-stu-id="96565-147">iat</span></span> |<span data-ttu-id="96565-148">Olá data e hora atuais na época.</span><span class="sxs-lookup"><span data-stu-id="96565-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="96565-149">jti</span><span class="sxs-lookup"><span data-stu-id="96565-149">jti</span></span> |<span data-ttu-id="96565-150">Um identificador exclusivo sobre esse token (cada token pode somente ser usado uma vez no sistema de castLabs Olá).</span><span class="sxs-lookup"><span data-stu-id="96565-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="96565-151">Configuração da solução de exemplo</span><span class="sxs-lookup"><span data-stu-id="96565-151">Sample solution set up</span></span>
<span data-ttu-id="96565-152">Olá [solução de exemplo](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consiste em dois projetos:</span><span class="sxs-lookup"><span data-stu-id="96565-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="96565-153">Um aplicativo de console que pode ser restrições de DRM tooset usado em um ativo já ingerido, para PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="96565-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="96565-154">Um aplicativo da Web que distribui os tokens, que poderia ser visto como uma versão MUITO SIMPLIFICADA de um STS.</span><span class="sxs-lookup"><span data-stu-id="96565-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="96565-155">aplicativo de console hello toouse:</span><span class="sxs-lookup"><span data-stu-id="96565-155">toouse hello console application:</span></span>

1. <span data-ttu-id="96565-156">Alterar credenciais de toosetup AMS Olá App. config, castLabs credenciais, configuração de STS e uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="96565-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="96565-157">Carregue um ativo no AMS.</span><span class="sxs-lookup"><span data-stu-id="96565-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="96565-158">Get hello UUID de saudação carregado ativo e alterar 32 de linha no arquivo Program.cs de saudação:</span><span class="sxs-lookup"><span data-stu-id="96565-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="96565-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="96565-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="96565-160">Use um AssetId para nomear ativo Olá no sistema de castLabs hello (44 linha no arquivo Program.cs de saudação).</span><span class="sxs-lookup"><span data-stu-id="96565-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="96565-161">Você deve definir AssetId para **castLabs**; ele precisa toobe uma cadeia de caracteres alfanumérica exclusiva.</span><span class="sxs-lookup"><span data-stu-id="96565-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="96565-162">Execute o programa de saudação.</span><span class="sxs-lookup"><span data-stu-id="96565-162">Run hello program.</span></span>

<span data-ttu-id="96565-163">Olá toouse aplicativo Web (STS):</span><span class="sxs-lookup"><span data-stu-id="96565-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="96565-164">Loja de castlabs alteração Olá Web. config toosetup ID, configuração de STS hello e uma chave compartilhada hello.</span><span class="sxs-lookup"><span data-stu-id="96565-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="96565-165">Implante tooAzure sites.</span><span class="sxs-lookup"><span data-stu-id="96565-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="96565-166">Navegue toohello site.</span><span class="sxs-lookup"><span data-stu-id="96565-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="96565-167">Reproduzir um vídeo</span><span class="sxs-lookup"><span data-stu-id="96565-167">Playing back a video</span></span>
<span data-ttu-id="96565-168">um vídeo de tooplayback criptografada com criptografia comum (PlayReady e/ou Widevine), você pode usar o hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="96565-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="96565-169">Ao executar o aplicativo de console hello, Olá ID de chave de conteúdo e hello URL de manifesto são exibidos.</span><span class="sxs-lookup"><span data-stu-id="96565-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="96565-170">Abra uma nova guia e inicie seu STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="96565-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="96565-171">Vá muito[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="96565-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="96565-172">Cole Olá URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="96565-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="96565-173">Clique em Olá **opções avançadas de** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="96565-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="96565-174">Em Olá **proteção** lista suspensa, selecione PlayReady e/ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="96565-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="96565-175">Cole o token Olá que você obteve seu STS na caixa de texto de Token hello.</span><span class="sxs-lookup"><span data-stu-id="96565-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="96565-176">servidor de licença do Hello castLab não precisa hello "portador =" prefixo na frente do token de saudação.</span><span class="sxs-lookup"><span data-stu-id="96565-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="96565-177">Então remova que antes de enviar o token hello.</span><span class="sxs-lookup"><span data-stu-id="96565-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="96565-178">Atualize o player de saudação.</span><span class="sxs-lookup"><span data-stu-id="96565-178">Update hello player.</span></span>
8. <span data-ttu-id="96565-179">Olá vídeo deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="96565-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="96565-180">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="96565-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="96565-181">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="96565-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

