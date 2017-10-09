### <a name="noconnection"></a>prefixos de endereço IP da gateway de rede local toomodify - nenhuma conexão de gateway

prefixos de endereço adicional tooadd:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

prefixos de endereço tooremove:<br>
Omitir os prefixos de saudação que não é mais necessário. Neste exemplo, não é necessário prefixar 20.0.0.0/24 (de saudação exemplo anterior), para que podemos atualizar o gateway de rede local Olá, excluindo esse prefixo.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify local de rede gateway prefixos de endereço IP - existente de conexão de gateway

Se você tiver uma conexão de gateway e deseja tooadd ou remove os prefixos de endereço IP de saudação contidos no seu gateway de rede local, você precisa Olá toodo etapas, na ordem a seguir. Isso resulta em algum tempo de inatividade para a conexão VPN. Ao modificar prefixos de endereço IP, gateway VPN Olá toodelete não é necessário. Você só precisa de conexão de saudação tooremove.


1. Remova conexão hello.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Modifique os prefixos de endereço de saudação do seu gateway de rede local.
   
  Definir variável Olá Olá LocalNetworkGateway.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Modifique os prefixos de saudação.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Crie conexão hello. Neste exemplo, configuramos um tipo de conexão IPsec. Ao recriar sua conexão, use o tipo de conexão de saudação que é especificado para sua configuração. Para tipos de conexão adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.
   
  Definir variável Olá Olá VirtualNetworkGateway.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Crie conexão hello. Este exemplo usa a variável de saudação $local definido na etapa 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```