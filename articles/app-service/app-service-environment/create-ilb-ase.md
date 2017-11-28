---
title: "aaaCreate e usar um balanceador de carga interno com um ambiente de serviço de aplicativo do Azure"
description: "Obter detalhes sobre como toocreate e usar um ambiente de serviço de aplicativo do Azure isolado da internet"
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
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="55547-103">Como criar e usar um balanceador de carga interno com um ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="55547-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="55547-104">O Ambiente do Serviço de Aplicativo do Azure é uma implantação do Serviço de Aplicativo do Azure em uma sub-rede de uma VNet (rede virtual) do Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="55547-105">Há dois toodeploy de maneiras de um ambiente de serviço de aplicativo (ASE):</span><span class="sxs-lookup"><span data-stu-id="55547-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="55547-106">Com um VIP em um endereço IP externo, geralmente chamado de ASE externo.</span><span class="sxs-lookup"><span data-stu-id="55547-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="55547-107">Com um VIP em um endereço IP interno, geralmente chamado uma ASE ILB, porque o ponto de extremidade interno Olá é um balanceador de carga interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="55547-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="55547-108">Este artigo mostra como toocreate uma ASE ILB.</span><span class="sxs-lookup"><span data-stu-id="55547-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="55547-109">Para obter uma visão geral sobre Olá ASE, consulte [ambientes de serviço Introdução tooApp][Intro].</span><span class="sxs-lookup"><span data-stu-id="55547-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="55547-110">toolearn como toocreate uma ASE externas, consulte [criar uma ASE externo][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="55547-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="55547-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="55547-111">Overview</span></span> ##

<span data-ttu-id="55547-112">Um ASE pode ser implantado com um ponto de extremidade acessível pela Internet ou com um endereço IP em sua VNet.</span><span class="sxs-lookup"><span data-stu-id="55547-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="55547-113">tooset tooa endereço de rede virtual, Olá ASE deve ser implantado com um ILB de endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="55547-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="55547-114">Para implantar o ASE com um ILB, você deve fornecer:</span><span class="sxs-lookup"><span data-stu-id="55547-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="55547-115">Seu próprio domínio, que você usa quando cria seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="55547-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="55547-116">certificado de saudação usado para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="55547-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="55547-117">Gerenciamento de DNS para o seu domínio.</span><span class="sxs-lookup"><span data-stu-id="55547-117">DNS management for your domain.</span></span>

<span data-ttu-id="55547-118">Em troca, você pode fazer coisas como:</span><span class="sxs-lookup"><span data-stu-id="55547-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="55547-119">Aplicativos de intranet do host com segurança na nuvem hello, o que você pode acessar por meio de um site a site ou VPN de rota expressa do Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="55547-120">Aplicativos de host na nuvem Olá que não estiverem em servidores DNS públicos.</span><span class="sxs-lookup"><span data-stu-id="55547-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="55547-121">Criar aplicativos back-end isolados da Internet, que podem ser integrados com seus aplicativos front-end com segurança.</span><span class="sxs-lookup"><span data-stu-id="55547-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="55547-122">Funcionalidade desabilitada</span><span class="sxs-lookup"><span data-stu-id="55547-122">Disabled functionality</span></span> ###

<span data-ttu-id="55547-123">Há algumas coisas que você não pode fazer ao usar um ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="55547-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="55547-124">Usar SSL baseado em IP.</span><span class="sxs-lookup"><span data-stu-id="55547-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="55547-125">Atribua endereços IP toospecific aplicativos.</span><span class="sxs-lookup"><span data-stu-id="55547-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="55547-126">Comprar e usar um certificado com um aplicativo por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="55547-127">Você pode obter certificados diretamente de uma autoridade de certificação e usá-los com seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="55547-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="55547-128">Não é possível obtê-las por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="55547-129">Criar um ASE ILB</span><span class="sxs-lookup"><span data-stu-id="55547-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="55547-130">toocreate uma ASE ILB:</span><span class="sxs-lookup"><span data-stu-id="55547-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="55547-131">No portal do Azure de Olá, selecione **novo** > **Web + móvel** > **ambiente de serviço de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="55547-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="55547-132">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="55547-132">Select your subscription.</span></span>

3. <span data-ttu-id="55547-133">Selecione ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="55547-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="55547-134">Selecione ou crie uma VNet.</span><span class="sxs-lookup"><span data-stu-id="55547-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="55547-135">Se você selecionar uma rede virtual existente, será necessário toocreate uma saudação de toohold sub-rede ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="55547-136">Certifique-se de tooset uma sub-rede tamanho grande o suficiente tooaccommodate qualquer crescimento futuro de sua ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="55547-137">O tamanho recomendado é `/25`, que tem 128 endereços e é compatível com um ASE com tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="55547-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="55547-138">Olá você pode selecionar o tamanho mínimo é um `/28`.</span><span class="sxs-lookup"><span data-stu-id="55547-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="55547-139">Depois que precisa de infraestrutura, esse tamanho pode ser dimensionado tooa máximo 11 instâncias.</span><span class="sxs-lookup"><span data-stu-id="55547-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="55547-140">Ir além da saudação padrão de no máximo de 100 instâncias nos planos de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55547-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="55547-141">Dimensione cerca de 100, mas com dimensionamento de front-end mais rápido.</span><span class="sxs-lookup"><span data-stu-id="55547-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="55547-142">Selecione **Rede Virtual/Local** > **Configuração de Rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="55547-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="55547-143">Saudação de conjunto **VIP tipo** muito**interno**.</span><span class="sxs-lookup"><span data-stu-id="55547-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="55547-144">Digite um nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="55547-144">Enter a domain name.</span></span> <span data-ttu-id="55547-145">Este domínio é hello usado para aplicativos criados neste ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="55547-146">Há algumas restrições.</span><span class="sxs-lookup"><span data-stu-id="55547-146">There are some restrictions.</span></span> <span data-ttu-id="55547-147">Ele não pode ser:</span><span class="sxs-lookup"><span data-stu-id="55547-147">It can't be:</span></span>

    * <span data-ttu-id="55547-148">net</span><span class="sxs-lookup"><span data-stu-id="55547-148">net</span></span>   

    * <span data-ttu-id="55547-149">azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="55547-149">azurewebsites.net</span></span>

    * <span data-ttu-id="55547-150">p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="55547-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="55547-151">&lt;asename&gt;.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="55547-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="55547-152">o nome de domínio personalizado Olá usado para aplicativos e nome de domínio Olá usado pelo seu ASE não pode se sobrepor.</span><span class="sxs-lookup"><span data-stu-id="55547-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="55547-153">Para uma ASE ILB com o nome de domínio Olá _contoso.com_, você não pode usar nomes de domínio personalizado para seus aplicativos, como:</span><span class="sxs-lookup"><span data-stu-id="55547-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="55547-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="55547-154">www.contoso.com</span></span>

    * <span data-ttu-id="55547-155">abcd.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="55547-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="55547-156">abcd.contoso.com</span><span class="sxs-lookup"><span data-stu-id="55547-156">abcd.contoso.com</span></span>

   <span data-ttu-id="55547-157">Se você souber os nomes de domínio personalizados Olá para seus aplicativos, escolha um domínio para Olá ASE ILB que não tem um conflito com esses nomes de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="55547-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="55547-158">Neste exemplo, você pode usar algo como *contoso internal.com* para domínio de saudação do seu ASE porque que não entra em conflito com nomes de domínio personalizado que terminam em *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="55547-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="55547-159">Selecione **OK** e, então, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="55547-159">Select **OK**, and then select **Create**.</span></span>

    ![Criação de ASE][1]

<span data-ttu-id="55547-161">Em Olá **rede Virtual** folha, há um **configuração de rede Virtual** opção.</span><span class="sxs-lookup"><span data-stu-id="55547-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="55547-162">Você pode usá-lo tooselect um VIP externo ou um VIP interno.</span><span class="sxs-lookup"><span data-stu-id="55547-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="55547-163">saudação padrão é **externo**.</span><span class="sxs-lookup"><span data-stu-id="55547-163">hello default is **External**.</span></span> <span data-ttu-id="55547-164">Se você selecionar **Externo**, o seu ASE usará um VIP acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="55547-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="55547-165">Se você selecionar **Interno**, o seu ASE será configurado com um ILB em um endereço IP na sua VNet.</span><span class="sxs-lookup"><span data-stu-id="55547-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="55547-166">Depois de selecionar **interno**, Olá capacidade tooadd mais endereços IP tooyour ASE é removido.</span><span class="sxs-lookup"><span data-stu-id="55547-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="55547-167">Em vez disso, você precisa tooprovide domínio Olá Olá ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="55547-168">Em uma ASE com um VIP externo, o nome de saudação do hello que ASE é usado no domínio Olá para aplicativos criados no que ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="55547-169">Se você definir **VIP tipo** muito**interno**, seu nome ASE não é usado no domínio Olá para Olá ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="55547-170">Você pode especificar domínio Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="55547-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="55547-171">Se o domínio for *contoso.corp.net* e criar um aplicativo que ASE denominado *timereporting*, Olá URL para que o aplicativo é timereporting.contoso.corp.net.</span><span class="sxs-lookup"><span data-stu-id="55547-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="55547-172">Como criar um aplicativo em uma ASE ILB</span><span class="sxs-lookup"><span data-stu-id="55547-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="55547-173">Criar um aplicativo em uma ASE ILB em Olá mesma maneira que você cria um aplicativo em uma ASE normalmente.</span><span class="sxs-lookup"><span data-stu-id="55547-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="55547-174">No portal do Azure de Olá, selecione **novo** > **Web + móvel** > **Web** ou **Mobile** ou  **Aplicativo de API**.</span><span class="sxs-lookup"><span data-stu-id="55547-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="55547-175">Insira o nome de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="55547-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="55547-176">Selecione a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="55547-176">Select hello subscription.</span></span>

4. <span data-ttu-id="55547-177">Selecione ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="55547-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="55547-178">Selecione ou crie um plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55547-178">Select or create an App Service plan.</span></span> <span data-ttu-id="55547-179">Se você quiser toocreate um novo plano de serviço de aplicativo, selecione seu ASE como local de saudação.</span><span class="sxs-lookup"><span data-stu-id="55547-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="55547-180">Selecione o pool do trabalhador Olá onde você deseja que seu toobe de plano de serviço de aplicativo criado.</span><span class="sxs-lookup"><span data-stu-id="55547-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="55547-181">Quando você cria Olá plano de serviço de aplicativo, selecione seu ASE como Olá local e o pool do trabalhador hello.</span><span class="sxs-lookup"><span data-stu-id="55547-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="55547-182">Quando você especifica o nome de saudação do aplicativo hello, domínio Olá em nome do aplicativo é substituído por domínio Olá para seu ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="55547-183">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="55547-183">Select **Create**.</span></span> <span data-ttu-id="55547-184">Se você desejar Olá tooappear de aplicativo em seu painel, selecione o **toodashboard Pin** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="55547-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![Criação do plano do Serviço de Aplicativo][2]

    <span data-ttu-id="55547-186">Em **nome do aplicativo**, nome de domínio de saudação é domínio de saudação tooreflect atualizada de seu ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="55547-187">Validação posterior à criação do ASE ILB</span><span class="sxs-lookup"><span data-stu-id="55547-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="55547-188">Uma ASE ILB é ligeiramente diferente de saudação não - ILB ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="55547-189">Como já observado, você precisa toomanage seu próprio DNS.</span><span class="sxs-lookup"><span data-stu-id="55547-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="55547-190">Você também tem tooprovide seu próprio certificado para conexões HTTPS.</span><span class="sxs-lookup"><span data-stu-id="55547-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="55547-191">Depois de criar seu ASE, nome de domínio Olá mostra domínio Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="55547-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="55547-192">Um novo item chamado **Certificado ILB** aparece no menu **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="55547-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="55547-193">Olá ASE é criada com um certificado que não especifica o domínio do ILB ASE hello.</span><span class="sxs-lookup"><span data-stu-id="55547-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="55547-194">Se você usar o hello ASE com esse certificado, seu navegador informa que é inválido.</span><span class="sxs-lookup"><span data-stu-id="55547-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="55547-195">Esse certificado torna mais fácil tootest HTTPS, mas você precisa tooupload seu próprio certificado associado tooyour ILB ASE domínio.</span><span class="sxs-lookup"><span data-stu-id="55547-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="55547-196">Essa etapa é necessária independentemente se o seu certificado é auto-assinado ou adquirido de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="55547-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![Nome de domínio ASE ILB][3]

<span data-ttu-id="55547-198">O ASE ILB precisa de um certificado SSL válido.</span><span class="sxs-lookup"><span data-stu-id="55547-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="55547-199">Use autoridades de certificação internas, compre um certificado de um emissor externo ou use um certificado auto-assinado.</span><span class="sxs-lookup"><span data-stu-id="55547-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="55547-200">Independentemente de fonte de saudação do certificado SSL hello, hello seguintes atributos de certificado necessário toobe configurado corretamente:</span><span class="sxs-lookup"><span data-stu-id="55547-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="55547-201">**Entidade**: este atributo deve ser definido como too*.your-raiz domínio aqui.</span><span class="sxs-lookup"><span data-stu-id="55547-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="55547-202">**Nome Alternativo da Entidade**: esse atributo deve incluir **.seu-domínio-raiz-aqui* e **.scm.seu-domínio-raiz-aqui*.</span><span class="sxs-lookup"><span data-stu-id="55547-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="55547-203">SSL conexões toohello site SCM/Kudu associado a cada aplicativo usar um endereço de formulário Olá *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="55547-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="55547-204">Certificado SSL da saudação de Convert/Salvar como um arquivo. pfx.</span><span class="sxs-lookup"><span data-stu-id="55547-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="55547-205">arquivo. pfx de saudação deve incluir todos os intermediário e raiz certificados.</span><span class="sxs-lookup"><span data-stu-id="55547-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="55547-206">Proteja-o com uma senha.</span><span class="sxs-lookup"><span data-stu-id="55547-206">Secure it with a password.</span></span>

<span data-ttu-id="55547-207">Se você quiser toocreate um certificado autoassinado, você pode usar comandos do PowerShell Olá aqui.</span><span class="sxs-lookup"><span data-stu-id="55547-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="55547-208">Ser toouse-se de que seu nome de domínio em vez de ASE ILB *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="55547-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="55547-209">certificado Olá que geram desses comandos do PowerShell é sinalizado por navegadores porque Olá certificado não foi criado por uma autoridade de certificação que está na cadeia de confiança de seu navegador.</span><span class="sxs-lookup"><span data-stu-id="55547-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="55547-210">tooget um certificado de confiança do seu navegador, primeiramente ele de uma autoridade de certificação comercial na cadeia de confiança de seu navegador.</span><span class="sxs-lookup"><span data-stu-id="55547-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![Defina o certificado ILB][4]

<span data-ttu-id="55547-212">tooupload seus próprios certificados e o acesso de teste:</span><span class="sxs-lookup"><span data-stu-id="55547-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="55547-213">Depois de saudação ASE é criado, vá toohello ASE da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="55547-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="55547-214">Selecione **ASE** > **Configurações** > **Certificado ILB**.</span><span class="sxs-lookup"><span data-stu-id="55547-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="55547-215">tooset certificado ILB hello, selecione Olá certificado. pfx arquivo e insira a senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="55547-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="55547-216">Esta etapa leva alguns tooprocess de tempo.</span><span class="sxs-lookup"><span data-stu-id="55547-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="55547-217">Será exibida uma mensagem informando que uma operação de carregamento está em andamento.</span><span class="sxs-lookup"><span data-stu-id="55547-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="55547-218">Obter o endereço ILB de saudação para seu ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="55547-219">Selecione **ASE** > **Propriedades** > **Endereço IP Virtual**.</span><span class="sxs-lookup"><span data-stu-id="55547-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="55547-220">Crie um aplicativo web no seu ASE depois Olá ASE é criado.</span><span class="sxs-lookup"><span data-stu-id="55547-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="55547-221">Se não tiver uma VM naquela VNet, crie uma.</span><span class="sxs-lookup"><span data-stu-id="55547-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55547-222">Não tente toocreate essa VM em Olá mesma sub-rede como Olá ASE porque irá falhar ou causar problemas.</span><span class="sxs-lookup"><span data-stu-id="55547-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="55547-223">Saudação de conjunto de DNS para seu domínio ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="55547-224">Você pode usar um caractere curinga com o seu domínio no DNS.</span><span class="sxs-lookup"><span data-stu-id="55547-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="55547-225">toodo alguns simples testa, edite o arquivo de hosts de saudação em sua VM tooset Olá web aplicativo nome toohello endereço IP VIP:</span><span class="sxs-lookup"><span data-stu-id="55547-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="55547-226">a.</span><span class="sxs-lookup"><span data-stu-id="55547-226">a.</span></span> <span data-ttu-id="55547-227">Se seu ASE tem o nome de domínio de saudação _. ilbase.com_ e criar o aplicativo web de saudação chamado _mytestapp_, é abordada em _mytestapp.ilbase.com_. Você então definir _mytestapp.ilbase.com_ endereço do tooresolve toohello ILB.</span><span class="sxs-lookup"><span data-stu-id="55547-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="55547-228">(No Windows, o arquivo de hosts do hello está em _C:\Windows\System32\drivers\etc\_.)</span><span class="sxs-lookup"><span data-stu-id="55547-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="55547-229">b.</span><span class="sxs-lookup"><span data-stu-id="55547-229">b.</span></span> <span data-ttu-id="55547-230">tootest web implantação publicação ou acesso toohello avançado do console, crie um registro para _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="55547-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="55547-231">Use um navegador nessa VM e acesse http://mytestapp.ilbase.com. (Ou vá toowhatever que é o nome do aplicativo web com o seu domínio).</span><span class="sxs-lookup"><span data-stu-id="55547-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="55547-232">Use um navegador nessa VM e acesse https://mytestapp.ilbase.com. Se você usar um certificado autoassinado, aceite a falta de saudação de segurança.</span><span class="sxs-lookup"><span data-stu-id="55547-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="55547-233">endereço IP Olá para o ILB está listado em **endereços IP**.</span><span class="sxs-lookup"><span data-stu-id="55547-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="55547-234">Essa lista também tem endereços IP de saudação usados pelo VIP externo hello e tráfego de entrada de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="55547-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![Endereço IP do ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="55547-236">Web trabalhos, funções e Olá ASE ILB</span><span class="sxs-lookup"><span data-stu-id="55547-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="55547-237">Funções e trabalhos da web têm suporte em uma ASE ILB, mas para Olá toowork portal com eles, você deve ter o site SCM do toohello de acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="55547-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="55547-238">Isso significa que seu navegador deve ser em um host que está em ou rede virtual toohello conectada.</span><span class="sxs-lookup"><span data-stu-id="55547-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="55547-239">Quando você usa funções do Azure em uma ASE ILB, você pode receber uma mensagem de erro que diz "não é capaz de tooretrieve suas funções no momento.</span><span class="sxs-lookup"><span data-stu-id="55547-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="55547-240">Tente novamente mais tarde.”</span><span class="sxs-lookup"><span data-stu-id="55547-240">Please try again later."</span></span> <span data-ttu-id="55547-241">Esse erro ocorre porque Olá funções da interface do usuário utiliza o site SCM Olá via HTTPS e certificado de raiz de saudação não está na cadeia de navegador de saudação de confiança.</span><span class="sxs-lookup"><span data-stu-id="55547-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="55547-242">Os trabalhos da Web têm um problema semelhante.</span><span class="sxs-lookup"><span data-stu-id="55547-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="55547-243">tooavoid esse problema, você pode fazer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="55547-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="55547-244">Adicione repositório de certificados confiáveis de tooyour Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="55547-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="55547-245">Isso desbloqueia o Edge e o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="55547-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="55547-246">Usar o Chrome e acesse o site SCM do toohello primeiro, aceitar o certificado não confiável hello e vá toohello portal.</span><span class="sxs-lookup"><span data-stu-id="55547-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="55547-247">Use um certificado comercial que esteja na sua cadeia de navegadores confiáveis.</span><span class="sxs-lookup"><span data-stu-id="55547-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="55547-248">Isso é Olá melhor opção.</span><span class="sxs-lookup"><span data-stu-id="55547-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="55547-249">Configuração de DNS</span><span class="sxs-lookup"><span data-stu-id="55547-249">DNS configuration</span></span> ##

<span data-ttu-id="55547-250">Quando você usar um VIP externo, Olá DNS é gerenciado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="55547-251">Qualquer aplicativo que criou no seu ASE é adicionado automaticamente tooAzure DNS, que é um DNS público.</span><span class="sxs-lookup"><span data-stu-id="55547-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="55547-252">Em um ASE ILB, é necessário gerenciar seu próprio DNS.</span><span class="sxs-lookup"><span data-stu-id="55547-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="55547-253">Para um determinado domínio como _contoso.net_, você precisa toocreate DNS A registros no DNS, endereço ponto tooyour ILB para:</span><span class="sxs-lookup"><span data-stu-id="55547-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="55547-254">*.contoso.net</span><span class="sxs-lookup"><span data-stu-id="55547-254">*.contoso.net</span></span>
- <span data-ttu-id="55547-255">*.scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="55547-255">*.scm.contoso.net</span></span>

<span data-ttu-id="55547-256">Se seu domínio ILB ASE é usado para várias coisas fora este ASE, talvez seja necessário toomanage DNS em cada nome por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55547-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="55547-257">Esse método é um desafio, pois você precisará tooadd cada novo nome de aplicativo em seu DNS ao criá-lo.</span><span class="sxs-lookup"><span data-stu-id="55547-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="55547-258">Por esse motivo, recomendamos que você use um domínio dedicado.</span><span class="sxs-lookup"><span data-stu-id="55547-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="55547-259">Publicação com um ASE ILB</span><span class="sxs-lookup"><span data-stu-id="55547-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="55547-260">Para cada aplicativo criado, há dois pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="55547-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="55547-261">Em um ASE ILB, você tem *&lt;nome do aplicativo>.&lt;Domínio do ASE ILB>* e *&lt;nome do aplicativo>.scm.&lt;Domínio do ASE ILB>*.</span><span class="sxs-lookup"><span data-stu-id="55547-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="55547-262">nome do site SCM Olá leva console de Kudu toohello, chamado hello **portal avançado**no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="55547-263">console de Kudu Olá lhe permite exibir as variáveis de ambiente, explorar Olá disco, use um console e muito mais.</span><span class="sxs-lookup"><span data-stu-id="55547-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="55547-264">Para obter mais informações, consulte [Console do Kudu para o Serviço de Aplicativo do Azure][Kudu].</span><span class="sxs-lookup"><span data-stu-id="55547-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="55547-265">Multilocatário de saudação do serviço de aplicativo e em uma ASE externos, não há logon único entre Olá portal do Azure e o console de Kudu hello.</span><span class="sxs-lookup"><span data-stu-id="55547-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="55547-266">Para Olá ASE ILB, no entanto, você precisa toouse seu toosign credenciais publicação no console do Kudu hello.</span><span class="sxs-lookup"><span data-stu-id="55547-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="55547-267">Sistemas de CI baseado na Internet, como GitHub e o Visual Studio Team Services, não funcionam com uma ASE ILB porque o ponto de extremidade de publicação do hello não está acessível pela internet.</span><span class="sxs-lookup"><span data-stu-id="55547-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="55547-268">Em vez disso, você precisa toouse um sistema de CI que usa um modelo de pull, como o Dropbox.</span><span class="sxs-lookup"><span data-stu-id="55547-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="55547-269">pontos de extremidade de publicação de saudação para aplicativos em uma ASE ILB usam domínio Olá que Olá com que ASE ILB foi criado.</span><span class="sxs-lookup"><span data-stu-id="55547-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="55547-270">Este domínio é exibido no perfil de publicação do aplicativo hello e na folha de portal do aplicativo hello (**visão geral** > **Essentials** e também **propriedades**).</span><span class="sxs-lookup"><span data-stu-id="55547-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="55547-271">Se você tiver uma ASE ILB com subdomínio Olá *contoso.net* e um aplicativo chamado *mytest*, use *mytest.contoso.net* para FTP e *mytest.scm.contoso.net*  para implantação da web.</span><span class="sxs-lookup"><span data-stu-id="55547-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="55547-272">Como acoplar um ASE ILB com um dispositivo WAF</span><span class="sxs-lookup"><span data-stu-id="55547-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="55547-273">Serviço de aplicativo do Azure fornece várias medidas de segurança que protegem o sistema hello.</span><span class="sxs-lookup"><span data-stu-id="55547-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="55547-274">Eles também ajudam a toodetermine se um aplicativo foi violado.</span><span class="sxs-lookup"><span data-stu-id="55547-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="55547-275">Olá melhor proteção para um aplicativo web é toocouple uma plataforma de hospedagem, como o serviço de aplicativo do Azure, com um firewall do aplicativo web (WAF).</span><span class="sxs-lookup"><span data-stu-id="55547-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="55547-276">Como Olá ASE ILB tem um ponto de extremidade do aplicativo de isolamento de rede, é apropriado para um uso.</span><span class="sxs-lookup"><span data-stu-id="55547-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="55547-277">toolearn mais sobre como tooconfigure ASE o ILB com um dispositivo WAF, consulte [configurar um firewall do aplicativo web com seu ambiente de serviço de aplicativo][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="55547-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="55547-278">Este artigo mostra como toouse um dispositivo virtual Barracuda com seu ASE.</span><span class="sxs-lookup"><span data-stu-id="55547-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="55547-279">Outra opção é toouse Gateway de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="55547-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="55547-280">Application Gateway usa Olá OWASP core regras toosecure todos os aplicativos são colocados por trás dele.</span><span class="sxs-lookup"><span data-stu-id="55547-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="55547-281">Para obter mais informações sobre o Application Gateway, consulte [firewall do aplicativo de web do Azure Introdução toohello][AppGW].</span><span class="sxs-lookup"><span data-stu-id="55547-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="55547-282">Introdução</span><span class="sxs-lookup"><span data-stu-id="55547-282">Get started</span></span> ##

<span data-ttu-id="55547-283">Todos os artigos e como-tooinstructions para ASs estão disponíveis no [Leiame para ambientes de serviço de aplicativo][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="55547-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="55547-284">tooget iniciado com ASs, consulte [ambientes de serviço Introdução tooApp][Intro].</span><span class="sxs-lookup"><span data-stu-id="55547-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="55547-285">Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="55547-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
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
