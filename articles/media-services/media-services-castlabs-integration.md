---
title: "Usando o castLabs para fornecer licenças Widevine aos Serviços de Mídia do Azure | Microsoft Docs"
description: "Este artigo descreve como é possível usar os serviços de mídia do Azure (AMS) para oferecer um fluxo dinamicamente é criptografado pelo AMS com os DRMs do PlayReady e Widevine. A licença do PlayReady vem do servidor de licenças do PlayReady dos serviços de mídia e a licença do Widevine é fornecida pelo servidor de licenças do castLabs."
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
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="15bca-104">Usando o castLabs para fornecer licenças Widevine para os Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="15bca-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15bca-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="15bca-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="15bca-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="15bca-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="15bca-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="15bca-107">Overview</span></span>
<span data-ttu-id="15bca-108">Este artigo descreve como é possível usar os serviços de mídia do Azure (AMS) para oferecer um fluxo dinamicamente é criptografado pelo AMS com os DRMs do PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="15bca-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="15bca-109">A licença do PlayReady vem do servidor de licenças do PlayReady dos serviços de mídia e a licença do Widevine é fornecida pelo servidor de licenças do **castLabs** .</span><span class="sxs-lookup"><span data-stu-id="15bca-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="15bca-110">Para reproduzir o conteúdo de streaming protegido por CENC (PlayReady e/ou Widevine), use o [Player de Mídia do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="15bca-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="15bca-111">Consulte o [documento sobre AMP](http://amp.azure.net/libs/amp/latest/docs/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="15bca-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="15bca-112">O diagrama a seguir demonstra uma arquitetura de integração de alto nível dos serviços de mídia do Azure e do castLabs.</span><span class="sxs-lookup"><span data-stu-id="15bca-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integração](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="15bca-114">Configuração típica do sistema</span><span class="sxs-lookup"><span data-stu-id="15bca-114">Typical system set up</span></span>
* <span data-ttu-id="15bca-115">O conteúdo de mídia é armazenado em AMS.</span><span class="sxs-lookup"><span data-stu-id="15bca-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="15bca-116">As IDs de chave de chaves de conteúdo são armazenados em castLabs e AMS.</span><span class="sxs-lookup"><span data-stu-id="15bca-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="15bca-117">O castLabs e o AMS têm autenticação de token interna.</span><span class="sxs-lookup"><span data-stu-id="15bca-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="15bca-118">As seções a seguir discutem os tokens de autenticação.</span><span class="sxs-lookup"><span data-stu-id="15bca-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="15bca-119">Quando um cliente solicita o fluxo do vídeo, o conteúdo é criptografado dinamicamente com **Criptografia comum** (CENC) e dinamicamente fornecido pelo AMS para DASH e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="15bca-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="15bca-120">Também fornecemos criptografia de fluxo elementar PlayReady M2TS para protocolo de streaming do HLS.</span><span class="sxs-lookup"><span data-stu-id="15bca-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="15bca-121">A licença do PlayReady é recuperada do servidor de licença do AMS e a licença Widevine é recuperada do servidor de licenças castLabs.</span><span class="sxs-lookup"><span data-stu-id="15bca-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="15bca-122">O Media Player decide automaticamente quais licenças buscar com base na capacidade de plataforma do cliente.</span><span class="sxs-lookup"><span data-stu-id="15bca-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="15bca-123">Geração de token de autenticação para obter uma licença</span><span class="sxs-lookup"><span data-stu-id="15bca-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="15bca-124">O castLabs e o AMS oferecem suporte ao formato de token JWT (JSON Web Token) usado para autorizar uma licença.</span><span class="sxs-lookup"><span data-stu-id="15bca-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="15bca-125">Token JWT no AMS</span><span class="sxs-lookup"><span data-stu-id="15bca-125">JWT token in AMS</span></span>
<span data-ttu-id="15bca-126">A tabela a seguir descreve o token JWT no AMS.</span><span class="sxs-lookup"><span data-stu-id="15bca-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="15bca-127">Emissor</span><span class="sxs-lookup"><span data-stu-id="15bca-127">Issuer</span></span> | <span data-ttu-id="15bca-128">Cadeia de caracteres do emissor do Secure Token Service (STS) escolhido</span><span class="sxs-lookup"><span data-stu-id="15bca-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="15bca-129">Público-alvo</span><span class="sxs-lookup"><span data-stu-id="15bca-129">Audience</span></span> |<span data-ttu-id="15bca-130">Cadeia de caracteres do público-alvo do STS usado</span><span class="sxs-lookup"><span data-stu-id="15bca-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="15bca-131">Declarações</span><span class="sxs-lookup"><span data-stu-id="15bca-131">Claims</span></span> |<span data-ttu-id="15bca-132">Um conjunto de declarações</span><span class="sxs-lookup"><span data-stu-id="15bca-132">A set of claims</span></span> |
| <span data-ttu-id="15bca-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="15bca-133">NotBefore</span></span> |<span data-ttu-id="15bca-134">Validade inicial do token</span><span class="sxs-lookup"><span data-stu-id="15bca-134">Start validity of the token</span></span> |
| <span data-ttu-id="15bca-135">Expira</span><span class="sxs-lookup"><span data-stu-id="15bca-135">Expires</span></span> |<span data-ttu-id="15bca-136">Validade final do token</span><span class="sxs-lookup"><span data-stu-id="15bca-136">End validity of the token</span></span> |
| <span data-ttu-id="15bca-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="15bca-137">SigningCredentials</span></span> |<span data-ttu-id="15bca-138">A chave que é compartilhada entre o servidor de licenças do PlayReady, servidor de licenças do castLabs e STS, pode ser simétrica ou assimétrica.</span><span class="sxs-lookup"><span data-stu-id="15bca-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="15bca-139">Token JWT no castLabs</span><span class="sxs-lookup"><span data-stu-id="15bca-139">JWT token in castLabs</span></span>
<span data-ttu-id="15bca-140">A tabela a seguir descreve o token JWT no castLabs.</span><span class="sxs-lookup"><span data-stu-id="15bca-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="15bca-141">Nome</span><span class="sxs-lookup"><span data-stu-id="15bca-141">Name</span></span> | <span data-ttu-id="15bca-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="15bca-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15bca-143">optData</span><span class="sxs-lookup"><span data-stu-id="15bca-143">optData</span></span> |<span data-ttu-id="15bca-144">Uma cadeia de caracteres JSON que contém informações sobre você.</span><span class="sxs-lookup"><span data-stu-id="15bca-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="15bca-145">crt</span><span class="sxs-lookup"><span data-stu-id="15bca-145">crt</span></span> |<span data-ttu-id="15bca-146">Uma cadeia de caracteres JSON que contém informações sobre o ativo, suas informações de licença e seus direitos de reprodução.</span><span class="sxs-lookup"><span data-stu-id="15bca-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="15bca-147">iat</span><span class="sxs-lookup"><span data-stu-id="15bca-147">iat</span></span> |<span data-ttu-id="15bca-148">A data e horário correntes na época.</span><span class="sxs-lookup"><span data-stu-id="15bca-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="15bca-149">jti</span><span class="sxs-lookup"><span data-stu-id="15bca-149">jti</span></span> |<span data-ttu-id="15bca-150">Um identificador exclusivo sobre esse token (cada token pode ser usado apenas uma vez no sistema do castLabs).</span><span class="sxs-lookup"><span data-stu-id="15bca-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="15bca-151">Configuração da solução de exemplo</span><span class="sxs-lookup"><span data-stu-id="15bca-151">Sample solution set up</span></span>
<span data-ttu-id="15bca-152">A [solução de exemplo](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consiste em dois projetos:</span><span class="sxs-lookup"><span data-stu-id="15bca-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="15bca-153">Um aplicativo de console que pode ser usado para definir as restrições de DRM em um ativo já incluído para o PlayReady e o Widevine.</span><span class="sxs-lookup"><span data-stu-id="15bca-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="15bca-154">Um aplicativo da Web que distribui os tokens, que poderia ser visto como uma versão MUITO SIMPLIFICADA de um STS.</span><span class="sxs-lookup"><span data-stu-id="15bca-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="15bca-155">Para usar o aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="15bca-155">To use the console application:</span></span>

1. <span data-ttu-id="15bca-156">Altere o app.config para configurar credenciais AMS, credenciais do castLabs, configuração de STS e chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="15bca-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="15bca-157">Carregue um ativo no AMS.</span><span class="sxs-lookup"><span data-stu-id="15bca-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="15bca-158">Obtenha o UUID do ativo carregado e altere a linha 32 no arquivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="15bca-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="15bca-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="15bca-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="15bca-160">Use um AssetId para nomear o ativo no sistema do castLabs (linha 44 no arquivo Program.cs).</span><span class="sxs-lookup"><span data-stu-id="15bca-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="15bca-161">Você deve definir o AssetId para o **castLabs**; ele precisa ser uma sequência alfanumérica e exclusiva.</span><span class="sxs-lookup"><span data-stu-id="15bca-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="15bca-162">Execute o programa.</span><span class="sxs-lookup"><span data-stu-id="15bca-162">Run the program.</span></span>

<span data-ttu-id="15bca-163">Para usar o aplicativo Web (STS):</span><span class="sxs-lookup"><span data-stu-id="15bca-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="15bca-164">Altere o web.config para configurar o ID do comerciante do castlabs, a configuração de STS e a chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="15bca-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="15bca-165">Implante os Sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="15bca-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="15bca-166">Navegue até o site.</span><span class="sxs-lookup"><span data-stu-id="15bca-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="15bca-167">Reproduzir um vídeo</span><span class="sxs-lookup"><span data-stu-id="15bca-167">Playing back a video</span></span>
<span data-ttu-id="15bca-168">Para reproduzir um vídeo criptografado com criptografia comum (PlayReady e/ou Widevine), é possível usar o [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="15bca-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="15bca-169">Ao executar o aplicativo de console, a ID de chave de conteúdo e a URL de manifesto são exibidos.</span><span class="sxs-lookup"><span data-stu-id="15bca-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="15bca-170">Abra uma nova guia e inicie seu STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="15bca-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="15bca-171">Vá para [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="15bca-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="15bca-172">Cole na URL de streaming.</span><span class="sxs-lookup"><span data-stu-id="15bca-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="15bca-173">Clique na caixa de seleção **Opções avançadas** .</span><span class="sxs-lookup"><span data-stu-id="15bca-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="15bca-174">Selecione PlayReady e/ou Widevine na lista suspensa **Proteção** .</span><span class="sxs-lookup"><span data-stu-id="15bca-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="15bca-175">Cole o token que você obteve no seu STS na caixa de texto do token.</span><span class="sxs-lookup"><span data-stu-id="15bca-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="15bca-176">O servidor de licença do castLab não precisa do prefixo "Portador =" na frente do token.</span><span class="sxs-lookup"><span data-stu-id="15bca-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="15bca-177">Nesse caso, remova-o antes de enviar o token.</span><span class="sxs-lookup"><span data-stu-id="15bca-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="15bca-178">Atualize o player.</span><span class="sxs-lookup"><span data-stu-id="15bca-178">Update the player.</span></span>
8. <span data-ttu-id="15bca-179">O vídeo deve estar em reprodução.</span><span class="sxs-lookup"><span data-stu-id="15bca-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="15bca-180">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="15bca-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="15bca-181">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="15bca-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

