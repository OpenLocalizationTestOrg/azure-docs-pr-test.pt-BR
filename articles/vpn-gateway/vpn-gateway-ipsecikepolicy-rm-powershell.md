---
title: "Configurar a política de IPsec/IKE para conexões VPN S2S ou VNet para VNet: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artigo orienta na configuração da política IPsec/IKE para conexões S2S ou VNet-para-VNet  com gateways de VPN do Azure usando o Azure Resource Manager e o PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="6c350-103">Configurar a política de IPsec/IKE para conexões VPN S2S ou VNet para VNet</span><span class="sxs-lookup"><span data-stu-id="6c350-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="6c350-104">Este artigo orienta Olá etapas tooconfigure política IPsec/IKE para conexões VPN Site a Site ou VNet para VNet usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c350-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="6c350-105"><a name="about"></a>Sobre os parâmetros de política IKE e IPsec para os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="6c350-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="6c350-106">O padrão de protocolo IKE e IPsec suporta uma ampla gama de algoritmos criptográficos em várias combinações.</span><span class="sxs-lookup"><span data-stu-id="6c350-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="6c350-107">Consulte também[sobre os requisitos de criptografia e gateways de VPN do Azure](vpn-gateway-about-compliance-crypto.md) toosee como isso pode ajudar a garantir entre locais e conectividade de rede virtual a rede atender a seus requisitos de conformidade ou de segurança.</span><span class="sxs-lookup"><span data-stu-id="6c350-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="6c350-108">Este artigo fornece instruções toocreate e configurar uma política de IPsec/IKE e aplicar tooa conexão de novo ou existente:</span><span class="sxs-lookup"><span data-stu-id="6c350-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="6c350-109">Parte 1 - toocreate de fluxo de trabalho e definir a diretiva de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="6c350-110">Parte 2 - Suporte para algoritmos de criptografia e restrições de chave</span><span class="sxs-lookup"><span data-stu-id="6c350-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="6c350-111">Parte 3 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="6c350-112">Parte 4 - Criar uma nova conexão de VNet para VNet com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="6c350-113">Parte 5 - Gerenciar (criar, adicionar, remover) política IPsec/IKE para uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="6c350-114">Observe que a diretiva de IPsec/IKE só funciona em Olá SKUs de gateway a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c350-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="6c350-115">***VpnGw1, VpnGw2, VpnGw3*** (baseado em rotas)</span><span class="sxs-lookup"><span data-stu-id="6c350-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="6c350-116">***Standard*** e ***HighPerformance*** (baseado em rotas)</span><span class="sxs-lookup"><span data-stu-id="6c350-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="6c350-117">Você só pode especificar ***uma*** combinação de políticas para uma determinada conexão.</span><span class="sxs-lookup"><span data-stu-id="6c350-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="6c350-118">Você deve especificar todos os algoritmos e parâmetros para IKE (modo principal) e IPsec (modo rápido).</span><span class="sxs-lookup"><span data-stu-id="6c350-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="6c350-119">A especificação de política parcial não é permitida.</span><span class="sxs-lookup"><span data-stu-id="6c350-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="6c350-120">Consulte as especificações de fornecedor de dispositivo VPN tooensure política de saudação é suportada em seus dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="6c350-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="6c350-121">S2S ou conexões de rede virtual a rede não é possível estabelecer se políticas Olá são incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="6c350-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="6c350-122"><a name ="workflow"></a>Parte 1 - toocreate de fluxo de trabalho e definir a diretiva de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="6c350-123">Esta seção descreve a saudação fluxo de trabalho toocreate e atualização IPsec/IKE política em uma conexão VPN S2S ou VNet para VNet:</span><span class="sxs-lookup"><span data-stu-id="6c350-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="6c350-124">Criar uma rede virtual e um gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="6c350-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="6c350-125">Criar um gateway de rede local para a conexão cruzada local ou outra rede virtual e o gateway de conexão VNet para VNet</span><span class="sxs-lookup"><span data-stu-id="6c350-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="6c350-126">Criar uma política de IPsec/IKE com parâmetros e algoritmos selecionados</span><span class="sxs-lookup"><span data-stu-id="6c350-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="6c350-127">Criar uma conexão (IPsec ou VNet2VNet) com a diretiva de IPsec/IKE Olá</span><span class="sxs-lookup"><span data-stu-id="6c350-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="6c350-128">Adicionar/atualizar/remover uma política de IPsec/IKE para uma conexão existente</span><span class="sxs-lookup"><span data-stu-id="6c350-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="6c350-129">instruções Olá neste artigo o ajudará a instalar e configurar políticas de IPsec/IKE, conforme mostrado no diagrama de saudação:</span><span class="sxs-lookup"><span data-stu-id="6c350-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="6c350-131"><a name ="params"></a>Parte 2 - Suporte para algoritmos de criptografia e restrições de chave</span><span class="sxs-lookup"><span data-stu-id="6c350-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="6c350-132">Olá tabela a seguir lista Olá suporte para algoritmos de criptografia e restrições de chave podem ser configuradas por clientes hello:</span><span class="sxs-lookup"><span data-stu-id="6c350-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="6c350-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="6c350-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="6c350-134">**Opções**</span><span class="sxs-lookup"><span data-stu-id="6c350-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="6c350-135">Criptografia IKEv2</span><span class="sxs-lookup"><span data-stu-id="6c350-135">IKEv2 Encryption</span></span> | <span data-ttu-id="6c350-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="6c350-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="6c350-137">Integridade do IKEv2</span><span class="sxs-lookup"><span data-stu-id="6c350-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="6c350-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="6c350-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="6c350-139">Grupo DH</span><span class="sxs-lookup"><span data-stu-id="6c350-139">DH Group</span></span>         | <span data-ttu-id="6c350-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, Nenhum</span><span class="sxs-lookup"><span data-stu-id="6c350-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="6c350-141">Criptografia IPsec</span><span class="sxs-lookup"><span data-stu-id="6c350-141">IPsec Encryption</span></span> | <span data-ttu-id="6c350-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, nenhum</span><span class="sxs-lookup"><span data-stu-id="6c350-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="6c350-143">Integridade do IPsec</span><span class="sxs-lookup"><span data-stu-id="6c350-143">IPsec Integrity</span></span>  | <span data-ttu-id="6c350-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="6c350-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="6c350-145">Grupo PFS</span><span class="sxs-lookup"><span data-stu-id="6c350-145">PFS Group</span></span>        | <span data-ttu-id="6c350-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, nenhum</span><span class="sxs-lookup"><span data-stu-id="6c350-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="6c350-147">Tempo de vida da QM SA</span><span class="sxs-lookup"><span data-stu-id="6c350-147">QM SA Lifetime</span></span>   | <span data-ttu-id="6c350-148">(**Opcional**: os valores padrão serão usados se não for especificados)</span><span class="sxs-lookup"><span data-stu-id="6c350-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="6c350-149">Segundos (inteiro; **mínimo de 300**/padrão de 27000 segundos)</span><span class="sxs-lookup"><span data-stu-id="6c350-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="6c350-150">KBytes (inteiro; **mín. de 1024** /padrão de 102400000 KBytes)</span><span class="sxs-lookup"><span data-stu-id="6c350-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="6c350-151">Seletor de tráfego</span><span class="sxs-lookup"><span data-stu-id="6c350-151">Traffic Selector</span></span> | <span data-ttu-id="6c350-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, padrão$False, se não especificado)</span><span class="sxs-lookup"><span data-stu-id="6c350-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="6c350-153">**Se GCMAES é usado para o algoritmo de criptografia de IPsec, você deve selecionar hello GCMAES o mesmo algoritmo e comprimento de chave para integridade de IPsec; Por exemplo, usando GCMAES128 para ambos**</span><span class="sxs-lookup"><span data-stu-id="6c350-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="6c350-154">Tempo de vida do SA do modo principal IKEv2 é fixo em 28.800 segundos em gateways de VPN do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="6c350-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="6c350-155">Configuração de "UsePolicyBasedTrafficSelectors" muito$ True em uma conexão configurará Olá VPN do Azure gateway tooconnect toopolicy VPN firewall baseado no local.</span><span class="sxs-lookup"><span data-stu-id="6c350-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="6c350-156">Se você habilitar PolicyBasedTrafficSelectors, você precisa tooensure que seu dispositivo VPN tem seletores de tráfego correspondente Olá definidos com todas as combinações de seu local (gateway de rede local) de prefixos de rede de prefixos de rede virtual do Azure Olá, em vez de para qualquer.</span><span class="sxs-lookup"><span data-stu-id="6c350-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="6c350-157">Por exemplo, se os prefixos de rede local são 10.1.0.0/16 e 10.2.0.0/16, e os prefixos de rede virtual são 192.168.0.0/16 e 172.16.0.0/16, você precisa toospecify Olá seletores de tráfego a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c350-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="6c350-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6c350-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="6c350-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6c350-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="6c350-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6c350-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="6c350-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6c350-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="6c350-162">Consulte [Conectar dispositivos VPN baseados em várias políticas locais](vpn-gateway-connect-multiple-policybased-rm-ps.md) para saber mais sobre os seletores de tráfego baseados em políticas.</span><span class="sxs-lookup"><span data-stu-id="6c350-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="6c350-163">Olá a tabela a seguir lista Olá grupos Diffie-Hellman correspondentes com suporte pela política personalizada do hello:</span><span class="sxs-lookup"><span data-stu-id="6c350-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="6c350-164">**Grupo Diffie-Hellman**</span><span class="sxs-lookup"><span data-stu-id="6c350-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="6c350-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="6c350-165">**DHGroup**</span></span>              | <span data-ttu-id="6c350-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="6c350-166">**PFSGroup**</span></span> | <span data-ttu-id="6c350-167">**Comprimento da chave**</span><span class="sxs-lookup"><span data-stu-id="6c350-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c350-168">1</span><span class="sxs-lookup"><span data-stu-id="6c350-168">1</span></span>                         | <span data-ttu-id="6c350-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="6c350-169">DHGroup1</span></span>                 | <span data-ttu-id="6c350-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="6c350-170">PFS1</span></span>         | <span data-ttu-id="6c350-171">MODP de 768 bits</span><span class="sxs-lookup"><span data-stu-id="6c350-171">768-bit MODP</span></span>   |
| <span data-ttu-id="6c350-172">2</span><span class="sxs-lookup"><span data-stu-id="6c350-172">2</span></span>                         | <span data-ttu-id="6c350-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="6c350-173">DHGroup2</span></span>                 | <span data-ttu-id="6c350-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="6c350-174">PFS2</span></span>         | <span data-ttu-id="6c350-175">MODP de 1024 bits</span><span class="sxs-lookup"><span data-stu-id="6c350-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="6c350-176">14</span><span class="sxs-lookup"><span data-stu-id="6c350-176">14</span></span>                        | <span data-ttu-id="6c350-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="6c350-177">DHGroup14</span></span><br><span data-ttu-id="6c350-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="6c350-178">DHGroup2048</span></span> | <span data-ttu-id="6c350-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="6c350-179">PFS2048</span></span>      | <span data-ttu-id="6c350-180">MODP de 2048 bits</span><span class="sxs-lookup"><span data-stu-id="6c350-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="6c350-181">19</span><span class="sxs-lookup"><span data-stu-id="6c350-181">19</span></span>                        | <span data-ttu-id="6c350-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="6c350-182">ECP256</span></span>                   | <span data-ttu-id="6c350-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="6c350-183">ECP256</span></span>       | <span data-ttu-id="6c350-184">ECP de 256 bits</span><span class="sxs-lookup"><span data-stu-id="6c350-184">256-bit ECP</span></span>    |
| <span data-ttu-id="6c350-185">20</span><span class="sxs-lookup"><span data-stu-id="6c350-185">20</span></span>                        | <span data-ttu-id="6c350-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="6c350-186">ECP384</span></span>                   | <span data-ttu-id="6c350-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="6c350-187">ECP284</span></span>       | <span data-ttu-id="6c350-188">ECP de 384 bits</span><span class="sxs-lookup"><span data-stu-id="6c350-188">384-bit ECP</span></span>    |
| <span data-ttu-id="6c350-189">24</span><span class="sxs-lookup"><span data-stu-id="6c350-189">24</span></span>                        | <span data-ttu-id="6c350-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="6c350-190">DHGroup24</span></span>                | <span data-ttu-id="6c350-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="6c350-191">PFS24</span></span>        | <span data-ttu-id="6c350-192">MODP de 2048 bits</span><span class="sxs-lookup"><span data-stu-id="6c350-192">2048-bit MODP</span></span>  |

