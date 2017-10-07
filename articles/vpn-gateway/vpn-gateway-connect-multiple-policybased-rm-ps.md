---
title: "Conectar dispositivos VPN com base na política do Azure VPN gateways toomultiple local: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artigo orienta você pela configuração do Azure baseadas em rota VPN gateway toomultiple baseado em políticas dispositivos VPN usando o Gerenciador de recursos do Azure e o PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>Conecte-se a VPN do Azure gateways toomultiple baseado em políticas VPN dispositivos locais usando o PowerShell

Este artigo ajuda você a configurar um Azure baseadas em rota VPN gateway tooconnect toomultiple local baseado em políticas dispositivos VPN utilizando políticas personalizadas de IPsec/IKE em conexões VPN S2S.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>Sobre gateways VPN com base em políticas e rotas

Política - *versus* dispositivos VPN com base em rota diferem em como os seletores de tráfego de IPsec Olá são definidos em uma conexão:

* **Com base na política** dispositivos VPN usam combinações de saudação de prefixos de ambos os toodefine de redes, como tráfego será criptografado/descriptografado por meio de túneis IPsec. Normalmente, ele é criado em dispositivos de firewall que executam a filtragem de pacote. Descriptografia e criptografia de túnel IPsec são adicionados a filtragem de pacotes toohello e o mecanismo de processamento.
* **Baseado em rotas** dispositivos VPN usam seletores de tráfego para qualquer (curinga) e permitem roteamento/encaminhamento tabelas túneis do IPsec toodifferent tráfego direto. Normalmente, ele é criado em plataformas de roteador, onde cada túnel IPsec é modelado como uma interface de rede ou VTI (interface do túnel virtual).

Olá diagramas a seguir realçam dois modelos de saudação:

