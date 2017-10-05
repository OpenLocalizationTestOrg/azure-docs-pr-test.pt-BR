---
title: "Introdução à Central de Segurança do Azure | Microsoft Docs"
description: "Saiba mais sobre a Central de Segurança do Azure, seus principais recursos e como ela funciona."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="47f61-103">Introdução à Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="47f61-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="47f61-104">Saiba mais sobre a Central de Segurança do Azure, seus principais recursos e como ela funciona.</span><span class="sxs-lookup"><span data-stu-id="47f61-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="47f61-105">A partir do início de junho de 2017, a Central de Segurança usará o Microsoft Monitoring Agent para coletar e armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="47f61-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="47f61-106">Veja [Migração da Plataforma Central de Segurança do Azure](security-center-platform-migration.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="47f61-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="47f61-107">As informações deste artigo representam a funcionalidade da Central de Segurança após a transição para o Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="47f61-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="47f61-108">O que é a Central de Segurança do Azure?</span><span class="sxs-lookup"><span data-stu-id="47f61-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="47f61-109">A Central de Segurança ajuda você a impedir, detectar e responder a ameaças com maior visibilidade e controle sobre a segurança dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-109">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="47f61-110">Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="47f61-111">Principais recursos</span><span class="sxs-lookup"><span data-stu-id="47f61-111">Key capabilities</span></span>
 <span data-ttu-id="47f61-112">A Central de Segurança oferece uma prevenção contra ameaças eficiente e fácil de usar, além de recursos de detecção e resposta que são internos no Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="47f61-113">Os principais recursos são:</span><span class="sxs-lookup"><span data-stu-id="47f61-113">Key capabilities are:</span></span>

