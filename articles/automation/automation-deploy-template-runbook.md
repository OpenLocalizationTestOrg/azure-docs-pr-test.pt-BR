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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="d8a78-104">Implantar um modelo do Azure Resource Manager em um runbook do PowerShell de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d8a78-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="d8a78-105">Você pode escrever um [runbook do PowerShell de Automação do Azure](automation-first-runbook-textual-powershell.md) que implanta um recurso do Azure usando um [modelo do Azure Resource Management](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="d8a78-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="d8a78-106">Ao fazer isso, você pode automatizar a implantação de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="d8a78-107">Você pode manter seus modelos do Resource Manager em um local central seguro, como no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="d8a78-108">Neste tópico, podemos criar um runbook do PowerShell que usa um modelo do Gerenciador de recursos armazenado em [armazenamento do Azure](../storage/common/storage-introduction.md) toodeploy uma nova conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8a78-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d8a78-109">Prerequisites</span></span>

<span data-ttu-id="d8a78-110">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8a78-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d8a78-111">Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-111">Azure subscription.</span></span> <span data-ttu-id="d8a78-112">Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d8a78-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d8a78-113">[Conta de automação](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="d8a78-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="d8a78-114">Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8a78-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="d8a78-115">[Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md) no qual modelo do Gerenciador de recursos de saudação toostore</span><span class="sxs-lookup"><span data-stu-id="d8a78-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="d8a78-116">Azure PowerShell instalado em um computador local.</span><span class="sxs-lookup"><span data-stu-id="d8a78-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="d8a78-117">Consulte [instalar e configurar o Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obter informações sobre como tooget PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="d8a78-118">Criar o modelo do Gerenciador de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="d8a78-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="d8a78-119">Para este exemplo, usamos um modelo do Resource Manager que implanta uma nova conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="d8a78-120">Em um editor de texto, copie Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8a78-120">In a text editor, copy hello following text:</span></span>

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

<span data-ttu-id="d8a78-121">Salve o arquivo hello localmente como `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="d8a78-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="d8a78-122">Salvar o modelo do Gerenciador de recursos de saudação no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d8a78-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="d8a78-123">Agora podemos usar o PowerShell toocreate um compartilhamento de arquivos de armazenamento do Azure e carregar Olá `TemplateTest.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d8a78-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="d8a78-124">Para obter instruções sobre como toocreate um arquivo de compartilhamento e carregar um arquivo em Olá portal do Azure, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="d8a78-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="d8a78-125">Inicie o PowerShell no computador local e executar Olá comandos toocreate um compartilhamento de arquivos a seguir e carregar o compartilhamento de arquivos toothat do modelo de Gerenciador de recursos de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a78-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

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

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="d8a78-126">Criar script de runbook saudação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8a78-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="d8a78-127">Agora podemos criar um script do PowerShell que obtém Olá `TemplateTest.json` de arquivos do armazenamento do Azure e implanta Olá modelo toocreate uma nova conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="d8a78-128">Em um editor de texto, cole Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8a78-128">In a text editor, paste hello following text:</span></span>

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

<span data-ttu-id="d8a78-129">Salve o arquivo hello localmente como `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="d8a78-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="d8a78-130">Importar e publicar o runbook de saudação à sua conta de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d8a78-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="d8a78-131">Agora use PowerShell tooimport Olá runbook em sua conta de automação do Azure e, em seguida, publicar o runbook hello.</span><span class="sxs-lookup"><span data-stu-id="d8a78-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="d8a78-132">Para obter informações sobre como tooimport e publicar um runbook em Olá portal do Azure, consulte [criar ou importar um runbook na automação do Azure](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d8a78-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="d8a78-133">tooimport `DeployTemplate.ps1` em sua conta de automação como um runbook do PowerShell, execute Olá comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8a78-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

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

## <a name="start-hello-runbook"></a><span data-ttu-id="d8a78-134">Iniciar o runbook Olá</span><span class="sxs-lookup"><span data-stu-id="d8a78-134">Start hello runbook</span></span>

<span data-ttu-id="d8a78-135">Agora, começamos runbook Olá Olá chamada [AzureRmAutomationRunbook início](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d8a78-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="d8a78-136">Para obter informações sobre como toostart um runbook no hello portal do Azure, consulte [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="d8a78-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="d8a78-137">Execute Olá comandos no console do PowerShell Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8a78-137">Run hello following commands in hello PowerShell console:</span></span>

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

<span data-ttu-id="d8a78-138">Olá runbook executa, e você pode verificar o status executando `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="d8a78-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="d8a78-139">Obtém o modelo do Gerenciador de recursos de saudação Olá runbook e o utiliza toodeploy uma nova conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="d8a78-140">Você pode ver que a nova conta de armazenamento Olá criada através da execução Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8a78-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="d8a78-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="d8a78-141">Summary</span></span>

<span data-ttu-id="d8a78-142">É isso!</span><span class="sxs-lookup"><span data-stu-id="d8a78-142">That's it!</span></span> <span data-ttu-id="d8a78-143">Agora você pode usar automação do Azure e o armazenamento do Azure e o Gerenciador de recursos modelos toodeploy todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a78-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8a78-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8a78-144">Next steps</span></span>

* <span data-ttu-id="d8a78-145">toolearn mais sobre modelos do Gerenciador de recursos, consulte [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d8a78-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="d8a78-146">tooget de Introdução ao armazenamento do Azure, consulte [tooAzure Introdução armazenamento](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d8a78-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="d8a78-147">toofind outros útil runbooks de automação do Azure, consulte [galerias de Runbook e o módulo de automação do Azure](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="d8a78-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="d8a78-148">toofind outros modelos do Gerenciador de recursos úteis, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="d8a78-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

