---
title: "tutorial de instâncias de contêiner aaaAzure - preparar o registro de contêiner do Azure | Microsoft Docs"
description: "Tutorial sobre Instâncias de Contêiner do Azure – preparar o Registro de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Implantar e usar o Registro de Contêiner do Azure

Esta é a parte dois de um tutorial de três partes. Em Olá [etapa anterior](./container-instances-tutorial-prepare-app.md), uma imagem de contêiner foi criada para um aplicativo da web simples escrito em [Node.js](http://nodejs.org). Neste tutorial, esta imagem é enviada por push tooan registro de contêiner do Azure. Se você não criou a imagem de contêiner hello, retornar muito[Tutorial 1 – Criar imagem de contêiner](./container-instances-tutorial-prepare-app.md). 

Olá registro de contêiner do Azure é um registro baseado no Azure, em particular, para imagens de contêiner do Docker. Este tutorial orienta por meio de implantação de uma instância de registro de contêiner do Azure e enviar um tooit da imagem de contêiner. As etapas concluídas incluem:

> [!div class="checklist"]
> * Implantando uma instância do Registro de Contêiner do Azure
> * Marcação de imagem de contêiner para o Registro de Contêiner do Azure
> * Carregar imagem tooAzure registro de contêiner

Tutoriais subsequentes, você implanta contêiner de saudação do tooAzure seu registro privada instâncias de contêiner.

## <a name="before-you-begin"></a>Antes de começar

Este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Implantar o Registro de Contêiner do Azure

Ao implantar um Registro de Contêiner do Azure, primeiro você precisa de um grupo de recursos. Um grupo de recursos do Azure é uma coleção lógica na qual os recursos do Azure são implantados e gerenciados.

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Neste exemplo, um grupo de recursos denominado *myResourceGroup* é criado no hello *eastus* região.

```azurecli
az group create --name myResourceGroup --location eastus
```

Criar um registro de contêiner do Azure com hello [criar acr az](/cli/azure/acr#create) comando. nome de saudação de um registro de contêiner **devem ser exclusivos**. Olá exemplo a seguir, usamos o nome de saudação *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

Restante Olá deste tutorial, usamos `<acrname>` como um espaço reservado para nome hello de registro de contêiner que você escolheu.

## <a name="container-registry-login"></a>Logon no registro de contêiner

Você deve fazer na instância ACR tooyour antes de enviar imagens tooit. Saudação de uso [logon de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete operação de saudação do comando. É necessário nome exclusivo do hello tooprovide atribuído toohello registro de contêiner quando ele foi criado.

```azurecli
az acr login --name <acrName>
```

comando Olá retorna uma mensagem de 'Logon bem-sucedido' uma vez concluída.

## <a name="tag-container-image"></a>Marcar imagem de contêiner

toodeploy uma imagem de contêiner de um registro particular, a imagem de saudação precisa toobe marcado com hello `loginServer` nome do registro de saudação.

toosee uma lista de imagens atuais, use Olá `docker images` comando.

```bash
docker images
```

Saída:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

nome de loginServer em Olá tooget, execute Olá comando a seguir.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Saudação de marca *aci de tutorial de aplicativo* imagem com loginServer de saudação do registro de contêiner de saudação. Além disso, adicionar `:v1` toohello final do nome da imagem hello. Essa marca indica o número de versão de imagem de saudação.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Quando marcada, executar `docker images` tooverify operação de saudação.

```bash
docker images
```

Saída:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Imagem de push tooAzure registro de contêiner

Enviar por push Olá *aci de tutorial de aplicativo* toohello registro da imagem.

Usando Olá exemplo a seguir, substitua Olá contêiner do registro loginServer por loginServer de saudação do seu ambiente.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Listar imagens no Registro de Contêiner do Azure

tooreturn uma lista de imagens que foram empurrados para registro de contêiner do Azure tooyour, Olá usuário [lista de repositórios de acr az](/cli/azure/acr/repository#list) comando. Atualize o comando Olá com nome de registro do contêiner de saudação.

```azurecli
az acr repository list --name <acrName> --output table
```

Saída:

```azurecli
Result
----------------
aci-tutorial-app
```

E, em seguida, marcas de saudação toosee para uma imagem específica, use Olá [az acr Mostrar repositório marcas](/cli/azure/acr/repository#show-tags) comando.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Saída:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, um registro de contêiner do Azure foi preparado para uso com instâncias de contêiner do Azure e imagem de contêiner Olá foi enviada por push. Olá, as etapas a seguir foram concluída:

> [!div class="checklist"]
> * Implantando uma instância do Registro de Contêiner do Azure
> * Marcação de imagem de contêiner para o Registro de Contêiner do Azure
> * Carregar imagem tooAzure registro de contêiner

Avançar toohello toolearn próximo de tutorial sobre como implantar Olá contêiner tooAzure usando instâncias de contêiner do Azure.

> [!div class="nextstepaction"]
> [Implantar contêineres tooAzure instâncias de contêiner](./container-instances-tutorial-deploy-app.md)
