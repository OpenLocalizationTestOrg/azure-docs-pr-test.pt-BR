---
title: "Conectar redes virtuais clássicas tooAzure VNets Gerenciador de recursos: PowerShell | Microsoft Docs"
description: "Saiba como toocreate uma conexão VPN entre clássico VNets e VNets Gerenciador de recursos usando o PowerShell e o Gateway de VPN"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Conectar redes virtuais de diferentes modelos de implantação usando o PowerShell



Este artigo mostra como tooconnect de clássico VNets tooResource tooallow Manager VNets Olá recursos localizados em toocommunicate de modelos de implantação separado Olá entre si. etapas Olá neste artigo usam o PowerShell, mas você também pode criar essa configuração usando Olá portal do Azure, selecionando o artigo Olá desta lista.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Conectar um tooa de rede virtual clássica VNet Gerenciador de recursos é semelhante tooconnecting uma VNet tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE. Você pode criar uma conexão entre redes virtuais em assinaturas e regiões diferentes. Você também pode conectar VNets que já têm redes de tooon locais de conexões, como gateway Olá que eles foram configurados com é dinâmica ou baseadas em rota. Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo. 

Se seus VNets estão em Olá mesma região, talvez você queira tooinstead considere conectá-los usando o emparelhamento de rede virtual. O emparelhamento Vnet não usa um gateway de VPN. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Antes de começar

Olá etapas a seguir orientam Olá configurações necessárias tooconfigure um gateway dinâmico ou baseadas em rota para cada rede virtual e criar uma conexão VPN entre os gateways de saudação. Essa configuração não dá suporte a gateways estáticos ou baseados em política.

### <a name="prerequisites"></a>Pré-requisitos

* Ambas as redes virtuais já foram criadas.
* intervalos de endereços Olá para Olá VNets não se sobrepõem uns com os outros, ou se sobrepõem com nenhum dos intervalos de saudação para outras conexões que gateways Olá podem estar conectados ao.
* Você instalou hello mais recente cmdlets do PowerShell. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações. Certifique-se de que instalar Olá gerenciamento de serviço (SM) e Olá cmdlets do Gerenciador de recursos (RM). 

### <a name="exampleref"></a>Configurações de exemplo

Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.

**Configurações da Rede Virtual clássica**

Nome da rede virtual = ClassicVNet  <br>
Local = Oeste dos EUA <br>
Espaços de Endereço da Rede Virtual = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
GatewaySubnet = 10.0.0.32/29 <br>
Nome da rede local = RMVNetLocal <br>
GatewayType = DynamicRouting

**Configurações de Rede Virtual do Resource Manager**

Nome da VNet = RMVNet  <br>
Grupo de recursos = RG1 <br>
Espaços de Endereço do IP da Rede Virtual = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Local = Leste dos EUA <br>
Nome do IP Público do Gateway = gwpip <br>
Gateway de Rede Local = ClassicVNetLocal <br>
Nome do Gateway de Rede Virtual = RMGateway <br>
Configuração de endereçamento IP do gateway = gwipconfig

## <a name="createsmgw"></a>Seção 1 - Configurar Olá VNet clássico
### <a name="part-1---download-your-network-configuration-file"></a>Parte 1 - Baixar o arquivo de configuração de rede
1. Faça logon no tooyour conta do Azure no console do PowerShell Olá com direitos elevados. Olá cmdlet a seguir solicita credenciais de logon Olá para sua conta do Azure. Após o logon, ele baixa as configurações de conta para que fiquem disponível tooAzure PowerShell. Você usar Olá toocomplete de cmdlets do PowerShell SM essa parte da configuração de saudação.

  ```powershell
  Add-AzureAccount
  ```
