---
title: "Migrar um nome DNS ativo para o Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como migrar um nome de domínio DNS personalizado que já está atribuído a um site ativo ao Serviço de Aplicativo do Azure sem nenhum tempo de inatividade."
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
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="ed9cf-103">Migrar um nome DNS ativo para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ed9cf-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="ed9cf-104">Este artigo mostra como migrar um nome DNS ativo para o [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) sem nenhum tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="ed9cf-105">Quando você migra um site ativo e seu nome de domínio DNS para o Serviço de Aplicativo, o nome DNS já está atendendo ao tráfego em tempo real.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="ed9cf-106">Evite o tempo de inatividade na resolução do DNS durante a migração associando o nome DNS ativo preventivamente ao aplicativo Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="ed9cf-107">Caso não esteja preocupado com o tempo de inatividade na resolução do DNS, consulte [Mapear um nome DNS personalizado existente para Aplicativos Web do Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ed9cf-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed9cf-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ed9cf-108">Prerequisites</span></span>

<span data-ttu-id="ed9cf-109">Para concluir estas instruções:</span><span class="sxs-lookup"><span data-stu-id="ed9cf-109">To complete this how-to:</span></span>

- <span data-ttu-id="ed9cf-110">[Verifique se o aplicativo Serviço de Aplicativo não está na camada GRATUITA](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="ed9cf-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="ed9cf-111">Vincular o nome de domínio preventivamente</span><span class="sxs-lookup"><span data-stu-id="ed9cf-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="ed9cf-112">Ao vincular um domínio personalizado preventivamente, você obtém o seguinte antes mesmo de fazer quaisquer alterações nos registros DNS:</span><span class="sxs-lookup"><span data-stu-id="ed9cf-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="ed9cf-113">Verificar a propriedade de domínio</span><span class="sxs-lookup"><span data-stu-id="ed9cf-113">Verify domain ownership</span></span>
- <span data-ttu-id="ed9cf-114">Habilitar o nome de domínio para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ed9cf-114">Enable the domain name for your app</span></span>

<span data-ttu-id="ed9cf-115">Quando você finalmente migrar o nome DNS personalizado do site antigo para o aplicativo Serviço de Aplicativo, não haverá nenhum tempo de inatividade na resolução do DNS.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="ed9cf-116">Criar registro de verificação de domínio</span><span class="sxs-lookup"><span data-stu-id="ed9cf-116">Create domain verification record</span></span>

<span data-ttu-id="ed9cf-117">Para verificar a propriedade do domínio, adicione um registro TXT.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="ed9cf-118">O registro TXT mapeia de _awverify.&lt;subdomain>_ para _&lt;appname>.azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="ed9cf-119">O registro TXT necessário depende do registro DNS que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="ed9cf-120">Para obter exemplos, consulte a seguinte tabela (`@` normalmente representa o domínio raiz):</span><span class="sxs-lookup"><span data-stu-id="ed9cf-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="ed9cf-121">Exemplo de registro DNS</span><span class="sxs-lookup"><span data-stu-id="ed9cf-121">DNS record example</span></span> | <span data-ttu-id="ed9cf-122">Host TXT</span><span class="sxs-lookup"><span data-stu-id="ed9cf-122">TXT Host</span></span> | <span data-ttu-id="ed9cf-123">Valor TXT</span><span class="sxs-lookup"><span data-stu-id="ed9cf-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="ed9cf-124">@ (raiz)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-124">@ (root)</span></span> | <span data-ttu-id="ed9cf-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-125">_awverify_</span></span> | <span data-ttu-id="ed9cf-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="ed9cf-127">www (sub)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-127">www (sub)</span></span> | <span data-ttu-id="ed9cf-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-128">_awverify.www_</span></span> | <span data-ttu-id="ed9cf-129">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="ed9cf-130">\* (curinga)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-130">\* (wildcard)</span></span> | <span data-ttu-id="ed9cf-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-131">_awverify.\*_</span></span> | <span data-ttu-id="ed9cf-132">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="ed9cf-133">Na página de registros DNS, anote o tipo de registro do nome DNS que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="ed9cf-134">O Serviço de Aplicativo dá suporte a mapeamentos de CNAME e registros A.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="ed9cf-135">Habilitar o domínio para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ed9cf-135">Enable the domain for your app</span></span>

<span data-ttu-id="ed9cf-136">No [portal do Azure](https://portal.azure.com), no painel de navegação à esquerda da página do aplicativo, selecione **Domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="ed9cf-138">Na página **Domínios personalizados**, selecione o ícone **+** ao lado de **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="ed9cf-140">Digite o nome de domínio totalmente qualificado ao qual você adicionou o registro TXT, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="ed9cf-141">Para um domínio de curinga (como \*.contoso.com), você pode usar qualquer nome DNS que corresponde ao domínio de curinga.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="ed9cf-142">Selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-142">Select **Validate**.</span></span>

<span data-ttu-id="ed9cf-143">O botão **Adicionar nome do host** é ativado.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="ed9cf-144">Verifique se **Tipo de registro do nome do host** está definido como o tipo de registro DNS que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="ed9cf-145">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-145">Select **Add hostname**.</span></span>

![Adicionar nome DNS para o aplicativo](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="ed9cf-147">Pode levar algum tempo para que o novo nome do host seja refletido na página **Domínios personalizados** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="ed9cf-148">Tente atualizar o navegador para atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-148">Try refreshing the browser to update the data.</span></span>

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="ed9cf-150">Agora, o nome DNS personalizado está habilitado no Azure App.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="ed9cf-151">Remapear o nome DNS ativo</span><span class="sxs-lookup"><span data-stu-id="ed9cf-151">Remap the active DNS name</span></span>

<span data-ttu-id="ed9cf-152">Agora só resta remapear o registro DNS ativo para que ele aponte para o Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="ed9cf-153">No momento, ele ainda aponta para o site antigo.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="ed9cf-154">Copiar o endereço IP do aplicativo (somente o registro A)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="ed9cf-155">Se estiver fazendo o remapeamento de um registro CNAME, ignore esta seção.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="ed9cf-156">Para remapear um registro A, você precisa do endereço IP externo do aplicativo Serviço de Aplicativo, que é mostrado na página **Domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="ed9cf-157">Feche a página **Adicionar nome do host** selecionando **X** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="ed9cf-158">Na página **domínios personalizados**, copie o endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="ed9cf-160">Atualizar o registro DNS</span><span class="sxs-lookup"><span data-stu-id="ed9cf-160">Update the DNS record</span></span>

<span data-ttu-id="ed9cf-161">Novamente na página de registros DNS do provedor de domínio, selecione o registro DNS a ser remapeado.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="ed9cf-162">Para o exemplo de domínio raiz `contoso.com`, remapeie o registro A ou CNAME como os exemplos na seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="ed9cf-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="ed9cf-163">Exemplo de FQDN</span><span class="sxs-lookup"><span data-stu-id="ed9cf-163">FQDN example</span></span> | <span data-ttu-id="ed9cf-164">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="ed9cf-164">Record type</span></span> | <span data-ttu-id="ed9cf-165">Host</span><span class="sxs-lookup"><span data-stu-id="ed9cf-165">Host</span></span> | <span data-ttu-id="ed9cf-166">Valor</span><span class="sxs-lookup"><span data-stu-id="ed9cf-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="ed9cf-167">contoso.com (raiz)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-167">contoso.com (root)</span></span> | <span data-ttu-id="ed9cf-168">O </span><span class="sxs-lookup"><span data-stu-id="ed9cf-168">A</span></span> | `@` | <span data-ttu-id="ed9cf-169">Endereço IP de [Copiar o endereço IP do aplicativo](#info)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="ed9cf-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="ed9cf-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="ed9cf-171">CNAME</span></span> | `www` | <span data-ttu-id="ed9cf-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="ed9cf-173">\*.contoso.com (curinga)</span><span class="sxs-lookup"><span data-stu-id="ed9cf-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="ed9cf-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="ed9cf-174">CNAME</span></span> | _\*_ | <span data-ttu-id="ed9cf-175">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ed9cf-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="ed9cf-176">Salve suas configurações.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-176">Save your settings.</span></span>

<span data-ttu-id="ed9cf-177">As consultas DNS devem começar a serem resolvidas para o aplicativo Serviço de Aplicativo imediatamente após a propagação do DNS.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed9cf-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed9cf-178">Next steps</span></span>

<span data-ttu-id="ed9cf-179">Saiba como associar um certificado SSL personalizado ao Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed9cf-180">Associar um certificado SSL personalizado existente a Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="ed9cf-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
