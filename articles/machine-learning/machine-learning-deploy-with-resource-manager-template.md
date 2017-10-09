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
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Implantar Espaço de Trabalho do Machine Learning usando o Azure Resource Manager
## <a name="introduction"></a>Introdução
Usando um Gerenciador de recursos do Azure modelo de implantação economiza tempo, fornecendo uma maneira escalável toodeploy interconectados componentes com um mecanismo de validação e tente novamente. tooset a espaços de trabalho de aprendizado de máquina do Azure, por exemplo, você precisa toofirst configurar uma conta de armazenamento do Azure e, em seguida, implante seu espaço de trabalho. Imagine fazer isso manualmente para centenas de espaços de trabalho. Uma alternativa mais fácil é toouse um toodeploy de modelo do Azure Resource Manager um espaço de trabalho do aprendizado de máquina do Azure e todas as suas dependências. Este artigo guia você pelo passo a passo desse processo. Para obter uma excelente visão geral do Azure Resource Manager, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Passo a passo: criar um Espaço de Trabalho do Machine Learning
Criaremos um grupo de recursos do Azure, implantaremos uma nova conta de armazenamento do Azure e um novo Espaço de Trabalho do Azure Machine Learning usando um modelo do Resource Manager. Após a conclusão da implantação hello, podemos imprimirá informações importantes sobre espaços de trabalho de saudação que foram criados (chave primária hello, workspaceID Olá e espaço de trabalho do hello URL toohello).

### <a name="create-an-azure-resource-manager-template"></a>Criar um modelo do Azure Resource Manager
Um espaço de trabalho do aprendizado de máquina requer um tooit de conjunto de dados vinculado do armazenamento do Azure conta toostore hello.
Olá modelo a seguir usa nome de saudação do hello recurso grupo toogenerate Olá nome conta de armazenamento e o nome do espaço de trabalho de saudação.  Ele também usa o nome de conta de armazenamento hello como uma propriedade ao criar o espaço de trabalho de saudação.

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
Salve esse modelo como arquivo mlworkspace.json em c:\temp\.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Implantar grupo de recursos hello, com base no modelo de saudação
* Abrir o PowerShell
* Instale módulos do Azure Resource Manager e do Gerenciamento de Serviços do Azure  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Essas etapas de baixar e instalar etapas restantes do Olá Olá módulos toocomplete necessário. Isso só precisa toobe feito uma vez no ambiente de saudação em que você estiver executando comandos do PowerShell hello.   

* Autenticar tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Esta etapa deve toobe repetido para cada sessão. Uma vez autenticado, as informações da sua assinatura devem ser exibidas.

![Conta do Azure][1]

Agora que temos acesso tooAzure, podemos criar grupo de recursos de saudação.

* Criar um grupo de recursos

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Verifique se que esse grupo de recursos hello está provisionado corretamente. **ProvisioningState** deve ser "Succeeded".
nome do grupo de recursos de saudação é usada pelo nome da conta do armazenamento toogenerate Olá Olá modelo. o nome de conta de armazenamento Olá deve ter entre 3 e 24 caracteres de comprimento e usar números e letras minúsculas apenas.

![Grupo de recursos][2]

* Usando a implantação do grupo de recursos de saudação, implante um novo espaço de trabalho de aprendizado de máquina.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Concluída a implantação Olá, é simples tooaccess propriedades do espaço de trabalho de saudação implantado. Por exemplo, você pode acessar Olá Token de chave primária.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Outro tokens tooretrieve de forma de espaço de trabalho existente é toouse Olá comando Invoke-AzureRmResourceAction. Por exemplo, você pode listar os tokens de saudação primário e secundário de todos os espaços de trabalho.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Depois que o espaço de trabalho de saudação é provisionado, você também pode automatizar muitas tarefas de estúdio de aprendizado de máquina do Azure usando Olá [módulo do PowerShell para aprendizado de máquina do Azure](http://aka.ms/amlps).

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [como criar modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). 
* Dê uma olhada nos Olá [repositório de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates). 
* Assista a este vídeo sobre o [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
