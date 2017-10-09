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
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Criar e montar um cluster de DC/OS de tooa de compartilhamento de arquivos
Este tutorial fornece detalhes sobre como toocreate um arquivo de compartilhamento no Azure e montá-lo em cada agente e o mestre de Olá cluster DC/OS. Configurar um compartilhamento de arquivo torna mais fácil arquivos de tooshare em todo o cluster como configuração, acesso, logs e muito mais. Olá seguintes tarefas é concluída neste tutorial:

> [!div class="checklist"]
> * Criar uma conta de armazenamento do Azure
> * Criar um compartilhamento de arquivos
> * Montar Olá compartilhamento no cluster do controlador de domínio/OS Olá

Você precisa de um controlador de domínio/SO ACS saudação do cluster toocomplete as etapas neste tutorial. Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Criar um compartilhamento de arquivos no Microsoft Azure

Antes de usar um compartilhamento de arquivos do Azure com um cluster ACS DC/OS, o compartilhamento de arquivo e a conta de armazenamento Olá deve ser criado. Execute Olá script toocreate Olá armazenamento e compartilhamento de arquivos a seguir. Atualize parâmetros de saudação com thoes do seu ambiente.

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

## <a name="mount-hello-share-in-your-cluster"></a>Montar Olá compartilhamento no cluster

Em seguida, Olá compartilhamento de arquivos precisa toobe montado em cada máquina virtual dentro de seu cluster. Essa tarefa é concluída usando o protocolo da ferramenta Olá cifs. operação de montagem Olá pode ser concluída manualmente em cada nó do cluster hello, ou executando um script em cada nó do cluster de saudação.

Neste exemplo, dois scripts são executados, um toomount hello Azure arquivos compartilhamento e um segundo toorun esse script em cada nó do cluster do hello DC/OS.

Primeiro, nome de conta de armazenamento do Azure hello e chave de acesso são necessários. Execute Olá tooget comandos a seguir essas informações. Tome nota de cada um, esses valores são usados em uma etapa posterior.

Nome da conta de armazenamento:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Chave de acesso da conta de armazenamento:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Em seguida, obtenha Olá FQDN do hello DC/SO mestre e armazená-lo em uma variável.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Copie o nó mestre toohello chave privada. Essa chave é necessária toocreate um ssh conexão com todos os nós no cluster de saudação. Atualize o nome de usuário de saudação se um valor padrão não foi usado durante a criação de cluster de saudação. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Crie uma conexão SSH com hello mestre (ou Olá primeiro mestre) do cluster baseado no controlador de domínio/sistema operacional. Atualize o nome de usuário de saudação se um valor padrão não foi usado durante a criação de cluster de saudação.

```azurecli-interactive
ssh azureuser@$FQDN
```

Crie um arquivo chamado **cifsMount.sh**, e Olá cópia seguindo o conteúdo nele. 

Esse script é um compartilhamento de arquivo do Azure Olá toomount usado. Saudação de atualização `STORAGE_ACCT_NAME` e `ACCESS_KEY` variáveis com hello informações coletadas anteriormente.

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
Crie um segundo arquivo denominado **getNodesRunScript.sh** e Olá copiar conteúdo a seguir no arquivo hello. 

Esse script descobre todos os nós de cluster e, em seguida, executa Olá **cifsMount.sh** toomount de script hello compartilhamento de arquivos em cada um.

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

Olá executar script toomount hello Azure compartilhamento de arquivos em todos os nós de cluster de saudação.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Olá compartilhamento de arquivos agora está acessível no `/mnt/share/dcosshare` em cada nó do cluster de saudação.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial do Azure compartilhamento de arquivos foi feita tooa disponível cluster de DC/OS usando Olá etapas:

> [!div class="checklist"]
> * Criar uma conta de armazenamento do Azure
> * Criar um compartilhamento de arquivos
> * Montar Olá compartilhamento no cluster do controlador de domínio/OS Olá

Avançar toohello toolearn próximo de tutorial sobre como integrar um registro de contêiner do Azure com o controlador de domínio/sistema operacional no Azure.  

> [!div class="nextstepaction"]
> [Aplicativos de balanceamento de carga](container-service-dcos-acr.md)