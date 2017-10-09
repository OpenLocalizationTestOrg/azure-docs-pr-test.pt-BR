<span data-ttu-id="5796c-101">Olá perguntas Frequentes de VNet para VNet se aplica a conexões de Gateway tooVPN.</span><span class="sxs-lookup"><span data-stu-id="5796c-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="5796c-102">Se você estiver procurando o Emparelhamento de Rede Virtual, confira [Emparelhamento de Rede Virtual](../articles/virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5796c-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="5796c-103">O Azure cobra pelo tráfego entre VNets?</span><span class="sxs-lookup"><span data-stu-id="5796c-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="5796c-104">Rede virtual a rede de tráfego dentro de saudação mesmo região é gratuita para ambas as direções ao usar uma conexão de gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="5796c-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="5796c-105">Cruzada região VNet para VNet saída tráfego é cobrado com taxas de transferência Olá inter-redes de saída dados com base em regiões de origem hello.</span><span class="sxs-lookup"><span data-stu-id="5796c-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="5796c-106">Consulte toohello [página de preços de Gateway de VPN](https://azure.microsoft.com/pricing/details/vpn-gateway/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5796c-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="5796c-107">Se você estiver se conectando seus VNets usando o emparelhamento de rede virtual, em vez de Gateway de VPN, consulte Olá [página de preços de rede Virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="5796c-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="5796c-108">Tráfego de rede virtual a rede transportados por Olá Internet?</span><span class="sxs-lookup"><span data-stu-id="5796c-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="5796c-109">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-109">No.</span></span> <span data-ttu-id="5796c-110">Tráfego de rede virtual a rede percorrem Olá backbone do Microsoft Azure, Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="5796c-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="5796c-111">O tráfego de VNet para VNet é seguro?</span><span class="sxs-lookup"><span data-stu-id="5796c-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="5796c-112">Sim, ele é protegido por criptografia IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="5796c-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="5796c-113">É necessário um dispositivo VPN tooconnect VNets juntas?</span><span class="sxs-lookup"><span data-stu-id="5796c-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="5796c-114">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-114">No.</span></span> <span data-ttu-id="5796c-115">A conexão de várias redes virtuais do Azure entre si não exige um dispositivo VPN, a menos que a conectividade entre locais seja necessária.</span><span class="sxs-lookup"><span data-stu-id="5796c-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="5796c-116">Minhas VNets precisarem toobe em Olá mesma região?</span><span class="sxs-lookup"><span data-stu-id="5796c-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="5796c-117">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-117">No.</span></span> <span data-ttu-id="5796c-118">redes virtuais Olá podem estar em Olá mesmas ou em diferentes regiões do Azure (locais).</span><span class="sxs-lookup"><span data-stu-id="5796c-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="5796c-119">Se Olá VNets não está no hello mesma assinatura, assinaturas de saudação necessário toobe associado Olá AD mesmo locatário?</span><span class="sxs-lookup"><span data-stu-id="5796c-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="5796c-120">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="5796c-121">Posso usar Rede Virtual para Rede Virtual com conexões multissite?</span><span class="sxs-lookup"><span data-stu-id="5796c-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="5796c-122">Sim.</span><span class="sxs-lookup"><span data-stu-id="5796c-122">Yes.</span></span> <span data-ttu-id="5796c-123">A conectividade de rede virtual pode ser usada simultaneamente com VPNs de multissite.</span><span class="sxs-lookup"><span data-stu-id="5796c-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="5796c-124">A quantos sites locais e redes virtuais uma rede virtual pode se conectar?</span><span class="sxs-lookup"><span data-stu-id="5796c-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="5796c-125">Veja a tabela [Requisitos de gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="5796c-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="5796c-126">Pode usar VNet para VNet tooconnect VMs ou serviços fora de uma rede virtual em nuvem?</span><span class="sxs-lookup"><span data-stu-id="5796c-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="5796c-127">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-127">No.</span></span> <span data-ttu-id="5796c-128">A rede virtual com rede virtual dá suporte à conexão de redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="5796c-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="5796c-129">Ele não dá suporte à conexão de máquinas virtuais ou serviços de nuvem que não estão em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5796c-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="5796c-130">Um serviço de nuvem ou um ponto de extremidade de balanceamento de carga pode abranger redes virtuais?</span><span class="sxs-lookup"><span data-stu-id="5796c-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="5796c-131">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-131">No.</span></span> <span data-ttu-id="5796c-132">Um serviço de nuvem ou um ponto de extremidade de balanceamento de carga não pode abranger redes virtuais, mesmo que elas estejam conectadas entre si.</span><span class="sxs-lookup"><span data-stu-id="5796c-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="5796c-133">Posso usar um tipo de VPN PolicyBased para conexões de Rede Virtual para Rede Virtual ou Multissite?</span><span class="sxs-lookup"><span data-stu-id="5796c-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="5796c-134">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-134">No.</span></span> <span data-ttu-id="5796c-135">As conexões de rede virtual para rede virtual e de vários sites exigem gateways de VPN com tipos de VPN RouteBased (anteriormente chamado de Roteamento Dinâmico).</span><span class="sxs-lookup"><span data-stu-id="5796c-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="5796c-136">Posso conectar uma rede virtual com um tipo de VPN RouteBased de tooanother VNet com um tipo PolicyBased VPN?</span><span class="sxs-lookup"><span data-stu-id="5796c-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="5796c-137">Não, ambas as redes virtuais DEVEM estar usando VPNs baseadas em rota (anteriormente chamado de Roteamento Dinâmico).</span><span class="sxs-lookup"><span data-stu-id="5796c-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="5796c-138">Os túneis de VPN compartilham largura de banda?</span><span class="sxs-lookup"><span data-stu-id="5796c-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="5796c-139">Sim.</span><span class="sxs-lookup"><span data-stu-id="5796c-139">Yes.</span></span> <span data-ttu-id="5796c-140">Todos os túneis VPN da rede virtual Olá compartilham largura de banda disponível no gateway de VPN do Azure Olá Olá e Olá mesmo SLA de tempo de atividade de gateway VPN no Azure.</span><span class="sxs-lookup"><span data-stu-id="5796c-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="5796c-141">Há suporte para túneis redundantes?</span><span class="sxs-lookup"><span data-stu-id="5796c-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="5796c-142">Os túneis redundantes entre um par de redes virtuais terão suporte quando um gateway de rede virtual estiver configurado como ativo.</span><span class="sxs-lookup"><span data-stu-id="5796c-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="5796c-143">Posso ter espaços de endereço sobrepostos para configurações de Rede Virtual para Rede Virtual?</span><span class="sxs-lookup"><span data-stu-id="5796c-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="5796c-144">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-144">No.</span></span> <span data-ttu-id="5796c-145">Você não pode ter intervalos de endereços IP sobrepostos.</span><span class="sxs-lookup"><span data-stu-id="5796c-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="5796c-146">Pode haver sobreposição de espaços de endereço entre as redes virtuais conectadas e sites local locais?</span><span class="sxs-lookup"><span data-stu-id="5796c-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="5796c-147">Não.</span><span class="sxs-lookup"><span data-stu-id="5796c-147">No.</span></span> <span data-ttu-id="5796c-148">Você não pode ter intervalos de endereços IP sobrepostos.</span><span class="sxs-lookup"><span data-stu-id="5796c-148">You can't have overlapping IP address ranges.</span></span>



