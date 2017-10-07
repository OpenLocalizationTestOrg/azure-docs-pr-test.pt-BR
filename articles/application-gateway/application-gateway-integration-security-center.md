---
title: "aaaApplication integração do Gateway com a Central de segurança do Azure | Microsoft Docs"
description: "Esta página fornece informações sobre como o Gateway de Aplicativo se integra à Central de segurança do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="bc224-103">Visão geral da integração entre o Gateway de Aplicativo e a Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bc224-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="bc224-104">Saiba como o Gateway de Aplicativo e a Central de segurança ajudam a proteger os recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bc224-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="bc224-105">Firewall do aplicativo web do Application gateway (WAF) integra-se com [Central de segurança](../security-center/security-center-intro.md) tooprovide tooprevent uma visualização perfeita, detectar e responder a aplicativos de web toounprotected toothreats em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bc224-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="bc224-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bc224-106">Overview</span></span>

<span data-ttu-id="bc224-107">O WAF do Gateway de Aplicativo é uma recomendação na Central de segurança para proteger aplicativos Web contra explorações e vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="bc224-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="bc224-108">Recursos da Web habilitado que não estão protegidos por WAF mostram no Centro de segurança de hello como recomendações de severidade alta.</span><span class="sxs-lookup"><span data-stu-id="bc224-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="bc224-109">Recomendações para firewalls de aplicativo da web são mostradas em Olá **visão geral** página em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bc224-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![integração com a central de segurança][1]

<span data-ttu-id="bc224-111">Clicando em todas as recomendações sobre o firewall do aplicativo da web abre uma nova folha que mostra os detalhes de saudação do recomendação hello.</span><span class="sxs-lookup"><span data-stu-id="bc224-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="bc224-112">Adicionar um recurso existente do web aplicativo firewall tooan</span><span class="sxs-lookup"><span data-stu-id="bc224-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="bc224-113">Navegue muito**mais serviços** > **segurança + identidade** > **Central de segurança** e Olá **Central de segurança - visão geral**  folha, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bc224-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="bc224-114">Em Olá **Central de segurança - aplicativos** folha, a tabela de saudação contém uma lista de aplicativos que a Central de segurança detectada na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bc224-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![aplicativos Web][3]

<span data-ttu-id="bc224-116">Ao clicar em um aplicativo web com um problema crítico, você obtém Olá **integridade da segurança do aplicativo** folha.</span><span class="sxs-lookup"><span data-stu-id="bc224-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="bc224-117">Na imagem de saudação abaixo, Olá aplicativo web que não está protegido por um firewall do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="bc224-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![recursos Web não protegidos][2]

<span data-ttu-id="bc224-119">Clique em **adicionar um firewall do aplicativo web** em **recomendações** tooopen Olá **adicionar um Firewall do aplicativo Web** folha.</span><span class="sxs-lookup"><span data-stu-id="bc224-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="bc224-120">Se você não tiver um Gateway existente do aplicativo, ou toocreate um novo, clique em **criar novo** e Olá **criar um novo Firewall do aplicativo Web** folha e clique em **Microsoft - Application Gateway**.</span><span class="sxs-lookup"><span data-stu-id="bc224-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="bc224-121">Isso leva você através de saudação etapas toocreate um application gateway.</span><span class="sxs-lookup"><span data-stu-id="bc224-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="bc224-122">Neste ponto, seu aplicativo Web é adicionado como um recurso protegido, agora a Central de segurança controla o que esse recurso está protegido por um firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="bc224-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="bc224-123">Isso não o adiciona como um membro do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="bc224-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="bc224-124">Se você tiver um gateway de aplicativo existente, é possível escolhê-lo em **Usar solução existente**</span><span class="sxs-lookup"><span data-stu-id="bc224-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![folha adicionar firewall do aplicativo Web][4]

