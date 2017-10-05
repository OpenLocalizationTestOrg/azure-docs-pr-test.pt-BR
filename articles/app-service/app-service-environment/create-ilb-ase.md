---
title: "Como criar e usar um balanceador de carga interno com um ambiente do Serviço de Aplicativo do Azure"
description: "Detalhes sobre como criar e usar um ambiente do Serviço de Aplicativo do Azure isolado da Internet"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: e7f85aaf2d940f114248d5925a1e97fe0f6bda6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="b6326-103">Como criar e usar um balanceador de carga interno com um ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b6326-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="b6326-104">O Ambiente do Serviço de Aplicativo do Azure é uma implantação do Serviço de Aplicativo do Azure em uma sub-rede de uma VNet (rede virtual) do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6326-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="b6326-105">Há duas maneiras de implantar um ASE (Ambiente do Serviço de Aplicativo):</span><span class="sxs-lookup"><span data-stu-id="b6326-105">There are two ways to deploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="b6326-106">Com um VIP em um endereço IP externo, geralmente chamado de ASE externo.</span><span class="sxs-lookup"><span data-stu-id="b6326-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="b6326-107">Com um VIP em um endereço IP interno, geralmente chamado de ASE ILB devido ao ponto de extremidade interno ser um balanceador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="b6326-107">With a VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="b6326-108">Este artigo mostra como criar um ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="b6326-108">This article shows you how to create an ILB ASE.</span></span> <span data-ttu-id="b6326-109">Para obter uma visão geral do ASE, confira [Introdução aos ambientes do Serviço de Aplicativo][Intro].</span><span class="sxs-lookup"><span data-stu-id="b6326-109">For an overview on the ASE, see [Introduction to App Service environments][Intro].</span></span> <span data-ttu-id="b6326-110">Para saber como criar um ASE externo, confira [Como criar um ASE externo][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="b6326-110">To learn how to create an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="b6326-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b6326-111">Overview</span></span> ##

<span data-ttu-id="b6326-112">Um ASE pode ser implantado com um ponto de extremidade acessível pela Internet ou com um endereço IP em sua VNet.</span><span class="sxs-lookup"><span data-stu-id="b6326-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="b6326-113">Para definir o endereço IP como um endereço de VNet, o ASE deve ser implantado com um ILB.</span><span class="sxs-lookup"><span data-stu-id="b6326-113">To set the IP address to a VNet address, the ASE must be deployed with an ILB.</span></span> <span data-ttu-id="b6326-114">Para implantar o ASE com um ILB, você deve fornecer:</span><span class="sxs-lookup"><span data-stu-id="b6326-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="b6326-115">Seu próprio domínio, que você usa quando cria seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b6326-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="b6326-116">O certificado usado para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b6326-116">The certificate used for HTTPS.</span></span>
-   <span data-ttu-id="b6326-117">Gerenciamento de DNS para o seu domínio.</span><span class="sxs-lookup"><span data-stu-id="b6326-117">DNS management for your domain.</span></span>

<span data-ttu-id="b6326-118">Em troca, você pode fazer coisas como:</span><span class="sxs-lookup"><span data-stu-id="b6326-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="b6326-119">Hospedar aplicativos da intranet na nuvem com segurança e acessá-los por meio de uma VPN do Azure ExpressRoute ou site a site.</span><span class="sxs-lookup"><span data-stu-id="b6326-119">Host intranet applications securely in the cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="b6326-120">Hospedar aplicativos na nuvem que não estão listados em servidores DNS públicos.</span><span class="sxs-lookup"><span data-stu-id="b6326-120">Host apps in the cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="b6326-121">Criar aplicativos back-end isolados da Internet, que podem ser integrados com seus aplicativos front-end com segurança.</span><span class="sxs-lookup"><span data-stu-id="b6326-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="b6326-122">Funcionalidade desabilitada</span><span class="sxs-lookup"><span data-stu-id="b6326-122">Disabled functionality</span></span> ###

