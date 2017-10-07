---
title: design de aaaHybrid do DRM subsistema (s) usando o Azure Media Services | Microsoft Docs
description: "Este tópico discute o design híbrido dos subsistemas DRM usando os Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="b93be-103">Design híbrido de subsistemas DRM</span><span class="sxs-lookup"><span data-stu-id="b93be-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="b93be-104">Este tópico discute o design híbrido dos subsistemas DRM usando os Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="b93be-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="b93be-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b93be-105">Overview</span></span>

<span data-ttu-id="b93be-106">Serviços de mídia do Azure fornece suporte para Olá sistema DRM três a seguir:</span><span class="sxs-lookup"><span data-stu-id="b93be-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="b93be-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="b93be-107">PlayReady</span></span>
* <span data-ttu-id="b93be-108">Widevine (Modular)</span><span class="sxs-lookup"><span data-stu-id="b93be-108">Widevine (Modular)</span></span>
* <span data-ttu-id="b93be-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="b93be-109">FairPlay</span></span>

<span data-ttu-id="b93be-110">suporte DRM Olá inclui criptografia DRM (criptografia dinâmica) e a entrega de licença, dando suporte a todos os 3 DRMs como um player de navegador SDK do Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="b93be-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="b93be-111">Para um tratamento detalhado de DRM/CENC subsistema design e implementação, consulte documento hello [CENC com várias DRM e controle de acesso](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="b93be-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="b93be-112">Embora oferecemos suporte completo para três sistemas DRM, às vezes, os clientes precisam toouse várias partes de seus próprios infraestrutura/subsistemas na adição tooAzure Media Services toobuild um subsistema DRM híbrido.</span><span class="sxs-lookup"><span data-stu-id="b93be-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="b93be-113">Abaixo estão algumas perguntas comuns feitas pelos clientes:</span><span class="sxs-lookup"><span data-stu-id="b93be-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="b93be-114">"Posso usar meus próprios servidores de licença DRM?"</span><span class="sxs-lookup"><span data-stu-id="b93be-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="b93be-115">(Nesse caso, os clientes investiram no farm de servidores de licença do DRM com lógica de negócios inserida).</span><span class="sxs-lookup"><span data-stu-id="b93be-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="b93be-116">"Posso usar somente sua entrega de licença do DRM nos Serviços de Mídia do Azure sem hospedar conteúdo no AMS?"</span><span class="sxs-lookup"><span data-stu-id="b93be-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="b93be-117">Modularidade de saudação plataforma AMS DRM</span><span class="sxs-lookup"><span data-stu-id="b93be-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="b93be-118">Como parte de uma plataforma de vídeo em nuvem abrangente, o DRM dos Serviços de Mídia do Azure tem um design elaborado pensando em flexibilidade e modularidade.</span><span class="sxs-lookup"><span data-stu-id="b93be-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="b93be-119">Você pode usar os serviços de mídia do Azure com qualquer Olá combinações diferentes descritas na tabela de saudação abaixo (segue uma explicação de notação Olá usada na tabela de saudação) a seguir.</span><span class="sxs-lookup"><span data-stu-id="b93be-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="b93be-120">**Hospedagem e origem de conteúdo**</span><span class="sxs-lookup"><span data-stu-id="b93be-120">**Content hosting & origin**</span></span>|<span data-ttu-id="b93be-121">**Criptografia de conteúdo**</span><span class="sxs-lookup"><span data-stu-id="b93be-121">**Content encryption**</span></span>|<span data-ttu-id="b93be-122">**Entrega de licença do DRM**</span><span class="sxs-lookup"><span data-stu-id="b93be-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="b93be-123">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-123">AMS</span></span>|<span data-ttu-id="b93be-124">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-124">AMS</span></span>|<span data-ttu-id="b93be-125">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-125">AMS</span></span>|
|<span data-ttu-id="b93be-126">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-126">AMS</span></span>|<span data-ttu-id="b93be-127">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-127">AMS</span></span>|<span data-ttu-id="b93be-128">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-128">Third-party</span></span>|
|<span data-ttu-id="b93be-129">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-129">AMS</span></span>|<span data-ttu-id="b93be-130">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-130">Third-party</span></span>|<span data-ttu-id="b93be-131">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-131">AMS</span></span>|
|<span data-ttu-id="b93be-132">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-132">AMS</span></span>|<span data-ttu-id="b93be-133">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-133">Third-party</span></span>|<span data-ttu-id="b93be-134">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-134">Third-party</span></span>|
|<span data-ttu-id="b93be-135">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-135">Third-party</span></span>|<span data-ttu-id="b93be-136">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-136">Third-party</span></span>|<span data-ttu-id="b93be-137">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="b93be-138">Hospedagem e origem de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b93be-138">Content hosting & origin</span></span>

