---
title: "Adicionar um Firewall do Aplicativo Web na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure **Adicionar um Firewall do Aplicativo Web** e **Finalizar a proteção do aplicativo**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: d04a07237029953d8a9b20704d85e852ce45d867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="49e42-103">Adicionar um Firewall do Aplicativo Web na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="49e42-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="49e42-104">A Central de Segurança do Azure pode recomendar que você adicione um WAF (Firewall do Aplicativo Web) de um parceiro da Microsoft para proteger seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="49e42-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span></span> <span data-ttu-id="49e42-105">Este documento guiará você por um exemplo de como realizar essa recomendação.</span><span class="sxs-lookup"><span data-stu-id="49e42-105">This document walks you through an example of how to apply this recommendation.</span></span>

<span data-ttu-id="49e42-106">Uma recomendação WAF é mostrada para qualquer IP voltado para uso público (IP de nível de instância ou IP de balanceamento de carga) que tem um grupo de segurança de rede associado com portas de entrada da Web abertas (80,443).</span><span class="sxs-lookup"><span data-stu-id="49e42-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="49e42-107">A Central de Segurança recomenda que você provisione um WAF para ajudar a proteger contra ataques direcionados a seus aplicativos Web em máquinas virtuais e no Ambiente do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49e42-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="49e42-108">Um ASE (Ambiente do Serviço de Aplicativo) é uma opção do plano de serviço [Premium](https://azure.microsoft.com/pricing/details/app-service/) do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e42-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="49e42-109">Para saber mais sobre o ASE, consulte a [Documentação do Ambiente do Serviço de Aplicativo](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="49e42-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="49e42-110">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="49e42-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="49e42-111">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="49e42-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="49e42-112">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="49e42-112">Implement the recommendation</span></span>
1. <span data-ttu-id="49e42-113">Na folha **Recomendações**, selecione **Proteger o aplicativo Web usando o Firewall do Aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="49e42-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="49e42-114">![Aplicativo Web protegido][1]</span><span class="sxs-lookup"><span data-stu-id="49e42-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="49e42-115">Na folha **Proteger seus aplicativos Web usando o Firewall do Aplicativo Web** , selecione um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="49e42-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="49e42-116">A folha **Adicionar um Firewall do Aplicativo Web** é aberta.</span><span class="sxs-lookup"><span data-stu-id="49e42-116">The **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="49e42-117">![Add a web application firewall][2]</span><span class="sxs-lookup"><span data-stu-id="49e42-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="49e42-118">Você pode optar por usar um Firewall do Aplicativo Web existente, se disponível, ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="49e42-118">You can choose to use an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="49e42-119">Neste exemplo, não existem WAFs disponíveis, por isso vamos criar um novo.</span><span class="sxs-lookup"><span data-stu-id="49e42-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="49e42-120">Para criar um WAF, selecione uma solução da lista dos parceiros integrados.</span><span class="sxs-lookup"><span data-stu-id="49e42-120">To create a WAF, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="49e42-121">Neste exemplo, selecionamos **Barracuda Web Application Firewall**.</span><span class="sxs-lookup"><span data-stu-id="49e42-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="49e42-122">A folha **Firewall do Aplicativo Web Barracuda** se abre e fornece informações sobre a solução do parceiro.</span><span class="sxs-lookup"><span data-stu-id="49e42-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="49e42-123">Selecione **Criar** na folha de informações.</span><span class="sxs-lookup"><span data-stu-id="49e42-123">Select **Create** in the information blade.</span></span>

   ![Folha Informações do firewall][3]

