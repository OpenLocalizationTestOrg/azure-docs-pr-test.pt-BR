---
title: "aaaBuy um nome de domínio personalizado para aplicativos Web do Azure"
description: "Saiba como nome do toobuy um domínio personalizado com um aplicativo web no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="ac347-103">Comprar um nome de domínio personalizado para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="ac347-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="ac347-104">Domínios do Serviço de Aplicativo (versão prévia) são domínios de nível superior gerenciados diretamente no Azure.</span><span class="sxs-lookup"><span data-stu-id="ac347-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="ac347-105">Eles tornam mais fácil toomanage os domínios personalizados [aplicativos Web do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac347-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="ac347-106">Este tutorial mostra como toobuy um domínio de aplicativo de serviço e atribuir DNS nomes tooAzure os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="ac347-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="ac347-107">Este artigo é para o Serviço de Aplicativo do Azure (aplicativos Web, aplicativos de API, aplicativos móveis, aplicativos lógicos).</span><span class="sxs-lookup"><span data-stu-id="ac347-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="ac347-108">Para a máquina virtual do Azure ou no armazenamento do Azure, consulte [tooAzure de domínio do serviço de aplicativo atribuir VM ou armazenamento do Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="ac347-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="ac347-109">Para serviços de nuvem, consulte [Configurando um nome de domínio personalizado para um serviço de nuvem do Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac347-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac347-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac347-110">Prerequisites</span></span>

<span data-ttu-id="ac347-111">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="ac347-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="ac347-112">[Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/) ou use um aplicativo que você criou para outro tutorial.</span><span class="sxs-lookup"><span data-stu-id="ac347-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="ac347-113">Preparar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ac347-113">Prepare hello app</span></span>

<span data-ttu-id="ac347-114">domínios personalizados de toouse em aplicativos Web do Azure, seu aplicativo web [plano de serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve ser uma camada paga (**compartilhado**, **básica**, **padrão**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ac347-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="ac347-115">Nesta etapa, verifique se que esse aplicativo da web hello é em Olá suportado de preço.</span><span class="sxs-lookup"><span data-stu-id="ac347-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="ac347-116">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="ac347-116">Sign in tooAzure</span></span>

<span data-ttu-id="ac347-117">Olá abrir [portal do Azure](https://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac347-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="ac347-118">Navegue toohello aplicativo hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ac347-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="ac347-119">No menu à esquerda do hello, selecione **serviços de aplicativos**e, em seguida, selecione o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ac347-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="ac347-121">Página de gerenciamento Olá de saudação do aplicativo de serviço de aplicativo é exibida.</span><span class="sxs-lookup"><span data-stu-id="ac347-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="ac347-122">Saudação de verificação de preço</span><span class="sxs-lookup"><span data-stu-id="ac347-122">Check hello pricing tier</span></span>

<span data-ttu-id="ac347-123">No hello barra de navegação de página de aplicativo hello esquerda, role toohello **configurações** seção e selecione **escalar verticalmente (plano de serviço de aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="ac347-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="ac347-125">camada atual do aplicativo Hello é realçada por uma borda azul.</span><span class="sxs-lookup"><span data-stu-id="ac347-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="ac347-126">Verificar toomake se esse aplicativo hello não está em Olá **livre** camada.</span><span class="sxs-lookup"><span data-stu-id="ac347-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="ac347-127">DNS personalizado não é suportada no hello **livre** camada.</span><span class="sxs-lookup"><span data-stu-id="ac347-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="ac347-129">Se hello plano de serviço de aplicativo não é **livre**, feche Olá **Escolher tipo de preços** página e ir muito[domínio de saudação comprar](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="ac347-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="ac347-130">Dimensionar o hello plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ac347-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="ac347-131">Selecione qualquer uma das camadas não estão livres de saudação (**compartilhado**, **básica**, **padrão**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ac347-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="ac347-132">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="ac347-132">Click **Select**.</span></span>

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="ac347-134">Quando você vir Olá notificação a seguir, a operação de escala de saudação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="ac347-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmação da operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="ac347-136">Comprar Olá domínio</span><span class="sxs-lookup"><span data-stu-id="ac347-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="ac347-137">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="ac347-137">Sign in tooAzure</span></span>
<span data-ttu-id="ac347-138">Olá abrir [portal do Azure](https://portal.azure.com/) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac347-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="ac347-139">Inicializar Comprar domínio</span><span class="sxs-lookup"><span data-stu-id="ac347-139">Launch Buy domains</span></span>
<span data-ttu-id="ac347-140">Em Olá **aplicativos Web** , clique em nome de saudação do seu aplicativo web, selecione **configurações**e, em seguida, selecione **domínios personalizados**</span><span class="sxs-lookup"><span data-stu-id="ac347-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ac347-141">Em Olá **domínios personalizados** , clique em **comprar domínios**.</span><span class="sxs-lookup"><span data-stu-id="ac347-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="ac347-142">Configurar a compra de domínio Olá</span><span class="sxs-lookup"><span data-stu-id="ac347-142">Configure hello domain purchase</span></span>

<span data-ttu-id="ac347-143">Em Olá **domínio de serviço de aplicativo** página Olá **pesquisar domínio** caixa, digite o nome de domínio de saudação deseja toobuy e tipo `Enter`.</span><span class="sxs-lookup"><span data-stu-id="ac347-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="ac347-144">Olá sugeridos domínios disponíveis são mostrados abaixo de caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac347-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="ac347-145">Selecione um ou mais domínios que você deseja toobuy.</span><span class="sxs-lookup"><span data-stu-id="ac347-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="ac347-146">Clique em Olá **as informações de contato** e preencha o formulário de informações de contato do domínio hello.</span><span class="sxs-lookup"><span data-stu-id="ac347-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="ac347-147">Quando terminar, clique em **Okey** página de domínio do serviço de aplicativo toohello tooreturn.</span><span class="sxs-lookup"><span data-stu-id="ac347-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="ac347-148">É importante preencher todos os campos obrigatórios com a máxima precisão possível.</span><span class="sxs-lookup"><span data-stu-id="ac347-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="ac347-149">Dados incorretos para informações de contato podem resultar em domínios de toopurchase de falha.</span><span class="sxs-lookup"><span data-stu-id="ac347-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="ac347-150">Em seguida, selecione opções de saudação desejada para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="ac347-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="ac347-151">Consulte Olá explicações para a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac347-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="ac347-152">Configuração</span><span class="sxs-lookup"><span data-stu-id="ac347-152">Setting</span></span> | <span data-ttu-id="ac347-153">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="ac347-153">Suggested Value</span></span> | <span data-ttu-id="ac347-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac347-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="ac347-155">Renovação automática</span><span class="sxs-lookup"><span data-stu-id="ac347-155">Auto renew</span></span> | <span data-ttu-id="ac347-156">**Habilitar**</span><span class="sxs-lookup"><span data-stu-id="ac347-156">**Enable**</span></span> | <span data-ttu-id="ac347-157">Renova seu Domínio do Serviço de Aplicativo automaticamente todo ano.</span><span class="sxs-lookup"><span data-stu-id="ac347-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="ac347-158">Seu cartão de crédito é cobrado Olá mesmo preço de compra no momento de saudação da renovação.</span><span class="sxs-lookup"><span data-stu-id="ac347-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="ac347-159">Proteção de privacidade</span><span class="sxs-lookup"><span data-stu-id="ac347-159">Privacy protection</span></span> | <span data-ttu-id="ac347-160">Habilitar</span><span class="sxs-lookup"><span data-stu-id="ac347-160">Enable</span></span> | <span data-ttu-id="ac347-161">Aceitar muito "Proteção de privacidade," que está incluída no preço de compra Olá _gratuitamente_ (exceto para os domínios de nível superior cujo registro não suportam a proteção de privacidade, como _. co.in_, _. Co.uk_, e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="ac347-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="ac347-162">Atribuir nomes de host padrão</span><span class="sxs-lookup"><span data-stu-id="ac347-162">Assign default hostnames</span></span> | <span data-ttu-id="ac347-163">**www** e **@**</span><span class="sxs-lookup"><span data-stu-id="ac347-163">**www** and **@**</span></span> | <span data-ttu-id="ac347-164">Selecione Olá desejado associações de nome de host, se desejado.</span><span class="sxs-lookup"><span data-stu-id="ac347-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="ac347-165">Quando Olá domínio compra operação estiver concluída, seu aplicativo web pode ser acessado em nomes de host de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="ac347-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="ac347-166">Se Olá web aplicativo estiver atrás de [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), você não vir o domínio raiz da saudação opção tooassign hello (@), pois o Gerenciador de tráfego não não suporte a registros.</span><span class="sxs-lookup"><span data-stu-id="ac347-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="ac347-167">Você pode fazer alterações toohello atribuições de nome de host após a conclusão da compra de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="ac347-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="ac347-168">Aceitar os termos e comprar</span><span class="sxs-lookup"><span data-stu-id="ac347-168">Accept terms and purchase</span></span>

<span data-ttu-id="ac347-169">Clique em **termos legais** tooreview termos de saudação e encargos hello, clique em **comprar**.</span><span class="sxs-lookup"><span data-stu-id="ac347-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="ac347-170">Domínios do serviço de aplicativo usam domínios de saudação toohost DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac347-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="ac347-171">Além disso toohello taxa de registro de domínio, os encargos de uso do Azure DNS se aplicam.</span><span class="sxs-lookup"><span data-stu-id="ac347-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="ac347-172">Para obter informações, consulte [Preços do DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="ac347-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="ac347-173">Em Olá **domínio de serviço de aplicativo** , clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ac347-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="ac347-174">Enquanto a operação de saudação está em andamento, você verá Olá notificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac347-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="ac347-175">Saudação de nomes de host de teste</span><span class="sxs-lookup"><span data-stu-id="ac347-175">Test hello hostnames</span></span>

<span data-ttu-id="ac347-176">Se você tiver atribuído padrão nomes de host tooyour web app, você também verá uma notificação de êxito para cada nome de host selecionado.</span><span class="sxs-lookup"><span data-stu-id="ac347-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="ac347-177">Você também verá nomes de host de saudação selecionada no hello **domínios personalizados** página Olá **nomes de host** seção.</span><span class="sxs-lookup"><span data-stu-id="ac347-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="ac347-178">nomes de host tootest hello, navegue toohello listado os nomes de host no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac347-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="ac347-179">No exemplo hello Olá anterior a captura de tela, tente navegar too_kontoso.net_ e _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="ac347-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="ac347-180">Atribuir nomes de host tooweb aplicativo</span><span class="sxs-lookup"><span data-stu-id="ac347-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="ac347-181">Se você escolher não tooassign um ou mais nomes de host padrão tooyour web a aplicativo durante a saudação processo de compra, ou se você precisar tooassign um nome de host não listados, você pode atribuir um nome de host a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="ac347-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="ac347-182">Você também pode atribuir nomes de host em tooany de domínio do serviço de aplicativo hello outro aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="ac347-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="ac347-183">Olá etapas dependem se hello domínio de aplicativo do serviço e aplicativo web de saudação pertencem toohello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="ac347-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="ac347-184">Assinatura diferente: mapear registros de DNS personalizados do aplicativo da web toohello Olá domínio de serviço de aplicativo como um domínio externamente adquirido.</span><span class="sxs-lookup"><span data-stu-id="ac347-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="ac347-185">Para obter informações sobre DNS personalizado adicionando nomes tooan domínio de serviço de aplicativo, consulte [gerenciar registros de DNS personalizados](#custom).</span><span class="sxs-lookup"><span data-stu-id="ac347-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="ac347-186">toomap um aplicativo web de tooa de domínio externo de adquiridas, consulte [mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ac347-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="ac347-187">Mesma assinatura: Olá Use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ac347-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="ac347-188">Inicializar adição de nome do host</span><span class="sxs-lookup"><span data-stu-id="ac347-188">Launch add hostname</span></span>
<span data-ttu-id="ac347-189">Em Olá **serviços de aplicativos** página, o nome de saudação select de seu aplicativo web que você deseja tooassign os nomes de host para selecionar **configurações**e, em seguida, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="ac347-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="ac347-190">Certifique-se de que seu domínio adquirido está listado no hello **domínios de serviço de aplicativo** seção, mas não selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="ac347-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="ac347-191">Todos os domínios de serviço de aplicativo de saudação mesma assinatura são mostrados no Olá web app **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="ac347-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="ac347-192">Se seu domínio está na assinatura do aplicativo da web hello, mas você não pode vê-lo em seu aplicativo da web hello **domínios personalizados** página, tente reabrir Olá **domínios personalizados** página ou atualizar Olá página da Web.</span><span class="sxs-lookup"><span data-stu-id="ac347-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="ac347-193">Além disso, verifique sino de notificação Olá na parte superior de saudação do hello portal do Azure para falhas de criação ou de andamento.</span><span class="sxs-lookup"><span data-stu-id="ac347-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="ac347-194">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="ac347-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="ac347-195">Configurar nome do host</span><span class="sxs-lookup"><span data-stu-id="ac347-195">Configure hostname</span></span>
<span data-ttu-id="ac347-196">Em Olá **Adicionar nome de host** caixa de diálogo, digite o nome de domínio totalmente qualificado de saudação do seu domínio do serviço de aplicativo ou qualquer subdomínio.</span><span class="sxs-lookup"><span data-stu-id="ac347-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="ac347-197">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac347-197">For example:</span></span>

- <span data-ttu-id="ac347-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ac347-198">kontoso.net</span></span>
- <span data-ttu-id="ac347-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ac347-199">www.kontoso.net</span></span>
- <span data-ttu-id="ac347-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="ac347-200">abc.kontoso.net</span></span>

<span data-ttu-id="ac347-201">Quando terminar, selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="ac347-201">When finished, select **Validate**.</span></span> <span data-ttu-id="ac347-202">tipo de registro de nome de host de saudação é selecionado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="ac347-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="ac347-203">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="ac347-203">Select **Add hostname**.</span></span>

<span data-ttu-id="ac347-204">Quando a saudação operação estiver concluída, você verá uma notificação de êxito para Olá atribuído um nome de host.</span><span class="sxs-lookup"><span data-stu-id="ac347-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="ac347-205">Feche Adicionar nome do host</span><span class="sxs-lookup"><span data-stu-id="ac347-205">Close add hostname</span></span>
<span data-ttu-id="ac347-206">Em Olá **Adicionar nome de host** página, atribua a qualquer outro nome de host tooyour aplicativo da web, conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="ac347-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="ac347-207">Quando terminar, feche Olá **Adicionar nome de host** página.</span><span class="sxs-lookup"><span data-stu-id="ac347-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="ac347-208">Agora você deve ver hostname(s) Olá atribuída recentemente em seu aplicativo **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="ac347-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="ac347-209">Saudação de nomes de host de teste</span><span class="sxs-lookup"><span data-stu-id="ac347-209">Test hello hostnames</span></span>

<span data-ttu-id="ac347-210">Navegue toohello listado os nomes de host no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac347-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="ac347-211">No exemplo hello Olá anterior a captura de tela, tente navegar too_abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="ac347-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="ac347-212">Gerenciar registros DNS personalizados</span><span class="sxs-lookup"><span data-stu-id="ac347-212">Manage custom DNS records</span></span>

<span data-ttu-id="ac347-213">No Azure, os registros DNS para um Domínio do Serviço de Aplicativo são gerenciados usando [DNS do Azure](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="ac347-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="ac347-214">Você pode adicionar, remover e atualizar registros DNS, assim como para um domínio adquirido externamente.</span><span class="sxs-lookup"><span data-stu-id="ac347-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="ac347-215">Abrir o Domínio do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ac347-215">Open App Service Domain</span></span>

<span data-ttu-id="ac347-216">No hello portal do Azure, no menu da esquerda hello, selecione **mais serviços** > **domínios de serviço de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="ac347-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="ac347-217">Selecione Olá toomanage de domínio.</span><span class="sxs-lookup"><span data-stu-id="ac347-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="ac347-218">Acessar zona DNS</span><span class="sxs-lookup"><span data-stu-id="ac347-218">Access DNS zone</span></span>

<span data-ttu-id="ac347-219">No menu da esquerda do domínio hello, selecione **zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="ac347-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="ac347-220">Essa ação abre Olá [zona DNS](../dns/dns-zones-records.md) página do seu domínio do serviço de aplicativo no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac347-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="ac347-221">Para obter informações sobre como tooedit registros DNS, consulte [como zonas DNS toomanage Olá portal do Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac347-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="ac347-222">Cancelar compra (excluir domínio)</span><span class="sxs-lookup"><span data-stu-id="ac347-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="ac347-223">Depois de comprar Olá domínio de serviço de aplicativo, você tem cinco dias toocancel sua compra, para obter um reembolso total.</span><span class="sxs-lookup"><span data-stu-id="ac347-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="ac347-224">Depois de cinco dias, você pode excluir Olá domínio de serviço de aplicativo, mas não pode receber um reembolso.</span><span class="sxs-lookup"><span data-stu-id="ac347-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="ac347-225">Abrir o Domínio do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ac347-225">Open App Service Domain</span></span>

<span data-ttu-id="ac347-226">No hello portal do Azure, no menu da esquerda hello, selecione **mais serviços** > **domínios de serviço de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="ac347-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="ac347-227">Selecione Olá domínio tooyou deseja toocancel ou excluir.</span><span class="sxs-lookup"><span data-stu-id="ac347-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="ac347-228">Excluir associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="ac347-228">Delete hostname bindings</span></span>

<span data-ttu-id="ac347-229">No menu da esquerda do domínio hello, selecione **associações de Hostname**.</span><span class="sxs-lookup"><span data-stu-id="ac347-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="ac347-230">associações de nome de host de saudação de todos os serviços do Azure são listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="ac347-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="ac347-231">Você não pode excluir Olá domínio de serviço de aplicativo até que todas as associações de nome de host são excluídas.</span><span class="sxs-lookup"><span data-stu-id="ac347-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="ac347-232">Exclua cada associação de nome do host selecionando **…** > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="ac347-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="ac347-233">Depois que todas as associações de saudação são excluídas, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ac347-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="ac347-234">Cancelar ou excluir</span><span class="sxs-lookup"><span data-stu-id="ac347-234">Cancel or delete</span></span>

<span data-ttu-id="ac347-235">No menu da esquerda do domínio hello, selecione **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="ac347-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="ac347-236">Se Olá cancelamento no domínio Olá adquirido não período, selecione **cancelar a compra**.</span><span class="sxs-lookup"><span data-stu-id="ac347-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="ac347-237">Caso contrário, você verá um botão **Excluir** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="ac347-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="ac347-238">domínio de saudação toodelete sem um reembolso, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="ac347-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="ac347-239">Selecione **Okey** tooconfirm operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac347-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="ac347-240">Se você não quiser tooproceed, clique em qualquer lugar fora da caixa de diálogo de confirmação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac347-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="ac347-241">Após a conclusão da operação de hello, domínio Olá é liberado da sua assinatura e disponível para qualquer pessoa toopurchase novamente.</span><span class="sxs-lookup"><span data-stu-id="ac347-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
