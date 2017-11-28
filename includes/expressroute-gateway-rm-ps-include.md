<span data-ttu-id="e3346-101">As etapas para essa tarefa usam uma VNet com base nos valores na lista de referência de configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3346-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="e3346-102">Nomes e configurações adicionais também são descritos nesta lista.</span><span class="sxs-lookup"><span data-stu-id="e3346-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="e3346-103">Não usamos essa lista diretamente em nenhuma uma das etapas, embora adicionemos variáveis com base nos valores contidos nessa lista.</span><span class="sxs-lookup"><span data-stu-id="e3346-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="e3346-104">É possível fazer uma cópia da lista para usá-la como referência, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="e3346-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="e3346-105">**Lista de referência de configuração**</span><span class="sxs-lookup"><span data-stu-id="e3346-105">**Configuration reference list**</span></span>

* <span data-ttu-id="e3346-106">Nome da Rede Virtual = “TestVNet”</span><span class="sxs-lookup"><span data-stu-id="e3346-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="e3346-107">Espaço de endereço da Rede Virtual = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e3346-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="e3346-108">Grupo de recursos = “TestRG”</span><span class="sxs-lookup"><span data-stu-id="e3346-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="e3346-109">Nome de Subnet1 = “FrontEnd”</span><span class="sxs-lookup"><span data-stu-id="e3346-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="e3346-110">Espaço de endereço de sub-rede1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="e3346-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="e3346-111">Nome da Sub-rede do Gateway: “GatewaySubnet” Deve-se sempre nomear uma sub-rede do gateway como *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="e3346-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="e3346-112">Espaço de endereço da Sub-Rede do Gateway = “192.168.200.0/26”</span><span class="sxs-lookup"><span data-stu-id="e3346-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="e3346-113">Região = “Leste dos EUA”</span><span class="sxs-lookup"><span data-stu-id="e3346-113">Region = "East US"</span></span>
* <span data-ttu-id="e3346-114">Nome do Gateway = “GW”</span><span class="sxs-lookup"><span data-stu-id="e3346-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="e3346-115">Nome do IP do Gateway = “GWIP”</span><span class="sxs-lookup"><span data-stu-id="e3346-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="e3346-116">Nome da configuração de IP do Gateway = “gwipconf”</span><span class="sxs-lookup"><span data-stu-id="e3346-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="e3346-117">Tipo = “Rota Expressa” Este tipo é necessário para uma configuração de Rota Expressa.</span><span class="sxs-lookup"><span data-stu-id="e3346-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="e3346-118">Nome do IP público do Gateway = “gwpip”</span><span class="sxs-lookup"><span data-stu-id="e3346-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="e3346-119">Adicionar um gateway</span><span class="sxs-lookup"><span data-stu-id="e3346-119">Add a gateway</span></span>
1. <span data-ttu-id="e3346-120">Conecte-se à sua Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3346-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="e3346-121">Declare as variáveis para este exercício.</span><span class="sxs-lookup"><span data-stu-id="e3346-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="e3346-122">Lembre-se de editar o exemplo para que elas reflitam as configurações que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e3346-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="e3346-123">Armazene o objeto de rede virtual como uma variável.</span><span class="sxs-lookup"><span data-stu-id="e3346-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="e3346-124">Adicione uma sub-rede de gateway à sua Rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="e3346-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="e3346-125">A sub-rede de gateway deve ser nomeada “GatewaySubnet”.</span><span class="sxs-lookup"><span data-stu-id="e3346-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="e3346-126">Você deve criar uma sub-rede de gateway que seja /27 ou maior (/26, /25 etc.).</span><span class="sxs-lookup"><span data-stu-id="e3346-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="e3346-127">Defina a configuração.</span><span class="sxs-lookup"><span data-stu-id="e3346-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="e3346-128">Armazene a sub-rede de gateway como uma variável.</span><span class="sxs-lookup"><span data-stu-id="e3346-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="e3346-129">Solicite um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="e3346-129">Request a public IP address.</span></span> <span data-ttu-id="e3346-130">O endereço IP é solicitado antes da criação do gateway.</span><span class="sxs-lookup"><span data-stu-id="e3346-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="e3346-131">Não é possível especificar o endereço IP que você deseja usar; ele é alocado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e3346-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="e3346-132">Você usará esse endereço IP na próxima seção de configuração.</span><span class="sxs-lookup"><span data-stu-id="e3346-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="e3346-133">O AllocationMethod deve ser Dynamic.</span><span class="sxs-lookup"><span data-stu-id="e3346-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="e3346-134">Crie a configuração de seu gateway.</span><span class="sxs-lookup"><span data-stu-id="e3346-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="e3346-135">A configuração do gateway define a sub-rede e o endereço IP público a serem usados.</span><span class="sxs-lookup"><span data-stu-id="e3346-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="e3346-136">Nesta etapa, você especificará a configuração que será usada quando o gateway for criado.</span><span class="sxs-lookup"><span data-stu-id="e3346-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="e3346-137">Essa etapa não cria, de fato, o objeto de gateway.</span><span class="sxs-lookup"><span data-stu-id="e3346-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="e3346-138">Use o exemplo a seguir para criar a configuração do gateway.</span><span class="sxs-lookup"><span data-stu-id="e3346-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="e3346-139">Crie o gateway.</span><span class="sxs-lookup"><span data-stu-id="e3346-139">Create the gateway.</span></span> <span data-ttu-id="e3346-140">Nesta etapa, o **-GatewayType** é especialmente importante.</span><span class="sxs-lookup"><span data-stu-id="e3346-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="e3346-141">É necessário usar o valor **Rota Expressa**.</span><span class="sxs-lookup"><span data-stu-id="e3346-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="e3346-142">Observe que, depois de executar esses cmdlets, o gateway pode levar 45 minutos ou mais para ser criado.</span><span class="sxs-lookup"><span data-stu-id="e3346-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="e3346-143">Verificar se o gateway foi criado</span><span class="sxs-lookup"><span data-stu-id="e3346-143">Verify the gateway was created</span></span>
<span data-ttu-id="e3346-144">Use os comandos a seguir para verificar se o gateway foi criado:</span><span class="sxs-lookup"><span data-stu-id="e3346-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="e3346-145">Redimensionar um gateway</span><span class="sxs-lookup"><span data-stu-id="e3346-145">Resize a gateway</span></span>
<span data-ttu-id="e3346-146">Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="e3346-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="e3346-147">Você pode usar o comando a seguir para alterar a SKU de gateway a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e3346-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3346-148">Esse comando não funciona para o gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="e3346-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="e3346-149">Para alterar o gateway para um gateway UltraPerformance, primeiro remova o gateway do ExpressRoute existente e crie um novo gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="e3346-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="e3346-150">Para fazer downgrade do gateway de um gateway UltraPerformance, primeiro remova o gateway UltraPerformance e crie um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="e3346-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="e3346-151">Remover um gateway</span><span class="sxs-lookup"><span data-stu-id="e3346-151">Remove a gateway</span></span>
<span data-ttu-id="e3346-152">Use o seguinte comando para remover um gateway:</span><span class="sxs-lookup"><span data-stu-id="e3346-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```