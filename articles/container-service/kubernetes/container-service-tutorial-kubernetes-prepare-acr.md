---
title: "tutorial de serviço de contêiner aaaAzure - preparar ACR | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – preparar o ACR"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Implantar e usar o Registro de Contêiner do Azure

O ACR (Registro de Contêiner do Azure) é um registro privado baseado no Azure, para imagens de contêiner do Docker. Este tutorial, a parte dois dos sete, orienta por meio de implantação de uma instância de registro de contêiner do Azure e enviar um tooit da imagem de contêiner. As etapas concluídas incluem:

> [!div class="checklist"]
> * Implantando uma instância de ACR (Registro de Contêiner do Azure)
> * Marcando uma imagem de contêiner para ACR
> * Carregando Olá imagem tooACR

Nos próximos tutoriais, essa instância do ACR será integrada a um cluster do Kubernetes de Serviço de Contêiner do Azure, para executar as imagens de contêiner com segurança. 

## <a name="before-you-begin"></a>Antes de começar

Em Olá [tutorial anterior](./container-service-tutorial-kubernetes-prepare-app.md), uma imagem de contêiner foi criada para um aplicativo simples de votação do Azure. Neste tutorial, esta imagem é enviada por push tooan registro de contêiner do Azure. Se você não criou a imagem de aplicativo do Azure votação hello, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md). Como alternativa, etapas Olá detalhadas aqui funcionam com qualquer imagem de contêiner.

Este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Implantar o Registro de Contêiner do Azure

Ao implantar um Registro de Contêiner do Azure, primeiro você precisa de um grupo de recursos. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Neste exemplo, um grupo de recursos denominado *myResourceGroup* é criado no hello *westeurope* região.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Criar um registro de contêiner do Azure com hello [criar acr az](/cli/azure/acr#create) comando. nome de saudação de um registro de contêiner **devem ser exclusivos**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

Restante Olá deste tutorial, usamos "acrname" como um espaço reservado para nome hello de registro de contêiner que você escolheu.

## <a name="container-registry-login"></a>Logon no registro de contêiner

Você deve fazer na instância ACR tooyour antes de enviar imagens tooit. Saudação de uso [logon de acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete operação de saudação do comando. É necessário nome exclusivo do hello tooprovide atribuído toohello registro de contêiner quando ele foi criado.

```azurecli
az acr login --name <acrName>
```

comando Olá retorna uma mensagem de 'Logon bem-sucedido' uma vez concluída.

## <a name="tag-container-images"></a>Marcar imagens de contêiner

Cada imagem de contêiner precisa toobe marcada com o nome de loginServer de saudação do registro hello. Essa marca é usada para roteamento ao enviar o registro de imagem de tooan de imagens de contêiner.

toosee uma lista de imagens atuais, use Olá [imagens do docker](https://docs.docker.com/engine/reference/commandline/images/) comando.

```bash
docker images
```

Saída:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

nome de loginServer em Olá tooget, execute Olá comando a seguir.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Agora, Olá de marca *front do azure-voto* imagem com loginServer de saudação do registro de contêiner de saudação. Além disso, adicionar `:redis-v1` toohello final do nome da imagem hello. Essa marca indica a versão da imagem hello.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Quando marcada, execute [imagens docker] operação de saudação tooverify (https://docs.docker.com/engine/reference/commandline/images/).

```bash
docker images
```

Saída:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Enviar por push tooregistry imagens

Enviar por push Olá *front do azure-voto* toohello registro da imagem. 

Usando Olá exemplo a seguir, substitua Olá ACR loginServer por loginServer de saudação do seu ambiente.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Isso leva alguns minutos toocomplete.

## <a name="list-images-in-registry"></a>Lista de imagens no registro

tooreturn uma lista de imagens que foram empurrados para registro de contêiner do Azure tooyour, Olá usuário [lista de repositórios de acr az](/cli/azure/acr/repository#list) comando. Atualize o comando Olá com nome de instância ACR hello.

```azurecli
az acr repository list --name <acrName> --output table
```

Saída:

```azurecli
Result
----------------
azure-vote-front
```

E, em seguida, marcas de saudação toosee para uma imagem específica, use Olá [az acr Mostrar repositório marcas](/cli/azure/acr/repository#show-tags) comando.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Saída:

```azurecli
Result
--------
redis-v1
```

Na conclusão do tutorial, a imagem de contêiner de saudação foi armazenada em uma instância particular de registro de contêiner do Azure. Esta imagem é implantada do cluster do ACR tooa Kubernetes em tutoriais subsequentes.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, um Registro de Contêiner do Azure foi preparado para ser usado em um cluster do Kubernetes do ACS. Olá, as etapas a seguir foram concluída:

> [!div class="checklist"]
> * Implantando uma instância de Registro de Contêiner do Azure
> * Marcando uma imagem de contêiner para ACR
> * Olá carregado tooACR de imagem

Avançar toohello toolearn próximo de tutorial sobre como implantar um cluster Kubernetes no Azure.

> [!div class="nextstepaction"]
> [Implantar um cluster do Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md)