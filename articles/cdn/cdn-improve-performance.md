---
title: aaaImprove desempenho compactando arquivos no Azure CDN | Microsoft Docs
description: "Saiba como o arquivo tooimprove transferir velocidade e aumentos de desempenho de carregamento de página por compactar os arquivos no Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="0ca93-103">Melhorar o desempenho compactando os arquivos na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ca93-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="0ca93-104">A compactação é uma velocidade de transferência de arquivo do método simples e eficaz tooimprove e aumento de desempenho de carregamento de página, reduzindo o tamanho do arquivo antes de ele é enviado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ca93-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="0ca93-105">Ela reduz os custos de largura de banda e oferece uma experiência mais responsiva para os seus usuários.</span><span class="sxs-lookup"><span data-stu-id="0ca93-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="0ca93-106">Há duas maneiras de compactação tooenable:</span><span class="sxs-lookup"><span data-stu-id="0ca93-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="0ca93-107">Você pode habilitar a compactação no servidor de origem, caso em que hello CDN passe Olá arquivos compactados e entregar tooclients arquivos compactados que fazem a solicitação.</span><span class="sxs-lookup"><span data-stu-id="0ca93-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="0ca93-108">Você pode habilitar a compactação diretamente nos servidores de borda CDN, na qual o caso Olá CDN compacta Olá arquivos e servi-los tooend usuários, mesmo se eles não são compactados com o servidor de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ca93-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ca93-109">Alterações de configuração de CDN levar alguns toopropagate tempo por meio da rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ca93-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="0ca93-110">Para perfis <b>CDN do Azure do Akamai</b> , a propagação normalmente é concluída em menos de um minuto.</span><span class="sxs-lookup"><span data-stu-id="0ca93-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="0ca93-111">Para perfis <b>CDN do Azure da Verizon</b> , você geralmente verá suas alterações serem aplicadas em 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="0ca93-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="0ca93-112">Se esse for Olá pela primeira vez que você definiu a compactação para o ponto de extremidade CDN, você deve considerar a espera-se de que as configurações de compactação Olá tenham se propagado POPs toohello antes de solucionar problemas de toobe de 1 a 2 horas</span><span class="sxs-lookup"><span data-stu-id="0ca93-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="0ca93-113">Habilitando a compactação</span><span class="sxs-lookup"><span data-stu-id="0ca93-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="0ca93-114">Olá camadas Standard e Premium CDN fornecem Olá a mesma funcionalidade de compactação, mas hello interface de usuário diferente.</span><span class="sxs-lookup"><span data-stu-id="0ca93-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="0ca93-115">Para obter mais informações sobre as diferenças de saudação entre camadas Standard e Premium CDN, consulte [visão geral do Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ca93-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="0ca93-116">Camada padrão</span><span class="sxs-lookup"><span data-stu-id="0ca93-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="0ca93-117">Esta seção aplica-se muito**Azure CDN padrão da Verizon** e **padrão do Azure CDN do Akamai** perfis.</span><span class="sxs-lookup"><span data-stu-id="0ca93-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="0ca93-118">Na página de perfil CDN hello, clique em ponto de extremidade CDN Olá desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="0ca93-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Pontos de extremidade da página de perfil da CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="0ca93-120">Abre a página de ponto de extremidade CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="0ca93-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="0ca93-121">Clique em Olá **configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ca93-121">Click hello **Configure** button.</span></span>
   
    ![Botão de gerenciamento de página de perfil da CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="0ca93-123">Abre a página de configuração de CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="0ca93-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="0ca93-124">Habilitar **Compactação**.</span><span class="sxs-lookup"><span data-stu-id="0ca93-124">Turn on **Compression**.</span></span>
   
    ![Opções de compactação da CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="0ca93-126">Use tipos de padrão de hello, ou modificar a lista de hello, removendo ou adicionando tipos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="0ca93-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0ca93-127">Embora possível, não é recomendável tooapply compactação toocompressed formatos, como ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="0ca93-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="0ca93-128">Depois de fazer suas alterações, clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ca93-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="0ca93-129">Camada premium</span><span class="sxs-lookup"><span data-stu-id="0ca93-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="0ca93-130">Esta seção aplica-se muito**Premium do Azure CDN da Verizon** perfis.</span><span class="sxs-lookup"><span data-stu-id="0ca93-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="0ca93-131">Na página de perfil CDN hello, clique em Olá **gerenciar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ca93-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Botão de gerenciamento de página de perfil da CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="0ca93-133">portal de gerenciamento de CDN Olá é aberto.</span><span class="sxs-lookup"><span data-stu-id="0ca93-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="0ca93-134">Passe o mouse sobre Olá **HTTP grande** guia, em seguida, passe o mouse sobre Olá **as configurações de Cache** flutuante.</span><span class="sxs-lookup"><span data-stu-id="0ca93-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="0ca93-135">Clique em **Compactação**.</span><span class="sxs-lookup"><span data-stu-id="0ca93-135">Click on **Compression**.</span></span>

    ![Seleção de compactação de arquivos](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="0ca93-137">As opções de compactação são exibidas.</span><span class="sxs-lookup"><span data-stu-id="0ca93-137">Compression options are displayed.</span></span>
   
    ![Compactação de arquivos](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="0ca93-139">Habilitar a compactação clicando Olá **compactação habilitada** botão de opção.</span><span class="sxs-lookup"><span data-stu-id="0ca93-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="0ca93-140">Inserir tipos MIME Olá desejar toocompress como uma lista delimitada por vírgulas (sem espaços) em Olá **tipos de arquivo** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0ca93-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0ca93-141">Embora possível, não é recomendável tooapply compactação toocompressed formatos, como ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="0ca93-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="0ca93-142">Depois de fazer suas alterações, clique em Olá **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="0ca93-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="0ca93-143">Regras de compactação</span><span class="sxs-lookup"><span data-stu-id="0ca93-143">Compression rules</span></span>
<span data-ttu-id="0ca93-144">Essas tabelas descrevem o comportamento de compactação CDN do Azure para cada cenário.</span><span class="sxs-lookup"><span data-stu-id="0ca93-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ca93-145">Para o **CDN do Azure da Verizon** (Standard e Premium), só os arquivos elegíveis são compactados.</span><span class="sxs-lookup"><span data-stu-id="0ca93-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="0ca93-146">toobe qualificada para compactação, um arquivo necessário:</span><span class="sxs-lookup"><span data-stu-id="0ca93-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="0ca93-147">Ser maior que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="0ca93-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="0ca93-148">Ser menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0ca93-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="0ca93-149">Para o **CDN do Azure do Akamai**, todos os arquivos estão qualificados para compactação.</span><span class="sxs-lookup"><span data-stu-id="0ca93-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="0ca93-150">Para todos os produtos de CDN do Azure, um arquivo deve ser um tipo MIME que foi [configurado para compactação](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="0ca93-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="0ca93-151">Os perfis da **CDN do Azure da Verizon** (Standard e Premium) oferecem suporte à codificação **gzip** (GNU zip), **deflate**, **bzip2** ou **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="0ca93-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="0ca93-152">Para codificação Brotli, compactação de saudação é feita apenas na borda de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ca93-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="0ca93-153">Olá cliente/navegador deve enviar a solicitação de saudação para codificação Brotli e ativo compactado Olá deve tiverem sido compactado no lado de origem Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="0ca93-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="0ca93-154">Os perfis da **CDN do Azure da Akamai** oferecem suporte somente á codificação **gzip**.</span><span class="sxs-lookup"><span data-stu-id="0ca93-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="0ca93-155">**Azure CDN do Akamai** pontos de extremidade sempre solicitar **gzip** codificada em arquivos de origem hello, independentemente de solicitação de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="0ca93-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="0ca93-156">Compactação desabilitada ou arquivo não qualificado para compactação</span><span class="sxs-lookup"><span data-stu-id="0ca93-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="0ca93-157">Formato solicitado pelo cliente (por meio do cabeçalho Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="0ca93-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="0ca93-158">Formato de arquivo armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="0ca93-158">Cached file format</span></span> | <span data-ttu-id="0ca93-159">Cliente de toohello de resposta CDN</span><span class="sxs-lookup"><span data-stu-id="0ca93-159">CDN response toohello client</span></span> | <span data-ttu-id="0ca93-160">Observações</span><span class="sxs-lookup"><span data-stu-id="0ca93-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ca93-161">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-161">Compressed</span></span> |<span data-ttu-id="0ca93-162">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-162">Compressed</span></span> |<span data-ttu-id="0ca93-163">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-163">Compressed</span></span> | |
| <span data-ttu-id="0ca93-164">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-164">Compressed</span></span> |<span data-ttu-id="0ca93-165">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-165">Uncompressed</span></span> |<span data-ttu-id="0ca93-166">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-166">Uncompressed</span></span> | |
| <span data-ttu-id="0ca93-167">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-167">Compressed</span></span> |<span data-ttu-id="0ca93-168">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="0ca93-168">Not cached</span></span> |<span data-ttu-id="0ca93-169">Compactada ou descompactada</span><span class="sxs-lookup"><span data-stu-id="0ca93-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="0ca93-170">Depende da resposta de origem</span><span class="sxs-lookup"><span data-stu-id="0ca93-170">Depends on origin response</span></span> |
| <span data-ttu-id="0ca93-171">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-171">Uncompressed</span></span> |<span data-ttu-id="0ca93-172">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-172">Compressed</span></span> |<span data-ttu-id="0ca93-173">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-173">Uncompressed</span></span> | |
| <span data-ttu-id="0ca93-174">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-174">Uncompressed</span></span> |<span data-ttu-id="0ca93-175">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-175">Uncompressed</span></span> |<span data-ttu-id="0ca93-176">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-176">Uncompressed</span></span> | |
| <span data-ttu-id="0ca93-177">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-177">Uncompressed</span></span> |<span data-ttu-id="0ca93-178">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="0ca93-178">Not cached</span></span> |<span data-ttu-id="0ca93-179">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="0ca93-180">Compactação habilitada ou arquivo qualificado para compactação</span><span class="sxs-lookup"><span data-stu-id="0ca93-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="0ca93-181">Formato solicitado pelo cliente (por meio do cabeçalho Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="0ca93-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="0ca93-182">Formato de arquivo armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="0ca93-182">Cached file format</span></span> | <span data-ttu-id="0ca93-183">Cliente de toohello de resposta CDN</span><span class="sxs-lookup"><span data-stu-id="0ca93-183">CDN response toohello client</span></span> | <span data-ttu-id="0ca93-184">Observações</span><span class="sxs-lookup"><span data-stu-id="0ca93-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ca93-185">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-185">Compressed</span></span> |<span data-ttu-id="0ca93-186">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-186">Compressed</span></span> |<span data-ttu-id="0ca93-187">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-187">Compressed</span></span> |<span data-ttu-id="0ca93-188">CDN transcodifica entre os formatos com suporte</span><span class="sxs-lookup"><span data-stu-id="0ca93-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="0ca93-189">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-189">Compressed</span></span> |<span data-ttu-id="0ca93-190">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-190">Uncompressed</span></span> |<span data-ttu-id="0ca93-191">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-191">Compressed</span></span> |<span data-ttu-id="0ca93-192">CDN executa compactação</span><span class="sxs-lookup"><span data-stu-id="0ca93-192">CDN performs compression</span></span> |
| <span data-ttu-id="0ca93-193">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-193">Compressed</span></span> |<span data-ttu-id="0ca93-194">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="0ca93-194">Not cached</span></span> |<span data-ttu-id="0ca93-195">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-195">Compressed</span></span> |<span data-ttu-id="0ca93-196">O CDN executará compactação se a origem for retornada descompactada.</span><span class="sxs-lookup"><span data-stu-id="0ca93-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="0ca93-197">**A CDN do Azure da Verizon** passa Olá arquivo não compactado na primeira solicitação de saudação e, em seguida, compacta e caches Olá arquivo para solicitações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="0ca93-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="0ca93-198">Os arquivos com o cabeçalho `Cache-Control: no-cache` nunca serão compactados.</span><span class="sxs-lookup"><span data-stu-id="0ca93-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="0ca93-199">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-199">Uncompressed</span></span> |<span data-ttu-id="0ca93-200">Compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-200">Compressed</span></span> |<span data-ttu-id="0ca93-201">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-201">Uncompressed</span></span> |<span data-ttu-id="0ca93-202">CDN executa descompactação</span><span class="sxs-lookup"><span data-stu-id="0ca93-202">CDN performs decompression</span></span> |
| <span data-ttu-id="0ca93-203">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-203">Uncompressed</span></span> |<span data-ttu-id="0ca93-204">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-204">Uncompressed</span></span> |<span data-ttu-id="0ca93-205">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-205">Uncompressed</span></span> | |
| <span data-ttu-id="0ca93-206">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-206">Uncompressed</span></span> |<span data-ttu-id="0ca93-207">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="0ca93-207">Not cached</span></span> |<span data-ttu-id="0ca93-208">Não compactado</span><span class="sxs-lookup"><span data-stu-id="0ca93-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="0ca93-209">Compactação de CDN dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="0ca93-209">Media Services CDN Compression</span></span>
<span data-ttu-id="0ca93-210">Para CDN de serviços de mídia habilitado pontos de extremidade de streaming, a compactação é habilitada por padrão para os seguintes tipos de conteúdo de saudação: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="0ca93-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="0ca93-211">Você não pode habilitar/desabilitar a compactação para Olá mencionado tipos usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ca93-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="0ca93-212">Consulte também</span><span class="sxs-lookup"><span data-stu-id="0ca93-212">See also</span></span>
* [<span data-ttu-id="0ca93-213">Solucionando problemas de compactação de arquivo CDN</span><span class="sxs-lookup"><span data-stu-id="0ca93-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

