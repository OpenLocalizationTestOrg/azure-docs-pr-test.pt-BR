---
title: "Visão geral do IPv6 para o Azure Load Balancer | Microsoft Docs"
description: Entender o suporte a IPv6 para o Azure Load Balancer e VMs com balanceamento de carga.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 8cca857314ecf37ef51700fd25aef228515ecd0a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="1fb73-104">Visão geral do IPv6 para o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="1fb73-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="1fb73-105">Balanceadores de carga voltados para a Internet podem ser implantados com um endereço IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="1fb73-106">Além de conectividade IPv4, isso permite os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="1fb73-106">In addition to IPv4 connectivity, this enables the following capabilities:</span></span>

* <span data-ttu-id="1fb73-107">Conectividade IPv6 nativa ponta a ponta entre clientes de Internet pública e VMs (máquinas virtuais) do Azure por meio do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="1fb73-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through the load balancer.</span></span>
* <span data-ttu-id="1fb73-108">Saída IPv6 nativa ponta a ponta entre VMs e clientes habilitados para IPv6 da Internet pública.</span><span class="sxs-lookup"><span data-stu-id="1fb73-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="1fb73-109">A figura a seguir ilustra a funcionalidade do IPv6 para o Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="1fb73-109">The following picture illustrates the IPv6 functionality for Azure Load Balancer.</span></span>