6. <span data-ttu-id="49e42-125">A folha **Novo Firewall do Aplicativo Web** é aberta e você pode executar as etapas de **Configuração da VM** e fornecer **Informações do WAF**.</span><span class="sxs-lookup"><span data-stu-id="49e42-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="49e42-126">Selecione **Configuração da VM**.</span><span class="sxs-lookup"><span data-stu-id="49e42-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="49e42-127">Na folha **Configuração da VM**, você deve inserir as informações necessárias para criar a máquina virtual que executará o WAF.</span><span class="sxs-lookup"><span data-stu-id="49e42-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span></span>
   <span data-ttu-id="49e42-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="49e42-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="49e42-129">Volte para a folha **Novo Firewall do Aplicativo Web** e selecione **Informações do WAF**.</span><span class="sxs-lookup"><span data-stu-id="49e42-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="49e42-130">Você configura o WAF em si na folha **Informações do WAF**.</span><span class="sxs-lookup"><span data-stu-id="49e42-130">In the **WAF Information** blade, you configure the WAF itself.</span></span> <span data-ttu-id="49e42-131">A Etapa 7 permite configurar a máquina virtual na qual o WAF será executado e a Etapa 8 permite provisionar o WAF em si.</span><span class="sxs-lookup"><span data-stu-id="49e42-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="49e42-132">Finalizar a proteção do aplicativo</span><span class="sxs-lookup"><span data-stu-id="49e42-132">Finalize application protection</span></span>
1. <span data-ttu-id="49e42-133">Volte para a folha **Recomendações** .</span><span class="sxs-lookup"><span data-stu-id="49e42-133">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="49e42-134">Uma nova entrada foi gerada depois que você criou o WAF, chamada **Finalizar a proteção do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="49e42-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="49e42-135">Essa entrada informa o que é necessário para concluir o processo de conectar o WAF dentro da Rede Virtual do Azure para que ele possa proteger o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49e42-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span></span>

   ![Finalizar a proteção do aplicativo][5]

2. <span data-ttu-id="49e42-137">Selecione **Finalizar a proteção do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="49e42-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="49e42-138">Uma nova lâmina é aberta.</span><span class="sxs-lookup"><span data-stu-id="49e42-138">A new blade opens.</span></span> <span data-ttu-id="49e42-139">Você pode ver que há um aplicativo Web que precisa ter seu tráfego redirecionado.</span><span class="sxs-lookup"><span data-stu-id="49e42-139">You can see that there is a web application that needs to have its traffic rerouted.</span></span>
3. <span data-ttu-id="49e42-140">Selecione o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="49e42-140">Select the web application.</span></span> <span data-ttu-id="49e42-141">Uma folha será aberta com etapas para concluir a configuração de firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="49e42-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span></span> <span data-ttu-id="49e42-142">Conclua as etapas e selecione **Restringir o tráfego**.</span><span class="sxs-lookup"><span data-stu-id="49e42-142">Complete the steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="49e42-143">A Central de Segurança criará então as estruturas para você.</span><span class="sxs-lookup"><span data-stu-id="49e42-143">Security Center then does the wiring-up for you.</span></span>

   ![Restringir o tráfego][6]

> [!NOTE]
> <span data-ttu-id="49e42-145">Você pode proteger vários aplicativos Web na Central de segurança adicionando-os às suas implantações do WAF existentes.</span><span class="sxs-lookup"><span data-stu-id="49e42-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span>
>
>

<span data-ttu-id="49e42-146">Os logs daquele WAF agora estão totalmente integrados.</span><span class="sxs-lookup"><span data-stu-id="49e42-146">The logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="49e42-147">A Central de Segurança pode iniciar a coleta e a análise dos logs automaticamente para revelar alertas de segurança importantes para você.</span><span class="sxs-lookup"><span data-stu-id="49e42-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49e42-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49e42-148">Next steps</span></span>
<span data-ttu-id="49e42-149">Este documento mostrou como implementar a recomendação da Central de Segurança "Adicionar um aplicativo Web".</span><span class="sxs-lookup"><span data-stu-id="49e42-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="49e42-150">Para saber mais sobre como configurar um Firewall do Aplicativo Web, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="49e42-150">To learn more about configuring a web application firewall, see the following:</span></span>

* [<span data-ttu-id="49e42-151">Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="49e42-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="49e42-152">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="49e42-152">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="49e42-153">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e42-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="49e42-154">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e42-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="49e42-155">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) – aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="49e42-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="49e42-156">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) – saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e42-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="49e42-157">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) – encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="49e42-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="49e42-158">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e42-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
