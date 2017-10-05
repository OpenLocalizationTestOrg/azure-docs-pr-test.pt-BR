---
title: "Obtenção de tabelas ARP: Clássico: Solução de problemas de ExpressRoute do Azure | Microsoft Docs"
description: "Esta página fornece instruções para obter tabelas ARP para um circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="8700d-103">Obter tabelas ARP no modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="8700d-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8700d-104">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8700d-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="8700d-105">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="8700d-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="8700d-106">Este artigo explica as etapas para obter as tabelas ARP (Address Resolution Protocol, protocolo de resolução de endereço) para o circuito de Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8700d-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8700d-107">Este documento tem como intenção ajudar você a diagnosticar e corrigir problemas simples.</span><span class="sxs-lookup"><span data-stu-id="8700d-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="8700d-108">Ela não deve ser usado como uma substituição ao suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8700d-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="8700d-109">Se você não conseguir resolver o problema usando as diretrizes a seguir, abra uma solicitação de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="8700d-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="8700d-110">ARP (Protocolo de resolução de endereço) e tabelas ARP</span><span class="sxs-lookup"><span data-stu-id="8700d-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="8700d-111">ARP é um protocolo de camada 2 definido em [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="8700d-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="8700d-112">ARP é usado para mapear o endereço de Ethernet (endereço MAC) para um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="8700d-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="8700d-113">A tabela ARP fornece um mapeamento do endereço IPv4 e do endereço MAC para um emparelhamento específico.</span><span class="sxs-lookup"><span data-stu-id="8700d-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="8700d-114">A tabela ARP para um emparelhamento de circuito de ExpressRoute fornece as seguintes informações para cada interface (primária e secundária):</span><span class="sxs-lookup"><span data-stu-id="8700d-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="8700d-115">Mapeamento do endereço IP da interface do roteador local para um endereço MAC</span><span class="sxs-lookup"><span data-stu-id="8700d-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="8700d-116">Mapeamento do endereço IP da interface do roteador de ExpressRoute para um endereço MAC</span><span class="sxs-lookup"><span data-stu-id="8700d-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="8700d-117">Idade do mapeamento</span><span class="sxs-lookup"><span data-stu-id="8700d-117">The age of the mapping</span></span>

<span data-ttu-id="8700d-118">As tabelas ARP podem ajudar a validar a configuração da camada 2 e a solucionar problemas básicos de conectividade da camada 2.</span><span class="sxs-lookup"><span data-stu-id="8700d-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="8700d-119">Segue um exemplo de uma tabela ARP:</span><span class="sxs-lookup"><span data-stu-id="8700d-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="8700d-120">A seção a seguir fornece informações sobre como exibir as tabelas de ARP vistas pelos roteadores de borda de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8700d-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="8700d-121">Pré-requisitos para o uso de tabelas ARP</span><span class="sxs-lookup"><span data-stu-id="8700d-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="8700d-122">Verifique se você tem o seguinte antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="8700d-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="8700d-123">Um circuito de ExpressRoute válido configurado com pelo menos um emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="8700d-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="8700d-124">O circuito deve ser totalmente configurado pelo provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="8700d-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="8700d-125">Você (ou seu provedor de conectividade) deve configurar pelo menos um dos emparelhamentos (particular do Azure, público do Azure ou Microsoft) neste circuito.</span><span class="sxs-lookup"><span data-stu-id="8700d-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="8700d-126">Os intervalos de endereços IP usados para configurar os emparelhamentos (particular do Azure, público do Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="8700d-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="8700d-127">Reveja os exemplos de atribuição de endereço IP na [página de requisitos de roteamento do ExpressRoute](expressroute-routing.md) para entender como os endereços IP são mapeados para interfaces em seu lado e no lado do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8700d-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="8700d-128">Saiba mais sobre a configuração de emparelhamento conferindo a [página de configuração de emparelhamento do ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="8700d-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="8700d-129">Informações de sua equipe de rede ou provedor de conectividade sobre os endereços MAC de interfaces usadas com esses endereços IP.</span><span class="sxs-lookup"><span data-stu-id="8700d-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="8700d-130">O módulo mais recente do Windows PowerShell para Azure (versão 1.50 ou mais recente).</span><span class="sxs-lookup"><span data-stu-id="8700d-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="8700d-131">Tabelas ARP para o circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8700d-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="8700d-132">Esta seção fornece instruções sobre como exibir as tabelas ARP para cada tipo de emparelhamento usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8700d-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="8700d-133">Antes de continuar, você ou seu provedor de conectividade precisa configurar o emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="8700d-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="8700d-134">Cada circuito tem dois caminhos (primário e secundário).</span><span class="sxs-lookup"><span data-stu-id="8700d-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="8700d-135">Você pode verificar a tabela ARP para cada caminho de forma independente.</span><span class="sxs-lookup"><span data-stu-id="8700d-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="8700d-136">Tabelas ARP para emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="8700d-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="8700d-137">O cmdlet a seguir fornece as tabelas ARP para o emparelhamento privado do Azure:</span><span class="sxs-lookup"><span data-stu-id="8700d-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="8700d-138">Veja abaixo um exemplo de saída para um dos caminhos:</span><span class="sxs-lookup"><span data-stu-id="8700d-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="8700d-139">Tabelas ARP para emparelhamento público do Azure:</span><span class="sxs-lookup"><span data-stu-id="8700d-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="8700d-140">O cmdlet a seguir fornece as tabelas ARP para o emparelhamento público do Azure:</span><span class="sxs-lookup"><span data-stu-id="8700d-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="8700d-141">Veja abaixo um exemplo de saída para um dos caminhos:</span><span class="sxs-lookup"><span data-stu-id="8700d-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="8700d-142">Veja abaixo um exemplo de saída para um dos caminhos:</span><span class="sxs-lookup"><span data-stu-id="8700d-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="8700d-143">Tabelas ARP para emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="8700d-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="8700d-144">O cmdlet a seguir fornece as tabelas ARP para o emparelhamento da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="8700d-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="8700d-145">Veja abaixo um exemplo de saída para um dos caminhos:</span><span class="sxs-lookup"><span data-stu-id="8700d-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="8700d-146">Como usar essas informações</span><span class="sxs-lookup"><span data-stu-id="8700d-146">How to use this information</span></span>
<span data-ttu-id="8700d-147">A tabela ARP de um emparelhamento pode ser usada para validar a configuração e a conectividade da camada 2.</span><span class="sxs-lookup"><span data-stu-id="8700d-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="8700d-148">Esta seção fornece uma visão geral da aparência das tabelas ARP em cenários diferentes.</span><span class="sxs-lookup"><span data-stu-id="8700d-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="8700d-149">Tabela ARP quando um circuito está no estado operacional (esperado)</span><span class="sxs-lookup"><span data-stu-id="8700d-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="8700d-150">A tabela ARP tem uma entrada para o lado local com um endereço IP válido e um endereço MAC e uma entrada semelhante para o lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8700d-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="8700d-151">O último octeto do endereço IP local é sempre um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="8700d-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="8700d-152">O último octeto do endereço IP da Microsoft é sempre um número par.</span><span class="sxs-lookup"><span data-stu-id="8700d-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="8700d-153">O mesmo endereço MAC aparece no lado da Microsoft para todos os três emparelhamentos (primário/secundário).</span><span class="sxs-lookup"><span data-stu-id="8700d-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="8700d-154">Tabela ARP quando ela é local ou o lado do provedor de conectividade/local tiver problemas</span><span class="sxs-lookup"><span data-stu-id="8700d-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="8700d-155">Aparece apenas uma entrada na tabela ARP.</span><span class="sxs-lookup"><span data-stu-id="8700d-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="8700d-156">Ela mostra o mapeamento entre o endereço MAC e o endereço IP usado no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8700d-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="8700d-157">Se você tiver um problema assim, abra uma solicitação de suporte com seu provedor de conectividade para resolvê-lo.</span><span class="sxs-lookup"><span data-stu-id="8700d-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="8700d-158">Tabela ARP quando o lado da Microsoft apresentar problemas</span><span class="sxs-lookup"><span data-stu-id="8700d-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="8700d-159">Você não verá uma tabela ARP para um emparelhamento se houver problemas no lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8700d-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="8700d-160">Abra uma solicitação de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="8700d-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="8700d-161">Especifique que você tem um problema de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="8700d-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8700d-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8700d-162">Next steps</span></span>
* <span data-ttu-id="8700d-163">Validar as configurações de Camada 3 para o circuito de ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="8700d-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="8700d-164">Obter um resumo de rota para determinar o estado das sessões BGP.</span><span class="sxs-lookup"><span data-stu-id="8700d-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="8700d-165">Obter uma tabela de rota para determinar quais prefixos são anunciados pelo ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8700d-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="8700d-166">Validar a transferência de dados examinando os bytes de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="8700d-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="8700d-167">Abra um tíquete de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você ainda estiver enfrentando problemas.</span><span class="sxs-lookup"><span data-stu-id="8700d-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

