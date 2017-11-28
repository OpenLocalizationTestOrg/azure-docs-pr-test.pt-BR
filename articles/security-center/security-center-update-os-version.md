---
title: "Atualizar a versão do SO na Central de Segurança do Azure | Microsoft Docs"
description: "Este artigo mostra como implementar a recomendação da Central de Segurança do Azure **Atualizar versão do sistema operacional**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="6ca47-103">Atualizar a versão do sistema operacional na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="6ca47-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="6ca47-104">Para VMs (máquinas virtuais) em serviços de nuvem, a Central de Segurança do Azure recomendará que o SO (sistema operacional) seja atualizado se houver uma versão mais recente disponível.</span><span class="sxs-lookup"><span data-stu-id="6ca47-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="6ca47-105">Apenas serviços de nuvem da Web e funções de trabalho em execução em slots de produção são monitorados.</span><span class="sxs-lookup"><span data-stu-id="6ca47-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="6ca47-106">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6ca47-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="6ca47-107">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="6ca47-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="6ca47-108">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="6ca47-108">Implement the recommendation</span></span>
1. <span data-ttu-id="6ca47-109">Na folha **Recomendações**, selecione **Atualizar versão do sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="6ca47-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="6ca47-110">![Atualizar a versão do sistema operacional][1]</span><span class="sxs-lookup"><span data-stu-id="6ca47-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="6ca47-111">Isso abrirá a folha **Atualizar versão do sistema operacional**.</span><span class="sxs-lookup"><span data-stu-id="6ca47-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="6ca47-112">Siga as etapas nessa folha para atualizar a versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="6ca47-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="6ca47-113">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6ca47-113">See also</span></span>
<span data-ttu-id="6ca47-114">Este artigo mostrou como implementar a recomendação da Central de Segurança "Atualizar versão do iOS".</span><span class="sxs-lookup"><span data-stu-id="6ca47-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="6ca47-115">Para saber mais sobre os serviços de nuvem e atualizar a versão do sistema operacional para um serviço de nuvem, confira:</span><span class="sxs-lookup"><span data-stu-id="6ca47-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="6ca47-116">Visão geral dos Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="6ca47-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="6ca47-117">Como atualizar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="6ca47-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="6ca47-118">Como configurar serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="6ca47-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="6ca47-119">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6ca47-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="6ca47-120">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca47-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6ca47-121">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca47-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6ca47-122">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca47-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="6ca47-123">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="6ca47-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="6ca47-124">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="6ca47-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="6ca47-125">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.</span><span class="sxs-lookup"><span data-stu-id="6ca47-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="6ca47-126">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca47-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