2. Exporte o arquivo de configuração de rede do Azure executando o comando a seguir de saudação. Você pode alterar o local de saudação do hello tooexport tooa diferentes local do arquivo se necessário.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Arquivo. XML de saudação abertos que você baixou tooedit-lo. Para obter um exemplo de arquivo de configuração de rede hello, consulte Olá [esquema de configuração de rede](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Parte 2 - Verifique a sub-rede de gateway Olá
Em Olá **VirtualNetworkSites** elemento, adicionar uma sub-rede de gateway tooyour VNet se já não foi criado. Ao trabalhar com o arquivo de configuração de rede hello, sub-rede de gateway Olá deve ser nomeado "GatewaySubnet" ou o Azure não pode reconhecer e usá-lo como uma sub-rede do gateway.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Exemplo:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Parte 3 - adicionar o site de rede local Olá
site de rede local Olá que adicionar representa Olá toowhich RM VNet que você deseja tooconnect. Adicionar um **LocalNetworkSites** arquivo toohello de elemento se ainda não existir. Nesse ponto na configuração de saudação Olá VPNGatewayAddress pode ser qualquer endereço IP público válido porque nós ainda não tiver criado o gateway Olá Olá VNet Gerenciador de recursos. Quando criamos o gateway hello, substituímos esse endereço IP de espaço reservado com hello correto endereço IP público que recebeu o gateway do RM toohello.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Parte 4: associar Olá VNet com o site de rede local Olá
Nesta seção, podemos especificar o site de rede local Olá que você deseja tooconnect Olá VNet para. Nesse caso, é Olá VNet Gerenciador de recursos que você referenciou anteriormente. Verifique se nomes de saudação corresponder. Esta etapa não cria um gateway. Ele especifica a rede local Olá Olá gateway será conectado ao.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Parte 5 - salvar arquivo hello e carregar
Salve o arquivo hello e importá-lo tooAzure executando o comando a seguir de saudação. Certifique-se de que alterar o caminho do arquivo hello conforme necessário para seu ambiente.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Você verá um resultado semelhante mostrando importação Olá foi bem-sucedida.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Parte 6 - criar gateway Olá

Antes de executar este exemplo, consulte toohello arquivo de configuração de rede que você baixou de Olá exata de nomes que o Azure espera toosee. arquivo de configuração de rede Olá contém valores de saudação para suas redes virtuais clássicas. Às vezes, nomes de saudação para clássico em que vnets são alterados no arquivo de configuração de rede Olá ao criar configurações de rede virtual clássicas Olá portal do Azure devido a diferenças toohello nos modelos de implantação de saudação. Por exemplo, se você usou hello Azure toocreate portal uma rede virtual clássica chamada 'VNet clássico' e criou em um grupo de recursos denominado 'ClassicRG', o nome de saudação que está contida no arquivo de configuração de rede de saudação é convertido too'Group VNet clássico ClassicRG'. Ao especificar o nome de saudação de uma rede virtual que contém espaços, use aspas ao redor do valor de saudação.


Use Olá exemplo toocreate um gateway de roteamento dinâmico a seguir:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Você pode verificar o status de saudação do gateway hello usando Olá **Get-AzureVNetGateway** cmdlet.

## <a name="creatermgw"></a>Seção 2: Configurar Olá gateway de rede virtual do RM
toocreate um gateway VPN para Olá RM VNet, Olá siga as instruções a seguir. Não inicie etapas Olá até depois de recuperar o endereço IP público de saudação para gateway Olá clássico da rede virtual. 

1. Faça logon no tooyour conta do Azure no console do PowerShell hello. Olá cmdlet a seguir solicita credenciais de logon Olá para sua conta do Azure. Após o logon, as configurações de conta são baixadas para que fiquem disponível tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Obtenha uma lista de suas assinaturas do Azure, se você tiver mais de uma assinatura.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Especifique que você deseja toouse de assinatura de saudação.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Criar um gateway de rede local. Em uma rede virtual, o gateway de rede local Olá geralmente se refere a tooyour no local. Nesse caso, o gateway de rede local Olá refere-se tooyour VNet clássico. Dê um nome pelo qual Azure pode consulte tooit e também especificar o prefixo do espaço de endereço de saudação. O Azure usa o prefixo de endereço IP de saudação especificar tooidentify tooyour de toosend qual tráfego local. Se você precisar tooadjust Olá aqui as informações mais tarde, antes de criar o gateway, você pode modificar os valores hello e exemplo hello execução novamente.
   
   **-Nome** é Olá nome você deseja que o gateway de rede local tooassign toorefer toohello.<br>
   **-AddressPrefix** é hello espaço de endereço para sua rede virtual clássica.<br>
   **-GatewayIpAddress** é o endereço IP público de saudação do gateway Olá clássico da rede virtual. Certifique-se de que a seguir Olá toochange tooreflect Olá endereço IP de exemplo.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Solicite um público IP endereço toobe toohello alocado gateway de rede virtual para Olá VNet Gerenciador de recursos. Não é possível especificar o endereço IP de saudação que você deseja toouse. endereço IP de saudação é alocado dinamicamente toohello gateway de rede virtual. No entanto, isso não significa alterações de endereço IP hello. somente tempo de saudação alterações de endereço IP do gateway de rede virtual hello quando é Olá gateway é excluído e recriado. Ele não altera em redimensionamento, redefinir ou outros internas manutenção/atualizações do gateway de saudação.

  Nesta etapa, também definimos uma variável usada em uma etapa posterior.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Verifique se sua rede virtual tem uma sub-rede de gateway. Se não houver sub-rede de gateway, adicione uma. Certifique-se de sub-rede de gateway Olá é denominado *GatewaySubnet*.
5. Recupere sub-rede Olá usada para o gateway de saudação executando o comando a seguir de saudação. Nesta etapa, podemos também definir uma variável toobe usado na próxima etapa de saudação.
   
   **-Nome** é Olá nome de sua VNet do Gerenciador de recursos.<br>
   **-ResourceGroupName** é o grupo de recursos Olá que hello rede virtual está associado. sub-rede de gateway Olá já deve existir para essa rede virtual e deve ser nomeado *GatewaySubnet* toowork corretamente.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Crie a configuração de endereçamento IP do gateway de saudação. configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello. Use Olá de exemplo a seguir toocreate sua configuração de gateway.

  Nesta etapa, Olá **- SubnetId** e **- PublicIpAddressId** parâmetros devem ser passados a propriedade id Olá da sub-rede hello e objetos de endereço IP, respectivamente. Você não pode usar uma cadeia de caracteres simples. Essas variáveis são definidas em Olá etapa toorequest um IP público e Olá etapa tooretrieve Olá sub-rede.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Crie gateway de rede virtual do Gerenciador de recursos de saudação executando Olá comando a seguir. Olá `-VpnType` devem ser *RouteBased*. Pode levar até 45 minutos ou mais para Olá gateway toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Copie o endereço IP público de saudação após a criação de gateway VPN hello. Você usá-lo quando você configura as configurações de rede local Olá para a sua rede virtual clássica. Você pode usar o hello endereço IP público do cmdlet tooretrieve Olá a seguir. Olá endereço IP público está listado no hello retorno como *IpAddress*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Seção 3: Modificar configurações de site local de rede virtual clássicas Olá

Nesta seção, você trabalha com hello VNet clássico. Substitua o endereço IP do espaço reservado Olá usado ao especificar as configurações de site local Olá que serão usado tooconnect toohello VNet Gerenciador de recursos de gateway. 

1. Exporte arquivo de configuração de rede hello.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Usando um editor de texto, modifique o valor de saudação para VPNGatewayAddress. Substitua o endereço IP de espaço reservado de saudação com endereço IP público de saudação do gateway do Gerenciador de recursos de saudação e, em seguida, salvar as alterações de saudação.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Saudação de importação modificado tooAzure de arquivo de configuração de rede.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Seção 4: Criar uma conexão entre os gateways Olá
Criar uma conexão entre os gateways Olá requer o PowerShell. Talvez você precise tooadd sua conta do Azure toouse Olá clássica versão Olá de cmdlets do PowerShell. Assim, use toodo **Add-AzureAccount**.

1. No console do PowerShell hello, defina a chave compartilhada. Antes de executar os cmdlets de hello, consulte toohello arquivo de configuração de rede que você baixou de Olá exata de nomes que o Azure espera toosee. Ao especificar o nome de saudação de uma rede virtual que contém espaços, use aspas ao redor do valor de saudação.<br><br>No exemplo a seguir, **- VNetName** é o nome de saudação do hello clássico VNet e **- LocalNetworkSiteName** é Olá nome especificado para o site de rede local hello. Olá **- SharedKey** é um valor que você gera e especificar. No exemplo hello, usamos 'abc123', mas você pode gerar e usar algo mais complexas. Olá importante é esse valor de saudação que você especificar aqui deve ser Olá que mesmo valor que você especificar na próxima etapa do hello quando você criar sua conexão. Olá retorno deve mostrar **Status: bem-sucedida**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Crie conexão de VPN Olá executando Olá comandos a seguir:
   
  Definir variáveis de saudação.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Crie conexão hello. Observe que Olá **- ConnectionType** é IPsec, não Vnet2Vnet.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Seção 5: Verificar suas conexões

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>conexão de saudação tooverify de seu tooyour de rede virtual clássica VNet Gerenciador de recursos

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Portal do Azure

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>conexão de saudação tooverify de tooyour sua VNet Gerenciador de recursos de rede virtual clássica

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Portal do Azure

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