| <span data-ttu-id="47f61-114">Estágio</span><span class="sxs-lookup"><span data-stu-id="47f61-114">Stage</span></span> | <span data-ttu-id="47f61-115">Recurso</span><span class="sxs-lookup"><span data-stu-id="47f61-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="47f61-116">Evitar</span><span class="sxs-lookup"><span data-stu-id="47f61-116">Prevent</span></span> |<span data-ttu-id="47f61-117">Monitora o estado de segurança de seus recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="47f61-117">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="47f61-118">Evitar</span><span class="sxs-lookup"><span data-stu-id="47f61-118">Prevent</span></span> | <span data-ttu-id="47f61-119">Define políticas para suas assinaturas do Azure com base nos requisitos de segurança da sua empresa, nos tipos de aplicativos que você usa e na confidencialidade dos seus dados</span><span class="sxs-lookup"><span data-stu-id="47f61-119">Defines policies for your Azure subscriptions based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="47f61-120">Evitar</span><span class="sxs-lookup"><span data-stu-id="47f61-120">Prevent</span></span> | <span data-ttu-id="47f61-121">Usa recomendações de segurança orientadas por políticas para guiar seus proprietários através do processo de implementação dos controles necessários</span><span class="sxs-lookup"><span data-stu-id="47f61-121">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="47f61-122">Evitar</span><span class="sxs-lookup"><span data-stu-id="47f61-122">Prevent</span></span> | <span data-ttu-id="47f61-123">Implanta rapidamente aplicativos da Microsoft e de parceiros e serviços de segurança</span><span class="sxs-lookup"><span data-stu-id="47f61-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="47f61-124">Detectar</span><span class="sxs-lookup"><span data-stu-id="47f61-124">Detect</span></span> |<span data-ttu-id="47f61-125">Coleta e analisa dados de segurança automaticamente de seus recursos do Azure, da rede e de soluções de parceiros, como programas antimalware e firewalls</span><span class="sxs-lookup"><span data-stu-id="47f61-125">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="47f61-126">Detectar</span><span class="sxs-lookup"><span data-stu-id="47f61-126">Detect</span></span> | <span data-ttu-id="47f61-127">Usa as ameaças globais de inteligência dos produtos e serviços Microsoft, a unidade de Crimes digitais da Microsoft (DCU), o Microsoft Security Response Center (MSRC) e feeds externos</span><span class="sxs-lookup"><span data-stu-id="47f61-127">Uses global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="47f61-128">Detectar</span><span class="sxs-lookup"><span data-stu-id="47f61-128">Detect</span></span> | <span data-ttu-id="47f61-129">Aplica a análise avançada, incluindo aprendizado de máquina e análise comportamental</span><span class="sxs-lookup"><span data-stu-id="47f61-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="47f61-130">Responder</span><span class="sxs-lookup"><span data-stu-id="47f61-130">Respond</span></span> |<span data-ttu-id="47f61-131">Fornece alertas/incidentes de segurança priorizados</span><span class="sxs-lookup"><span data-stu-id="47f61-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="47f61-132">Responder</span><span class="sxs-lookup"><span data-stu-id="47f61-132">Respond</span></span> | <span data-ttu-id="47f61-133">Oferece informações sobre a origem do ataque e dos recursos afetados</span><span class="sxs-lookup"><span data-stu-id="47f61-133">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="47f61-134">Responder</span><span class="sxs-lookup"><span data-stu-id="47f61-134">Respond</span></span> | <span data-ttu-id="47f61-135">Sugere maneiras para interromper o ataque atual e ajudar a evitar ataques futuros</span><span class="sxs-lookup"><span data-stu-id="47f61-135">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="47f61-136">Passo a passo introdutório</span><span class="sxs-lookup"><span data-stu-id="47f61-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="47f61-137">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="47f61-137">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="47f61-138">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="47f61-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="47f61-139">Você acessar a Central de Segurança pelo [portal do Azure](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="47f61-139">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="47f61-140">[Entre no Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47f61-140">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="47f61-141">No menu principal do portal, role até a opção **Central de Segurança** ou escolha o bloco **Central de Segurança** que você fixou anteriormente ao painel do Portal.</span><span class="sxs-lookup"><span data-stu-id="47f61-141">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Bloco de segurança no portal do Azure][1]

<span data-ttu-id="47f61-143">Na Central de Segurança, defina as políticas de segurança, monitore as configurações de segurança e exiba alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="47f61-144">Diretivas de segurança</span><span class="sxs-lookup"><span data-stu-id="47f61-144">Security policies</span></span>
<span data-ttu-id="47f61-145">Você pode definir políticas para suas assinaturas do Azure de acordo com os requisitos de segurança da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="47f61-145">You can define policies for your Azure subscriptions according to your company's security requirements.</span></span> <span data-ttu-id="47f61-146">Você também pode personalizar os tipos de aplicativos que está usando ou a confidencialidade dos dados em cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="47f61-146">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="47f61-147">Por exemplo, os recursos usados para desenvolvimento ou teste podem ter requisitos de segurança diferentes daqueles usados para aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="47f61-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="47f61-148">Da mesma forma, os aplicativos com dados regulamentados, como PII, podem exigir um nível mais alto de segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="47f61-149">Para modificar uma política de segurança, você deve ser um Administrador de Segurança ou o Proprietário ou Colaborador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="47f61-149">To modify a security policy, you must be a Security Administrator or the subscription's Owner or Contributor.</span></span> <span data-ttu-id="47f61-150">Confira [Permissões na Central de Segurança do Azure](security-center-permissions.md) para saber mais sobre as funções e as ações permitidas na Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-150">To learn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="47f61-151">Na folha **Central de segurança**, selecione o bloco **Política** para obter uma lista de suas assinaturas e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="47f61-151">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Folha da Central de segurança][2]

<span data-ttu-id="47f61-153">Na folha **Política de segurança** , selecione uma assinatura para exibir os detalhes da política.</span><span class="sxs-lookup"><span data-stu-id="47f61-153">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

<span data-ttu-id="47f61-154">**Coleta de dados** habilita a coleta de dados para uma política de segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="47f61-155">A habilitação fornece:</span><span class="sxs-lookup"><span data-stu-id="47f61-155">Enabling provides:</span></span>

* <span data-ttu-id="47f61-156">Verificação diária de todas as máquinas virtuais com suporte para monitoramento de segurança e recomendações.</span><span class="sxs-lookup"><span data-stu-id="47f61-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="47f61-157">Coleção de eventos de segurança para a análise e detecção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="47f61-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="47f61-158">A coleta de dados é configurada no nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="47f61-158">Data collection is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="47f61-159">Selecione **Política de prevenção** para abrir a folha **Política de prevenção**.</span><span class="sxs-lookup"><span data-stu-id="47f61-159">Select **Prevention policy** to open the **Prevention policy** blade.</span></span> <span data-ttu-id="47f61-160">**Mostrar recomendações para** permite que você escolha os controles de segurança que deseja monitorar e as recomendações que você deseja ver, com base nas necessidades de segurança dos recursos na assinatura.</span><span class="sxs-lookup"><span data-stu-id="47f61-160">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="47f61-161">Recomendações de segurança</span><span class="sxs-lookup"><span data-stu-id="47f61-161">Security recommendations</span></span>
 <span data-ttu-id="47f61-162">A Central de Segurança analisa o estado de segurança de seus recursos do Azure para identificar possíveis vulnerabilidades na segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-162">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="47f61-163">Uma lista de recomendações orienta você no processo de configuração dos controles necessários.</span><span class="sxs-lookup"><span data-stu-id="47f61-163">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="47f61-164">Os exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="47f61-164">Examples include:</span></span>

* <span data-ttu-id="47f61-165">Provisionamento de antimalware para ajudar a identificar e remover software mal-intencionado</span><span class="sxs-lookup"><span data-stu-id="47f61-165">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="47f61-166">Configurando os grupos de segurança de rede e as regras para controlar o tráfego para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="47f61-166">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="47f61-167">Provisionamento de firewalls do aplicativo Web para ajudar a proteger contra ataques direcionados aos seus aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="47f61-167">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="47f61-168">Como implantar atualizações de sistema ausentes</span><span class="sxs-lookup"><span data-stu-id="47f61-168">Deploying missing system updates</span></span>
* <span data-ttu-id="47f61-169">Endereçamento de configurações do sistema operacional que não coincidem com as linhas de base recomendadas</span><span class="sxs-lookup"><span data-stu-id="47f61-169">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="47f61-170">Clique no bloco **Recomendações** para obter uma lista de recomendações.</span><span class="sxs-lookup"><span data-stu-id="47f61-170">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="47f61-171">Clique em cada recomendação para exibir informações adicionais ou tomar uma atitude para resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="47f61-171">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Recomendações de segurança na Central de Segurança do Azure][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="47f61-173">Estado da segurança dos recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="47f61-173">Security state of Azure resources</span></span>
<span data-ttu-id="47f61-174">A seção **Prevenção** do painel mostra a postura geral de segurança do ambiente por tipo de recurso, incluindo VMs, aplicativos Web e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="47f61-174">The **Prevention** section of the dashboard shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="47f61-175">Selecione um tipo de recurso em **Prevenção** para exibir mais informações, incluindo uma lista de possíveis vulnerabilidades de segurança que foram identificadas.</span><span class="sxs-lookup"><span data-stu-id="47f61-175">Select a resource type under **Prevention** to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="47f61-176">(**Computação** é selecionado no exemplo a seguir.)</span><span class="sxs-lookup"><span data-stu-id="47f61-176">(**Compute** is selected in the example below.)</span></span>

![Bloco de integridade de recursos][6]

### <a name="security-alerts"></a><span data-ttu-id="47f61-178">Alertas de segurança</span><span class="sxs-lookup"><span data-stu-id="47f61-178">Security alerts</span></span>
 <span data-ttu-id="47f61-179">A Central de segurança automaticamente coleta, analisa e integra os dados de registro de seus recursos do Azure, da rede e das soluções de parceiros como programas antimalware e firewalls.</span><span class="sxs-lookup"><span data-stu-id="47f61-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="47f61-180">Quando forem detectadas ameaças, é criado um alerta de segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="47f61-181">Os exemplos abrangem a detecção de:</span><span class="sxs-lookup"><span data-stu-id="47f61-181">Examples include detection of:</span></span>

* <span data-ttu-id="47f61-182">As máquinas virtuais comprometidas se comunicam com os endereços IP mal-intencionados conhecidos</span><span class="sxs-lookup"><span data-stu-id="47f61-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="47f61-183">Malware avançado detectado usando o relatório de erros do Windows</span><span class="sxs-lookup"><span data-stu-id="47f61-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="47f61-184">Ataques por força bruta contra máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="47f61-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="47f61-185">Alertas de segurança dos firewalls e programas antimalware integrados</span><span class="sxs-lookup"><span data-stu-id="47f61-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="47f61-186">Clicar no bloco **alertas de segurança** exibe uma lista de alertas prioritários.</span><span class="sxs-lookup"><span data-stu-id="47f61-186">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Alertas de segurança][7]

<span data-ttu-id="47f61-188">Selecionar um alerta mostra mais informações sobre o ataque e sugestões para corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="47f61-188">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![Detalhes do alerta de segurança][8]

### <a name="partner-solutions"></a><span data-ttu-id="47f61-190">Soluções de parceiros</span><span class="sxs-lookup"><span data-stu-id="47f61-190">Partner solutions</span></span>
<span data-ttu-id="47f61-191">O bloco **Soluções de parceiros** permite monitorar rapidamente o estado da segurança de suas soluções de parceiros integradas com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-191">The **Partner solutions** tile lets you monitor at a glance the security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="47f61-192">A Central de Segurança exibe alertas das soluções.</span><span class="sxs-lookup"><span data-stu-id="47f61-192">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="47f61-193">Selecione o bloco **Soluções de parceiros** .</span><span class="sxs-lookup"><span data-stu-id="47f61-193">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="47f61-194">Uma folha será aberta exibindo uma lista de todas as soluções de parceiro conectadas.</span><span class="sxs-lookup"><span data-stu-id="47f61-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![Soluções de parceiros][9]

## <a name="get-started"></a><span data-ttu-id="47f61-196">Introdução</span><span class="sxs-lookup"><span data-stu-id="47f61-196">Get started</span></span>
<span data-ttu-id="47f61-197">Para começar a usar a Central de Segurança, você precisa ter uma assinatura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-197">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="47f61-198">A Central de segurança é habilitada com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="47f61-199">Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47f61-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="47f61-200">Você acessar a Central de Segurança pelo [portal do Azure](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="47f61-200">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="47f61-201">Consulte a [documentação do portal](https://azure.microsoft.com/documentation/services/azure-portal/) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="47f61-201">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="47f61-202">[Introdução à Central de Segurança do Azure](security-center-get-started.md) o orienta rapidamente quanto ao monitoramento de segurança e aos componentes de gerenciamento da política da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47f61-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47f61-203">Next steps</span></span>
<span data-ttu-id="47f61-204">Neste documento, você foi apresentado à Central de Segurança, seus principais recursos e como começar.</span><span class="sxs-lookup"><span data-stu-id="47f61-204">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="47f61-205">Para saber mais, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="47f61-205">To learn more, see the following resources:</span></span>

* <span data-ttu-id="47f61-206">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) : saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="47f61-207">[Gerenciando as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="47f61-208">[Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="47f61-209">[Gerenciando e respondendo aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="47f61-209">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="47f61-210">[Monitorando as soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="47f61-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="47f61-211">[Segurança de dados da Central de Segurança do Azure](security-center-data-security.md) – saiba como os dados são gerenciados e protegidos na Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="47f61-212">[Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="47f61-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="47f61-213">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="47f61-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
