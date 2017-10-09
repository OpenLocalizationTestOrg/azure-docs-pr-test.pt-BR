etapas de saudação para usar essa tarefa uma rede virtual com base nos valores Olá Olá lista de referências de configuração a seguir. Nomes e configurações adicionais também são descritos nesta lista. Não usamos essa lista diretamente em qualquer uma das etapas hello, embora adicionamos variáveis com base nos valores hello nesta lista. Você pode copiar Olá toouse de lista como referência, substituindo valores hello com seus próprios.

**Lista de referência de configuração**

* Nome da Rede Virtual = “TestVNet”
* Espaço de endereço da Rede Virtual = 192.168.0.0/16
* Grupo de recursos = “TestRG”
* Nome de Subnet1 = “FrontEnd” 
* Espaço de endereço de sub-rede1 = "192.168.1.0/24"
* Nome da Sub-rede do Gateway: “GatewaySubnet” Deve-se sempre nomear uma sub-rede do gateway como *GatewaySubnet*.
* Espaço de endereço da Sub-Rede do Gateway = “192.168.200.0/26”
* Região = “Leste dos EUA”
* Nome do Gateway = “GW”
* Nome do IP do Gateway = “GWIP”
* Nome da configuração de IP do Gateway = “gwipconf”
* Tipo = “ExpressRoute” Este tipo é necessário para uma configuração de ExpressRoute.
* Nome do IP público do Gateway = “gwpip”

## <a name="add-a-gateway"></a>Adicionar um gateway
1. Conecte-se tooyour assinatura do Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Declare as variáveis para este exercício. Ser tooedit-se de que as configurações de saudação tooreflect exemplo hello que você deseja toouse.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Armazenar o objeto de rede virtual hello como uma variável.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Adicione uma sub-rede de gateway tooyour rede Virtual. subrede Olá gateway deve ser nomeado "GatewaySubnet". Você deve criar uma sub-rede de gateway que seja /27 ou maior (/26, /25 etc.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Definir a configuração de saudação.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Armazenar a sub-rede de gateway hello como uma variável.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Solicite um endereço IP público. o endereço IP Hello é solicitado antes de criar o gateway de saudação. Não é possível especificar o endereço IP de saudação que você deseja toouse; ela é alocada dinamicamente. Você usará esse endereço IP na próxima seção de configuração hello. Olá AllocationMethod deve ser dinâmico.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Crie a configuração de saudação do seu gateway. configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello. Nesta etapa, você está especificando configuração Olá que será usada quando você criar hello gateway. Essa etapa não cria realmente objeto de gateway hello. Use o exemplo hello abaixo toocreate sua configuração de gateway.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Crie gateway de saudação. Nesta etapa, Olá **- GatewayType** é especialmente importante. Você deve usar o valor de saudação **ExpressRoute**. Depois de executar esses cmdlets, gateway Olá pode levar até 45 minutos ou mais toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Verifique se o gateway de saudação foi criado
Use Olá tooverify que Olá gateway foi criado de comandos a seguir:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Redimensionar um gateway
Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Você pode usar Olá Olá do comando toochange SKU de Gateway a seguir a qualquer momento.

> [!IMPORTANT]
> Esse comando não funciona para o gateway UltraPerformance. toochange gateway gateway tooan UltraPerformance, primeiro remova Olá existente do gateway de rota expressa e, em seguida, criar um novo gateway UltraPerformance. toodowngrade seu gateway de um gateway UltraPerformance, primeiro remova Olá UltraPerformance gateway e, em seguida, criar um novo gateway.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Remover um gateway
Use Olá comando tooremove um gateway a seguir:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```