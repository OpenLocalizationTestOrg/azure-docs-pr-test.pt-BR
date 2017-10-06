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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Obtendo ARP tabelas no modelo de implantação do Gerenciador de recursos de saudação
> [!div class="op_single_selector"]
> * [PowerShell – Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - clássico](expressroute-troubleshooting-arp-classic.md)
> 
> 

Este artigo orienta Olá Olá de toolearn etapas que ARP tabelas para o circuito de rota expressa. 

> [!IMPORTANT]
> Este documento é pretendido toohelp diagnosticar e corrigir problemas simples. Não é pretendido toobe uma substituição para o suporte da Microsoft. Você deve abrir um tíquete de suporte com [o suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você estiver toosolve não é possível problema de saudação usando Olá diretrizes descritas abaixo.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>ARP (Protocolo de resolução de endereço) e tabelas ARP
ARP (Protocolo de resolução de endereço) é um protocolo de camada 2 definido no [RFC 826](https://tools.ietf.org/html/rfc826). ARP é usada toomap Olá endereço Ethernet (endereço MAC) com um endereço ip.

Olá tabela ARP fornece um mapeamento de endereço ipv4 de saudação e o endereço MAC de um emparelhamento particular. Olá tabela ARP para um emparelhamento do circuito de rota expressa fornece Olá seguintes informações para cada interface (primário e secundário)

1. Mapeamento de endereço de MAC toohello de endereço ip de interface roteador de local
2. Mapeamento de endereço de MAC toohello de endereço ip de interface roteador de rota expressa
3. Idade de mapeamento de saudação

As tabelas ARP podem ajudar a validar a configuração da camada 2 e a solucionar problemas básicos de conectividade da camada 2. 

Exemplo de tabela ARP: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Olá seção a seguir fornece informações sobre como você pode exibir hello tabelas ARP vistas por roteadores de borda de rota expressa hello. 

## <a name="prerequisites-for-learning-arp-tables"></a>Pré-requisitos para o aprendizado de tabelas ARP
Verifique se você tem Olá a seguir antes de mais de andamento

* Um circuito de ExpressRoute válido configurado com pelo menos um emparelhamento. circuito Olá deve ser totalmente configurado pelo provedor de conectividade de saudação. Você (ou seu provedor de conectividade) deve ter configurado pelo menos um dos emparelhamentos de saudação (público particular, o Azure do Azure e Microsoft) neste circuito.
* Intervalos de endereços IP usados para configurar os emparelhamentos de saudação (público particular, o Azure do Azure e Microsoft). Revisar os exemplos de atribuição de endereços de ip de saudação em Olá [página requisitos de roteamento de rota expressa](expressroute-routing.md) tooget uma compreensão de como os endereços ip são mapeados toointerfaces em seu lado e em Olá lado de rota expressa. Para obter informações sobre configuração de emparelhamento Olá revisando Olá [página de configuração de emparelhamento de rota expressa](expressroute-howto-routing-arm.md).
* Informações de sua equipe de rede / provedor de conectividade em endereços MAC de saudação de interfaces usados com esses endereços IP.
* Você deve ter o módulo do PowerShell mais recente de saudação do Azure (versão 1.50 ou mais recente).

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Obtendo Olá ARP tabelas para o circuito de rota expressa
Esta seção fornece instruções sobre como você pode exibir hello tabelas ARP por emparelhamento usando o PowerShell. Você ou seu provedor de conectividade deve ter configurado a saudação emparelhamento antes de fazer mais. Cada circuito tem dois caminhos (primário e secundário). Você pode verificar Olá tabela ARP para cada caminho de forma independente.

### <a name="arp-tables-for-azure-private-peering"></a>Tabelas ARP para emparelhamento privado do Azure
Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento particular do Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Saída de exemplo é mostrada abaixo para um dos caminhos de saudação

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tabelas ARP para emparelhamento público do Azure
Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento público do Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Saída de exemplo é mostrada abaixo para um dos caminhos de saudação

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tabelas ARP para emparelhamento da Microsoft
Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento da Microsoft

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Saída de exemplo é mostrada abaixo para um dos caminhos de saudação

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Como toouse essas informações
Olá tabela ARP de um emparelhamento pode ser usada toodetermine validar configuração de camada 2 e conectividade. Esta seção fornece uma visão geral da aparência das tabelas ARP em cenários diferentes.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Tabela ARP quando um circuito está no estado operacional (estado esperado)
* Olá tabela ARP terá uma entrada para o lado do local de saudação com um endereço IP válido e um endereço MAC e uma entrada semelhante para Olá lado da Microsoft. 
* último octeto saudação do endereço de ip local Olá sempre será um número ímpar.
* sempre o último byte Olá Olá endereço ip da Microsoft será um número par.
* Olá mesmo endereço MAC aparecerá em Olá lado da Microsoft para todos os emparelhamentos de 3 (primários / secundários). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>Tabela de ARP quando o lado do provedor de conectividade/local tiver problemas
Se houver problemas com hello local ou provedor de conectividade, você pode ver que a apenas uma entrada será exibida no hello endereço de MAC de local de tabela ou saudação de ARP mostrará incompleta. Isso mostrará o mapeamento de saudação entre hello endereço MAC e endereço IP usado em Olá lado da Microsoft. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

ou o
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Abra uma solicitação de suporte com o toodebug do provedor de conectividade esses problemas. Se não tiver Olá tabela ARP desses endereços IP das interfaces de saudação mapeado tooMAC endereços, Olá revisar informações a seguir:
> 
> 1. Se Olá primeiro endereço IP de sub-rede Olá /30 atribuído para Olá link entre Olá PR MSEE e MSEE é usado na interface de saudação do MSEE pr Azure sempre usa o endereço IP da segunda Olá para MSEEs.
> 2. Confirme se Prezado cliente (C-Tag) e marcas de VLAN de serviço (S-Tag) correspondem em par PR MSEE e MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Tabela ARP quando o lado da Microsoft apresentar problemas
* Você não verá uma tabela ARP mostrada para um emparelhamento se há problemas no hello lado da Microsoft. 
* Abra um tíquete com o suporte com o [suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Especifique que você tem um problema de conectividade de camada 2. 

## <a name="next-steps"></a>Próximas etapas
* Validar as configurações de Camada 3 para o circuito de ExpressRoute
  * Obter o estado de saudação rota toodetermine resumo de sessões BGP 
  * Obter toodetermine de tabela de rota que prefixos são anunciados pela rota expressa
* Validar a transferência de dados examinando os bytes de entrada/saída
* Abra um tíquete de suporte com o [suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você ainda estiver enfrentando problemas.

