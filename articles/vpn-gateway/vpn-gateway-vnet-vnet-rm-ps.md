---
title: 'Conectar uma rede virtual de tooanother de rede virtual do Azure: PowerShell | Microsoft Docs'
description: Este artigo mostra como conectar redes virtuais em conjunto usando o PowerShell e o Gerenciador de Recursos do Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Configurar uma conexão gateway de VPN de Vnet pra VNet usando o PowerShell

Este artigo mostra como toocreate uma conexão de gateway VPN entre redes virtuais. Olá redes virtuais podem ser Olá mesmas ou em diferentes regiões e de Olá mesmo ou em assinaturas diferentes. Quando conexão VNets de assinaturas diferentes, assinaturas de saudação não precisarem toobe associado Olá mesmo locatário do Active Directory. 

etapas de saudação neste artigo aplicam o modelo de implantação do Gerenciador de recursos de toohello e usam o PowerShell. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI do Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conectar modelos de implantação diferentes – portal do Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conectar modelos de implantação diferentes - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma VNet tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE. Se seus VNets estão em Olá mesma região, talvez você queira tooconsider conectá-los usando o emparelhamento de rede virtual. O emparelhamento Vnet não usa um gateway de VPN. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).

Você pode combinar a comunicação de VNet a VNet usando configurações multissite. Isso permite que você estabeleça topologias de rede que combinem conectividade entre instalações com conectividade de rede intervirtual, como mostrado no diagrama a seguir de saudação:

![Sobre as conexões](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Por que conectar redes virtuais?

Você talvez queira redes virtuais tooconnect para Olá motivos a seguir:

* **Redundância geográfica entre regiões e presença geográfica**

  * Você pode configurar sua própria sincronização ou replicação geográfica com conectividade segura sem passar por pontos de extremidade voltados para a Internet.
  * Com o Balanceador de Carga e o Gerenciador de Tráfego do Azure você pode configurar a carga de trabalho de alta disponibilidade com redundância geográfica em várias regiões do Azure. Um exemplo importante é tooset backup SQL Always On com grupos de disponibilidade espalhados por várias regiões do Azure.
* **Aplicativos multicamadas regionais com limite administrativo ou de isolamento**

  * Olá na mesma região, você pode configurar aplicativos de várias camadas com várias redes virtuais conectadas devido tooisolation ou requisitos administrativos.

Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo.

## <a name="which-set-of-steps-should-i-use"></a>Qual conjunto de etapas devo usar?

Neste artigo, você verá dois conjuntos de etapas diferentes. Um conjunto de etapas para [Olá de VNets que residem na mesma assinatura](#samesub)e outro para [VNets que residem em diferentes assinaturas](#difsub). Olá diferença importante entre conjuntos de saudação é se você pode criar e configurar todos os recursos de rede e gateway virtuais dentro Olá mesma sessão do PowerShell.

Hello etapas neste artigo utilizar variáveis que são declaradas no início de cada seção Olá. Se você já estiver trabalhando com VNets existentes, modificar configurações de saudação de tooreflect do hello variáveis no seu ambiente. Se você deseja resolução de nomes para suas redes virtuais, confira [a Resolução de nomes](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>Como a tooconnect VNets que estão em Olá mesma assinatura

![Diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Antes de começar

Antes de começar, é necessário a versão mais recente do tooinstall Olá Olá Azure o Gerenciador de recursos de cmdlets do PowerShell, pelo menos 4.0 ou posteriores. Para obter mais informações sobre como instalar os cmdlets do PowerShell hello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Etapa 1 – Planejar os intervalos de endereços IP

Olá etapas a seguir, criamos duas redes virtuais junto com suas configurações e sub-redes do respectivos gateway. Em seguida, criamos uma conexão VPN entre hello duas VNets. É importante tooplan intervalos de endereços IP Olá para sua configuração de rede. Lembre-se de que você deve garantir que nenhum de seus intervalos de VNet ou intervalos de rede local se sobreponham de forma alguma. Nestes exemplos, não incluímos um servidor DNS. Se você deseja resolução de nomes para suas redes virtuais, confira [a Resolução de nomes](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Usamos Olá valores nos exemplos Olá a seguir:

**Valores para TestVNet1:**

* Nome da rede virtual: TestVNet1
* Grupo de recursos: TestRG1
* Local: Leste dos EUA
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* IP público: VNet1GWIP
* VpnType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valores para TestVNet4:**

* Nome da rede virtual: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupo de recursos: TestRG4
* Local: Oeste dos EUA
* GatewayName: VNet4GW
* IP público: VNet4GWIP
* VpnType: RouteBased
* Conexão: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Etapa 2: Criar e configurar o TestVNet1

1. Declare as variáveis. Este exemplo declara variáveis hello usando valores de saudação para este exercício. Na maioria dos casos, você deve substituir os valores hello com seus próprios. No entanto, você pode usar essas variáveis, se você estiver executando a saudação etapas toobecome familiarizado com esse tipo de configuração. Modificar variáveis de saudação se necessário, em seguida, copiar e colá-los em seu console do PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

  ```powershell
  Login-AzureRmAccount
  ```

  Verificar as assinaturas de saudação para conta de saudação.

  ```powershell
  Get-AzureRmSubscription
  ```

  Especifique que você deseja toouse de assinatura de saudação.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Crie um novo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Crie configurações de sub-rede para TestVNet1 de saudação. Este exemplo cria uma rede virtual denominada TestVNet1 e três sub-redes, uma chamada GatewaySubnet, outra FrontEnd e outra Backend. Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet. Se você usar outro nome, a criação do gateway falhará.

  Olá exemplo a seguir usa variáveis de saudação que você definiu anteriormente. Neste exemplo, a sub-rede de gateway de saudação está usando um /27. Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando pelo menos /28 ou /27. Isso permitirá suficiente endereços tooaccommodate possíveis configurações adicionais que você pode em Olá futuras.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Crie a TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Solicite um público endereço toobe toohello alocado gateway IP que você criará para sua rede virtual. Observe que Olá AllocationMethod é dinâmico. Não é possível especificar o endereço IP de saudação que você deseja toouse. É gateway tooyour alocada dinamicamente. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Crie a configuração do gateway hello. configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello. Use toocreate do exemplo hello sua configuração de gateway.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Crie gateway Olá para TestVNet1. Nesta etapa, você pode criar o gateway de rede virtual Olá para sua TestVNet1. As configurações de rede virtual com rede virtual exigem um VpnType RouteBased. Criar um gateway pode levar até 45 minutos ou mais, dependendo da SKU do gateway Olá selecionado.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Etapa 3: criar e configurar TestVNet4

Depois de configurar TestVNet1, crie TestVNet4. Siga as etapas de saudação abaixo, substituindo valores hello com seu próprio quando necessário. Esta etapa pode ser feita em Olá mesma sessão do PowerShell porque ele está em Olá mesmo assinatura.

1. Declare as variáveis. Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Crie um novo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Crie configurações de sub-rede para TestVNet4 de saudação.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Crie a TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Solicite um endereço IP público.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Crie a configuração do gateway hello.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Crie hello TestVNet4 gateway. Criar um gateway pode levar até 45 minutos ou mais, dependendo da SKU do gateway Olá selecionado.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Etapa 4 - criar conexões Olá

1. Obter ambos os gateways de rede virtual. Se ambos os gateways Olá Olá mesma assinatura, como estão no exemplo hello, você pode concluir esta etapa no hello mesma sessão do PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Crie conexão de tooTestVNet4 TestVNet1 hello. Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet4. Você verá uma chave compartilhada referenciada nos exemplos de saudação. Você pode usar seus próprios valores para a chave compartilhada hello. Olá importante é chave compartilhada Olá deve corresponder para ambas as conexões. Criar uma conexão pode demorar um pouco ao toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Crie conexão de tooTestVNet1 TestVNet4 hello. Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet4 tooTestVNet1. Certifique-se de saudação compartilhada chaves correspondentes. conexão Olá será estabelecida após alguns minutos.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Verifique a conexão. Consulte a seção Olá [como tooverify sua conexão](#verify).

## <a name="difsub"></a>Como tooconnect VNets que estão em diferentes assinaturas

![Diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

Nesse cenário, conectamos TestVNet1 e TestVNet5. TestVNet1 e TestVNet5 residem em uma assinatura diferente. Olá assinaturas não precisem toobe associado Olá mesmo locatário do Active Directory. diferença de saudação entre essas etapas e o conjunto anterior de saudação é que algumas das etapas de configuração de saudação necessário toobe executada em uma sessão separada do PowerShell no contexto de saudação da assinatura segundo hello. Especialmente quando assinaturas de saudação dois pertencem toodifferent organizações.

### <a name="step-5---create-and-configure-testvnet1"></a>Etapa 5: criar e configurar o TestVNet1

Você deve concluir [etapa 1](#Step1) e [etapa 2](#Step2) de saudação anterior seção toocreate e configurar TestVNet1 e hello Gateway VPN para TestVNet1. Para essa configuração, você não é necessário toocreate TestVNet4 da seção anterior do hello, embora se você criá-lo, ele não está em conflito com estas etapas. Depois de concluir a etapa 1 e 2, continue com a etapa 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Etapa 6 - Verifique se os intervalos de endereços IP Olá

É importante toomake-se de que o espaço de endereço IP de saudação do hello nova rede virtual, TestVNet5, não coincide com nenhum dos seus intervalos de VNet ou intervalos de gateway de rede local. Neste exemplo, redes virtuais Olá podem pertencer toodifferent organizações. Para este exercício, você pode usar Olá Olá TestVNet5 valores a seguir:

**Valores para TestVNet5:**

* Nome da rede virtual: TestVNet5
* Grupo de recursos: TestRG5
* Local: Leste do Japão
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* IP público: VNet5GWIP
* VpnType: RouteBased
* Connection: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Etapa 7: criar e configurar TestVNet5

Esta etapa deve ser feita no contexto de saudação da nova assinatura de saudação. Esta parte pode ser executada pelo administrador Olá em uma organização diferente que possui assinatura hello.

1. Declare as variáveis. Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Conecte-se toosubscription 5. Abra o console do PowerShell e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

  ```powershell
  Login-AzureRmAccount
  ```

  Verificar as assinaturas de saudação para conta de saudação.

  ```powershell
  Get-AzureRmSubscription
  ```

  Especifique que você deseja toouse de assinatura de saudação.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Crie um novo grupo de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Crie configurações de sub-rede para TestVNet5 de saudação.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Crie a TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Solicite um endereço IP público.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Crie a configuração do gateway hello.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Crie hello TestVNet5 gateway.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Etapa 8 — criar conexões Olá

Neste exemplo, como gateways Olá estão em assinaturas diferentes do hello, você dividiremos esta etapa em duas sessões do PowerShell marcadas como [1 assinatura] e [5 assinatura].

1. **[Assinatura 1]**  Obter gateway de rede virtual Olá para 1 de assinatura. Logon e se conectar tooSubscription 1 antes de executar o exemplo a seguir de saudação:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Copiar saída Olá Olá elementos a seguir e enviar esses administrador toohello de 5 de assinatura por email ou outro método.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Esses dois elementos terão valores toohello semelhante a saída de exemplo a seguir:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Assinatura 5]**  Obter gateway de rede virtual Olá para 5 de assinatura. Logon e se conectar tooSubscription 5 antes de executar o exemplo a seguir de saudação:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Copiar saída Olá Olá elementos a seguir e enviar esses administrador toohello 1 assinatura via email ou outro método.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Esses dois elementos terão valores toohello semelhante a saída de exemplo a seguir:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Assinatura 1]**  Criar conexão Olá TestVNet1 tooTestVNet5. Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet5. diferença de saudação aqui é que vnet5gw $ não podem ser obtidos diretamente, porque ele está em uma assinatura diferente. Você precisará toocreate um novo objeto do PowerShell com valores hello comunicados de 1 de assinatura de etapas de saudação acima. Use o exemplo hello abaixo. Substitua seus próprios valores hello nome, Id e uma chave compartilhada. Olá importante é chave compartilhada Olá deve corresponder para ambas as conexões. Criar uma conexão pode demorar um pouco ao toocomplete.

  Conecte-se tooSubscription 1 antes de executar o exemplo a seguir de saudação:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Assinatura 5]**  Criar conexão Olá TestVNet5 tooTestVNet1. Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet5 tooTestVNet1. Olá mesmo processo de criação de um objeto do PowerShell com base nos valores hello obtidos 1 assinatura se aplica aqui também. Nesta etapa, certifique-se de que correspondem chaves Olá compartilhado.

  Conecte-se tooSubscription 5 antes de executar o exemplo a seguir de saudação:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Como tooverify uma conexão

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas

* Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Consulte Olá [documentação de máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obter mais informações.
* Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
