---
title: Suporte do Azure Resource Manager para o Balanceador de Carga | Microsoft Docs
description: Usando o powershell do Load Balancer com o Azure Resource Manager. Usando modelos de balanceador de carga
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="f441b-104">Usando o suporte do Azure Resource Manager com o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="f441b-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="f441b-105">O Azure Resource Manager é a estrutura de gerenciamento preferida dos serviços no Azure.</span><span class="sxs-lookup"><span data-stu-id="f441b-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="f441b-106">O Azure Load Balancer pode ser gerenciado usando ferramentas e APIs baseadas no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f441b-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="f441b-107">Conceitos</span><span class="sxs-lookup"><span data-stu-id="f441b-107">Concepts</span></span>

<span data-ttu-id="f441b-108">Com Resource Manager, o Azure Load Balancer contém os recursos filho a seguir:</span><span class="sxs-lookup"><span data-stu-id="f441b-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="f441b-109">Configuração de IP front-end – um balanceador de carga pode incluir um ou mais endereços IP front-end, também conhecidos como VIPs (IPs virtuais).</span><span class="sxs-lookup"><span data-stu-id="f441b-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="f441b-110">Esses endereços IP servem como entrada para o tráfego.</span><span class="sxs-lookup"><span data-stu-id="f441b-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="f441b-111">Pool de endereços back-end – são endereços IP associados a NIC (Placa de Interface de Rede) de máquina virtual nos quais a carga será distribuída.</span><span class="sxs-lookup"><span data-stu-id="f441b-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="f441b-112">Regras de balanceamento de carga – uma propriedade de regra mapeia determinada combinação de porta e IP front-end para um conjunto de endereços IP back-end e combinação de portas.</span><span class="sxs-lookup"><span data-stu-id="f441b-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="f441b-113">Um balanceador de carga único pode ter várias regras de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="f441b-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="f441b-114">Cada regra é uma combinação de um IP de front-end e IP de porta e back-end e porta associada a VMs.</span><span class="sxs-lookup"><span data-stu-id="f441b-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="f441b-115">Investigações – as investigações permitem que você controle a integridade das instâncias VM.</span><span class="sxs-lookup"><span data-stu-id="f441b-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="f441b-116">Se um teste de integridade falhar, a instância VM será retirada automaticamente do rodízio.</span><span class="sxs-lookup"><span data-stu-id="f441b-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="f441b-117">Regras NAT de entrada – regras NAT definem o tráfego de entrada que flui pelo IP front-end e é distribuído para o IP back-end.</span><span class="sxs-lookup"><span data-stu-id="f441b-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="f441b-118">Modelos de início rápido</span><span class="sxs-lookup"><span data-stu-id="f441b-118">Quickstart templates</span></span>

<span data-ttu-id="f441b-119">O Gerenciador de Recursos do Azure permite que você provisione seus aplicativos usando um modelo declarativo.</span><span class="sxs-lookup"><span data-stu-id="f441b-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="f441b-120">Em um modelo único, você pode implantar vários serviços, juntamente com suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f441b-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="f441b-121">Use o mesmo modelo para implantar repetidamente seu aplicativo durante cada estágio do ciclo de vida do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f441b-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="f441b-122">Modelos podem incluir definições para máquinas virtuais, redes virtuais, conjuntos de disponibilidade, NICs (Interfaces de Rede), contas de armazenamento, balanceadores de carga, grupos de segurança de rede e IPs públicos.</span><span class="sxs-lookup"><span data-stu-id="f441b-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="f441b-123">Com os modelos, você pode criar tudo o que precisa para um aplicativo complexo.</span><span class="sxs-lookup"><span data-stu-id="f441b-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="f441b-124">O arquivo de modelo pode ser inserido no sistema de gerenciamento de conteúdo para controle de versão e colaboração.</span><span class="sxs-lookup"><span data-stu-id="f441b-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="f441b-125">Saiba mais sobre modelos</span><span class="sxs-lookup"><span data-stu-id="f441b-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="f441b-126">Saiba mais sobre recursos de rede</span><span class="sxs-lookup"><span data-stu-id="f441b-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="f441b-127">Modelos de início rápido que usam o Azure Load Balancer podem ser encontrados em um [repositório GitHub](https://github.com/Azure/azure-quickstart-templates) que hospeda um conjunto de modelos gerados pela comunidade.</span><span class="sxs-lookup"><span data-stu-id="f441b-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="f441b-128">Exemplos de modelos:</span><span class="sxs-lookup"><span data-stu-id="f441b-128">Examples of templates:</span></span>

* [<span data-ttu-id="f441b-129">2 VMs em um balanceador de carga e regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="f441b-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="f441b-130">2 VMs em uma VNET com as regras de um balanceador de carga interno e regras do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f441b-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="f441b-131">2 VMs em um balanceador de carga e regras NAT configuradas no balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f441b-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="f441b-132">Configurando o balanceador de carga do Azure com PowerShell ou CLI</span><span class="sxs-lookup"><span data-stu-id="f441b-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="f441b-133">Introdução aos cmdlets do Azure Resource Manager, ferramentas de linha de comando e APIs REST</span><span class="sxs-lookup"><span data-stu-id="f441b-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="f441b-134">[Cmdlets de rede do Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) podem ser usados para criar um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f441b-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="f441b-135">Como criar um balanceador de carga usando o gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="f441b-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="f441b-136">Usando a CLI do Azure com o gerenciamento de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="f441b-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="f441b-137">APIs REST do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="f441b-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="f441b-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f441b-138">Next steps</span></span>

<span data-ttu-id="f441b-139">Também é possível [começar a criar um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md) e configurar que tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f441b-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="f441b-140">Saiba como gerenciar [tempo limite de TCP ocioso para um balanceador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="f441b-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="f441b-141">Isso será importante quando seu aplicativo precisar manter conexões ativas para servidores atrás de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="f441b-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
