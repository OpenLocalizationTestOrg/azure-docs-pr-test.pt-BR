---
title: "aaaNetworking para conjuntos de escala de máquina virtual do Azure | Microsoft Docs"
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="bea65-103">Rede para conjuntos de dimensionamento de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="bea65-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="bea65-104">Quando você implanta uma escala de máquina virtual do Azure definido por meio do portal hello, determinadas propriedades de rede são padronizadas, por exemplo um balanceador de carga do Azure com as regras de NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="bea65-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="bea65-105">Este artigo descreve como toouse alguns hello mais avançados recursos de rede que você pode configurar com escala define.</span><span class="sxs-lookup"><span data-stu-id="bea65-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="bea65-106">Você pode configurar todos os recursos de saudação abordados neste artigo usando modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bea65-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="bea65-107">Exemplos da CLI do Azure e PowerShell também estão incluídos para os recursos selecionados.</span><span class="sxs-lookup"><span data-stu-id="bea65-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="bea65-108">Use a CLI 2.10 e o PowerShell 4.2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bea65-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="bea65-109">Rede Acelerada</span><span class="sxs-lookup"><span data-stu-id="bea65-109">Accelerated Networking</span></span>
<span data-ttu-id="bea65-110">Azure [acelerado rede](../virtual-network/virtual-network-create-vm-accelerated-networking.md) melhora o desempenho da rede, permitindo que a máquina virtual do e/s de raiz única (SR-IOV) virtualização tooa.</span><span class="sxs-lookup"><span data-stu-id="bea65-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="bea65-111">toouse acelerado de rede com conjuntos de escala, defina enableAcceleratedNetworking muito**true** nas configurações de networkInterfaceConfigurations do conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="bea65-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="bea65-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="bea65-113">Criar um conjunto de dimensionamento que faz referência a um Azure Load Balancer existente</span><span class="sxs-lookup"><span data-stu-id="bea65-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="bea65-114">Quando um conjunto de escala é criado usando Olá portal do Azure, um balanceador de carga novo é criado para a maioria das opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="bea65-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="bea65-115">Se você criar um conjunto de escala, o que precisa tooreference um balanceador de carga, você pode fazer isso usando a CLI.</span><span class="sxs-lookup"><span data-stu-id="bea65-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="bea65-116">Olá, script de exemplo a seguir cria um balanceador de carga e, em seguida, cria um conjunto de escala, o que faz referência a ela:</span><span class="sxs-lookup"><span data-stu-id="bea65-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="bea65-117">Configurações DNS configuráveis</span><span class="sxs-lookup"><span data-stu-id="bea65-117">Configurable DNS Settings</span></span>
<span data-ttu-id="bea65-118">Por padrão, conjuntos de escala leva em configurações específicas de DNS Olá Olá rede virtual e sub-rede que foram criados.</span><span class="sxs-lookup"><span data-stu-id="bea65-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="bea65-119">No entanto, você pode definir configurações de DNS Olá para uma escala definida diretamente.</span><span class="sxs-lookup"><span data-stu-id="bea65-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="bea65-120">Como criar um conjunto de dimensionamento com servidores DNS configuráveis</span><span class="sxs-lookup"><span data-stu-id="bea65-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="bea65-121">toocreate uma escala definida com uma configuração de DNS personalizada usando a CLI 2.0, adicionar Olá **servidores dns -** argumento toohello **vmss criar** separados de comando, seguido por um espaço de endereços ip do servidor.</span><span class="sxs-lookup"><span data-stu-id="bea65-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="bea65-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="bea65-123">tooconfigure servidores DNS personalizados em um modelo do Azure, adicione uma escala de toohello propriedade dnsSettings definir networkInterfaceConfigurations seção.</span><span class="sxs-lookup"><span data-stu-id="bea65-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="bea65-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="bea65-125">Como criar um conjunto de dimensionamento com nomes de domínio configuráveis de máquina de virtual</span><span class="sxs-lookup"><span data-stu-id="bea65-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="bea65-126">toocreate uma escala definida com um nome DNS personalizado para máquinas virtuais usando a CLI 2.0, adicionar Olá **nome de domínio - vm** argumento toohello **vmss criar** comando, seguido por uma cadeia de caracteres que representa o nome de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="bea65-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="bea65-127">nome de domínio Olá tooset em um modelo do Azure, adicione um **dnsSettings** conjunto de escalas da propriedade toohello **networkInterfaceConfigurations** seção.</span><span class="sxs-lookup"><span data-stu-id="bea65-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="bea65-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-128">For example:</span></span>

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

