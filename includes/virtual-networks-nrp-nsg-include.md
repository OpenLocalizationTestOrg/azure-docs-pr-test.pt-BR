## <a name="network-security-group"></a><span data-ttu-id="48dcb-101">Grupo de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="48dcb-101">Network Security Group</span></span>
<span data-ttu-id="48dcb-102">Um recurso NSG permite a criação de saudação do limite de segurança para cargas de trabalho, com a implementação de permissão e negação de regras.</span><span class="sxs-lookup"><span data-stu-id="48dcb-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="48dcb-103">Essas regras podem ser aplicadas tooa VM, uma NIC ou uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="48dcb-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="48dcb-104">Propriedade</span><span class="sxs-lookup"><span data-stu-id="48dcb-104">Property</span></span> | <span data-ttu-id="48dcb-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="48dcb-105">Description</span></span> | <span data-ttu-id="48dcb-106">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="48dcb-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48dcb-107">**sub-redes**</span><span class="sxs-lookup"><span data-stu-id="48dcb-107">**subnets**</span></span> |<span data-ttu-id="48dcb-108">Lista de ids de subrede Olá NSG é aplicada ao.</span><span class="sxs-lookup"><span data-stu-id="48dcb-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="48dcb-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="48dcb-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="48dcb-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="48dcb-110">**securityRules**</span></span> |<span data-ttu-id="48dcb-111">Lista de regras de segurança que compõem a saudação NSG</span><span class="sxs-lookup"><span data-stu-id="48dcb-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="48dcb-112">Veja [Regra de segurança](#Security-rule) abaixo</span><span class="sxs-lookup"><span data-stu-id="48dcb-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="48dcb-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="48dcb-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="48dcb-114">Lista de regras de segurança padrão presentes em cada NSG</span><span class="sxs-lookup"><span data-stu-id="48dcb-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="48dcb-115">Veja [Regras de segurança padrão](#Default-security-rules) abaixo</span><span class="sxs-lookup"><span data-stu-id="48dcb-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="48dcb-116">**Regra de segurança** - um NSG um pode ter várias regras de segurança definidas.</span><span class="sxs-lookup"><span data-stu-id="48dcb-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="48dcb-117">Cada regra pode permitir ou negar diferentes tipos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="48dcb-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="48dcb-118">Regra de segurança</span><span class="sxs-lookup"><span data-stu-id="48dcb-118">Security rule</span></span>
<span data-ttu-id="48dcb-119">Uma regra de segurança é um recurso filho de um NSG que contém as propriedades de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="48dcb-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="48dcb-120">Propriedade</span><span class="sxs-lookup"><span data-stu-id="48dcb-120">Property</span></span> | <span data-ttu-id="48dcb-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="48dcb-121">Description</span></span> | <span data-ttu-id="48dcb-122">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="48dcb-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48dcb-123">**description**</span><span class="sxs-lookup"><span data-stu-id="48dcb-123">**description**</span></span> |<span data-ttu-id="48dcb-124">Descrição para a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-124">Description for hello rule</span></span> |<span data-ttu-id="48dcb-125">Permitir tráfego de entrada para todas as VMs na sub-rede X</span><span class="sxs-lookup"><span data-stu-id="48dcb-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="48dcb-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="48dcb-126">**protocol**</span></span> |<span data-ttu-id="48dcb-127">Toomatch de protocolo para a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="48dcb-128">TCP, UDP ou *</span><span class="sxs-lookup"><span data-stu-id="48dcb-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="48dcb-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="48dcb-129">**sourcePortRange**</span></span> |<span data-ttu-id="48dcb-130">Origem toomatch de intervalo de porta para a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="48dcb-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="48dcb-131">80, 100-200, *</span></span> |
| <span data-ttu-id="48dcb-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="48dcb-132">**destinationPortRange**</span></span> |<span data-ttu-id="48dcb-133">Toomatch de intervalo de porta de destino para a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="48dcb-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="48dcb-134">80, 100-200, *</span></span> |
| <span data-ttu-id="48dcb-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="48dcb-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="48dcb-136">Toomatch de prefixo de endereço de origem para regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="48dcb-137">10.10.10.1, 10.10.10.0/24, Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="48dcb-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="48dcb-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="48dcb-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="48dcb-139">Toomatch de prefixo de endereço de destino para a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="48dcb-140">10.10.10.1, 10.10.10.0/24, Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="48dcb-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="48dcb-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="48dcb-141">**direction**</span></span> |<span data-ttu-id="48dcb-142">Direção do tráfego toomatch para regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="48dcb-143">entrada ou saída</span><span class="sxs-lookup"><span data-stu-id="48dcb-143">inbound or outbound</span></span> |
| <span data-ttu-id="48dcb-144">**prioridade**</span><span class="sxs-lookup"><span data-stu-id="48dcb-144">**priority**</span></span> |<span data-ttu-id="48dcb-145">Prioridade de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="48dcb-145">Priority for hello rule.</span></span> <span data-ttu-id="48dcb-146">As regras são verificadas em ordem de prioridade, e depois que uma regra é aplicada, nenhuma outra regra é testada quanto à correspondência.</span><span class="sxs-lookup"><span data-stu-id="48dcb-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="48dcb-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="48dcb-147">10, 100, 65000</span></span> |
| <span data-ttu-id="48dcb-148">**access**</span><span class="sxs-lookup"><span data-stu-id="48dcb-148">**access**</span></span> |<span data-ttu-id="48dcb-149">Tipo de acesso tooapply se corresponder a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="48dcb-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="48dcb-150">permitir ou negar</span><span class="sxs-lookup"><span data-stu-id="48dcb-150">allow or deny</span></span> |

<span data-ttu-id="48dcb-151">Exemplo de NSG no formato JSON:</span><span class="sxs-lookup"><span data-stu-id="48dcb-151">Sample NSG in JSON format:</span></span>

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

### <a name="default-security-rules"></a><span data-ttu-id="48dcb-152">Regras de segurança padrão</span><span class="sxs-lookup"><span data-stu-id="48dcb-152">Default security rules</span></span>

<span data-ttu-id="48dcb-153">Regras de segurança padrão têm Olá mesmas propriedades disponíveis nas regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="48dcb-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="48dcb-154">Elas existem tooprovide a conectividade básica entre os recursos que têm toothem NSGs aplicados.</span><span class="sxs-lookup"><span data-stu-id="48dcb-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="48dcb-155">Certifique-se de que você sabe quais [regras de segurança padrão](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existem.</span><span class="sxs-lookup"><span data-stu-id="48dcb-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="48dcb-156">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="48dcb-156">Additional resources</span></span>
* <span data-ttu-id="48dcb-157">Obtenha mais informações sobre [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="48dcb-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="48dcb-158">Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="48dcb-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="48dcb-159">Saudação de leitura [documentação de referência da API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) para regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="48dcb-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