<span data-ttu-id="b6326-123">Há algumas coisas que você não pode fazer ao usar um ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="b6326-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="b6326-124">Usar SSL baseado em IP.</span><span class="sxs-lookup"><span data-stu-id="b6326-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="b6326-125">Atribuir endereços IP a aplicativos específicos.</span><span class="sxs-lookup"><span data-stu-id="b6326-125">Assign IP addresses to specific apps.</span></span>
-   <span data-ttu-id="b6326-126">Comprar e usar um certificado com um aplicativo por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6326-126">Buy and use a certificate with an app through the Azure portal.</span></span> <span data-ttu-id="b6326-127">Você pode obter certificados diretamente de uma autoridade de certificação e usá-los com seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b6326-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="b6326-128">Não é possível obtê-los por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6326-128">You can't obtain them through the Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="b6326-129">Criar um ASE ILB</span><span class="sxs-lookup"><span data-stu-id="b6326-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="b6326-130">Para criar um ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="b6326-130">To create an ILB ASE:</span></span>

1. <span data-ttu-id="b6326-131">No Portal do Azure, escolha **Novo** > **Web + Móvel** > **Ambiente do Serviço de Aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="b6326-131">In the Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="b6326-132">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b6326-132">Select your subscription.</span></span>

3. <span data-ttu-id="b6326-133">Selecione ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b6326-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="b6326-134">Selecione ou crie uma VNet.</span><span class="sxs-lookup"><span data-stu-id="b6326-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="b6326-135">Ao selecionar uma VNet existente, você precisa criar uma sub-rede para manter o ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-135">If you select an existing VNet, you need to create a subnet to hold the ASE.</span></span> <span data-ttu-id="b6326-136">Lembre-se de definir um tamanho de sub-rede grande o suficiente para acomodar qualquer crescimento futuro do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-136">Make sure to set a subnet size large enough to accommodate any future growth of your ASE.</span></span> <span data-ttu-id="b6326-137">O tamanho recomendado é `/25`, que tem 128 endereços e é compatível com um ASE com tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="b6326-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="b6326-138">E o tamanho mínimo que você pode selecionar é `/28`.</span><span class="sxs-lookup"><span data-stu-id="b6326-138">The minimum size you can select is a `/28`.</span></span> <span data-ttu-id="b6326-139">Dependendo da necessidade da infraestrutura, esse tamanho pode ser dimensionado para um máximo de 11 instâncias.</span><span class="sxs-lookup"><span data-stu-id="b6326-139">After infrastructure needs, this size can be scaled to a maximum of 11 instances.</span></span>

    * <span data-ttu-id="b6326-140">Vá além do padrão máximo de 100 instâncias nos planos do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6326-140">Go beyond the default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="b6326-141">Dimensione cerca de 100, mas com dimensionamento de front-end mais rápido.</span><span class="sxs-lookup"><span data-stu-id="b6326-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="b6326-142">Selecione **Rede Virtual/Local** > **Configuração de Rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="b6326-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="b6326-143">Defina o **Tipo de VIP** como **Interno**.</span><span class="sxs-lookup"><span data-stu-id="b6326-143">Set the **VIP Type** to **Internal**.</span></span>

7. <span data-ttu-id="b6326-144">Digite um nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="b6326-144">Enter a domain name.</span></span> <span data-ttu-id="b6326-145">Esse domínio é usado para aplicativos criados neste ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-145">This domain is the one used for apps created in this ASE.</span></span> <span data-ttu-id="b6326-146">Há algumas restrições.</span><span class="sxs-lookup"><span data-stu-id="b6326-146">There are some restrictions.</span></span> <span data-ttu-id="b6326-147">Ele não pode ser:</span><span class="sxs-lookup"><span data-stu-id="b6326-147">It can't be:</span></span>

    * <span data-ttu-id="b6326-148">net</span><span class="sxs-lookup"><span data-stu-id="b6326-148">net</span></span>   

    * <span data-ttu-id="b6326-149">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b6326-149">azurewebsites.net</span></span>

    * <span data-ttu-id="b6326-150">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b6326-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="b6326-151">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b6326-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="b6326-152">O nome de domínio personalizado usado para aplicativos e o nome de domínio usado pelo seu ASE não podem ser os mesmos.</span><span class="sxs-lookup"><span data-stu-id="b6326-152">The custom domain name used for apps and the domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="b6326-153">Em um ASE ILB com o nome de domínio _contoso.com_, não é possível usar nomes de domínio personalizados para seus aplicativos, como:</span><span class="sxs-lookup"><span data-stu-id="b6326-153">For an ILB ASE with the domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="b6326-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="b6326-154">www.contoso.com</span></span>

    * <span data-ttu-id="b6326-155">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="b6326-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="b6326-156">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="b6326-156">abcd.contoso.com</span></span>

   <span data-ttu-id="b6326-157">Se você souber os nomes de domínio personalizados dos seus aplicativos, escolha um domínio para o ASE ILB que não seja conflitante com os nomes de domínio personalizados.</span><span class="sxs-lookup"><span data-stu-id="b6326-157">If you know the custom domain names for your apps, choose a domain for the ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="b6326-158">Neste exemplo, você pode usar algo como *contoso-internal.com* para o domínio do seu ASE porque isso não entra em conflito com os nomes de domínio personalizados que terminam em *.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="b6326-158">In this example, you can use something like *contoso-internal.com* for the domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="b6326-159">Selecione **OK** e, então, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b6326-159">Select **OK**, and then select **Create**.</span></span>

    ![Criação de ASE][1]