<span data-ttu-id="bea65-129">saudação de saída, para um nome de dns da máquina virtual individual seria em Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="bea65-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="bea65-130">IPv4 público por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bea65-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="bea65-131">Em geral, as máquinas de virtuais do conjunto de dimensionamento do Azure não exigem seus próprios endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="bea65-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="bea65-132">Na maioria dos cenários, é mais seguro e econômico tooassociate uma público IP endereço tooa carga balanceador tooan individual máquina virtual ou (também conhecido como um jumpbox), que encaminha entrada máquinas de virtuais conexões tooscale conjunto conforme necessário (por exemplo, por meio de regras de NAT entrada).</span><span class="sxs-lookup"><span data-stu-id="bea65-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="bea65-133">No entanto, alguns cenários exigem um conjunto de escala de máquinas virtuais toohave seus endereços IP público endereços.</span><span class="sxs-lookup"><span data-stu-id="bea65-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="bea65-134">Um exemplo é jogos, onde um console precisa toomake uma conexão direta tooa nuvem máquina virtual, que está fazendo o processamento de jogo física.</span><span class="sxs-lookup"><span data-stu-id="bea65-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="bea65-135">Outro exemplo é onde necessário toomake conexões externas tooone as máquinas virtuais outra entre regiões em um banco de dados distribuído.</span><span class="sxs-lookup"><span data-stu-id="bea65-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="bea65-136">Como criar um conjunto de dimensionamento com IP público por máquina de virtual</span><span class="sxs-lookup"><span data-stu-id="bea65-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="bea65-137">toocreate um conjunto de escala que atribui uma público IP endereço tooeach máquina virtual com 2.0 do CLI, adicionar Olá **-ip público por vm** parâmetro toohello **vmss criar** comando.</span><span class="sxs-lookup"><span data-stu-id="bea65-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="bea65-138">toocreate uma escala definida usando um modelo do Azure, certifique-se de saudação API versão de hello Microsoft.Compute/virtualMachineScaleSets recurso é pelo menos **2017-03-30**e adicione um **publicIpAddressConfiguration**IpConfigurations seção de conjuntos de escala de toohello de propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="bea65-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="bea65-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="bea65-140">Modelo de exemplo: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="bea65-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="bea65-141">Consultando o IP público Olá conjunto de endereços de máquinas virtuais de saudação em uma escala</span><span class="sxs-lookup"><span data-stu-id="bea65-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="bea65-142">toolist Olá os endereços IP públicos atribuídos tooscale máquinas virtuais de conjunto usando 2.0 do CLI, use Olá **az vmss ips-público-instância-lista** comando.</span><span class="sxs-lookup"><span data-stu-id="bea65-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="bea65-143">conjunto de escala de toolist de endereços IP públicos usando o PowerShell, use Olá _AzureRmPublicIpAddress Get_ comando.</span><span class="sxs-lookup"><span data-stu-id="bea65-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="bea65-144">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="bea65-145">Você também pode consulta Olá os endereços IP públicos referenciando a id de recurso de saudação da configuração de endereço IP pública Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="bea65-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="bea65-146">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="bea65-147">tooquery Olá os endereços IP públicos atribuídos tooscale máquinas virtuais de conjunto usando Olá [Gerenciador de recursos do Azure](https://resources.azure.com), ou Olá API REST do Azure com a versão **2017-03-30** ou superior.</span><span class="sxs-lookup"><span data-stu-id="bea65-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="bea65-148">endereços IP públicos de tooview para uma escala definidas usando Olá Gerenciador de recursos, examinar Olá **publicipaddresses** seção em seu conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="bea65-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="bea65-149">Por exemplo: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="bea65-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="bea65-150">Saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="bea65-151">Vários endereços IP por NIC</span><span class="sxs-lookup"><span data-stu-id="bea65-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="bea65-152">Cada NIC conectada tooa que VM em um conjunto de escala pode ter uma ou mais configurações de IP associadas a ele.</span><span class="sxs-lookup"><span data-stu-id="bea65-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="bea65-153">Cada configuração é atribuída a um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="bea65-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="bea65-154">Cada configuração também pode ter um recurso de endereço IP público associado a ela.</span><span class="sxs-lookup"><span data-stu-id="bea65-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="bea65-155">toounderstand quantos endereços IP pode ser atribuído a tooa NIC, e quantos endereços IP públicos, você pode usar em uma assinatura do Azure, consulte muito[limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="bea65-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="bea65-156">Várias NICs por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bea65-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="bea65-157">Você pode ter até too8 NICs por máquina virtual, dependendo do tamanho da máquina.</span><span class="sxs-lookup"><span data-stu-id="bea65-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="bea65-158">número máximo de saudação de NICs por máquina está disponível no hello [artigo de tamanho VM](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="bea65-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="bea65-159">Olá exemplo a seguir é que uma escala Defina o perfil de rede mostrando várias entradas NIC e vários IPs públicos por máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="bea65-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="bea65-160">NSG por conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="bea65-160">NSG per scale set</span></span>
<span data-ttu-id="bea65-161">Grupos de segurança de rede podem ser aplicados diretamente o conjunto de escala tooa, adicionando uma seção de referência toohello rede interface configuração de escala de saudação definir propriedades de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bea65-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="bea65-162">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bea65-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="bea65-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bea65-163">Next steps</span></span>
<span data-ttu-id="bea65-164">Para obter mais informações sobre redes virtuais do Azure, consulte muito[esta documentação](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bea65-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
