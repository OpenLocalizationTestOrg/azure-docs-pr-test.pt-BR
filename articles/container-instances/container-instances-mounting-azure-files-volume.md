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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="e6434-103">Montar um compartilhamento de arquivos do Azure com Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="e6434-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="e6434-104">Por padrão, as Instâncias de Contêiner do Azure são sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="e6434-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="e6434-105">Se o contêiner Olá falha ou interrompido, todos os seus estados serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="e6434-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="e6434-106">toopersist estado além do tempo de vida de saudação do contêiner hello, você deve montar um volume de um repositório externo.</span><span class="sxs-lookup"><span data-stu-id="e6434-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="e6434-107">Este artigo mostra como toomount um Azure compartilhamento de arquivos para uso com instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6434-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="e6434-108">Criar um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="e6434-108">Create an Azure file share</span></span>

<span data-ttu-id="e6434-109">Antes de usar um compartilhamento de arquivos do Azure com Instâncias de Contêiner do Azure, você deve criá-lo.</span><span class="sxs-lookup"><span data-stu-id="e6434-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="e6434-110">Executar Olá toocreate de script a seguir um compartilhamento de arquivos do armazenamento conta toohost hello e hello compartilham em si.</span><span class="sxs-lookup"><span data-stu-id="e6434-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="e6434-111">Observe que esse nome de conta de armazenamento Olá deve ser globalmente exclusivo, para que o script hello adiciona uma cadeia de caracteres valor aleatório toohello base.</span><span class="sxs-lookup"><span data-stu-id="e6434-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

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

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="e6434-112">Obter detalhes de acesso da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e6434-112">Acquire storage account access details</span></span>

<span data-ttu-id="e6434-113">toomount compartilhamento de um arquivo do Azure como um volume em instâncias de contêiner do Azure, você precisa de três valores: Olá nome da conta de armazenamento, o nome de compartilhamento de saudação e a chave de acesso de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6434-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="e6434-114">Se você usou o script de saudação acima, o nome de conta de armazenamento Olá foi criado com um valor aleatório no final da saudação.</span><span class="sxs-lookup"><span data-stu-id="e6434-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="e6434-115">cadeia de caracteres final (incluindo Olá aleatório parte), do tooquery Olá use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6434-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="e6434-116">Olá nome de compartilhamento já é conhecido (é *acishare* no script de saudação acima), portanto, tudo o que resta é a chave de conta de armazenamento hello, que pode ser encontrada usando Olá o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6434-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="e6434-117">Armazenar detalhes de acesso da conta de armazenamento com o Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e6434-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="e6434-118">Chaves da conta de armazenamento proteger acesso tooyour dados, portanto, recomendamos armazená-las em um cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6434-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="e6434-119">Crie um cofre de chaves com hello CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="e6434-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="e6434-120">Olá `enabled-for-template-deployment` switch permite toopull do Gerenciador de recursos do Azure segredos do seu Cofre de chaves no momento da implantação.</span><span class="sxs-lookup"><span data-stu-id="e6434-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="e6434-121">Armazenar chave de conta de armazenamento hello como um novo segredo no cofre de chaves hello:</span><span class="sxs-lookup"><span data-stu-id="e6434-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="e6434-122">Monte o volume de saudação</span><span class="sxs-lookup"><span data-stu-id="e6434-122">Mount hello volume</span></span>

<span data-ttu-id="e6434-123">Montar um compartilhamento de arquivos do Azure como um volume em um contêiner é um processo de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="e6434-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="e6434-124">Primeiro, você fornecer os detalhes de saudação do compartilhamento hello como parte da definição de grupo de contêiner Olá, e você especificar como você deseja que o volume de saudação montado em um ou mais contêineres de saudação no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6434-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="e6434-125">volumes de saudação toodefine desejar toomake disponível para montagem, adicione um `volumes` toohello definição de grupo de contêiner no modelo do Azure Resource Manager Olá de matriz, em seguida, fazer referência a eles na definição de saudação de contêineres individuais hello.</span><span class="sxs-lookup"><span data-stu-id="e6434-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="e6434-126">modelo de saudação inclui Olá nome de conta de armazenamento e chave como parâmetros, que podem ser fornecidos em um arquivo de parâmetros separados.</span><span class="sxs-lookup"><span data-stu-id="e6434-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="e6434-127">arquivo de parâmetros de saudação toopopulate, você precisará de três valores: Olá nome da conta de armazenamento, Olá ID de recurso do seu Cofre de chaves do Azure e Olá nome secreto do Cofre de chaves que você usou a chave de armazenamento toostore hello.</span><span class="sxs-lookup"><span data-stu-id="e6434-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="e6434-128">Se você tiver seguido as etapas anteriores, você pode obter esses valores com hello script a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6434-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="e6434-129">Inserir valores hello no arquivo de parâmetros de saudação:</span><span class="sxs-lookup"><span data-stu-id="e6434-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="e6434-130">Contêiner de saudação de implantar e gerenciar arquivos</span><span class="sxs-lookup"><span data-stu-id="e6434-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="e6434-131">Com o modelo de saudação definido, você pode criar contêiner hello e montar o volume usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6434-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="e6434-132">Supondo que hello arquivo de modelo é denominado *azuredeploy.json* e nomeado de arquivo hello parâmetros *azuredeploy.parameters.json*, Olá linha de comando é:</span><span class="sxs-lookup"><span data-stu-id="e6434-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="e6434-133">Depois que o contêiner de saudação é iniciado, você pode usar Olá web simples aplicativo implantado por meio de saudação **aci/seanmckenna-hellofiles** imagem, toohello gerenciar arquivos no compartilhamento de arquivos do Azure Olá no caminho de montagem Olá que você especificou.</span><span class="sxs-lookup"><span data-stu-id="e6434-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="e6434-134">Obter o endereço de ip de saudação do aplicativo web de saudação por meio do seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e6434-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="e6434-135">Você pode usar uma ferramenta como Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve e inspecione o compartilhamento de arquivo hello arquivos writen toohello.</span><span class="sxs-lookup"><span data-stu-id="e6434-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="e6434-136">toolearn mais sobre como usar modelos do Gerenciador de recursos do Azure, arquivos de parâmetro e a implantação com hello CLI do Azure, consulte [implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6434-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6434-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6434-137">Next steps</span></span>

- <span data-ttu-id="e6434-138">Implantar para o primeiro contêiner usando as instâncias de contêiner do hello Azure [início rápido](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="e6434-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="e6434-139">Saiba mais sobre Olá [relacionamento entre instâncias de contêiner do Azure e orchestrators de contêiner](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="e6434-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
