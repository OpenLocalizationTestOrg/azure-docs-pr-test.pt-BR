### <span data-ttu-id="63975-101"><a name="noconnection"></a>Para modificar prefixos de endereço IP de gateway de rede local - sem conexão de gateway</span><span class="sxs-lookup"><span data-stu-id="63975-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="63975-102">Para adicionar prefixos de endereço adicional:</span><span class="sxs-lookup"><span data-stu-id="63975-102">To add additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="63975-103">Para remover os prefixo de endereço:</span><span class="sxs-lookup"><span data-stu-id="63975-103">To remove address prefixes:</span></span><br>
<span data-ttu-id="63975-104">Exclua os prefixos de que você não precisa mais.</span><span class="sxs-lookup"><span data-stu-id="63975-104">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="63975-105">Neste exemplo, não é mais necessário prefixar 20.0.0.0/24 (do exemplo anterior), portanto, atualizaremos o gateway de rede local e excluiremos o prefixo.</span><span class="sxs-lookup"><span data-stu-id="63975-105">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we update the local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="63975-106"><a name="withconnection"></a>Para modificar prefixos de endereço IP de gateway de rede local - conexão de gateway existente</span><span class="sxs-lookup"><span data-stu-id="63975-106"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="63975-107">Se você possui uma conexão de gateway e deseja adicionar ou remover os prefixos do endereço IP contidos no gateway de rede local, você precisará executar as etapas a seguir nessa ordem.</span><span class="sxs-lookup"><span data-stu-id="63975-107">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="63975-108">Isso resulta em algum tempo de inatividade para a conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="63975-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="63975-109">Ao modificar prefixos de endereço IP, você não precisa excluir o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="63975-109">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="63975-110">Você precisa apenas remover a conexão.</span><span class="sxs-lookup"><span data-stu-id="63975-110">You only need to remove the connection.</span></span>


1. <span data-ttu-id="63975-111">Remova a conexão.</span><span class="sxs-lookup"><span data-stu-id="63975-111">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="63975-112">Modifique os prefixos do endereço para seu gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="63975-112">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="63975-113">Defina a variável para LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="63975-113">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="63975-114">Modifique os prefixos.</span><span class="sxs-lookup"><span data-stu-id="63975-114">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="63975-115">Crie a conexão.</span><span class="sxs-lookup"><span data-stu-id="63975-115">Create the connection.</span></span> <span data-ttu-id="63975-116">Neste exemplo, configuramos um tipo de conexão IPsec.</span><span class="sxs-lookup"><span data-stu-id="63975-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="63975-117">Quando você recriar a conexão, use o tipo de conexão especificado para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="63975-117">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="63975-118">Para outros tipos de conexão, consulte a página [Cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) .</span><span class="sxs-lookup"><span data-stu-id="63975-118">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="63975-119">Defina a variável para VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="63975-119">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="63975-120">Crie a conexão.</span><span class="sxs-lookup"><span data-stu-id="63975-120">Create the connection.</span></span> <span data-ttu-id="63975-121">Este exemplo usa a variável $local que você definiu na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="63975-121">This example uses the variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```