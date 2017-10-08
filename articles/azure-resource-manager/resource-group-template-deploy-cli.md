---
title: recursos de aaaDeploy com CLI do Azure e o modelo | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e a CLI do Azure toodeploy um tooAzure de recursos. Olá recursos são definidos em um modelo do Gerenciador de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Implantar recursos com modelos do Resource Manager e a CLI do Azure

Este tópico explica como toouse 2.0 do CLI do Azure com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos. Se você não estiver familiarizado com conceitos de saudação de implantar e gerenciar suas soluções do Azure, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).  

modelo do Gerenciador de recursos de saudação implantar pode ser um arquivo local no seu computador ou um arquivo externo que está localizado em um repositório como GitHub. modelo de saudação implantar neste artigo está disponível no hello [modelo](#sample-template) seção, ou como um [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Se você não tiver a CLI do Azure instalado, você pode usar o hello [nuvem Shell](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Implantar o modelo local

Ao implantar recursos tooAzure, você:

1. Faça logon no tooyour conta do Azure
2. Crie um grupo de recursos que funciona como contêiner Olá para recursos de saudação implantado. nome de Olá saudação do grupo de recursos pode incluir somente caracteres alfanuméricos, períodos, sublinhados, hifens e parênteses. Ele pode ser too90 caracteres. Não pode terminar com um ponto.
3. Implantar o modelo Olá de grupo de recursos de toohello que define Olá recursos toocreate

Um modelo pode incluir parâmetros que permitem a implantação de saudação toocustomize. Por exemplo, você pode fornecer valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção). modelo de exemplo Hello define um parâmetro para a conta de armazenamento Olá SKU. 

saudação de exemplo a seguir cria um grupo de recursos e implanta um modelo do computador local:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

implantação de saudação pode levar toocomplete de alguns minutos. Quando terminar, você verá uma mensagem que contém o resultado de saudação:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Implantar modelo externo

Em vez de armazenar modelos do Gerenciador de recursos em seu computador local, você pode preferir toostore-los em um local externo. É possível armazenar modelos em um repositório de controle de código-fonte (como o GitHub). Ou ainda armazená-los em uma conta de armazenamento do Azure para acesso compartilhado na sua organização.

toodeploy um modelo externo, use Olá **modelo uri** parâmetro. Use Olá URI no modelo de exemplo hello exemplo toodeploy saudação do GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Olá exemplo anterior requer um URI acessível publicamente para modelo de saudação, que funciona na maioria dos cenários, porque o modelo não deve incluir dados confidenciais. Se você precisar toospecify os dados confidenciais (como uma senha de administrador), passe esse valor como um parâmetro seguro. No entanto, se você não quiser que seu modelo toobe publicamente acessível, você pode protegê-los, armazenando-o em um contêiner de armazenamento privado. Para obter informações sobre como implantar um modelo que exige um token SAS (assinatura de acesso compartilhado), confira [Implantar modelo particular com o token SAS](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Implantar o modelo do Cloud Shell

Você pode usar [nuvem Shell](../cloud-shell/overview.md) comandos toorun Olá CLI do Azure para implantar o modelo. No entanto, você deve carregar o modelo pela primeira vez no compartilhamento de arquivo hello para o Shell de nuvem. Se você ainda não usou o Cloud Shell, confira [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md) para saber mais sobre como configurá-lo.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).   

2. Selecione o grupo de recursos do Cloud Shell. Olá nome padrão é `cloud-shell-storage-<region>`.

   ![Escolha o grupo de recursos](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Selecione a conta de armazenamento de saudação para o Shell de nuvem.

   ![Escolher conta de armazenamento](./media/resource-group-template-deploy-cli/select-storage.png)

4. Selecionar **Arquivos**.

   ![Selecionar arquivos](./media/resource-group-template-deploy-cli/select-files.png)

5. Selecione o compartilhamento de arquivo de saudação para o Shell de nuvem. Olá nome padrão é `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selecionar compartilhamento de arquivos](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Selecione **Adicionar diretório**.

   ![Adicionar diretório](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Dê a ele o nome de **modelos**e selecione **OK**.

   ![Nomear diretório](./media/resource-group-template-deploy-cli/name-templates.png)

8. Selecione o novo diretório.

   ![Selecionar diretório](./media/resource-group-template-deploy-cli/select-templates.png)

9. Escolha **Carregar**.

   ![Selecionar Carregar](./media/resource-group-template-deploy-cli/select-upload.png)

10. Localizar e carregar o modelo.

   ![Carregar arquivo](./media/resource-group-template-deploy-cli/upload-files.png)

11. Prompt Olá aberto.

   ![Abrir Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Digite hello comandos Olá Shell de nuvem a seguir:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

toopass um arquivo de parâmetro de local, use `@` toospecify um arquivo local chamado storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Testar uma implantação de modelo

tootest seus valores de parâmetro e de modelo sem realmente implantar qualquer recurso, use [implantação de grupo az validar](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Se nenhum erro for detectado, o comando de Olá retorna informações sobre a implantação de teste de saudação. Em particular, observe que Olá **erro** valor é nulo.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Se um erro for detectado, o comando Olá retorna uma mensagem de erro. Por exemplo, a tentativa de toopass um valor incorreto para a conta de armazenamento Olá SKU, retorna Olá erro a seguir:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Se seu modelo tem um erro de sintaxe, o comando Olá retorna um erro indicando que ele não foi possível analisar o modelo de saudação. mensagem de saudação indica o número de linha de saudação e a posição do erro de análise de saudação.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse completa modo, use Olá `mode` parâmetro:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* exemplos de saudação neste artigo implantar grupo de recursos de tooa de recursos em sua assinatura padrão. toouse uma assinatura diferente, consulte [gerenciar várias assinaturas do Azure](/cli/azure/manage-azure-subscriptions-azure-cli).
* Para um script de exemplo completo que implanta um modelo, veja [Script de implantação do modelo do Resource Manager](resource-manager-samples-cli-deploy.md).
* toounderstand como toodefine parâmetros em seu modelo, consulte [entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](resource-group-authoring-templates.md).
* Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-cli-sas-token.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).
