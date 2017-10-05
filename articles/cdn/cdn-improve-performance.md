---
title: Melhorar o desempenho compactando os arquivos na CDN do Azure | Microsoft Docs
description: "Saiba como melhorar a velocidade de transferência do arquivo e aumentar o desempenho de carregamento da página compactando os arquivos na CDN do Azure."
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
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="ffc82-103">Melhorar o desempenho compactando os arquivos na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ffc82-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="ffc82-104">A compactação é um método simples e eficiente para melhorar a velocidade de transferência de arquivos e aumentar o desempenho de carregamento de páginas, reduzindo o tamanho de arquivos antes de serem enviados do servidor.</span><span class="sxs-lookup"><span data-stu-id="ffc82-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="ffc82-105">Ela reduz os custos de largura de banda e oferece uma experiência mais responsiva para os seus usuários.</span><span class="sxs-lookup"><span data-stu-id="ffc82-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="ffc82-106">Há duas maneiras de habilitar a compactação:</span><span class="sxs-lookup"><span data-stu-id="ffc82-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="ffc82-107">Você pode habilitar a compactação em seu servidor de origem. Nesse caso, a CDN passa os arquivos compactados e entrega arquivos compactados para os clientes que os solicitem.</span><span class="sxs-lookup"><span data-stu-id="ffc82-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="ffc82-108">Você pode habilitar a compactação diretamente nos servidores de borda CDN; nesse caso, o CDN compacta os arquivos e os fornece aos usuários finais mesmo se eles não forem compactados pelo servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="ffc82-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffc82-109">As alterações de configuração de CDN levam algum tempo para se propagarem pela rede.</span><span class="sxs-lookup"><span data-stu-id="ffc82-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="ffc82-110">Para perfis <b>CDN do Azure do Akamai</b> , a propagação normalmente é concluída em menos de um minuto.</span><span class="sxs-lookup"><span data-stu-id="ffc82-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="ffc82-111">Para perfis <b>CDN do Azure da Verizon</b> , você geralmente verá suas alterações serem aplicadas em 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="ffc82-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="ffc82-112">Se esta for a primeira vez que você configura a compactação do seu ponto de extremidade CDN, será necessário considerar uma espera de 1 a 2 horas para garantir que as configurações de compactação sejam propagadas para os POPs antes de solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ffc82-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="ffc82-113">Habilitando a compactação</span><span class="sxs-lookup"><span data-stu-id="ffc82-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="ffc82-114">As camadas CDN Standard e Premium fornecem a mesma funcionalidade de compactação, mas a interface do usuário varia.</span><span class="sxs-lookup"><span data-stu-id="ffc82-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="ffc82-115">Para saber mais sobre as diferenças entre as camadas CDN Standard e Premium, confira [Visão geral da CDN do Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffc82-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="ffc82-116">Camada padrão</span><span class="sxs-lookup"><span data-stu-id="ffc82-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="ffc82-117">Esta seção aplica-se aos perfis da **CDN Standard do Azure da Verizon** e da **CDN Standard do Azure da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="ffc82-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="ffc82-118">Na página de perfil da CDN, clique no ponto de extremidade da CDN que deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="ffc82-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![Pontos de extremidade da página de perfil da CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="ffc82-120">A página do ponto de extremidade da CDN se abre.</span><span class="sxs-lookup"><span data-stu-id="ffc82-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="ffc82-121">Clique no botão **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="ffc82-121">Click the **Configure** button.</span></span>
   
    ![Botão de gerenciamento de página de perfil da CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="ffc82-123">A página de Configuração da CDN é aberta.</span><span class="sxs-lookup"><span data-stu-id="ffc82-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="ffc82-124">Habilitar **Compactação**.</span><span class="sxs-lookup"><span data-stu-id="ffc82-124">Turn on **Compression**.</span></span>
   
    ![Opções de compactação da CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="ffc82-126">Use os tipos padrão ou modifique a lista removendo ou adicionando tipos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="ffc82-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ffc82-127">Embora seja possível, não é recomendável aplicar a compactação a formatos compactados, como ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="ffc82-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="ffc82-128">Após fazer suas alterações, clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ffc82-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="ffc82-129">Camada premium</span><span class="sxs-lookup"><span data-stu-id="ffc82-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="ffc82-130">Esta seção aplica-se aos perfis **CDN do Azure Premium da Verizon** .</span><span class="sxs-lookup"><span data-stu-id="ffc82-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="ffc82-131">Na página de perfil da CDN, clique no botão **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="ffc82-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![Botão de gerenciamento de página de perfil da CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="ffc82-133">O portal de gerenciamento da CDN é aberto.</span><span class="sxs-lookup"><span data-stu-id="ffc82-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="ffc82-134">Passe o mouse sobre a guia **HTTP Grande**, em seguida, sobre o submenu **Configurações do Cache**.</span><span class="sxs-lookup"><span data-stu-id="ffc82-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="ffc82-135">Clique em **Compactação**.</span><span class="sxs-lookup"><span data-stu-id="ffc82-135">Click on **Compression**.</span></span>

    ![Seleção de compactação de arquivos](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="ffc82-137">As opções de compactação são exibidas.</span><span class="sxs-lookup"><span data-stu-id="ffc82-137">Compression options are displayed.</span></span>
   
    ![Compactação de arquivos](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="ffc82-139">Habilite a compactação clicando no botão de opção **Compactação Habilitada** .</span><span class="sxs-lookup"><span data-stu-id="ffc82-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="ffc82-140">Insira os tipos MIME que você deseja compactar como uma lista delimitada por vírgula (sem espaços) na caixa de texto **Tipos de Arquivo** .</span><span class="sxs-lookup"><span data-stu-id="ffc82-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ffc82-141">Embora seja possível, não é recomendável aplicar a compactação a formatos compactados, como ZIP, MP3, MP4, JPG, etc.</span><span class="sxs-lookup"><span data-stu-id="ffc82-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="ffc82-142">Depois de fazer as alterações, clique no botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="ffc82-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="ffc82-143">Regras de compactação</span><span class="sxs-lookup"><span data-stu-id="ffc82-143">Compression rules</span></span>
<span data-ttu-id="ffc82-144">Essas tabelas descrevem o comportamento de compactação CDN do Azure para cada cenário.</span><span class="sxs-lookup"><span data-stu-id="ffc82-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffc82-145">Para o **CDN do Azure da Verizon** (Standard e Premium), só os arquivos elegíveis são compactados.</span><span class="sxs-lookup"><span data-stu-id="ffc82-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="ffc82-146">Para se qualificar para a compactação, um arquivo deve:</span><span class="sxs-lookup"><span data-stu-id="ffc82-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="ffc82-147">Ser maior que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="ffc82-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="ffc82-148">Ser menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="ffc82-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="ffc82-149">Para o **CDN do Azure do Akamai**, todos os arquivos estão qualificados para compactação.</span><span class="sxs-lookup"><span data-stu-id="ffc82-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="ffc82-150">Para todos os produtos de CDN do Azure, um arquivo deve ser um tipo MIME que foi [configurado para compactação](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="ffc82-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="ffc82-151">Os perfis da **CDN do Azure da Verizon** (Standard e Premium) oferecem suporte à codificação **gzip** (GNU zip), **deflate**, **bzip2** ou **br** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="ffc82-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="ffc82-152">Para a codificação Brotli, a compactação é realizada apenas na borda.</span><span class="sxs-lookup"><span data-stu-id="ffc82-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="ffc82-153">O cliente/navegador deve enviar a solicitação para codificação Brotli, e o ativo compactado deve ter sido compactado primeiro no lado de origem.</span><span class="sxs-lookup"><span data-stu-id="ffc82-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="ffc82-154">Os perfis da **CDN do Azure da Akamai** oferecem suporte somente á codificação **gzip**.</span><span class="sxs-lookup"><span data-stu-id="ffc82-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="ffc82-155">Os pontos de extremidade da **CDN do Azure da Akamai** sempre solicitam os arquivos codificados **gzip** na origem, independentemente da solicitação do cliente.</span><span class="sxs-lookup"><span data-stu-id="ffc82-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="ffc82-156">Compactação desabilitada ou arquivo não qualificado para compactação</span><span class="sxs-lookup"><span data-stu-id="ffc82-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="ffc82-157">Formato solicitado pelo cliente (por meio do cabeçalho Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="ffc82-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="ffc82-158">Formato de arquivo armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="ffc82-158">Cached file format</span></span> | <span data-ttu-id="ffc82-159">Resposta CDN para o cliente</span><span class="sxs-lookup"><span data-stu-id="ffc82-159">CDN response to the client</span></span> | <span data-ttu-id="ffc82-160">Observações</span><span class="sxs-lookup"><span data-stu-id="ffc82-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ffc82-161">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-161">Compressed</span></span> |<span data-ttu-id="ffc82-162">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-162">Compressed</span></span> |<span data-ttu-id="ffc82-163">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-163">Compressed</span></span> | |
| <span data-ttu-id="ffc82-164">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-164">Compressed</span></span> |<span data-ttu-id="ffc82-165">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-165">Uncompressed</span></span> |<span data-ttu-id="ffc82-166">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-166">Uncompressed</span></span> | |
| <span data-ttu-id="ffc82-167">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-167">Compressed</span></span> |<span data-ttu-id="ffc82-168">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="ffc82-168">Not cached</span></span> |<span data-ttu-id="ffc82-169">Compactada ou descompactada</span><span class="sxs-lookup"><span data-stu-id="ffc82-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="ffc82-170">Depende da resposta de origem</span><span class="sxs-lookup"><span data-stu-id="ffc82-170">Depends on origin response</span></span> |
| <span data-ttu-id="ffc82-171">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-171">Uncompressed</span></span> |<span data-ttu-id="ffc82-172">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-172">Compressed</span></span> |<span data-ttu-id="ffc82-173">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-173">Uncompressed</span></span> | |
| <span data-ttu-id="ffc82-174">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-174">Uncompressed</span></span> |<span data-ttu-id="ffc82-175">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-175">Uncompressed</span></span> |<span data-ttu-id="ffc82-176">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-176">Uncompressed</span></span> | |
| <span data-ttu-id="ffc82-177">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-177">Uncompressed</span></span> |<span data-ttu-id="ffc82-178">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="ffc82-178">Not cached</span></span> |<span data-ttu-id="ffc82-179">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="ffc82-180">Compactação habilitada ou arquivo qualificado para compactação</span><span class="sxs-lookup"><span data-stu-id="ffc82-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="ffc82-181">Formato solicitado pelo cliente (por meio do cabeçalho Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="ffc82-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="ffc82-182">Formato de arquivo armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="ffc82-182">Cached file format</span></span> | <span data-ttu-id="ffc82-183">Resposta CDN para o cliente</span><span class="sxs-lookup"><span data-stu-id="ffc82-183">CDN response to the client</span></span> | <span data-ttu-id="ffc82-184">Observações</span><span class="sxs-lookup"><span data-stu-id="ffc82-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ffc82-185">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-185">Compressed</span></span> |<span data-ttu-id="ffc82-186">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-186">Compressed</span></span> |<span data-ttu-id="ffc82-187">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-187">Compressed</span></span> |<span data-ttu-id="ffc82-188">CDN transcodifica entre os formatos com suporte</span><span class="sxs-lookup"><span data-stu-id="ffc82-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="ffc82-189">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-189">Compressed</span></span> |<span data-ttu-id="ffc82-190">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-190">Uncompressed</span></span> |<span data-ttu-id="ffc82-191">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-191">Compressed</span></span> |<span data-ttu-id="ffc82-192">CDN executa compactação</span><span class="sxs-lookup"><span data-stu-id="ffc82-192">CDN performs compression</span></span> |
| <span data-ttu-id="ffc82-193">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-193">Compressed</span></span> |<span data-ttu-id="ffc82-194">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="ffc82-194">Not cached</span></span> |<span data-ttu-id="ffc82-195">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-195">Compressed</span></span> |<span data-ttu-id="ffc82-196">O CDN executará compactação se a origem for retornada descompactada.</span><span class="sxs-lookup"><span data-stu-id="ffc82-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="ffc82-197">**CDN do Azure da Verizon** passa o arquivo descompactado na primeira solicitação e, em seguida, compacta e armazena em cache o arquivo para solicitações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="ffc82-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="ffc82-198">Os arquivos com o cabeçalho `Cache-Control: no-cache` nunca serão compactados.</span><span class="sxs-lookup"><span data-stu-id="ffc82-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="ffc82-199">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-199">Uncompressed</span></span> |<span data-ttu-id="ffc82-200">Compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-200">Compressed</span></span> |<span data-ttu-id="ffc82-201">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-201">Uncompressed</span></span> |<span data-ttu-id="ffc82-202">CDN executa descompactação</span><span class="sxs-lookup"><span data-stu-id="ffc82-202">CDN performs decompression</span></span> |
| <span data-ttu-id="ffc82-203">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-203">Uncompressed</span></span> |<span data-ttu-id="ffc82-204">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-204">Uncompressed</span></span> |<span data-ttu-id="ffc82-205">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-205">Uncompressed</span></span> | |
| <span data-ttu-id="ffc82-206">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-206">Uncompressed</span></span> |<span data-ttu-id="ffc82-207">Não armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="ffc82-207">Not cached</span></span> |<span data-ttu-id="ffc82-208">Não compactado</span><span class="sxs-lookup"><span data-stu-id="ffc82-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="ffc82-209">Compactação de CDN dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ffc82-209">Media Services CDN Compression</span></span>
<span data-ttu-id="ffc82-210">Para pontos de extremidade de streaming habilitado para a CDN de Serviços de Mídia, a compactação está habilitada por padrão para os seguintes tipos de conteúdo: application/vnd.ms-sstr+xml,application/dash+xml,application/vnd.apple.mpegurl,application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="ffc82-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="ffc82-211">Você não pode habilitar/desabilitar a compactação para os tipos mencionados usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc82-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="ffc82-212">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ffc82-212">See also</span></span>
* [<span data-ttu-id="ffc82-213">Solucionando problemas de compactação de arquivo CDN</span><span class="sxs-lookup"><span data-stu-id="ffc82-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

