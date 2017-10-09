---
title: "configuração aaaSample - dispositivo Cisco ASA conectar gateways de VPN tooAzure | Microsoft Docs"
description: "Este artigo fornece um exemplo de configuração de dispositivo Cisco ASA conectando tooAzure gateways de VPN."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="c6ad9-103">Exemplo de configuração: dispositivo Cisco ASA (IKEv2/não BGP)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="c6ad9-104">Este artigo fornece exemplos de configurações para dispositivos Cisco ASA conectando tooAzure gateways de VPN.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="c6ad9-105">Visão rápida do dispositivo</span><span class="sxs-lookup"><span data-stu-id="c6ad9-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="c6ad9-106">Fornecedor do dispositivo</span><span class="sxs-lookup"><span data-stu-id="c6ad9-106">Device vendor</span></span>          | <span data-ttu-id="c6ad9-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="c6ad9-107">Cisco</span></span>                             |
| <span data-ttu-id="c6ad9-108">Modelo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="c6ad9-108">Device model</span></span>           | <span data-ttu-id="c6ad9-109">ASA (Dispositivo de Segurança Adaptável)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="c6ad9-110">Versão de destino</span><span class="sxs-lookup"><span data-stu-id="c6ad9-110">Target version</span></span>         | <span data-ttu-id="c6ad9-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="c6ad9-111">8.4+</span></span>                              |
| <span data-ttu-id="c6ad9-112">Modelo testado</span><span class="sxs-lookup"><span data-stu-id="c6ad9-112">Tested model</span></span>           | <span data-ttu-id="c6ad9-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="c6ad9-113">ASA 5505</span></span>                          |
| <span data-ttu-id="c6ad9-114">Versão testada</span><span class="sxs-lookup"><span data-stu-id="c6ad9-114">Tested version</span></span>         | <span data-ttu-id="c6ad9-115">9.2</span><span class="sxs-lookup"><span data-stu-id="c6ad9-115">9.2</span></span>                               |
| <span data-ttu-id="c6ad9-116">Versão do IKE</span><span class="sxs-lookup"><span data-stu-id="c6ad9-116">IKE version</span></span>            | <span data-ttu-id="c6ad9-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="c6ad9-118">BGP</span><span class="sxs-lookup"><span data-stu-id="c6ad9-118">BGP</span></span>                    | <span data-ttu-id="c6ad9-119">**Não**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-119">**No**</span></span>                            |
| <span data-ttu-id="c6ad9-120">Tipo de gateway VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="c6ad9-120">Azure VPN gateway type</span></span> | <span data-ttu-id="c6ad9-121">Gateway VPN **baseado em rota**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="c6ad9-122">configuração de saudação abaixo se conecta a um tooan do dispositivo Cisco ASA Azure **baseadas em rota** gateway VPN usando política IPsec/IKE personalizada com a opção "UserPolicyBasedTrafficSelectors", conforme descrito em [neste artigo](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c6ad9-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="c6ad9-123">Requer ASA dispositivos toouse **IKEv2** com configurações baseada em lista de acesso, não com base em VTI.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="c6ad9-124">Consulte as especificações de fornecedor de dispositivo VPN tooensure política de saudação é suportada em seus dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="c6ad9-125">Requisitos do dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="c6ad9-125">VPN device requirements</span></span>
<span data-ttu-id="c6ad9-126">Gateways VPN do Azure usam túneis de VPN S2S de tooestablish de pacotes do IPsec/IKE protocolo padrão.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="c6ad9-127">Consulte também[sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md) para Olá detalhadas parâmetros do protocolo IPsec/IKE e algoritmos de criptografia padrão para gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="c6ad9-128">Você pode opcionalmente especificar combinação exata de saudação de algoritmos de criptografia e restrições de chave para uma conexão específica, conforme descrito em [sobre os requisitos de criptografia](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="c6ad9-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="c6ad9-129">Se você selecionar uma combinação específica de algoritmos de criptografia e restrições de chave, verifique se que você usar especificações de saudação correspondentes em seus dispositivos VPN.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="c6ad9-130">Túnel VPN único</span><span class="sxs-lookup"><span data-stu-id="c6ad9-130">Single VPN tunnel</span></span>
<span data-ttu-id="c6ad9-131">Essa topologia consiste em um único túnel VPN S2S entre um gateway de VPN do Azure e o dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="c6ad9-132">Opcionalmente você pode configurar o BGP em túnel VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![túnel único](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="c6ad9-134">Consulte também[configuração de túnel único](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) obter, instruções passo a passo toobuild Olá configurações do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="c6ad9-135">Informações de gateway de VPN e de rede</span><span class="sxs-lookup"><span data-stu-id="c6ad9-135">Network and VPN gateway information</span></span>
<span data-ttu-id="c6ad9-136">Esta seção lista parâmetros Olá Olá Este exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="c6ad9-137">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-137">**Parameter**</span></span>                | <span data-ttu-id="c6ad9-138">**Valor**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="c6ad9-139">Prefixos de endereços da VNET</span><span class="sxs-lookup"><span data-stu-id="c6ad9-139">VNet address prefixes</span></span>        | <span data-ttu-id="c6ad9-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c6ad9-140">10.11.0.0/16</span></span><br><span data-ttu-id="c6ad9-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c6ad9-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="c6ad9-142">IP do gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="c6ad9-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="c6ad9-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c6ad9-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="c6ad9-144">Prefixos de endereço local</span><span class="sxs-lookup"><span data-stu-id="c6ad9-144">On-premises address prefixes</span></span> | <span data-ttu-id="c6ad9-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c6ad9-145">10.51.0.0/16</span></span><br><span data-ttu-id="c6ad9-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c6ad9-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="c6ad9-147">IP do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="c6ad9-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="c6ad9-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c6ad9-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="c6ad9-149">*ASN de BGP da VNet</span><span class="sxs-lookup"><span data-stu-id="c6ad9-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="c6ad9-150">65010</span><span class="sxs-lookup"><span data-stu-id="c6ad9-150">65010</span></span>                        |
| <span data-ttu-id="c6ad9-151">*IP de par no nível de protocolo BGP do Azure</span><span class="sxs-lookup"><span data-stu-id="c6ad9-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="c6ad9-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="c6ad9-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="c6ad9-153">* ASN de BGP local</span><span class="sxs-lookup"><span data-stu-id="c6ad9-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="c6ad9-154">65050</span><span class="sxs-lookup"><span data-stu-id="c6ad9-154">65050</span></span>                        |
| <span data-ttu-id="c6ad9-155">* IP de par no nível de protocolo BGP local</span><span class="sxs-lookup"><span data-stu-id="c6ad9-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="c6ad9-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="c6ad9-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="c6ad9-157">(*) Parâmetros opcionais apenas para o BGP.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="c6ad9-158">Parâmetros e política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="c6ad9-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="c6ad9-159">Olá tabela a seguir lista os algoritmos de IPsec/IKE hello e parâmetros usados no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="c6ad9-160">Consulte a certeza de que todos os algoritmos listados acima são compatíveis com seus modelos de dispositivo VPN e versões de firmware toomake de especificações de dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="c6ad9-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="c6ad9-162">**Valor**</span><span class="sxs-lookup"><span data-stu-id="c6ad9-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="c6ad9-163">Criptografia IKEv2</span><span class="sxs-lookup"><span data-stu-id="c6ad9-163">IKEv2 Encryption</span></span> | <span data-ttu-id="c6ad9-164">AES256</span><span class="sxs-lookup"><span data-stu-id="c6ad9-164">AES256</span></span>                               |
| <span data-ttu-id="c6ad9-165">Integridade do IKEv2</span><span class="sxs-lookup"><span data-stu-id="c6ad9-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="c6ad9-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="c6ad9-166">SHA384</span></span>                               |
| <span data-ttu-id="c6ad9-167">Grupo DH</span><span class="sxs-lookup"><span data-stu-id="c6ad9-167">DH Group</span></span>         | <span data-ttu-id="c6ad9-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="c6ad9-168">DHGroup24</span></span>                            |
| <span data-ttu-id="c6ad9-169">Criptografia IPsec</span><span class="sxs-lookup"><span data-stu-id="c6ad9-169">IPsec Encryption</span></span> | <span data-ttu-id="c6ad9-170">AES256</span><span class="sxs-lookup"><span data-stu-id="c6ad9-170">AES256</span></span>                               |
| <span data-ttu-id="c6ad9-171">Integridade do IPsec</span><span class="sxs-lookup"><span data-stu-id="c6ad9-171">IPsec Integrity</span></span>  | <span data-ttu-id="c6ad9-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="c6ad9-172">SHA1</span></span>                                 |
| <span data-ttu-id="c6ad9-173">Grupo PFS</span><span class="sxs-lookup"><span data-stu-id="c6ad9-173">PFS Group</span></span>        | <span data-ttu-id="c6ad9-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="c6ad9-174">PFS24</span></span>                                |
| <span data-ttu-id="c6ad9-175">Tempo de vida da QM SA</span><span class="sxs-lookup"><span data-stu-id="c6ad9-175">QM SA Lifetime</span></span>   | <span data-ttu-id="c6ad9-176">7.200 segundos</span><span class="sxs-lookup"><span data-stu-id="c6ad9-176">7200 seconds</span></span>                         |
| <span data-ttu-id="c6ad9-177">Seletor de tráfego</span><span class="sxs-lookup"><span data-stu-id="c6ad9-177">Traffic Selector</span></span> | <span data-ttu-id="c6ad9-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="c6ad9-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="c6ad9-179">Chave Pré-Compartilhada</span><span class="sxs-lookup"><span data-stu-id="c6ad9-179">Pre-Shared Key</span></span>   | <span data-ttu-id="c6ad9-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="c6ad9-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="c6ad9-181">(*) Em alguns dispositivos, a integridade de IPsec deverá ser "nula" se o GCM-AES for usado como o algoritmo de criptografia IPsec.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="c6ad9-182">Notas do dispositivo</span><span class="sxs-lookup"><span data-stu-id="c6ad9-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="c6ad9-183">Suporte ao IKEv2 requer ASA versão 8.4 e acima.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="c6ad9-184">Suporte de grupo DH e PFS superior (além do Grupo de 5) requer ASA versão 9. x.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="c6ad9-185">Criptografia IPsec com integridade de AES-GCM e IPsec com suporte para SHA-256, SHA-384 e SHA-512 requer ASA versão 9. x em hardware ASA mais recente; ASA 5505, 5510, 5520, 5540, 5550, 5580 **não** têm suporte.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="c6ad9-186">(Verifique Olá fornecedor especificações tooconfirm.)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="c6ad9-187">Exemplos de configurações de dispositivo</span><span class="sxs-lookup"><span data-stu-id="c6ad9-187">Sample device configurations</span></span>
<span data-ttu-id="c6ad9-188">script de saudação abaixo fornece um exemplo de configuração com base na topologia de saudação e os parâmetros listados acima.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="c6ad9-189">configuração de túnel VPN S2S Olá consiste Olá partes a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6ad9-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="c6ad9-190">Interfaces e rotas</span><span class="sxs-lookup"><span data-stu-id="c6ad9-190">Interfaces & routes</span></span>
2. <span data-ttu-id="c6ad9-191">Listas de acesso</span><span class="sxs-lookup"><span data-stu-id="c6ad9-191">Access lists</span></span>
3. <span data-ttu-id="c6ad9-192">Política e parâmetros IKE (fase 1 ou modo principal)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="c6ad9-193">Política e parâmetros IPsec (fase 2 ou modo rápido)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="c6ad9-194">Outros parâmetros (fixação de MSS TCP etc.)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c6ad9-195">Verifique se você concluir a configuração adicional de Olá listada abaixo e substitua os espaços reservados de saudação com valores reais de saudação:</span><span class="sxs-lookup"><span data-stu-id="c6ad9-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="c6ad9-196">Configuração de interface para as interfaces interna e externa</span><span class="sxs-lookup"><span data-stu-id="c6ad9-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="c6ad9-197">Rotas para suas redes privadas/internas e externas/públicas</span><span class="sxs-lookup"><span data-stu-id="c6ad9-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="c6ad9-198">Verifique se todos os nomes e números de política são exclusivos no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="c6ad9-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="c6ad9-199">Certifique-se de algoritmos criptográficos Olá têm suporte em seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="c6ad9-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="c6ad9-200">Substituir saudação espaços reservados por valores reais Olá a seguir</span><span class="sxs-lookup"><span data-stu-id="c6ad9-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="c6ad9-201">Nome da interface externa: "externa"</span><span class="sxs-lookup"><span data-stu-id="c6ad9-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="c6ad9-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c6ad9-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="c6ad9-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="c6ad9-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="c6ad9-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="c6ad9-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="c6ad9-205">Nomes do gateway de rede local e da VNet (VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="c6ad9-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="c6ad9-206">Prefixos de endereço de rede local e da VNet</span><span class="sxs-lookup"><span data-stu-id="c6ad9-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="c6ad9-207">Máscaras de rede adequadas</span><span class="sxs-lookup"><span data-stu-id="c6ad9-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="c6ad9-208">Exemplo de configuração</span><span class="sxs-lookup"><span data-stu-id="c6ad9-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="c6ad9-209">Comandos de depuração simples</span><span class="sxs-lookup"><span data-stu-id="c6ad9-209">Simple debugging commands</span></span>

<span data-ttu-id="c6ad9-210">Aqui estão alguns comandos ASA para fins de depuração:</span><span class="sxs-lookup"><span data-stu-id="c6ad9-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="c6ad9-211">Mostrar Olá IPsec e do IKE SA</span><span class="sxs-lookup"><span data-stu-id="c6ad9-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="c6ad9-212">"show crypto ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="c6ad9-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="c6ad9-213">"show crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="c6ad9-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="c6ad9-214">Inserir o modo de depuração - isso pode obter com muito ruído em console Olá</span><span class="sxs-lookup"><span data-stu-id="c6ad9-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="c6ad9-215">"debug crypto ikev2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="c6ad9-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="c6ad9-216">"debug crypto ikev2 protocol <level>"</span><span class="sxs-lookup"><span data-stu-id="c6ad9-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="c6ad9-217">Listar configurações atuais</span><span class="sxs-lookup"><span data-stu-id="c6ad9-217">List current configurations</span></span>
    - <span data-ttu-id="c6ad9-218">"Mostrar execução" - mostra Olá atuais configurações no dispositivo Olá; Você pode usar Olá partes específicas do várias toolist de subsistema de comandos de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="c6ad9-219">Por exemplo, "show run crypto", "show run access-list", "show run tunnel-group" etc.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6ad9-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6ad9-220">Next steps</span></span>
<span data-ttu-id="c6ad9-221">Consulte [Gateways de VPN configuração ativa-ativa para conexões de rede virtual a rede e entre locais](vpn-gateway-activeactive-rm-powershell.md) para conexões de rede virtual a rede e etapas tooconfigure ativo-ativo entre locais.</span><span class="sxs-lookup"><span data-stu-id="c6ad9-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

