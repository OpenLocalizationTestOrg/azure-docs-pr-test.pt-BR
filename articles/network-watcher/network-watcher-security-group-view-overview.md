---
title: "Introdução à exibição do grupo de segurança no Observador de Rede do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral da capacidade de exibição da segurança do Observador de Rede"
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
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="f4808-103">Introdução à exibição do grupo de segurança da rede no Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="f4808-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="f4808-104">Os grupos Segurança da Rede podem ser associados no nível da sub-rede ou no nível da NIC.</span><span class="sxs-lookup"><span data-stu-id="f4808-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="f4808-105">Quando associado no um nível da sub-rede, ele se aplica a todas as instâncias de VM na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f4808-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="f4808-106">A exibição Grupo de Segurança da Rede retorna todo NSG configurado e regras associadas no nível da NIC e da sub-rede para uma máquina virtual que fornece informações sobre a configuração.</span><span class="sxs-lookup"><span data-stu-id="f4808-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="f4808-107">Além disso, as regras de segurança efetivas são retornadas para cada NIC em uma VM.</span><span class="sxs-lookup"><span data-stu-id="f4808-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="f4808-108">Usando a exibição Grupo de Segurança da Rede, você pode avaliar uma VM quanto às vulnerabilidades da rede, como as portas abertas.</span><span class="sxs-lookup"><span data-stu-id="f4808-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="f4808-109">Também é possível validar se o Grupo de Segurança da Rede está funcionando como o esperado com base em uma [comparação entre as regras de segurança configuradas e as efetivas](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f4808-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="f4808-110">Um caso de uso mais estendido está em conformidade com a segurança e auditoria.</span><span class="sxs-lookup"><span data-stu-id="f4808-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="f4808-111">Você pode definir um conjunto prescritivo de regras de segurança como um modelo de controle da segurança em sua organização.</span><span class="sxs-lookup"><span data-stu-id="f4808-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="f4808-112">Uma auditoria de conformidade periódica pode ser implementada de forma programática comparando as regras prescritivas com as regras efetivas para cada uma das VMs em sua rede.</span><span class="sxs-lookup"><span data-stu-id="f4808-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="f4808-113">No portal, as regras são divididas em Efetiva, Sub-rede, Interface de Rede e Padrão.</span><span class="sxs-lookup"><span data-stu-id="f4808-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="f4808-114">Isso fornece uma exibição simples das regras aplicadas em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f4808-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="f4808-115">Um botão de download é fornecido para baixar com facilidade todas as regras de segurança, independentemente da guia em um arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="f4808-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![exibição do grupo de segurança][1]

<span data-ttu-id="f4808-117">As regras podem ser selecionadas e uma nova folha é aberta para mostrar o Grupo de Segurança da Rede e os prefixos de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="f4808-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="f4808-118">Nessa folha, você pode navegar diretamente para o recurso Grupo de Segurança da Rede.</span><span class="sxs-lookup"><span data-stu-id="f4808-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![busca detalhada][2]

### <a name="next-steps"></a><span data-ttu-id="f4808-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4808-120">Next steps</span></span>

<span data-ttu-id="f4808-121">Saiba como fazer a auditoria das configurações do Grupo de Segurança da Rede visitando [Auditar as configurações do Grupo de Segurança da Rede com o PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f4808-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









