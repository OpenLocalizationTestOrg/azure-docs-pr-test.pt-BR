## <a name="network-security-group"></a><span data-ttu-id="57e58-101">Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="57e58-101">Network Security Group</span></span>
<span data-ttu-id="57e58-102">Um recurso NSG habilita a criação de limite de segurança para cargas de trabalho, por meio de regras de permissão e recusa.</span><span class="sxs-lookup"><span data-stu-id="57e58-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="57e58-103">Essas regras podem ser aplicadas a uma VM, NIC ou sub-rede.</span><span class="sxs-lookup"><span data-stu-id="57e58-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="57e58-104">Propriedade</span><span class="sxs-lookup"><span data-stu-id="57e58-104">Property</span></span> | <span data-ttu-id="57e58-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="57e58-105">Description</span></span> | <span data-ttu-id="57e58-106">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="57e58-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57e58-107">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="57e58-107">**subnets**</span></span> |<span data-ttu-id="57e58-108">Lista de IDS de sub-rede às quais o NSG é aplicado.</span><span class="sxs-lookup"><span data-stu-id="57e58-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="57e58-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="57e58-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="57e58-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="57e58-110">**securityRules**</span></span> |<span data-ttu-id="57e58-111">Lista de regras de segurança que compõem o NSG</span><span class="sxs-lookup"><span data-stu-id="57e58-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="57e58-112">Veja [Regra de segurança](#Security-rule) abaixo</span><span class="sxs-lookup"><span data-stu-id="57e58-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="57e58-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="57e58-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="57e58-114">Lista de regras de segurança padrão presentes em cada NSG</span><span class="sxs-lookup"><span data-stu-id="57e58-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="57e58-115">Veja [Regras de segurança padrão](#Default-security-rules) abaixo</span><span class="sxs-lookup"><span data-stu-id="57e58-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="57e58-116">**Regra de segurança** - um NSG um pode ter várias regras de segurança definidas.</span><span class="sxs-lookup"><span data-stu-id="57e58-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="57e58-117">Cada regra pode permitir ou negar diferentes tipos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="57e58-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="57e58-118">Regra de segurança</span><span class="sxs-lookup"><span data-stu-id="57e58-118">Security rule</span></span>
<span data-ttu-id="57e58-119">Uma regra de segurança é um recurso filho de um NSG que contém as propriedades abaixo.</span><span class="sxs-lookup"><span data-stu-id="57e58-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="57e58-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="57e58-120">Property</span></span> | <span data-ttu-id="57e58-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="57e58-121">Description</span></span> | <span data-ttu-id="57e58-122">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="57e58-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57e58-123">**description**</span><span class="sxs-lookup"><span data-stu-id="57e58-123">**description**</span></span> |<span data-ttu-id="57e58-124">Descrição da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-124">Description for the rule</span></span> |<span data-ttu-id="57e58-125">Permitir tráfego de entrada para todas as VMs na sub-rede X</span><span class="sxs-lookup"><span data-stu-id="57e58-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="57e58-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="57e58-126">**protocol**</span></span> |<span data-ttu-id="57e58-127">Protocolo para fazer a correspondência da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-127">Protocol to match for the rule</span></span> |<span data-ttu-id="57e58-128">TCP, UDP ou *</span><span class="sxs-lookup"><span data-stu-id="57e58-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="57e58-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="57e58-129">**sourcePortRange**</span></span> |<span data-ttu-id="57e58-130">Intervalo de portas de origem para fazer a correspondência da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-130">Source port range to match for the rule</span></span> |<span data-ttu-id="57e58-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="57e58-131">80, 100-200, *</span></span> |
| <span data-ttu-id="57e58-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="57e58-132">**destinationPortRange**</span></span> |<span data-ttu-id="57e58-133">Intervalo de portas de destino para fazer a correspondência da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="57e58-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="57e58-134">80, 100-200, *</span></span> |
| <span data-ttu-id="57e58-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="57e58-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="57e58-136">Prefixo de endereço de origem para fazer a correspondência da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="57e58-137">10.10.10.1, 10.10.10.0/24, Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="57e58-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="57e58-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="57e58-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="57e58-139">Prefixo de endereço de destino para fazer a correspondência da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="57e58-140">10.10.10.1, 10.10.10.0/24, Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="57e58-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="57e58-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="57e58-141">**direction**</span></span> |<span data-ttu-id="57e58-142">Direção do tráfego para fazer a correspondência da regra</span><span class="sxs-lookup"><span data-stu-id="57e58-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="57e58-143">entrada ou saída</span><span class="sxs-lookup"><span data-stu-id="57e58-143">inbound or outbound</span></span> |
| <span data-ttu-id="57e58-144">**prioridade**</span><span class="sxs-lookup"><span data-stu-id="57e58-144">**priority**</span></span> |<span data-ttu-id="57e58-145">Prioridade da regra.</span><span class="sxs-lookup"><span data-stu-id="57e58-145">Priority for the rule.</span></span> <span data-ttu-id="57e58-146">As regras são verificadas em ordem de prioridade, e depois que uma regra é aplicada, nenhuma outra regra é testada quanto à correspondência.</span><span class="sxs-lookup"><span data-stu-id="57e58-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="57e58-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="57e58-147">10, 100, 65000</span></span> |
| <span data-ttu-id="57e58-148">**access**</span><span class="sxs-lookup"><span data-stu-id="57e58-148">**access**</span></span> |<span data-ttu-id="57e58-149">Tipo de acesso a ser aplicado se a regra for correspondente</span><span class="sxs-lookup"><span data-stu-id="57e58-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="57e58-150">permitir ou negar</span><span class="sxs-lookup"><span data-stu-id="57e58-150">allow or deny</span></span> |

<span data-ttu-id="57e58-151">Exemplo de NSG no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="57e58-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="57e58-152">Regras de segurança padrão</span><span class="sxs-lookup"><span data-stu-id="57e58-152">Default security rules</span></span>

<span data-ttu-id="57e58-153">As regras de segurança padrão têm as mesmas propriedades disponíveis nas regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="57e58-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="57e58-154">Elas existem para fornecer a conectividade básica entre os recursos com NSGs aplicados.</span><span class="sxs-lookup"><span data-stu-id="57e58-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="57e58-155">Certifique-se de que você sabe quais [regras de segurança padrão](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existem.</span><span class="sxs-lookup"><span data-stu-id="57e58-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="57e58-156">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="57e58-156">Additional resources</span></span>
* <span data-ttu-id="57e58-157">Obtenha mais informações sobre [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="57e58-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="57e58-158">Leia a [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) para obter NSGs.</span><span class="sxs-lookup"><span data-stu-id="57e58-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="57e58-159">Leia a [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) para obter regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="57e58-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