* <span data-ttu-id="b93be-139">AMS: ativo de vídeo é hospedado no AMS e streaming é por meio de pontos de extremidade de streaming do AMS (mas não necessariamente empacotamento dinâmico).</span><span class="sxs-lookup"><span data-stu-id="b93be-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="b93be-140">Terceiros: o vídeo é hospedada e distribuído em uma plataforma de streaming de terceiros fora do AMS.</span><span class="sxs-lookup"><span data-stu-id="b93be-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="b93be-141">Criptografia de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b93be-141">Content encryption</span></span>

* <span data-ttu-id="b93be-142">AMS: criptografia de conteúdo é realizada dinamicamente/sob demanda por criptografia dinâmica do AMS.</span><span class="sxs-lookup"><span data-stu-id="b93be-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="b93be-143">Terceiros: criptografia de conteúdo é executada fora do AMS usando um fluxo de trabalho pré-processamento.</span><span class="sxs-lookup"><span data-stu-id="b93be-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="b93be-144">Entrega de licença do DRM</span><span class="sxs-lookup"><span data-stu-id="b93be-144">DRM license delivery</span></span>

* <span data-ttu-id="b93be-145">AMS: a licença DRM é fornecida pelo serviço de entrega de licença do AMS.</span><span class="sxs-lookup"><span data-stu-id="b93be-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="b93be-146">Terceiros: a licença DRM é fornecida por um servidor de licença DRM de terceiros fora do AMS.</span><span class="sxs-lookup"><span data-stu-id="b93be-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="b93be-147">Configurar com base em seu cenário híbrido</span><span class="sxs-lookup"><span data-stu-id="b93be-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="b93be-148">Chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b93be-148">Content key</span></span>

<span data-ttu-id="b93be-149">Por meio da configuração de uma chave de conteúdo, você pode controlar Olá atributos de criptografia dinâmica AMS e o serviço de entrega de licença AMS a seguir:</span><span class="sxs-lookup"><span data-stu-id="b93be-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="b93be-150">chave de conteúdo do Hello usado para criptografia dinâmica do DRM.</span><span class="sxs-lookup"><span data-stu-id="b93be-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="b93be-151">DRM licença conteúdo toobe fornecido pelos serviços de entrega de licença: direitos, chave de conteúdo e as restrições.</span><span class="sxs-lookup"><span data-stu-id="b93be-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="b93be-152">Tipo de **restrição de política de autorização da chave de conteúdo**: restrição aberta, de IP ou de token.</span><span class="sxs-lookup"><span data-stu-id="b93be-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="b93be-153">Se **token** tipo de **restrição de política de autorização da chave de conteúdo é usada**, Olá **restrição de política de autorização da chave de conteúdo** devem ser atendidos antes da emissão de uma licença.</span><span class="sxs-lookup"><span data-stu-id="b93be-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="b93be-154">Política de fornecimento de ativos</span><span class="sxs-lookup"><span data-stu-id="b93be-154">Asset delivery policy</span></span>

