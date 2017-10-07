---
title: "aaaMounting um volume de arquivos do Azure em instâncias de contêiner do Azure"
description: "Saiba como toomount um Azure arquivos de estado do volume toopersist com instâncias de contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Montar um compartilhamento de arquivos do Azure com Instâncias de Contêiner do Azure

Por padrão, as Instâncias de Contêiner do Azure são sem monitoração de estado. Se o contêiner Olá falha ou interrompido, todos os seus estados serão perdidos. toopersist estado além do tempo de vida de saudação do contêiner hello, você deve montar um volume de um repositório externo. Este artigo mostra como toomount um Azure compartilhamento de arquivos para uso com instâncias de contêiner do Azure.

## <a name="create-an-azure-file-share"></a>Criar um compartilhamento de arquivos do Azure

Antes de usar um compartilhamento de arquivos do Azure com Instâncias de Contêiner do Azure, você deve criá-lo. Executar Olá toocreate de script a seguir um compartilhamento de arquivos do armazenamento conta toohost hello e hello compartilham em si. Observe que esse nome de conta de armazenamento Olá deve ser globalmente exclusivo, para que o script hello adiciona uma cadeia de caracteres valor aleatório toohello base.

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a>Obter detalhes de acesso da conta de armazenamento

toomount compartilhamento de um arquivo do Azure como um volume em instâncias de contêiner do Azure, você precisa de três valores: Olá nome da conta de armazenamento, o nome de compartilhamento de saudação e a chave de acesso de armazenamento de saudação. 

Se você usou o script de saudação acima, o nome de conta de armazenamento Olá foi criado com um valor aleatório no final da saudação. cadeia de caracteres final (incluindo Olá aleatório parte), do tooquery Olá use Olá comandos a seguir:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Olá nome de compartilhamento já é conhecido (é *acishare* no script de saudação acima), portanto, tudo o que resta é a chave de conta de armazenamento hello, que pode ser encontrada usando Olá o comando a seguir:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Armazenar detalhes de acesso da conta de armazenamento com o Azure Key Vault

Chaves da conta de armazenamento proteger acesso tooyour dados, portanto, recomendamos armazená-las em um cofre de chaves do Azure. 

Crie um cofre de chaves com hello CLI do Azure:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Olá `enabled-for-template-deployment` switch permite toopull do Gerenciador de recursos do Azure segredos do seu Cofre de chaves no momento da implantação.

Armazenar chave de conta de armazenamento hello como um novo segredo no cofre de chaves hello:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Monte o volume de saudação

Montar um compartilhamento de arquivos do Azure como um volume em um contêiner é um processo de duas etapas. Primeiro, você fornecer os detalhes de saudação do compartilhamento hello como parte da definição de grupo de contêiner Olá, e você especificar como você deseja que o volume de saudação montado em um ou mais contêineres de saudação no grupo de saudação.

volumes de saudação toodefine desejar toomake disponível para montagem, adicione um `volumes` toohello definição de grupo de contêiner no modelo do Azure Resource Manager Olá de matriz, em seguida, fazer referência a eles na definição de saudação de contêineres individuais hello.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

modelo de saudação inclui Olá nome de conta de armazenamento e chave como parâmetros, que podem ser fornecidos em um arquivo de parâmetros separados. arquivo de parâmetros de saudação toopopulate, você precisará de três valores: Olá nome da conta de armazenamento, Olá ID de recurso do seu Cofre de chaves do Azure e Olá nome secreto do Cofre de chaves que você usou a chave de armazenamento toostore hello. Se você tiver seguido as etapas anteriores, você pode obter esses valores com hello script a seguir:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Inserir valores hello no arquivo de parâmetros de saudação:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a>Contêiner de saudação de implantar e gerenciar arquivos

Com o modelo de saudação definido, você pode criar contêiner hello e montar o volume usando Olá CLI do Azure. Supondo que hello arquivo de modelo é denominado *azuredeploy.json* e nomeado de arquivo hello parâmetros *azuredeploy.parameters.json*, Olá linha de comando é:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Depois que o contêiner de saudação é iniciado, você pode usar Olá web simples aplicativo implantado por meio de saudação **aci/seanmckenna-hellofiles** imagem, toohello gerenciar arquivos no compartilhamento de arquivos do Azure Olá no caminho de montagem Olá que você especificou. Obter o endereço de ip de saudação do aplicativo web de saudação por meio do seguinte hello:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Você pode usar uma ferramenta como Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve e inspecione o compartilhamento de arquivo hello arquivos writen toohello.

>[!NOTE]
> toolearn mais sobre como usar modelos do Gerenciador de recursos do Azure, arquivos de parâmetro e a implantação com hello CLI do Azure, consulte [implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Próximas etapas

- Implantar para o primeiro contêiner usando as instâncias de contêiner do hello Azure [início rápido](container-instances-quickstart.md)
- Saiba mais sobre Olá [relacionamento entre instâncias de contêiner do Azure e orchestrators de contêiner](container-instances-orchestrator-relationship.md)
