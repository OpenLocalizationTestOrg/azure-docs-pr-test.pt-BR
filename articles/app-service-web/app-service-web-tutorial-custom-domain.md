---
title: aaaMap um DNS personalizado existente nome tooAzure Web Apps | Microsoft Docs
description: "Saiba como tooadd um domínio DNS personalizado existente nome de aplicativo de web (domínio banido) tooa, back-end do aplicativo móvel ou aplicativo de API no serviço de aplicativo do Azure."
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
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="89af8-103">Mapear um tooAzure de nome DNS de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="89af8-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="89af8-104">Os [aplicativos Web do Azure](app-service-web-overview.md) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="89af8-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="89af8-105">Este tutorial mostra como toomap um DNS personalizado existente nome tooAzure os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="89af8-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="89af8-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="89af8-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89af8-108">Mapear um subdomínio (por exemplo, `www.contoso.com`) usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="89af8-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="89af8-109">Mapear um domínio raiz (por exemplo, `contoso.com`) usando um registro A</span><span class="sxs-lookup"><span data-stu-id="89af8-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="89af8-110">Mapear um domínio curinga (por exemplo, `*.contoso.com`) usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="89af8-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="89af8-111">Automatizar o mapeamento de domínio com scripts</span><span class="sxs-lookup"><span data-stu-id="89af8-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="89af8-112">Você pode usar um **registro CNAME** ou um **um registro** tooApp serviço de nome de toomap um DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="89af8-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="89af8-113">É recomendável que você use um CNAME para todos os nomes DNS personalizados, exceto um domínio raiz (por exemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="89af8-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="89af8-114">toomigrate um site em tempo real e seu tooApp de nome de domínio DNS serviço, consulte [migrar um ativo tooAzure de nome DNS do serviço de aplicativo](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="89af8-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89af8-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89af8-115">Prerequisites</span></span>

<span data-ttu-id="89af8-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="89af8-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="89af8-117">[Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/) ou use um aplicativo que você criou para outro tutorial.</span><span class="sxs-lookup"><span data-stu-id="89af8-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="89af8-118">Comprar um nome de domínio e verifique se você acessar toohello o registro DNS para o seu provedor de domínio (como GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="89af8-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="89af8-119">Por exemplo, as entradas DNS tooadd para `contoso.com` e `www.contoso.com`, você deve ser capaz de tooconfigure Olá configurações de DNS Olá `contoso.com` domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="89af8-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="89af8-120">Se você não tiver um domínio existente de nome, considere [comprar um domínio usando Olá portal do Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="89af8-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="89af8-121">Preparar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="89af8-121">Prepare hello app</span></span>

<span data-ttu-id="89af8-122">toomap um personalizado DNS nome tooa do aplicativo web, aplicativo web de saudação [plano de serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve ser uma camada paga (**compartilhado**, **básica**, **padrão**, ou  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="89af8-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="89af8-123">Nesta etapa, você verifique se esse aplicativo está em saudação do serviço de aplicativo hello suporte para a camada de preços.</span><span class="sxs-lookup"><span data-stu-id="89af8-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="89af8-124">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="89af8-124">Sign in tooAzure</span></span>

<span data-ttu-id="89af8-125">Olá abrir [portal do Azure](https://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="89af8-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="89af8-126">Navegue toohello aplicativo hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="89af8-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="89af8-127">No menu à esquerda do hello, selecione **serviços de aplicativos**e, em seguida, selecione o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="89af8-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="89af8-129">Página de gerenciamento Olá de saudação do aplicativo de serviço de aplicativo é exibida.</span><span class="sxs-lookup"><span data-stu-id="89af8-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="89af8-130">Saudação de verificação de preço</span><span class="sxs-lookup"><span data-stu-id="89af8-130">Check hello pricing tier</span></span>

<span data-ttu-id="89af8-131">No hello barra de navegação de página de aplicativo hello esquerda, role toohello **configurações** seção e selecione **escalar verticalmente (plano de serviço de aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="89af8-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="89af8-133">camada atual do aplicativo Hello é realçada por uma borda azul.</span><span class="sxs-lookup"><span data-stu-id="89af8-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="89af8-134">Verificar toomake se esse aplicativo hello não está em Olá **livre** camada.</span><span class="sxs-lookup"><span data-stu-id="89af8-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="89af8-135">DNS personalizado não é suportada no hello **livre** camada.</span><span class="sxs-lookup"><span data-stu-id="89af8-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="89af8-137">Se hello plano de serviço de aplicativo não é **livre**, feche Olá **Escolher tipo de preços** página e ir muito[mapear um registro CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="89af8-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="89af8-138">Dimensionar o hello plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="89af8-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="89af8-139">Selecione qualquer uma das camadas não estão livres de saudação (**compartilhado**, **básica**, **padrão**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="89af8-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="89af8-140">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="89af8-140">Click **Select**.</span></span>

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="89af8-142">Quando você vir Olá notificação a seguir, a operação de escala de saudação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="89af8-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmação da operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="89af8-144">Criar um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="89af8-144">Map a CNAME record</span></span>

<span data-ttu-id="89af8-145">Exemplo de tutorial hello, você adiciona um registro CNAME para Olá `www` subdomínio (por exemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="89af8-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="89af8-146">Criar registro CNAME Olá</span><span class="sxs-lookup"><span data-stu-id="89af8-146">Create hello CNAME record</span></span>

<span data-ttu-id="89af8-147">Adicionar nome do host padrão do aplicativo de toohello um subdomínio de um toomap de registro de CNAME (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="89af8-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="89af8-148">Para Olá `www.contoso.com` exemplo de domínio, adicione um registro CNAME que mapeia o nome hello `www` muito`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="89af8-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="89af8-149">Depois de adicionar Olá CNAME, página de registros DNS Olá aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="89af8-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="89af8-151">Habilitar o mapeamento de registro CNAME Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="89af8-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="89af8-152">No hello deixado navegação de página de aplicativo hello no hello portal do Azure, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="89af8-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="89af8-154">Em Olá **domínios personalizados** página do aplicativo hello, adicione Olá totalmente qualificado nome DNS personalizado (`www.contoso.com`) toohello lista.</span><span class="sxs-lookup"><span data-stu-id="89af8-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="89af8-155">Selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.</span><span class="sxs-lookup"><span data-stu-id="89af8-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="89af8-157">Nome de domínio totalmente qualificado do tipo hello que você adicionou um registro CNAME para, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="89af8-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="89af8-158">Selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="89af8-158">Select **Validate**.</span></span>

<span data-ttu-id="89af8-159">Olá **Adicionar nome de host** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="89af8-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="89af8-160">Verifique se **tipo de registro de nome de host** está definido muito**CNAME (www.example.com ou qualquer subdomínio)**.</span><span class="sxs-lookup"><span data-stu-id="89af8-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="89af8-161">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="89af8-161">Select **Add hostname**.</span></span>

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="89af8-163">Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="89af8-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="89af8-164">Tente atualizar os dados de saudação do hello navegador tooupdate.</span><span class="sxs-lookup"><span data-stu-id="89af8-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="89af8-166">Se você perdeu uma etapa ou digitação em algum lugar anteriormente, você verá um erro de verificação final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="89af8-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="89af8-168">Mapear um registro A</span><span class="sxs-lookup"><span data-stu-id="89af8-168">Map an A record</span></span>

<span data-ttu-id="89af8-169">Exemplo de tutorial hello, você adiciona um registro a para o domínio raiz da saudação (por exemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="89af8-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="89af8-170">Copie o endereço IP de saudação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="89af8-170">Copy hello app's IP address</span></span>

<span data-ttu-id="89af8-171">toomap um um registro, é necessário o endereço IP externo de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89af8-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="89af8-172">Você pode encontrar esse endereço IP do aplicativo hello **domínios personalizados** página Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89af8-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="89af8-173">No hello deixado navegação de página de aplicativo hello no hello portal do Azure, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="89af8-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="89af8-175">Em Olá **domínios personalizados** página, copie o endereço IP de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89af8-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="89af8-177">Crie um registro a saudação</span><span class="sxs-lookup"><span data-stu-id="89af8-177">Create hello A record</span></span>

<span data-ttu-id="89af8-178">requer o serviço de aplicativo toomap um um aplicativo de registro tooan, **duas** registros de DNS:</span><span class="sxs-lookup"><span data-stu-id="89af8-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="89af8-179">Um **um** registrar o endereço IP do toomap toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89af8-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="89af8-180">Um **TXT** registre o nome do host do aplicativo do toomap toohello padrão `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="89af8-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="89af8-181">Serviço de aplicativo usa esse registro somente em tempo de configuração, tooverify que você possui o domínio personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="89af8-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="89af8-182">Depois que o domínio personalizado for validado e configurado no Serviço de Aplicativo, você poderá excluir esse registro TXT.</span><span class="sxs-lookup"><span data-stu-id="89af8-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="89af8-183">Para Olá `contoso.com` exemplo de domínio, criar registros e TXT Olá toohello a tabela a seguir de acordo com (`@` normalmente representa Olá domínio raiz).</span><span class="sxs-lookup"><span data-stu-id="89af8-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="89af8-184">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="89af8-184">Record type</span></span> | <span data-ttu-id="89af8-185">Host</span><span class="sxs-lookup"><span data-stu-id="89af8-185">Host</span></span> | <span data-ttu-id="89af8-186">Valor</span><span class="sxs-lookup"><span data-stu-id="89af8-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="89af8-187">Uma</span><span class="sxs-lookup"><span data-stu-id="89af8-187">A</span></span> | `@` | <span data-ttu-id="89af8-188">Endereço IP do [endereço IP do aplicativo da saudação de cópia](#info)</span><span class="sxs-lookup"><span data-stu-id="89af8-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="89af8-189">TXT</span><span class="sxs-lookup"><span data-stu-id="89af8-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="89af8-190">Quando Olá registros são adicionados, Olá página de registros DNS aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="89af8-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Página de Registros DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="89af8-192">Habilitar Olá um mapeamento de registro no aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="89af8-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="89af8-193">No aplicativo hello **domínios personalizados** página Olá portal do Azure, adicione o nome personalizado do DNS totalmente qualificado do Olá (por exemplo, `contoso.com`) toohello lista.</span><span class="sxs-lookup"><span data-stu-id="89af8-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="89af8-194">Selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.</span><span class="sxs-lookup"><span data-stu-id="89af8-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="89af8-196">Nome de domínio totalmente qualificado do tipo hello configuradas Olá um registro, como `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="89af8-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="89af8-197">Selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="89af8-197">Select **Validate**.</span></span>

<span data-ttu-id="89af8-198">Olá **Adicionar nome de host** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="89af8-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="89af8-199">Verifique se **tipo de registro de nome de host** está definido muito**um registro (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="89af8-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="89af8-200">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="89af8-200">Select **Add hostname**.</span></span>

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="89af8-202">Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="89af8-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="89af8-203">Tente atualizar os dados de saudação do hello navegador tooupdate.</span><span class="sxs-lookup"><span data-stu-id="89af8-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Registro A adicionado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="89af8-205">Se você perdeu uma etapa ou digitação em algum lugar anteriormente, você verá um erro de verificação final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="89af8-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="89af8-207">Mapear um domínio curinga</span><span class="sxs-lookup"><span data-stu-id="89af8-207">Map a wildcard domain</span></span>

<span data-ttu-id="89af8-208">No exemplo de tutorial hello, você mapeia uma [nome DNS de curinga](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por exemplo, `*.contoso.com`) toohello aplicativo de serviço de aplicativo adicionando um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="89af8-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="89af8-209">Criar registro CNAME Olá</span><span class="sxs-lookup"><span data-stu-id="89af8-209">Create hello CNAME record</span></span>

<span data-ttu-id="89af8-210">Adicionar nome do host do aplicativo um curinga nome toohello padrão de um toomap de registro de CNAME (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="89af8-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="89af8-211">Para Olá `*.contoso.com` domínio exemplo hello registro CNAME mapeará nome hello `*` muito`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="89af8-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="89af8-212">Quando Olá CNAME é adicionado, Olá página de registros DNS aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="89af8-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="89af8-214">Habilitar o mapeamento de registro CNAME Olá no aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="89af8-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="89af8-215">Agora você pode adicionar qualquer subdomínio que corresponde a saudação curinga nome toohello aplicativo (por exemplo, `sub1.contoso.com` e `sub2.contoso.com` corresponder `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="89af8-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="89af8-216">No hello deixado navegação de página de aplicativo hello no hello portal do Azure, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="89af8-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="89af8-218">Selecione Olá  **+**  ícone Avançar muito**Adicionar nome de host**.</span><span class="sxs-lookup"><span data-stu-id="89af8-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Adicionar nome do host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="89af8-220">Digite um nome de domínio totalmente qualificado que corresponda Olá curinga domínio (por exemplo, `sub1.contoso.com`) e, em seguida, selecione **validar**.</span><span class="sxs-lookup"><span data-stu-id="89af8-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="89af8-221">Olá **Adicionar nome de host** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="89af8-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="89af8-222">Verifique se **tipo de registro de nome de host** está definido muito**registro CNAME (www.example.com ou qualquer subdomínio)**.</span><span class="sxs-lookup"><span data-stu-id="89af8-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="89af8-223">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="89af8-223">Select **Add hostname**.</span></span>

![Adicionar aplicativo de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="89af8-225">Pode levar algum tempo para Olá novo nome de host toobe refletida no aplicativo hello **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="89af8-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="89af8-226">Tente atualizar os dados de saudação do hello navegador tooupdate.</span><span class="sxs-lookup"><span data-stu-id="89af8-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="89af8-227">Selecione Olá  **+**  ícone novamente tooadd outro nome de host que corresponda Olá curinga domínio.</span><span class="sxs-lookup"><span data-stu-id="89af8-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="89af8-228">Por exemplo, adicione `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="89af8-228">For example, add `sub2.contoso.com`.</span></span>

![Registro CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="89af8-230">Testar no navegador</span><span class="sxs-lookup"><span data-stu-id="89af8-230">Test in browser</span></span>

<span data-ttu-id="89af8-231">Procurar toohello nomes DNS que você configurou anteriormente (por exemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, e `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="89af8-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="89af8-233">Automatizar com scripts</span><span class="sxs-lookup"><span data-stu-id="89af8-233">Automate with scripts</span></span>

<span data-ttu-id="89af8-234">Você pode automatizar o gerenciamento de domínios personalizados com scripts, usando Olá [CLI do Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="89af8-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="89af8-235">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="89af8-235">Azure CLI</span></span> 

<span data-ttu-id="89af8-236">saudação de comando a seguir adiciona uma tooan de nome DNS de personalizado configurado o aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89af8-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="89af8-237">Para obter mais informações, consulte [mapear um aplicativo web do domínio personalizado tooa](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="89af8-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="89af8-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89af8-238">Azure PowerShell</span></span> 

<span data-ttu-id="89af8-239">saudação de comando a seguir adiciona uma tooan de nome DNS de personalizado configurado o aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89af8-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="89af8-240">Para obter mais informações, consulte [atribuir um aplicativo web do domínio personalizado tooa](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="89af8-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89af8-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89af8-241">Next steps</span></span>

<span data-ttu-id="89af8-242">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="89af8-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89af8-243">Mapear um subdomínio usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="89af8-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="89af8-244">Mapear um domínio raiz usando um registro A</span><span class="sxs-lookup"><span data-stu-id="89af8-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="89af8-245">Mapear um domínio curinga usando um registro CNAME</span><span class="sxs-lookup"><span data-stu-id="89af8-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="89af8-246">Automatizar o mapeamento de domínio com scripts</span><span class="sxs-lookup"><span data-stu-id="89af8-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="89af8-247">Avançar toolearn tutorial do próximo toohello como toobind um SSL personalizado de certificado tooa web app.</span><span class="sxs-lookup"><span data-stu-id="89af8-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89af8-248">Associar um tooAzure de certificado SSL de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="89af8-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
