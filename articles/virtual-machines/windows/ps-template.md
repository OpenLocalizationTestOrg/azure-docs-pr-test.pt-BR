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
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Criar uma máquina virtual Windows usando um modelo do Resource Manager

Este artigo mostra como toodeploy um Gerenciador de recursos do Azure usando o PowerShell do modelo. modelo Olá criados por você implanta uma única máquina virtual executando o Windows Server em uma nova rede virtual com uma única sub-rede.

Para obter uma descrição detalhada do recurso de máquina virtual hello, consulte [máquinas virtuais em um modelo do Azure Resource Manager](template-description.md). Para obter mais informações sobre todos os recursos de saudação em um modelo, consulte [passo a passo do Gerenciador de recursos do Azure modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Ele deve levar cerca de cinco minutos Olá toodo as etapas neste artigo.

## <a name="install-azure-powershell"></a>Instalar o Azure Powershell

Consulte [como tooinstall e configurar o Azure PowerShell](../../powershell-install-configure.md) para obter informações sobre como instalar a versão mais recente de saudação do PowerShell do Azure, selecione sua assinatura e tooyour conta de assinatura.

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Todos os recursos devem estar implantados em um [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

1. Obtenha uma lista dos locais disponíveis nos quais os recursos podem ser criados.
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. Crie grupo de recursos de saudação no local de saudação que você selecionar. Este exemplo mostra a criação de um grupo de recursos denominado hello **myResourceGroup** em Olá **Oeste dos EUA** local:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>Criar arquivos de saudação

Nesta etapa, você pode criar um arquivo de modelo que implanta recursos hello e um arquivo de parâmetros que fornece o modelo de toohello de valores de parâmetro. Você também pode criar um arquivo de autorização é usada tooperform do Azure Resource Manager operations.

1. Crie um arquivo chamado *CreateVMTemplate.json* e adicionar esse tooit de código JSON:

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

2. Crie um arquivo chamado *Parameters.json* e adicionar esse tooit de código JSON:

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

3. Crie uma nova conta de armazenamento e um contêiner:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Carregar conta de armazenamento Olá arquivos toohello:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Alteração Olá - local do toohello de caminhos de arquivo onde você armazenou os arquivos de saudação.

## <a name="create-hello-resources"></a>Criar recursos de saudação

Implante o modelo de saudação usando parâmetros de saudação:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> Também é possível implantar modelos e parâmetros de arquivos locais. mais, consulte toolearn [usando o PowerShell do Azure com o armazenamento do Azure](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Próximas etapas

- Se houver problemas com a implantação de saudação, você pode dar uma olhada [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
- Saiba como toocreate e gerenciar uma máquina virtual no [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