<span data-ttu-id="6c350-193">Consulte também[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6c350-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="6c350-194"><a name ="crossprem"></a>Parte 3 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-195">Esta seção orienta você pelas etapas de saudação da criação de uma conexão VPN S2S com uma política de IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="6c350-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="6c350-196">Olá etapas a seguir criam conexão Olá conforme mostrado no diagrama de saudação:</span><span class="sxs-lookup"><span data-stu-id="6c350-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![política de S2S](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="6c350-198">Consulte [Criar uma conexão VPN S2S](vpn-gateway-create-site-to-site-rm-powershell.md) para obter instruções passo a passo mais detalhadas para criar uma conexão VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="6c350-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="6c350-199"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6c350-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="6c350-200">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c350-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="6c350-201">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c350-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6c350-202">Instale os cmdlets do PowerShell do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="6c350-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6c350-203">Consulte [visão geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="6c350-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="6c350-204"><a name="createvnet1"></a>Etapa 1 - Criar rede virtual hello, gateway de VPN e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="6c350-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="6c350-205">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="6c350-205">1. Declare your variables</span></span>

<span data-ttu-id="6c350-206">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="6c350-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="6c350-207">Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção.</span><span class="sxs-lookup"><span data-stu-id="6c350-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="6c350-208">2. Conecte-se a assinatura de tooyour e criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6c350-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="6c350-209">Verifique se que você alternar Olá toouse de modo tooPowerShell cmdlets do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6c350-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="6c350-210">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6c350-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="6c350-211">Abra o console do PowerShell e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="6c350-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="6c350-212">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c350-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="6c350-213">3. Criar rede virtual hello, gateway de VPN e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="6c350-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="6c350-214">saudação de exemplo a seguir cria rede virtual hello, TestVNet1, com três sub-redes e gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="6c350-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="6c350-215">Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="6c350-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="6c350-216">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="6c350-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="6c350-217"><a name="s2sconnection"></a>Parte 2 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="6c350-218">1. Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-219">Olá, script de exemplo a seguir cria uma política de IPsec/IKE com hello algoritmos e os parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c350-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="6c350-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="6c350-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="6c350-221">IPsec: AES256, SHA256, PFS24, SA tempo de vida 7200 segundos & 2048KB</span><span class="sxs-lookup"><span data-stu-id="6c350-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="6c350-222">Se você usar GCMAES para IPsec, você deve usar Olá GCMAES o mesmo algoritmo e comprimento de chave de criptografia IPsec e integridade, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6c350-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="6c350-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="6c350-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="6c350-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Tempo de vida 7.200 segundos e 2.048 KB</span><span class="sxs-lookup"><span data-stu-id="6c350-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="6c350-225">2. Criar conexão de VPN S2S Olá com hello diretiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-226">Criar uma conexão VPN S2S e aplicar a diretiva de IPsec/IKE Olá criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6c350-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="6c350-227">Opcionalmente, você pode adicionar "-UsePolicyBasedTrafficSelectors $True" toohello criar conexão cmdlet tooenable VPN Azure gateway tooconnect toopolicy dispositivos baseados em VPN no local, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="6c350-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c350-228">Quando uma política de IPsec/IKE é especificada em uma conexão, o gateway de VPN do Azure Olá só enviar ou aceitar proposta de IPsec/IKE Olá com algoritmos de criptografia especificados e as restrições de chave que determinada conexão.</span><span class="sxs-lookup"><span data-stu-id="6c350-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="6c350-229">Verifique se o dispositivo VPN local para conexão Olá usa ou aceita a combinação de política exata Olá, caso contrário túnel de VPN S2S Olá não estabelecerá.</span><span class="sxs-lookup"><span data-stu-id="6c350-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="6c350-230"><a name ="vnet2vnet"></a>Parte 4 - Criar uma nova conexão de VNet para VNet com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-231">etapas de saudação da criação de uma conexão de rede virtual a rede com uma política de IPsec/IKE são semelhante toothat de uma conexão VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="6c350-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="6c350-232">Olá scripts de exemplo a seguir criam conexão Olá conforme mostrado no diagrama de saudação:</span><span class="sxs-lookup"><span data-stu-id="6c350-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![política de V2V](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="6c350-234">Consulte [Criar uma conexão VNet para VNet](vpn-gateway-vnet-vnet-rm-ps.md) para obter etapas mais detalhadas para criar uma conexão VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="6c350-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="6c350-235">Você deve concluir [parte 3](#crossprem) toocreate configurar TestVNet1 e Olá Gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="6c350-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="6c350-236"><a name="createvnet2"></a>Etapa 1 - Criar rede virtual do segundo hello e gateway da VPN</span><span class="sxs-lookup"><span data-stu-id="6c350-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="6c350-237">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="6c350-237">1. Declare your variables</span></span>

<span data-ttu-id="6c350-238">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="6c350-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="6c350-239">2. Criar rede virtual do segundo hello e gateway da VPN no novo grupo de recursos Olá</span><span class="sxs-lookup"><span data-stu-id="6c350-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="6c350-240">Etapa 2: criar uma conexão de rede virtual toVNet com hello diretiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-241">Toohello semelhante conexão VPN S2S, criar uma política de IPsec/IKE, aplique toopolicy toohello nova conexão.</span><span class="sxs-lookup"><span data-stu-id="6c350-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="6c350-242">1. Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-243">Olá, script de exemplo a seguir cria uma política de IPsec/IKE diferente com hello algoritmos e os parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c350-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="6c350-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="6c350-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="6c350-245">IPsec: GCMAES128, GCMAES128, PFS14, tempo de vida do SA 7200 segundos e 4096KB</span><span class="sxs-lookup"><span data-stu-id="6c350-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="6c350-246">2. Criar conexões VNet para VNet com hello diretiva IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="6c350-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="6c350-247">Criar uma conexão de rede virtual a rede e aplicar a diretiva de IPsec/IKE Olá criado por você.</span><span class="sxs-lookup"><span data-stu-id="6c350-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="6c350-248">Neste exemplo, ambos os gateways estão em Olá mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="6c350-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="6c350-249">Portanto é possível toocreate e configurar as conexões com Olá a mesma diretiva de IPsec/IKE Olá mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c350-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="6c350-250">Quando uma política de IPsec/IKE é especificada em uma conexão, o gateway de VPN do Azure Olá só enviar ou aceitar proposta de IPsec/IKE Olá com algoritmos de criptografia especificados e as restrições de chave que determinada conexão.</span><span class="sxs-lookup"><span data-stu-id="6c350-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="6c350-251">Verifique se Olá diretivas IPsec para ambas as conexões são Olá iguais, caso contrário, a conexão de rede virtual a rede não estabelecerá.</span><span class="sxs-lookup"><span data-stu-id="6c350-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="6c350-252">Depois de concluir essas etapas, conexão Olá é estabelecida em poucos minutos, e você terá Olá topologia de rede a seguir conforme mostrado no início da saudação:</span><span class="sxs-lookup"><span data-stu-id="6c350-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="6c350-254"><a name ="managepolicy"></a>Parte 5 - Atualizar política de IPsec/IKE para uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="6c350-255">Olá última seção mostra a você como toomanage política IPsec/IKE para uma conexão existente S2S ou VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="6c350-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="6c350-256">Exercício de saudação abaixo orienta Olá operações em uma conexão a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c350-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="6c350-257">Mostrar política de IPsec/IKE de saudação de uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="6c350-258">Adicionar ou atualizar a conexão de tooa de diretiva de IPsec/IKE Olá</span><span class="sxs-lookup"><span data-stu-id="6c350-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="6c350-259">Remover a diretiva de IPsec/IKE Olá de uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="6c350-260">Olá mesmas etapas se aplicam tooboth S2S e conexões de rede virtual a rede.</span><span class="sxs-lookup"><span data-stu-id="6c350-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c350-261">A política de IPsec/IKE tem suporte somente nos gateways de VPN baseados en rota *Standard* e *HighPerformance*.</span><span class="sxs-lookup"><span data-stu-id="6c350-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="6c350-262">Ele não funciona no SKU do gateway básica Olá ou gateway VPN com base na política hello.</span><span class="sxs-lookup"><span data-stu-id="6c350-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="6c350-263">1. Mostrar política de IPsec/IKE de saudação de uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="6c350-264">saudação de exemplo a seguir mostra como tooget Olá política IPsec/IKE configurada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="6c350-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="6c350-265">os scripts de saudação também continuam de exercícios de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="6c350-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="6c350-266">comando último Olá lista política IPsec/IKE atual Olá configurada na conexão hello, se houver algum.</span><span class="sxs-lookup"><span data-stu-id="6c350-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="6c350-267">Olá saída de exemplo a seguir destina-se a conexão de saudação:</span><span class="sxs-lookup"><span data-stu-id="6c350-267">hello following sample output is for hello connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="6c350-268">Se não houver nenhuma política de IPsec/IKE configurada, Olá comando (PS > $connection6.policy) obtém vazio retornado.</span><span class="sxs-lookup"><span data-stu-id="6c350-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="6c350-269">Isso não significa IPsec/IKE não está configurado na conexão hello, mas que não há nenhuma diretiva de IPsec/IKE personalizada.</span><span class="sxs-lookup"><span data-stu-id="6c350-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="6c350-270">conexão real Olá usa a política de padrão de saudação negociada entre o dispositivo VPN de local e Olá gateway VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c350-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="6c350-271">2. Adicionar e atualizar uma política de IPsec/IKE para uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="6c350-272">Olá etapas tooadd uma nova política ou atualização de uma política existente em uma conexão são Olá mesmo: criar uma nova política, aplique a nova conexão de toohello política hello.</span><span class="sxs-lookup"><span data-stu-id="6c350-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="6c350-273">tooenable "UsePolicyBasedTrafficSelectors" ao conectar tooan local dispositivo VPN baseado em políticas, adicionar hello "-UsePolicyBaseTrafficSelectors" parâmetro toohello cmdlet, ou defina-o muito opção de saudação do $ toodisable False:</span><span class="sxs-lookup"><span data-stu-id="6c350-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="6c350-274">Você pode obter conexão Olá toocheck novamente se a política de saudação é atualizada.</span><span class="sxs-lookup"><span data-stu-id="6c350-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="6c350-275">Você deve ver a saída de saudação da última linha de saudação, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="6c350-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="6c350-276">3. Remover uma política de IPsec/IKE de uma conexão</span><span class="sxs-lookup"><span data-stu-id="6c350-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="6c350-277">Quando você remover a política personalizada de saudação de uma conexão, gateway de VPN do Azure Olá reverte back toohello [lista padrão de propostas de IPsec/IKE](vpn-gateway-about-vpn-devices.md) e nova negociação será iniciada novamente com o dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="6c350-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="6c350-278">Você pode usar Olá mesmo toocheck de script se Olá política foi removida da conexão hello.</span><span class="sxs-lookup"><span data-stu-id="6c350-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c350-279">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c350-279">Next steps</span></span>

<span data-ttu-id="6c350-280">Consulte [Conectar dispositivos VPN baseados em várias políticas locais](vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter mais detalhes sobre os seletores de tráfego baseado em políticas.</span><span class="sxs-lookup"><span data-stu-id="6c350-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="6c350-281">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="6c350-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="6c350-282">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="6c350-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
