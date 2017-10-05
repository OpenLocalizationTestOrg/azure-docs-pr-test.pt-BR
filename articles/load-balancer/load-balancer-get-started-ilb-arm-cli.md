---
title: Criar um balanceador de carga interno - CLI do Azure | Microsoft Docs
description: Saiba como criar um balanceador de carga interno no Gerenciador de Recursos usando a CLI do Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="cc84c-103">Criar um balanceador de carga interno usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cc84c-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc84c-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cc84c-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="cc84c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc84c-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="cc84c-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cc84c-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="cc84c-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="cc84c-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="cc84c-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cc84c-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="cc84c-109">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do [modelo de implantação clássico](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cc84c-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="cc84c-110">Implantar a solução usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cc84c-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="cc84c-111">As etapas a seguir mostram como criar um balanceador de carga para a Internet usando o Azure Resource Manager com a CLI.</span><span class="sxs-lookup"><span data-stu-id="cc84c-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="cc84c-112">Com o Azure Resource Manager, todos os recursos são criados e configurados individualmente e colocados juntos para criar um recurso.</span><span class="sxs-lookup"><span data-stu-id="cc84c-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="cc84c-113">Você precisa criar e configurar os seguintes objetos para implantar um balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="cc84c-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="cc84c-114">**Configuração de IP de front-end**: contém endereços IP públicos para o tráfego de rede de entrada</span><span class="sxs-lookup"><span data-stu-id="cc84c-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="cc84c-115">**Pool de endereços de back-end**: contém NICs (interfaces de rede) que permitem que as máquinas virtuais recebam o tráfego de rede do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cc84c-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="cc84c-116">**Regras de balanceamento de carga**: contém regras que mapeiam uma porta pública no balanceador de carga para uma porta no pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="cc84c-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="cc84c-117">**Regras NAT de entrada**: contém regras que mapeiam uma porta pública no balanceador de carga para uma porta de uma máquina virtual específica no pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="cc84c-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="cc84c-118">**Investigações**: contém investigações de integridade usadas para verificar a disponibilidade de instâncias de máquinas virtuais no pool de endereços de back-end</span><span class="sxs-lookup"><span data-stu-id="cc84c-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="cc84c-119">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="cc84c-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="cc84c-120">Configurar a CLI para usar o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="cc84c-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="cc84c-121">Se você nunca tiver usado a CLI do Azure, consulte [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cc84c-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="cc84c-122">Siga as instruções até o ponto onde você seleciona a conta e a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84c-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="cc84c-123">Execute o comando **azure config mode** para alternar para o modo do Resource Manager, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cc84c-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="cc84c-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="cc84c-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="cc84c-125">Criar um balanceador de carga interno, passo a passo</span><span class="sxs-lookup"><span data-stu-id="cc84c-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="cc84c-126">Entre no Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84c-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="cc84c-127">Inserir as credenciais do Azure, quando for solicitado.</span><span class="sxs-lookup"><span data-stu-id="cc84c-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="cc84c-128">Altere as ferramentas de comando para o modo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc84c-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="cc84c-129">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="cc84c-129">Create a resource group</span></span>

<span data-ttu-id="cc84c-130">Todos os recursos no Azure Resource Manager estão associados a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc84c-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="cc84c-131">Se você ainda não fez isso, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cc84c-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="cc84c-132">Criar um conjunto do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="cc84c-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="cc84c-133">Criar um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="cc84c-133">Create an internal load balancer</span></span>

    <span data-ttu-id="cc84c-134">No cenário a seguir, é criado um grupo de recursos chamado nrprg na região Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="cc84c-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="cc84c-135">Todos os recursos de balanceadores de carga internos, como redes virtuais e sub-redes da rede virtual, devem estar no mesmo grupo de recursos e na mesma região.</span><span class="sxs-lookup"><span data-stu-id="cc84c-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="cc84c-136">Crie um endereço IP de front-end para o balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="cc84c-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="cc84c-137">O endereço IP usado deve estar dentro do intervalo da sub-rede de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cc84c-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="cc84c-138">Criar um pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="cc84c-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="cc84c-139">Depois de definir um endereço IP de front-end e um pool de endereços de back-end, você poderá criar regras de balanceador de carga, regras NAT de entrada e investigações de integridade personalizadas.</span><span class="sxs-lookup"><span data-stu-id="cc84c-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="cc84c-140">Crie uma regra do balanceador de carga para o balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="cc84c-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="cc84c-141">Ao executar as etapas anteriores, o comando cria uma regra do balanceador de carga que escuta a porta 1433 no pool de front-end e envia o tráfego de rede com carga balanceada ao pool de endereços de back-end também usando a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="cc84c-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="cc84c-142">Crie regras NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="cc84c-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="cc84c-143">As regras NAT de entrada são usadas para criar pontos de extremidade em um balanceador de carga, que são destinados a uma instância específica de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc84c-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="cc84c-144">As etapas anteriores criaram duas regras NAT para a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="cc84c-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="cc84c-145">Crie investigações de integridade para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="cc84c-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="cc84c-146">Uma investigação de integridade verifica todas as instâncias da máquina virtual para se certificar de que ela pode enviar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="cc84c-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="cc84c-147">A instância de máquina virtual com verificações de investigação com falha é removida do balanceador de carga até ele ficar online novamente e as verificações de investigação determinarem sua integridade.</span><span class="sxs-lookup"><span data-stu-id="cc84c-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="cc84c-148">A plataforma Microsoft Azure usa um endereço IPv4 estático e publicamente roteável para uma variedade de cenários administrativos.</span><span class="sxs-lookup"><span data-stu-id="cc84c-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="cc84c-149">O endereço IP é 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="cc84c-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="cc84c-150">Esse endereço IP não deve ser bloqueado por nenhum firewall porque ele pode causar um comportamento inesperado.</span><span class="sxs-lookup"><span data-stu-id="cc84c-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="cc84c-151">Em relação ao Balanceamento de Carga Interno do Azure, esse endereço IP é usado por testes de monitoramento do balanceador de carga para determinar o estado de integridade para máquinas virtuais em um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="cc84c-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="cc84c-152">Se um grupo de segurança de rede é usado para restringir o tráfego para máquinas virtuais do Azure em um conjunto com balanceamento de carga interno, ou então é aplicado a uma Sub-rede de Rede Virtual, certifique-se de que uma regra de segurança de rede seja adicionada para permitir o tráfego em 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="cc84c-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="cc84c-153">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="cc84c-153">Create NICs</span></span>

<span data-ttu-id="cc84c-154">Você precisa criar NICs (ou modificar as existentes) e associá-las a regras NAT, regras do balanceador de carga e testes.</span><span class="sxs-lookup"><span data-stu-id="cc84c-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="cc84c-155">Crie um NIC chamada *lb-nic1-be* e a associe à regra NAT *rdp1* e ao pool de endereços de back-end *beilb*.</span><span class="sxs-lookup"><span data-stu-id="cc84c-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="cc84c-156">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="cc84c-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="cc84c-157">Crie um NIC chamada *lb-nic2-be* e a associe à regra NAT *rdp2* e ao pool de endereços de back-end *beilb*.</span><span class="sxs-lookup"><span data-stu-id="cc84c-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="cc84c-158">Crie uma máquina virtual chamada *DB1* e a associe à NIC chamada *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="cc84c-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="cc84c-159">Uma conta de armazenamento denominada *web1nrp* é criada antes da execução do comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc84c-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="cc84c-160">As VMs em um balanceador de carga precisam estar no mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="cc84c-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="cc84c-161">Use `azure availset create` para criar um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="cc84c-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="cc84c-162">Crie uma VM (máquina virtual) chamada *DB2* e a associe à NIC chamada *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="cc84c-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="cc84c-163">Uma conta de armazenamento denominada *web1nrp* foi criada antes da execução do comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc84c-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="cc84c-164">Excluir um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cc84c-164">Delete a load balancer</span></span>

<span data-ttu-id="cc84c-165">Para remover um balanceador de carga, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc84c-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="cc84c-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc84c-166">Next steps</span></span>

[<span data-ttu-id="cc84c-167">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="cc84c-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="cc84c-168">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="cc84c-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

