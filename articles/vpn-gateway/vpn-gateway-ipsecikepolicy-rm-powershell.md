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
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>Configurar a política de IPsec/IKE para conexões VPN S2S ou VNet para VNet

Este artigo orienta Olá etapas tooconfigure política IPsec/IKE para conexões VPN Site a Site ou VNet para VNet usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.

## <a name="about"></a>Sobre os parâmetros de política IKE e IPsec para os gateways de VPN do Azure
O padrão de protocolo IKE e IPsec suporta uma ampla gama de algoritmos criptográficos em várias combinações. Consulte também[sobre os requisitos de criptografia e gateways de VPN do Azure](vpn-gateway-about-compliance-crypto.md) toosee como isso pode ajudar a garantir entre locais e conectividade de rede virtual a rede atender a seus requisitos de conformidade ou de segurança.

Este artigo fornece instruções toocreate e configurar uma política de IPsec/IKE e aplicar tooa conexão de novo ou existente:

* [Parte 1 - toocreate de fluxo de trabalho e definir a diretiva de IPsec/IKE](#workflow)
* [Parte 2 - Suporte para algoritmos de criptografia e restrições de chave](#params)
* [Parte 3 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE](#crossprem)
* [Parte 4 - Criar uma nova conexão de VNet para VNet com a política de IPsec/IKE](#vnet2vnet)
* [Parte 5 - Gerenciar (criar, adicionar, remover) política IPsec/IKE para uma conexão](#managepolicy)

> [!IMPORTANT]
> 1. Observe que a diretiva de IPsec/IKE só funciona em Olá SKUs de gateway a seguir:
>    * ***VpnGw1, VpnGw2, VpnGw3*** (baseado em rotas)
>    * ***Standard*** e ***HighPerformance*** (baseado em rotas)
> 2. Você só pode especificar ***uma*** combinação de políticas para uma determinada conexão.
> 3. Você deve especificar todos os algoritmos e parâmetros para IKE (modo principal) e IPsec (modo rápido). A especificação de política parcial não é permitida.
> 4. Consulte as especificações de fornecedor de dispositivo VPN tooensure política de saudação é suportada em seus dispositivos VPN local. S2S ou conexões de rede virtual a rede não é possível estabelecer se políticas Olá são incompatíveis.

## <a name ="workflow"></a>Parte 1 - toocreate de fluxo de trabalho e definir a diretiva de IPsec/IKE
Esta seção descreve a saudação fluxo de trabalho toocreate e atualização IPsec/IKE política em uma conexão VPN S2S ou VNet para VNet:
1. Criar uma rede virtual e um gateway de VPN
2. Criar um gateway de rede local para a conexão cruzada local ou outra rede virtual e o gateway de conexão VNet para VNet
3. Criar uma política de IPsec/IKE com parâmetros e algoritmos selecionados
4. Criar uma conexão (IPsec ou VNet2VNet) com a diretiva de IPsec/IKE Olá
5. Adicionar/atualizar/remover uma política de IPsec/IKE para uma conexão existente

instruções Olá neste artigo o ajudará a instalar e configurar políticas de IPsec/IKE, conforme mostrado no diagrama de saudação:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Parte 2 - Suporte para algoritmos de criptografia e restrições de chave

Olá tabela a seguir lista Olá suporte para algoritmos de criptografia e restrições de chave podem ser configuradas por clientes hello:

| **IPsec/IKEv2**  | **Opções**    |
| ---  | --- 
| Criptografia IKEv2 | AES256, AES192, AES128, DES3, DES  
| Integridade do IKEv2  | SHA384, SHA256, SHA1, MD5  |
| Grupo DH         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, Nenhum |
| Criptografia IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, nenhum    |
| Integridade do IPsec  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| Grupo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, nenhum 
| Tempo de vida da QM SA   | (**Opcional**: os valores padrão serão usados se não for especificados)<br>Segundos (inteiro; **mínimo de 300**/padrão de 27000 segundos)<br>KBytes (inteiro; **mín. de 1024** /padrão de 102400000 KBytes)   |
| Seletor de tráfego | UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, padrão$False, se não especificado)    |
|  |  |

> [!IMPORTANT]
> 1. **Se GCMAES é usado para o algoritmo de criptografia de IPsec, você deve selecionar hello GCMAES o mesmo algoritmo e comprimento de chave para integridade de IPsec; Por exemplo, usando GCMAES128 para ambos**
> 2. Tempo de vida do SA do modo principal IKEv2 é fixo em 28.800 segundos em gateways de VPN do Azure Olá
> 3. Configuração de "UsePolicyBasedTrafficSelectors" muito$ True em uma conexão configurará Olá VPN do Azure gateway tooconnect toopolicy VPN firewall baseado no local. Se você habilitar PolicyBasedTrafficSelectors, você precisa tooensure que seu dispositivo VPN tem seletores de tráfego correspondente Olá definidos com todas as combinações de seu local (gateway de rede local) de prefixos de rede de prefixos de rede virtual do Azure Olá, em vez de para qualquer. Por exemplo, se os prefixos de rede local são 10.1.0.0/16 e 10.2.0.0/16, e os prefixos de rede virtual são 192.168.0.0/16 e 172.16.0.0/16, você precisa toospecify Olá seletores de tráfego a seguir:
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

Consulte [Conectar dispositivos VPN baseados em várias políticas locais](vpn-gateway-connect-multiple-policybased-rm-ps.md) para saber mais sobre os seletores de tráfego baseados em políticas.

Olá a tabela a seguir lista Olá grupos Diffie-Hellman correspondentes com suporte pela política personalizada do hello:

| **Grupo Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Comprimento da chave** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | MODP de 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP de 1024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP de 2048 bits  |
| 19                        | ECP256                   | ECP256       | ECP de 256 bits    |
| 20                        | ECP384                   | ECP284       | ECP de 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP de 2048 bits  |

Consulte também[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) para obter mais detalhes.

## <a name ="crossprem"></a>Parte 3 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE

Esta seção orienta você pelas etapas de saudação da criação de uma conexão VPN S2S com uma política de IPsec/IKE. Olá etapas a seguir criam conexão Olá conforme mostrado no diagrama de saudação:

![política de S2S](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Consulte [Criar uma conexão VPN S2S](vpn-gateway-create-site-to-site-rm-powershell.md) para obter instruções passo a passo mais detalhadas para criar uma conexão VPN S2S.

### <a name="before"></a>Antes de começar

* Verifique se você tem uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instale os cmdlets do PowerShell do Azure Resource Manager hello. Consulte [visão geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.

### <a name="createvnet1"></a>Etapa 1 - Criar rede virtual hello, gateway de VPN e gateway de rede local

#### <a name="1-declare-your-variables"></a>1. Declare as variáveis

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Conecte-se a assinatura de tooyour e criar um novo grupo de recursos

Verifique se que você alternar Olá toouse de modo tooPowerShell cmdlets do Gerenciador de recursos. Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).

Abra o console do PowerShell e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Criar rede virtual hello, gateway de VPN e gateway de rede local

saudação de exemplo a seguir cria rede virtual hello, TestVNet1, com três sub-redes e gateway VPN hello. Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet. Se você usar outro nome, a criação do gateway falhará.

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

### <a name="s2sconnection"></a>Parte 2 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Criar uma política de IPsec/IKE

Olá, script de exemplo a seguir cria uma política de IPsec/IKE com hello algoritmos e os parâmetros a seguir:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, SA tempo de vida 7200 segundos & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

Se você usar GCMAES para IPsec, você deve usar Olá GCMAES o mesmo algoritmo e comprimento de chave de criptografia IPsec e integridade, por exemplo:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, SA Tempo de vida 7.200 segundos e 2.048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. Criar conexão de VPN S2S Olá com hello diretiva IPsec/IKE

Criar uma conexão VPN S2S e aplicar a diretiva de IPsec/IKE Olá criada anteriormente.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Opcionalmente, você pode adicionar "-UsePolicyBasedTrafficSelectors $True" toohello criar conexão cmdlet tooenable VPN Azure gateway tooconnect toopolicy dispositivos baseados em VPN no local, conforme descrito acima.

> [!IMPORTANT]
> Quando uma política de IPsec/IKE é especificada em uma conexão, o gateway de VPN do Azure Olá só enviar ou aceitar proposta de IPsec/IKE Olá com algoritmos de criptografia especificados e as restrições de chave que determinada conexão. Verifique se o dispositivo VPN local para conexão Olá usa ou aceita a combinação de política exata Olá, caso contrário túnel de VPN S2S Olá não estabelecerá.


## <a name ="vnet2vnet"></a>Parte 4 - Criar uma nova conexão de VNet para VNet com a política de IPsec/IKE

etapas de saudação da criação de uma conexão de rede virtual a rede com uma política de IPsec/IKE são semelhante toothat de uma conexão VPN S2S. Olá scripts de exemplo a seguir criam conexão Olá conforme mostrado no diagrama de saudação:

![política de V2V](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Consulte [Criar uma conexão VNet para VNet](vpn-gateway-vnet-vnet-rm-ps.md) para obter etapas mais detalhadas para criar uma conexão VNet para VNet. Você deve concluir [parte 3](#crossprem) toocreate configurar TestVNet1 e Olá Gateway VPN.

### <a name="createvnet2"></a>Etapa 1 - Criar rede virtual do segundo hello e gateway da VPN

#### <a name="1-declare-your-variables"></a>1. Declare as variáveis

Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

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

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Criar rede virtual do segundo hello e gateway da VPN no novo grupo de recursos Olá

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

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>Etapa 2: criar uma conexão de rede virtual toVNet com hello diretiva IPsec/IKE

Toohello semelhante conexão VPN S2S, criar uma política de IPsec/IKE, aplique toopolicy toohello nova conexão.

#### <a name="1-create-an-ipsecike-policy"></a>1. Criar uma política de IPsec/IKE

Olá, script de exemplo a seguir cria uma política de IPsec/IKE diferente com hello algoritmos e os parâmetros a seguir:
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, tempo de vida do SA 7200 segundos e 4096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. Criar conexões VNet para VNet com hello diretiva IPsec/IKE

Criar uma conexão de rede virtual a rede e aplicar a diretiva de IPsec/IKE Olá criado por você. Neste exemplo, ambos os gateways estão em Olá mesma assinatura. Portanto é possível toocreate e configurar as conexões com Olá a mesma diretiva de IPsec/IKE Olá mesma sessão do PowerShell.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> Quando uma política de IPsec/IKE é especificada em uma conexão, o gateway de VPN do Azure Olá só enviar ou aceitar proposta de IPsec/IKE Olá com algoritmos de criptografia especificados e as restrições de chave que determinada conexão. Verifique se Olá diretivas IPsec para ambas as conexões são Olá iguais, caso contrário, a conexão de rede virtual a rede não estabelecerá.

Depois de concluir essas etapas, conexão Olá é estabelecida em poucos minutos, e você terá Olá topologia de rede a seguir conforme mostrado no início da saudação:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Parte 5 - Atualizar política de IPsec/IKE para uma conexão

Olá última seção mostra a você como toomanage política IPsec/IKE para uma conexão existente S2S ou VNet para VNet. Exercício de saudação abaixo orienta Olá operações em uma conexão a seguir:

1. Mostrar política de IPsec/IKE de saudação de uma conexão
2. Adicionar ou atualizar a conexão de tooa de diretiva de IPsec/IKE Olá
3. Remover a diretiva de IPsec/IKE Olá de uma conexão

Olá mesmas etapas se aplicam tooboth S2S e conexões de rede virtual a rede.

> [!IMPORTANT]
> A política de IPsec/IKE tem suporte somente nos gateways de VPN baseados en rota *Standard* e *HighPerformance*. Ele não funciona no SKU do gateway básica Olá ou gateway VPN com base na política hello.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Mostrar política de IPsec/IKE de saudação de uma conexão

saudação de exemplo a seguir mostra como tooget Olá política IPsec/IKE configurada em uma conexão. os scripts de saudação também continuam de exercícios de saudação acima.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

comando último Olá lista política IPsec/IKE atual Olá configurada na conexão hello, se houver algum. Olá saída de exemplo a seguir destina-se a conexão de saudação:

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

Se não houver nenhuma política de IPsec/IKE configurada, Olá comando (PS > $connection6.policy) obtém vazio retornado. Isso não significa IPsec/IKE não está configurado na conexão hello, mas que não há nenhuma diretiva de IPsec/IKE personalizada. conexão real Olá usa a política de padrão de saudação negociada entre o dispositivo VPN de local e Olá gateway VPN do Azure.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Adicionar e atualizar uma política de IPsec/IKE para uma conexão

Olá etapas tooadd uma nova política ou atualização de uma política existente em uma conexão são Olá mesmo: criar uma nova política, aplique a nova conexão de toohello política hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable "UsePolicyBasedTrafficSelectors" ao conectar tooan local dispositivo VPN baseado em políticas, adicionar hello "-UsePolicyBaseTrafficSelectors" parâmetro toohello cmdlet, ou defina-o muito opção de saudação do $ toodisable False:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

Você pode obter conexão Olá toocheck novamente se a política de saudação é atualizada.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Você deve ver a saída de saudação da última linha de saudação, conforme mostrado no exemplo a seguir de saudação:

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

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Remover uma política de IPsec/IKE de uma conexão

Quando você remover a política personalizada de saudação de uma conexão, gateway de VPN do Azure Olá reverte back toohello [lista padrão de propostas de IPsec/IKE](vpn-gateway-about-vpn-devices.md) e nova negociação será iniciada novamente com o dispositivo VPN local.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

Você pode usar Olá mesmo toocheck de script se Olá política foi removida da conexão hello.

## <a name="next-steps"></a>Próximas etapas

Consulte [Conectar dispositivos VPN baseados em várias políticas locais](vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter mais detalhes sobre os seletores de tráfego baseado em políticas.

Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.
