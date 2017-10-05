---
title: "Rede para conjuntos de dimensionamento de máquinas virtuais do Azure | Microsoft Docs"
description: "Propriedades da rede de configuração dos conjuntos de dimensionamento de máquina virtual do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="8fbb0-103">Rede para conjuntos de dimensionamento de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="8fbb0-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="8fbb0-104">Quando você implanta um conjunto de dimensionamento de máquinas virtuais do Azure pelo portal, determinadas propriedades de rede são padronizadas, por exemplo um Azure Load Balancer com regras NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="8fbb0-105">Este artigo descreve como usar alguns dos recursos mais avançados de rede que podem ser configurados com conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="8fbb0-106">Todos os recursos discutidos neste artigo podem ser configurados usando modelos do ARM (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="8fbb0-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="8fbb0-107">Exemplos da CLI do Azure e PowerShell também estão incluídos para os recursos selecionados.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="8fbb0-108">Use a CLI 2.10 e o PowerShell 4.2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="8fbb0-109">Rede Acelerada</span><span class="sxs-lookup"><span data-stu-id="8fbb0-109">Accelerated Networking</span></span>
<span data-ttu-id="8fbb0-110">A [Rede Acelerada](../virtual-network/virtual-network-create-vm-accelerated-networking.md) permite SR-IOV (Virtualização de E/S de Raiz Única) para uma VM (máquina virtual), melhorando muito seu desempenho de rede.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="8fbb0-111">Para usar a rede acelerado com conjuntos de dimensionamento, defina enableAcceleratedNetworking como **true** nas configurações de networkInterfaceConfigurations do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="8fbb0-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="8fbb0-113">Criar um conjunto de dimensionamento que faz referência a um Azure Load Balancer existente</span><span class="sxs-lookup"><span data-stu-id="8fbb0-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="8fbb0-114">Quando um conjunto de dimensionamento é criado usando o portal do Azure, um balanceador de carga novo é criado para a maioria das opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="8fbb0-115">Se você criar um conjunto de dimensionamento, que precisa fazer referência a um balanceador de carga existente, isso pode ser feito usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="8fbb0-116">O script de exemplo a seguir cria um balanceador de carga e, em seguida, cria um conjunto de dimensionamento que faz referência a ele:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="8fbb0-117">Configurações DNS configuráveis</span><span class="sxs-lookup"><span data-stu-id="8fbb0-117">Configurable DNS Settings</span></span>
<span data-ttu-id="8fbb0-118">Por padrão, os conjuntos de dimensionamento assumem as configurações DNS específicas da VNET e da sub-rede na qual eles foram criados.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="8fbb0-119">No entanto, você pode definir diretamente as configurações DNS de um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="8fbb0-120">Como criar um conjunto de dimensionamento com servidores DNS configuráveis</span><span class="sxs-lookup"><span data-stu-id="8fbb0-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="8fbb0-121">Para criar um conjunto de dimensionamento com uma configuração DNS personalizada usando a CLI 2.0, adicione o argumento **--dns-servers** ao comando **vmss create**, seguido por endereços IP do servidor separados por espaços.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="8fbb0-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="8fbb0-123">Para configurar servidores DNS personalizados em um modelo do Azure, adicione uma propriedade dnsSettings à seção de networkInterfaceConfigurations do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="8fbb0-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="8fbb0-125">Como criar um conjunto de dimensionamento com nomes de domínio configuráveis de máquina de virtual</span><span class="sxs-lookup"><span data-stu-id="8fbb0-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="8fbb0-126">Para criar um conjunto de dimensionamento com um nome DNS personalizado para máquinas virtuais usando a CLI 2.0, adicione o argumento **--vm-domain-name** ao comando **vmss create**, seguido por uma cadeia de caracteres representando o nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="8fbb0-127">Para configurar o nome de domínio em um modelo do Azure, adicione uma propriedade **dnsSettings** à seção **networkInterfaceConfigurations**  do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="8fbb0-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="8fbb0-129">A saída, para um nome de dns de máquina virtual individual teria no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="8fbb0-130">IPv4 público por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8fbb0-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="8fbb0-131">Em geral, as máquinas de virtuais do conjunto de dimensionamento do Azure não exigem seus próprios endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="8fbb0-132">Na maioria dos cenários, é mais econômico e seguro associar um endereço IP público a um balanceador de carga ou a uma máquina virtual individual (também conhecida como um jumpbox) que encaminha as conexões de entrada para dimensionar máquinas virtuais do conjunto de dimensionamento, conforme necessário (por exemplo, por meio de regras NAT de entrada).</span><span class="sxs-lookup"><span data-stu-id="8fbb0-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="8fbb0-133">No entanto, alguns cenários exigem que as máquinas de virtuais do conjunto de dimensionamento do Azure tenham seus próprios endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="8fbb0-134">Um exemplo é o jogo, onde um console precisa fazer uma conexão direta com uma máquina virtual da nuvem, que está fazendo o processamento da física do jogo.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="8fbb0-135">Outro exemplo é onde as máquinas virtuais precisam fazer conexões externas umas com as outras em regiões em um banco de dados distribuído.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="8fbb0-136">Como criar um conjunto de dimensionamento com IP público por máquina de virtual</span><span class="sxs-lookup"><span data-stu-id="8fbb0-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="8fbb0-137">Para criar um conjunto de dimensionamento que atribui um endereço IP público para cada máquina virtual com a CLI 2.0, adicione o parâmetro **--public-ip-per-vm** ao comando **vmss create**.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="8fbb0-138">Para criar um conjunto de dimensionamento usando um modelo do Azure, verifique se a versão da API do recurso Microsoft.Compute/virtualMachineScaleSets seja, pelo menos, **2017-03-30** e adicione uma propriedade JSON **publicIpAddressConfiguration** à seção ipConfigurations do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="8fbb0-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="8fbb0-140">Modelo de exemplo: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="8fbb0-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="8fbb0-141">Como consultar os endereços IP públicos das máquinas virtuais em um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8fbb0-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="8fbb0-142">Use o comando **az vmss list-instance-public-ips** para listar os endereços IP públicos atribuídos às máquinas virtuais do conjunto de dimensionamento usando a CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="8fbb0-143">Para listar os endereços IP públicos do conjunto de dimensionamento usando o PowerShell, use o comando _Get-AzureRmPublicIpAddress_.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="8fbb0-144">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="8fbb0-145">Você também pode consultar diretamente os endereços IP públicos referenciando a ID de recurso da configuração de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="8fbb0-146">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="8fbb0-147">Para consultar os endereços IP públicos atribuídos às máquinas virtuais do conjunto de dimensionamento usando o [Azure Resource Explorer](https://resources.azure.com) ou a API REST do Azure com a versão **2017-03-30** ou superior.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="8fbb0-148">Para exibir os endereços IP públicos de um conjunto de dimensionamento usando o Resource Explorer, consulte a seção **publicipaddresses** em seu conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="8fbb0-149">Por exemplo: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="8fbb0-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="8fbb0-150">Saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="8fbb0-151">Vários endereços IP por NIC</span><span class="sxs-lookup"><span data-stu-id="8fbb0-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="8fbb0-152">Todas as NICs anexadas a uma VM em um conjunto de dimensionamento têm uma ou mais configurações IP associadas a elas.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="8fbb0-153">Cada configuração é atribuída a um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="8fbb0-154">Cada configuração também pode ter um recurso de endereço IP público associado a ela.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="8fbb0-155">Para entender quantos endereços IP podem ser atribuídos a uma NIC e quantos endereços IP públicos você pode usar em uma assinatura do Azure, confira [Limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="8fbb0-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="8fbb0-156">Várias NICs por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8fbb0-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="8fbb0-157">Você pode ter até 8 NICs por máquina virtual, dependendo do tamanho da máquina.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="8fbb0-158">O número máximo de NICs por máquina está disponível no [artigo Tamanho de VM](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8fbb0-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="8fbb0-159">O exemplo a seguir é um perfil de rede do conjunto de dimensionamento mostrando várias entradas NIC e vários IPs públicos por máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="8fbb0-160">NSG por conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8fbb0-160">NSG per scale set</span></span>
<span data-ttu-id="8fbb0-161">Os Grupos de Segurança de Rede podem ser aplicados diretamente a um conjunto de dimensionamento referenciando-os na seção de configuração da interface de rede das propriedades de máquina virtual do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8fbb0-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="8fbb0-162">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fbb0-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="8fbb0-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fbb0-163">Next steps</span></span>
<span data-ttu-id="8fbb0-164">Para obter mais informações sobre redes do Azure, confira [essa documentação](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fbb0-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
