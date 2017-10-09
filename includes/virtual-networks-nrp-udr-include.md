## <a name="route-tables"></a><span data-ttu-id="3e76f-101">Tabelas de rotas</span><span class="sxs-lookup"><span data-stu-id="3e76f-101">Route tables</span></span>
<span data-ttu-id="3e76f-102">Recursos de tabela de rota contém rotas usadas toodefine como fluxos de tráfego dentro de sua infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e76f-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="3e76f-103">Você pode usar toosend de rotas (UDR) definidos pelo usuário em todo o tráfego de um determinada sub-rede tooa dispositivo virtual, como um sistema de detecção firewall ou invasão (IDS).</span><span class="sxs-lookup"><span data-stu-id="3e76f-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="3e76f-104">Você pode associar um toosubnets da tabela de rota.</span><span class="sxs-lookup"><span data-stu-id="3e76f-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="3e76f-105">Tabelas de rotas contêm Olá propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="3e76f-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="3e76f-106">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3e76f-106">Property</span></span> | <span data-ttu-id="3e76f-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="3e76f-107">Description</span></span> | <span data-ttu-id="3e76f-108">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3e76f-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e76f-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="3e76f-109">**routes**</span></span> |<span data-ttu-id="3e76f-110">Coleção de usuário definida rotas na tabela de rotas Olá</span><span class="sxs-lookup"><span data-stu-id="3e76f-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="3e76f-111">veja [rotas definidas pelo usuário](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="3e76f-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="3e76f-112">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="3e76f-112">**subnets**</span></span> |<span data-ttu-id="3e76f-113">Coleção de tabela de rotas Olá sub-redes é aplicada muito</span><span class="sxs-lookup"><span data-stu-id="3e76f-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="3e76f-114">veja [sub-redes](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="3e76f-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="3e76f-115">rotas definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="3e76f-115">User defined routes</span></span>
<span data-ttu-id="3e76f-116">Você pode criar toospecify UDRs onde o tráfego deve ser enviado, com base em seu endereço de destino.</span><span class="sxs-lookup"><span data-stu-id="3e76f-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="3e76f-117">Você pode pensar em uma rota como definição de gateway padrão de saudação com base no endereço de destino de saudação de um pacote de rede.</span><span class="sxs-lookup"><span data-stu-id="3e76f-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="3e76f-118">UDRs contêm Olá propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="3e76f-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="3e76f-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3e76f-119">Property</span></span> | <span data-ttu-id="3e76f-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="3e76f-120">Description</span></span> | <span data-ttu-id="3e76f-121">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3e76f-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e76f-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="3e76f-122">**addressPrefix**</span></span> |<span data-ttu-id="3e76f-123">Prefixo de endereço ou endereço IP completo para o destino de saudação</span><span class="sxs-lookup"><span data-stu-id="3e76f-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="3e76f-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="3e76f-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="3e76f-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="3e76f-125">**nextHopType**</span></span> |<span data-ttu-id="3e76f-126">Tipo de dispositivo Olá tráfego será enviado muito</span><span class="sxs-lookup"><span data-stu-id="3e76f-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="3e76f-127">Dispositivo Virtual, Gateway de VPN, Internet</span><span class="sxs-lookup"><span data-stu-id="3e76f-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="3e76f-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="3e76f-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="3e76f-129">Endereço IP do próximo salto de saudação</span><span class="sxs-lookup"><span data-stu-id="3e76f-129">IP address for hello next hop</span></span> |<span data-ttu-id="3e76f-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="3e76f-130">192.168.1.4</span></span> |

<span data-ttu-id="3e76f-131">Exemplo de tabela de rotas no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="3e76f-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="3e76f-132">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3e76f-132">Additional resources</span></span>
* <span data-ttu-id="3e76f-133">Obtenha mais informações sobre [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e76f-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="3e76f-134">Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) para tabelas de rotas.</span><span class="sxs-lookup"><span data-stu-id="3e76f-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="3e76f-135">Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) para o usuário definido rotas (UDRs).</span><span class="sxs-lookup"><span data-stu-id="3e76f-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

