---
title: "aaaProtecting sua rede na Central de segurança do Azure | Microsoft Docs"
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
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="5f289-103">Protegendo sua rede na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="5f289-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="5f289-104">Central de segurança do Azure analisa o estado de segurança Olá seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f289-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="5f289-105">Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria recomendações que o guiam pelo processo de saudação de Configurando controles de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="5f289-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="5f289-106">Recomendações se aplicam a tipos de recurso tooAzure: máquinas virtuais (VMs), redes, aplicativos e SQL.</span><span class="sxs-lookup"><span data-stu-id="5f289-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="5f289-107">Este artigo aborda as recomendações que se aplicam a rede tooyour.</span><span class="sxs-lookup"><span data-stu-id="5f289-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="5f289-108">As recomendações da rede giram em torno da próxima geração de firewalls, Grupos de Segurança da Rede, configuração das regras do tráfego de entrada e muito mais.</span><span class="sxs-lookup"><span data-stu-id="5f289-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="5f289-109">Tabela de saudação uso abaixo como uma referência toohelp entender recomendações de rede disponível hello e o que faz cada uma se você aplicá-lo.</span><span class="sxs-lookup"><span data-stu-id="5f289-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="5f289-110">Recomendações disponíveis da rede</span><span class="sxs-lookup"><span data-stu-id="5f289-110">Available network recommendations</span></span>
| <span data-ttu-id="5f289-111">Recomendações</span><span class="sxs-lookup"><span data-stu-id="5f289-111">Recommendation</span></span> | <span data-ttu-id="5f289-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="5f289-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="5f289-113">Adicionar um Firewall de Última Geração</span><span class="sxs-lookup"><span data-stu-id="5f289-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="5f289-114">Recomenda que você adicione um Firewall de próxima geração (NGFW) de um tooincrease de parceiro Microsoft suas proteções de segurança.</span><span class="sxs-lookup"><span data-stu-id="5f289-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="5f289-115">Rotear o tráfego apenas através do NGFW</span><span class="sxs-lookup"><span data-stu-id="5f289-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="5f289-116">Recomenda que você configure regras de grupo (NSG) de segurança de rede que forçar o tráfego de entrada tooyour VM por meio de seu NGFW.</span><span class="sxs-lookup"><span data-stu-id="5f289-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="5f289-117">Habilitar Grupos de Segurança de Rede em sub-redes ou máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5f289-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="5f289-118">Recomenda que você habilite NSGs em sub-redes ou VMs.</span><span class="sxs-lookup"><span data-stu-id="5f289-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="5f289-119">Restringir o acesso por meio de ponto de extremidade para a Internet</span><span class="sxs-lookup"><span data-stu-id="5f289-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="5f289-120">Recomenda que você configure regras de tráfego de entrada para NSGs.</span><span class="sxs-lookup"><span data-stu-id="5f289-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="5f289-121">Consulte também</span><span class="sxs-lookup"><span data-stu-id="5f289-121">See also</span></span>
<span data-ttu-id="5f289-122">toolearn mais informações sobre recomendações que se aplicam a tipos de recursos do Azure tooother, consulte Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="5f289-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="5f289-123">Protegendo suas máquinas virtuais na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="5f289-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="5f289-124">Protegendo seus aplicativos na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="5f289-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="5f289-125">Protegendo o serviço do SQL Azure na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="5f289-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="5f289-126">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5f289-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="5f289-127">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="5f289-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5f289-128">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="5f289-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="5f289-129">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f289-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
