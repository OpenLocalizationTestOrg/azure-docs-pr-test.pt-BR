## <a name="virtual-network"></a><span data-ttu-id="ad84f-101">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="ad84f-101">Virtual Network</span></span>
<span data-ttu-id="ad84f-102">Os recursos de VNETs (Redes Virtuais) e de sub-redes ajudam a definir um limite de segurança para cargas de trabalho em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ad84f-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="ad84f-103">Uma VNet é caracterizada por uma coleção de espaços de endereços, definidos como blocos CIDR.</span><span class="sxs-lookup"><span data-stu-id="ad84f-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad84f-104">Os administradores de rede estão familiarizados com a notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="ad84f-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="ad84f-105">Se não estiver familiarizado com o CIDR, [saiba mais sobre ele](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="ad84f-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![VNet com várias sub-redes](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="ad84f-107">As VNets contêm as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="ad84f-107">VNets contain the following properties.</span></span>

| <span data-ttu-id="ad84f-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ad84f-108">Property</span></span> | <span data-ttu-id="ad84f-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="ad84f-109">Description</span></span> | <span data-ttu-id="ad84f-110">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="ad84f-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad84f-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="ad84f-111">**addressSpace**</span></span> |<span data-ttu-id="ad84f-112">Coleção de prefixos de endereços que compõem a notação CIDR da VNet</span><span class="sxs-lookup"><span data-stu-id="ad84f-112">Collection of address prefixes that make up the VNet in CIDR notation</span></span> |<span data-ttu-id="ad84f-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ad84f-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="ad84f-114">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="ad84f-114">**subnets**</span></span> |<span data-ttu-id="ad84f-115">Coleção de sub-redes que compõem a VNet</span><span class="sxs-lookup"><span data-stu-id="ad84f-115">Collection of subnets that make up the VNet</span></span> |<span data-ttu-id="ad84f-116">veja [sub-redes](#Subnets) abaixo.</span><span class="sxs-lookup"><span data-stu-id="ad84f-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="ad84f-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="ad84f-117">**ipAddress**</span></span> |<span data-ttu-id="ad84f-118">Endereço IP atribuído a um objeto.</span><span class="sxs-lookup"><span data-stu-id="ad84f-118">IP address assigned to object.</span></span> <span data-ttu-id="ad84f-119">Essa é uma propriedade somente leitura.</span><span class="sxs-lookup"><span data-stu-id="ad84f-119">This is a read-only property.</span></span> |<span data-ttu-id="ad84f-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="ad84f-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="ad84f-121">Sub-redes</span><span class="sxs-lookup"><span data-stu-id="ad84f-121">Subnets</span></span>
<span data-ttu-id="ad84f-122">Uma sub-rede é um recurso filho de uma VNet e ajuda a definir segmentos de espaços de endereços em um bloco CIDR, usando prefixos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="ad84f-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="ad84f-123">As NICs podem ser adicionadas a sub-redes e conectadas a VMs, fornecendo conectividade para diversas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ad84f-123">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="ad84f-124">As sub-redes contêm as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="ad84f-124">Subnets contain the following properties.</span></span> 

| <span data-ttu-id="ad84f-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ad84f-125">Property</span></span> | <span data-ttu-id="ad84f-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="ad84f-126">Description</span></span> | <span data-ttu-id="ad84f-127">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="ad84f-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad84f-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="ad84f-128">**addressPrefix**</span></span> |<span data-ttu-id="ad84f-129">Prefixo de endereço único que compõe a sub-rede na notação CIDR</span><span class="sxs-lookup"><span data-stu-id="ad84f-129">Single address prefix that make up the subnet in CIDR notation</span></span> |<span data-ttu-id="ad84f-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="ad84f-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="ad84f-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="ad84f-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="ad84f-132">NSG aplicado à sub-rede</span><span class="sxs-lookup"><span data-stu-id="ad84f-132">NSG applied to the subnet</span></span> |<span data-ttu-id="ad84f-133">veja [NSGs](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="ad84f-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="ad84f-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="ad84f-134">**routeTable**</span></span> |<span data-ttu-id="ad84f-135">Tabela de rotas aplicada à sub-rede</span><span class="sxs-lookup"><span data-stu-id="ad84f-135">Route table applied to the subnet</span></span> |<span data-ttu-id="ad84f-136">veja [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="ad84f-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="ad84f-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="ad84f-137">**ipConfigurations**</span></span> |<span data-ttu-id="ad84f-138">Coleção de objetos de configuração IP usada pelas NICs conectadas à sub-rede</span><span class="sxs-lookup"><span data-stu-id="ad84f-138">Collection of IP configruation objects used by NICs connected to the subnet</span></span> |<span data-ttu-id="ad84f-139">veja [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="ad84f-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="ad84f-140">Exemplo de VNet no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="ad84f-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="ad84f-141">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ad84f-141">Additional resources</span></span>
* <span data-ttu-id="ad84f-142">Obtenha mais informações sobre a [VNet](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad84f-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="ad84f-143">Leia a [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) para obter VNets.</span><span class="sxs-lookup"><span data-stu-id="ad84f-143">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="ad84f-144">Leia a [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) para obter Sub-redes.</span><span class="sxs-lookup"><span data-stu-id="ad84f-144">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

