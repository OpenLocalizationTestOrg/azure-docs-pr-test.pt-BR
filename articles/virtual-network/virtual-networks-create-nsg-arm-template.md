---
title: "aaaCreate rede grupos de segurança - modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Saiba como toocreate e implantar grupos de segurança de rede usando um modelo do Gerenciador de recursos do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="2eb7d-103">Criar grupos de segurança de rede usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2eb7d-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="2eb7d-104">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="2eb7d-105">Você também pode [criar NSGs no modelo de implantação clássico Olá](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2eb7d-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="2eb7d-106">Recursos NSG em um arquivo de modelo</span><span class="sxs-lookup"><span data-stu-id="2eb7d-106">NSG resources in a template file</span></span>
<span data-ttu-id="2eb7d-107">Você pode exibir e baixar Olá [modelo](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="2eb7d-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="2eb7d-108">Olá, seção a seguir mostra a definição de saudação de saudação NSG front-end, com base no cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
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
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="2eb7d-109">tooassociate Olá NSG toohello front-end subrede, você tem a definição de subrede Olá toochange no modelo hello e use Olá id de referência Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="2eb7d-110">Observe Olá mesmo sendo feita para Olá back-end NSG e hello sub-rede back-end no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="2eb7d-111">Implantar o modelo do ARM hello usando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="2eb7d-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="2eb7d-112">Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="2eb7d-113">toodeploy usando esse modelo clique toodeploy, execute [este link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), clique em **implantar tooAzure**, substitua os valores de parâmetro de padrão de saudação se necessário e siga as instruções de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="2eb7d-114">Implantar o modelo do ARM hello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2eb7d-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="2eb7d-115">modelo do ARM Olá toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="2eb7d-116">Se você nunca tiver usado o PowerShell do Azure, siga as instruções de Olá Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall e configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="2eb7d-117">Executar Olá  **`New-AzureRmResourceGroup`**  toocreate cmdlet um grupo de recursos usando Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="2eb7d-118">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="2eb7d-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="2eb7d-119">Implantar o modelo do ARM hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2eb7d-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="2eb7d-120">modelo do ARM Olá toodeploy usando Olá CLI do Azure, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="2eb7d-121">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="2eb7d-122">Executar Olá  **`azure config mode`**  modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="2eb7d-123">seguinte Olá é saída de hello esperado para o comando hello:</span><span class="sxs-lookup"><span data-stu-id="2eb7d-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="2eb7d-124">Executar Olá  **`azure group deployment create`**  cmdlet toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="2eb7d-125">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="2eb7d-126">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="2eb7d-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="2eb7d-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-127">**-n (or --name)**.</span></span> <span data-ttu-id="2eb7d-128">Nome da saudação toobe de grupo de recursos criado.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="2eb7d-129">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-129">**-l (or --location)**.</span></span> <span data-ttu-id="2eb7d-130">Região do Azure onde o grupo de recursos Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="2eb7d-131">**-f (ou --arquivo de modelo)**.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="2eb7d-132">Arquivo de modelo do caminho tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="2eb7d-133">**-e (ou --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="2eb7d-134">Arquivo de parâmetros do caminho tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="2eb7d-134">Path tooyour ARM parameters file.</span></span>