### <a name="policy-based-vpn-example"></a>Exemplo de VPN com base em políticas
![baseado em políticas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Exemplo de VPN com base em rotas
![baseado em rotas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Suporte do Azure para VPN com base em políticas
Atualmente, o Azure oferece suporte a ambos os modos de gateways VPN: gateways VPN com base em rotas e gateways VPN com base em políticas. Eles são criados em diferentes plataformas internas que resultam em especificações diferentes:

|                          | **Gateway de VPN PolicyBased** | **Gateway de VPN RouteBased**               |
| ---                      | ---                         | ---                                      |
| **SKU de gateway do Azure**    | Basic                       | Basic, Standard, HighPerformance         |
| **Versão IKE**          | IKEv1                       | IKEv2                                    |
| **IOPS Conexões S2S** | **1**                       | Basic/Standard: 10<br> HighPerformance: 30 |
|                          |                             |                                          |

Com a diretiva de IPsec/IKE personalizada hello, agora você pode configurar o Azure baseadas em rota VPN gateways toouse com base no prefixo seletores de tráfego com a opção "**PolicyBasedTrafficSelectors**", dispositivos VPN com base na política do tooconnect tooon locais. Esse recurso permite que você tooconnect de uma rede virtual do Azure e toomultiple de gateway VPN de dispositivos VPN/firewall baseado em políticas, removendo o limite de conexão única de saudação do atuais gateways VPN com base na política do Azure Olá no local.

> [!IMPORTANT]
> 1. tooenable essa conectividade, seus dispositivos VPN com base na política local devem oferecer suporte **IKEv2** tooconnect toohello Azure baseadas em rota gateways VPN. Verifique as especificações do dispositivo VPN.
> 2. redes locais de saudação conectando por meio de dispositivos VPN com base na política com esse mecanismo só podem se conectar toohello rede virtual do Azure. **não é possível atravessam redes locais de tooother ou redes virtuais por meio de Olá mesmo gateway VPN do Azure**.
> 3. opção de configuração de saudação faz parte da política personalizada de conexão do IPsec/IKE hello. Se você habilitar a opção de seletor Olá tráfego baseado em políticas, você deve especificar política completa de saudação (algoritmos de criptografia e a integridade de IPsec/IKE, restrições de chave e tempos de vida do SA).

Olá diagrama a seguir mostra por que o roteamento de tráfego por meio do gateway de VPN do Azure não funciona com a opção de baseado em políticas de saudação:

![trânsito com base em políticas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Conforme mostrado no diagrama hello, gateway de VPN do Azure Olá tem seletores de tráfego de saudação tooeach de rede virtual de prefixos de rede local hello, mas não os prefixos de conexão entre hello. Por exemplo, no site local 2, site 3 e 4 do site podem cada comunicar tooVNet1 respectivamente, mas não podem se conectar via Olá VPN do Azure gateway tooeach outros. diagrama de saudação mostra Olá conectar-se entre os seletores de tráfego que não estão disponíveis no gateway de VPN do Azure Olá nesta configuração.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Configurar os seletores de tráfego com base em políticas para uma conexão

Olá instruções deste artigo, siga Olá mesmo exemplo conforme descrito em [política IPsec/IKE configurar conexões S2S ou VNet para VNet](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish uma conexão VPN S2S. Isso é mostrado no diagrama a seguir de saudação:

![política de S2S](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Olá tooenable de fluxo de trabalho essa conectividade:
1. Criar rede virtual hello, gateway de VPN e o gateway de rede local para a conexão entre locais
2. Criar uma política de IPsec/IKE
3. Aplique a política de hello quando você criar uma conexão S2S ou VNet para VNet, e **habilitar seletores de tráfego com base na política de saudação** na conexão Olá
4. Se a conexão de saudação já foi criado, você pode aplicar ou atualizar a conexão existente do hello política tooan

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Habilitar os seletores de tráfego com base em políticas para uma conexão

Verifique se você concluiu [parte 3 de artigo de diretiva de IPsec/IKE configurar Olá](vpn-gateway-ipsecikepolicy-rm-powershell.md) para essa seção. Olá seguindo o exemplo usa Olá mesmos parâmetros e etapas:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Etapa 1 - Criar rede virtual hello, gateway de VPN e gateway de rede local

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Declare as variáveis & conectar-se a assinatura de tooyour
Para este exercício, começaremos declarando nossa variáveis. Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção.

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
toouse Olá cmdlets do Gerenciador de recursos, verifique se você alternar o modo de tooPowerShell. Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

Abra o console do PowerShell e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Criar rede virtual hello, gateway de VPN e gateway de rede local
saudação de exemplo a seguir cria rede virtual hello, TestVNet1 com três sub-redes e gateway VPN hello. Ao substituir valores, é importante que você sempre nomeie sua sub-rede de gateway especificamente como ‘GatewaySubnet’. Se você usar outro nome, a criação do gateway falhará.

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Parte 2 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Criar uma política de IPsec/IKE

> [!IMPORTANT]
> Você precisa de toocreate uma política de IPsec/IKE na ordem tooenable opção "UsePolicyBasedTrafficSelectors" na conexão hello.

Olá exemplo a seguir cria uma política de IPsec/IKE com esses algoritmos e parâmetros:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, tempo de vida da SA 3600 segundos e 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Criar conexão de VPN S2S Olá com seletores de tráfego com base em política e a diretiva de IPsec/IKE
Criar uma conexão VPN S2S e aplicar a diretiva de IPsec/IKE Olá criada na etapa anterior hello. Lembre-se de parâmetro adicionais hello "-UsePolicyBasedTrafficSelectors $True" que permite que os seletores de tráfego baseado em políticas na conexão hello.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Depois de concluir as etapas de Olá, Olá conexão VPN S2S usará Olá política IPsec/IKE definida e habilitar os seletores de tráfego baseado em políticas em conexão hello. Você pode repetir Olá mesmo etapas tooadd mais conexões tooadditional local com base na política dispositivos VPN de Olá mesmo gateway VPN do Azure.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Atualizar seletores de tráfego com base em políticas para uma conexão
Olá última seção mostra a você como seletores de tráfego com base na política de saudação tooupdate opção para uma conexão VPN S2S existente.

### <a name="1-get-hello-connection"></a>1. Obter conexão Olá
Obter recurso de conexão de saudação.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Verificar opção de seletores de tráfego com base na política de saudação
Olá linha a seguir mostra se os seletores de tráfego com base na política de saudação são usados para conexão hello:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Se a linha hello retorna "**True**", em seguida, seletores de tráfego com base na política são configurados na conexão de saudação; caso contrário, ele retorna "**False**."

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Atualizar seletores de tráfego com base na política de saudação em uma conexão
Depois de obter o recurso de conexão hello, você pode habilitar ou desabilitar a opção de saudação.

#### <a name="disable-usepolicybasedtrafficselectors"></a>Desabilitar UsePolicyBasedTrafficSelectors
Olá exemplo a seguir desabilita a opção de seletores de tráfego com base na política de hello, mas deixa Olá política IPsec/IKE inalterada:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>Habilitar UsePolicyBasedTrafficSelectors
Olá exemplo a seguir habilita a opção de seletores de tráfego com base na política de saudação, mas deixa Olá política IPsec/IKE inalterada:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Próximas etapas
Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.

Também analise [Configurar política de IPsec/IKE para conexões de VPN S2S ou Rede Virtual para Rede Virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter mais detalhes sobre políticas de IPsec/IKE personalizadas.
