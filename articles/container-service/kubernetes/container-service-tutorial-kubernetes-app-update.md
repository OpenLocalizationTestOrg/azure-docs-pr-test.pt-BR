---
title: "tutorial de serviço de contêiner aaaAzure - aplicativo de atualização | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – atualizar aplicativo"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Atualizar um aplicativo no Kubernetes

Após implantar um aplicativo em Kubernetes, ele poderá ser atualizado especificando uma nova imagem de contêiner ou versão de imagem. Quando você atualizar um aplicativo, distribuição de atualização de saudação preparada para que apenas uma parte da implantação de saudação é atualizada simultaneamente. Essa atualização em etapas permite Olá tookeep de aplicativo em execução durante a atualização de saudação e fornece um mecanismo de reversão se ocorrer uma falha de implantação. 

Neste tutorial, parte seis sete, aplicativo de voto do Azure de exemplo hello é atualizado. As tarefas a serem concluídas incluem:

> [!div class="checklist"]
> * Atualizando o código do aplicativo front-end Olá
> * Criando uma imagem de contêiner atualizada
> * Enviar por push tooAzure de imagem de contêiner Olá registro de contêiner
> * Implantação de imagem de contêiner atualizadas Olá

Em tutoriais subsequentes, Operations Management Suite é cluster de Kubernetes Olá toomonitor configurado.

## <a name="before-you-begin"></a>Antes de começar

Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, imagem Olá carregado tooAzure registro de contêiner e um cluster Kubernetes criado. aplicativo Hello, em seguida, foi executado no cluster de Kubernetes hello. 

Se você não concluir essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Atualizar aplicativo

toocomplete Olá etapas deste tutorial, você deve ter uma cópia clonada de saudação aplicativo voto do Azure. Se necessário, crie essa cópia clonada com hello comando a seguir:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Olá abrir `config_file.cfg` arquivo com qualquer editor de texto ou código. Você pode encontrar esse arquivo em Olá seguindo o diretório de repositório de saudação clonado.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Alterar valores de saudação do `VOTE1VALUE` e `VOTE2VALUE`e, em seguida, salve o arquivo hello.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Use [compor docker](https://docs.docker.com/compose/) toore-criar imagem de front-end hello e aplicativo hello execução atualizado.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Testar o aplicativo localmente

Procurar muito`http://localhost:8080` toosee Olá atualizado o aplicativo.

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Marcar e enviar mensagens por push

Saudação de marca *front do azure-voto* imagem com loginServer de saudação do registro de contêiner de saudação.

Se você estiver usando o registro de contêiner do Azure, obter o nome do servidor de logon de saudação com hello [lista de acr az](/cli/azure/acr#list) comando.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Use [marca docker](https://docs.docker.com/engine/reference/commandline/tag/) tootag imagem de saudação. Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Use [push do docker](https://docs.docker.com/engine/reference/commandline/push/) tooyour registro da imagem de saudação tooupload. Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Implantar aplicativo de atualização

tempo de atividade máximo tooensure, devem estar executando várias instâncias do pod de aplicativo hello. Verifique se essa configuração com hello [kubectl obter pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```bash
kubectl get pod
```

Saída:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Se você não tiver vários compartimentos executando Olá front do azure-voto imagem, dimensionar Olá *front do azure-voto* implantação.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

aplicativo de hello tooupdate, use Olá [kubectl conjunto](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) comando. Atualização `<acrLoginServer>` com o nome de host ou servidor de logon de saudação do registro do contêiner.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

implantação de saudação toomonitor, use Olá [kubectl obter pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando. Como o aplicativo hello atualizado é implantado, seus compartimentos são encerrados e criados novamente com a nova imagem de contêiner Olá.

```azurecli-interactive
kubectl get pod
```

Saída:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Testar aplicativo atualizado

Obter o endereço IP externo de saudação do hello *front do azure-voto* serviço.

```azurecli-interactive
kubectl get service azure-vote-front
```

Procurar toohello IP endereço toosee Olá atualizar o aplicativo.

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você atualizou um aplicativo e distribuiu este cluster de Kubernetes tooa atualização. Olá tarefas a seguir foram concluída:

> [!div class="checklist"]
> * Código do aplicativo front-end Olá atualizado
> * Criamos uma imagem de contêiner atualizada
> * Enviado por push tooAzure de imagem de contêiner Olá registro de contêiner
> * Aplicativo implantado hello atualizado

Avançar toohello toolearn próximo de tutorial sobre como toomonitor Kubernetes com o Operations Management Suite.

> [!div class="nextstepaction"]
> [Monitorar o Kubernetes com o OMS](./container-service-tutorial-kubernetes-monitor.md)