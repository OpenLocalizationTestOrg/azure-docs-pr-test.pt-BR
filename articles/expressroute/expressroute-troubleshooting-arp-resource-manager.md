---
title: "Obtenção de tabelas ARP: Resource Manager: Solução de problemas de ExpressRoute do Azure | Microsoft Docs"
description: "Esta página fornece instruções sobre Olá obtendo ARP tabelas para um circuito de rota expressa"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="27a29-103">Obtendo ARP tabelas no modelo de implantação do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="27a29-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27a29-104">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27a29-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="27a29-105">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="27a29-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="27a29-106">Este artigo orienta Olá Olá de toolearn etapas que ARP tabelas para o circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="27a29-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="27a29-107">Este documento é pretendido toohelp diagnosticar e corrigir problemas simples.</span><span class="sxs-lookup"><span data-stu-id="27a29-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="27a29-108">Não é pretendido toobe uma substituição para o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27a29-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="27a29-109">Você deve abrir um tíquete de suporte com [o suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você estiver toosolve não é possível problema de saudação usando Olá diretrizes descritas abaixo.</span><span class="sxs-lookup"><span data-stu-id="27a29-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="27a29-110">ARP (Protocolo de resolução de endereço) e tabelas ARP</span><span class="sxs-lookup"><span data-stu-id="27a29-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="27a29-111">ARP (Protocolo de resolução de endereço) é um protocolo de camada 2 definido no [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="27a29-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="27a29-112">ARP é usada toomap Olá endereço Ethernet (endereço MAC) com um endereço ip.</span><span class="sxs-lookup"><span data-stu-id="27a29-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="27a29-113">Olá tabela ARP fornece um mapeamento de endereço ipv4 de saudação e o endereço MAC de um emparelhamento particular.</span><span class="sxs-lookup"><span data-stu-id="27a29-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="27a29-114">Olá tabela ARP para um emparelhamento do circuito de rota expressa fornece Olá seguintes informações para cada interface (primário e secundário)</span><span class="sxs-lookup"><span data-stu-id="27a29-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="27a29-115">Mapeamento de endereço de MAC toohello de endereço ip de interface roteador de local</span><span class="sxs-lookup"><span data-stu-id="27a29-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="27a29-116">Mapeamento de endereço de MAC toohello de endereço ip de interface roteador de rota expressa</span><span class="sxs-lookup"><span data-stu-id="27a29-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="27a29-117">Idade de mapeamento de saudação</span><span class="sxs-lookup"><span data-stu-id="27a29-117">Age of hello mapping</span></span>

