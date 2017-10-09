<span data-ttu-id="14cc1-101">etapas de saudação para usar essa tarefa uma rede virtual com base nos valores Olá Olá lista de referências de configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="14cc1-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="14cc1-102">Nomes e configurações adicionais também são descritos nesta lista.</span><span class="sxs-lookup"><span data-stu-id="14cc1-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="14cc1-103">Não usamos essa lista diretamente em qualquer uma das etapas hello, embora adicionamos variáveis com base nos valores hello nesta lista.</span><span class="sxs-lookup"><span data-stu-id="14cc1-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="14cc1-104">Você pode copiar Olá toouse de lista como referência, substituindo valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="14cc1-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="14cc1-105">**Lista de referência de configuração**</span><span class="sxs-lookup"><span data-stu-id="14cc1-105">**Configuration reference list**</span></span>

* <span data-ttu-id="14cc1-106">Nome da Rede Virtual = “TestVNet”</span><span class="sxs-lookup"><span data-stu-id="14cc1-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="14cc1-107">Espaço de endereço da Rede Virtual = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="14cc1-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="14cc1-108">Grupo de recursos = “TestRG”</span><span class="sxs-lookup"><span data-stu-id="14cc1-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="14cc1-109">Nome de Subnet1 = “FrontEnd”</span><span class="sxs-lookup"><span data-stu-id="14cc1-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="14cc1-110">Espaço de endereço de sub-rede1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="14cc1-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="14cc1-111">Nome da Sub-rede do Gateway: “GatewaySubnet” Deve-se sempre nomear uma sub-rede do gateway como *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="14cc1-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="14cc1-112">Espaço de endereço da Sub-Rede do Gateway = “192.168.200.0/26”</span><span class="sxs-lookup"><span data-stu-id="14cc1-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="14cc1-113">Região = “Leste dos EUA”</span><span class="sxs-lookup"><span data-stu-id="14cc1-113">Region = "East US"</span></span>
* <span data-ttu-id="14cc1-114">Nome do Gateway = “GW”</span><span class="sxs-lookup"><span data-stu-id="14cc1-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="14cc1-115">Nome do IP do Gateway = “GWIP”</span><span class="sxs-lookup"><span data-stu-id="14cc1-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="14cc1-116">Nome da configuração de IP do Gateway = “gwipconf”</span><span class="sxs-lookup"><span data-stu-id="14cc1-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="14cc1-117">Tipo = “ExpressRoute” Este tipo é necessário para uma configuração de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="14cc1-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="14cc1-118">Nome do IP público do Gateway = “gwpip”</span><span class="sxs-lookup"><span data-stu-id="14cc1-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="14cc1-119">Adicionar um gateway</span><span class="sxs-lookup"><span data-stu-id="14cc1-119">Add a gateway</span></span>
1. <span data-ttu-id="14cc1-120">Conecte-se tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="14cc1-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="14cc1-121">Declare as variáveis para este exercício.</span><span class="sxs-lookup"><span data-stu-id="14cc1-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="14cc1-122">Ser tooedit-se de que as configurações de saudação tooreflect exemplo hello que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="14cc1-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="14cc1-123">Armazenar o objeto de rede virtual hello como uma variável.</span><span class="sxs-lookup"><span data-stu-id="14cc1-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="14cc1-124">Adicione uma sub-rede de gateway tooyour rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="14cc1-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="14cc1-125">subrede Olá gateway deve ser nomeado "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="14cc1-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="14cc1-126">Você deve criar uma sub-rede de gateway que seja /27 ou maior (/26, /25 etc.).</span><span class="sxs-lookup"><span data-stu-id="14cc1-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="14cc1-127">Definir a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="14cc1-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="14cc1-128">Armazenar a sub-rede de gateway hello como uma variável.</span><span class="sxs-lookup"><span data-stu-id="14cc1-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="14cc1-129">Solicite um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="14cc1-129">Request a public IP address.</span></span> <span data-ttu-id="14cc1-130">o endereço IP Hello é solicitado antes de criar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="14cc1-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="14cc1-131">Não é possível especificar o endereço IP de saudação que você deseja toouse; ela é alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="14cc1-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="14cc1-132">Você usará esse endereço IP na próxima seção de configuração hello.</span><span class="sxs-lookup"><span data-stu-id="14cc1-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="14cc1-133">Olá AllocationMethod deve ser dinâmico.</span><span class="sxs-lookup"><span data-stu-id="14cc1-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="14cc1-134">Crie a configuração de saudação do seu gateway.</span><span class="sxs-lookup"><span data-stu-id="14cc1-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="14cc1-135">configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello.</span><span class="sxs-lookup"><span data-stu-id="14cc1-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="14cc1-136">Nesta etapa, você está especificando configuração Olá que será usada quando você criar hello gateway.</span><span class="sxs-lookup"><span data-stu-id="14cc1-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="14cc1-137">Essa etapa não cria realmente objeto de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="14cc1-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="14cc1-138">Use o exemplo hello abaixo toocreate sua configuração de gateway.</span><span class="sxs-lookup"><span data-stu-id="14cc1-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="14cc1-139">Crie gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="14cc1-139">Create hello gateway.</span></span> <span data-ttu-id="14cc1-140">Nesta etapa, Olá **- GatewayType** é especialmente importante.</span><span class="sxs-lookup"><span data-stu-id="14cc1-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="14cc1-141">Você deve usar o valor de saudação **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="14cc1-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="14cc1-142">Depois de executar esses cmdlets, gateway Olá pode levar até 45 minutos ou mais toocreate.</span><span class="sxs-lookup"><span data-stu-id="14cc1-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="14cc1-143">Verifique se o gateway de saudação foi criado</span><span class="sxs-lookup"><span data-stu-id="14cc1-143">Verify hello gateway was created</span></span>
<span data-ttu-id="14cc1-144">Use Olá tooverify que Olá gateway foi criado de comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="14cc1-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="14cc1-145">Redimensionar um gateway</span><span class="sxs-lookup"><span data-stu-id="14cc1-145">Resize a gateway</span></span>
<span data-ttu-id="14cc1-146">Há uma série de [SKUs de Gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="14cc1-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="14cc1-147">Você pode usar Olá Olá do comando toochange SKU de Gateway a seguir a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="14cc1-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14cc1-148">Esse comando não funciona para o gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="14cc1-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="14cc1-149">toochange gateway gateway tooan UltraPerformance, primeiro remova Olá existente do gateway de rota expressa e, em seguida, criar um novo gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="14cc1-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="14cc1-150">toodowngrade seu gateway de um gateway UltraPerformance, primeiro remova Olá UltraPerformance gateway e, em seguida, criar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="14cc1-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="14cc1-151">Remover um gateway</span><span class="sxs-lookup"><span data-stu-id="14cc1-151">Remove a gateway</span></span>
<span data-ttu-id="14cc1-152">Use Olá comando tooremove um gateway a seguir:</span><span class="sxs-lookup"><span data-stu-id="14cc1-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```