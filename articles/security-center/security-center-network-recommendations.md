---
title: "Protegendo sua rede na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento endereça as recomendações na Central de Segurança do Azure que ajudam a proteger sua rede do Azure e cumprir as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="3e1da-103">Protegendo sua rede na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="3e1da-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="3e1da-104">A Central de Segurança do Azure analisa o estado de segurança de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1da-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="3e1da-105">Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, ela cria recomendações que orientam você durante o processo de configuração dos controles necessários.</span><span class="sxs-lookup"><span data-stu-id="3e1da-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="3e1da-106">As recomendações se aplicam aos tipos de recursos do Azure: máquinas virtuais (VMs), rede, aplicativos e SQL.</span><span class="sxs-lookup"><span data-stu-id="3e1da-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="3e1da-107">Este artigo endereça as recomendações que se aplicam à rede.</span><span class="sxs-lookup"><span data-stu-id="3e1da-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="3e1da-108">As recomendações da rede giram em torno da próxima geração de firewalls, Grupos de Segurança da Rede, configuração das regras do tráfego de entrada e muito mais.</span><span class="sxs-lookup"><span data-stu-id="3e1da-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="3e1da-109">Use a tabela abaixo como referência para ajudá-lo a entender as recomendações da rede disponíveis e a ação de cada uma delas se forem aplicadas.</span><span class="sxs-lookup"><span data-stu-id="3e1da-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="3e1da-110">Recomendações disponíveis da rede</span><span class="sxs-lookup"><span data-stu-id="3e1da-110">Available network recommendations</span></span>
| <span data-ttu-id="3e1da-111">Recomendações</span><span class="sxs-lookup"><span data-stu-id="3e1da-111">Recommendation</span></span> | <span data-ttu-id="3e1da-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="3e1da-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3e1da-113">Adicionar um Firewall de Última Geração</span><span class="sxs-lookup"><span data-stu-id="3e1da-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="3e1da-114">Recomenda que você adicione um NGFW (Firewall de Última Geração) de um parceiro da Microsoft para aumentar suas proteções de segurança.</span><span class="sxs-lookup"><span data-stu-id="3e1da-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="3e1da-115">Rotear o tráfego apenas através do NGFW</span><span class="sxs-lookup"><span data-stu-id="3e1da-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="3e1da-116">Recomenda que você configure regras para o grupo de segurança de rede (NSG) que forcem o tráfego de entrada em sua VM a passar pelo NGFW.</span><span class="sxs-lookup"><span data-stu-id="3e1da-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="3e1da-117">Habilitar Grupos de Segurança de Rede em sub-redes ou máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="3e1da-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="3e1da-118">Recomenda que você habilite NSGs em sub-redes ou VMs.</span><span class="sxs-lookup"><span data-stu-id="3e1da-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="3e1da-119">Restringir o acesso por meio de ponto de extremidade para a Internet</span><span class="sxs-lookup"><span data-stu-id="3e1da-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="3e1da-120">Recomenda que você configure regras de tráfego de entrada para NSGs.</span><span class="sxs-lookup"><span data-stu-id="3e1da-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="3e1da-121">Confira também</span><span class="sxs-lookup"><span data-stu-id="3e1da-121">See also</span></span>
<span data-ttu-id="3e1da-122">Para saber mais sobre as recomendações que se aplicam aos outros tipos de recursos do Azure, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e1da-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="3e1da-123">Protegendo suas máquinas virtuais na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="3e1da-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="3e1da-124">Protegendo seus aplicativos na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="3e1da-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="3e1da-125">Protegendo o serviço do SQL Azure na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="3e1da-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="3e1da-126">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e1da-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="3e1da-127">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) : saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1da-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3e1da-128">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="3e1da-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="3e1da-129">[Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="3e1da-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
