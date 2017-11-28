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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="e8397-103">Configuração do roteador exemplos tooset backup e gerenciar o roteamento</span><span class="sxs-lookup"><span data-stu-id="e8397-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="e8397-104">Esta página fornece interface e modelos de configuração de roteamento para roteadores da série Cisco IOS-XE e Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="e8397-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="e8397-105">Esses exemplos toobe pretendido para obter orientação apenas e não devem ser usados como está.</span><span class="sxs-lookup"><span data-stu-id="e8397-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="e8397-106">Você pode trabalhar com seu fornecedor toocome com as configurações apropriadas para sua rede.</span><span class="sxs-lookup"><span data-stu-id="e8397-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e8397-107">Os exemplos nesta página são toobe pretendido puramente para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="e8397-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="e8397-108">Você deve trabalhar com a equipe de vendas / técnico do fornecedor e sua rede toocome de equipe backup com as configurações apropriadas toomeet suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="e8397-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="e8397-109">A Microsoft não oferecerá suporte para problemas relacionados ao tooconfigurations listados nesta página.</span><span class="sxs-lookup"><span data-stu-id="e8397-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="e8397-110">Você deve entrar em contato com o fornecedor do dispositivo para problemas de suporte.</span><span class="sxs-lookup"><span data-stu-id="e8397-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="e8397-111">Configurações de MSS TCP e MTU em interfaces do roteador</span><span class="sxs-lookup"><span data-stu-id="e8397-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="e8397-112">Olá MTU para interface de rota expressa Olá é 1500, Olá típico MTU padrão para uma interface Ethernet em um roteador.</span><span class="sxs-lookup"><span data-stu-id="e8397-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="e8397-113">A menos que seu roteador tem uma MTU diferente por padrão, há toospecify sem necessidade de um valor na interface do roteador hello.</span><span class="sxs-lookup"><span data-stu-id="e8397-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="e8397-114">Ao contrário de um Gateway de VPN do Azure, Olá MSS TCP para um circuito de rota expressa não precisa toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="e8397-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="e8397-115">Exemplos de configuração de roteador abaixo se aplicam a tooall emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="e8397-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="e8397-116">Examine [emparelhamentos do ExpressRoute](expressroute-circuit-peerings.md) e [requisitos de roteamento do ExpressRoute](expressroute-routing.md) para obter mais detalhes sobre roteamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="e8397-117">Roteadores com base em Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="e8397-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="e8397-118">exemplos de saudação nesta seção se aplica a qualquer roteador executando a família de sistemas operacionais de IOS XE de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8397-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="e8397-119">1. Configurando interfaces e sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="e8397-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="e8397-120">Você precisará de uma interface sub por emparelhamento em cada roteador conectar tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="e8397-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="e8397-121">Uma interface de sub-rotina pode ser identificada com uma ID de VLAN ou um par empilhado de IDs VLAN e um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e8397-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="e8397-122">**Definição da interface Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="e8397-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="e8397-123">Este exemplo fornece a definição de interface subgrupos de saudação para uma interface sub com uma única ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="e8397-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="e8397-124">Olá VLAN ID é exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="e8397-125">último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="e8397-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="e8397-126">**Definição da interface QinQ**</span><span class="sxs-lookup"><span data-stu-id="e8397-126">**QinQ interface definition**</span></span>