<span data-ttu-id="b6326-161">Na folha **Rede Virtual**, há uma opção **Configuração da Rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="b6326-161">On the **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="b6326-162">Você pode usá-la para selecionar um VIP Externo ou um VIP Interno.</span><span class="sxs-lookup"><span data-stu-id="b6326-162">You can use it to select an External VIP or an Internal VIP.</span></span> <span data-ttu-id="b6326-163">O padrão é **Externo**.</span><span class="sxs-lookup"><span data-stu-id="b6326-163">The default is **External**.</span></span> <span data-ttu-id="b6326-164">Se você selecionar **Externo**, o seu ASE usará um VIP acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="b6326-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="b6326-165">Se você selecionar **Interno**, o seu ASE será configurado com um ILB em um endereço IP na sua VNet.</span><span class="sxs-lookup"><span data-stu-id="b6326-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="b6326-166">Depois de selecionar **Interno**, não é possível adicionar mais endereços IP ao seu ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-166">After you select **Internal**, the ability to add more IP addresses to your ASE is removed.</span></span> <span data-ttu-id="b6326-167">Em vez disso, você precisa fornecer o domínio do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-167">Instead, you need to provide the domain of the ASE.</span></span> <span data-ttu-id="b6326-168">Em um ASE com um VIP Externo, o nome do ASE é usado no domínio dos aplicativos criados nesse ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-168">In an ASE with an External VIP, the name of the ASE is used in the domain for apps created in that ASE.</span></span>

<span data-ttu-id="b6326-169">Se você definir **Tipo de VIP** como **Interno**, o nome do ASE não será usado no domínio do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-169">If you set **VIP Type** to **Internal**, your ASE name is not used in the domain for the ASE.</span></span> <span data-ttu-id="b6326-170">Especifique o domínio explicitamente.</span><span class="sxs-lookup"><span data-stu-id="b6326-170">You specify the domain explicitly.</span></span> <span data-ttu-id="b6326-171">Se o domínio for *contoso.corp.net* e você criar um aplicativo nesse ASE chamado *timereporting*, a URL desse aplicativo será timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="b6326-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, the URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="b6326-172">Como criar um aplicativo em uma ASE ILB</span><span class="sxs-lookup"><span data-stu-id="b6326-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="b6326-173">Você pode criar um aplicativo em uma ASE ILB da mesma maneira que você cria um aplicativo em um ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-173">You create an app in an ILB ASE in the same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="b6326-174">No Portal do Azure, escolha **Novo** > **Web + Móvel** > **Web** ou **Móvel** ou **Aplicativo de API**.</span><span class="sxs-lookup"><span data-stu-id="b6326-174">In the Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="b6326-175">Digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6326-175">Enter the name of the app.</span></span>

3. <span data-ttu-id="b6326-176">Selecione a assinatura.</span><span class="sxs-lookup"><span data-stu-id="b6326-176">Select the subscription.</span></span>

4. <span data-ttu-id="b6326-177">Selecione ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b6326-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="b6326-178">Selecione ou crie um plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6326-178">Select or create an App Service plan.</span></span> <span data-ttu-id="b6326-179">Se você quiser criar um novo plano do Serviço de Aplicativo, selecione o seu ASE como o local.</span><span class="sxs-lookup"><span data-stu-id="b6326-179">If you want to create a new App Service plan, select your ASE as the location.</span></span> <span data-ttu-id="b6326-180">Selecione o pool de trabalhos no qual deseja criar o seu plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6326-180">Select the worker pool where you want your App Service plan to be created.</span></span> <span data-ttu-id="b6326-181">Ao criar o plano do Serviço de Aplicativo, selecione o ASE como a localização e o pool de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b6326-181">When you create the App Service plan, select your ASE as the location and the worker pool.</span></span> <span data-ttu-id="b6326-182">Ao especificar o nome do aplicativo, o domínio sob o nome do aplicativo é substituído pelo domínio do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-182">When you specify the name of the app, the domain under your app name is replaced by the domain for your ASE.</span></span>

