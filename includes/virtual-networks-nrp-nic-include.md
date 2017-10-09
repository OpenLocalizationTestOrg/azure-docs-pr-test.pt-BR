## <a name="nic"></a><span data-ttu-id="06f80-101">NIC</span><span class="sxs-lookup"><span data-stu-id="06f80-101">NIC</span></span>
<span data-ttu-id="06f80-102">Um recurso de placa de interface de rede fornece conectividade tooan existente sub-rede em um recurso de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="06f80-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="06f80-103">Embora você possa criar uma NIC como um objeto autônomo, você precisa tooassociate-tooanother objeto tooactually fornecer conectividade.</span><span class="sxs-lookup"><span data-stu-id="06f80-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="06f80-104">Uma NIC pode ser usado tooconnect tooa uma subrede VM, um endereço IP público ou um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="06f80-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="06f80-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="06f80-105">Property</span></span> | <span data-ttu-id="06f80-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="06f80-106">Description</span></span> | <span data-ttu-id="06f80-107">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="06f80-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06f80-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="06f80-108">**virtualMachine**</span></span> |<span data-ttu-id="06f80-109">Saudação VM NIC está associada.</span><span class="sxs-lookup"><span data-stu-id="06f80-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="06f80-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="06f80-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="06f80-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="06f80-111">**macAddress**</span></span> |<span data-ttu-id="06f80-112">Endereço MAC para Olá NIC</span><span class="sxs-lookup"><span data-stu-id="06f80-112">MAC address for hello NIC</span></span> |<span data-ttu-id="06f80-113">qualquer valor entre 4 e 30</span><span class="sxs-lookup"><span data-stu-id="06f80-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="06f80-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="06f80-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="06f80-115">NSG associado toohello NIC</span><span class="sxs-lookup"><span data-stu-id="06f80-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="06f80-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="06f80-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="06f80-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="06f80-117">**dnsSettings**</span></span> |<span data-ttu-id="06f80-118">Configurações de DNS para Olá NIC</span><span class="sxs-lookup"><span data-stu-id="06f80-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="06f80-119">veja [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="06f80-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="06f80-120">Uma placa de Interface de rede ou NIC, representa uma interface de rede que pode ser associado tooa VM (máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="06f80-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="06f80-121">Uma VM pode ter uma ou mais NICs.</span><span class="sxs-lookup"><span data-stu-id="06f80-121">A VM can have one or more NICs.</span></span>

![NICs em uma única VM](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="06f80-123">Configurações de IP</span><span class="sxs-lookup"><span data-stu-id="06f80-123">IP configurations</span></span>
<span data-ttu-id="06f80-124">NICs têm um objeto filho chamado **ipConfigurations** contendo Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="06f80-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="06f80-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="06f80-125">Property</span></span> | <span data-ttu-id="06f80-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="06f80-126">Description</span></span> | <span data-ttu-id="06f80-127">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="06f80-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06f80-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="06f80-128">**subnet**</span></span> |<span data-ttu-id="06f80-129">Olá sub-rede NIC está conectado ao.</span><span class="sxs-lookup"><span data-stu-id="06f80-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="06f80-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="06f80-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="06f80-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="06f80-131">**privateIPAddress**</span></span> |<span data-ttu-id="06f80-132">Endereço IP para Olá NIC na sub-rede Olá</span><span class="sxs-lookup"><span data-stu-id="06f80-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="06f80-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="06f80-133">10.0.0.8</span></span> |
| <span data-ttu-id="06f80-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="06f80-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="06f80-135">Método de alocação de IP</span><span class="sxs-lookup"><span data-stu-id="06f80-135">IP allocation method</span></span> |<span data-ttu-id="06f80-136">Dinâmico ou estático</span><span class="sxs-lookup"><span data-stu-id="06f80-136">Dynamic or Static</span></span> |
| <span data-ttu-id="06f80-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="06f80-137">**enableIPForwarding**</span></span> |<span data-ttu-id="06f80-138">Se Olá NIC pode ser usado para roteamento</span><span class="sxs-lookup"><span data-stu-id="06f80-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="06f80-139">true ou false</span><span class="sxs-lookup"><span data-stu-id="06f80-139">true or false</span></span> |
| <span data-ttu-id="06f80-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="06f80-140">**primary**</span></span> |<span data-ttu-id="06f80-141">Se Olá NIC é Olá NIC primário para Olá VM</span><span class="sxs-lookup"><span data-stu-id="06f80-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="06f80-142">true ou false</span><span class="sxs-lookup"><span data-stu-id="06f80-142">true or false</span></span> |
| <span data-ttu-id="06f80-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="06f80-143">**publicIPAddress**</span></span> |<span data-ttu-id="06f80-144">PIP associado Olá NIC</span><span class="sxs-lookup"><span data-stu-id="06f80-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="06f80-145">consulte [Configurações DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="06f80-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="06f80-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="06f80-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="06f80-147">Faça a saudação de pools de endereço final que NIC está associada</span><span class="sxs-lookup"><span data-stu-id="06f80-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="06f80-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="06f80-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="06f80-149">NIC está associada a saudação de regras carga balanceador NAT de entrada</span><span class="sxs-lookup"><span data-stu-id="06f80-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="06f80-150">Endereço IP de público exemplo, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="06f80-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="06f80-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="06f80-151">Additional resources</span></span>
* <span data-ttu-id="06f80-152">Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) para as NICs.</span><span class="sxs-lookup"><span data-stu-id="06f80-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