<span data-ttu-id="27a29-118">As tabelas ARP podem ajudar a validar a configuração da camada 2 e a solucionar problemas básicos de conectividade da camada 2.</span><span class="sxs-lookup"><span data-stu-id="27a29-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="27a29-119">Exemplo de tabela ARP:</span><span class="sxs-lookup"><span data-stu-id="27a29-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="27a29-120">Olá seção a seguir fornece informações sobre como você pode exibir hello tabelas ARP vistas por roteadores de borda de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="27a29-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="27a29-121">Pré-requisitos para o aprendizado de tabelas ARP</span><span class="sxs-lookup"><span data-stu-id="27a29-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="27a29-122">Verifique se você tem Olá a seguir antes de mais de andamento</span><span class="sxs-lookup"><span data-stu-id="27a29-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="27a29-123">Um circuito de ExpressRoute válido configurado com pelo menos um emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="27a29-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="27a29-124">circuito Olá deve ser totalmente configurado pelo provedor de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="27a29-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="27a29-125">Você (ou seu provedor de conectividade) deve ter configurado pelo menos um dos emparelhamentos de saudação (público particular, o Azure do Azure e Microsoft) neste circuito.</span><span class="sxs-lookup"><span data-stu-id="27a29-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="27a29-126">Intervalos de endereços IP usados para configurar os emparelhamentos de saudação (público particular, o Azure do Azure e Microsoft).</span><span class="sxs-lookup"><span data-stu-id="27a29-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="27a29-127">Revisar os exemplos de atribuição de endereços de ip de saudação em Olá [página requisitos de roteamento de rota expressa](expressroute-routing.md) tooget uma compreensão de como os endereços ip são mapeados toointerfaces em seu lado e em Olá lado de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="27a29-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="27a29-128">Para obter informações sobre configuração de emparelhamento Olá revisando Olá [página de configuração de emparelhamento de rota expressa](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="27a29-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="27a29-129">Informações de sua equipe de rede / provedor de conectividade em endereços MAC de saudação de interfaces usados com esses endereços IP.</span><span class="sxs-lookup"><span data-stu-id="27a29-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="27a29-130">Você deve ter o módulo do PowerShell mais recente de saudação do Azure (versão 1.50 ou mais recente).</span><span class="sxs-lookup"><span data-stu-id="27a29-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="27a29-131">Obtendo Olá ARP tabelas para o circuito de rota expressa</span><span class="sxs-lookup"><span data-stu-id="27a29-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="27a29-132">Esta seção fornece instruções sobre como você pode exibir hello tabelas ARP por emparelhamento usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27a29-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="27a29-133">Você ou seu provedor de conectividade deve ter configurado a saudação emparelhamento antes de fazer mais.</span><span class="sxs-lookup"><span data-stu-id="27a29-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="27a29-134">Cada circuito tem dois caminhos (primário e secundário).</span><span class="sxs-lookup"><span data-stu-id="27a29-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="27a29-135">Você pode verificar Olá tabela ARP para cada caminho de forma independente.</span><span class="sxs-lookup"><span data-stu-id="27a29-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="27a29-136">Tabelas ARP para emparelhamento privado do Azure</span><span class="sxs-lookup"><span data-stu-id="27a29-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="27a29-137">Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento particular do Azure</span><span class="sxs-lookup"><span data-stu-id="27a29-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="27a29-138">Saída de exemplo é mostrada abaixo para um dos caminhos de saudação</span><span class="sxs-lookup"><span data-stu-id="27a29-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="27a29-139">Tabelas ARP para emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="27a29-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="27a29-140">Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento público do Azure</span><span class="sxs-lookup"><span data-stu-id="27a29-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="27a29-141">Saída de exemplo é mostrada abaixo para um dos caminhos de saudação</span><span class="sxs-lookup"><span data-stu-id="27a29-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="27a29-142">Tabelas ARP para emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="27a29-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="27a29-143">Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento da Microsoft</span><span class="sxs-lookup"><span data-stu-id="27a29-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="27a29-144">Saída de exemplo é mostrada abaixo para um dos caminhos de saudação</span><span class="sxs-lookup"><span data-stu-id="27a29-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="27a29-145">Como toouse essas informações</span><span class="sxs-lookup"><span data-stu-id="27a29-145">How toouse this information</span></span>
<span data-ttu-id="27a29-146">Olá tabela ARP de um emparelhamento pode ser usada toodetermine validar configuração de camada 2 e conectividade.</span><span class="sxs-lookup"><span data-stu-id="27a29-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="27a29-147">Esta seção fornece uma visão geral da aparência das tabelas ARP em cenários diferentes.</span><span class="sxs-lookup"><span data-stu-id="27a29-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="27a29-148">Tabela ARP quando um circuito está no estado operacional (estado esperado)</span><span class="sxs-lookup"><span data-stu-id="27a29-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="27a29-149">Olá tabela ARP terá uma entrada para o lado do local de saudação com um endereço IP válido e um endereço MAC e uma entrada semelhante para Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27a29-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="27a29-150">último octeto saudação do endereço de ip local Olá sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="27a29-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="27a29-151">sempre o último byte Olá Olá endereço ip da Microsoft será um número par.</span><span class="sxs-lookup"><span data-stu-id="27a29-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="27a29-152">Olá mesmo endereço MAC aparecerá em Olá lado da Microsoft para todos os emparelhamentos de 3 (primários / secundários).</span><span class="sxs-lookup"><span data-stu-id="27a29-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="27a29-153">Tabela de ARP quando o lado do provedor de conectividade/local tiver problemas</span><span class="sxs-lookup"><span data-stu-id="27a29-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="27a29-154">Se houver problemas com hello local ou provedor de conectividade, você pode ver que a apenas uma entrada será exibida no hello endereço de MAC de local de tabela ou saudação de ARP mostrará incompleta.</span><span class="sxs-lookup"><span data-stu-id="27a29-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="27a29-155">Isso mostrará o mapeamento de saudação entre hello endereço MAC e endereço IP usado em Olá lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27a29-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="27a29-156">ou o</span><span class="sxs-lookup"><span data-stu-id="27a29-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="27a29-157">Abra uma solicitação de suporte com o toodebug do provedor de conectividade esses problemas.</span><span class="sxs-lookup"><span data-stu-id="27a29-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="27a29-158">Se não tiver Olá tabela ARP desses endereços IP das interfaces de saudação mapeado tooMAC endereços, Olá revisar informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="27a29-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="27a29-159">Se Olá primeiro endereço IP de sub-rede Olá /30 atribuído para Olá link entre Olá PR MSEE e MSEE é usado na interface de saudação do MSEE pr</span><span class="sxs-lookup"><span data-stu-id="27a29-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="27a29-160">Azure sempre usa o endereço IP da segunda Olá para MSEEs.</span><span class="sxs-lookup"><span data-stu-id="27a29-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="27a29-161">Confirme se Prezado cliente (C-Tag) e marcas de VLAN de serviço (S-Tag) correspondem em par PR MSEE e MSEE.</span><span class="sxs-lookup"><span data-stu-id="27a29-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="27a29-162">Tabela ARP quando o lado da Microsoft apresentar problemas</span><span class="sxs-lookup"><span data-stu-id="27a29-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="27a29-163">Você não verá uma tabela ARP mostrada para um emparelhamento se há problemas no hello lado da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27a29-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="27a29-164">Abra um tíquete com o suporte com o [suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="27a29-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="27a29-165">Especifique que você tem um problema de conectividade de camada 2.</span><span class="sxs-lookup"><span data-stu-id="27a29-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="27a29-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27a29-166">Next Steps</span></span>
* <span data-ttu-id="27a29-167">Validar as configurações de Camada 3 para o circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="27a29-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="27a29-168">Obter o estado de saudação rota toodetermine resumo de sessões BGP</span><span class="sxs-lookup"><span data-stu-id="27a29-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="27a29-169">Obter toodetermine de tabela de rota que prefixos são anunciados pela rota expressa</span><span class="sxs-lookup"><span data-stu-id="27a29-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="27a29-170">Validar a transferência de dados examinando os bytes de entrada/saída</span><span class="sxs-lookup"><span data-stu-id="27a29-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="27a29-171">Abra um tíquete de suporte com o [suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você ainda estiver enfrentando problemas.</span><span class="sxs-lookup"><span data-stu-id="27a29-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

