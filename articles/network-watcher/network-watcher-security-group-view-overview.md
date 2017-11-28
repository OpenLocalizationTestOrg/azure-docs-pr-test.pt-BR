---
title: "exibição de grupo de toosecurity aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral da saudação recurso de exibição de segurança do observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="c59d6-103">Exibição de grupo de segurança Introdução toonetwork no Inspetor de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="c59d6-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="c59d6-104">Os grupos Segurança da Rede podem ser associados no nível da sub-rede ou no nível da NIC.</span><span class="sxs-lookup"><span data-stu-id="c59d6-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="c59d6-105">Quando associado em um nível de sub-rede, ele se aplica a instâncias de VM Olá tooall na sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="c59d6-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="c59d6-106">Exibição de grupo de segurança de rede retorna todos os NSGs Olá configurado e regras associadas em um nível NIC e de sub-rede para uma máquina virtual fornece ideias sobre configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c59d6-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="c59d6-107">Além disso, as regras de segurança efetiva de saudação são retornadas para cada uma das NICs de saudação em uma VM.</span><span class="sxs-lookup"><span data-stu-id="c59d6-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="c59d6-108">Usando a exibição Grupo de Segurança da Rede, você pode avaliar uma VM quanto às vulnerabilidades da rede, como as portas abertas.</span><span class="sxs-lookup"><span data-stu-id="c59d6-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="c59d6-109">Você também pode validar se o grupo de segurança de rede está funcionando conforme o esperado com base em um [comparação entre hello configurado e Olá regras de segurança efetiva](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c59d6-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="c59d6-110">Um caso de uso mais estendido está em conformidade com a segurança e auditoria.</span><span class="sxs-lookup"><span data-stu-id="c59d6-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="c59d6-111">Você pode definir um conjunto prescritivo de regras de segurança como um modelo de controle da segurança em sua organização.</span><span class="sxs-lookup"><span data-stu-id="c59d6-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="c59d6-112">Uma auditoria periódica de conformidade pode ser implementada de forma programática, comparando regras de prescritivas Olá com regras efetivo Olá para cada uma das VMs de saudação em sua rede.</span><span class="sxs-lookup"><span data-stu-id="c59d6-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="c59d6-113">Em Olá portais regras são divididas por efetiva, sub-rede, Interface de rede e padrão.</span><span class="sxs-lookup"><span data-stu-id="c59d6-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="c59d6-114">Isso fornece uma exibição simple na máquina virtual do hello regras aplicadas tooa.</span><span class="sxs-lookup"><span data-stu-id="c59d6-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="c59d6-115">Um botão de download é fornecido tooeasily baixar todas as regras de segurança de hello, independentemente do guia de saudação em um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="c59d6-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![exibição do grupo de segurança][1]

<span data-ttu-id="c59d6-117">As regras podem ser selecionadas e prefixos de grupo de segurança de rede e de origem e de destino de saudação tooshow abre uma nova folha.</span><span class="sxs-lookup"><span data-stu-id="c59d6-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="c59d6-118">Desta folha você pode navegar toohello recurso de grupo de segurança de rede diretamente.</span><span class="sxs-lookup"><span data-stu-id="c59d6-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![busca detalhada][2]

### <a name="next-steps"></a><span data-ttu-id="c59d6-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c59d6-120">Next steps</span></span>

<span data-ttu-id="c59d6-121">Saiba como tooaudit a segurança da rede agrupar configurações visitando [configurações de grupo de segurança de rede de auditoria com o PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c59d6-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