<span data-ttu-id="e8397-127">Este exemplo fornece uma definição de interface sub Olá para uma interface sub com duas IDs de VLAN.</span><span class="sxs-lookup"><span data-stu-id="e8397-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="e8397-128">Olá externa VLAN ID (s-tag), se usado permanece Olá iguais em todos os emparelhamentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8397-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="e8397-129">interna Olá ID de VLAN (c-tag) seja exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="e8397-130">último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="e8397-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="e8397-131">2. Configuração das sessões eBGP</span><span class="sxs-lookup"><span data-stu-id="e8397-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="e8397-132">Você deve configurar uma sessão BGP com a Microsoft para cada emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="e8397-133">exemplo Hello abaixo permite que você toosetup uma sessão BGP com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e8397-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="e8397-134">Se Olá endereço IPv4 usado para a sua interface sub a.b.c. d, endereço IP de saudação do vizinho BGP hello (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="e8397-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="e8397-135">último octeto saudação do endereço de IPv4 do vizinho BGP Olá sempre será um número par.</span><span class="sxs-lookup"><span data-stu-id="e8397-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="e8397-136">3. Configuração de toobe prefixos divulgados sessão BGP de saudação</span><span class="sxs-lookup"><span data-stu-id="e8397-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="e8397-137">Você pode configurar seu tooMicrosoft do roteador tooadvertise prefixos select.</span><span class="sxs-lookup"><span data-stu-id="e8397-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="e8397-138">Você pode fazer isso usando Olá exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="e8397-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="e8397-139">4. Mapas de rotas</span><span class="sxs-lookup"><span data-stu-id="e8397-139">4. Route maps</span></span>
<span data-ttu-id="e8397-140">Você pode usar mapas de rota e prefixo lista toofilter prefixos propagados em sua rede.</span><span class="sxs-lookup"><span data-stu-id="e8397-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="e8397-141">Você pode usar o exemplo hello abaixo tooaccomplish tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8397-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="e8397-142">Certifique-se de que as listas de prefixo foram configuradas apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="e8397-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="e8397-143">Roteadores da série Juniper MX</span><span class="sxs-lookup"><span data-stu-id="e8397-143">Juniper MX series routers</span></span>
<span data-ttu-id="e8397-144">exemplos de saudação nesta seção se aplicam para os roteadores da série Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="e8397-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="e8397-145">1. Configurando interfaces e sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="e8397-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="e8397-146">**Definição da interface Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="e8397-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="e8397-147">Este exemplo fornece a definição de interface subgrupos de saudação para uma interface sub com uma única ID de VLAN.</span><span class="sxs-lookup"><span data-stu-id="e8397-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="e8397-148">Olá VLAN ID é exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="e8397-149">último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="e8397-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="e8397-150">**Definição da interface QinQ**</span><span class="sxs-lookup"><span data-stu-id="e8397-150">**QinQ interface definition**</span></span>

<span data-ttu-id="e8397-151">Este exemplo fornece uma definição de interface sub Olá para uma interface sub com duas IDs de VLAN.</span><span class="sxs-lookup"><span data-stu-id="e8397-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="e8397-152">Olá externa VLAN ID (s-tag), se usado permanece Olá iguais em todos os emparelhamentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8397-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="e8397-153">interna Olá ID de VLAN (c-tag) seja exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="e8397-154">último octeto saudação de seu endereço de IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="e8397-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="e8397-155">2. Configuração das sessões eBGP</span><span class="sxs-lookup"><span data-stu-id="e8397-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="e8397-156">Você deve configurar uma sessão BGP com a Microsoft para cada emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="e8397-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="e8397-157">exemplo Hello abaixo permite que você toosetup uma sessão BGP com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e8397-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="e8397-158">Se Olá endereço IPv4 usado para a sua interface sub a.b.c. d, endereço IP de saudação do vizinho BGP hello (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="e8397-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="e8397-159">último octeto saudação do endereço de IPv4 do vizinho BGP Olá sempre será um número par.</span><span class="sxs-lookup"><span data-stu-id="e8397-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="e8397-160">3. Configuração de toobe prefixos divulgados sessão BGP de saudação</span><span class="sxs-lookup"><span data-stu-id="e8397-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="e8397-161">Você pode configurar seu tooMicrosoft do roteador tooadvertise prefixos select.</span><span class="sxs-lookup"><span data-stu-id="e8397-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="e8397-162">Você pode fazer isso usando Olá exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="e8397-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="e8397-163">4. Mapas de rotas</span><span class="sxs-lookup"><span data-stu-id="e8397-163">4. Route maps</span></span>
<span data-ttu-id="e8397-164">Você pode usar mapas de rota e prefixo lista toofilter prefixos propagados em sua rede.</span><span class="sxs-lookup"><span data-stu-id="e8397-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="e8397-165">Você pode usar o exemplo hello abaixo tooaccomplish tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8397-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="e8397-166">Certifique-se de que as listas de prefixo foram configuradas apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="e8397-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e8397-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8397-167">Next Steps</span></span>
<span data-ttu-id="e8397-168">Consulte Olá [perguntas frequentes sobre o rota expressa](expressroute-faqs.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e8397-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