6. <span data-ttu-id="b6326-183">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b6326-183">Select **Create**.</span></span> <span data-ttu-id="b6326-184">Se você deseja que o aplicativo seja exibido no painel, selecione a caixa de seleção **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="b6326-184">If you want the app to appear on your dashboard, select the **Pin to dashboard** check box.</span></span>

    ![Criação do plano do Serviço de Aplicativo][2]

    <span data-ttu-id="b6326-186">No **Nome do aplicativo**, o nome de domínio é atualizado para refletir o domínio do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-186">Under **App name**, the domain name is updated to reflect the domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="b6326-187">Validação posterior à criação do ASE ILB</span><span class="sxs-lookup"><span data-stu-id="b6326-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="b6326-188">Um ASE com ILB é ligeiramente diferente do ASE que não tem um ILB.</span><span class="sxs-lookup"><span data-stu-id="b6326-188">An ILB ASE is slightly different than the non-ILB ASE.</span></span> <span data-ttu-id="b6326-189">Como já foi observado, você precisa gerenciar o seu próprio DNS.</span><span class="sxs-lookup"><span data-stu-id="b6326-189">As already noted, you need to manage your own DNS.</span></span> <span data-ttu-id="b6326-190">Você também precisa fornecer o seu próprio certificado para conexões HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b6326-190">You also have to provide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="b6326-191">Depois de criar o seu ASE, o nome de domínio mostra o domínio especificado.</span><span class="sxs-lookup"><span data-stu-id="b6326-191">After you create your ASE, the domain name shows the domain you specified.</span></span> <span data-ttu-id="b6326-192">Um novo item chamado **Certificado ILB** aparece no menu **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b6326-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="b6326-193">O ASE é criado com um certificado que não especifica o domínio do ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="b6326-193">The ASE is created with a certificate that doesn't specify the ILB ASE domain.</span></span> <span data-ttu-id="b6326-194">Se você usar o ASE com esse certificado, o navegador informará que ele é inválido.</span><span class="sxs-lookup"><span data-stu-id="b6326-194">If you use the ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="b6326-195">Esse certificado facilita o teste de HTTPS, mas você precisa carregar o seu próprio certificado vinculado ao domínio ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="b6326-195">This certificate makes it easier to test HTTPS, but you need to upload your own certificate that's tied to your ILB ASE domain.</span></span> <span data-ttu-id="b6326-196">Essa etapa é necessária independentemente se o seu certificado é auto-assinado ou adquirido de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="b6326-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![Nome de domínio ASE ILB][3]

<span data-ttu-id="b6326-198">O ASE ILB precisa de um certificado SSL válido.</span><span class="sxs-lookup"><span data-stu-id="b6326-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="b6326-199">Use autoridades de certificação internas, compre um certificado de um emissor externo ou use um certificado auto-assinado.</span><span class="sxs-lookup"><span data-stu-id="b6326-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="b6326-200">Independentemente da origem do certificado SSL, os seguintes atributos de certificado devem ser configurados corretamente:</span><span class="sxs-lookup"><span data-stu-id="b6326-200">Regardless of the source of the SSL certificate, the following certificate attributes need to be configured properly:</span></span>

* <span data-ttu-id="b6326-201">**Entidade**: esse atributo deve ser definido como *.seu-domínio-raiz-aqui.</span><span class="sxs-lookup"><span data-stu-id="b6326-201">**Subject**: This attribute must be set to *.your-root-domain-here.</span></span>
* <span data-ttu-id="b6326-202">**Nome Alternativo da Entidade**: esse atributo deve incluir **.seu-domínio-raiz-aqui* e **.scm.seu-domínio-raiz-aqui*.</span><span class="sxs-lookup"><span data-stu-id="b6326-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="b6326-203">Conexões SSL para o site SCM/Kudu associados a cada aplicativo usam um endereço no formato *nome-do-seu-aplicativo.scm.seu-domínio-raiz-aqui*.</span><span class="sxs-lookup"><span data-stu-id="b6326-203">SSL connections to the SCM/Kudu site associated with each app use an address of the form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="b6326-204">Converta ou salve o certificado SSL como um arquivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="b6326-204">Convert/save the SSL certificate as a .pfx file.</span></span> <span data-ttu-id="b6326-205">O arquivo .pfx deve incluir todos os certificados intermediários e raiz.</span><span class="sxs-lookup"><span data-stu-id="b6326-205">The .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="b6326-206">Proteja-o com uma senha.</span><span class="sxs-lookup"><span data-stu-id="b6326-206">Secure it with a password.</span></span>

