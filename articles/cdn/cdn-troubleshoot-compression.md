---
title: "Solucionando problemas de compactação de arquivo na CDN do Azure | Microsoft Docs"
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="aca77-103">Solucionando problemas de compactação de arquivo CDN</span><span class="sxs-lookup"><span data-stu-id="aca77-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="aca77-104">Este artigo ajuda você a solucionar problemas com a [compactação de arquivo CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="aca77-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="aca77-105">Se você precisar de mais ajuda em qualquer momento neste artigo, você pode contatar os especialistas do Azure nos [fóruns do Azure MSDN e Excedente de Pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="aca77-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="aca77-106">Como alternativa, você também pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="aca77-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="aca77-107">Vá para o [site de Suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **Obter Suporte**.</span><span class="sxs-lookup"><span data-stu-id="aca77-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="aca77-108">Sintoma</span><span class="sxs-lookup"><span data-stu-id="aca77-108">Symptom</span></span>
<span data-ttu-id="aca77-109">A compactação do ponto de extremidade está habilitada, mas os arquivos estão sendo retornados descompactados.</span><span class="sxs-lookup"><span data-stu-id="aca77-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="aca77-110">Para verificar se os arquivos estão sendo retornados compactados, você precisará usar uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) ou as [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) do seu navegador.</span><span class="sxs-lookup"><span data-stu-id="aca77-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="aca77-111">Verifique os cabeçalhos de resposta HTTP retornados com o conteúdo CDN armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="aca77-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="aca77-112">Se houver um cabeçalho chamado `Content-Encoding` com um valor **gzip**, **bzip2** ou **deflate**, seu conteúdo será compactado.</span><span class="sxs-lookup"><span data-stu-id="aca77-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Cabeçalho Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="aca77-114">Causa</span><span class="sxs-lookup"><span data-stu-id="aca77-114">Cause</span></span>
<span data-ttu-id="aca77-115">Há várias causas possíveis, incluindo:</span><span class="sxs-lookup"><span data-stu-id="aca77-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="aca77-116">O conteúdo solicitado não está qualificado para compactação.</span><span class="sxs-lookup"><span data-stu-id="aca77-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="aca77-117">A compactação não está habilitada para o tipo de arquivo solicitado.</span><span class="sxs-lookup"><span data-stu-id="aca77-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="aca77-118">A solicitação HTTP não incluía um cabeçalho solicitando um tipo de compactação válido.</span><span class="sxs-lookup"><span data-stu-id="aca77-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="aca77-119">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="aca77-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="aca77-120">Assim como ocorre com a implantação de novos pontos de extremidade, alterações na configuração da CDN demoram um pouco para serem propagadas pela rede.</span><span class="sxs-lookup"><span data-stu-id="aca77-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="aca77-121">Normalmente, as alterações são aplicadas dentro de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="aca77-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="aca77-122">Se esta for a primeira vez que você configura a compactação do ponto de extremidade CDN, será necessário considerar uma espera de 1 a 2 horas para garantir que as configurações de compactação são propagadas para os POPs.</span><span class="sxs-lookup"><span data-stu-id="aca77-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="aca77-123">Verificar a solicitação</span><span class="sxs-lookup"><span data-stu-id="aca77-123">Verify the request</span></span>
<span data-ttu-id="aca77-124">Primeiro, devemos fazer uma verificação de integridade rápida na solicitação.</span><span class="sxs-lookup"><span data-stu-id="aca77-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="aca77-125">É possível usar as [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) do navegador para exibir as solicitações feitas no momento.</span><span class="sxs-lookup"><span data-stu-id="aca77-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="aca77-126">Verifique se a solicitação está sendo enviada para a URL do ponto de extremidade, `<endpointname>.azureedge.net`, e não para sua origem.</span><span class="sxs-lookup"><span data-stu-id="aca77-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="aca77-127">Verifique se a solicitação contém um cabeçalho **Accept-Encoding** e se o valor desse cabeçalho contém **gzip**, **deflate** ou **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="aca77-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="aca77-128">Os perfis da **CDN do Azure da Akamai** suportam somente a codificação **gzip**.</span><span class="sxs-lookup"><span data-stu-id="aca77-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Cabeçalhos da solicitação CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="aca77-130">Verificar as configurações de compactação (perfil CDN Standard)</span><span class="sxs-lookup"><span data-stu-id="aca77-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="aca77-131">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN Standard do Azure da Verizon** ou **CDN Standard do Azure do Akamai**.</span><span class="sxs-lookup"><span data-stu-id="aca77-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="aca77-132">Navegue até seu ponto de extremidade no [Portal do Azure](https://portal.azure.com) e clique no botão **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="aca77-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="aca77-133">Verifique se a compactação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="aca77-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="aca77-134">Verifique se o tipo MIME do conteúdo a ser compactado está incluído na lista de formatos compactados.</span><span class="sxs-lookup"><span data-stu-id="aca77-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Configurações de compactação CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="aca77-136">Verificar as configurações de compactação (perfil CDN Premium)</span><span class="sxs-lookup"><span data-stu-id="aca77-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="aca77-137">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN Premium do Azure da Verizon** .</span><span class="sxs-lookup"><span data-stu-id="aca77-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="aca77-138">Navegue até seu ponto de extremidade no [Portal do Azure](https://portal.azure.com) e clique no botão **Gerenciar** .</span><span class="sxs-lookup"><span data-stu-id="aca77-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="aca77-139">O portal suplementar será aberto.</span><span class="sxs-lookup"><span data-stu-id="aca77-139">The supplemental portal will open.</span></span>  <span data-ttu-id="aca77-140">Passe o mouse sobre a guia **HTTP Grande**, em seguida, sobre o submenu **Configurações do Cache**.</span><span class="sxs-lookup"><span data-stu-id="aca77-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="aca77-141">Clique em **Compactação**.</span><span class="sxs-lookup"><span data-stu-id="aca77-141">Click **Compression**.</span></span> 

* <span data-ttu-id="aca77-142">Verifique se a compactação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="aca77-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="aca77-143">Verifique se a lista **Tipos de Arquivo** contém uma lista separada por vírgula (sem espaços) de tipos MIME.</span><span class="sxs-lookup"><span data-stu-id="aca77-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="aca77-144">Verifique se o tipo MIME do conteúdo a ser compactado está incluído na lista de formatos compactados.</span><span class="sxs-lookup"><span data-stu-id="aca77-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Configurações de compactação premium CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="aca77-146">Verificar se que o conteúdo está armazenado em cache</span><span class="sxs-lookup"><span data-stu-id="aca77-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="aca77-147">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN do Azure da Verizon** (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="aca77-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="aca77-148">Usando as ferramentas de desenvolvedor do navegador, verifique os cabeçalhos de resposta para garantir que o arquivo está armazenado em cache na região em que está sendo solicitado.</span><span class="sxs-lookup"><span data-stu-id="aca77-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="aca77-149">Verifique o cabeçalho de resposta **Server** .</span><span class="sxs-lookup"><span data-stu-id="aca77-149">Check the **Server** response header.</span></span>  <span data-ttu-id="aca77-150">O cabeçalho deve ter o formato **Plataforma (POP/ID do Servidor)**, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="aca77-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="aca77-151">Verifique o cabeçalho de resposta **X-Cache** .</span><span class="sxs-lookup"><span data-stu-id="aca77-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="aca77-152">No cabeçalho, deve-se ler **HIT**.</span><span class="sxs-lookup"><span data-stu-id="aca77-152">The header should read **HIT**.</span></span>  

![Cabeçalhos de resposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="aca77-154">Verificar se o arquivo atende aos requisitos de tamanho</span><span class="sxs-lookup"><span data-stu-id="aca77-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="aca77-155">Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN do Azure da Verizon** (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="aca77-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="aca77-156">Para ser elegível para compactação, um arquivo deve atender aos seguintes requisitos de tamanho:</span><span class="sxs-lookup"><span data-stu-id="aca77-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="aca77-157">Maior que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="aca77-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="aca77-158">Menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="aca77-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="aca77-159">Verifique a solicitação no servidor de origem por um cabeçalho **Via**</span><span class="sxs-lookup"><span data-stu-id="aca77-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="aca77-160">O cabeçalho HTTP **Via** indica ao servidor Web que a solicitação está sendo passada por um servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="aca77-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="aca77-161">Por padrão, os servidores Web do Microsoft IIS não compactam as respostas quando a solicitação contém um cabeçalho **Via** .</span><span class="sxs-lookup"><span data-stu-id="aca77-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="aca77-162">Para substituir esse comportamento, execute o seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="aca77-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="aca77-163">**IIS 6**: [Defina HcNoCompressionForProxies="FALSE" nas propriedades do IIS Metabase](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="aca77-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="aca77-164">**IIS 7 e superior**: [defina **noCompressionForHttp10** e **noCompressionForProxies** como False na configuração do servidor](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="aca77-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

