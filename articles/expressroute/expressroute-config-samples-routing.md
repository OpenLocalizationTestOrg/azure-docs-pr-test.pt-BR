---
title: "Exemplos de configuração do roteador do cliente ExpressRoute | Microsoft Docs"
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
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="ffa91-103">Exemplos de configuração do roteador para configurar e gerenciar o roteamento</span><span class="sxs-lookup"><span data-stu-id="ffa91-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="ffa91-104">Esta página fornece interface e modelos de configuração de roteamento para roteadores da série Cisco IOS-XE e Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="ffa91-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="ffa91-105">Devem ser exemplos para obter orientação apenas e não devem ser usados como estão.</span><span class="sxs-lookup"><span data-stu-id="ffa91-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="ffa91-106">Você pode trabalhar com o fornecedor para exibir as configurações apropriadas para sua rede.</span><span class="sxs-lookup"><span data-stu-id="ffa91-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ffa91-107">Exemplos nesta página devem ser exclusivamente para obter orientação.</span><span class="sxs-lookup"><span data-stu-id="ffa91-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="ffa91-108">Trabalhe com a equipe de vendas / equipe técnica e sua equipe de rede para exibir as configurações adequadas para atendar às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ffa91-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="ffa91-109">A Microsoft não oferecerá suporte a problemas relacionados a configurações listadas nesta página.</span><span class="sxs-lookup"><span data-stu-id="ffa91-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="ffa91-110">Você deve entrar em contato com o fornecedor do dispositivo para problemas de suporte.</span><span class="sxs-lookup"><span data-stu-id="ffa91-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="ffa91-111">Configurações de MSS TCP e MTU em interfaces do roteador</span><span class="sxs-lookup"><span data-stu-id="ffa91-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="ffa91-112">A MTU para a interface do ExpressRoute é 1500, que é a MTU padrão típica para uma interface Ethernet em um roteador.</span><span class="sxs-lookup"><span data-stu-id="ffa91-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="ffa91-113">A menos que seu roteador tenha uma MTU diferente por padrão, não é necessário especificar um valor na interface do roteador.</span><span class="sxs-lookup"><span data-stu-id="ffa91-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="ffa91-114">Ao contrário de um Gateway de VPN do Azure, o MSS TCP para um circuito ExpressRoute não precisa ser especificado.</span><span class="sxs-lookup"><span data-stu-id="ffa91-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="ffa91-115">Os modelos de configuração abaixo se aplicam a todos os emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="ffa91-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="ffa91-116">Examine [emparelhamentos do ExpressRoute](expressroute-circuit-peerings.md) e [requisitos de roteamento do ExpressRoute](expressroute-routing.md) para obter mais detalhes sobre roteamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="ffa91-117">Roteadores com base em Cisco IOS-XE</span><span class="sxs-lookup"><span data-stu-id="ffa91-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="ffa91-118">Os modelos nesta seção se aplicam a qualquer roteador que esteja executando a família de sistemas operacionais IOS XE.</span><span class="sxs-lookup"><span data-stu-id="ffa91-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="ffa91-119">1. Configurando interfaces e sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="ffa91-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="ffa91-120">Você precisará de uma sub interface por emparelhamento em cada roteador, que o conecte à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffa91-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="ffa91-121">Uma interface de sub-rotina pode ser identificada com uma ID de VLAN ou um par empilhado de IDs VLAN e um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ffa91-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="ffa91-122">**Definição da interface Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="ffa91-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="ffa91-123">Este exemplo fornece a definição de sub-interface para a sub-interface com uma ID de VLAN única.</span><span class="sxs-lookup"><span data-stu-id="ffa91-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="ffa91-124">A ID de VLAN é exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="ffa91-125">O último octeto de seu endereço IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="ffa91-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="ffa91-126">**Definição da interface QinQ**</span><span class="sxs-lookup"><span data-stu-id="ffa91-126">**QinQ interface definition**</span></span>

