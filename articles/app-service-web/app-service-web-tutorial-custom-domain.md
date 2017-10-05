---
title: Mapear um nome DNS personalizado existente para aplicativos Web do Azure | Documentos do Microsoft
description: "Saiba como adicionar um nome de domínio DNS personalizado existente (domínio intuitivo) a um aplicativo Web, back-end de aplicativo móvel ou aplicativo de API no Serviço de Aplicativo do Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="da0aa-103">Mapear um nome DNS personalizado existente para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="da0aa-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="da0aa-104">Os [aplicativos Web do Azure](app-service-web-overview.md) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="da0aa-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="da0aa-105">Este tutorial mostra como mapear um nome DNS personalizado existente para os Aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="da0aa-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="da0aa-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="da0aa-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="da0aa-108">Mapear um subdomínio (por exemplo, `www.contoso.com`) usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="da0aa-109">Mapear um domínio raiz (por exemplo, `contoso.com`) usando um registro A</span><span class="sxs-lookup"><span data-stu-id="da0aa-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="da0aa-110">Mapear um domínio curinga (por exemplo, `*.contoso.com`) usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="da0aa-111">Automatizar o mapeamento de domínio com scripts</span><span class="sxs-lookup"><span data-stu-id="da0aa-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="da0aa-112">Você pode usar um **registro CNAME** ou um **registro A** para mapear um nome DNS personalizado para o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="da0aa-113">É recomendável que você use um CNAME para todos os nomes DNS personalizados, exceto um domínio raiz (por exemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="da0aa-114">Para migrar um site ativo e seu nome de domínio DNS para o Serviço de Aplicativo, consulte [Migrar um nome DNS ativo para o Serviço de Aplicativo do Azure](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="da0aa-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da0aa-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da0aa-115">Prerequisites</span></span>

<span data-ttu-id="da0aa-116">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="da0aa-116">To complete this tutorial:</span></span>

* <span data-ttu-id="da0aa-117">[Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/) ou use um aplicativo que você criou para outro tutorial.</span><span class="sxs-lookup"><span data-stu-id="da0aa-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="da0aa-118">Compre um nome de domínio e verifique se você tem acesso ao registro DNS do provedor de domínio (como o GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="da0aa-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="da0aa-119">Por exemplo, para adicionar entradas DNS a `contoso.com` e `www.contoso.com`, você deve poder definir as configurações de DNS do domínio raiz de `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="da0aa-120">Caso não tenha um nome de domínio existente, considere a possibilidade de [comprar um domínio usando o portal do Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="da0aa-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="da0aa-121">Preparar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="da0aa-121">Prepare the app</span></span>

<span data-ttu-id="da0aa-122">Para mapear um nome DNS personalizado para um aplicativo Web, o [plano do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/) do aplicativo Web deve ser uma camada paga (**Compartilhado**, **Básico**, **Standard** ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="da0aa-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="da0aa-123">Nesta etapa, você verifica se o aplicativo do Serviço de Aplicativo está no tipo de preço com suporte.</span><span class="sxs-lookup"><span data-stu-id="da0aa-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="da0aa-124">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="da0aa-124">Sign in to Azure</span></span>

<span data-ttu-id="da0aa-125">Abra o [portal do Azure](https://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="da0aa-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="da0aa-126">Navegar para o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da0aa-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="da0aa-127">No menu à esquerda, selecione **Serviços de Aplicativos** e, em seguida, selecione o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="da0aa-129">A página de gerenciamento do aplicativo do Serviço de Aplicativo é exibida.</span><span class="sxs-lookup"><span data-stu-id="da0aa-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="da0aa-130">Verifique o tipo de preço</span><span class="sxs-lookup"><span data-stu-id="da0aa-130">Check the pricing tier</span></span>

<span data-ttu-id="da0aa-131">No painel de navegação à esquerda da página do aplicativo, role até a seção **Configurações** e selecione **Escalar verticalmente (plano do Serviço de Aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="da0aa-133">A camada atual do aplicativo é realçada por uma borda azul.</span><span class="sxs-lookup"><span data-stu-id="da0aa-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="da0aa-134">Verifique se o aplicativo não está na camada **Gratuita**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="da0aa-135">Não há suporte para DNS personalizado no tipo **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="da0aa-137">Se o plano do Serviço de Aplicativo não for **Gratuito**, feche a página **Escolher o tipo de preço** e vá para [Mapear um registro CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="da0aa-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="da0aa-138">Escalar verticalmente o plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="da0aa-138">Scale up the App Service plan</span></span>

<span data-ttu-id="da0aa-139">Selecione qualquer uma das camadas não estão livres (**compartilhado**, **básica**, **padrão**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="da0aa-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="da0aa-140">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-140">Click **Select**.</span></span>

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="da0aa-142">Quando você receber a notificação a seguir, a operação de escala terá sido concluída.</span><span class="sxs-lookup"><span data-stu-id="da0aa-142">When you see the following notification, the scale operation is complete.</span></span>

![Confirmação da operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="da0aa-144">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-144">Map a CNAME record</span></span>

<span data-ttu-id="da0aa-145">No exemplo do tutorial, você adiciona um registro CNAME ao subdomínio `www` (por exemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="da0aa-146">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-146">Create the CNAME record</span></span>

<span data-ttu-id="da0aa-147">Adicione um registro CNAME para mapear um subdomínio para o nome do host padrão do aplicativo (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="da0aa-148">Para o exemplo do domínio `www.contoso.com`, adicione um registro CNAME que mapeia o nome `www` para `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="da0aa-149">Depois de adicionar o CNAME, a página de registros DNS será parecida com o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="da0aa-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="da0aa-151">Habilitar o mapeamento de registro CNAME no Azure</span><span class="sxs-lookup"><span data-stu-id="da0aa-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="da0aa-152">No painel de navegação à esquerda da página do aplicativo no portal do Azure, selecione **Domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="da0aa-154">Na página **Domínios personalizados** do aplicativo, adicione o nome DNS personalizado totalmente qualificado (`www.contoso.com`) à lista.</span><span class="sxs-lookup"><span data-stu-id="da0aa-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="da0aa-155">Selecione o ícone **+** ao lado de **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-155">Select the **+** icon next to **Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="da0aa-157">Digite o nome de domínio totalmente qualificado ao qual você adicionou um registro CNAME, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="da0aa-158">Selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-158">Select **Validate**.</span></span>

<span data-ttu-id="da0aa-159">O botão **Adicionar nome do host** é ativado.</span><span class="sxs-lookup"><span data-stu-id="da0aa-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="da0aa-160">Verifique se **Tipo de registro de nome do host** está definido como **CNAME (www.example.com ou um subdomínio)**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="da0aa-161">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-161">Select **Add hostname**.</span></span>

![Adicionar nome DNS para o aplicativo](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="da0aa-163">Pode levar algum tempo para que o novo nome do host seja refletido na página **Domínios personalizados** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="da0aa-164">Tente atualizar o navegador para atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="da0aa-164">Try refreshing the browser to update the data.</span></span>

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="da0aa-166">Se você perdeu uma etapa ou cometeu um erro de digitação em algum lugar anteriormente, você verá um erro de verificação na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="da0aa-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="da0aa-168">Mapear um registro A</span><span class="sxs-lookup"><span data-stu-id="da0aa-168">Map an A record</span></span>

<span data-ttu-id="da0aa-169">No exemplo do tutorial, você adiciona um registro A ao domínio raiz (por exemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="da0aa-170">Copiar o endereço IP do aplicativo</span><span class="sxs-lookup"><span data-stu-id="da0aa-170">Copy the app's IP address</span></span>

<span data-ttu-id="da0aa-171">Para mapear um registro A, você precisa do endereço IP externo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="da0aa-172">Encontre esse endereço IP na página **Domínios personalizados** do aplicativo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="da0aa-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="da0aa-173">No painel de navegação à esquerda da página do aplicativo no portal do Azure, selecione **Domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="da0aa-175">Na página **domínios personalizados**, copie o endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="da0aa-177">Criar um conjunto A de registros</span><span class="sxs-lookup"><span data-stu-id="da0aa-177">Create the A record</span></span>

<span data-ttu-id="da0aa-178">Para mapear um registro A para um aplicativo, o Serviço de Aplicativo exige **dois** registros DNS:</span><span class="sxs-lookup"><span data-stu-id="da0aa-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="da0aa-179">Um registro **A** a ser mapeado para o endereço IP do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="da0aa-180">Um registro **TXT** a ser mapeado para o nome do host padrão do aplicativo `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="da0aa-181">O Serviço de Aplicativo usa esse registro somente em tempo de configuração, para verificar se você possui o domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="da0aa-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="da0aa-182">Depois que o domínio personalizado for validado e configurado no Serviço de Aplicativo, você poderá excluir esse registro TXT.</span><span class="sxs-lookup"><span data-stu-id="da0aa-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="da0aa-183">Para o `contoso.com` exemplo de domínio, crie os registros TXT e acordo com a tabela a seguir (`@` normalmente representa o domínio raiz).</span><span class="sxs-lookup"><span data-stu-id="da0aa-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="da0aa-184">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="da0aa-184">Record type</span></span> | <span data-ttu-id="da0aa-185">Host</span><span class="sxs-lookup"><span data-stu-id="da0aa-185">Host</span></span> | <span data-ttu-id="da0aa-186">Valor</span><span class="sxs-lookup"><span data-stu-id="da0aa-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="da0aa-187">O </span><span class="sxs-lookup"><span data-stu-id="da0aa-187">A</span></span> | `@` | <span data-ttu-id="da0aa-188">Endereço IP de [Copiar o endereço IP do aplicativo](#info)</span><span class="sxs-lookup"><span data-stu-id="da0aa-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="da0aa-189">TXT</span><span class="sxs-lookup"><span data-stu-id="da0aa-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="da0aa-190">Quando os registros são adicionados, a página de registros DNS fica parecida com o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="da0aa-190">When the records are added, the DNS records page looks like the following example:</span></span>

![Página de Registros DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="da0aa-192">Habilitar o mapeamento de registro A no aplicativo</span><span class="sxs-lookup"><span data-stu-id="da0aa-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="da0aa-193">De volta à página **Domínios personalizados** do aplicativo no portal do Azure, adicione o nome DNS personalizado totalmente qualificado (por exemplo, `contoso.com`) à lista.</span><span class="sxs-lookup"><span data-stu-id="da0aa-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="da0aa-194">Selecione o ícone **+** ao lado de **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-194">Select the **+** icon next to **Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="da0aa-196">Digite o nome de domínio totalmente qualificado para o qual você configurou o registro A, como `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="da0aa-197">Selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-197">Select **Validate**.</span></span>

<span data-ttu-id="da0aa-198">O botão **Adicionar nome do host** é ativado.</span><span class="sxs-lookup"><span data-stu-id="da0aa-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="da0aa-199">Verifique se **Tipo de registro de nome de host** está definido como **Registro A (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="da0aa-200">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-200">Select **Add hostname**.</span></span>

![Adicionar nome DNS para o aplicativo](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="da0aa-202">Pode levar algum tempo para que o novo nome do host seja refletido na página **Domínios personalizados** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="da0aa-203">Tente atualizar o navegador para atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="da0aa-203">Try refreshing the browser to update the data.</span></span>

![Registro A adicionado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="da0aa-205">Se você perdeu uma etapa ou cometeu um erro de digitação em algum lugar anteriormente, você verá um erro de verificação na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="da0aa-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="da0aa-207">Mapear um domínio curinga</span><span class="sxs-lookup"><span data-stu-id="da0aa-207">Map a wildcard domain</span></span>

<span data-ttu-id="da0aa-208">No exemplo do tutorial, você mapeia um [nome DNS curinga](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por exemplo, `*.contoso.com`) para o aplicativo do Serviço de Aplicativo adicionando um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="da0aa-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="da0aa-209">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-209">Create the CNAME record</span></span>

<span data-ttu-id="da0aa-210">Adicione um registro CNAME para mapear um nome curinga para o nome do host padrão do aplicativo (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="da0aa-211">Para o exemplo do domínio `*.contoso.com`, o registro CNAME mapeará o nome `*` para `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="da0aa-212">Quando o CNAME é adicionado, a página de registros DNS fica parecida com o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="da0aa-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="da0aa-214">Habilitar o mapeamento de registro CNAME no aplicativo</span><span class="sxs-lookup"><span data-stu-id="da0aa-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="da0aa-215">Agora você pode adicionar qualquer subdomínio que corresponde o nome curinga ao aplicativo (por exemplo, `sub1.contoso.com` e `sub2.contoso.com` correspondem a `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="da0aa-216">No painel de navegação à esquerda da página do aplicativo no portal do Azure, selecione **Domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="da0aa-218">Selecione o ícone **+** ao lado de **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-218">Select the **+** icon next to **Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="da0aa-220">Digite um nome de domínio totalmente qualificado que corresponde ao domínio curinga (por exemplo, `sub1.contoso.com`) e, em seguida, selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="da0aa-221">O botão **Adicionar nome do host** é ativado.</span><span class="sxs-lookup"><span data-stu-id="da0aa-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="da0aa-222">Verifique se **Tipo de registro de nome do host** está definido como **Registro CNAME (www.example.com ou um subdomínio)**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="da0aa-223">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="da0aa-223">Select **Add hostname**.</span></span>

![Adicionar nome DNS para o aplicativo](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="da0aa-225">Pode levar algum tempo para que o novo nome do host seja refletido na página **Domínios personalizados** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="da0aa-226">Tente atualizar o navegador para atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="da0aa-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="da0aa-227">Selecione o ícone **+** novamente para adicionar outro nome de host que corresponde ao domínio curinga.</span><span class="sxs-lookup"><span data-stu-id="da0aa-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="da0aa-228">Por exemplo, adicione `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="da0aa-228">For example, add `sub2.contoso.com`.</span></span>

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="da0aa-230">Testar no navegador</span><span class="sxs-lookup"><span data-stu-id="da0aa-230">Test in browser</span></span>

<span data-ttu-id="da0aa-231">Navegue para os nomes DNS que você configurou anteriormente (por exemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com` e `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="da0aa-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="da0aa-233">Automatizar com scripts</span><span class="sxs-lookup"><span data-stu-id="da0aa-233">Automate with scripts</span></span>

<span data-ttu-id="da0aa-234">Você pode automatizar o gerenciamento de domínios personalizados com scripts, usando o [CLI do Azure](/cli/azure/install-azure-cli) ou [PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da0aa-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="da0aa-235">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="da0aa-235">Azure CLI</span></span> 

<span data-ttu-id="da0aa-236">O comando a seguir adiciona um nome DNS personalizado configurado para um aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="da0aa-237">Para obter mais informações, consulte [Mapear um domínio personalizado para um aplicativo Web](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="da0aa-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="da0aa-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="da0aa-238">Azure PowerShell</span></span> 

<span data-ttu-id="da0aa-239">O comando a seguir adiciona um nome DNS personalizado configurado para um aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da0aa-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="da0aa-240">Para obter mais informações, consulte [Atribuir um domínio personalizado para um aplicativo web](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="da0aa-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da0aa-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da0aa-241">Next steps</span></span>

<span data-ttu-id="da0aa-242">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="da0aa-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="da0aa-243">Mapear um subdomínio usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="da0aa-244">Mapear um domínio raiz usando um registro A</span><span class="sxs-lookup"><span data-stu-id="da0aa-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="da0aa-245">Mapear um domínio curinga usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="da0aa-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="da0aa-246">Automatizar o mapeamento de domínio com scripts</span><span class="sxs-lookup"><span data-stu-id="da0aa-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="da0aa-247">Vá para o próximo tutorial para saber como associar um certificado SSL personalizado a um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="da0aa-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="da0aa-248">Associar um certificado SSL personalizado existente a Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="da0aa-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
