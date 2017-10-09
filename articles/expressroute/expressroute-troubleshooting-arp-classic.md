---
title: "Obtenção de tabelas ARP: Clássico: Solução de problemas de ExpressRoute do Azure | Microsoft Docs"
description: "Esta página fornece instruções para obter Olá ARP tabelas para um circuito de rota expressa."
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="7a9c1-103">Obtendo ARP tabelas no modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="7a9c1-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a9c1-104">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a9c1-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="7a9c1-105">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="7a9c1-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="7a9c1-106">Este artigo o orienta pelas etapas de saudação para obtenção de tabelas de protocolo de resolução de endereço (ARP) Olá para o circuito de rota expressa do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a9c1-107">Este documento é pretendido toohelp diagnosticar e corrigir problemas simples.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="7a9c1-108">Não é pretendido toobe uma substituição para o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="7a9c1-109">Se você não conseguir resolver o problema de saudação usando Olá diretrizes a seguir, abra uma solicitação de suporte com [Microsoft Azure ajuda + suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="7a9c1-110">ARP (Protocolo de resolução de endereço) e tabelas ARP</span><span class="sxs-lookup"><span data-stu-id="7a9c1-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="7a9c1-111">ARP é um protocolo de camada 2 definido em [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="7a9c1-112">ARP é toomap usado um endereço IP tooan Ethernet (endereço MAC).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="7a9c1-113">Uma tabela de ARP fornece um mapeamento de endereço IPv4 de saudação e o endereço MAC de um emparelhamento particular.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="7a9c1-114">Olá tabela ARP para um emparelhamento do circuito de rota expressa fornece Olá informações para cada interface (primário e secundário) a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="7a9c1-115">Mapeamento de um endereço de MAC local roteador interface IP endereço tooa</span><span class="sxs-lookup"><span data-stu-id="7a9c1-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="7a9c1-116">Mapeamento de um endereço de MAC rota expressa roteador interface IP endereço tooa</span><span class="sxs-lookup"><span data-stu-id="7a9c1-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="7a9c1-117">idade de saudação do mapeamento de saudação</span><span class="sxs-lookup"><span data-stu-id="7a9c1-117">hello age of hello mapping</span></span>

<span data-ttu-id="7a9c1-118">As tabelas ARP podem ajudar a validar a configuração da camada 2 e a solucionar problemas básicos de conectividade da camada 2.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="7a9c1-119">Segue um exemplo de uma tabela ARP:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="7a9c1-120">Olá seção a seguir fornece informações sobre como tooview Olá tabelas ARP que são vistas por roteadores de borda de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="7a9c1-121">Pré-requisitos para o uso de tabelas ARP</span><span class="sxs-lookup"><span data-stu-id="7a9c1-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="7a9c1-122">Certifique-se de que você tenha a seguinte Olá antes de continuar:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="7a9c1-123">Um circuito de ExpressRoute válido configurado com pelo menos um emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="7a9c1-124">circuito Olá deve ser totalmente configurado pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="7a9c1-125">Você (ou seu provedor de conectividade) deve configurar pelo menos um dos emparelhamentos de saudação (Azure público particular, o Azure ou Microsoft) neste circuito.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="7a9c1-126">Intervalos de endereços IP que são usados para configurar os emparelhamentos de saudação (público particular, o Azure do Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="7a9c1-127">Revisar os exemplos de atribuição de endereços IP de saudação em Olá [página requisitos de roteamento de rota expressa](expressroute-routing.md) tooget uma compreensão de como os endereços IP são mapeados toointerfaces no seu aise e no lado de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="7a9c1-128">Você pode obter informações sobre a configuração de emparelhamento Olá revisando Olá [página de configuração de emparelhamento de rota expressa](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="7a9c1-129">Informações do provedor de equipe ou conectividade de rede sobre endereços MAC de saudação de interfaces de saudação que são usados com esses endereços IP.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="7a9c1-130">Olá módulo mais recente Windows PowerShell do Azure (versão 1,50 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="7a9c1-131">Tabelas ARP para o circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7a9c1-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="7a9c1-132">Esta seção fornece instruções sobre como tooview Olá ARP tabelas para cada tipo de emparelhamento usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="7a9c1-133">Antes de continuar, você ou seu provedor de conectividade precisa tooconfigure Olá emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="7a9c1-134">Cada circuito tem dois caminhos (primário e secundário).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="7a9c1-135">Você pode verificar Olá tabela ARP para cada caminho de forma independente.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="7a9c1-136">Tabelas ARP para emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="7a9c1-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="7a9c1-137">Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento particular do Azure:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="7a9c1-138">O seguinte é um exemplo de saída de um dos caminhos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="7a9c1-139">Tabelas ARP para emparelhamento público do Azure:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="7a9c1-140">Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento público do Azure:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="7a9c1-141">O seguinte é um exemplo de saída de um dos caminhos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="7a9c1-142">O seguinte é um exemplo de saída de um dos caminhos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="7a9c1-143">Tabelas ARP para emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="7a9c1-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="7a9c1-144">Olá cmdlet a seguir fornece Olá ARP tabelas de emparelhamento da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="7a9c1-145">Saída de exemplo é mostrada abaixo para um dos caminhos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="7a9c1-146">Como toouse essas informações</span><span class="sxs-lookup"><span data-stu-id="7a9c1-146">How toouse this information</span></span>
<span data-ttu-id="7a9c1-147">Olá tabela ARP de um emparelhamento pode ser usado toovalidate camada 2 configuração e a conectividade.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="7a9c1-148">Esta seção fornece uma visão geral da aparência das tabelas ARP em cenários diferentes.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="7a9c1-149">Tabela ARP quando um circuito está no estado operacional (esperado)</span><span class="sxs-lookup"><span data-stu-id="7a9c1-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="7a9c1-150">Olá tabela ARP tem uma entrada para o lado do local de saudação com um endereço IP e MAC e uma entrada semelhante para Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="7a9c1-151">último octeto saudação do endereço IP hello local é sempre um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="7a9c1-152">último byte Olá Olá endereço IP da Microsoft é sempre um número par.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="7a9c1-153">Olá mesmo endereço MAC aparece no hello lado da Microsoft para todos os emparelhamentos de três (primário/secundário).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="7a9c1-154">Tabela ARP quando ela é local ou ao lado do provedor de conectividade Olá tem problemas</span><span class="sxs-lookup"><span data-stu-id="7a9c1-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="7a9c1-155">Apenas uma entrada aparece no hello tabela ARP.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="7a9c1-156">Ele mostra o mapeamento de saudação entre o endereço MAC de saudação e o endereço IP de saudação que é usado em saudação do lado do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="7a9c1-157">Se você tiver um problema com isso, abra um suporte solicitá-la com sua tooresolve de provedor de conectividade.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="7a9c1-158">Tabela ARP quando Olá lado Microsoft apresenta problemas</span><span class="sxs-lookup"><span data-stu-id="7a9c1-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="7a9c1-159">Você não verá uma tabela ARP mostrada para um emparelhamento se há problemas no hello lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="7a9c1-160">Abra uma solicitação de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="7a9c1-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="7a9c1-161">Especifique que você tem um problema de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a9c1-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a9c1-162">Next steps</span></span>
* <span data-ttu-id="7a9c1-163">Validar as configurações de Camada 3 para o circuito de ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="7a9c1-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="7a9c1-164">Obter o estado de saudação do resumo toodetermine de rota de sessões BGP.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="7a9c1-165">Obter um toodetermine de tabela de rota que prefixos são anunciados pela rota expressa.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="7a9c1-166">Validar a transferência de dados examinando os bytes de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="7a9c1-167">Abra um tíquete de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você ainda estiver enfrentando problemas.</span><span class="sxs-lookup"><span data-stu-id="7a9c1-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

