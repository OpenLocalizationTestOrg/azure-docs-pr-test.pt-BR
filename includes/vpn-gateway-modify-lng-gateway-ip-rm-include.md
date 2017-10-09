### <span data-ttu-id="a1309-101"><a name="gwipnoconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - nenhuma conexão de gateway</span><span class="sxs-lookup"><span data-stu-id="a1309-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="a1309-102">Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="a1309-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="a1309-103">Use toomodify de exemplo hello um gateway de rede local que não tem uma conexão de gateway.</span><span class="sxs-lookup"><span data-stu-id="a1309-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="a1309-104">Ao modificar esse valor, você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a1309-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="a1309-105">Citar se toouse Olá existente do seu gateway de rede local nas configurações atuais da ordem toooverwrite hello.</span><span class="sxs-lookup"><span data-stu-id="a1309-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="a1309-106">Se você usar um nome diferente, você pode criar um novo gateway de rede local, em vez de substituir Olá existente.</span><span class="sxs-lookup"><span data-stu-id="a1309-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="a1309-107"><a name="gwipwithconnection"></a>gateway de rede local toomodify Olá 'GatewayIpAddress' - conexão de gateway existente</span><span class="sxs-lookup"><span data-stu-id="a1309-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="a1309-108">Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="a1309-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="a1309-109">Se uma conexão de gateway já existir, você primeiro precisa tooremove conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1309-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="a1309-110">Após a conexão de saudação for removido, você pode modificar o endereço IP do gateway de saudação e recriar uma nova conexão.</span><span class="sxs-lookup"><span data-stu-id="a1309-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="a1309-111">Você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a1309-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="a1309-112">Isso resulta em algum tempo de inatividade para a conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="a1309-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="a1309-113">Ao modificar o endereço IP do gateway hello, gateway VPN Olá toodelete não é necessário.</span><span class="sxs-lookup"><span data-stu-id="a1309-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="a1309-114">Você só precisa de conexão de saudação tooremove.</span><span class="sxs-lookup"><span data-stu-id="a1309-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="a1309-115">Remova conexão hello.</span><span class="sxs-lookup"><span data-stu-id="a1309-115">Remove hello connection.</span></span> <span data-ttu-id="a1309-116">Você pode localizar o nome de saudação da sua conexão usando o cmdlet Olá 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="a1309-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="a1309-117">Modifique o valor de 'GatewayIpAddress' hello.</span><span class="sxs-lookup"><span data-stu-id="a1309-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="a1309-118">Você também pode modificar os prefixos de endereço de saudação em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a1309-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="a1309-119">Citar se toouse Olá existente de suas configurações atuais do local de rede gateway toooverwrite hello.</span><span class="sxs-lookup"><span data-stu-id="a1309-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="a1309-120">Se você não fizer isso, você criar um novo gateway de rede local, em vez de substituir Olá existente.</span><span class="sxs-lookup"><span data-stu-id="a1309-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="a1309-121">Crie conexão hello.</span><span class="sxs-lookup"><span data-stu-id="a1309-121">Create hello connection.</span></span> <span data-ttu-id="a1309-122">Neste exemplo, configuramos um tipo de conexão IPsec.</span><span class="sxs-lookup"><span data-stu-id="a1309-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="a1309-123">Ao recriar sua conexão, use o tipo de conexão de saudação que é especificado para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="a1309-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="a1309-124">Para tipos de conexão adicionais, consulte Olá [cmdlet do PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="a1309-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="a1309-125">nome da VirtualNetworkGateway tooobtain hello, você pode executar Olá 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a1309-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="a1309-126">Definir variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1309-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="a1309-127">Crie conexão hello.</span><span class="sxs-lookup"><span data-stu-id="a1309-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```