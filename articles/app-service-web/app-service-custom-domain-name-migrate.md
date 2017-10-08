---
title: "aaaMigrate um DNS active nome tooAzure do serviço de aplicativo | Microsoft Docs"
description: "Saiba como toomigrate um nome de domínio DNS personalizado que já está atribuído a tooa live tooAzure do serviço de aplicativo do site sem qualquer tempo de inatividade."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="caf7a-103">Migrar um ativo tooAzure de nome DNS do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="caf7a-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="caf7a-104">Este artigo mostra como toomigrate um DNS active nome muito[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) sem qualquer tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="caf7a-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="caf7a-105">Quando você migra um site em tempo real e seu tooApp de nome de domínio DNS serviço, o nome DNS já está servindo tráfego ao vivo.</span><span class="sxs-lookup"><span data-stu-id="caf7a-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="caf7a-106">Você pode evitar o tempo de inatividade na resolução DNS durante a migração de saudação associando preventivamente Olá active DNS nome tooyour aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="caf7a-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="caf7a-107">Se você não estiver preocupado com tempo de inatividade na resolução de DNS, consulte [mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="caf7a-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caf7a-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="caf7a-108">Prerequisites</span></span>

<span data-ttu-id="caf7a-109">toocomplete nesse instruções:</span><span class="sxs-lookup"><span data-stu-id="caf7a-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="caf7a-110">[Verifique se o aplicativo Serviço de Aplicativo não está na camada GRATUITA](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="caf7a-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="caf7a-111">Associar o nome de domínio Olá preventivamente</span><span class="sxs-lookup"><span data-stu-id="caf7a-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="caf7a-112">Quando você associa um domínio personalizado preventivamente, realiza as seguinte Olá antes de fazer alterações nos registros DNS:</span><span class="sxs-lookup"><span data-stu-id="caf7a-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="caf7a-113">Verificar a propriedade de domínio</span><span class="sxs-lookup"><span data-stu-id="caf7a-113">Verify domain ownership</span></span>
- <span data-ttu-id="caf7a-114">Habilitar o nome de domínio de saudação para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="caf7a-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="caf7a-115">Quando você migra, por fim, seu nome DNS personalizado Olá antigo toohello de site do aplicativo de serviço de aplicativo, haverá sem tempo de inatividade na resolução de DNS.</span><span class="sxs-lookup"><span data-stu-id="caf7a-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="caf7a-116">Criar registro de verificação de domínio</span><span class="sxs-lookup"><span data-stu-id="caf7a-116">Create domain verification record</span></span>

<span data-ttu-id="caf7a-117">propriedade do domínio tooverify, adicionar um TXT registrar.</span><span class="sxs-lookup"><span data-stu-id="caf7a-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="caf7a-118">Olá registro TXT mapas de _awverify.&lt; subdomínio >_ too_&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="caf7a-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="caf7a-119">Olá registro TXT é necessário depende Olá deseja toomigrate de registro DNS.</span><span class="sxs-lookup"><span data-stu-id="caf7a-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="caf7a-120">Para obter exemplos, consulte Olá a tabela a seguir (`@` normalmente representa Olá domínio raiz):</span><span class="sxs-lookup"><span data-stu-id="caf7a-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="caf7a-121">Exemplo de registro DNS</span><span class="sxs-lookup"><span data-stu-id="caf7a-121">DNS record example</span></span> | <span data-ttu-id="caf7a-122">Host TXT</span><span class="sxs-lookup"><span data-stu-id="caf7a-122">TXT Host</span></span> | <span data-ttu-id="caf7a-123">Valor TXT</span><span class="sxs-lookup"><span data-stu-id="caf7a-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="caf7a-124">@ (raiz)</span><span class="sxs-lookup"><span data-stu-id="caf7a-124">@ (root)</span></span> | <span data-ttu-id="caf7a-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="caf7a-125">_awverify_</span></span> | <span data-ttu-id="caf7a-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="caf7a-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="caf7a-127">www (sub)</span><span class="sxs-lookup"><span data-stu-id="caf7a-127">www (sub)</span></span> | <span data-ttu-id="caf7a-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="caf7a-128">_awverify.www_</span></span> | <span data-ttu-id="caf7a-129">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="caf7a-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="caf7a-130">\* (curinga)</span><span class="sxs-lookup"><span data-stu-id="caf7a-130">\* (wildcard)</span></span> | <span data-ttu-id="caf7a-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="caf7a-131">_awverify.\*_</span></span> | <span data-ttu-id="caf7a-132">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="caf7a-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="caf7a-133">Em sua página de registros DNS, observe o tipo de registro de saudação do hello nome DNS que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="caf7a-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="caf7a-134">O Serviço de Aplicativo dá suporte a mapeamentos de CNAME e registros A.</span><span class="sxs-lookup"><span data-stu-id="caf7a-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="caf7a-135">Habilitar Olá domínio para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="caf7a-135">Enable hello domain for your app</span></span>

<span data-ttu-id="caf7a-136">Em Olá [portal do Azure](https://portal.azure.com), no hello navegação à esquerda da página de aplicativo hello, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="caf7a-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="caf7a-138">Em Olá **domínios personalizados** página, selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.</span><span class="sxs-lookup"><span data-stu-id="caf7a-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="caf7a-140">Nome de domínio totalmente qualificado do tipo hello que você adicionou o registro TXT de saudação, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="caf7a-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="caf7a-141">Para um domínio de curinga (como \*. contoso.com), você pode usar qualquer nome DNS que coincide com o domínio de curinga hello.</span><span class="sxs-lookup"><span data-stu-id="caf7a-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="caf7a-142">Selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="caf7a-142">Select **Validate**.</span></span>

<span data-ttu-id="caf7a-143">Olá **Adicionar nome de host** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="caf7a-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="caf7a-144">Verifique se **tipo de registro de nome de host** é definir o tipo de registro de DNS do toohello deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="caf7a-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="caf7a-145">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="caf7a-145">Select **Add hostname**.</span></span>

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="caf7a-147">Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="caf7a-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="caf7a-148">Tente atualizar os dados de saudação do hello navegador tooupdate.</span><span class="sxs-lookup"><span data-stu-id="caf7a-148">Try refreshing hello browser tooupdate hello data.</span></span>

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="caf7a-150">Agora, o nome DNS personalizado está habilitado no Azure App.</span><span class="sxs-lookup"><span data-stu-id="caf7a-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="caf7a-151">Remapear o nome do DNS do active Olá</span><span class="sxs-lookup"><span data-stu-id="caf7a-151">Remap hello active DNS name</span></span>

<span data-ttu-id="caf7a-152">Olá somente coisa toodo esquerdo é remapeamento seu ativo tooApp de toopoint de registro de DNS serviço.</span><span class="sxs-lookup"><span data-stu-id="caf7a-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="caf7a-153">Direita agora, ele ainda aponta site antigo tooyour.</span><span class="sxs-lookup"><span data-stu-id="caf7a-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="caf7a-154">Copie o endereço IP de saudação do aplicativo (somente um registro)</span><span class="sxs-lookup"><span data-stu-id="caf7a-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="caf7a-155">Se estiver fazendo o remapeamento de um registro CNAME, ignore esta seção.</span><span class="sxs-lookup"><span data-stu-id="caf7a-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="caf7a-156">tooremap um um registro, é necessário que o endereço IP externo do aplicativo de serviço de aplicativo hello que é mostrado na Olá **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="caf7a-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="caf7a-157">Olá fechar **Adicionar nome de host** página selecionando **X** no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="caf7a-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="caf7a-158">Em Olá **domínios personalizados** página, copie o endereço IP de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="caf7a-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="caf7a-160">Atualizar o registro DNS Olá</span><span class="sxs-lookup"><span data-stu-id="caf7a-160">Update hello DNS record</span></span>

<span data-ttu-id="caf7a-161">Em página de registros DNS de saudação do seu provedor de domínio, selecione tooremap de registro de DNS hello.</span><span class="sxs-lookup"><span data-stu-id="caf7a-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="caf7a-162">Para Olá `contoso.com` raiz de domínio exemplo, remapear o registro A ou CNAME hello como exemplos Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="caf7a-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="caf7a-163">Exemplo de FQDN</span><span class="sxs-lookup"><span data-stu-id="caf7a-163">FQDN example</span></span> | <span data-ttu-id="caf7a-164">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="caf7a-164">Record type</span></span> | <span data-ttu-id="caf7a-165">Host</span><span class="sxs-lookup"><span data-stu-id="caf7a-165">Host</span></span> | <span data-ttu-id="caf7a-166">Valor</span><span class="sxs-lookup"><span data-stu-id="caf7a-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="caf7a-167">contoso.com (raiz)</span><span class="sxs-lookup"><span data-stu-id="caf7a-167">contoso.com (root)</span></span> | <span data-ttu-id="caf7a-168">Uma</span><span class="sxs-lookup"><span data-stu-id="caf7a-168">A</span></span> | `@` | <span data-ttu-id="caf7a-169">Endereço IP do [endereço IP do aplicativo da saudação de cópia](#info)</span><span class="sxs-lookup"><span data-stu-id="caf7a-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="caf7a-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="caf7a-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="caf7a-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="caf7a-171">CNAME</span></span> | `www` | <span data-ttu-id="caf7a-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="caf7a-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="caf7a-173">\*.contoso.com (curinga)</span><span class="sxs-lookup"><span data-stu-id="caf7a-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="caf7a-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="caf7a-174">CNAME</span></span> | _\*_ | <span data-ttu-id="caf7a-175">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="caf7a-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="caf7a-176">Salve suas configurações.</span><span class="sxs-lookup"><span data-stu-id="caf7a-176">Save your settings.</span></span>

<span data-ttu-id="caf7a-177">Consultas DNS devem iniciar a resolução tooyour aplicativo de serviço de aplicativo imediatamente após a propagação DNS ocorre.</span><span class="sxs-lookup"><span data-stu-id="caf7a-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caf7a-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="caf7a-178">Next steps</span></span>

<span data-ttu-id="caf7a-179">Saiba como toobind um SSL personalizado tooApp serviço de certificado.</span><span class="sxs-lookup"><span data-stu-id="caf7a-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="caf7a-180">Associar um tooAzure de certificado SSL de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="caf7a-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
