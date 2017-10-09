---
title: "padrões de aaaNetworking para o Azure Service Fabric | Microsoft Docs"
description: "Descreve os padrões comuns de rede de malha do serviço e como toocreate um cluster usando os recursos de rede do Azure."
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
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="16b32-103">Padrões de rede do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="16b32-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="16b32-104">Você pode integrar seu cluster do Azure Service Fabric a outros recursos de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="16b32-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="16b32-105">Neste artigo, mostramos como toocreate clusters que Olá use recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="16b32-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="16b32-106">Rede virtual ou sub-rede existente</span><span class="sxs-lookup"><span data-stu-id="16b32-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="16b32-107">Endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="16b32-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="16b32-108">Balanceador de carga somente interno</span><span class="sxs-lookup"><span data-stu-id="16b32-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="16b32-109">Balanceador interno e externo de carga</span><span class="sxs-lookup"><span data-stu-id="16b32-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="16b32-110">O Service Fabric é executado em um conjunto de dimensionamento de máquinas virtuais padrão.</span><span class="sxs-lookup"><span data-stu-id="16b32-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="16b32-111">Qualquer funcionalidade que você pode usar em um conjunto de dimensionamento de máquinas virtuais você pode usar também com um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16b32-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="16b32-112">seções de rede Olá dos modelos do Azure Resource Manager Olá para conjuntos de escala de máquina virtual e serviço de malha são idênticas.</span><span class="sxs-lookup"><span data-stu-id="16b32-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="16b32-113">Depois de implantar tooan existentes de rede virtual, é fácil tooincorporate outros recursos, como a rota expressa do Azure, o Gateway de VPN do Azure, um grupo de segurança de rede e o emparelhamento de rede virtual do sistema de rede.</span><span class="sxs-lookup"><span data-stu-id="16b32-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="16b32-114">O Service Fabric é único entre outros recursos de rede em um aspecto.</span><span class="sxs-lookup"><span data-stu-id="16b32-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="16b32-115">Olá [portal do Azure](https://portal.azure.com) internamente usa Olá Service Fabric recurso provedor toocall tooa cluster tooget informações sobre nós e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="16b32-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="16b32-116">provedor de recursos de malha do serviço Olá requer acesso de entrada publicamente acessível toohello HTTP gateway porta (19080, por padrão) no ponto de extremidade de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="16b32-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="16b32-117">[Gerenciador do Service Fabric](service-fabric-visualizing-your-cluster.md) usa Olá toomanage de ponto de extremidade de gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="16b32-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="16b32-118">provedor de recursos de malha do serviço Olá também usa essas informações de tooquery de porta sobre o cluster, toodisplay em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="16b32-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="16b32-119">Se a porta 19080 não é acessível pelo provedor de recursos de malha do serviço hello, uma mensagem como *nós não encontrado* aparece no portal do hello, e sua lista de nó e o aplicativo estiver vazia.</span><span class="sxs-lookup"><span data-stu-id="16b32-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="16b32-120">Se você quiser toosee seu cluster em Olá portal do Azure, o balanceador de carga deve expor um endereço IP público e seu grupo de segurança de rede deve permitir o tráfego da porta 19080.</span><span class="sxs-lookup"><span data-stu-id="16b32-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="16b32-121">Se a configuração não atender a esses requisitos, Olá portal do Azure não exibir o status de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="16b32-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="16b32-122">Modelos</span><span class="sxs-lookup"><span data-stu-id="16b32-122">Templates</span></span>

