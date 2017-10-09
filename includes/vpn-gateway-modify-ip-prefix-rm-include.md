### <span data-ttu-id="1e77b-101"><a name="noconnection"></a>prefixos de endereço IP da gateway de rede local toomodify - nenhuma conexão de gateway</span><span class="sxs-lookup"><span data-stu-id="1e77b-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="1e77b-102">prefixos de endereço adicional tooadd:</span><span class="sxs-lookup"><span data-stu-id="1e77b-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="1e77b-103">prefixos de endereço tooremove:</span><span class="sxs-lookup"><span data-stu-id="1e77b-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="1e77b-104">Omitir os prefixos de saudação que não é mais necessário.</span><span class="sxs-lookup"><span data-stu-id="1e77b-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="1e77b-105">Neste exemplo, não é necessário prefixar 20.0.0.0/24 (de saudação exemplo anterior), para que podemos atualizar o gateway de rede local Olá, excluindo esse prefixo.</span><span class="sxs-lookup"><span data-stu-id="1e77b-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="1e77b-106"><a name="withconnection"></a>toomodify local de rede gateway prefixos de endereço IP - existente de conexão de gateway</span><span class="sxs-lookup"><span data-stu-id="1e77b-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="1e77b-107">Se você tiver uma conexão de gateway e deseja tooadd ou remove os prefixos de endereço IP de saudação contidos no seu gateway de rede local, você precisa Olá toodo etapas, na ordem a seguir.</span><span class="sxs-lookup"><span data-stu-id="1e77b-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="1e77b-108">Isso resulta em algum tempo de inatividade para a conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="1e77b-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="1e77b-109">Ao modificar prefixos de endereço IP, gateway VPN Olá toodelete não é necessário.</span><span class="sxs-lookup"><span data-stu-id="1e77b-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="1e77b-110">Você só precisa de conexão de saudação tooremove.</span><span class="sxs-lookup"><span data-stu-id="1e77b-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="1e77b-111">Remova conexão hello.</span><span class="sxs-lookup"><span data-stu-id="1e77b-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="1e77b-112">Modifique os prefixos de endereço de saudação do seu gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="1e77b-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="1e77b-113">Definir variável Olá Olá LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="1e77b-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="1e77b-114">Modifique os prefixos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e77b-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="1e77b-115">Crie conexão hello.</span><span class="sxs-lookup"><span data-stu-id="1e77b-115">Create hello connection.</span></span> <span data-ttu-id="1e77b-116">Neste exemplo, configuramos um tipo de conexão IPsec.</span><span class="sxs-lookup"><span data-stu-id="1e77b-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="1e77b-117">Ao recriar sua conexão, use o tipo de conexão de saudação que é especificado para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="1e77b-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="1e77b-118">Para tipos de conexão adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="1e77b-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="1e77b-119">Definir variável Olá Olá VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="1e77b-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="1e77b-120">Crie conexão hello.</span><span class="sxs-lookup"><span data-stu-id="1e77b-120">Create hello connection.</span></span> <span data-ttu-id="1e77b-121">Este exemplo usa a variável de saudação $local definido na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="1e77b-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```