---
title: "aaaDeploy um modelo do Gerenciador de recursos do Azure em um runbook de automação do Azure | Microsoft Docs"
description: Como toodeploy um modelo do Azure Resource Manager armazenados no armazenamento do Azure de um runbook
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell,  runbook, json, automação do azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Implantar um modelo do Azure Resource Manager em um runbook do PowerShell de Automação do Azure

Você pode escrever um [runbook do PowerShell de Automação do Azure](automation-first-runbook-textual-powershell.md) que implanta um recurso do Azure usando um [modelo do Azure Resource Management](../azure-resource-manager/resource-manager-create-first-template.md).

Ao fazer isso, você pode automatizar a implantação de recursos do Azure. Você pode manter seus modelos do Resource Manager em um local central seguro, como no Armazenamento do Azure.

Neste tópico, podemos criar um runbook do PowerShell que usa um modelo do Gerenciador de recursos armazenado em [armazenamento do Azure](../storage/common/storage-introduction.md) toodeploy uma nova conta de armazenamento do Azure.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisa Olá a seguir:

* Assinatura do Azure. Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).
* [Conta de automação](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.  Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.
* [Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md) no qual modelo do Gerenciador de recursos de saudação toostore
* Azure PowerShell instalado em um computador local. Consulte [instalar e configurar o Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obter informações sobre como tooget PowerShell do Azure.

## <a name="create-hello-resource-manager-template"></a>Criar o modelo do Gerenciador de recursos de saudação

Para este exemplo, usamos um modelo do Resource Manager que implanta uma nova conta de Armazenamento do Azure.

Em um editor de texto, copie Olá texto a seguir:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

Salve o arquivo hello localmente como `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Salvar o modelo do Gerenciador de recursos de saudação no armazenamento do Azure

Agora podemos usar o PowerShell toocreate um compartilhamento de arquivos de armazenamento do Azure e carregar Olá `TemplateTest.json` arquivo.
Para obter instruções sobre como toocreate um arquivo de compartilhamento e carregar um arquivo em Olá portal do Azure, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](../storage/files/storage-dotnet-how-to-use-files.md).

Inicie o PowerShell no computador local e executar Olá comandos toocreate um compartilhamento de arquivos a seguir e carregar o compartilhamento de arquivos toothat do modelo de Gerenciador de recursos de hello.

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a>Criar script de runbook saudação do PowerShell

Agora podemos criar um script do PowerShell que obtém Olá `TemplateTest.json` de arquivos do armazenamento do Azure e implanta Olá modelo toocreate uma nova conta de armazenamento do Azure.

Em um editor de texto, cole Olá texto a seguir:

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

Salve o arquivo hello localmente como `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>Importar e publicar o runbook de saudação à sua conta de automação do Azure

Agora use PowerShell tooimport Olá runbook em sua conta de automação do Azure e, em seguida, publicar o runbook hello.
Para obter informações sobre como tooimport e publicar um runbook em Olá portal do Azure, consulte [criar ou importar um runbook na automação do Azure](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` em sua conta de automação como um runbook do PowerShell, execute Olá comandos do PowerShell a seguir:

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a>Iniciar o runbook Olá

Agora, começamos runbook Olá Olá chamada [AzureRmAutomationRunbook início](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.

Para obter informações sobre como toostart um runbook no hello portal do Azure, consulte [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md).

Execute Olá comandos no console do PowerShell Olá a seguir:

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

Olá runbook executa, e você pode verificar o status executando `$job.Status`.

Obtém o modelo do Gerenciador de recursos de saudação Olá runbook e o utiliza toodeploy uma nova conta de armazenamento do Azure.
Você pode ver que a nova conta de armazenamento Olá criada através da execução Olá comando a seguir:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Resumo

É isso! Agora você pode usar automação do Azure e o armazenamento do Azure e o Gerenciador de recursos modelos toodeploy todos os recursos do Azure.

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre modelos do Gerenciador de recursos, consulte [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md)
* tooget de Introdução ao armazenamento do Azure, consulte [tooAzure Introdução armazenamento](../storage/common/storage-introduction.md).
* toofind outros útil runbooks de automação do Azure, consulte [galerias de Runbook e o módulo de automação do Azure](automation-runbook-gallery.md).
* toofind outros modelos do Gerenciador de recursos úteis, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/)