![Azure Load Balancer com IPv6](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="1fb73-111">Uma vez implantado, um cliente de internet habilitado para IPv4 ou IPv6 pode se comunicar com endereços IPv4 ou IPv6 públicos (ou nomes de host) do balanceador de carga voltado para a Internet do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb73-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with the public IPv4 or IPv6 addresses (or hostnames) of the Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="1fb73-112">O balanceador de carga encaminha os pacotes IPv6 para os endereços IPv6 privados das VMs usando a conversão de endereços de rede (NAT).</span><span class="sxs-lookup"><span data-stu-id="1fb73-112">The load balancer routes the IPv6 packets to the private IPv6 addresses of the VMs using network address translation (NAT).</span></span> <span data-ttu-id="1fb73-113">O cliente da Internet IPv6 não pode se comunicar diretamente com o endereço IPv6 das VMs.</span><span class="sxs-lookup"><span data-stu-id="1fb73-113">The IPv6 Internet client cannot communicate directly with the IPv6 address of the VMs.</span></span>

## <a name="features"></a><span data-ttu-id="1fb73-114">Recursos</span><span class="sxs-lookup"><span data-stu-id="1fb73-114">Features</span></span>

<span data-ttu-id="1fb73-115">O suporte nativo a IPv6 para VMs implantadas por meio do Azure Resource Manager fornece:</span><span class="sxs-lookup"><span data-stu-id="1fb73-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="1fb73-116">Serviços de IPv6 com balanceamento de carga para clientes IPv6 na Internet</span><span class="sxs-lookup"><span data-stu-id="1fb73-116">Load-balanced IPv6 services for IPv6 clients on the Internet</span></span>
2. <span data-ttu-id="1fb73-117">Pontos de extremidade IPv4 e IPv6 nativos em VMs ("pilha dupla")</span><span class="sxs-lookup"><span data-stu-id="1fb73-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="1fb73-118">Conexões IPv6 nativas iniciadas por entrada e saída</span><span class="sxs-lookup"><span data-stu-id="1fb73-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="1fb73-119">Protocolos com suporte, como TCP, UDP e HTTP(S), permitem uma ampla gama de arquiteturas de serviço</span><span class="sxs-lookup"><span data-stu-id="1fb73-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="1fb73-120">Benefícios</span><span class="sxs-lookup"><span data-stu-id="1fb73-120">Benefits</span></span>

<span data-ttu-id="1fb73-121">Essa funcionalidade permite os seguintes benefícios principais:</span><span class="sxs-lookup"><span data-stu-id="1fb73-121">This functionality enables the following key benefits:</span></span>

* <span data-ttu-id="1fb73-122">Atender as normas governamentais que exigem que os novos aplicativos sejam acessíveis somente aos clientes IPv6</span><span class="sxs-lookup"><span data-stu-id="1fb73-122">Meet government regulations requiring that new applications be accessible to IPv6-only clients</span></span>
* <span data-ttu-id="1fb73-123">Permitir que desenvolvedores móveis e de IOT (Internet das coisas) usem Máquinas Virtuais do Azure com pilha dupla (IPv4 + IPv6) para atender aos mercados móveis & IOT em expansão</span><span class="sxs-lookup"><span data-stu-id="1fb73-123">Enable mobile and Internet of things (IOT) developers to use dual-stacked (IPv4+IPv6) Azure Virtual Machines to address the growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="1fb73-124">Detalhes e limitações</span><span class="sxs-lookup"><span data-stu-id="1fb73-124">Details and limitations</span></span>

<span data-ttu-id="1fb73-125">Detalhes</span><span class="sxs-lookup"><span data-stu-id="1fb73-125">Details</span></span>

* <span data-ttu-id="1fb73-126">O serviço DNS do Azure contém registros de nome AAAA IPv4 e IPv6 e responde com os dois registros para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="1fb73-126">The Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for the load balancer.</span></span> <span data-ttu-id="1fb73-127">O cliente escolhe com qual endereço (IPv4 ou IPv6) quer se comunicar.</span><span class="sxs-lookup"><span data-stu-id="1fb73-127">The client chooses which address (IPv4 or IPv6) to communicate with.</span></span>
* <span data-ttu-id="1fb73-128">Quando uma VM inicia uma conexão com um dispositivo conectado com a Internet IPv6 pública, o endereço IPv6 de origem da VM é o endereço de rede convertido (NAT) para o endereço IPv6 público do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="1fb73-128">When a VM initiates a connection to a public Internet IPv6-connected device, the VM's source IPv6 address is network address translated (NAT) to the public IPv6 address of the load balancer.</span></span>
* <span data-ttu-id="1fb73-129">As VMs que executam o sistema operacional Linux devem ser configuradas para receber um endereço IP IPv6 por meio de DHCP.</span><span class="sxs-lookup"><span data-stu-id="1fb73-129">VMs running the Linux operating system must be configured to receive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="1fb73-130">Muitas das imagens do Linux na Galeria do Azure já estão configuradas para oferecer suporte a IPv6 sem modificação.</span><span class="sxs-lookup"><span data-stu-id="1fb73-130">Many of the Linux images in the Azure Gallery are already configured to support IPv6 without modification.</span></span> <span data-ttu-id="1fb73-131">Para saber mais, confira [Configuração de DHCPv6 em VMs do Linux](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1fb73-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="1fb73-132">Se você optar por usar uma investigação de integridade com o balanceador de carga, crie uma investigação de IPv4 e use-a com pontos de extremidade IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-132">If you choose to use a health probe with your load balancer, create an IPv4 probe and use it with both the IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="1fb73-133">Se o serviço em sua VM falhar, os pontos de extremidade IPv4 e IPv6 são tirados do rodízio.</span><span class="sxs-lookup"><span data-stu-id="1fb73-133">If the service on your VM goes down, both the IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="1fb73-134">Limitações</span><span class="sxs-lookup"><span data-stu-id="1fb73-134">Limitations</span></span>

* <span data-ttu-id="1fb73-135">Você não pode adicionar regras de balanceamento de carga do IPv6 no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb73-135">You cannot add IPv6 load balancing rules in the Azure portal.</span></span> <span data-ttu-id="1fb73-136">As regras só podem ser criadas por meio de modelo, da CLI e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fb73-136">The rules can only be created through the template, CLI, PowerShell.</span></span>
* <span data-ttu-id="1fb73-137">Você não pode atualizar VMs existentes para usar endereços IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-137">You may not upgrade existing VMs to use IPv6 addresses.</span></span> <span data-ttu-id="1fb73-138">Você deve implantar novas VMs.</span><span class="sxs-lookup"><span data-stu-id="1fb73-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="1fb73-139">Um único endereço IPv6 pode ser atribuído a uma única interface de rede em cada VM.</span><span class="sxs-lookup"><span data-stu-id="1fb73-139">A single IPv6 address can be assigned to a single network interface in each VM.</span></span>
* <span data-ttu-id="1fb73-140">Os endereços IPv6 públicos não podem ser atribuídos a uma VM.</span><span class="sxs-lookup"><span data-stu-id="1fb73-140">The public IPv6 addresses cannot be assigned to a VM.</span></span> <span data-ttu-id="1fb73-141">Eles podem ser atribuídos somente a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="1fb73-141">They can only be assigned to a load balancer.</span></span>
* <span data-ttu-id="1fb73-142">Não é possível configurar a pesquisa reversa de DNS para endereços IPv6 públicos.</span><span class="sxs-lookup"><span data-stu-id="1fb73-142">You cannot configure the reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="1fb73-143">As VMs com os endereços IPv6 não podem ser membros de um Serviço de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fb73-143">The VMs with the IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="1fb73-144">Elas podem ser conectadas a uma Rede Virtual do Azure (VNet) e se comunicarem entre si por meio de seus endereços IPv4.</span><span class="sxs-lookup"><span data-stu-id="1fb73-144">They can be connected to an Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="1fb73-145">Endereços IPv6 privados podem ser implantados em VMs individuais em um grupo de recursos, mas não podem ser implantados em um grupo de recursos por meio de Conjuntos de Escala.</span><span class="sxs-lookup"><span data-stu-id="1fb73-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="1fb73-146">As VMs do Azure não podem se conectar via IPv6 com outras VMs, outros serviços do Azure ou dispositivos locais.</span><span class="sxs-lookup"><span data-stu-id="1fb73-146">Azure VMs cannot connect over IPv6 to other VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="1fb73-147">Eles só podem se comunicar com o Azure Load Balancer via IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-147">They can only communicate with the Azure load balancer over IPv6.</span></span> <span data-ttu-id="1fb73-148">No entanto, elas podem se comunicar com esses outros recursos usando IPv4.</span><span class="sxs-lookup"><span data-stu-id="1fb73-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="1fb73-149">Há suporte para proteção de NSG (grupo de segurança de rede) para IPv4 em implantações de pilha dupla (IPv4+IPv6).</span><span class="sxs-lookup"><span data-stu-id="1fb73-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="1fb73-150">Os NSGs não se aplicam aos pontos de extremidade IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-150">NSGs do not apply to the IPv6 endpoints.</span></span>
* <span data-ttu-id="1fb73-151">O ponto de extremidade IPv6 na VM não é exposto diretamente à internet.</span><span class="sxs-lookup"><span data-stu-id="1fb73-151">The IPv6 endpoint on the VM is not exposed directly to the internet.</span></span> <span data-ttu-id="1fb73-152">Ele fica atrás de um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="1fb73-152">It is behind a load balancer.</span></span> <span data-ttu-id="1fb73-153">Somente as portas especificadas nas regras do balanceador de carga são acessíveis via IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-153">Only the ports specified in the load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="1fb73-154">**No momento, não há suporte** para mudar o parâmetro IdleTimeout para IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-154">Changing the IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="1fb73-155">O padrão é de quatro minutos.</span><span class="sxs-lookup"><span data-stu-id="1fb73-155">The default is four minutes.</span></span>
* <span data-ttu-id="1fb73-156">**No momento, não há suporte** para alterar o parâmetro loadDistributionMethod para IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-156">Changing the loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="1fb73-157">**No momento, não há suporte** para IPs IPv6 reservados (em que IPAllocationMethod = estático).</span><span class="sxs-lookup"><span data-stu-id="1fb73-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fb73-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fb73-158">Next steps</span></span>

<span data-ttu-id="1fb73-159">Saiba como implantar um balanceador de carga com IPv6.</span><span class="sxs-lookup"><span data-stu-id="1fb73-159">Learn how to deploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="1fb73-160">Disponibilidade do IPv6 por região</span><span class="sxs-lookup"><span data-stu-id="1fb73-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="1fb73-161">Implantar um balanceador de carga com IPv6 usando um modelo</span><span class="sxs-lookup"><span data-stu-id="1fb73-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="1fb73-162">Implantar um balanceador de carga com IPv6 usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fb73-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="1fb73-163">Implantar um balanceador de carga com IPv6 usando CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1fb73-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
