---
title: "exemplos de configuração de roteador aaaExpressRoute cliente | Microsoft Docs"
description: "Esta página fornece exemplos de configuração do roteador para os roteadores da série Cisco ASA e Juniper."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>Configuração do roteador exemplos tooset backup e gerenciar o roteamento
Esta página fornece interface e modelos de configuração de roteamento para roteadores da série Cisco IOS-XE e Juniper MX. Esses exemplos toobe pretendido para obter orientação apenas e não devem ser usados como está. Você pode trabalhar com seu fornecedor toocome com as configurações apropriadas para sua rede. 

> [!IMPORTANT]
> Os exemplos nesta página são toobe pretendido puramente para obter orientação. Você deve trabalhar com a equipe de vendas / técnico do fornecedor e sua rede toocome de equipe backup com as configurações apropriadas toomeet suas necessidades. A Microsoft não oferecerá suporte para problemas relacionados ao tooconfigurations listados nesta página. Você deve entrar em contato com o fornecedor do dispositivo para problemas de suporte.
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>Configurações de MSS TCP e MTU em interfaces do roteador
* Olá MTU para interface de rota expressa Olá é 1500, Olá típico MTU padrão para uma interface Ethernet em um roteador. A menos que seu roteador tem uma MTU diferente por padrão, há toospecify sem necessidade de um valor na interface do roteador hello.
* Ao contrário de um Gateway de VPN do Azure, Olá MSS TCP para um circuito de rota expressa não precisa toobe especificado.

Exemplos de configuração de roteador abaixo se aplicam a tooall emparelhamentos. Examine [emparelhamentos do ExpressRoute](expressroute-circuit-peerings.md) e [requisitos de roteamento do ExpressRoute](expressroute-routing.md) para obter mais detalhes sobre roteamento.


## <a name="cisco-ios-xe-based-routers"></a>Roteadores com base em Cisco IOS-XE
exemplos de saudação nesta seção se aplica a qualquer roteador executando a família de sistemas operacionais de IOS XE de saudação.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configurando interfaces e sub-interfaces
Você precisará de uma interface sub por emparelhamento em cada roteador conectar tooMicrosoft. Uma interface de sub-rotina pode ser identificada com uma ID de VLAN ou um par empilhado de IDs VLAN e um endereço IP.

**Definição da interface Dot1Q**

Este exemplo fornece a definição de interface subgrupos de saudação para uma interface sub com uma única ID de VLAN. Olá VLAN ID é exclusiva por emparelhamento. último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**Definição da interface QinQ**

Este exemplo fornece uma definição de interface sub Olá para uma interface sub com duas IDs de VLAN. Olá externa VLAN ID (s-tag), se usado permanece Olá iguais em todos os emparelhamentos de saudação. interna Olá ID de VLAN (c-tag) seja exclusiva por emparelhamento. último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2. Configuração das sessões eBGP
Você deve configurar uma sessão BGP com a Microsoft para cada emparelhamento. exemplo Hello abaixo permite que você toosetup uma sessão BGP com a Microsoft. Se Olá endereço IPv4 usado para a sua interface sub a.b.c. d, endereço IP de saudação do vizinho BGP hello (Microsoft) será a.b.c.d+1. último octeto saudação do endereço de IPv4 do vizinho BGP Olá sempre será um número par.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Configuração de toobe prefixos divulgados sessão BGP de saudação
Você pode configurar seu tooMicrosoft do roteador tooadvertise prefixos select. Você pode fazer isso usando Olá exemplo abaixo.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4. Mapas de rotas
Você pode usar mapas de rota e prefixo lista toofilter prefixos propagados em sua rede. Você pode usar o exemplo hello abaixo tooaccomplish tarefa de saudação. Certifique-se de que as listas de prefixo foram configuradas apropriadamente.

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a>Roteadores da série Juniper MX
exemplos de saudação nesta seção se aplicam para os roteadores da série Juniper MX.

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1. Configurando interfaces e sub-interfaces

**Definição da interface Dot1Q**

Este exemplo fornece a definição de interface subgrupos de saudação para uma interface sub com uma única ID de VLAN. Olá VLAN ID é exclusiva por emparelhamento. último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


**Definição da interface QinQ**

Este exemplo fornece uma definição de interface sub Olá para uma interface sub com duas IDs de VLAN. Olá externa VLAN ID (s-tag), se usado permanece Olá iguais em todos os emparelhamentos de saudação. interna Olá ID de VLAN (c-tag) seja exclusiva por emparelhamento. último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a>2. Configuração das sessões eBGP
Você deve configurar uma sessão BGP com a Microsoft para cada emparelhamento. exemplo Hello abaixo permite que você toosetup uma sessão BGP com a Microsoft. Se Olá endereço IPv4 usado para a sua interface sub a.b.c. d, endereço IP de saudação do vizinho BGP hello (Microsoft) será a.b.c.d+1. último octeto saudação do endereço de IPv4 do vizinho BGP Olá sempre será um número par.

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3. Configuração de toobe prefixos divulgados sessão BGP de saudação
Você pode configurar seu tooMicrosoft do roteador tooadvertise prefixos select. Você pode fazer isso usando Olá exemplo abaixo.

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a>4. Mapas de rotas
Você pode usar mapas de rota e prefixo lista toofilter prefixos propagados em sua rede. Você pode usar o exemplo hello abaixo tooaccomplish tarefa de saudação. Certifique-se de que as listas de prefixo foram configuradas apropriadamente.

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a>Próximas etapas
Consulte Olá [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para obter mais detalhes.

