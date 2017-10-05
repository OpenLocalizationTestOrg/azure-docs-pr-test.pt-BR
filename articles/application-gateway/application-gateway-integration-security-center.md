---
title: "Integração de Gateway de Aplicativo do com a Central de segurança do Azure | Microsoft Docs"
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
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="3e34e-103">Visão geral da integração entre o Gateway de Aplicativo e a Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="3e34e-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="3e34e-104">Saiba como o Gateway de Aplicativo e a Central de segurança ajudam a proteger os recursos do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3e34e-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="3e34e-105">O firewall do aplicativo Web do Gateway de aplicativo (WAF) integra-se com a [Central de segurança](../security-center/security-center-intro.md) para fornecer uma visualização perfeita para evitar, detectar e reagir às ameaças a aplicativos Web desprotegidos no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3e34e-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="3e34e-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3e34e-106">Overview</span></span>

<span data-ttu-id="3e34e-107">O WAF do Gateway de Aplicativo é uma recomendação na Central de segurança para proteger aplicativos Web contra explorações e vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="3e34e-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="3e34e-108">Recursos da Web que não estão protegidos por WAF são exibidos na central de segurança como recomendações de severidade alta.</span><span class="sxs-lookup"><span data-stu-id="3e34e-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="3e34e-109">Recomendações para firewalls de aplicativo Web são mostradas na página **Visão geral** em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![integração com a central de segurança][1]

<span data-ttu-id="3e34e-111">Clicando em uma recomendação sobre o firewall do aplicativo Web abre uma nova folha mostrando os detalhes da recomendação.</span><span class="sxs-lookup"><span data-stu-id="3e34e-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="3e34e-112">Adicionar o firewall do aplicativo Web a um recurso existente</span><span class="sxs-lookup"><span data-stu-id="3e34e-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="3e34e-113">Navegue até **Mais serviços** > **Segurança + Identidade** > **Central de Segurança** e na folha **Central de Segurança - Visão geral**, clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="3e34e-114">Na folha **Central de Segurança - Aplicativos**, a tabela contém uma lista de aplicativos que a Central de segurança detectou na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3e34e-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![aplicativos Web][3]

<span data-ttu-id="3e34e-116">Ao clicar em um aplicativo Web com um problema crítico, você obtém a folha **Integridade da segurança do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="3e34e-117">Na imagem abaixo, está o aplicativo Web que não está protegido por um firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3e34e-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![recursos Web não protegidos][2]

<span data-ttu-id="3e34e-119">Clique em **Adicionar um firewall do aplicativo Web** em **Recomendações** para abrir a folha **Adicionar um Firewall do aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="3e34e-120">Se você não tiver um Gateway de aplicativo existente ou quiser criar um novo, clique em **Criar novo** e na folha **Criar um novo Firewall do aplicativo Web**, clique em **Microsoft - Gateway de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="3e34e-121">Isso leva você para as etapas para criar um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="3e34e-122">Neste ponto, seu aplicativo Web é adicionado como um recurso protegido, agora a Central de segurança controla o que esse recurso está protegido por um firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="3e34e-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="3e34e-123">Isso não o adiciona como um membro do pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="3e34e-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="3e34e-124">Se você tiver um gateway de aplicativo existente, é possível escolhê-lo em **Usar solução existente**</span><span class="sxs-lookup"><span data-stu-id="3e34e-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![folha adicionar firewall do aplicativo Web][4]

<span data-ttu-id="3e34e-126">Adicionar que um aplicativo Web a um gateway de aplicativo por meio da Central de segurança não adiciona o recurso como um membro do pool de back-end, isso deve ser feito no recurso de gateway de aplicativo diretamente.</span><span class="sxs-lookup"><span data-stu-id="3e34e-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="3e34e-127">Adicionar um recurso a um firewall do aplicativo Web existente</span><span class="sxs-lookup"><span data-stu-id="3e34e-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="3e34e-128">Navegue até **Mais serviços** > **Segurança + Identidade** > **Central de Segurança** e na folha **Central de Segurança - Visão geral**, clique em **Soluções de parceiros**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="3e34e-129">Gateways de aplicativo com reconhecimento da Central de segurança existentes na folha **Soluções de parceiros**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![soluções de parceiros][7]

<span data-ttu-id="3e34e-131">Clique em **Vincular aplicativo** para abrir a folha **Vincular aplicativos**, aqui você terá as opções para selecionar os aplicativos existentes.</span><span class="sxs-lookup"><span data-stu-id="3e34e-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="3e34e-132">Escolha os aplicativos para serem protegidos e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="3e34e-133">Isso não adiciona o aplicativo Web ao pool de back-end do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="3e34e-134">Isso define os recursos como um recurso protegido para que a Central de segurança possa controlá-lo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="3e34e-135">Para adicionar o recurso como um membro do pool de back-end, isso deve ser feito no gateway de aplicativo, na folha atual, você pode clicar em **Console de solução** para ser levado ao recurso de gateway de aplicativo onde você pode adicionar o aplicativo Web ao pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="3e34e-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![aplicativos de soluções de parceiros][6]

## <a name="finalize-configuration"></a><span data-ttu-id="3e34e-137">Finalizar a configuração</span><span class="sxs-lookup"><span data-stu-id="3e34e-137">Finalize configuration</span></span>

<span data-ttu-id="3e34e-138">A Central de segurança controla os aplicativos adicionados a um gateway de aplicativo como um recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="3e34e-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="3e34e-139">Ela monitora a integridade desse recurso e garante que ele seja protegido por um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="3e34e-140">A próxima etapa é adicionar o IP privado, o IP público ou a NIC de sua máquina virtual para o pool de back-end do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="3e34e-141">Até que isso seja feito, uma recomendação adicional de **Finalizar a proteção do aplicativo** é mostrada até que o recurso seja adicionado.</span><span class="sxs-lookup"><span data-stu-id="3e34e-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![folha adicionar firewall do aplicativo Web][5]

## <a name="security-alerts"></a><span data-ttu-id="3e34e-143">Alertas de segurança</span><span class="sxs-lookup"><span data-stu-id="3e34e-143">Security Alerts</span></span>

<span data-ttu-id="3e34e-144">Na Central de segurança, navegue até **DETECÇÃO** > **Alertas de segurança**.</span><span class="sxs-lookup"><span data-stu-id="3e34e-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="3e34e-145">Aqui você encontra alertas do WAF para seus gateways de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="3e34e-146">Os alertas são divididos pela regra do WAF.</span><span class="sxs-lookup"><span data-stu-id="3e34e-146">Alerts are broken down by WAF rule.</span></span>

![alertas de segurança][8]

<span data-ttu-id="3e34e-148">Clicar em uma regra fornecerá uma lista de alertas para essa regra específica do WAF.</span><span class="sxs-lookup"><span data-stu-id="3e34e-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="3e34e-149">Cada alerta mostra detalhes adicionais sobre a descoberta.</span><span class="sxs-lookup"><span data-stu-id="3e34e-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="3e34e-150">Os detalhes fornecem um link para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e34e-150">The details provide a link to the application gateway.</span></span>
 
![detalhes do alerta][9]

## <a name="next-steps"></a><span data-ttu-id="3e34e-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e34e-152">Next steps</span></span>

<span data-ttu-id="3e34e-153">Para saber como ativar o firewall de aplicativo Web em um Gateway de Aplicativo existente, visite [Criar ou atualizar um Gateway de Aplicativo do Azure com o firewall de aplicativo Web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="3e34e-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png