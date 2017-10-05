---
title: "Comprar um nome de domínio personalizado para aplicativos Web do Azure"
description: "Saiba como comprar um nome de domínio personalizado com um aplicativo Web no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="39a39-103">Comprar um nome de domínio personalizado para aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="39a39-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="39a39-104">Domínios do Serviço de Aplicativo (versão prévia) são domínios de nível superior gerenciados diretamente no Azure.</span><span class="sxs-lookup"><span data-stu-id="39a39-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="39a39-105">Eles facilitam o gerenciamento de domínios personalizados para [Aplicativos Web do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39a39-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="39a39-106">Este tutorial mostra como comprar um domínio de Serviço de Aplicativo e atribuir nomes DNS a Aplicativos Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="39a39-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="39a39-107">Este artigo é para o Serviço de Aplicativo do Azure (aplicativos Web, aplicativos de API, aplicativos móveis, aplicativos lógicos).</span><span class="sxs-lookup"><span data-stu-id="39a39-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="39a39-108">Para a VM do Azure ou Armazenamento do Azure, consulte [Atribuir o domínio do Serviço de Aplicativo para a VM Azure ou o Armazenamento do Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="39a39-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="39a39-109">Para serviços de nuvem, consulte [Configurando um nome de domínio personalizado para um serviço de nuvem do Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39a39-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39a39-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39a39-110">Prerequisites</span></span>

<span data-ttu-id="39a39-111">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="39a39-111">To complete this tutorial:</span></span>

* <span data-ttu-id="39a39-112">[Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/) ou use um aplicativo que você criou para outro tutorial.</span><span class="sxs-lookup"><span data-stu-id="39a39-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="39a39-113">Preparar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="39a39-113">Prepare the app</span></span>

<span data-ttu-id="39a39-114">Para usar domínios personalizados em Aplicativos Web do Azure, o [plano de Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/) do seu aplicativo Web deve ser uma camada paga (**Shared**, **Basic**, **Standard** ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="39a39-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="39a39-115">Nesta etapa, você precisa ter certeza de que seu aplicativo Web está no tipo de preço com suporte.</span><span class="sxs-lookup"><span data-stu-id="39a39-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="39a39-116">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="39a39-116">Sign in to Azure</span></span>

<span data-ttu-id="39a39-117">Abra o [portal do Azure](https://portal.azure.com) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="39a39-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="39a39-118">Navegar para o aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="39a39-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="39a39-119">No menu à esquerda, selecione **Serviços de Aplicativos** e, em seguida, selecione o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39a39-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="39a39-121">A página de gerenciamento do aplicativo do Serviço de Aplicativo é exibida.</span><span class="sxs-lookup"><span data-stu-id="39a39-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="39a39-122">Verifique o tipo de preço</span><span class="sxs-lookup"><span data-stu-id="39a39-122">Check the pricing tier</span></span>

<span data-ttu-id="39a39-123">No painel de navegação à esquerda da página do aplicativo, role até a seção **Configurações** e selecione **Escalar verticalmente (plano do Serviço de Aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="39a39-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="39a39-125">A camada atual do aplicativo é realçada por uma borda azul.</span><span class="sxs-lookup"><span data-stu-id="39a39-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="39a39-126">Verifique se o aplicativo não está na camada **Gratuita**.</span><span class="sxs-lookup"><span data-stu-id="39a39-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="39a39-127">Não há suporte para DNS personalizado no tipo **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="39a39-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="39a39-129">Se o plano do Serviço de Aplicativo não for **Gratuito**, feche a página **Escolher o tipo de preço** e vá para [Comprar o domínio](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="39a39-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="39a39-130">Escalar verticalmente o plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="39a39-130">Scale up the App Service plan</span></span>

<span data-ttu-id="39a39-131">Selecione qualquer uma das camadas não estão livres (**compartilhado**, **básica**, **padrão**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="39a39-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="39a39-132">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="39a39-132">Click **Select**.</span></span>

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="39a39-134">Quando você receber a notificação a seguir, a operação de escala terá sido concluída.</span><span class="sxs-lookup"><span data-stu-id="39a39-134">When you see the following notification, the scale operation is complete.</span></span>

![Confirmação da operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="39a39-136">Comprar o domínio</span><span class="sxs-lookup"><span data-stu-id="39a39-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="39a39-137">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="39a39-137">Sign in to Azure</span></span>
<span data-ttu-id="39a39-138">Abra o [portal do Azure](https://portal.azure.com/) e entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="39a39-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="39a39-139">Inicializar Comprar domínio</span><span class="sxs-lookup"><span data-stu-id="39a39-139">Launch Buy domains</span></span>
<span data-ttu-id="39a39-140">Na guia **Aplicativos Web**, clique no nome do seu aplicativo Web, selecione **Configuraçõe**s e selecione **Domínios personalizados**</span><span class="sxs-lookup"><span data-stu-id="39a39-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="39a39-141">Na página **Domínios personalizados**, clique em **Comprar domínios**.</span><span class="sxs-lookup"><span data-stu-id="39a39-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="39a39-142">Configurar a compra de domínio</span><span class="sxs-lookup"><span data-stu-id="39a39-142">Configure the domain purchase</span></span>

<span data-ttu-id="39a39-143">Na página **Domínio de Serviço de Aplicativo**, na caixa **Pesquisar domínio**, digite o nome de domínio que você deseja comprar e digite `Enter`.</span><span class="sxs-lookup"><span data-stu-id="39a39-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="39a39-144">Os domínios disponíveis sugeridos são mostrados logo abaixo da caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="39a39-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="39a39-145">Selecione um ou mais domínios que deseja comprar.</span><span class="sxs-lookup"><span data-stu-id="39a39-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="39a39-146">Clique em **Informações de Contato** e preencha o formulário de informações de contato do domínio.</span><span class="sxs-lookup"><span data-stu-id="39a39-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="39a39-147">Quando terminar, clique em **OK** para retornar à página de Domínio do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39a39-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="39a39-148">É importante preencher todos os campos obrigatórios com a máxima precisão possível.</span><span class="sxs-lookup"><span data-stu-id="39a39-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="39a39-149">Dados incorretos para informações de contato resultarão em falhas em comprar domínios.</span><span class="sxs-lookup"><span data-stu-id="39a39-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="39a39-150">Em seguida, selecione as opções desejadas para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="39a39-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="39a39-151">Consulte a tabela a seguir para obter explicações:</span><span class="sxs-lookup"><span data-stu-id="39a39-151">See the following table for explanations:</span></span>

| <span data-ttu-id="39a39-152">Configuração</span><span class="sxs-lookup"><span data-stu-id="39a39-152">Setting</span></span> | <span data-ttu-id="39a39-153">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="39a39-153">Suggested Value</span></span> | <span data-ttu-id="39a39-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="39a39-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="39a39-155">Renovação automática</span><span class="sxs-lookup"><span data-stu-id="39a39-155">Auto renew</span></span> | <span data-ttu-id="39a39-156">**Habilitar**</span><span class="sxs-lookup"><span data-stu-id="39a39-156">**Enable**</span></span> | <span data-ttu-id="39a39-157">Renova seu Domínio do Serviço de Aplicativo automaticamente todo ano.</span><span class="sxs-lookup"><span data-stu-id="39a39-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="39a39-158">Seu cartão de crédito é cobrado no mesmo preço de compra no momento da renovação.</span><span class="sxs-lookup"><span data-stu-id="39a39-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="39a39-159">Proteção de privacidade</span><span class="sxs-lookup"><span data-stu-id="39a39-159">Privacy protection</span></span> | <span data-ttu-id="39a39-160">Habilitar</span><span class="sxs-lookup"><span data-stu-id="39a39-160">Enable</span></span> | <span data-ttu-id="39a39-161">Escolha "Proteção de privacidade", que está incluída no preço de compra _gratuitamente_ (exceto por domínios de nível superior cujo registro não dê suporte a proteção de privacidade, como _.co.in_, _.co.uk_ e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="39a39-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="39a39-162">Atribuir nomes de host padrão</span><span class="sxs-lookup"><span data-stu-id="39a39-162">Assign default hostnames</span></span> | <span data-ttu-id="39a39-163">**www** e **@**</span><span class="sxs-lookup"><span data-stu-id="39a39-163">**www** and **@**</span></span> | <span data-ttu-id="39a39-164">Se você quiser, selecione as associações de nome do host desejadas.</span><span class="sxs-lookup"><span data-stu-id="39a39-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="39a39-165">Quando a operação de compra de domínio for concluída, seu aplicativo Web pode ser acessado nos nomes de host selecionados.</span><span class="sxs-lookup"><span data-stu-id="39a39-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="39a39-166">Se o aplicativo Web estiver por trás do [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/services/traffic-manager/), você não verá a opção de atribuir o domínio raiz (@), pois o Gerenciador de Tráfego não dá suporte a registros A.</span><span class="sxs-lookup"><span data-stu-id="39a39-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="39a39-167">Você pode fazer alterações às atribuições de nome do host após a compra de domínio ser concluída.</span><span class="sxs-lookup"><span data-stu-id="39a39-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="39a39-168">Aceitar os termos e comprar</span><span class="sxs-lookup"><span data-stu-id="39a39-168">Accept terms and purchase</span></span>

<span data-ttu-id="39a39-169">Clique em **Termos Legais** para examinar os termos e os encargos, clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="39a39-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="39a39-170">Domínios do Serviço de Aplicativo usam o DNS do Azure para hospedar os domínios.</span><span class="sxs-lookup"><span data-stu-id="39a39-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="39a39-171">Além da taxa de registro de domínio, encargos de uso do DNS do Azure se aplicam.</span><span class="sxs-lookup"><span data-stu-id="39a39-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="39a39-172">Para obter informações, consulte [Preços do DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="39a39-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="39a39-173">De volta à página **Domínio de Serviço de Aplicativo**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="39a39-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="39a39-174">Enquanto a operação estiver em andamento, você verá as seguintes notificações:</span><span class="sxs-lookup"><span data-stu-id="39a39-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="39a39-175">Testar os nomes de host</span><span class="sxs-lookup"><span data-stu-id="39a39-175">Test the hostnames</span></span>

<span data-ttu-id="39a39-176">Se você tiver atribuído nomes de host padrão ao seu aplicativo Web, também verá uma notificação de êxito para cada nome do host selecionado.</span><span class="sxs-lookup"><span data-stu-id="39a39-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="39a39-177">Você também verá os nomes de host selecionados na página **Domínios personalizados** na seção **Nomes de host**.</span><span class="sxs-lookup"><span data-stu-id="39a39-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="39a39-178">Para testar os nomes de host, navegue até os nomes de host listados no navegador.</span><span class="sxs-lookup"><span data-stu-id="39a39-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="39a39-179">O exemplo na captura de tela anterior, tente navegar para _kontoso.net_ e _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="39a39-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="39a39-180">Atribuir nomes de host ao aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="39a39-180">Assign hostnames to web app</span></span>

<span data-ttu-id="39a39-181">Se você optar por não atribuir um ou mais nomes de host padrão ao seu aplicativo Web durante o processo de compra ou, se for necessário atribuir um nome do host não listado, você poderá atribuir um nome do host a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="39a39-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="39a39-182">Você também pode atribuir nomes de host no Domínio de Serviço de Aplicativo a qualquer outro aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="39a39-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="39a39-183">As etapas dependem se o Domínio do Serviço de Aplicativo e o aplicativo Web pertencem à mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="39a39-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="39a39-184">Assinatura diferente: mapear registros de DNS personalizados do Domínio do Serviço de Aplicativo para o aplicativo Web como um domínio adquirido externamente.</span><span class="sxs-lookup"><span data-stu-id="39a39-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="39a39-185">Para obter informações sobre como adicionar nomes DNS personalizados a um Domínio do Serviço de Aplicativo, consulte [Gerenciar registros de DNS personalizados](#custom).</span><span class="sxs-lookup"><span data-stu-id="39a39-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="39a39-186">Para mapear um domínio adquirido externo para um aplicativo Web, consulte [Mapear um nome DNS personalizado existente para Aplicativos Web do Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="39a39-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="39a39-187">Mesma assinatura: use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="39a39-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="39a39-188">Inicializar adição de nome do host</span><span class="sxs-lookup"><span data-stu-id="39a39-188">Launch add hostname</span></span>
<span data-ttu-id="39a39-189">Na página **Serviços de Aplicativos**, selecione o nome do aplicativo Web ao qual você deseja atribuir nomes de host, selecione **Configurações** e, em seguida, selecione **Domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="39a39-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="39a39-190">Certifique-se de que seu domínio adquirido esteja listado na seção **Domínios do Serviço de Aplicativo**, mas não o selecione.</span><span class="sxs-lookup"><span data-stu-id="39a39-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="39a39-191">Todos os Domínios de Serviço de Aplicativo na mesma assinatura são mostrados na página **Domínios personalizados** do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="39a39-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="39a39-192">Se seu domínio estiver na assinatura do aplicativo Web, mas você não conseguir vê-lo na página **Domínios personalizados** do aplicativo Web, tente reabrir a página **Domínios personalizados** ou atualizar a página Web.</span><span class="sxs-lookup"><span data-stu-id="39a39-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="39a39-193">Além disso, verifique o sino de notificação na parte superior do portal do Azure para progresso ou falhas de criação.</span><span class="sxs-lookup"><span data-stu-id="39a39-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="39a39-194">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="39a39-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="39a39-195">Configurar nome do host</span><span class="sxs-lookup"><span data-stu-id="39a39-195">Configure hostname</span></span>
<span data-ttu-id="39a39-196">Na caixa de diálogo **Adicionar nome do host**, digite o nome de domínio totalmente qualificado do Domínio do Serviço de Aplicativo ou qualquer subdomínio.</span><span class="sxs-lookup"><span data-stu-id="39a39-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="39a39-197">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="39a39-197">For example:</span></span>

- <span data-ttu-id="39a39-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="39a39-198">kontoso.net</span></span>
- <span data-ttu-id="39a39-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="39a39-199">www.kontoso.net</span></span>
- <span data-ttu-id="39a39-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="39a39-200">abc.kontoso.net</span></span>

<span data-ttu-id="39a39-201">Quando terminar, selecione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="39a39-201">When finished, select **Validate**.</span></span> <span data-ttu-id="39a39-202">O tipo de registro de nome do host é selecionado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="39a39-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="39a39-203">Selecione **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="39a39-203">Select **Add hostname**.</span></span>

<span data-ttu-id="39a39-204">Quando a operação for concluída, você verá uma notificação de êxito para o nome do host atribuído.</span><span class="sxs-lookup"><span data-stu-id="39a39-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="39a39-205">Feche Adicionar nome do host</span><span class="sxs-lookup"><span data-stu-id="39a39-205">Close add hostname</span></span>
<span data-ttu-id="39a39-206">Na página **Adicionar nome do host**, atribua qualquer outro nome do host ao seu aplicativo Web, conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="39a39-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="39a39-207">Quando terminar, feche a página **Adicionar nome do host**.</span><span class="sxs-lookup"><span data-stu-id="39a39-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="39a39-208">Agora você deve ver os nomes do host recentemente atribuídos na página **Domínios personalizados** do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39a39-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="39a39-209">Testar os nomes de host</span><span class="sxs-lookup"><span data-stu-id="39a39-209">Test the hostnames</span></span>

<span data-ttu-id="39a39-210">Navegue até o nome do host listado no navegador.</span><span class="sxs-lookup"><span data-stu-id="39a39-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="39a39-211">No exemplo na captura de tela anterior, tente navegar para _abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="39a39-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="39a39-212">Gerenciar registros DNS personalizados</span><span class="sxs-lookup"><span data-stu-id="39a39-212">Manage custom DNS records</span></span>

<span data-ttu-id="39a39-213">No Azure, os registros DNS para um Domínio do Serviço de Aplicativo são gerenciados usando [DNS do Azure](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="39a39-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="39a39-214">Você pode adicionar, remover e atualizar registros DNS, assim como para um domínio adquirido externamente.</span><span class="sxs-lookup"><span data-stu-id="39a39-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="39a39-215">Abrir o Domínio do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="39a39-215">Open App Service Domain</span></span>

<span data-ttu-id="39a39-216">No portal do Azure, no menu à esquerda, selecione **Mais Serviços** > **Domínios do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="39a39-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="39a39-217">Selecione o domínio a gerenciar.</span><span class="sxs-lookup"><span data-stu-id="39a39-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="39a39-218">Acessar zona DNS</span><span class="sxs-lookup"><span data-stu-id="39a39-218">Access DNS zone</span></span>

<span data-ttu-id="39a39-219">No menu da esquerda do domínio, selecione **zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="39a39-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="39a39-220">Essa ação abre a página [Zona DNS](../dns/dns-zones-records.md) do seu Domínio do Serviço de Aplicativo no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="39a39-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="39a39-221">Para obter informações sobre como editar os registros DNS, consulte [Como gerenciar zonas DNS no portal do Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39a39-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="39a39-222">Cancelar compra (excluir domínio)</span><span class="sxs-lookup"><span data-stu-id="39a39-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="39a39-223">Depois de comprar o Domínio do Serviço de Aplicativo, você tem cinco dias para cancelar sua compra para obter um reembolso integral.</span><span class="sxs-lookup"><span data-stu-id="39a39-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="39a39-224">Depois de cinco dias, você pode excluir o Domínio do Serviço de Aplicativo, mas não pode receber um reembolso.</span><span class="sxs-lookup"><span data-stu-id="39a39-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="39a39-225">Abrir o Domínio do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="39a39-225">Open App Service Domain</span></span>

<span data-ttu-id="39a39-226">No portal do Azure, no menu à esquerda, selecione **Mais Serviços** > **Domínios do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="39a39-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="39a39-227">Selecione o domínio que você deseja cancelar ou excluir.</span><span class="sxs-lookup"><span data-stu-id="39a39-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="39a39-228">Excluir associações de nome de host</span><span class="sxs-lookup"><span data-stu-id="39a39-228">Delete hostname bindings</span></span>

<span data-ttu-id="39a39-229">No menu da esquerda do domínio, selecione **Associações de nome do host**.</span><span class="sxs-lookup"><span data-stu-id="39a39-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="39a39-230">As associações de nome do host de todos os serviços do Azure são listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="39a39-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="39a39-231">Você não pode excluir o Domínio de Serviço de Aplicativo até que todas as associações de nome de host sejam excluídas.</span><span class="sxs-lookup"><span data-stu-id="39a39-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="39a39-232">Exclua cada associação de nome do host selecionando **…** > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="39a39-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="39a39-233">Depois que todas as associações forem excluídas, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="39a39-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="39a39-234">Cancelar ou excluir</span><span class="sxs-lookup"><span data-stu-id="39a39-234">Cancel or delete</span></span>

<span data-ttu-id="39a39-235">No menu da esquerda do domínio, selecione **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="39a39-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="39a39-236">Se o período de cancelamento do domínio adquirido não tiver se passado, selecione **Cancelar compra**.</span><span class="sxs-lookup"><span data-stu-id="39a39-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="39a39-237">Caso contrário, você verá um botão **Excluir** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="39a39-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="39a39-238">Para excluir o domínio sem um reembolso, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="39a39-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="39a39-239">Selecione **OK** para confirmar a operação.</span><span class="sxs-lookup"><span data-stu-id="39a39-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="39a39-240">Se você não quiser continuar, clique em qualquer lugar fora da caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="39a39-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="39a39-241">Depois que a operação estiver concluída, o domínio será liberado da sua assinatura e ficará disponível para qualquer pessoa comprar novamente.</span><span class="sxs-lookup"><span data-stu-id="39a39-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
