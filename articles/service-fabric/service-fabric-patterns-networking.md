---
title: "Padrões de rede do Service Fabric do Azure | Microsoft Docs"
description: "Descreve os padrões de rede comuns do Service Fabric e como criar um cluster usando os recursos de rede do Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 126637002b24391058fb702227a570aa0b58c1d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="9a706-103">Padrões de rede do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9a706-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="9a706-104">Você pode integrar seu cluster do Azure Service Fabric a outros recursos de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a706-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="9a706-105">Neste artigo, mostramos como criar clusters que usam os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="9a706-105">In this article, we show you how to create clusters that use the following features:</span></span>

- [<span data-ttu-id="9a706-106">Rede virtual ou sub-rede existente</span><span class="sxs-lookup"><span data-stu-id="9a706-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="9a706-107">Endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="9a706-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="9a706-108">Balanceador de carga somente interno</span><span class="sxs-lookup"><span data-stu-id="9a706-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="9a706-109">Balanceador interno e externo de carga</span><span class="sxs-lookup"><span data-stu-id="9a706-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="9a706-110">O Service Fabric é executado em um conjunto de dimensionamento de máquinas virtuais padrão.</span><span class="sxs-lookup"><span data-stu-id="9a706-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="9a706-111">Qualquer funcionalidade que você pode usar em um conjunto de dimensionamento de máquinas virtuais você pode usar também com um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9a706-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="9a706-112">As seções de rede dos modelos do Azure Resource Manager para os conjuntos de dimensionamento de máquinas virtuais e o Service Fabric são idênticas.</span><span class="sxs-lookup"><span data-stu-id="9a706-112">The networking sections of the Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="9a706-113">Depois de implantar uma rede virtual existente, é fácil incorporar outros recursos de rede como o Azure ExpressRoute, o Gateway de VPN do Azure, um grupo de segurança de rede e emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9a706-113">After you deploy to an existing virtual network, it's easy to incorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="9a706-114">O Service Fabric é único entre outros recursos de rede em um aspecto.</span><span class="sxs-lookup"><span data-stu-id="9a706-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="9a706-115">O [portal do Azure](https://portal.azure.com) usa internamente o provedor de recursos do Service Fabric para chamar um cluster para obter informações sobre nós e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9a706-115">The [Azure portal](https://portal.azure.com) internally uses the Service Fabric resource provider to call to a cluster to get information about nodes and applications.</span></span> <span data-ttu-id="9a706-116">O provedor de recursos do Service Fabric exige acesso de entrada acessível publicamente à porta do Gateway HTTP (19080 por padrão) no ponto de extremidade de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="9a706-116">The Service Fabric resource provider requires publicly accessible inbound access to the HTTP gateway port (port 19080, by default) on the management endpoint.</span></span> <span data-ttu-id="9a706-117">O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) usa o ponto de extremidade de gerenciamento para gerenciar o cluster.</span><span class="sxs-lookup"><span data-stu-id="9a706-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses the management endpoint to manage your cluster.</span></span> <span data-ttu-id="9a706-118">Essa porta também é usada pelo provedor de recursos do Service Fabric para consultar informações sobre o cluster para exibição no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a706-118">The Service Fabric resource provider also uses this port to query information about your cluster, to display in the Azure portal.</span></span> 

<span data-ttu-id="9a706-119">Se a porta 19080 não estiver acessível no provedor de recursos do Service Fabric, uma mensagem como *Nós Não Encontrados* será exibida no portal e a lista de nós e aplicativos aparecerá vazia.</span><span class="sxs-lookup"><span data-stu-id="9a706-119">If port 19080 is not accessible from the Service Fabric resource provider, a message like *Nodes Not Found* appears in the portal, and your node and application list appears empty.</span></span> <span data-ttu-id="9a706-120">Se desejar ver o cluster por meio do Portal do Azure, o balanceador de carga deverá expor um endereço IP público e o grupo de segurança de rede deverá permitir o tráfego de entrada pela porta 19080.</span><span class="sxs-lookup"><span data-stu-id="9a706-120">If you want to see your cluster in the Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="9a706-121">Se a sua configuração não atender a esses requisitos, o Portal do Azure não exibirá o status atual do cluster.</span><span class="sxs-lookup"><span data-stu-id="9a706-121">If your setup does not meet these requirements, the Azure portal does not display the status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="9a706-122">Modelos</span><span class="sxs-lookup"><span data-stu-id="9a706-122">Templates</span></span>

<span data-ttu-id="9a706-123">Todos os modelos do Service Fabric estão em [um arquivo de download](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="9a706-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="9a706-124">Você deverá conseguir implantar os modelos no estado em que se encontram usando os comandos do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="9a706-124">You should be able to deploy the templates as-is by using the following PowerShell commands.</span></span> <span data-ttu-id="9a706-125">Se você estiver implantando o modelo de rede Virtual do Azure existente ou o modelo de IP público estático, leia primeiro a seção [Instalação inicial](#initialsetup) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="9a706-125">If you are deploying the existing Azure Virtual Network template or the static public IP template, first read the [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="9a706-126">Configuração inicial</span><span class="sxs-lookup"><span data-stu-id="9a706-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="9a706-127">Rede virtual existente</span><span class="sxs-lookup"><span data-stu-id="9a706-127">Existing virtual network</span></span>

<span data-ttu-id="9a706-128">No exemplo a seguir, começamos com uma rede virtual existente chamada ExistingRG-vnet no grupo de recursos **ExistingRG**.</span><span class="sxs-lookup"><span data-stu-id="9a706-128">In the following example, we start with an existing virtual network named ExistingRG-vnet, in the **ExistingRG** resource group.</span></span> <span data-ttu-id="9a706-129">Essa sub-rede é chamada de default.</span><span class="sxs-lookup"><span data-stu-id="9a706-129">The subnet is named default.</span></span> <span data-ttu-id="9a706-130">Esses recursos padrão são criados ao usar o Portal do Azure para criar uma VM (máquina virtual) padrão.</span><span class="sxs-lookup"><span data-stu-id="9a706-130">These default resources are created when you use the Azure portal to create a standard virtual machine (VM).</span></span> <span data-ttu-id="9a706-131">Você pode criar a rede virtual e a sub-rede sem criar a VM, mas a meta principal de adicionar um cluster a uma rede virtual existente é fornecer conectividade de rede para outras VMs.</span><span class="sxs-lookup"><span data-stu-id="9a706-131">You could create the virtual network and subnet without creating the VM, but the main goal of adding a cluster to an existing virtual network is to provide network connectivity to other VMs.</span></span> <span data-ttu-id="9a706-132">Criar a VM fornece um bom exemplo de como uma rede virtual existente é normalmente usada.</span><span class="sxs-lookup"><span data-stu-id="9a706-132">Creating the VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="9a706-133">Se o cluster do Service Fabric usar apenas um balanceador de carga interno sem um endereço IP público, a VM e seu IP público poderão ser usados como uma *jump box*.</span><span class="sxs-lookup"><span data-stu-id="9a706-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use the VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="9a706-134">Endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="9a706-134">Static public IP address</span></span>

<span data-ttu-id="9a706-135">Um endereço IP público estático geralmente é um recurso dedicado gerenciado separadamente da VM ou VMs às quais ele é atribuído.</span><span class="sxs-lookup"><span data-stu-id="9a706-135">A static public IP address generally is a dedicated resource that's managed separately from the VM or VMs it's assigned to.</span></span> <span data-ttu-id="9a706-136">Ele é provisionado em um grupo de recursos de rede dedicado (em vez de no grupo de recursos de cluster do Service Fabric em si).</span><span class="sxs-lookup"><span data-stu-id="9a706-136">It's provisioned in a dedicated networking resource group (as opposed to in the Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="9a706-137">Crie um endereço IP público estático com o nome staticIP1 no mesmo grupo de recursos ExistingRG no Portal do Azure ou usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9a706-137">Create a static public IP address named staticIP1 in the same ExistingRG resource group, either in the Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="9a706-138">Modelo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9a706-138">Service Fabric template</span></span>

<span data-ttu-id="9a706-139">Nos exemplos neste artigo, usamos o template.json do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9a706-139">In the examples in this article, we use the Service Fabric template.json.</span></span> <span data-ttu-id="9a706-140">Você pode usar o Assistente do portal padrão para baixar o modelo por meio do Portal antes de criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="9a706-140">You can use the standard portal wizard to download the template from the portal before you create a cluster.</span></span> <span data-ttu-id="9a706-141">Você também pode usar um dos modelos da [galeria de modelos](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), por exemplo o [cluster de cinco nós do Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="9a706-141">You also can use one of the templates in the [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like the [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="9a706-142">Rede virtual ou sub-rede existente</span><span class="sxs-lookup"><span data-stu-id="9a706-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="9a706-143">Altere o parâmetro da sub-rede para o nome da sub-rede existente e adicione dois novos parâmetros para referenciar a rede virtual existente:</span><span class="sxs-lookup"><span data-stu-id="9a706-143">Change the subnet parameter to the name of the existing subnet, and then add two new parameters to reference the existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="9a706-144">Altere a variável `vnetID` para que ela aponte para a rede virtual existente:</span><span class="sxs-lookup"><span data-stu-id="9a706-144">Change the `vnetID` variable to point to the existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="9a706-145">Remova `Microsoft.Network/virtualNetworks` de seus recursos de modo que o Azure não crie uma nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="9a706-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="9a706-146">Comente a rede virtual com base no atributo `dependsOn` de `Microsoft.Compute/virtualMachineScaleSets`, de modo que você não dependa da criação de uma nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="9a706-146">Comment out the virtual network from the `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="9a706-147">Implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="9a706-147">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="9a706-148">Após a implantação, sua rede virtual deverá incluir as VMs do novo conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9a706-148">After deployment, your virtual network should include the new scale set VMs.</span></span> <span data-ttu-id="9a706-149">O tipo de nó de conjunto de dimensionamento de máquinas virtuais deve mostrar a rede virtual e a sub-rede existentes.</span><span class="sxs-lookup"><span data-stu-id="9a706-149">The virtual machine scale set node type should show the existing virtual network and subnet.</span></span> <span data-ttu-id="9a706-150">Você também pode usar o protocolo RDP para acessar a VM que já está na rede virtual e executar o ping nas VMs do novo conjunto de dimensionamento:</span><span class="sxs-lookup"><span data-stu-id="9a706-150">You also can use Remote Desktop Protocol (RDP) to access the VM that was already in the virtual network, and to ping the new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="9a706-151">Para obter outro exemplo, consulte [um que não seja específico para o Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="9a706-151">For another example, see [one that is not specific to Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="9a706-152">Endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="9a706-152">Static public IP address</span></span>

1. <span data-ttu-id="9a706-153">Adicione parâmetros para o grupo de recursos do IP estático existente, nome e FQDN (nome de domínio totalmente qualificado):</span><span class="sxs-lookup"><span data-stu-id="9a706-153">Add parameters for the name of the existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="9a706-154">Remova o parâmetro `dnsName`.</span><span class="sxs-lookup"><span data-stu-id="9a706-154">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="9a706-155">(O endereço IP estático já tem um.)</span><span class="sxs-lookup"><span data-stu-id="9a706-155">(The static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="9a706-156">Adicione uma variável para referenciar o endereço IP estático existente:</span><span class="sxs-lookup"><span data-stu-id="9a706-156">Add a variable to reference the existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="9a706-157">Remova `Microsoft.Network/publicIPAddresses` de seus recursos de modo que o Azure não crie um novo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="9a706-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="9a706-158">Comente o endereço IP com base no atributo `dependsOn` de `Microsoft.Network/loadBalancers`, de modo que você não dependa da criação de um novo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="9a706-158">Comment out the IP address from the `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="9a706-159">No recurso `Microsoft.Network/loadBalancers`, altere o elemento `publicIPAddress` de `frontendIPConfigurations` para referenciar o endereço IP estático existente em vez de um recém-criado:</span><span class="sxs-lookup"><span data-stu-id="9a706-159">In the `Microsoft.Network/loadBalancers` resource, change the `publicIPAddress` element of `frontendIPConfigurations` to reference the existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="9a706-160">No recurso `Microsoft.ServiceFabric/clusters`, altere `managementEndpoint` para o FQDN do DNS do endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="9a706-160">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to the DNS FQDN of the static IP address.</span></span> <span data-ttu-id="9a706-161">Se estiver usando um cluster seguro, lembre-se de alterar *http://* para *https://*.</span><span class="sxs-lookup"><span data-stu-id="9a706-161">If you are using a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="9a706-162">(Observe que essa etapa se aplica apenas aos clusters do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9a706-162">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="9a706-163">Se estiver usando um conjunto de dimensionamento de máquinas virtuais, ignore esta etapa.)</span><span class="sxs-lookup"><span data-stu-id="9a706-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="9a706-164">Implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="9a706-164">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="9a706-165">Após a implantação, você pode ver que o balanceador de carga está limitado ao endereço IP público estático do outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a706-165">After deployment, you can see that your load balancer is bound to the public static IP address from the other resource group.</span></span> <span data-ttu-id="9a706-166">O ponto de extremidade da conexão de cliente do Service Fabric e o ponto de extremidade do [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) apontam para o FQDN do DNS do endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="9a706-166">The Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point to the DNS FQDN of the static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="9a706-167">Balanceador de carga somente interno</span><span class="sxs-lookup"><span data-stu-id="9a706-167">Internal-only load balancer</span></span>

<span data-ttu-id="9a706-168">Este cenário substitui o balanceador externo de carga no modelo padrão do Service Fabric por um balanceador de carga somente interno.</span><span class="sxs-lookup"><span data-stu-id="9a706-168">This scenario replaces the external load balancer in the default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="9a706-169">Para obter implicações para o Portal do Azure e o provedor de recursos do Service Fabric, consulte a seção anterior.</span><span class="sxs-lookup"><span data-stu-id="9a706-169">For implications for the Azure portal and for the Service Fabric resource provider, see the preceding section.</span></span>

1. <span data-ttu-id="9a706-170">Remova o parâmetro `dnsName`.</span><span class="sxs-lookup"><span data-stu-id="9a706-170">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="9a706-171">(Ele não é necessário.)</span><span class="sxs-lookup"><span data-stu-id="9a706-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="9a706-172">Opcionalmente, você poderá adicionar um parâmetro de endereço IP estático se estiver usando o método de alocação estática.</span><span class="sxs-lookup"><span data-stu-id="9a706-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="9a706-173">Se você usar um método de alocação dinâmica, você não precisará realizar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="9a706-173">If you use a dynamic allocation method, you do not need to do this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="9a706-174">Remova `Microsoft.Network/publicIPAddresses` de seus recursos de modo que o Azure não crie um novo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="9a706-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="9a706-175">Remova o atributo `dependsOn` do endereço IP de `Microsoft.Network/loadBalancers`, de modo que você não dependa da criação de um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="9a706-175">Remove the IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="9a706-176">Adicione o atributo `dependsOn` de rede virtual porque o balanceador de carga agora depende da sub-rede da rede virtual:</span><span class="sxs-lookup"><span data-stu-id="9a706-176">Add the virtual network `dependsOn` attribute because the load balancer now depends on the subnet from the virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="9a706-177">Altere a configuração `frontendIPConfigurations` do balanceador de carga, anteriormente configurado para usar `publicIPAddress`, para que passe a usar uma sub-rede e `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="9a706-177">Change the load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, to using a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="9a706-178">`privateIPAddress` usa um endereço IP interno estático predefinido.</span><span class="sxs-lookup"><span data-stu-id="9a706-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="9a706-179">Para usar um endereço IP dinâmico, remova o elemento `privateIPAddress` e altere `privateIPAllocationMethod` para **Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="9a706-179">To use a dynamic IP address, remove the `privateIPAddress` element, and then change `privateIPAllocationMethod` to **Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="9a706-180">No recurso `Microsoft.ServiceFabric/clusters`, altere `managementEndpoint` para apontar para o endereço do balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9a706-180">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to point to the internal load balancer address.</span></span> <span data-ttu-id="9a706-181">Se estiver usando um cluster seguro, lembre-se de alterar *http://* para *https://*.</span><span class="sxs-lookup"><span data-stu-id="9a706-181">If you use a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="9a706-182">(Observe que essa etapa se aplica apenas aos clusters do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9a706-182">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="9a706-183">Se estiver usando um conjunto de dimensionamento de máquinas virtuais, ignore esta etapa.)</span><span class="sxs-lookup"><span data-stu-id="9a706-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="9a706-184">Implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="9a706-184">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="9a706-185">Após a implantação, o balanceador de carga usa o endereço IP estático privado 10.0.0.250.</span><span class="sxs-lookup"><span data-stu-id="9a706-185">After deployment, your load balancer uses the private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="9a706-186">Se você tiver outro computador na mesma rede virtual, você poderá ir para o ponto de extremidade interno do [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9a706-186">If you have another machine in that same virtual network, you can go to the internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="9a706-187">Observe que ele se conecta a um dos nós por trás do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="9a706-187">Note that it connects to one of the nodes behind the load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="9a706-188">Balanceador de carga interno e externo</span><span class="sxs-lookup"><span data-stu-id="9a706-188">Internal and external load balancer</span></span>

<span data-ttu-id="9a706-189">Neste cenário, você começa com o balanceador externo de carga de tipo de nó único existente e adiciona um balanceador de carga interno para o mesmo tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="9a706-189">In this scenario, you start with the existing single-node type external load balancer, and add an internal load balancer for the same node type.</span></span> <span data-ttu-id="9a706-190">Uma porta de back-end anexada ao pool de endereços de back-end pode ser atribuída somente a um único balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="9a706-190">A back-end port attached to a back-end address pool can be assigned only to a single load balancer.</span></span> <span data-ttu-id="9a706-191">Escolha qual balanceador de carga terá as suas portas do aplicativo e o balanceador de carga terá seus pontos de extremidade de gerenciamento (portas 19000 e 19080).</span><span class="sxs-lookup"><span data-stu-id="9a706-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="9a706-192">Se você colocar os pontos de extremidade de gerenciamento no balanceador de carga interno, lembre-se das restrições do provedor de recursos do Service Fabric discutidas anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9a706-192">If you put the management endpoints on the internal load balancer, keep in mind the Service Fabric resource provider restrictions discussed earlier in the article.</span></span> <span data-ttu-id="9a706-193">No exemplo que usamos, os pontos de extremidade de gerenciamento permanecem no balanceador externo de carga.</span><span class="sxs-lookup"><span data-stu-id="9a706-193">In the example we use, the management endpoints remain on the external load balancer.</span></span> <span data-ttu-id="9a706-194">Você também pode adicionar uma porta 80 do aplicativo e colocá-la no balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9a706-194">You also add a port 80 application port, and place it on the internal load balancer.</span></span>

<span data-ttu-id="9a706-195">Em um cluster com dois tipos de nós, um tipo de nó é no balanceador externo de carga.</span><span class="sxs-lookup"><span data-stu-id="9a706-195">In a two-node-type cluster, one node type is on the external load balancer.</span></span> <span data-ttu-id="9a706-196">O outro tipo de nó é no balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9a706-196">The other node type is on the internal load balancer.</span></span> <span data-ttu-id="9a706-197">Para usar um cluster com dois tipos de nós, no modelo com dois tipos de nós criado pelo portal (que vem com dois balanceadores de carga), mude o segundo balanceador de carga para um balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9a706-197">To use a two-node-type cluster, in the portal-created two-node-type template (which comes with two load balancers), switch the second load balancer to an internal load balancer.</span></span> <span data-ttu-id="9a706-198">Para obter mais informações, consulte a seção [Balanceador de carga somente interno](#internallb).</span><span class="sxs-lookup"><span data-stu-id="9a706-198">For more information, see the [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="9a706-199">Adicione o parâmetro do endereço IP de balanceador de carga interno estático.</span><span class="sxs-lookup"><span data-stu-id="9a706-199">Add the static internal load balancer IP address parameter.</span></span> <span data-ttu-id="9a706-200">(Para obter notas relacionadas ao uso de um endereço IP dinâmico, consulte as seções anteriores deste artigo.)</span><span class="sxs-lookup"><span data-stu-id="9a706-200">(For notes related to using a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="9a706-201">Adicione um parâmetro de porta 80 do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9a706-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="9a706-202">Para adicionar versões internas das variáveis de rede existentes, copie e cole-as, adicionando “-Int” ao nome:</span><span class="sxs-lookup"><span data-stu-id="9a706-202">To add internal versions of the existing networking variables, copy and paste them, and add "-Int" to the name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="9a706-203">Se você começar com o modelo gerado pelo portal que usa a porta 80 do aplicativo, o modelo padrão do portal adicionará AppPort1 (porta 80) ao balanceador externo de carga.</span><span class="sxs-lookup"><span data-stu-id="9a706-203">If you start with the portal-generated template that uses application port 80, the default portal template adds AppPort1 (port 80) on the external load balancer.</span></span> <span data-ttu-id="9a706-204">Nesse caso, remova AppPort1 do balanceador externo de carga `loadBalancingRules` e das investigações, para que seja possível adicioná-la ao balanceador interno de carga:</span><span class="sxs-lookup"><span data-stu-id="9a706-204">In this case, remove AppPort1 from the external load balancer `loadBalancingRules` and probes, so you can add it to the internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from the external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from the external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="9a706-205">Adicione um segundo recurso `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="9a706-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="9a706-206">Ele tem aparência similar à do balanceador de carga interno criado na seção [Balanceador de carga somente interno](#internallb), mas usa as variáveis de balanceador de carga "-Int" e implementa apenas a porta 80 do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9a706-206">It looks similar to the internal load balancer created in the [Internal-only load balancer](#internallb) section, but it uses the "-Int" load balancer variables, and implements only the application port 80.</span></span> <span data-ttu-id="9a706-207">Isso também remove `inboundNatPools` para manter os pontos de extremidade de RDP no balanceador de carga público.</span><span class="sxs-lookup"><span data-stu-id="9a706-207">This also removes `inboundNatPools`, to keep RDP endpoints on the public load balancer.</span></span> <span data-ttu-id="9a706-208">Se você desejar RDP no balanceador interno de carga, mova `inboundNatPools` do balanceador externo de carga para este balanceador interno de carga:</span><span class="sxs-lookup"><span data-stu-id="9a706-208">If you want RDP on the internal load balancer, move `inboundNatPools` from the external load balancer to this internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and the "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" to the name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public to Private IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add the AppPort rule. Be sure to reference the "-Int" versions of backendAddressPool, frontendIPConfiguration, and the probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add the probe for the app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="9a706-209">Em `networkProfile` para o recurso `Microsoft.Compute/virtualMachineScaleSets`, adicione o pool de endereços de back-end interno:</span><span class="sxs-lookup"><span data-stu-id="9a706-209">In `networkProfile` for the `Microsoft.Compute/virtualMachineScaleSets` resource, add the internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="9a706-210">Implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="9a706-210">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="9a706-211">Após a implantação, você poderá ver dois balanceadores de carga no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9a706-211">After deployment, you can see two load balancers in the resource group.</span></span> <span data-ttu-id="9a706-212">Se você procurar os balanceadores de carga, você poderá ver os endereços IP públicos e pontos de extremidade de gerenciamento (portas 19000 e 19080) atribuídos ao endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="9a706-212">If you browse the load balancers, you can see the public IP address and management endpoints (ports 19000 and 19080) assigned to the public IP address.</span></span> <span data-ttu-id="9a706-213">Você também poderá ver o endereço IP interno estático e o ponto de extremidade do aplicativo (porta 80) atribuído ao balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9a706-213">You also can see the static internal IP address and application endpoint (port 80) assigned to the internal load balancer.</span></span> <span data-ttu-id="9a706-214">Ambos os balanceadores de carga usam o mesmo pool de back-end de conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9a706-214">Both load balancers use the same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a706-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a706-215">Next steps</span></span>
[<span data-ttu-id="9a706-216">Criar um cluster</span><span class="sxs-lookup"><span data-stu-id="9a706-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
