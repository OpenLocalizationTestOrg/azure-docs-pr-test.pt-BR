---
title: recursos de aaaDeploy com o PowerShell e o modelo | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e o Azure PowerShell toodeploy um tooAzure de recursos. Olá recursos são definidos em um modelo do Gerenciador de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Implantar recursos com modelos do Resource Manager e o Azure PowerShell

Este tópico explica como toouse PowerShell do Azure com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos. Se você não estiver familiarizado com conceitos de saudação de implantar e gerenciar suas soluções do Azure, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).

modelo do Gerenciador de recursos de saudação implantar pode ser um arquivo local no seu computador ou um arquivo externo que está localizado em um repositório como GitHub. modelo de saudação implantar neste artigo está disponível no hello [modelo](#sample-template) seção, ou como [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Implantar um modelo do computador local

Ao implantar recursos tooAzure, você:

1. Faça logon no tooyour conta do Azure
2. Crie um grupo de recursos que funciona como contêiner Olá para recursos de saudação implantado. nome de Olá saudação do grupo de recursos pode incluir somente caracteres alfanuméricos, períodos, sublinhados, hifens e parênteses. Ele pode ser too90 caracteres. Não pode terminar com um ponto.
3. Implantar o modelo Olá de grupo de recursos de toohello que define Olá recursos toocreate

Um modelo pode incluir parâmetros que permitem a implantação de saudação toocustomize. Por exemplo, você pode fornecer valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção). modelo de exemplo Hello define um parâmetro para a conta de armazenamento Olá SKU.

saudação de exemplo a seguir cria um grupo de recursos e implanta um modelo do computador local:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

implantação de saudação pode levar toocomplete de alguns minutos. Quando terminar, você verá uma mensagem que contém o resultado de saudação:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Implantar um modelo de uma fonte externa

Em vez de armazenar modelos do Gerenciador de recursos em seu computador local, você pode preferir toostore-los em um local externo. É possível armazenar modelos em um repositório de controle de código-fonte (como o GitHub). Ou ainda armazená-los em uma conta de armazenamento do Azure para acesso compartilhado na sua organização.

toodeploy um modelo externo, use Olá **TemplateUri** parâmetro. Use Olá URI no modelo de exemplo hello exemplo toodeploy saudação do GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Olá exemplo anterior requer um URI acessível publicamente para modelo de saudação, que funciona na maioria dos cenários, porque o modelo não deve incluir dados confidenciais. Se você precisar toospecify os dados confidenciais (como uma senha de administrador), passe esse valor como um parâmetro seguro. No entanto, se você não quiser que seu modelo toobe publicamente acessível, você pode protegê-los, armazenando-o em um contêiner de armazenamento privado. Para obter informações sobre como implantar um modelo que exige um token SAS (assinatura de acesso compartilhado), confira [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>Arquivos de parâmetros

Em vez de passar parâmetros como valores embutido em seu script, talvez seja mais fácil toouse um arquivo JSON que contém os valores de parâmetro hello. arquivo de parâmetro Hello deve ser Olá formato a seguir:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Observe que a seção de parâmetros de saudação inclui um nome de parâmetro que coincide com o parâmetro hello definido no modelo (storageAccountType). arquivo de parâmetro Hello contém um valor para o parâmetro hello. Esse valor é automaticamente passado toohello modelo durante a implantação. Você pode criar vários arquivos de parâmetro para diferentes cenários de implantação e, em seguida, passe no arquivo de parâmetro apropriado de saudação. 

Copie Olá anterior de exemplo e salve-o como um arquivo chamado `storage.parameters.json`.

toopass um arquivo de parâmetro de local, use Olá **TemplateParameterFile** parâmetro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass um arquivo de parâmetro externo, use Olá **TemplateParameterUri** parâmetro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Você pode usar parâmetros embutido e um parâmetro de local de arquivo por Olá mesma operação de implantação. Por exemplo, você pode especificar alguns valores no arquivo de parâmetro local hello e adicionar outros valores embutido durante a implantação. Se você fornecer valores para um parâmetro no arquivo de parâmetro local hello e embutido, o valor de embutido de saudação terá precedência.

No entanto, quando você usa um arquivo de parâmetro externo, não é possível passar outros valores embutidos ou de um arquivo local. Quando você especifica um arquivo de parâmetro no hello **TemplateParameterUri** parâmetro, embutidas todos os parâmetros são ignorados. Forneça todos os valores de parâmetro no arquivo externo hello. Se seu modelo incluir um valor confidencial que você não pode incluir no arquivo de parâmetro hello, adicionar esse Cofre de chaves do valor tooa ou fornecer dinamicamente em linha todos os valores de parâmetro.

Se seu modelo incluir um parâmetro com o mesmo nome como um dos parâmetros Olá Olá comando do PowerShell de saudação, PowerShell apresenta o parâmetro hello de seu modelo com sufixo Olá **FromTemplate**. Por exemplo, um parâmetro denominado **ResourceGroupName** em seu modelo está em conflito com hello **ResourceGroupName** parâmetro hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet. Você está tooprovide solicitado um valor para **ResourceGroupNameFromTemplate**. Em geral, você deve evitar essa confusão ao não nomear parâmetros com o mesmo nome como parâmetros usados para operações de implantação de saudação.

## <a name="test-a-template-deployment"></a>Testar uma implantação de modelo

tootest seus valores de parâmetro e de modelo sem realmente implantar qualquer recurso, use [AzureRmResourceGroupDeployment teste](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Se nenhum erro for detectado, o comando Olá termina sem uma resposta. Se um erro for detectado, o comando Olá retorna uma mensagem de erro. Por exemplo, a tentativa de toopass um valor incorreto para a conta de armazenamento Olá SKU, retorna Olá erro a seguir:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Se seu modelo tem um erro de sintaxe, o comando Olá retorna um erro indicando que ele não foi possível analisar o modelo de saudação. mensagem de saudação indica o número de linha de saudação e a posição do erro de análise de saudação.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse completa modo, use Olá `Mode` parâmetro:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Modelo de exemplo

Olá modelo a seguir é usado para obter exemplos de saudação neste tópico. Copie-o e salve-o como um arquivo chamado storage.json. toounderstand como toocreate esse modelo, consulte [criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).  

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

## <a name="next-steps"></a>Próximas etapas
* exemplos de saudação neste artigo implantar grupo de recursos de tooa de recursos em sua assinatura padrão. toouse uma assinatura diferente, consulte [gerenciar várias assinaturas do Azure](/powershell/azure/manage-subscriptions-azureps).
* Para um script de exemplo completo que implanta um modelo, veja [Script de implantação do modelo do Resource Manager](resource-manager-samples-powershell-deploy.md).
* toounderstand como toodefine parâmetros em seu modelo, consulte [entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](resource-group-authoring-templates.md).
* Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