<span data-ttu-id="b6326-207">Se você quiser criar um certificado auto-assinado, pode usar os comandos do PowerShell aqui.</span><span class="sxs-lookup"><span data-stu-id="b6326-207">If you want to create a self-signed certificate, you can use the PowerShell commands here.</span></span> <span data-ttu-id="b6326-208">Lembre-se de usar o nome de domínio do ASE ILB em vez de *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="b6326-208">Be sure to use your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="b6326-209">O certificado gerado por comandos do PowerShell é sinalizado por navegadores porque o certificado não foi criado por uma autoridade de certificação que está na cadeia de confiança do seu navegador.</span><span class="sxs-lookup"><span data-stu-id="b6326-209">The certificate that these PowerShell commands generate is flagged by browsers because the certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="b6326-210">Para obter um certificado que o navegador confie, procure uma autoridade de certificação comercial da cadeia de confiança do seu navegador.</span><span class="sxs-lookup"><span data-stu-id="b6326-210">To get a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Defina o certificado ILB][4]

<span data-ttu-id="b6326-212">Para carregar seus próprios certificados e testar o acesso:</span><span class="sxs-lookup"><span data-stu-id="b6326-212">To upload your own certificates and test access:</span></span>

1. <span data-ttu-id="b6326-213">Depois que o ASE for criado, acesse a interface do usuário do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-213">After the ASE is created, go to the ASE UI.</span></span> <span data-ttu-id="b6326-214">Selecione **ASE** > **Configurações** > **Certificado ILB**.</span><span class="sxs-lookup"><span data-stu-id="b6326-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="b6326-215">Para definir o certificado ILB, selecione o arquivo .pfx do certificado e digite a senha.</span><span class="sxs-lookup"><span data-stu-id="b6326-215">To set the ILB certificate, select the certificate .pfx file and enter the password.</span></span> <span data-ttu-id="b6326-216">Esta etapa leva algum tempo para processar.</span><span class="sxs-lookup"><span data-stu-id="b6326-216">This step takes some time to process.</span></span> <span data-ttu-id="b6326-217">Será exibida uma mensagem informando que uma operação de carregamento está em andamento.</span><span class="sxs-lookup"><span data-stu-id="b6326-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="b6326-218">Obtenha o endereço do ILB para seu ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-218">Get the ILB address for your ASE.</span></span> <span data-ttu-id="b6326-219">Selecione **ASE** > **Propriedades** > **Endereço IP Virtual**.</span><span class="sxs-lookup"><span data-stu-id="b6326-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="b6326-220">Depois de criar o ASE, crie um aplicativo Web nele.</span><span class="sxs-lookup"><span data-stu-id="b6326-220">Create a web app in your ASE after the ASE is created.</span></span>

