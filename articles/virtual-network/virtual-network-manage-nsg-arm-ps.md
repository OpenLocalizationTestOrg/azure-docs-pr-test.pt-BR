---
title: "aaaManage rede grupos de segurança - Azure PowerShell | Microsoft Docs"
description: "Saiba como toomanage rede grupos de segurança usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="5ee6d-103">Gerenciar grupos de segurança usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ee6d-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5ee6d-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5ee6d-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5ee6d-105">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="5ee6d-106">Recuperar informações</span><span class="sxs-lookup"><span data-stu-id="5ee6d-106">Retrieve Information</span></span>
<span data-ttu-id="5ee6d-107">Você pode exibir seus NSGs existentes, recuperar regras para um NSG existente e descobrir a quais recursos um NSG está associado.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="5ee6d-108">Exibir NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="5ee6d-108">View existing NSGs</span></span>
<span data-ttu-id="5ee6d-109">tooview todos os NSGs existentes em uma assinatura, execute Olá `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="5ee6d-110">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="5ee6d-111">lista de saudação do tooview de NSGs em um grupo de recursos específico, execute Olá `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="5ee6d-112">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="5ee6d-113">Listar todas as regras de um NSG</span><span class="sxs-lookup"><span data-stu-id="5ee6d-113">List all rules for an NSG</span></span>
<span data-ttu-id="5ee6d-114">regras de saudação tooview de um NSG denominado **NSG-front-end**, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="5ee6d-115">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="5ee6d-116">Você também pode usar `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` regras de padrão de saudação toolist de saudação **NSG-front-end** NSG.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="5ee6d-117">Exibir associações de NSGs</span><span class="sxs-lookup"><span data-stu-id="5ee6d-117">View NSGs associations</span></span>
<span data-ttu-id="5ee6d-118">tooview Olá quais recursos **NSG-front-end** NSG está associado ao, execute hello seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="5ee6d-119">Procure Olá **NetworkInterfaces** e **sub-redes** propriedades conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="5ee6d-120">No exemplo anterior de saudação, Olá NSG não está associado tooany interfaces de rede (NICs). é a sub-rede associada tooa denominada **front-end**.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="5ee6d-121">Gerenciar regras</span><span class="sxs-lookup"><span data-stu-id="5ee6d-121">Manage rules</span></span>
<span data-ttu-id="5ee6d-122">Você pode adicionar regras tooan existente NSG, editar regras existentes e remova regras.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="5ee6d-123">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="5ee6d-123">Add a rule</span></span>
<span data-ttu-id="5ee6d-124">tooadd uma regra permitindo **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="5ee6d-125">Execute Olá Olá do comando tooretrieve existente NSG a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="5ee6d-126">Execute toohello uma regra NSG de Olá tooadd de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="5ee6d-127">alterações de saudação do toosave feitas toohello NSG, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="5ee6d-128">Saída esperada mostrando Olá somente as regras de segurança:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="5ee6d-129">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="5ee6d-129">Change a rule</span></span>
<span data-ttu-id="5ee6d-130">regra de saudação toochange criada acima tooallow Olá o tráfego de entrada **Internet** apenas, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="5ee6d-131">Execute Olá Olá do comando tooretrieve existente NSG a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="5ee6d-132">Execute Olá comando com novas configurações de regra Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="5ee6d-133">alterações de saudação do toosave feitas toohello NSG, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="5ee6d-134">Saída esperada mostrando Olá somente as regras de segurança:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="5ee6d-135">Excluir uma regra</span><span class="sxs-lookup"><span data-stu-id="5ee6d-135">Delete a rule</span></span>
1. <span data-ttu-id="5ee6d-136">Execute Olá Olá do comando tooretrieve existente NSG a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="5ee6d-137">Saudação de execução a seguir de regra do comando tooremove Olá Olá NSG:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="5ee6d-138">Salve as alterações feitas de saudação toohello NSG, executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="5ee6d-139">Saída esperada mostrando Olá apenas regras de segurança, observe Olá **regra https** não está mais listado:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="5ee6d-140">Gerenciar associações</span><span class="sxs-lookup"><span data-stu-id="5ee6d-140">Manage associations</span></span>
<span data-ttu-id="5ee6d-141">Você pode associar um NSG toosubnets e placas de rede.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="5ee6d-142">Você também pode desassociar um NSG de qualquer recurso ao qual ele esteja associado.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="5ee6d-143">Associar um NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="5ee6d-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="5ee6d-144">Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="5ee6d-145">Execute Olá Olá do comando tooretrieve existente NSG a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="5ee6d-146">Execute Olá Olá do comando tooretrieve existente NIC a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="5ee6d-147">Olá conjunto **NetworkSecurityGroup** propriedade Olá **NIC** valor variável toohello Olá **NSG** variável, digitando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="5ee6d-148">alterações de saudação do toosave feitas toohello NIC, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="5ee6d-149">Olá somente do resultado esperado mostrando **NetworkSecurityGroup** propriedade:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="5ee6d-150">Desassociar um NSG de uma NIC</span><span class="sxs-lookup"><span data-stu-id="5ee6d-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="5ee6d-151">Olá toodissociate **NSG-front-end** NSG de saudação **TestNICWeb1** NIC, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="5ee6d-152">Execute Olá Olá do comando tooretrieve existente NIC a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="5ee6d-153">Saudação de conjunto **NetworkSecurityGroup** propriedade Olá **NIC** variável muito**$null** executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="5ee6d-154">alterações de saudação do toosave feitas toohello NIC, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="5ee6d-155">Olá somente do resultado esperado mostrando **NetworkSecurityGroup** propriedade:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="5ee6d-156">Desassociar um NSG de uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="5ee6d-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="5ee6d-157">Olá toodissociate **NSG-front-end** NSG de saudação **front-end** sub-rede, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="5ee6d-158">Execute Olá Olá do comando tooretrieve existente redes a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="5ee6d-159">Execução hello seguintes comando tooretrieve Olá **front-end** sub-rede e armazená-la em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="5ee6d-160">Saudação de conjunto **NetworkSecurityGroup** propriedade Olá **sub-rede** variável muito**$null** inserindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="5ee6d-161">toosave Olá alterações toohello sub-rede, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="5ee6d-162">Saída esperada, mostrando apenas as propriedades de saudação do hello **front-end** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="5ee6d-163">Observe que não existe uma propriedade para **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="5ee6d-164">Associar uma sub-rede de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="5ee6d-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="5ee6d-165">Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="5ee6d-166">Execute Olá Olá do comando tooretrieve existente redes a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="5ee6d-167">Execução hello seguintes comando tooretrieve Olá **front-end** sub-rede e armazená-la em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="5ee6d-168">Execute Olá Olá do comando tooretrieve existente NSG a seguir e armazená-lo em uma variável:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="5ee6d-169">Olá conjunto **NetworkSecurityGroup** propriedade da saudação **sub-rede** variável muito**$null** executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="5ee6d-170">toosave Olá alterações toohello sub-rede, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="5ee6d-171">Olá somente do resultado esperado mostrando **NetworkSecurityGroup** propriedade Olá **front-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="5ee6d-172">Excluir um NSG</span><span class="sxs-lookup"><span data-stu-id="5ee6d-172">Delete an NSG</span></span>
<span data-ttu-id="5ee6d-173">Você só pode excluir um NSG se ela não está associada tooany recursos.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="5ee6d-174">toodelete um NSG, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="5ee6d-175">recursos de saudação toocheck associado tooan NSG, execute Olá `azure network nsg show` conforme mostrado na [NSGs exibir associações](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="5ee6d-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="5ee6d-176">Se Olá NSG é associado tooany NICs, execute Olá `azure network nic set` conforme mostrado na [dissociar um NSG de uma NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="5ee6d-177">Se Olá NSG sub-rede associada tooany, execute Olá `azure network vnet subnet set` conforme mostrado na [dissociar um NSG de uma sub-rede](#Dissociate-an-NSG-from-a-subnet) para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="5ee6d-178">Olá toodelete NSG, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ee6d-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="5ee6d-179">Olá `-Force` parâmetro garante a exclusão de saudação tooconfirm não é necessário.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="5ee6d-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ee6d-180">Next steps</span></span>
* <span data-ttu-id="5ee6d-181">[Habilitar registro em log](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="5ee6d-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

