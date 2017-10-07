---
title: "modelos de aaaLink para implantação do Azure | Microsoft Docs"
description: "Descreve como toouse vinculados modelos em um toocreate de modelo do Azure Resource Manager uma solução de modelo modular. Mostra como os valores de parâmetros toopass, especificar um arquivo de parâmetro e criados dinamicamente as URLs."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Usando modelos vinculados ao implantar os recursos do Azure
De dentro de um modelo do Azure Resource Manager, você pode vincular tooanother modelo, que permite que você toodecompose sua implantação em um conjunto de modelos de destino, a finalidade específica. Assim como com a decomposição de um aplicativo em várias classes de código, a decomposição oferece benefícios em termos de teste, reutilização e legibilidade.  

Você pode passar parâmetros de um modelo vinculado do modelo principal tooa e esses parâmetros diretamente podem mapear tooparameters ou variáveis expostos pelo Olá chamando o modelo. modelo vinculado Olá também pode passar um modelo de origem da variável toohello back saída, habilitando uma troca de dados bidirecional entre os modelos.

## <a name="linking-tooa-template"></a>Vinculando tooa modelo
Você cria um vínculo entre dois modelos com a adição de um recurso de implantação no modelo principal Olá pontos toohello modelo vinculado. Definir Olá **templateLink** toohello propriedade URI de modelo vinculada hello. Você pode fornecer valores de parâmetro de modelo vinculada Olá diretamente em seu modelo ou em um arquivo de parâmetro. Olá, exemplo a seguir usa Olá **parâmetros** propriedade toospecify diretamente um valor de parâmetro.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Como outros tipos de recurso, você pode definir dependências entre modelo vinculado hello e outros recursos. Portanto, quando outros recursos requerem um valor de saída de modelo vinculada hello, você pode fazer se o modelo vinculado Olá foi implantado antes delas. Ou, quando o modelo vinculado Olá depende de outros recursos, você pode verificar se que outros recursos são implantados antes de modelo vinculada hello. Você pode recuperar um valor de um modelo vinculado com hello sintaxe a seguir:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Olá serviço Gerenciador de recursos deve ser modelo vinculada do tooaccess capaz de saudação. Você não pode especificar um arquivo local ou um arquivo que está disponível apenas em sua rede local para o modelo vinculado hello. Você só pode fornecer um valor de URI que inclua **http** ou **https**. Uma opção é tooplace seu modelo vinculado em uma conta de armazenamento e use hello URI para esse item, como mostrado no exemplo a seguir de saudação:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Embora o modelo vinculado Olá deve estar disponível externamente, não precisa toobe toohello disponível público. Você pode adicionar sua conta de armazenamento particular de tooa de modelo que é proprietário da conta de armazenamento tooonly acessível hello. Em seguida, você deve criar um acesso de tooenable token de assinatura (SAS) de acesso compartilhado durante a implantação. Você adiciona esse toohello token SAS URI para o modelo vinculado hello. Para ver as etapas para configurar um modelo em uma conta de armazenamento e gerar um token SAS, consulte [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md) ou [Implantar recursos com modelos do Resource Manager e a CLI do Azure](resource-group-template-deploy-cli.md). 

saudação de exemplo a seguir mostra um modelo de pai modelo tooanother links. modelo vinculado Olá é acessado com um token SAS que é passado como um parâmetro.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Mesmo que o token de saudação é passado como uma cadeia de caracteres segura, hello URI do modelo de saudação vinculado, incluindo o token SAS Olá, é registrado em operações de implantação de saudação. exposição de toolimit, definir uma expiração de token de saudação.

O Resource Manager trata cada modelo vinculado como uma implantação separada. Histórico de implantação Olá Olá para grupo de recursos, você verá implantações separadas para pai hello e modelos aninhados.

![histórico de implantações](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Arquivo de parâmetro tooa de vinculação
Olá próximo exemplo usa Olá **parametersLink** arquivo de parâmetro propriedade toolink tooa.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Olá URI valor Olá parâmetro vinculado arquivo não pode ser um arquivo local e deve incluir **http** ou **https**. arquivo de parâmetro Hello também pode ser limitado tooaccess por meio de um token SAS.

## <a name="using-variables-toolink-templates"></a>Usando variáveis toolink modelos
exemplos anteriores Olá mostraram valores codificados de URL para links de modelo hello. Essa abordagem pode funcionar para um modelo simples, mas não funciona bem quando ao trabalhar com um grande conjunto de modelos modulares. Em vez disso, você pode criar uma variável estática que armazena uma URL base para o modelo principal hello e, em seguida, criar dinamicamente URLs para modelos de saudação vinculado dessa URL base. benefício de saudação dessa abordagem é, você pode facilmente mover ou bifurcação de modelo de saudação porque você só precisa de variável estática do toochange Olá no modelo principal hello. modelo principal Olá passa Olá correto de que URIs em toda a saudação decomposto modelo.

Olá exemplo a seguir mostra como toouse uma toocreate URL base duas URLs para vinculam modelos (**sharedTemplateUrl** e **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

Você também pode usar [deployment()](resource-group-template-functions-deployment.md#deployment) tooget Olá URL base para o modelo atual hello e usar essa URL de saudação do tooget para outros modelos de saudação mesmo local. Essa abordagem é útil se o local do modelo for alterado (talvez devido tooversioning) ou deseja tooavoid rígido URLs no arquivo de modelo de saudação de codificação. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Exemplo completo
Olá modelos de exemplo a seguir mostra uma organização simplificada de modelos vinculados tooillustrate vários conceitos Olá neste artigo. Ele pressupõe que foram adicionados modelos Olá toohello mesmo contêiner em uma conta de armazenamento com acesso público desativado. modelo vinculado Olá passa um modelo principal do valor toohello back Olá **gera** seção.

Olá **parent.json** arquivo consiste em:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Olá **helloworld.json** arquivo consiste em:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

No PowerShell, obter um token para o contêiner de saudação e implantar modelos de saudação com:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

No 2.0 do CLI do Azure, obter um token para o contêiner de saudação e implantar modelos de saudação com hello código a seguir:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre Olá definindo a ordem de implantação Olá para seus recursos, consulte [definem as dependências em modelos do Gerenciador de recursos do Azure](resource-group-define-dependencies.md)
* toolearn como um recurso de toodefine mas criar muitas instâncias do mesmo, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md)

