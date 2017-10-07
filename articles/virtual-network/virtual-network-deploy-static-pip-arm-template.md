---
title: "aaaCreate uma VM com um endereço IP público estático - modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com um endereço IP público estático endereço usando um modelo do Gerenciador de recursos do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="4d970-103">Criar uma VM com um endereço IP público estático usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4d970-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d970-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4d970-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="4d970-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d970-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="4d970-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4d970-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="4d970-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="4d970-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="4d970-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="4d970-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="4d970-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4d970-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4d970-110">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="4d970-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="4d970-111">Recursos de endereço IP público em um arquivo de modelo</span><span class="sxs-lookup"><span data-stu-id="4d970-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="4d970-112">Você pode exibir e baixar Olá [modelo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="4d970-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="4d970-113">Olá, seção a seguir mostra a definição de saudação do recurso IP público de hello, com base no cenário de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="4d970-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="4d970-114">Saudação de aviso **publicIPAllocationMethod** propriedade, que está definida muito*estático*.</span><span class="sxs-lookup"><span data-stu-id="4d970-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="4d970-115">Essa propriedade pode ser *Dinâmica* (valor padrão) ou *Estática*.</span><span class="sxs-lookup"><span data-stu-id="4d970-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="4d970-116">Definindo-toostatic garante que o endereço IP público Olá atribuído nunca será alterado.</span><span class="sxs-lookup"><span data-stu-id="4d970-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="4d970-117">Olá, seção a seguir mostra a associação de saudação do endereço IP público de saudação com uma interface de rede:</span><span class="sxs-lookup"><span data-stu-id="4d970-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="4d970-118">Saudação de aviso **publicIPAddress** propriedade apontando toohello **Id** de um recurso chamado **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="4d970-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="4d970-119">Esse é o nome de saudação do recurso IP público Olá mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="4d970-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="4d970-120">Por fim, acima da interface de rede de saudação está listada no hello **networkProfile** propriedade Olá VM que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="4d970-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="4d970-121">Implantar o modelo de saudação usando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="4d970-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="4d970-122">Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="4d970-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="4d970-123">toodeploy usando esse modelo clique toodeploy, clique em **implantar tooAzure** no arquivo Readme.md Olá Olá [VM com PIP estático](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modelo.</span><span class="sxs-lookup"><span data-stu-id="4d970-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="4d970-124">Substituir valores de parâmetro padrão hello, se desejado e insira valores para parâmetros de saudação em branco.</span><span class="sxs-lookup"><span data-stu-id="4d970-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="4d970-125">Siga as instruções de Olá Olá portal toocreate uma máquina virtual com um endereço IP público estático.</span><span class="sxs-lookup"><span data-stu-id="4d970-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="4d970-126">Implante o modelo de saudação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d970-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="4d970-127">modelo de saudação toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d970-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="4d970-128">Se você nunca usou o Azure PowerShell, Olá concluir etapas no hello [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="4d970-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="4d970-129">Em um console do PowerShell, execute Olá `New-AzureRmResourceGroup` cmdlet toocreate um novo grupo de recursos, se necessário.</span><span class="sxs-lookup"><span data-stu-id="4d970-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="4d970-130">Se você já tiver criado um grupo de recursos, vá toostep 3.</span><span class="sxs-lookup"><span data-stu-id="4d970-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="4d970-131">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4d970-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="4d970-132">Em um console do PowerShell, execute Olá `New-AzureRmResourceGroupDeployment` modelo do cmdlet toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="4d970-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="4d970-133">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="4d970-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="4d970-134">Implantar o modelo hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4d970-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="4d970-135">modelo de saudação toodeploy usando Olá CLI do Azure, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d970-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="4d970-136">Se você nunca tiver usado a CLI do Azure, siga as etapas de Olá Olá [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) artigo tooinstall e configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="4d970-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="4d970-137">Executar Olá `azure config mode` modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d970-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="4d970-138">Olá esperado saída Olá comando acima:</span><span class="sxs-lookup"><span data-stu-id="4d970-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="4d970-139">Olá abrir [arquivo de parâmetro](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selecione o seu conteúdo e salve-o arquivo tooa no seu computador.</span><span class="sxs-lookup"><span data-stu-id="4d970-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="4d970-140">Neste exemplo, os parâmetros de saudação são salvos arquivo tooa chamado *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="4d970-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="4d970-141">Alterar valores de parâmetro de saudação do arquivo hello, se desejado, mas, no mínimo, é recomendável que você altere o valor Olá Olá adminPassword parâmetro tooa complexo senha exclusiva.</span><span class="sxs-lookup"><span data-stu-id="4d970-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="4d970-142">Executar Olá `azure group deployment create` cmd toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima.</span><span class="sxs-lookup"><span data-stu-id="4d970-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="4d970-143">O comando Olá abaixo, substitua <path> com caminho de saudação você salvou o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4d970-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="4d970-144">Saída esperada (lista os valores de parâmetro usados):</span><span class="sxs-lookup"><span data-stu-id="4d970-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