<span data-ttu-id="b93be-155">Por meio da configuração de uma política de entrega de ativos, você pode controlar Olá atributos usados pelo empacotador dinâmico AMS e criptografia dinâmica de um ponto de extremidade de streaming de AMS a seguir:</span><span class="sxs-lookup"><span data-stu-id="b93be-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="b93be-156">Combinação de protocolo de streaming e criptografia do DRM, como DASH em CENC (PlayReady e Widevine), streaming suave em PlayReady, HLS em Widevine ou PlayReady.</span><span class="sxs-lookup"><span data-stu-id="b93be-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="b93be-157">saudação padrão/inseridos licença entrega URLs para cada Olá envolvidos DRMs.</span><span class="sxs-lookup"><span data-stu-id="b93be-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="b93be-158">Se as URLs de aquisição de licença (LA_URLs) na lista de reprodução do DASH MPD ou do HLS contêm uma cadeia de caracteres de consulta de KID (ID de chave) para Widevine e FairPlay, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b93be-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="b93be-159">Cenários e exemplos</span><span class="sxs-lookup"><span data-stu-id="b93be-159">Scenarios and samples</span></span>

<span data-ttu-id="b93be-160">Com base em explicações Olá na seção anterior hello, Olá após cinco cenários híbridos usa respectivos **chave de conteúdo**-**política de entrega de ativos** combinações de configurações (Olá exemplos mencionados na última coluna do hello siga tabela Olá):</span><span class="sxs-lookup"><span data-stu-id="b93be-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="b93be-161">**Hospedagem e origem de conteúdo**</span><span class="sxs-lookup"><span data-stu-id="b93be-161">**Content hosting & origin**</span></span>|<span data-ttu-id="b93be-162">**Criptografia do DRM**</span><span class="sxs-lookup"><span data-stu-id="b93be-162">**DRM encryption**</span></span>|<span data-ttu-id="b93be-163">**Entrega de licença do DRM**</span><span class="sxs-lookup"><span data-stu-id="b93be-163">**DRM license delivery**</span></span>|<span data-ttu-id="b93be-164">**Configurar chave de conteúdo**</span><span class="sxs-lookup"><span data-stu-id="b93be-164">**Configure content key**</span></span>|<span data-ttu-id="b93be-165">**Configurar política de entrega de ativos**</span><span class="sxs-lookup"><span data-stu-id="b93be-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="b93be-166">**Amostra**</span><span class="sxs-lookup"><span data-stu-id="b93be-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="b93be-167">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-167">AMS</span></span>|<span data-ttu-id="b93be-168">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-168">AMS</span></span>|<span data-ttu-id="b93be-169">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-169">AMS</span></span>|<span data-ttu-id="b93be-170">Sim</span><span class="sxs-lookup"><span data-stu-id="b93be-170">Yes</span></span>|<span data-ttu-id="b93be-171">Sim</span><span class="sxs-lookup"><span data-stu-id="b93be-171">Yes</span></span>|<span data-ttu-id="b93be-172">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="b93be-172">Sample 1</span></span>|
|<span data-ttu-id="b93be-173">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-173">AMS</span></span>|<span data-ttu-id="b93be-174">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-174">AMS</span></span>|<span data-ttu-id="b93be-175">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-175">Third-party</span></span>|<span data-ttu-id="b93be-176">Sim</span><span class="sxs-lookup"><span data-stu-id="b93be-176">Yes</span></span>|<span data-ttu-id="b93be-177">Sim</span><span class="sxs-lookup"><span data-stu-id="b93be-177">Yes</span></span>|<span data-ttu-id="b93be-178">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="b93be-178">Sample 2</span></span>|
|<span data-ttu-id="b93be-179">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-179">AMS</span></span>|<span data-ttu-id="b93be-180">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-180">Third-party</span></span>|<span data-ttu-id="b93be-181">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-181">AMS</span></span>|<span data-ttu-id="b93be-182">Sim</span><span class="sxs-lookup"><span data-stu-id="b93be-182">Yes</span></span>|<span data-ttu-id="b93be-183">Não</span><span class="sxs-lookup"><span data-stu-id="b93be-183">No</span></span>|<span data-ttu-id="b93be-184">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="b93be-184">Sample 3</span></span>|
|<span data-ttu-id="b93be-185">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-185">AMS</span></span>|<span data-ttu-id="b93be-186">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-186">Third-party</span></span>|<span data-ttu-id="b93be-187">Externa</span><span class="sxs-lookup"><span data-stu-id="b93be-187">Outside</span></span>|<span data-ttu-id="b93be-188">Não</span><span class="sxs-lookup"><span data-stu-id="b93be-188">No</span></span>|<span data-ttu-id="b93be-189">Não</span><span class="sxs-lookup"><span data-stu-id="b93be-189">No</span></span>|<span data-ttu-id="b93be-190">Exemplo 4</span><span class="sxs-lookup"><span data-stu-id="b93be-190">Sample 4</span></span>|
|<span data-ttu-id="b93be-191">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-191">Third-party</span></span>|<span data-ttu-id="b93be-192">Terceiros</span><span class="sxs-lookup"><span data-stu-id="b93be-192">Third-party</span></span>|<span data-ttu-id="b93be-193">AMS</span><span class="sxs-lookup"><span data-stu-id="b93be-193">AMS</span></span>|<span data-ttu-id="b93be-194">Sim</span><span class="sxs-lookup"><span data-stu-id="b93be-194">Yes</span></span>|<span data-ttu-id="b93be-195">Não</span><span class="sxs-lookup"><span data-stu-id="b93be-195">No</span></span>|    

