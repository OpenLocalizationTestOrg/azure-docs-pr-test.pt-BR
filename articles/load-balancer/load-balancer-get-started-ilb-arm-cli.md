---
title: aaaCreate um interno carregar balanceador - CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um balanceador de carga interno usando Olá CLI do Azure no Gerenciador de recursos"
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
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="b0559-103">Criar um balanceador de carga interno usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b0559-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0559-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b0559-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="b0559-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0559-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="b0559-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b0559-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="b0559-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="b0559-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b0559-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0559-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b0559-109">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b0559-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="b0559-110">Implantar solução hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b0559-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="b0559-111">Olá, as etapas a seguir mostra como toocreate um voltados para Internet balanceador de carga usando o Gerenciador de recursos do Azure com CLI.</span><span class="sxs-lookup"><span data-stu-id="b0559-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="b0559-112">No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente e juntar toocreate um recurso.</span><span class="sxs-lookup"><span data-stu-id="b0559-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="b0559-113">Você precisa toocreate e configurar Olá objetos toodeploy um balanceador de carga a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0559-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="b0559-114">**Configuração de IP de front-end**: contém endereços IP públicos para o tráfego de rede de entrada</span><span class="sxs-lookup"><span data-stu-id="b0559-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="b0559-115">**Pool de endereços de back-end**: contém as interfaces de rede (NICs) que permitam o tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="b0559-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="b0559-116">**Regras de balanceamento de carga**: contém regras que mapeiam uma porta pública Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação</span><span class="sxs-lookup"><span data-stu-id="b0559-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="b0559-117">**Regras NAT de entrada**: contém regras que mapeiam uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação</span><span class="sxs-lookup"><span data-stu-id="b0559-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="b0559-118">**Testes**: contém investigações de integridade que são usadas toocheck Olá disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação</span><span class="sxs-lookup"><span data-stu-id="b0559-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="b0559-119">Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b0559-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="b0559-120">Configurar CLI toouse Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="b0559-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="b0559-121">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b0559-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="b0559-122">Siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="b0559-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b0559-123">Executar Olá **modo de configuração do azure** comando tooswitch tooResource Manager modo, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b0559-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="b0559-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b0559-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="b0559-125">Criar um balanceador de carga interno, passo a passo</span><span class="sxs-lookup"><span data-stu-id="b0559-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="b0559-126">Entrar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b0559-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="b0559-127">Inserir as credenciais do Azure, quando for solicitado.</span><span class="sxs-lookup"><span data-stu-id="b0559-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="b0559-128">Alterar o modo de Gerenciador de recursos do hello comando ferramentas tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b0559-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="b0559-129">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b0559-129">Create a resource group</span></span>

