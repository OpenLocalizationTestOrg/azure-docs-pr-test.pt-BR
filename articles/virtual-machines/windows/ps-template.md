---
title: aaaCreate uma VM do Windows de um modelo no Azure | Microsoft Docs
description: Use um modelo do Gerenciador de recursos e PowerShell tooeasily criar uma nova VM do Windows.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="67a3f-103">Criar uma máquina virtual Windows usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67a3f-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="67a3f-104">Este artigo mostra como toodeploy um Gerenciador de recursos do Azure usando o PowerShell do modelo.</span><span class="sxs-lookup"><span data-stu-id="67a3f-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="67a3f-105">modelo Olá criados por você implanta uma única máquina virtual executando o Windows Server em uma nova rede virtual com uma única sub-rede.</span><span class="sxs-lookup"><span data-stu-id="67a3f-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="67a3f-106">Para obter uma descrição detalhada do recurso de máquina virtual hello, consulte [máquinas virtuais em um modelo do Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="67a3f-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="67a3f-107">Para obter mais informações sobre todos os recursos de saudação em um modelo, consulte [passo a passo do Gerenciador de recursos do Azure modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="67a3f-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="67a3f-108">Ele deve levar cerca de cinco minutos Olá toodo as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="67a3f-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="67a3f-109">Instalar o Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="67a3f-109">Install Azure PowerShell</span></span>

<span data-ttu-id="67a3f-110">Consulte [como tooinstall e configurar o Azure PowerShell](../../powershell-install-configure.md) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.</span><span class="sxs-lookup"><span data-stu-id="67a3f-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="67a3f-111">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="67a3f-111">Create a resource group</span></span>

<span data-ttu-id="67a3f-112">Todos os recursos devem estar implantados em um [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67a3f-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="67a3f-113">Obtenha uma lista dos locais disponíveis nos quais os recursos podem ser criados.</span><span class="sxs-lookup"><span data-stu-id="67a3f-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="67a3f-114">Crie grupo de recursos de saudação no local de saudação que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="67a3f-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="67a3f-115">Este exemplo mostra a criação de um grupo de recursos denominado hello **myResourceGroup** em Olá **Oeste dos EUA** local:</span><span class="sxs-lookup"><span data-stu-id="67a3f-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="67a3f-116">Criar arquivos de saudação</span><span class="sxs-lookup"><span data-stu-id="67a3f-116">Create hello files</span></span>

<span data-ttu-id="67a3f-117">Nesta etapa, você pode criar um arquivo de modelo que implanta recursos hello e um arquivo de parâmetros que fornece o modelo de toohello de valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="67a3f-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="67a3f-118">Você também pode criar um arquivo de autorização é usada tooperform do Azure Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="67a3f-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="67a3f-119">Crie um arquivo chamado *CreateVMTemplate.json* e adicionar esse tooit de código JSON:</span><span class="sxs-lookup"><span data-stu-id="67a3f-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="67a3f-120">Crie um arquivo chamado *Parameters.json* e adicionar esse tooit de código JSON:</span><span class="sxs-lookup"><span data-stu-id="67a3f-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="67a3f-121">Crie uma nova conta de armazenamento e um contêiner:</span><span class="sxs-lookup"><span data-stu-id="67a3f-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="67a3f-122">Carregar conta de armazenamento Olá arquivos toohello:</span><span class="sxs-lookup"><span data-stu-id="67a3f-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="67a3f-123">Alteração Olá - local do toohello de caminhos de arquivo onde você armazenou os arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="67a3f-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="67a3f-124">Criar recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="67a3f-124">Create hello resources</span></span>

<span data-ttu-id="67a3f-125">Implante o modelo de saudação usando parâmetros de saudação:</span><span class="sxs-lookup"><span data-stu-id="67a3f-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="67a3f-126">Também é possível implantar modelos e parâmetros de arquivos locais.</span><span class="sxs-lookup"><span data-stu-id="67a3f-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="67a3f-127">mais, consulte toolearn [usando o PowerShell do Azure com o armazenamento do Azure](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="67a3f-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67a3f-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67a3f-128">Next Steps</span></span>

- <span data-ttu-id="67a3f-129">Se houver problemas com a implantação de saudação, você pode dar uma olhada [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="67a3f-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="67a3f-130">Saiba como toocreate e gerenciar uma máquina virtual no [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67a3f-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

