---
title: "endereços IP privados de aaaConfigure para VMs - 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais usando hello Azure interface de linha de comando (CLI) 2.0."
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
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="056ea-103">Configurar endereços IP para uma máquina virtual usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="056ea-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="056ea-104">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="056ea-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="056ea-105">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="056ea-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="056ea-106">[1.0 de CLI do Azure](virtual-networks-static-private-ip-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá</span><span class="sxs-lookup"><span data-stu-id="056ea-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="056ea-107">[2.0 do CLI do Azure](#specify-a-static-private-ip-address-when-creating-a-vm) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="056ea-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="056ea-108">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="056ea-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="056ea-109">Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="056ea-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="056ea-110">comandos do Azure CLI 2.0 de exemplo Hello abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="056ea-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="056ea-111">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="056ea-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="056ea-112">Especificar um endereço IP estático e privado ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="056ea-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="056ea-113">toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="056ea-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="056ea-114">Se você ainda não tiver ainda, instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="056ea-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="056ea-115">Criar um IP público para Olá VM com hello [criar az rede ip público](/cli/azure/network/public-ip#create) comando.</span><span class="sxs-lookup"><span data-stu-id="056ea-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="056ea-116">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="056ea-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="056ea-117">Você pode desejar ou precisar toouse diferentes valores para seus argumentos nesta e as etapas subsequentes, dependendo de seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="056ea-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="056ea-118">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="056ea-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="056ea-119">`--resource-group`: Nome do grupo de recursos de saudação no toocreate Olá IP público.</span><span class="sxs-lookup"><span data-stu-id="056ea-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="056ea-120">`--name`: Nome do IP público hello.</span><span class="sxs-lookup"><span data-stu-id="056ea-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="056ea-121">`--location`: Região do azure no toocreate Olá IP público.</span><span class="sxs-lookup"><span data-stu-id="056ea-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="056ea-122">Executar Olá [nic da rede az criar](/cli/azure/network/nic#create) comando toocreate uma NIC com um endereço IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="056ea-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="056ea-123">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="056ea-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="056ea-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="056ea-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="056ea-125">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="056ea-125">Parameters:</span></span>

    * <span data-ttu-id="056ea-126">`--private-ip-address`: Endereço IP privado estático para Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="056ea-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="056ea-127">`--vnet-name`: O nome do VNet Olá no qual toocreate Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="056ea-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="056ea-128">`--subnet`: O nome da sub-rede de saudação no qual Olá toocreate NIC.</span><span class="sxs-lookup"><span data-stu-id="056ea-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="056ea-129">Executar Olá [criar vm do azure](/cli/azure/vm/nic#create) saudação do comando toocreate VM usando o IP público hello e NIC criado acima.</span><span class="sxs-lookup"><span data-stu-id="056ea-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="056ea-130">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="056ea-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="056ea-131">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="056ea-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="056ea-132">Parâmetros diferentes Olá básico [criar vm az](/cli/azure/vm#create) parâmetros.</span><span class="sxs-lookup"><span data-stu-id="056ea-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="056ea-133">`--nics`: O nome da saudação toowhich da NIC Olá VM está conectado.</span><span class="sxs-lookup"><span data-stu-id="056ea-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="056ea-134">Recuperar informações do endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="056ea-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="056ea-135">tooview Olá endereço IP privado estático que você criou, execute Olá após o comando CLI do Azure e observar os valores de saudação para *método de alocação de IP privado* e *endereço IP privado*:</span><span class="sxs-lookup"><span data-stu-id="056ea-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="056ea-136">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="056ea-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="056ea-137">toodisplay Olá informações de IP específicas de saudação NIC para a VM, Olá consulta NIC especificamente:</span><span class="sxs-lookup"><span data-stu-id="056ea-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="056ea-138">saída de Hello tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="056ea-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="056ea-139">Remover o endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="056ea-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="056ea-140">Você não pode remover um endereço IP privado estático de uma NIC na CLI do Azure para o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="056ea-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="056ea-141">Você deve:</span><span class="sxs-lookup"><span data-stu-id="056ea-141">You must:</span></span>
- <span data-ttu-id="056ea-142">Criar uma nova NIC que usa um IP dinâmico</span><span class="sxs-lookup"><span data-stu-id="056ea-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="056ea-143">Definir Olá NIC em Olá Olá VM recém-criada NIC.</span><span class="sxs-lookup"><span data-stu-id="056ea-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="056ea-144">Olá toochange NIC para Olá VM usada em comandos de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="056ea-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="056ea-145">Executar Olá **nic de rede do azure criar** comando toocreate uma nova NIC usando a alocação de IP dinâmico com um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="056ea-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="056ea-146">Observe que porque nenhum endereço IP for especificado, o método de alocação Olá **dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="056ea-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="056ea-147">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="056ea-147">Expected output:</span></span>

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

2. <span data-ttu-id="056ea-148">Executar Olá **conjunto de vm do azure** saudação do comando toochange NIC usada por Olá VM.</span><span class="sxs-lookup"><span data-stu-id="056ea-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="056ea-149">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="056ea-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="056ea-150">Se Olá VM for grande o suficiente toohave mais de uma NIC, executar Olá **nic de rede do azure excluir** comando toodelete Olá antigo placa de rede.</span><span class="sxs-lookup"><span data-stu-id="056ea-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="056ea-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="056ea-151">Next steps</span></span>
* <span data-ttu-id="056ea-152">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="056ea-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="056ea-153">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="056ea-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="056ea-154">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="056ea-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

