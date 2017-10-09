---
title: "aaaUsing ACR com um cluster de SO/controlador de domínio do Azure | Microsoft Docs"
description: "Usar um Registro de Contêiner do Azure com um cluster DC/OS no Serviço de Contêiner do Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>Usar ACR com toodeploy de cluster um controlador de domínio/SO seu aplicativo

Neste artigo, exploraremos como toouse registro de contêiner do Azure com um cluster de DC/OS. Usando ACR permite tooprivately repositório e gerenciar imagens de contêiner. Este tutorial aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Implantar o Registro de Contêiner do Azure (se necessário)
> * Configurar a autenticação do ACR em um cluster de DC/SO
> * Carregar uma imagem toohello registro de contêiner do Azure
> * Executar uma imagem de contêiner de saudação do registro de contêiner do Azure

Você precisa de um controlador de domínio/SO ACS saudação do cluster toocomplete as etapas neste tutorial. Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Implantar o Registro de Contêiner do Azure

Se necessário, crie um registro de contêiner do Azure com hello [criar acr az](/cli/azure/acr#create) comando. 

Olá, exemplo a seguir cria um registro com um nome de gerar aleatoriamente. registro de saudação também é configurado com uma conta de administrador usando Olá `--admin-enabled` argumento.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Quando o registro de saudação tiver sido criado, Olá CLI do Azure gera dados semelhantes toohello a seguir. Anote Olá `name` e `loginServer`, eles são usados em etapas posteriores.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Obter credenciais de registro de contêiner hello usando Olá [Mostrar de credencial de acr az](/cli/azure/acr/credential) comando. Olá substituto `--name` com hello um observado na última etapa do hello. Anote uma senha, ela será necessária em uma etapa posterior.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Para obter mais informações sobre o registro de contêiner do Azure, consulte [registros de contêiner de Docker Introdução tooprivate](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>Gerenciar a autenticação do ACR

Olá convencional forma imagem toopush e recepção de um registro particular toofirst autenticar com o registro de saudação. toodo assim, você usaria Olá `docker login` comando em qualquer cliente que precisa do Registro particular do tooaccess hello. Como um cluster de DC/OS pode conter muitos nós, todos precisam toobe autenticado com hello ACR, é útil tooautomate esse processo em cada nó. 

### <a name="create-shared-storage"></a>Criar um armazenamento compartilhado

Esse processo usa um compartilhamento de arquivos do Azure que foi montado em cada nó no cluster hello. Se você ainda não definiu o armazenamento compartilhado, consulte [Criar e montar um compartilhamento de arquivos em um cluster de controlador de domínio/sistema operacional](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>Configurar a autenticação do ACR

Primeiro, obtenha Olá FQDN do hello DC/SO mestre e armazená-lo em uma variável.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Crie uma conexão SSH com hello mestre (ou Olá primeiro mestre) do cluster baseado no controlador de domínio/sistema operacional. Atualize o nome de usuário de saudação se um valor padrão não foi usado durante a criação de cluster de saudação.

```azurecli-interactive
ssh azureuser@$FQDN
```

Olá execução após o comando toologin toohello registro de contêiner do Azure. Substituir saudação `--username` com o nome de saudação do registro de contêiner hello e hello `--password` com uma das senhas Olá fornecido. Substituir o último argumento de saudação *mycontainerregistry.azurecr.io* no exemplo hello com o nome de loginServer de saudação do registro de contêiner de saudação. 

Este comando armazena valores de autenticação Olá localmente em hello `~/.docker` caminho.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Crie um arquivo compactado que contém valores de autenticação Olá contêiner do registro.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Copie esse armazenamento de cluster compartilhado do arquivo toohello. Esta etapa disponibiliza arquivo hello em todos os nós do cluster do hello DC/OS.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Carregar imagem tooACR

Agora um computador de desenvolvimento, ou qualquer outro sistema com o Docker instalado, crie uma imagem e carregá-lo toohello registro de contêiner do Azure.

Crie um recipiente de imagem do Ubuntu hello.

```azurecli-interactive
docker run ubunut --name base-image
```

Agora captura Olá contêiner em uma nova imagem. nome da imagem Olá precisa Olá tooinclude `loginServer` nome da saudação contêiner registrywith um formato de `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Faça logon em Olá registro de contêiner do Azure. Substituir nome hello com o nome de loginServer hello, Olá - nome de usuário com o nome da saudação de registro de contêiner hello e hello – senha com uma das senhas Olá fornecido.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Por fim, carregue o registro da saudação imagem toohello ACR. Este exemplo carrega uma imagem chamada dcos-demo.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Execute uma imagem do ACR

toouse uma imagem do registro ACR hello, crie um arquivo de nomes de *acrDemo.json* e Olá cópia após o texto nela. Substitua o nome de imagem Olá Olá contêiner do registro loginServer nome e imagem, por exemplo `loginServer/imageName`. Anote Olá `uris` propriedade. Esta propriedade contém o local de saudação do arquivo autenticação do hello contêiner do registro, que nesse caso é o compartilhamento de arquivos do Azure de saudação montado em cada nó no cluster de DC/OS de saudação.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Implante o aplicativo de saudação com hello DC/OC CLI.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você tem configurar toouse DC/OS registro de contêiner do Azure incluindo Olá seguintes tarefas:

> [!div class="checklist"]
> * Implantar o Registro de Contêiner do Azure (se necessário)
> * Configurar a autenticação do ACR em um cluster de DC/SO
> * Carregar uma imagem toohello registro de contêiner do Azure
> * Executar uma imagem de contêiner de saudação do registro de contêiner do Azure
