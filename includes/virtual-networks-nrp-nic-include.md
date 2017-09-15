## <a name="nic"></a><span data-ttu-id="21a0c-101">NIC</span><span class="sxs-lookup"><span data-stu-id="21a0c-101">NIC</span></span>
<span data-ttu-id="21a0c-102">Um recurso de placa de interface de rede (NIC) fornece conectividade de rede com uma sub-rede existente em um recurso de VNet.</span><span class="sxs-lookup"><span data-stu-id="21a0c-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="21a0c-103">Embora você possa criar uma NIC como um objeto autônomo, você precisa associá-la a outro objeto para fornecer a conectividade.</span><span class="sxs-lookup"><span data-stu-id="21a0c-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="21a0c-104">Uma NIC pode ser usada para conectar uma VM a uma sub-rede, um endereço IP público ou um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="21a0c-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="21a0c-105">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21a0c-105">Property</span></span> | <span data-ttu-id="21a0c-106">Descrição</span><span class="sxs-lookup"><span data-stu-id="21a0c-106">Description</span></span> | <span data-ttu-id="21a0c-107">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="21a0c-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21a0c-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="21a0c-108">**virtualMachine**</span></span> |<span data-ttu-id="21a0c-109">A VM à qual a NIC está associada.</span><span class="sxs-lookup"><span data-stu-id="21a0c-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="21a0c-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="21a0c-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="21a0c-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="21a0c-111">**macAddress**</span></span> |<span data-ttu-id="21a0c-112">Endereço MAC da NIC</span><span class="sxs-lookup"><span data-stu-id="21a0c-112">MAC address for the NIC</span></span> |<span data-ttu-id="21a0c-113">qualquer valor entre 4 e 30</span><span class="sxs-lookup"><span data-stu-id="21a0c-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="21a0c-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="21a0c-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="21a0c-115">NSG associado à NIC</span><span class="sxs-lookup"><span data-stu-id="21a0c-115">NSG associated to the NIC</span></span> |<span data-ttu-id="21a0c-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="21a0c-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="21a0c-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="21a0c-117">**dnsSettings**</span></span> |<span data-ttu-id="21a0c-118">Configurações de DNS para a NIC</span><span class="sxs-lookup"><span data-stu-id="21a0c-118">DNS settings for the NIC</span></span> |<span data-ttu-id="21a0c-119">veja [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="21a0c-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="21a0c-120">Uma Placa de Interface de rede ou NIC representa uma interface de rede que pode ser associada a uma VM (máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="21a0c-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="21a0c-121">Uma VM pode ter uma ou mais NICs.</span><span class="sxs-lookup"><span data-stu-id="21a0c-121">A VM can have one or more NICs.</span></span>

![NICs em uma única VM](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="21a0c-123">Configurações de IP</span><span class="sxs-lookup"><span data-stu-id="21a0c-123">IP configurations</span></span>
<span data-ttu-id="21a0c-124">NICs têm um objeto filho chamado **ipConfigurations** que contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="21a0c-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="21a0c-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21a0c-125">Property</span></span> | <span data-ttu-id="21a0c-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="21a0c-126">Description</span></span> | <span data-ttu-id="21a0c-127">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="21a0c-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21a0c-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="21a0c-128">**subnet**</span></span> |<span data-ttu-id="21a0c-129">A sub-rede à qual a NIC está conectada.</span><span class="sxs-lookup"><span data-stu-id="21a0c-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="21a0c-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="21a0c-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="21a0c-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="21a0c-131">**privateIPAddress**</span></span> |<span data-ttu-id="21a0c-132">Endereço IP da NIC na sub-rede</span><span class="sxs-lookup"><span data-stu-id="21a0c-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="21a0c-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="21a0c-133">10.0.0.8</span></span> |
| <span data-ttu-id="21a0c-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="21a0c-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="21a0c-135">Método de alocação de IP</span><span class="sxs-lookup"><span data-stu-id="21a0c-135">IP allocation method</span></span> |<span data-ttu-id="21a0c-136">Dinâmico ou estático</span><span class="sxs-lookup"><span data-stu-id="21a0c-136">Dynamic or Static</span></span> |
| <span data-ttu-id="21a0c-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="21a0c-137">**enableIPForwarding**</span></span> |<span data-ttu-id="21a0c-138">Se a NIC pode ser usada para roteamento</span><span class="sxs-lookup"><span data-stu-id="21a0c-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="21a0c-139">true ou false</span><span class="sxs-lookup"><span data-stu-id="21a0c-139">true or false</span></span> |
| <span data-ttu-id="21a0c-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="21a0c-140">**primary**</span></span> |<span data-ttu-id="21a0c-141">Se a NIC é a NIC primária para a VM</span><span class="sxs-lookup"><span data-stu-id="21a0c-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="21a0c-142">true ou false</span><span class="sxs-lookup"><span data-stu-id="21a0c-142">true or false</span></span> |
| <span data-ttu-id="21a0c-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="21a0c-143">**publicIPAddress**</span></span> |<span data-ttu-id="21a0c-144">PIP associado à NIC</span><span class="sxs-lookup"><span data-stu-id="21a0c-144">PIP associated with the NIC</span></span> |<span data-ttu-id="21a0c-145">consulte [Configurações DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="21a0c-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="21a0c-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="21a0c-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="21a0c-147">Pools de endereços de back-end aos quais a NIC está associada</span><span class="sxs-lookup"><span data-stu-id="21a0c-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="21a0c-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="21a0c-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="21a0c-149">Regras de NAT do balanceador de carga às quais a NIC está associada</span><span class="sxs-lookup"><span data-stu-id="21a0c-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="21a0c-150">Endereço IP de público exemplo, no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="21a0c-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="21a0c-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="21a0c-151">Additional resources</span></span>
* <span data-ttu-id="21a0c-152">Leia a [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) para obter NICs.</span><span class="sxs-lookup"><span data-stu-id="21a0c-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

