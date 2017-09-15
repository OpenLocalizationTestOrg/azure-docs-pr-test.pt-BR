<span data-ttu-id="e3afd-101">Ao criar um gateway de rede virtual, você precisa especificar o SKU do gateway que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e3afd-101">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="e3afd-102">Selecione as SKUs que atendem às suas necessidades com base nos tipos de SLAs, taxas de transferência, recursos e cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3afd-102">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="e3afd-103"><a name="workloads"></a>Produção *versus* Cargas de Trabalho de Desenvolvimento e Teste</span><span class="sxs-lookup"><span data-stu-id="e3afd-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="e3afd-104">Devido a diferenças nos SLAs e conjuntos de recursos, é recomendável usar as SKUs a seguir para produção *versus* desenvolvimento e teste:</span><span class="sxs-lookup"><span data-stu-id="e3afd-104">Due to the differences in SLAs and feature sets, we recommend the following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="e3afd-105">**Carga de trabalho**</span><span class="sxs-lookup"><span data-stu-id="e3afd-105">**Workload**</span></span>                       | <span data-ttu-id="e3afd-106">**SKUs**</span><span class="sxs-lookup"><span data-stu-id="e3afd-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="e3afd-107">**Produção, cargas de trabalho críticas**</span><span class="sxs-lookup"><span data-stu-id="e3afd-107">**Production, critical workloads**</span></span> | <span data-ttu-id="e3afd-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="e3afd-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="e3afd-109">**Teste de desenvolvimento ou prova de conceito**</span><span class="sxs-lookup"><span data-stu-id="e3afd-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="e3afd-110">Basic</span><span class="sxs-lookup"><span data-stu-id="e3afd-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="e3afd-111">Se você estiver usando as SKUs antigas, as recomendações de SKU de produção serão Standard e Alto Desempenho.</span><span class="sxs-lookup"><span data-stu-id="e3afd-111">If you are using the old SKUs, the production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="e3afd-112">Para saber mais sobre os SKUs antigos, confira [SKUs de Gateway (SKUs herdados)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="e3afd-112">For information on the old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="e3afd-113"><a name="feature"></a>Conjuntos de recursos do SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="e3afd-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="e3afd-114">As novas SKUs do gateway simplificam os conjuntos de recursos oferecidos nos gateways:</span><span class="sxs-lookup"><span data-stu-id="e3afd-114">The new gateway SKUs streamline the feature sets offered on the gateways:</span></span>

| <span data-ttu-id="e3afd-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="e3afd-115">**SKU**</span></span>| <span data-ttu-id="e3afd-116">**Recursos**</span><span class="sxs-lookup"><span data-stu-id="e3afd-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="e3afd-117">**Básico**</span><span class="sxs-lookup"><span data-stu-id="e3afd-117">**Basic**</span></span>   | <span data-ttu-id="e3afd-118">**VPN baseada em rota**: 10 túneis com P2S</span><span class="sxs-lookup"><span data-stu-id="e3afd-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="e3afd-119">**VPN baseada em políticas:** (IKEv1): 1 túnel; sem P2S</span><span class="sxs-lookup"><span data-stu-id="e3afd-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="e3afd-120">**VpnGw1, VpnGw2 e VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="e3afd-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="e3afd-121">**VPN baseada em rota**: até 30 túneis (*), P2S, BGP, ativo-ativo, política IPsec/IKE personalizada, coexistência ExpressRoute/VPN</span><span class="sxs-lookup"><span data-stu-id="e3afd-121">**Route-based VPN**: up to 30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="e3afd-122">(*) Você pode configurar "PolicyBasedTrafficSelectors" para se conectar a um gateway de VPN baseado em rota (VpnGw1, VpnGw2, VpnGw3) para vários dispositivos de firewall baseados em políticas.</span><span class="sxs-lookup"><span data-stu-id="e3afd-122">(*) You can configure "PolicyBasedTrafficSelectors" to connect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) to multiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="e3afd-123">Confira [Conectar gateways de VPN a vários dispositivos VPN baseados em políticas usando o PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e3afd-123">Refer to [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="e3afd-124"><a name="resize"></a>Redimensionamento de SKUs de gateway</span><span class="sxs-lookup"><span data-stu-id="e3afd-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="e3afd-125">Você pode redimensionar entre as SKUs VpnGw1, VpnGw2 e VpnGw3.</span><span class="sxs-lookup"><span data-stu-id="e3afd-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="e3afd-126">Ao trabalhar com SKUs antigas, você ainda pode redimensionar entre SKUs Básicas, Standard e de Alto Desempenho.</span><span class="sxs-lookup"><span data-stu-id="e3afd-126">When working with the old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="e3afd-127">Você **não pode** redimensionar as SKUs Basic/Standard/Alto Desempenho para as novas SKUs VpnGw1/VpnGw2/VpnGw3.</span><span class="sxs-lookup"><span data-stu-id="e3afd-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs to the new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="e3afd-128">Em vez disso, você deve [migrar](#migrate) para as novas SKUs.</span><span class="sxs-lookup"><span data-stu-id="e3afd-128">You must, instead, [migrate](#migrate) to the new SKUs.</span></span>

###  <span data-ttu-id="e3afd-129"><a name="migrate"></a>Migrando de SKUs antigas para novas SKUs</span><span class="sxs-lookup"><span data-stu-id="e3afd-129"><a name="migrate"></a>Migrating from old SKUs to the new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
