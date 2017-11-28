---
title: "Configuração de endereços IP privados para VMs - CLI 2.0 do Azure | Microsoft Docs"
description: "Aprenda a configurar endereços IP privados para máquinas virtuais usando a interface de linha de comando (CLI) 2.0 do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="ac1c6-103">Como configurar endereços IP privados para uma máquina virtual usando a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ac1c6-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ac1c6-104">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="ac1c6-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="ac1c6-105">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="ac1c6-106">[CLI do Azure 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="ac1c6-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="ac1c6-107">[CLI do Azure 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) – nossa CLI da próxima geração para o modelo de implantação do resource manager (este artigo)</span><span class="sxs-lookup"><span data-stu-id="ac1c6-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ac1c6-108">Este artigo aborda o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="ac1c6-109">Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ac1c6-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="ac1c6-110">Os comandos da CLI 2.0 do Azure de exemplo abaixam esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="ac1c6-111">Se você quiser executar os comandos da forma como eles aparecem neste documento, primeiro crie o ambiente de teste descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ac1c6-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="ac1c6-112">Especificar um endereço IP estático e privado ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="ac1c6-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="ac1c6-113">Para criar uma VM denominada *DNS01* na sub-rede *FrontEnd* de uma VNet chamada *TestVNet* com o endereço IP privado estático *192.168.1.101*, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="ac1c6-114">Caso ainda não tenha feito isso, instale e configure a versão mais recente da [CLI do Azure 2.0](/cli/azure/install-az-cli2) e faça logon na conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ac1c6-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="ac1c6-115">Crie um IP público para a VM com o comando [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="ac1c6-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="ac1c6-116">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac1c6-117">Dependendo do seu ambiente, talvez você queira ou precise usar valores diferentes em seus argumentos nesta e nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="ac1c6-118">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="ac1c6-119">`--resource-group`: o nome do grupo de recursos no qual criar o IP público.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="ac1c6-120">`--name`: nome do IP público.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="ac1c6-121">`--location`: região do Azure no qual criar o IP público.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="ac1c6-122">Execute o comando [az network nic create](/cli/azure/network/nic#create) para criar uma NIC com um endereço IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="ac1c6-123">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="ac1c6-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="ac1c6-125">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-125">Parameters:</span></span>

    * <span data-ttu-id="ac1c6-126">`--private-ip-address`: endereço IP privado estático para a NIC.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="ac1c6-127">`--vnet-name`: o nome da VNet na qual criar a NIC.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="ac1c6-128">`--subnet`: o nome da subrede na qual criar a NIC.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="ac1c6-129">Execute o comando [azure vm create](/cli/azure/vm/nic#create) para criar a VM usando o IP público e a NIC criada acima.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="ac1c6-130">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-130">The list shown after the output explains the parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="ac1c6-131">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="ac1c6-132">Parâmetros diferentes dos parâmetros básicos [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ac1c6-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="ac1c6-133">`--nics`: nome da NIC à qual a VM está conectada.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="ac1c6-134">Recuperar informações do endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="ac1c6-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="ac1c6-135">Para exibir o endereço IP privado estático que você criou, execute o seguinte comando CLI do Azure e observe os valores de *método de alocação de IP privado* e *endereço IP privado*:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="ac1c6-136">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="ac1c6-137">Para exibir as informações específicas de IP da NIC da VM em questão, consulte a NIC:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="ac1c6-138">A saída será algo semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="ac1c6-139">Remover o endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="ac1c6-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="ac1c6-140">Você não pode remover um endereço IP privado estático de uma NIC na CLI do Azure para o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="ac1c6-141">Você deve:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-141">You must:</span></span>
- <span data-ttu-id="ac1c6-142">Criar uma nova NIC que usa um IP dinâmico</span><span class="sxs-lookup"><span data-stu-id="ac1c6-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="ac1c6-143">Definir a NIC na VM à NIC recém-criada.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="ac1c6-144">Para alterar a NIC para a VM usada nos comandos acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="ac1c6-145">Execute o comando **azure network nic create** para criar uma nova NIC usando alocação de IP dinâmico com um endereço IP novo.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="ac1c6-146">Observe que quando nenhum endereço IP for especificado, o método de alocação será **dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="ac1c6-147">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="ac1c6-148">Execute o comando **azure vm set** para alterar a NIC usada pela VM.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="ac1c6-149">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ac1c6-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="ac1c6-150">Se a VM for grande o suficiente para ter mais de uma NIC, execute o comando **azure network nic delete** para excluir a NIC antiga.</span><span class="sxs-lookup"><span data-stu-id="ac1c6-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="ac1c6-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac1c6-151">Next steps</span></span>
* <span data-ttu-id="ac1c6-152">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="ac1c6-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ac1c6-153">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="ac1c6-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ac1c6-154">Consulte as [APIs REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac1c6-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

