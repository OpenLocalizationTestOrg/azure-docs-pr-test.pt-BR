---
title: "compartilhamento aaaFile para cluster de SO/controlador de domínio do Azure | Microsoft Docs"
description: "Criar e montar um cluster de DC/OS de tooa de compartilhamento de arquivos no serviço de contêiner do Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="9cf98-104">Criar e montar um cluster de DC/OS de tooa de compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="9cf98-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="9cf98-105">Este tutorial fornece detalhes sobre como toocreate um arquivo de compartilhamento no Azure e montá-lo em cada agente e o mestre de Olá cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9cf98-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="9cf98-106">Configurar um compartilhamento de arquivo torna mais fácil arquivos de tooshare em todo o cluster como configuração, acesso, logs e muito mais.</span><span class="sxs-lookup"><span data-stu-id="9cf98-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="9cf98-107">Olá seguintes tarefas é concluída neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="9cf98-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9cf98-108">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf98-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="9cf98-109">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="9cf98-109">Create a file share</span></span>
> * <span data-ttu-id="9cf98-110">Montar Olá compartilhamento no cluster do controlador de domínio/OS Olá</span><span class="sxs-lookup"><span data-stu-id="9cf98-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="9cf98-111">Você precisa de um controlador de domínio/SO ACS saudação do cluster toocomplete as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="9cf98-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="9cf98-112">Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.</span><span class="sxs-lookup"><span data-stu-id="9cf98-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="9cf98-113">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9cf98-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9cf98-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9cf98-115">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9cf98-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="9cf98-116">Criar um compartilhamento de arquivos no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9cf98-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="9cf98-117">Antes de usar um compartilhamento de arquivos do Azure com um cluster ACS DC/OS, o compartilhamento de arquivo e a conta de armazenamento Olá deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="9cf98-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="9cf98-118">Execute Olá script toocreate Olá armazenamento e compartilhamento de arquivos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9cf98-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="9cf98-119">Atualize parâmetros de saudação com thoes do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9cf98-119">Update hello parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="9cf98-120">Montar Olá compartilhamento no cluster</span><span class="sxs-lookup"><span data-stu-id="9cf98-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="9cf98-121">Em seguida, Olá compartilhamento de arquivos precisa toobe montado em cada máquina virtual dentro de seu cluster.</span><span class="sxs-lookup"><span data-stu-id="9cf98-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="9cf98-122">Essa tarefa é concluída usando o protocolo da ferramenta Olá cifs.</span><span class="sxs-lookup"><span data-stu-id="9cf98-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="9cf98-123">operação de montagem Olá pode ser concluída manualmente em cada nó do cluster hello, ou executando um script em cada nó do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="9cf98-124">Neste exemplo, dois scripts são executados, um toomount hello Azure arquivos compartilhamento e um segundo toorun esse script em cada nó do cluster do hello DC/OS.</span><span class="sxs-lookup"><span data-stu-id="9cf98-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="9cf98-125">Primeiro, nome de conta de armazenamento do Azure hello e chave de acesso são necessários.</span><span class="sxs-lookup"><span data-stu-id="9cf98-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="9cf98-126">Execute Olá tooget comandos a seguir essas informações.</span><span class="sxs-lookup"><span data-stu-id="9cf98-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="9cf98-127">Tome nota de cada um, esses valores são usados em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="9cf98-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="9cf98-128">Nome da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="9cf98-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="9cf98-129">Chave de acesso da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="9cf98-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="9cf98-130">Em seguida, obtenha Olá FQDN do hello DC/SO mestre e armazená-lo em uma variável.</span><span class="sxs-lookup"><span data-stu-id="9cf98-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="9cf98-131">Copie o nó mestre toohello chave privada.</span><span class="sxs-lookup"><span data-stu-id="9cf98-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="9cf98-132">Essa chave é necessária toocreate um ssh conexão com todos os nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="9cf98-133">Atualize o nome de usuário de saudação se um valor padrão não foi usado durante a criação de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="9cf98-134">Crie uma conexão SSH com hello mestre (ou Olá primeiro mestre) do cluster baseado no controlador de domínio/sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="9cf98-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="9cf98-135">Atualize o nome de usuário de saudação se um valor padrão não foi usado durante a criação de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="9cf98-136">Crie um arquivo chamado **cifsMount.sh**, e Olá cópia seguindo o conteúdo nele.</span><span class="sxs-lookup"><span data-stu-id="9cf98-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="9cf98-137">Esse script é um compartilhamento de arquivo do Azure Olá toomount usado.</span><span class="sxs-lookup"><span data-stu-id="9cf98-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="9cf98-138">Saudação de atualização `STORAGE_ACCT_NAME` e `ACCESS_KEY` variáveis com hello informações coletadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9cf98-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="9cf98-139">Crie um segundo arquivo denominado **getNodesRunScript.sh** e Olá copiar conteúdo a seguir no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="9cf98-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="9cf98-140">Esse script descobre todos os nós de cluster e, em seguida, executa Olá **cifsMount.sh** toomount de script hello compartilhamento de arquivos em cada um.</span><span class="sxs-lookup"><span data-stu-id="9cf98-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="9cf98-141">Olá executar script toomount hello Azure compartilhamento de arquivos em todos os nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="9cf98-142">Olá compartilhamento de arquivos agora está acessível no `/mnt/share/dcosshare` em cada nó do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9cf98-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cf98-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9cf98-143">Next steps</span></span>

<span data-ttu-id="9cf98-144">Neste tutorial do Azure compartilhamento de arquivos foi feita tooa disponível cluster de DC/OS usando Olá etapas:</span><span class="sxs-lookup"><span data-stu-id="9cf98-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9cf98-145">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf98-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="9cf98-146">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="9cf98-146">Create a file share</span></span>
> * <span data-ttu-id="9cf98-147">Montar Olá compartilhamento no cluster do controlador de domínio/OS Olá</span><span class="sxs-lookup"><span data-stu-id="9cf98-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="9cf98-148">Avançar toohello toolearn próximo de tutorial sobre como integrar um registro de contêiner do Azure com o controlador de domínio/sistema operacional no Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf98-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="9cf98-149">Aplicativos de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="9cf98-149">Load balance applications</span></span>](container-service-dcos-acr.md)