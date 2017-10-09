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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>Obtendo ARP tabelas no modelo de implantação clássico Olá
> [!div class="op_single_selector"]
> * [PowerShell – Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - clássico](expressroute-troubleshooting-arp-classic.md)
> 
> 

Este artigo o orienta pelas etapas de saudação para obtenção de tabelas de protocolo de resolução de endereço (ARP) Olá para o circuito de rota expressa do Azure.

> [!IMPORTANT]
> Este documento é pretendido toohelp diagnosticar e corrigir problemas simples. Não é pretendido toobe uma substituição para o suporte da Microsoft. Se você não conseguir resolver o problema de saudação usando Olá diretrizes a seguir, abra uma solicitação de suporte com [Microsoft Azure ajuda + suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>ARP (Protocolo de resolução de endereço) e tabelas ARP
ARP é um protocolo de camada 2 definido em [RFC 826](https://tools.ietf.org/html/rfc826). ARP é toomap usado um endereço IP tooan Ethernet (endereço MAC).

Uma tabela de ARP fornece um mapeamento de endereço IPv4 de saudação e o endereço MAC de um emparelhamento particular. Olá tabela ARP para um emparelhamento do circuito de rota expressa fornece Olá informações para cada interface (primário e secundário) a seguir:

1. Mapeamento de um endereço de MAC local roteador interface IP endereço tooa
2. Mapeamento de um endereço de MAC rota expressa roteador interface IP endereço tooa
3. idade de saudação do mapeamento de saudação

As tabelas ARP podem ajudar a validar a configuração da camada 2 e a solucionar problemas básicos de conectividade da camada 2.

Segue um exemplo de uma tabela ARP:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Olá seção a seguir fornece informações sobre como tooview Olá tabelas ARP que são vistas por roteadores de borda de rota expressa hello.

## <a name="prerequisites-for-using-arp-tables"></a>Pré-requisitos para o uso de tabelas ARP
Certifique-se de que você tenha a seguinte Olá antes de continuar:

* Um circuito de ExpressRoute válido configurado com pelo menos um emparelhamento. circuito Olá deve ser totalmente configurado pelo provedor de conectividade de saudação. Você (ou seu provedor de conectividade) deve configurar pelo menos um dos emparelhamentos de saudação (Azure público particular, o Azure ou Microsoft) neste circuito.
* Intervalos de endereços IP que são usados para configurar os emparelhamentos de saudação (público particular, o Azure do Azure e Microsoft). Revisar os exemplos de atribuição de endereços IP de saudação em Olá [página requisitos de roteamento de rota expressa](expressroute-routing.md) tooget uma compreensão de como os endereços IP são mapeados toointerfaces no seu aise e no lado de rota expressa hello. Você pode obter informações sobre a configuração de emparelhamento Olá revisando Olá [página de configuração de emparelhamento de rota expressa](expressroute-howto-routing-classic.md).
* Informações do provedor de equipe ou conectividade de rede sobre endereços MAC de saudação de interfaces de saudação que são usados com esses endereços IP.
* Olá módulo mais recente Windows PowerShell do Azure (versão 1,50 ou posterior).

## <a name="arp-tables-for-your-expressroute-circuit"></a>Tabelas ARP para o circuito de ExpressRoute
Esta seção fornece instruções sobre como tooview Olá ARP tabelas para cada tipo de emparelhamento usando o PowerShell. Antes de continuar, você ou seu provedor de conectividade precisa tooconfigure Olá emparelhamento. Cada circuito tem dois caminhos (primário e secundário). Você pode verificar Olá tabela ARP para cada caminho de forma independente.

### <a name="arp-tables-for-azure-private-peering"></a>Tabelas ARP para emparelhamento privado do Azure
Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento particular do Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

O seguinte é um exemplo de saída de um dos caminhos de saudação:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tabelas ARP para emparelhamento público do Azure:
Olá cmdlet a seguir fornece Olá ARP tabelas para emparelhamento público do Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

O seguinte é um exemplo de saída de um dos caminhos de saudação:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


O seguinte é um exemplo de saída de um dos caminhos de saudação:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tabelas ARP para emparelhamento da Microsoft
Olá cmdlet a seguir fornece Olá ARP tabelas de emparelhamento da Microsoft:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Saída de exemplo é mostrada abaixo para um dos caminhos de saudação:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Como toouse essas informações
Olá tabela ARP de um emparelhamento pode ser usado toovalidate camada 2 configuração e a conectividade. Esta seção fornece uma visão geral da aparência das tabelas ARP em cenários diferentes.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>Tabela ARP quando um circuito está no estado operacional (esperado)
* Olá tabela ARP tem uma entrada para o lado do local de saudação com um endereço IP e MAC e uma entrada semelhante para Olá lado da Microsoft.
* último octeto saudação do endereço IP hello local é sempre um número ímpar.
* último byte Olá Olá endereço IP da Microsoft é sempre um número par.
* Olá mesmo endereço MAC aparece no hello lado da Microsoft para todos os emparelhamentos de três (primário/secundário).

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Tabela ARP quando ela é local ou ao lado do provedor de conectividade Olá tem problemas
 Apenas uma entrada aparece no hello tabela ARP. Ele mostra o mapeamento de saudação entre o endereço MAC de saudação e o endereço IP de saudação que é usado em saudação do lado do Microsoft.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Se você tiver um problema com isso, abra um suporte solicitá-la com sua tooresolve de provedor de conectividade.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Tabela ARP quando Olá lado Microsoft apresenta problemas
* Você não verá uma tabela ARP mostrada para um emparelhamento se há problemas no hello lado da Microsoft.
* Abra uma solicitação de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Especifique que você tem um problema de conectividade de camada 2.

## <a name="next-steps"></a>Próximas etapas
* Validar as configurações de Camada 3 para o circuito de ExpressRoute:
  * Obter o estado de saudação do resumo toodetermine de rota de sessões BGP.
  * Obter um toodetermine de tabela de rota que prefixos são anunciados pela rota expressa.
* Validar a transferência de dados examinando os bytes de entrada e saída.
* Abra um tíquete de suporte com a [Ajuda + suporte do Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) se você ainda estiver enfrentando problemas.