<span data-ttu-id="b93be-196">Exemplos de saudação proteção PlayReady funciona para DASH e smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="b93be-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="b93be-197">as URLs de vídeo de saudação abaixo são smooth URLs de streaming.</span><span class="sxs-lookup"><span data-stu-id="b93be-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="b93be-198">tooget Olá URLs de DASH correspondente, acrescentar apenas "(formato = mpd-tempo-csf)".</span><span class="sxs-lookup"><span data-stu-id="b93be-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="b93be-199">Você pode usar o hello [executor de teste de mídia do azure](http://aka.ms/amtest) tootest em um navegador.</span><span class="sxs-lookup"><span data-stu-id="b93be-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="b93be-200">Ele permite tooconfigure que toouse de protocolo, em qual tecnologia de streaming.</span><span class="sxs-lookup"><span data-stu-id="b93be-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="b93be-201">IE11 e MS Edge no Windows 10 dão suporte a PlayReady por meio de EME.</span><span class="sxs-lookup"><span data-stu-id="b93be-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="b93be-202">Para obter mais informações, consulte [detalhes sobre Olá testar ferramenta](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="b93be-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="b93be-203">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="b93be-203">Sample 1</span></span>

* <span data-ttu-id="b93be-204">URL da fonte (base): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="b93be-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="b93be-205">PlayReady LA_URL (DASH e suave): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="b93be-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="b93be-206">LA_URL do Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="b93be-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="b93be-207">LA_URL do FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="b93be-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="b93be-208">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="b93be-208">Sample 2</span></span>

* <span data-ttu-id="b93be-209">URL da fonte (base): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="b93be-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="b93be-210">LA_URL do PlayReady (DASH e suave): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="b93be-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="b93be-211">Exemplo 3</span><span class="sxs-lookup"><span data-stu-id="b93be-211">Sample 3</span></span>

* <span data-ttu-id="b93be-212">URL da fonte: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="b93be-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="b93be-213">PlayReady LA_URL (DASH e suave): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="b93be-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="b93be-214">Exemplo 4</span><span class="sxs-lookup"><span data-stu-id="b93be-214">Sample 4</span></span>

* <span data-ttu-id="b93be-215">URL da fonte: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="b93be-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="b93be-216">LA_URL do PlayReady (DASH e suave): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="b93be-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="b93be-217">Resumo</span><span class="sxs-lookup"><span data-stu-id="b93be-217">Summary</span></span>

<span data-ttu-id="b93be-218">Em resumo, componentes de DRM dos Serviços de Mídia do Azure são flexíveis, você pode usá-los em um cenário híbrido configurando corretamente a chave de conteúdo e a política de entrega de ativos conforme descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="b93be-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b93be-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b93be-219">Next steps</span></span>
<span data-ttu-id="b93be-220">Exibir os roteiros de aprendizagem dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="b93be-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b93be-221">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="b93be-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

