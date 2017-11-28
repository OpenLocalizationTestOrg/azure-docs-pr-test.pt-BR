---
title: "compactação de arquivo aaaTroubleshooting no Azure CDN | Microsoft Docs"
description: "Solucione problemas com a compactação de arquivo da CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="b6c3e-103">Solucionando problemas de compactação de arquivo CDN</span><span class="sxs-lookup"><span data-stu-id="b6c3e-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="b6c3e-104">Este artigo ajuda você a solucionar problemas com a [compactação de arquivo CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b6c3e-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="b6c3e-105">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b6c3e-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="b6c3e-106">Como alternativa, você também pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="b6c3e-107">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="b6c3e-108">Sintoma</span><span class="sxs-lookup"><span data-stu-id="b6c3e-108">Symptom</span></span>
<span data-ttu-id="b6c3e-109">A compactação do ponto de extremidade está habilitada, mas os arquivos estão sendo retornados descompactados.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="b6c3e-110">toocheck se os arquivos estão sendo retornados compactados, você precisa toouse uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) ou seu navegador [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="b6c3e-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="b6c3e-111">Cabeçalhos de resposta HTTP de saudação seleção retornado com a CDN em cache conteúdos.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="b6c3e-112">Se houver um cabeçalho chamado `Content-Encoding` com um valor **gzip**, **bzip2** ou **deflate**, seu conteúdo será compactado.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Cabeçalho Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="b6c3e-114">Causa</span><span class="sxs-lookup"><span data-stu-id="b6c3e-114">Cause</span></span>
<span data-ttu-id="b6c3e-115">Há várias causas possíveis, incluindo:</span><span class="sxs-lookup"><span data-stu-id="b6c3e-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="b6c3e-116">Olá solicitou o conteúdo não está qualificado para compactação.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="b6c3e-117">A compactação não está habilitada para Olá tipo de arquivo solicitado.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="b6c3e-118">solicitação HTTP Olá não incluir um cabeçalho solicitando um tipo de compactação inválido.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="b6c3e-119">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b6c3e-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="b6c3e-120">Assim como a implantação de novos pontos de extremidade, as alterações de configuração de CDN levar alguns toopropagate tempo por meio da rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="b6c3e-121">Normalmente, as alterações são aplicadas dentro de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="b6c3e-122">Se esse for Olá pela primeira vez que você definiu a compactação para o ponto de extremidade CDN, você deve considerar a espera-se de que as configurações de compactação Olá tenham se propagado toohello POPs de toobe de 1 a 2 horas.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="b6c3e-123">Verifique se a solicitação de saudação</span><span class="sxs-lookup"><span data-stu-id="b6c3e-123">Verify hello request</span></span>
<span data-ttu-id="b6c3e-124">Primeiro, devemos fazer uma verificação de integridade rápido na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="b6c3e-125">Você pode usar o navegador [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview Olá solicitações feitas.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="b6c3e-126">Verifique se a solicitação hello está sendo enviada a URL de ponto de extremidade tooyour, `<endpointname>.azureedge.net`e não sua origem.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="b6c3e-127">Verifique se a solicitação Olá contém um **Accept-Encoding** cabeçalho e hello valor para esse cabeçalho contém **gzip**, **deflate**, ou **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="b6c3e-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="b6c3e-128">Os perfis da **CDN do Azure da Akamai** suportam somente a codificação **gzip**.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Cabeçalhos da solicitação CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="b6c3e-130">Verificar as configurações de compactação (perfil CDN Standard)</span><span class="sxs-lookup"><span data-stu-id="b6c3e-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="b6c3e-131">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN Standard do Azure da Verizon** ou **CDN Standard do Azure do Akamai**.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="b6c3e-132">Navegue de ponto de extremidade tooyour no hello [portal do Azure](https://portal.azure.com) e clique em Olá **configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="b6c3e-133">Verifique se a compactação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="b6c3e-134">Verifique se o tipo MIME Olá Olá conteúdo toobe compactado está incluído na lista de saudação dos formatos compactados.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Configurações de compactação CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="b6c3e-136">Verificar as configurações de compactação (perfil CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="b6c3e-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="b6c3e-137">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN Premium do Azure da Verizon** .</span><span class="sxs-lookup"><span data-stu-id="b6c3e-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="b6c3e-138">Navegue de ponto de extremidade tooyour no hello [portal do Azure](https://portal.azure.com) e clique em Olá **gerenciar** botão.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="b6c3e-139">portal suplementar Olá será aberto.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="b6c3e-140">Passe o mouse sobre Olá **HTTP grande** guia, em seguida, passe o mouse sobre Olá **as configurações de Cache** flutuante.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="b6c3e-141">Clique em **Compactação**.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-141">Click **Compression**.</span></span> 

* <span data-ttu-id="b6c3e-142">Verifique se a compactação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="b6c3e-143">Verifique se Olá **tipos de arquivo** lista contém uma lista separada por vírgulas (sem espaços) dos tipos MIME.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="b6c3e-144">Verifique se o tipo MIME Olá Olá conteúdo toobe compactado está incluído na lista de saudação dos formatos compactados.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Configurações de compactação premium CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="b6c3e-146">Verifique se o conteúdo de saudação é armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="b6c3e-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="b6c3e-147">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN do Azure da Verizon** (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="b6c3e-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="b6c3e-148">Usando ferramentas de desenvolvedor do navegador, verifique se o arquivo de saudação do hello resposta cabeçalhos tooensure é armazenado em cache na região Olá onde ele está sendo solicitado.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="b6c3e-149">Verificar Olá **Server** cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="b6c3e-150">cabeçalho Olá deve ter o formato de saudação **plataforma (ID do servidor/POP)**, como mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="b6c3e-151">Verificar Olá **X Cache** cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="b6c3e-152">deve ler o cabeçalho de saudação **ocorrências**.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-152">hello header should read **HIT**.</span></span>  

![Cabeçalhos de resposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="b6c3e-154">Verifique se o arquivo hello atende aos requisitos de tamanho de saudação</span><span class="sxs-lookup"><span data-stu-id="b6c3e-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="b6c3e-155">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN do Azure da Verizon** (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="b6c3e-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="b6c3e-156">toobe qualificada para compactação, um arquivo deve atender Olá seguindo os requisitos de tamanho:</span><span class="sxs-lookup"><span data-stu-id="b6c3e-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="b6c3e-157">Maior que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="b6c3e-158">Menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="b6c3e-159">Verificar Olá solicitação no servidor de origem Olá para um **Via** cabeçalho</span><span class="sxs-lookup"><span data-stu-id="b6c3e-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="b6c3e-160">Olá **Via** cabeçalho HTTP indica o servidor de web toohello que Olá solicitação está sendo passado por um servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="b6c3e-161">Servidores de web Microsoft IIS por padrão não compactar respostas quando Olá solicitação contém um **Via** cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="b6c3e-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="b6c3e-162">toooverride esse comportamento, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b6c3e-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="b6c3e-163">**IIS 6**: [definir HcNoCompressionForProxies = "FALSE" nas propriedades de Metabase do IIS Olá](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="b6c3e-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="b6c3e-164">**IIS 7 e superior**: [tanto **noCompressionForHttp10** e **noCompressionForProxies** tooFalse na configuração do servidor de saudação](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="b6c3e-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

