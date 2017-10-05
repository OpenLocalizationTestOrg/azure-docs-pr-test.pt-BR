---
title: "Instalar o Endpoint Protection na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Instalar Endpoint Protection**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="01ddb-103">Instalar o Endpoint Protection na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="01ddb-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="01ddb-104">A Central de Segurança do Azure recomenda que você instale a proteção de ponto de extremidade nas VMs (máquinas virtuais) do Azure caso ainda não esteja habilitada.</span><span class="sxs-lookup"><span data-stu-id="01ddb-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="01ddb-105">Essa recomendação se aplica somente às VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="01ddb-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="01ddb-106">Esta implantação de exemplo usa o Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="01ddb-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="01ddb-107">Consulte a [Integração de parceiro na Central de Segurança do Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) para obter uma lista de parceiros integrados com a Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="01ddb-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="01ddb-108">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="01ddb-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="01ddb-109">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="01ddb-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="01ddb-110">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="01ddb-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="01ddb-111">Na folha **Recomendações**, selecione **Instalar o Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="01ddb-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="01ddb-112">![Selecione Instalar o Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="01ddb-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="01ddb-113">A folha **Instalar o Endpoint Protection** é aberta, exibindo uma lista de VMs sem a proteção de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="01ddb-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="01ddb-114">Selecione na lista as VMs em que você deseja instalar a proteção de ponto de extremidade e clique em **Instalar nas VMs**.</span><span class="sxs-lookup"><span data-stu-id="01ddb-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="01ddb-115">![Selecione as VMs nas quais instalar o Endpoint Protection][2]</span><span class="sxs-lookup"><span data-stu-id="01ddb-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="01ddb-116">A folha **Selecionar Endpoint Protection** será aberta para que você possa selecionar a solução de proteção de ponto de extremidade que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="01ddb-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="01ddb-117">Neste exemplo, vamos selecionar **Antimalware da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="01ddb-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="01ddb-118">![Selecionar Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="01ddb-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="01ddb-119">Informações adicionais sobre a solução de proteção de ponto de extremidade são exibidas.</span><span class="sxs-lookup"><span data-stu-id="01ddb-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="01ddb-120">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="01ddb-120">Select **Create**.</span></span>
   <span data-ttu-id="01ddb-121">![Criar solução antimalware][4]</span><span class="sxs-lookup"><span data-stu-id="01ddb-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="01ddb-122">Insira as configurações necessárias na folha **Adicionar Extensão** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="01ddb-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="01ddb-123">Para saber mais sobre as definições de configuração, veja [Configuração personalizada e padrão de antimalware](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="01ddb-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="01ddb-124">O [Microsoft Antimalware](../security/azure-security-antimalware.md) agora está ativo nas VMs selecionadas.</span><span class="sxs-lookup"><span data-stu-id="01ddb-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="01ddb-125">Confira também</span><span class="sxs-lookup"><span data-stu-id="01ddb-125">See also</span></span>
<span data-ttu-id="01ddb-126">Este artigo mostrou como implementar a recomendação da Central de Segurança "Instalar Endpoint Protection".</span><span class="sxs-lookup"><span data-stu-id="01ddb-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="01ddb-127">Para saber mais sobre como habilitar o Microsoft Antimalware no Azure, consulte o seguinte documento:</span><span class="sxs-lookup"><span data-stu-id="01ddb-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="01ddb-128">[Microsoft Antimalware para Serviços de Nuvem e Máquinas Virtuais](../security/azure-security-antimalware.md) – saiba como implantar o Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="01ddb-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="01ddb-129">Para saber mais sobre a Central de Segurança, confira os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="01ddb-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="01ddb-130">[Configuração de políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como definir as políticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="01ddb-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="01ddb-131">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="01ddb-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="01ddb-132">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="01ddb-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="01ddb-133">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="01ddb-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="01ddb-134">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="01ddb-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="01ddb-135">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="01ddb-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="01ddb-136">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="01ddb-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
