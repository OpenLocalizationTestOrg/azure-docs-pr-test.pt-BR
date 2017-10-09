### <a name="gwipnoconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - nenhuma conexão de gateway

Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram. Use toomodify de exemplo hello um gateway de rede local que não tem uma conexão de gateway.

Ao modificar esse valor, você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente. Citar se toouse Olá existente do seu gateway de rede local nas configurações atuais da ordem toooverwrite hello. Se você usar um nome diferente, você pode criar um novo gateway de rede local, em vez de substituir Olá existente.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - conexão de gateway existente

Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram. Se uma conexão de gateway já existir, você primeiro precisa tooremove conexão de saudação. Após a conexão de saudação for removido, você pode modificar o endereço IP do gateway de saudação e recriar uma nova conexão. Você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente. Isso resulta em algum tempo de inatividade para a conexão VPN. Ao modificar o endereço IP do gateway hello, gateway VPN Olá toodelete não é necessário. Você só precisa de conexão de saudação tooremove.
 

1. Remova conexão hello. Você pode localizar o nome de saudação da sua conexão usando o cmdlet Olá 'Get-AzureRmVirtualNetworkGatewayConnection'.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Modifique o valor de 'GatewayIpAddress' hello. Você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente. Citar se toouse Olá existente de suas configurações atuais do local de rede gateway toooverwrite hello. Se você não fizer isso, você criar um novo gateway de rede local, em vez de substituir Olá existente.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Crie conexão hello. Neste exemplo, configuramos um tipo de conexão IPsec. Ao recriar sua conexão, use o tipo de conexão de saudação que é especificado para sua configuração. Para tipos de conexão adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.  nome da VirtualNetworkGateway tooobtain hello, você pode executar Olá 'Get-AzureRmVirtualNetworkGateway' cmdlet.
   
    Definir variáveis de saudação.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Crie conexão hello.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```