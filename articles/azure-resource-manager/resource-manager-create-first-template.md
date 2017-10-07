---
title: aaaCreate primeiro o modelo do Gerenciador de recursos do Azure | Microsoft Docs
description: "Um guia passo a passo toocreating seu primeiro modelo do Gerenciador de recursos do Azure. Ele mostra como toouse Olá referência de modelo para um modelo de saudação de toocreate de conta de armazenamento."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Criar e implantar seu primeiro modelo do Azure Resource Manager
Este tópico o guiará durante as etapas de saudação de criar seu primeiro modelo do Gerenciador de recursos do Azure. Modelos do Gerenciador de recursos são arquivos JSON que definem recursos Olá precisar toodeploy para sua solução. conceitos de saudação do toounderstand associados ao implantar e gerenciar suas soluções do Azure, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md). Se você tiver os recursos existentes e deseja tooget um modelo para esses recursos, consulte [exportar um modelo do Gerenciador de recursos do Azure de recursos existentes](resource-manager-export-template.md).

modelos de toocreate e revisar, é necessário um editor de JSON. [Visual Studio Code](https://code.visualstudio.com/) é um editor de código entre plataformas aberto e leve. Recomendamos usar o Visual Studio Code para criar modelos do Resource Manager. Este tópico pressupõe que você esteja usando o VS Code; no entanto, se você tiver outro editor de JSON (como o Visual Studio), use-o.

## <a name="prerequisites"></a>Pré-requisitos

* Visual Studio Code. Se for necessário, instale-o pelo site [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Uma assinatura do Azure. Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="create-template"></a>Criar modelo

Vamos começar com um modelo simple que implanta uma tooyour assinatura da conta de armazenamento.

1. Selecione **Arquivo** > **Novo Arquivo**. 

   ![Novo arquivo](./media/resource-manager-create-first-template/new-file.png)

2. Copie e cole Olá sintaxe JSON a seguir no arquivo:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Nomes de conta de armazenamento tem várias restrições que os tornam difícil tooset. Olá nome deve ter entre 3 e 24 caracteres de comprimento, use apenas números e letras minúsculas e ser exclusivo. o modelo anterior Hello usa Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate um valor de hash de função. toogive esse hash valor mais ou seja, ele adiciona o prefixo Olá *armazenamento*. 

3. Salve esse arquivo como **azuredeploy.json** tooa pasta de local.

   ![Salvar modelo](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Implantar modelo

Você está pronto toodeploy este modelo. Use o PowerShell ou CLI do Azure toocreate um grupo de recursos. Em seguida, você pode implantar um grupo de recursos de toothat de conta de armazenamento.

* Para o PowerShell, use Olá comandos a seguir da pasta Olá contendo Olá modelo:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Para uma instalação local da CLI do Azure, use Olá comandos a seguir da pasta Olá contendo Olá modelo:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Quando termina de implantação, sua conta de armazenamento existe no grupo de recursos de saudação.

## <a name="deploy-template-from-cloud-shell"></a>Implantar o modelo do Cloud Shell

Você pode usar [nuvem Shell](../cloud-shell/overview.md) comandos toorun Olá CLI do Azure para implantar o modelo. No entanto, você deve carregar o modelo pela primeira vez no compartilhamento de arquivo hello para o Shell de nuvem. Se você ainda não usou o Cloud Shell, confira [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md) para saber mais sobre como configurá-lo.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).   

2. Selecione o grupo de recursos do Cloud Shell. Olá nome padrão é `cloud-shell-storage-<region>`.

   ![Escolha o grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Selecione a conta de armazenamento de saudação para o Shell de nuvem.

   ![Escolher conta de armazenamento](./media/resource-manager-create-first-template/select-storage.png)

4. Selecionar **Arquivos**.

   ![Selecionar arquivos](./media/resource-manager-create-first-template/select-files.png)

5. Selecione o compartilhamento de arquivo de saudação para o Shell de nuvem. Olá nome padrão é `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Selecionar compartilhamento de arquivos](./media/resource-manager-create-first-template/select-file-share.png)

6. Selecione **Adicionar diretório**.

   ![Adicionar diretório](./media/resource-manager-create-first-template/select-add-directory.png)

7. Dê a ele o nome de **modelos**e selecione **OK**.

   ![Nomear diretório](./media/resource-manager-create-first-template/name-templates.png)

8. Selecione o novo diretório.

   ![Selecionar diretório](./media/resource-manager-create-first-template/select-templates.png)

9. Escolha **Carregar**.

   ![Selecionar Carregar](./media/resource-manager-create-first-template/select-upload.png)

10. Localizar e carregar o modelo.

   ![Carregar arquivo](./media/resource-manager-create-first-template/upload-files.png)

11. Prompt Olá aberto.

   ![Abrir Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Digite hello comandos Olá Shell de nuvem a seguir:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Quando termina de implantação, sua conta de armazenamento existe no grupo de recursos de saudação.

## <a name="customize-hello-template"></a>Personalizar o modelo de saudação

modelo de saudação funciona bem, mas não é flexível. Ele sempre implanta tooSouth um armazenamento redundante localmente centro dos EUA. nome da saudação é sempre *armazenamento* seguido de um valor de hash. tooenable usando o modelo de saudação para diferentes cenários, adicionar parâmetros toohello modelo.

Olá exemplo a seguir mostra a saudação parâmetros seção com dois parâmetros. Olá primeiro parâmetro `storageSKU` permite que você toospecify o tipo de saudação de redundância. Ele limita os valores hello que você pode passar de toovalues são válidos para uma conta de armazenamento. Ela também especifica um valor padrão. Olá segundo parâmetro `storageNamePrefix` é conjunto tooallow um máximo de 11 caracteres. Ele especifica um valor padrão.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

Na seção de variáveis hello, adicione uma variável chamada `storageName`. Ele combina o valor de prefixo de saudação de parâmetros de saudação e um valor de hash da saudação [uniqueString](resource-group-template-functions-string.md#uniquestring) função. Ele usa Olá [toLower](resource-group-template-functions-string.md#tolower) função tooconvert toolowercase de todos os caracteres.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse esses novos valores para a conta de armazenamento, altere a definição de recurso de saudação:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

Observe que Olá nome da conta de armazenamento Olá agora está definido para a variável toohello que você adicionou. nome da SKU Olá estiver definido como toohello valor do parâmetro hello. Olá local é definido Olá mesmo local que o grupo de recursos de saudação.

Salve o arquivo. 

Depois de concluir as etapas de saudação neste artigo, seu modelo agora se parece com:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Reimplantar o modelo

Reimplante o modelo de saudação com valores diferentes.

Para o PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Para a CLI do Azure, use:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Para Olá Shell de nuvem, carregue o compartilhamento de arquivo do modelo alterado toohello. Substitua arquivo existente hello. Em seguida, use Olá comando a seguir:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, limpe os recursos de saudação implantado excluindo grupo de recursos de saudação.

Para o PowerShell, use:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Para a CLI do Azure, use:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a estrutura de saudação de um modelo, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sobre propriedades de saudação para uma conta de armazenamento, consulte [referência de modelo de contas de armazenamento](/azure/templates/microsoft.storage/storageaccounts).
* modelos de tooview completa para muitos tipos diferentes de soluções, consulte Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).