<span data-ttu-id="b0559-130">Todos os recursos no Azure Resource Manager estão associados a um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b0559-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="b0559-131">Se você ainda não fez isso, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b0559-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="b0559-132">Criar um conjunto do balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="b0559-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="b0559-133">Criar um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="b0559-133">Create an internal load balancer</span></span>

    <span data-ttu-id="b0559-134">Em Olá cenário a seguir, um grupo de recursos chamado nrprg é criado na região Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="b0559-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="b0559-135">Todos os recursos de um balanceador de carga interno, como redes virtuais e sub-redes da rede virtual, devem ser no hello mesmo grupo de recursos e no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="b0559-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="b0559-136">Crie um endereço IP de front-end para o balanceador de carga interno hello.</span><span class="sxs-lookup"><span data-stu-id="b0559-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="b0559-137">endereço IP de saudação que você usa deve ser dentro do intervalo de sub-rede de saudação da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b0559-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="b0559-138">Crie pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0559-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="b0559-139">Depois de definir um endereço IP de front-end e um pool de endereços de back-end, você poderá criar regras de balanceador de carga, regras NAT de entrada e investigações de integridade personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b0559-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="b0559-140">Crie uma regra de Balanceador de carga para o balanceador de carga interno hello.</span><span class="sxs-lookup"><span data-stu-id="b0559-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="b0559-141">Quando você segue etapas anteriores Olá, o comando Olá cria uma regra de Balanceador de carga para escuta tooport 1433 no pool de front-end do hello e envio com balanceamento de carga de rede tráfego toohello back-end pool de endereços, usando a porta 1433.</span><span class="sxs-lookup"><span data-stu-id="b0559-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="b0559-142">Crie regras NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="b0559-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="b0559-143">Regras de NAT de entrada são usados toocreate pontos de extremidade em um balanceador de carga que vão tooa instância de máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="b0559-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="b0559-144">etapas anteriores Olá criadas duas regras NAT para a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="b0559-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="b0559-145">Crie testes de integridade Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b0559-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="b0559-146">Um teste de integridade verifica todos os toomake de instâncias de máquina virtual-se de que eles podem enviar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="b0559-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="b0559-147">instância de máquina virtual de saudação com verificações de investigação com falha será removida do balanceador de carga Olá até que ele ficar online novamente e uma verificação de teste determina que ele esteja íntegro.</span><span class="sxs-lookup"><span data-stu-id="b0559-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="b0559-148">plataforma do Microsoft Azure Olá usa um endereço IPv4 estático, roteável publicamente para uma variedade de cenários administrativos.</span><span class="sxs-lookup"><span data-stu-id="b0559-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="b0559-149">endereço IP de saudação é 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="b0559-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="b0559-150">Esse endereço IP não deve ser bloqueado por nenhum firewall porque ele pode causar um comportamento inesperado.</span><span class="sxs-lookup"><span data-stu-id="b0559-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="b0559-151">Com relação tooAzure balanceamento de carga interno, esse endereço IP é usado pelo monitoramento de testes do estado de integridade de Olá Olá carga balanceador toodetermine para máquinas virtuais em um conjunto com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="b0559-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="b0559-152">Se um grupo de segurança de rede é usada toorestrict tráfego tooAzure VMs em um conjunto de balanceamento de carga internamente ou sub-rede da rede virtual tooa aplicada, certifique-se de que uma regra de segurança de rede é adicionada tooallow tráfego de 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="b0559-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="b0559-153">Criar NICs</span><span class="sxs-lookup"><span data-stu-id="b0559-153">Create NICs</span></span>

<span data-ttu-id="b0559-154">Você precisa toocreate NICs (ou modificar as existentes) e associá-los tooNAT regras, regras de Balanceador de carga e testes.</span><span class="sxs-lookup"><span data-stu-id="b0559-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="b0559-155">Criar uma NIC denominado *lb-nic1 ser*e, em seguida, associe-Olá *rdp1* NAT regra e hello *beilb* pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="b0559-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="b0559-156">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b0559-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
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

2. <span data-ttu-id="b0559-157">Criar uma NIC denominado *lb-nic2 ser*e, em seguida, associe-Olá *rdp2* NAT regra e hello *beilb* pool de endereços de back-end.</span><span class="sxs-lookup"><span data-stu-id="b0559-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="b0559-158">Criar uma máquina virtual denominada *DB1*e, em seguida, associe-Olá NIC denominado *lb-nic1 ser*.</span><span class="sxs-lookup"><span data-stu-id="b0559-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="b0559-159">Uma conta de armazenamento chamado *web1nrp* é criado antes de saudação execuções de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0559-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="b0559-160">Máquinas virtuais em um toobe de necessidade de Balanceador de carga no hello mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b0559-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="b0559-161">Use `azure availset create` toocreate um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b0559-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="b0559-162">Criar uma máquina virtual (VM) denominada *DB2*e, em seguida, associe-Olá NIC denominado *lb-nic2 ser*.</span><span class="sxs-lookup"><span data-stu-id="b0559-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="b0559-163">Uma conta de armazenamento chamado *web1nrp* foi criado antes de executar o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0559-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="b0559-164">Excluir um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b0559-164">Delete a load balancer</span></span>

<span data-ttu-id="b0559-165">tooremove um balanceador de carga, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0559-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="b0559-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b0559-166">Next steps</span></span>

[<span data-ttu-id="b0559-167">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="b0559-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b0559-168">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="b0559-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