<span data-ttu-id="16b32-123">Todos os modelos do Service Fabric estão em [um arquivo de download](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="16b32-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="16b32-124">Você deve ser capaz de toodeploy modelos hello como-usando Olá comandos do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="16b32-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="16b32-125">Se você estiver implantando Olá modelo de rede Virtual do Azure existente ou Olá estático público modelo de IP, leia primeiro a saudação [inicial instalação](#initialsetup) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="16b32-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="16b32-126">Configuração inicial</span><span class="sxs-lookup"><span data-stu-id="16b32-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="16b32-127">Rede virtual existente</span><span class="sxs-lookup"><span data-stu-id="16b32-127">Existing virtual network</span></span>

<span data-ttu-id="16b32-128">Olá exemplo a seguir, vamos começar com uma rede virtual existente chamada ExistingRG-vnet no hello **ExistingRG** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="16b32-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="16b32-129">subrede Olá é denominado default.</span><span class="sxs-lookup"><span data-stu-id="16b32-129">hello subnet is named default.</span></span> <span data-ttu-id="16b32-130">Esses recursos padrão são criados quando você usar Olá toocreate portal do Azure uma máquina de virtual (VM) padrão.</span><span class="sxs-lookup"><span data-stu-id="16b32-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="16b32-131">Você pode criar uma rede virtual hello e sub-rede sem criar hello VM, mas Olá principal objetivo de adicionar uma rede de virtual cluster tooan existente é tooother de conectividade de rede tooprovide VMs.</span><span class="sxs-lookup"><span data-stu-id="16b32-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="16b32-132">Olá criar VM fornece um bom exemplo de como uma rede virtual existente normalmente é usada.</span><span class="sxs-lookup"><span data-stu-id="16b32-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="16b32-133">Se o cluster do Service Fabric usa apenas um balanceador de carga interno, sem um endereço IP público, você pode usar Olá VM e seu IP público como seguro *saltar caixa*.</span><span class="sxs-lookup"><span data-stu-id="16b32-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="16b32-134">Endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="16b32-134">Static public IP address</span></span>

<span data-ttu-id="16b32-135">Um endereço IP público estático geralmente é um recurso dedicado gerenciado separadamente do hello VM ou VMs que ele está atribuído.</span><span class="sxs-lookup"><span data-stu-id="16b32-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="16b32-136">Ela é provisionada em um grupo de recursos de rede dedicado (como tooin contrário Olá Service Fabric grupo de recursos em si).</span><span class="sxs-lookup"><span data-stu-id="16b32-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="16b32-137">Criar um endereço IP público estático chamado staticIP1 em Olá mesmo grupo de recursos de ExistingRG, no portal do Azure de saudação ou usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="16b32-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

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

### <a name="service-fabric-template"></a><span data-ttu-id="16b32-138">Modelo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="16b32-138">Service Fabric template</span></span>

<span data-ttu-id="16b32-139">Exemplos de saudação neste artigo, usamos Olá Service Fabric template.json.</span><span class="sxs-lookup"><span data-stu-id="16b32-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="16b32-140">Você pode usar o modelo de Olá de toodownload de assistente padrão do portal de saudação do portal de saudação antes de criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="16b32-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="16b32-141">Você também pode usar um dos modelos de saudação em Olá [Galeria de modelos de](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), como Olá [cluster do Service Fabric de cinco nós](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="16b32-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="16b32-142">Rede virtual ou sub-rede existente</span><span class="sxs-lookup"><span data-stu-id="16b32-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="16b32-143">Alterar nome de toohello de parâmetro hello sub-rede da sub-rede existente hello e, em seguida, adicione dois novos parâmetros tooreference Olá rede virtual existente:</span><span class="sxs-lookup"><span data-stu-id="16b32-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

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


2. <span data-ttu-id="16b32-144">Saudação de alteração `vnetID` toopoint variável toohello rede virtual existente:</span><span class="sxs-lookup"><span data-stu-id="16b32-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="16b32-145">Remova `Microsoft.Network/virtualNetworks` de seus recursos de modo que o Azure não crie uma nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="16b32-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

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

4. <span data-ttu-id="16b32-146">Comente a rede virtual de saudação da saudação `dependsOn` atributo de `Microsoft.Compute/virtualMachineScaleSets`, portanto, não dependem criando uma nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="16b32-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

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

5. <span data-ttu-id="16b32-147">Implante o modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="16b32-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="16b32-148">Após a implantação, sua rede virtual deve incluir as VMs de conjunto de escala de novo hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="16b32-149">tipo de nó de conjunto de escala do Hello máquina virtual deve mostrar a sub-rede e a rede virtual existente do hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="16b32-150">Você também pode usar protocolo de área de trabalho remota (RDP) tooaccess Olá VM que já estava na rede virtual hello e tooping Olá nova escala definida como VMs:</span><span class="sxs-lookup"><span data-stu-id="16b32-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="16b32-151">Outro exemplo, consulte [que não é específico tooService malha](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="16b32-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="16b32-152">Endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="16b32-152">Static public IP address</span></span>

1. <span data-ttu-id="16b32-153">Adicione parâmetros de nome de saudação do hello existentes do grupo de recursos IP estático, o nome e o nome de domínio totalmente qualificado (FQDN):</span><span class="sxs-lookup"><span data-stu-id="16b32-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

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

2. <span data-ttu-id="16b32-154">Remover Olá `dnsName` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="16b32-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="16b32-155">(endereço IP estático de saudação já tem um.)</span><span class="sxs-lookup"><span data-stu-id="16b32-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="16b32-156">Adicione um variável tooreference Olá endereço IP estático existente:</span><span class="sxs-lookup"><span data-stu-id="16b32-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="16b32-157">Remova `Microsoft.Network/publicIPAddresses` de seus recursos de modo que o Azure não crie um novo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="16b32-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

5. <span data-ttu-id="16b32-158">Comente o endereço IP de saudação do hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, portanto, você não depende de criar um novo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="16b32-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

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

6. <span data-ttu-id="16b32-159">Em hello `Microsoft.Network/loadBalancers` recurso, alteração Olá `publicIPAddress` elemento `frontendIPConfigurations` tooreference Olá endereço IP estático existente em vez de um criado recentemente:</span><span class="sxs-lookup"><span data-stu-id="16b32-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

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

7. <span data-ttu-id="16b32-160">Em Olá `Microsoft.ServiceFabric/clusters` recursos, alteração `managementEndpoint` toohello FQDN do DNS do endereço IP estático de saudação.</span><span class="sxs-lookup"><span data-stu-id="16b32-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="16b32-161">Se você estiver usando um cluster seguro, certifique-se de alterar *http://* muito*https://*.</span><span class="sxs-lookup"><span data-stu-id="16b32-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="16b32-162">(Observe que essa etapa se aplica somente os clusters de malha tooService.</span><span class="sxs-lookup"><span data-stu-id="16b32-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="16b32-163">Se estiver usando um conjunto de dimensionamento de máquinas virtuais, ignore esta etapa.)</span><span class="sxs-lookup"><span data-stu-id="16b32-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="16b32-164">Implante o modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="16b32-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="16b32-165">Após a implantação, você pode ver que o balanceador de carga é toohello associada público endereço IP estático de saudação outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="16b32-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="16b32-166">Olá ponto de extremidade de conexão de cliente do Service Fabric e [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello de ponto de extremidade FQDN do DNS do endereço IP estático de saudação.</span><span class="sxs-lookup"><span data-stu-id="16b32-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="16b32-167">Balanceador de carga somente interno</span><span class="sxs-lookup"><span data-stu-id="16b32-167">Internal-only load balancer</span></span>

<span data-ttu-id="16b32-168">Este cenário substitui Olá balanceador externo de carga no modelo de serviço malha saudação padrão com um balanceador de carga interno somente.</span><span class="sxs-lookup"><span data-stu-id="16b32-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="16b32-169">Para implicações para Olá portal do Azure e para o provedor de recursos de malha do serviço Olá, consulte Olá anterior de seção.</span><span class="sxs-lookup"><span data-stu-id="16b32-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="16b32-170">Remover Olá `dnsName` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="16b32-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="16b32-171">(Ele não é necessário.)</span><span class="sxs-lookup"><span data-stu-id="16b32-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="16b32-172">Opcionalmente, você poderá adicionar um parâmetro de endereço IP estático se estiver usando o método de alocação estática.</span><span class="sxs-lookup"><span data-stu-id="16b32-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="16b32-173">Se você usar um método de alocação dinâmica, você não precisará toodo desta etapa.</span><span class="sxs-lookup"><span data-stu-id="16b32-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="16b32-174">Remova `Microsoft.Network/publicIPAddresses` de seus recursos de modo que o Azure não crie um novo endereço IP:</span><span class="sxs-lookup"><span data-stu-id="16b32-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

4. <span data-ttu-id="16b32-175">Remova o endereço IP hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, portanto, você não depende de criar um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="16b32-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="16b32-176">Adicionar a rede virtual Olá `dependsOn` atributo porque balanceador de carga Olá agora depende de subrede da rede virtual Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="16b32-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

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

5. <span data-ttu-id="16b32-177">Alterar do balanceador de carga Olá `frontendIPConfigurations` configuração que usa um `publicIPAddress`, toousing uma sub-rede e `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="16b32-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="16b32-178">`privateIPAddress` usa um endereço IP interno estático predefinido.</span><span class="sxs-lookup"><span data-stu-id="16b32-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="16b32-179">toouse um endereço IP dinâmico, remover Olá `privateIPAddress` elemento e altere `privateIPAllocationMethod` muito**dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="16b32-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

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

6. <span data-ttu-id="16b32-180">Em Olá `Microsoft.ServiceFabric/clusters` recursos, alteração `managementEndpoint` endereço de Balanceador de carga interno toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="16b32-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="16b32-181">Se você usar um cluster seguro, certifique-se de alterar *http://* muito*https://*.</span><span class="sxs-lookup"><span data-stu-id="16b32-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="16b32-182">(Observe que essa etapa se aplica somente os clusters de malha tooService.</span><span class="sxs-lookup"><span data-stu-id="16b32-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="16b32-183">Se estiver usando um conjunto de dimensionamento de máquinas virtuais, ignore esta etapa.)</span><span class="sxs-lookup"><span data-stu-id="16b32-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="16b32-184">Implante o modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="16b32-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="16b32-185">Após a implantação, o balanceador de carga usa endereço IP de saudação privada 10.0.0.250 estático.</span><span class="sxs-lookup"><span data-stu-id="16b32-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="16b32-186">Se você tiver outro computador na mesma rede virtual, você pode ir toohello interno [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="16b32-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="16b32-187">Observe que se conecta tooone de nós de saudação por trás do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="16b32-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="16b32-188">Balanceador de carga interno e externo</span><span class="sxs-lookup"><span data-stu-id="16b32-188">Internal and external load balancer</span></span>

<span data-ttu-id="16b32-189">Nesse cenário, você começar com balanceador de carga externo de tipo de nó único existente hello e adicionar um balanceador de carga interno para Olá mesmo tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="16b32-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="16b32-190">Balanceador de carga único tooa só pode ser atribuído a um pool de endereços de back-end de tooa de porta de back-end conectado.</span><span class="sxs-lookup"><span data-stu-id="16b32-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="16b32-191">Escolha qual balanceador de carga terá as suas portas do aplicativo e o balanceador de carga terá seus pontos de extremidade de gerenciamento (portas 19000 e 19080).</span><span class="sxs-lookup"><span data-stu-id="16b32-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="16b32-192">Se você colocar pontos de extremidade de gerenciamento Olá no balanceador de carga interno hello, lembre-Olá mente recursos de malha do serviço discutidas anteriormente no artigo de saudação de restrições de provedor.</span><span class="sxs-lookup"><span data-stu-id="16b32-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="16b32-193">O exemplo hello que usamos, pontos de extremidade de gerenciamento Olá permanecem em Olá balanceador externo de carga.</span><span class="sxs-lookup"><span data-stu-id="16b32-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="16b32-194">Você também adicionar uma porta de aplicativo 80 e colocá-lo no balanceador de carga interno hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="16b32-195">Em um cluster de dois tipo de nó, um tipo de nó é no balanceador de carga externo hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="16b32-196">Olá outro tipo de nó é no balanceador de carga interno hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="16b32-197">toouse um cluster de dois tipo de nó, Olá portal dois tipo de nó modelo criado (o que vem com dois balanceadores de carga), comutador hello segundo carga balanceador tooan balanceador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="16b32-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="16b32-198">Para obter mais informações, consulte Olá [balanceador de carga interno somente](#internallb) seção.</span><span class="sxs-lookup"><span data-stu-id="16b32-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="16b32-199">Adicione o parâmetro do endereço IP estático de carga interno balanceador da saudação.</span><span class="sxs-lookup"><span data-stu-id="16b32-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="16b32-200">(Para anotações relacionadas toousing um endereço IP dinâmico, consulte as seções anteriores deste artigo).</span><span class="sxs-lookup"><span data-stu-id="16b32-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="16b32-201">Adicione um parâmetro de porta 80 do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16b32-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="16b32-202">versões interno tooadd Olá existente rede variáveis, copie e cole-os e adicionar "-Int" toohello nome:</span><span class="sxs-lookup"><span data-stu-id="16b32-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

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

4. <span data-ttu-id="16b32-203">Se você iniciar com o modelo gerado pelo portal Olá que usa a porta 80 do aplicativo, o modelo de portal saudação padrão adiciona AppPort1 (porta 80) no balanceador de carga externo hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="16b32-204">Nesse caso, remova AppPort1 balanceador externo de saudação `loadBalancingRules` e testes, para que você possa adicionar balanceador de carga interno toohello:</span><span class="sxs-lookup"><span data-stu-id="16b32-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

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
        } /* Remove AppPort1 from hello external load balancer.
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
        } /* Remove AppPort1 from hello external load balancer.
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

5. <span data-ttu-id="16b32-205">Adicione um segundo recurso `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="16b32-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="16b32-206">Parece semelhante balanceador de carga interno toohello criado no hello [balanceador de carga interno somente](#internallb) seção, mas usa hello "-Int" carregar balanceador variáveis e implementa somente Olá aplicativo porta 80.</span><span class="sxs-lookup"><span data-stu-id="16b32-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="16b32-207">Isso também remove `inboundNatPools`, tookeep pontos de extremidade RDP no balanceador de carga público hello.</span><span class="sxs-lookup"><span data-stu-id="16b32-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="16b32-208">Se você quiser RDP no balanceador de carga interno hello, mover `inboundNatPools` de toothis de Balanceador de carga externo de saudação interno balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="16b32-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
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
                                /* Switch from Public tooPrivate IP address
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
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
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
                    /* Add hello probe for hello app port. */
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

6. <span data-ttu-id="16b32-209">Em `networkProfile` para Olá `Microsoft.Compute/virtualMachineScaleSets` recursos, adicionar pool de endereços de back-end interno de saudação:</span><span class="sxs-lookup"><span data-stu-id="16b32-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

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

7. <span data-ttu-id="16b32-210">Implante o modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="16b32-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="16b32-211">Após a implantação, você pode ver dois balanceadores de carga no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="16b32-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="16b32-212">Se você procurar balanceadores de carga hello, você pode ver o endereço IP público de saudação e pontos de extremidade (portas 19000 e 19080) atribuídos toohello público endereço IP de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="16b32-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="16b32-213">Você também pode ver Olá estático interno IP endereço e o aplicativo de ponto de extremidade (porta 80) atribuído toohello interno balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="16b32-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="16b32-214">Uso de balanceadores de carga mesma escala de máquina virtual hello definir pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="16b32-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16b32-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16b32-215">Next steps</span></span>
[<span data-ttu-id="16b32-216">Criar um cluster</span><span class="sxs-lookup"><span data-stu-id="16b32-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
