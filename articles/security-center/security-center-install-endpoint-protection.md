---
title: "aaaInstall proteção de ponto de extremidade na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * instalar Endpoint Protection * *."
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
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="08abc-103">Instalar o Endpoint Protection na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="08abc-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="08abc-104">A Central de Segurança do Azure recomenda que você instale a proteção de ponto de extremidade nas VMs (máquinas virtuais) do Azure caso ainda não esteja habilitada.</span><span class="sxs-lookup"><span data-stu-id="08abc-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="08abc-105">Essa recomendação se aplica somente a máquinas virtuais tooWindows.</span><span class="sxs-lookup"><span data-stu-id="08abc-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="08abc-106">Esta implantação de exemplo usa o Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="08abc-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="08abc-107">Consulte a [Integração de parceiro na Central de Segurança do Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) para obter uma lista de parceiros integrados com a Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="08abc-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="08abc-108">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="08abc-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="08abc-109">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="08abc-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="08abc-110">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="08abc-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="08abc-111">Em Olá **recomendações** folha, selecione **instalar o Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="08abc-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="08abc-112">![Selecione Instalar o Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="08abc-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="08abc-113">Olá **instalar o Endpoint Protection** folha é aberta exibindo uma lista de máquinas virtuais sem proteção de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="08abc-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="08abc-114">Selecione Olá Olá de lista VMs que você deseja tooinstall proteção de ponto de extremidade em e clique em **instalar nas máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="08abc-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="08abc-115">![Selecione VMs tooinstall Endpoint Protection no][2]</span><span class="sxs-lookup"><span data-stu-id="08abc-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="08abc-116">Olá **selecione Endpoint Protection** folha abre tooallow você tooselect Olá endpoint protection solução desejada toouse.</span><span class="sxs-lookup"><span data-stu-id="08abc-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="08abc-117">Neste exemplo, vamos selecionar **Antimalware da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="08abc-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="08abc-118">![Selecionar Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="08abc-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="08abc-119">Informações adicionais sobre solução de proteção de ponto de extremidade de saudação são exibidas.</span><span class="sxs-lookup"><span data-stu-id="08abc-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="08abc-120">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08abc-120">Select **Create**.</span></span>
   <span data-ttu-id="08abc-121">![Criar solução antimalware][4]</span><span class="sxs-lookup"><span data-stu-id="08abc-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="08abc-122">Insira configurações Olá necessárias no hello **Adicionar extensão** folha e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="08abc-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="08abc-123">toolearn mais sobre configurações hello, consulte [padrão e a configuração de Antimalware personalizada](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="08abc-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="08abc-124">[O Antimalware da Microsoft](../security/azure-security-antimalware.md) está ativo no hello selecionado VMs.</span><span class="sxs-lookup"><span data-stu-id="08abc-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="08abc-125">Consulte também</span><span class="sxs-lookup"><span data-stu-id="08abc-125">See also</span></span>
<span data-ttu-id="08abc-126">Este artigo lhe mostrou como tooimplement Olá recomendação da Central de segurança "Instalar o Endpoint Protection."</span><span class="sxs-lookup"><span data-stu-id="08abc-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="08abc-127">toolearn mais sobre como habilitar o Antimalware da Microsoft no Azure, consulte Olá documento a seguir:</span><span class="sxs-lookup"><span data-stu-id="08abc-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="08abc-128">[O Antimalware da Microsoft para serviços de nuvem e máquinas virtuais](../security/azure-security-antimalware.md) – Saiba como toodeploy Antimalware da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="08abc-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="08abc-129">toolearn mais sobre o Centro de segurança, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="08abc-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="08abc-130">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="08abc-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="08abc-131">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="08abc-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="08abc-132">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="08abc-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="08abc-133">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="08abc-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="08abc-134">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="08abc-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="08abc-135">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="08abc-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="08abc-136">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="08abc-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
