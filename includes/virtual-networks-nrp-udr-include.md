## <a name="route-tables"></a><span data-ttu-id="533b9-101">Tabelas de rotas</span><span class="sxs-lookup"><span data-stu-id="533b9-101">Route tables</span></span>
<span data-ttu-id="533b9-102">Os recursos de tabela de rotas contêm as rotas usadas para definir o fluxo de tráfego em sua infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="533b9-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="533b9-103">Você pode usar UDRs (rotas definidas pelo usuário) para enviar todo o tráfego de uma determinada sub-rede para um dispositivo virtual, como um firewall ou IDS (sistema de detecção de intrusões).</span><span class="sxs-lookup"><span data-stu-id="533b9-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="533b9-104">É possível associar uma tabela de rotas a sub-redes.</span><span class="sxs-lookup"><span data-stu-id="533b9-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="533b9-105">As tabelas de rotas contêm as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="533b9-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="533b9-106">Propriedade</span><span class="sxs-lookup"><span data-stu-id="533b9-106">Property</span></span> | <span data-ttu-id="533b9-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="533b9-107">Description</span></span> | <span data-ttu-id="533b9-108">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="533b9-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="533b9-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="533b9-109">**routes**</span></span> |<span data-ttu-id="533b9-110">Coleção de rotas definidas pelo usuário na tabela de rotas</span><span class="sxs-lookup"><span data-stu-id="533b9-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="533b9-111">veja [rotas definidas pelo usuário](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="533b9-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="533b9-112">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="533b9-112">**subnets**</span></span> |<span data-ttu-id="533b9-113">Coleção de sub-redes às quais a tabela de rotas é aplicada</span><span class="sxs-lookup"><span data-stu-id="533b9-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="533b9-114">veja [sub-redes](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="533b9-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="533b9-115">rotas definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="533b9-115">User defined routes</span></span>
<span data-ttu-id="533b9-116">Você pode criar UDRs para especificar para onde o tráfego deve ser enviado, com base em seu endereço de destino.</span><span class="sxs-lookup"><span data-stu-id="533b9-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="533b9-117">Pense em uma rota como a definição de gateway padrão baseado no endereço de destino de um pacote de rede.</span><span class="sxs-lookup"><span data-stu-id="533b9-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="533b9-118">As UDRs contêm as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="533b9-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="533b9-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="533b9-119">Property</span></span> | <span data-ttu-id="533b9-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="533b9-120">Description</span></span> | <span data-ttu-id="533b9-121">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="533b9-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="533b9-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="533b9-122">**addressPrefix**</span></span> |<span data-ttu-id="533b9-123">Prefixo de endereço ou endereço IP completo para o destino</span><span class="sxs-lookup"><span data-stu-id="533b9-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="533b9-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="533b9-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="533b9-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="533b9-125">**nextHopType**</span></span> |<span data-ttu-id="533b9-126">Tipo de dispositivo para o qual o tráfego será enviado</span><span class="sxs-lookup"><span data-stu-id="533b9-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="533b9-127">Dispositivo Virtual, Gateway de VPN, Internet</span><span class="sxs-lookup"><span data-stu-id="533b9-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="533b9-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="533b9-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="533b9-129">Endereço IP do próximo salto</span><span class="sxs-lookup"><span data-stu-id="533b9-129">IP address for the next hop</span></span> |<span data-ttu-id="533b9-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="533b9-130">192.168.1.4</span></span> |

<span data-ttu-id="533b9-131">Exemplo de tabela de rotas no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="533b9-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="533b9-132">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="533b9-132">Additional resources</span></span>
* <span data-ttu-id="533b9-133">Obtenha mais informações sobre [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="533b9-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="533b9-134">Leia a [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) para obter tabelas de rotas.</span><span class="sxs-lookup"><span data-stu-id="533b9-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="533b9-135">Leitura de [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) para obter UDRs (rotas definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="533b9-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

