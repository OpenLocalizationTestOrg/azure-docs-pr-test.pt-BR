---
title: "aaaDeploy um espaço de trabalho do aprendizado de máquina do Azure Resource Manager | Microsoft Docs"
description: "Como toodeploy um espaço de trabalho para o aprendizado de máquina do Azure usando o modelo do Gerenciador de recursos do Azure"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="5961d-103">Implantar Espaço de Trabalho do Machine Learning usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5961d-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="5961d-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="5961d-104">Introduction</span></span>
<span data-ttu-id="5961d-105">Usando um Gerenciador de recursos do Azure modelo de implantação economiza tempo, fornecendo uma maneira escalável toodeploy interconectados componentes com um mecanismo de validação e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="5961d-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="5961d-106">tooset a espaços de trabalho de aprendizado de máquina do Azure, por exemplo, você precisa toofirst configurar uma conta de armazenamento do Azure e, em seguida, implante seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5961d-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="5961d-107">Imagine fazer isso manualmente para centenas de espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5961d-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="5961d-108">Uma alternativa mais fácil é toouse um toodeploy de modelo do Azure Resource Manager um espaço de trabalho do aprendizado de máquina do Azure e todas as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="5961d-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="5961d-109">Este artigo guia você pelo passo a passo desse processo.</span><span class="sxs-lookup"><span data-stu-id="5961d-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="5961d-110">Para obter uma excelente visão geral do Azure Resource Manager, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5961d-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="5961d-111">Passo a passo: criar um Espaço de Trabalho do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5961d-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="5961d-112">Criaremos um grupo de recursos do Azure, implantaremos uma nova conta de armazenamento do Azure e um novo Espaço de Trabalho do Azure Machine Learning usando um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5961d-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="5961d-113">Após a conclusão da implantação hello, podemos imprimirá informações importantes sobre espaços de trabalho de saudação que foram criados (chave primária hello, workspaceID Olá e espaço de trabalho do hello URL toohello).</span><span class="sxs-lookup"><span data-stu-id="5961d-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="5961d-114">Criar um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5961d-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="5961d-115">Um espaço de trabalho do aprendizado de máquina requer um tooit de conjunto de dados vinculado do armazenamento do Azure conta toostore hello.</span><span class="sxs-lookup"><span data-stu-id="5961d-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="5961d-116">Olá modelo a seguir usa nome de saudação do hello recurso grupo toogenerate Olá nome conta de armazenamento e o nome do espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5961d-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="5961d-117">Ele também usa o nome de conta de armazenamento hello como uma propriedade ao criar o espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5961d-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="5961d-118">Salve esse modelo como arquivo mlworkspace.json em c:\temp\.</span><span class="sxs-lookup"><span data-stu-id="5961d-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="5961d-119">Implantar grupo de recursos hello, com base no modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="5961d-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="5961d-120">Abrir o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5961d-120">Open PowerShell</span></span>
* <span data-ttu-id="5961d-121">Instale módulos do Azure Resource Manager e do Gerenciamento de Serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="5961d-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="5961d-122">Essas etapas de baixar e instalar etapas restantes do Olá Olá módulos toocomplete necessário.</span><span class="sxs-lookup"><span data-stu-id="5961d-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="5961d-123">Isso só precisa toobe feito uma vez no ambiente de saudação em que você estiver executando comandos do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5961d-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="5961d-124">Autenticar tooAzure</span><span class="sxs-lookup"><span data-stu-id="5961d-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="5961d-125">Esta etapa deve toobe repetido para cada sessão.</span><span class="sxs-lookup"><span data-stu-id="5961d-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="5961d-126">Uma vez autenticado, as informações da sua assinatura devem ser exibidas.</span><span class="sxs-lookup"><span data-stu-id="5961d-126">Once authenticated, your subscription information should be displayed.</span></span>

![Conta do Azure][1]

<span data-ttu-id="5961d-128">Agora que temos acesso tooAzure, podemos criar grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5961d-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="5961d-129">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5961d-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="5961d-130">Verifique se que esse grupo de recursos hello está provisionado corretamente.</span><span class="sxs-lookup"><span data-stu-id="5961d-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="5961d-131">**ProvisioningState** deve ser "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="5961d-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="5961d-132">nome do grupo de recursos de saudação é usada pelo nome da conta do armazenamento toogenerate Olá Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="5961d-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="5961d-133">o nome de conta de armazenamento Olá deve ter entre 3 e 24 caracteres de comprimento e usar números e letras minúsculas apenas.</span><span class="sxs-lookup"><span data-stu-id="5961d-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Grupo de recursos][2]

* <span data-ttu-id="5961d-135">Usando a implantação do grupo de recursos de saudação, implante um novo espaço de trabalho de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="5961d-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="5961d-136">Concluída a implantação Olá, é simples tooaccess propriedades do espaço de trabalho de saudação implantado.</span><span class="sxs-lookup"><span data-stu-id="5961d-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="5961d-137">Por exemplo, você pode acessar Olá Token de chave primária.</span><span class="sxs-lookup"><span data-stu-id="5961d-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="5961d-138">Outro tokens tooretrieve de forma de espaço de trabalho existente é toouse Olá comando Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="5961d-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="5961d-139">Por exemplo, você pode listar os tokens de saudação primário e secundário de todos os espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5961d-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="5961d-140">Depois que o espaço de trabalho de saudação é provisionado, você também pode automatizar muitas tarefas de estúdio de aprendizado de máquina do Azure usando Olá [módulo do PowerShell para aprendizado de máquina do Azure](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="5961d-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5961d-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5961d-141">Next Steps</span></span>
* <span data-ttu-id="5961d-142">Saiba mais sobre [como criar modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5961d-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="5961d-143">Dê uma olhada nos Olá [repositório de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5961d-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="5961d-144">Assista a este vídeo sobre o [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="5961d-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