<span data-ttu-id="bc224-126">Adicionar que um gateway do aplicativo web aplicativo tooan por meio da Central de segurança não adiciona recursos hello como um membro do pool de back-end, isso deve ser feito no recurso de gateway do aplicativo hello diretamente.</span><span class="sxs-lookup"><span data-stu-id="bc224-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="bc224-127">Adicionar um recurso tooan web aplicativo de firewall existente</span><span class="sxs-lookup"><span data-stu-id="bc224-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="bc224-128">Navegue muito**mais serviços** > **segurança + identidade** > **Central de segurança** e Olá **Central de segurança - visão geral**  folha, clique em **soluções de parceiros**.</span><span class="sxs-lookup"><span data-stu-id="bc224-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="bc224-129">Mostram gateways de aplicativo com reconhecimento de Central de segurança existentes no hello **soluções de parceiros** folha.</span><span class="sxs-lookup"><span data-stu-id="bc224-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![soluções de parceiros][7]

<span data-ttu-id="bc224-131">Clique em **aplicativo Link** tooopen Olá **aplicativos de Link** folha, aqui você terá aplicativos existentes do tooselect Olá opções.</span><span class="sxs-lookup"><span data-stu-id="bc224-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="bc224-132">Escolha Olá tooprotect de aplicativos e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="bc224-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="bc224-133">Isso não adicionar pool de back-end de toohello de aplicativos da web do hello do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bc224-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="bc224-134">Isso define recursos hello como um recurso protegido para a Central de segurança possa controlá-la.</span><span class="sxs-lookup"><span data-stu-id="bc224-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="bc224-135">recurso de saudação tooadd como um membro do pool de back-end, isso deve ser feito no gateway do aplicativo hello, folha atual Olá você pode clicar em **console de solução** toobe tomada toohello recursos de gateway de aplicativo onde você pode adicionar Olá web pool de back-end do aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="bc224-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![aplicativos de soluções de parceiros][6]

## <a name="finalize-configuration"></a><span data-ttu-id="bc224-137">Finalizar a configuração</span><span class="sxs-lookup"><span data-stu-id="bc224-137">Finalize configuration</span></span>

<span data-ttu-id="bc224-138">Central de segurança monitora aplicativos adicionados tooan gateway de aplicativo como um recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="bc224-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="bc224-139">Ele monitora a integridade de saudação deste recurso e garante que ele é protegido por um application gateway.</span><span class="sxs-lookup"><span data-stu-id="bc224-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="bc224-140">Olá próxima etapa é IP privado de saudação tooadd, IP público ou NIC de seu pool de back-end do toohello de máquina virtual do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="bc224-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="bc224-141">Até que isso é feito uma recomendação adicional de **finalizar a proteção do aplicativo** é exibido até que o recurso de saudação é adicionado.</span><span class="sxs-lookup"><span data-stu-id="bc224-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![folha adicionar firewall do aplicativo Web][5]

## <a name="security-alerts"></a><span data-ttu-id="bc224-143">Alertas de segurança</span><span class="sxs-lookup"><span data-stu-id="bc224-143">Security Alerts</span></span>

<span data-ttu-id="bc224-144">Em Central de segurança navegue muito**detecção** > **alertas de segurança**.</span><span class="sxs-lookup"><span data-stu-id="bc224-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="bc224-145">Aqui você encontra alertas do WAF para seus gateways de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bc224-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="bc224-146">Os alertas são divididos pela regra do WAF.</span><span class="sxs-lookup"><span data-stu-id="bc224-146">Alerts are broken down by WAF rule.</span></span>

![alertas de segurança][8]

<span data-ttu-id="bc224-148">Clicar em uma regra fornecerá uma lista de alertas para essa regra específica do WAF.</span><span class="sxs-lookup"><span data-stu-id="bc224-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="bc224-149">Cada alerta mostra detalhes adicionais sobre como localizar hello.</span><span class="sxs-lookup"><span data-stu-id="bc224-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="bc224-150">detalhes de saudação oferecem um gateway de aplicativo de toohello do link.</span><span class="sxs-lookup"><span data-stu-id="bc224-150">hello details provide a link toohello application gateway.</span></span>
 
![detalhes do alerta][9]

## <a name="next-steps"></a><span data-ttu-id="bc224-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc224-152">Next steps</span></span>

<span data-ttu-id="bc224-153">toolearn como o firewall do aplicativo web tooenable em um gateway existente do aplicativo, visite [criar ou atualizar um Gateway de aplicativo do Azure com firewall do aplicativo web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="bc224-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png