<span data-ttu-id="ffa91-127">Este exemplo fornece a definição de sub-interface para a sub-interface com duas IDs de VLAN única.</span><span class="sxs-lookup"><span data-stu-id="ffa91-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="ffa91-128">ID da VLAN externa (s-tag), se usada permanece a mesma em todos os emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="ffa91-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="ffa91-129">A ID de VLAN interna (marca c) é exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="ffa91-130">O último octeto de seu endereço IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="ffa91-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="ffa91-131">2. Configuração das sessões eBGP</span><span class="sxs-lookup"><span data-stu-id="ffa91-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="ffa91-132">Você deve configurar uma sessão BGP com a Microsoft para cada emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="ffa91-133">O exemplo a seguir lhe permite configurar uma sessão BGP com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffa91-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="ffa91-134">Se o endereço IPv4 usado para a sua sub interface era a.b.c. d, o endereço IP do vizinho BGP (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="ffa91-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="ffa91-135">O último octeto do endereço de IPv4 do vizinho BGP sempre será um número par.</span><span class="sxs-lookup"><span data-stu-id="ffa91-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="ffa91-136">3. Configurando os prefixos anunciados sobre a sessão BGP</span><span class="sxs-lookup"><span data-stu-id="ffa91-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="ffa91-137">Você pode configurar seu roteador para anunciar prefixos selecionados para a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffa91-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="ffa91-138">Você pode fazer isso usando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ffa91-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="ffa91-139">4. Mapas de rotas</span><span class="sxs-lookup"><span data-stu-id="ffa91-139">4. Route maps</span></span>
<span data-ttu-id="ffa91-140">Você pode usar mapas de rotas e listas de prefixo para prefixos de filtro propagados em sua rede.</span><span class="sxs-lookup"><span data-stu-id="ffa91-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="ffa91-141">Você pode usar o exemplo a seguir para realizar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="ffa91-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="ffa91-142">Certifique-se de que as listas de prefixo foram configuradas apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="ffa91-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="ffa91-143">Roteadores da série Juniper MX</span><span class="sxs-lookup"><span data-stu-id="ffa91-143">Juniper MX series routers</span></span>
<span data-ttu-id="ffa91-144">Os exemplos nesta seção se aplicam aos os roteadores da série Juniper MX.</span><span class="sxs-lookup"><span data-stu-id="ffa91-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="ffa91-145">1. Configurando interfaces e sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="ffa91-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="ffa91-146">**Definição da interface Dot1Q**</span><span class="sxs-lookup"><span data-stu-id="ffa91-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="ffa91-147">Este exemplo fornece a definição de sub-interface para a sub-interface com uma ID de VLAN única.</span><span class="sxs-lookup"><span data-stu-id="ffa91-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="ffa91-148">A ID de VLAN é exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="ffa91-149">O último octeto de seu endereço IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="ffa91-149">The last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="ffa91-150">**Definição da interface QinQ**</span><span class="sxs-lookup"><span data-stu-id="ffa91-150">**QinQ interface definition**</span></span>

<span data-ttu-id="ffa91-151">Este exemplo fornece a definição de sub-interface para a sub-interface com duas IDs de VLAN única.</span><span class="sxs-lookup"><span data-stu-id="ffa91-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="ffa91-152">ID da VLAN externa (s-tag), se usada permanece a mesma em todos os emparelhamentos.</span><span class="sxs-lookup"><span data-stu-id="ffa91-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="ffa91-153">A ID de VLAN interna (marca c) é exclusiva por emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="ffa91-154">O último octeto de seu endereço IPv4 sempre será um número ímpar.</span><span class="sxs-lookup"><span data-stu-id="ffa91-154">The last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="ffa91-155">2. Configuração das sessões eBGP</span><span class="sxs-lookup"><span data-stu-id="ffa91-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="ffa91-156">Você deve configurar uma sessão BGP com a Microsoft para cada emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="ffa91-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="ffa91-157">O exemplo a seguir lhe permite configurar uma sessão BGP com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffa91-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="ffa91-158">Se o endereço IPv4 usado para a sua sub interface era a.b.c. d, o endereço IP do vizinho BGP (Microsoft) será a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="ffa91-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="ffa91-159">O último octeto do endereço de IPv4 do vizinho BGP sempre será um número par.</span><span class="sxs-lookup"><span data-stu-id="ffa91-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="ffa91-160">3. Configurando os prefixos anunciados sobre a sessão BGP</span><span class="sxs-lookup"><span data-stu-id="ffa91-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="ffa91-161">Você pode configurar seu roteador para anunciar prefixos selecionados para a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffa91-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="ffa91-162">Você pode fazer isso usando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ffa91-162">You can do so using the sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="ffa91-163">4. Mapas de rotas</span><span class="sxs-lookup"><span data-stu-id="ffa91-163">4. Route maps</span></span>
<span data-ttu-id="ffa91-164">Você pode usar mapas de rotas e listas de prefixo para prefixos de filtro propagados em sua rede.</span><span class="sxs-lookup"><span data-stu-id="ffa91-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="ffa91-165">Você pode usar o exemplo a seguir para realizar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="ffa91-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="ffa91-166">Certifique-se de que as listas de prefixo foram configuradas apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="ffa91-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ffa91-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ffa91-167">Next Steps</span></span>
<span data-ttu-id="ffa91-168">Consulte as [Perguntas Frequentes sobre ExpressRoute](expressroute-faqs.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ffa91-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