5. <span data-ttu-id="b6326-221">Se não tiver uma VM naquela VNet, crie uma.</span><span class="sxs-lookup"><span data-stu-id="b6326-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6326-222">Não tente criar essa VM na mesma sub-rede que o ASE porque irá falhar ou causar problemas.</span><span class="sxs-lookup"><span data-stu-id="b6326-222">Don't try to create this VM in the same subnet as the ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="b6326-223">Defina o DNS para o domínio do ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-223">Set the DNS for your ASE domain.</span></span> <span data-ttu-id="b6326-224">Você pode usar um caractere curinga com o seu domínio no DNS.</span><span class="sxs-lookup"><span data-stu-id="b6326-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="b6326-225">Para fazer alguns testes simples, edite o arquivo de hosts na sua VM para definir o nome do aplicativo Web para o endereço IP VIP:</span><span class="sxs-lookup"><span data-stu-id="b6326-225">To do some simple tests, edit the hosts file on your VM to set the web app name to the VIP IP address:</span></span>

    <span data-ttu-id="b6326-226">a.</span><span class="sxs-lookup"><span data-stu-id="b6326-226">a.</span></span> <span data-ttu-id="b6326-227">Se o ASE tiver o nome de domínio _.ilbase.com_ e você criar o aplicativo Web chamado _mytestapp_, ele será endereçado em _mytestapp.ilbase.com_. Em seguida, você definirá _mytestapp.ilbase.com_ para resolver o endereço do ILB.</span><span class="sxs-lookup"><span data-stu-id="b6326-227">If your ASE has the domain name _.ilbase.com_ and you create the web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ to resolve to the ILB address.</span></span> <span data-ttu-id="b6326-228">(No Windows, o arquivo dos hosts está em _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="b6326-228">(On Windows, the hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="b6326-229">b.</span><span class="sxs-lookup"><span data-stu-id="b6326-229">b.</span></span> <span data-ttu-id="b6326-230">Para testar a publicação de implantação da Web ou o acesso ao console avançado, crie um registro para _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="b6326-230">To test web deployment publishing or access to the advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="b6326-231">Use um navegador nessa VM e acesse http://mytestapp.ilbase.com. (Ou acesse o nome do aplicativo Web, independente do nome que você escolheu, com o seu domínio.)</span><span class="sxs-lookup"><span data-stu-id="b6326-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go to whatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="b6326-232">Use um navegador nessa VM e acesse https://mytestapp.ilbase.com. Se você usar um certificado auto-assinado, aceite a falta de segurança.</span><span class="sxs-lookup"><span data-stu-id="b6326-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept the lack of security.</span></span>

    <span data-ttu-id="b6326-233">O endereço IP do ILB está listado em **Endereços IP**.</span><span class="sxs-lookup"><span data-stu-id="b6326-233">The IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="b6326-234">Essa lista também contém os endereços IP usados pelo VIP externo e para o tráfego de gerenciamento de entrada.</span><span class="sxs-lookup"><span data-stu-id="b6326-234">This list also has the IP addresses used by the external VIP and for inbound management traffic.</span></span>

    ![Endereço IP do ILB][5]

### <a name="web-jobs-functions-and-the-ilb-ase"></a><span data-ttu-id="b6326-236">Trabalhos da Web, Funções e o ILB ASE</span><span class="sxs-lookup"><span data-stu-id="b6326-236">Web jobs, Functions and the ILB ASE</span></span>

<span data-ttu-id="b6326-237">As Funções e os trabalhos da Web são suportados em um ILB ASE, mas para que o portal funcione com eles, você deve ter acesso de rede ao site SCM.</span><span class="sxs-lookup"><span data-stu-id="b6326-237">Both Functions and web jobs are supported on an ILB ASE but for the portal to work with them, you must have network access to the SCM site.</span></span>  <span data-ttu-id="b6326-238">Isso significa que seu navegador deve estar em um host que esteja na rede virtual ou conectado a ela.</span><span class="sxs-lookup"><span data-stu-id="b6326-238">This means your browser must either be on a host that is either in or connected to the virtual network.</span></span>  

<span data-ttu-id="b6326-239">Quando você usa o Azure Functions em um ASE ILB, você pode receber uma mensagem de erro informando: "Não é possível recuperar as funções no momento.</span><span class="sxs-lookup"><span data-stu-id="b6326-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able to retrieve your functions right now.</span></span> <span data-ttu-id="b6326-240">Tente novamente mais tarde.”</span><span class="sxs-lookup"><span data-stu-id="b6326-240">Please try again later."</span></span> <span data-ttu-id="b6326-241">Esse erro ocorre porque a interface do usuário de Funções aproveita o site SCM por HTTPS e o certificado raiz não está na cadeia de navegadores de confiança.</span><span class="sxs-lookup"><span data-stu-id="b6326-241">This error occurs because the Functions UI leverages the SCM site over HTTPS and the root certificate is not in the browser chain of trust.</span></span> <span data-ttu-id="b6326-242">Os trabalhos da Web têm um problema semelhante.</span><span class="sxs-lookup"><span data-stu-id="b6326-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="b6326-243">Para evitar esse problema, você pode executar uma destas ações:</span><span class="sxs-lookup"><span data-stu-id="b6326-243">To avoid this problem you can do one of the following:</span></span>

- <span data-ttu-id="b6326-244">Adicionar o certificado ao seu repositório de certificados confiáveis.</span><span class="sxs-lookup"><span data-stu-id="b6326-244">Add the certificate to your trusted certificate store.</span></span> <span data-ttu-id="b6326-245">Isso desbloqueia o Edge e o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b6326-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="b6326-246">Use o Chrome e acesse o site SCM primeiro, aceite o certificado não confiável e vá para o portal.</span><span class="sxs-lookup"><span data-stu-id="b6326-246">Use Chrome and go to the SCM site first, accept the untrusted certificate and then go to the portal.</span></span>
- <span data-ttu-id="b6326-247">Use um certificado comercial que esteja na sua cadeia de navegadores confiáveis.</span><span class="sxs-lookup"><span data-stu-id="b6326-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="b6326-248">Essa é a melhor opção.</span><span class="sxs-lookup"><span data-stu-id="b6326-248">This is the best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="b6326-249">Configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="b6326-249">DNS configuration</span></span> ##

<span data-ttu-id="b6326-250">Ao usar um VIP Externo, o DNS é gerenciado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="b6326-250">When you use an External VIP, the DNS is managed by Azure.</span></span> <span data-ttu-id="b6326-251">Qualquer aplicativo criado no ASE é automaticamente adicionado ao DNS do Azure, que é um DNS público.</span><span class="sxs-lookup"><span data-stu-id="b6326-251">Any app created in your ASE is automatically added to Azure DNS, which is a public DNS.</span></span> <span data-ttu-id="b6326-252">Em um ASE ILB, é necessário gerenciar seu próprio DNS.</span><span class="sxs-lookup"><span data-stu-id="b6326-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="b6326-253">Para um domínio específico, como _contoso.net_, você precisa criar registros DNS A no seu DNS que apontam para o endereço do ILB de:</span><span class="sxs-lookup"><span data-stu-id="b6326-253">For a given domain such as _contoso.net_, you need to create DNS A records in your DNS that point to your ILB address for:</span></span>

- <span data-ttu-id="b6326-254">*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="b6326-254">*.contoso.net</span></span>
- <span data-ttu-id="b6326-255">*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="b6326-255">*.scm.contoso.net</span></span>

<span data-ttu-id="b6326-256">Se o domínio do ASE ILB for usado para várias tarefas fora desse ASE, talvez seja necessário gerenciar o DNS baseado no nome de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6326-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need to manage DNS on a per-app-name basis.</span></span> <span data-ttu-id="b6326-257">Esse método é um desafio, pois você precisa adicionar cada nome de aplicativo novo em seu DNS ao criá-lo.</span><span class="sxs-lookup"><span data-stu-id="b6326-257">This method is challenging because you need to add each new app name into your DNS when you create it.</span></span> <span data-ttu-id="b6326-258">Por esse motivo, recomendamos que você use um domínio dedicado.</span><span class="sxs-lookup"><span data-stu-id="b6326-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="b6326-259">Publicação com um ASE ILB</span><span class="sxs-lookup"><span data-stu-id="b6326-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="b6326-260">Para cada aplicativo criado, há dois pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b6326-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="b6326-261">Em um ASE ILB, você tem *&lt;nome do aplicativo>.&lt;Domínio do ASE ILB>* e *&lt;nome do aplicativo>.scm.&lt;Domínio do ASE ILB>*.</span><span class="sxs-lookup"><span data-stu-id="b6326-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="b6326-262">O nome do site SCM leva você para o console do Kudu, que é chamado de **Portal avançado** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6326-262">The SCM site name takes you to the Kudu console, called the **Advanced portal**, within the Azure portal.</span></span> <span data-ttu-id="b6326-263">O console do Kudu lhe permite visualizar as variáveis de ambiente, explorar o disco, usar um console e muito mais.</span><span class="sxs-lookup"><span data-stu-id="b6326-263">The Kudu console lets you view environment variables, explore the disk, use a console, and much more.</span></span> <span data-ttu-id="b6326-264">Para obter mais informações, consulte [Console do Kudu para o Serviço de Aplicativo do Azure][Kudu].</span><span class="sxs-lookup"><span data-stu-id="b6326-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="b6326-265">No Serviço de Aplicativo multilocatário e em um ASE Externo, há logon único entre o portal do Azure e o console do Kudu.</span><span class="sxs-lookup"><span data-stu-id="b6326-265">In the multitenant App Service and in an External ASE, there's single sign-on between the Azure portal and the Kudu console.</span></span> <span data-ttu-id="b6326-266">No entanto, para o ASE ILB, você precisa usar suas credenciais de publicação para entrar no console do Kudu.</span><span class="sxs-lookup"><span data-stu-id="b6326-266">For the ILB ASE, however, you need to use your publishing credentials to sign into the Kudu console.</span></span>

<span data-ttu-id="b6326-267">Sistemas de CI baseados na Internet, como GitHub e o Visual Studio Team Services, não funcionam em ASE ILB porque o ponto de extremidade de publicação não está acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="b6326-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because the publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="b6326-268">Em vez disso, você precisa usar um sistema de CI que usa um modelo pull, como o Dropbox.</span><span class="sxs-lookup"><span data-stu-id="b6326-268">Instead, you need to use a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="b6326-269">Os pontos de extremidade de publicação para aplicativos em um ASE ILB usam o domínio com o qual o ASE ILB foi criado.</span><span class="sxs-lookup"><span data-stu-id="b6326-269">The publishing endpoints for apps in an ILB ASE use the domain that the ILB ASE was created with.</span></span> <span data-ttu-id="b6326-270">Este domínio é exibido no perfil de publicação do aplicativo e na folha do portal do aplicativo (**Visão geral** > **Essentials** e também **Propriedades**).</span><span class="sxs-lookup"><span data-stu-id="b6326-270">This domain appears in the app's publishing profile and in the app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="b6326-271">Se você tiver um ASE ILB com o subdomínio *contoso.net* e um aplicativo chamado *mytest*, use *mytest.contoso.net* para FTP e *mytest.scm.contoso.net* para implantação da Web.</span><span class="sxs-lookup"><span data-stu-id="b6326-271">If you have an ILB ASE with the subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="b6326-272">Como acoplar um ASE ILB com um dispositivo WAF</span><span class="sxs-lookup"><span data-stu-id="b6326-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="b6326-273">O Serviço de Aplicativo do Azure fornece várias medidas de segurança que protegem o sistema.</span><span class="sxs-lookup"><span data-stu-id="b6326-273">Azure App Service provides many security measures that protect the system.</span></span> <span data-ttu-id="b6326-274">Eles também ajudam a determinar se um aplicativo foi atacado por um hacker.</span><span class="sxs-lookup"><span data-stu-id="b6326-274">They also help to determine whether an app was hacked.</span></span> <span data-ttu-id="b6326-275">A melhor proteção para um aplicativo Web é acoplar uma plataforma de hospedagem, como o Serviço de Aplicativo do Azure, com um firewall de aplicativo Web (WAF).</span><span class="sxs-lookup"><span data-stu-id="b6326-275">The best protection for a web application is to couple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="b6326-276">Como o ASE ILB tem um ponto de extremidade do aplicativo isolado da rede, ele é perfeito para esse uso.</span><span class="sxs-lookup"><span data-stu-id="b6326-276">Because the ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="b6326-277">Para saber mais sobre como configurar o ASE ILB com um dispositivo WAF, confira [Configuração de um firewall do aplicativo Web com o ambiente do serviço de aplicativo][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="b6326-277">To learn more about how to configure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="b6326-278">Este artigo mostra como usar uma solução de virtualização Barracuda com o seu ASE.</span><span class="sxs-lookup"><span data-stu-id="b6326-278">This article shows how to use a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="b6326-279">Outra opção é usar o gateway de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6326-279">Another option is to use Azure Application Gateway.</span></span> <span data-ttu-id="b6326-280">O gateway de aplicativo usa as regras básicas do OWASP para proteger os aplicativos colocados atrás dele.</span><span class="sxs-lookup"><span data-stu-id="b6326-280">Application Gateway uses the OWASP core rules to secure any applications placed behind it.</span></span> <span data-ttu-id="b6326-281">Para obter mais informações sobre o gateway de aplicativo do Azure, confira [Introdução ao firewall de aplicativo Web do Azure][AppGW].</span><span class="sxs-lookup"><span data-stu-id="b6326-281">For more information about Application Gateway, see [Introduction to the Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="b6326-282">Introdução</span><span class="sxs-lookup"><span data-stu-id="b6326-282">Get started</span></span> ##

<span data-ttu-id="b6326-283">Todos os artigos e instruções para ASEs estão disponíveis no [LEIAME para ambientes do Serviço de Aplicativo][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="b6326-283">All articles and how-to instructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="b6326-284">Para começar a usar ASEs, confira [Introdução aos ambientes do Serviço de Aplicativo][Intro].</span><span class="sxs-lookup"><span data-stu-id="b6326-284">To get started with ASEs, see [Introduction to App Service environments][Intro].</span></span>
* <span data-ttu-id="b6326-285">Para obter mais informações sobre a plataforma de Serviço de Aplicativo do Azure, consulte [Serviço de Aplicativo do Azure](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="b6326-285">For more information about the Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
