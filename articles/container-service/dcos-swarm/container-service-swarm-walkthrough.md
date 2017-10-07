---
title: aaaQuickstart - Azure Docker Swarm cluster para Linux | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster de Docker Swarm para contêineres do Linux no serviço de contêiner do Azure com hello CLI do Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a>Implantar cluster do Docker Swarm

Esse início rápido, um cluster de Docker Swarm é implantado usando Olá CLI do Azure. Um aplicativo de contêiner vários consistindo de front-end da web e uma instância do Redis, em seguida, é implantado e executado no cluster hello. Depois de concluído, o aplicativo hello está acessível pela internet de hello.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westus* local.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Saída:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Criar um cluster do Docker Swarm

Criar um cluster de Docker Swarm no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando. 

Olá, exemplo a seguir cria um cluster denominado *mySwarmCluster* com um Linux mestre de nó e três nós de agente do Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

Após alguns minutos, o comando de saudação for concluído e retorna informações de formatados em json sobre cluster de saudação.

## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello

Em todo este guia rápido, é necessário o endereço IP de saudação do mestre de Docker Swarm hello e pool de agente Olá Docker. Execute Olá tooreturn de comando a seguir os dois endereços IP.


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

Saída:

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

Crie um SSH mestre do túnel toohello por nuvem. Substituir `IPAddress` com o endereço IP de saudação do mestre do hello por nuvem.

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

Saudação de conjunto `DOCKER_HOST` variável de ambiente. Isso permite comandos do docker toorun contra Olá Docker Swarm sem ter que toospecify Olá nome de host de saudação.

```bash
export DOCKER_HOST=:2375
```

Agora você está pronto toorun serviços Docker Olá Docker Swarm.


## <a name="run-hello-application"></a>Executar o aplicativo hello

Crie um arquivo chamado `docker-compose.yaml` e Olá cópia após o conteúdo nele.

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Execute Olá após comando toocreate hello Azure voto serviço.

```bash
docker-compose up -d
```

Saída:

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a>Testar o aplicativo hello

Procure o endereço IP toohello Olá por nuvem agente pool tootest aplicativo do Azure voto hello.

![Imagem de navegação tooAzure voto](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Excluir cluster
Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Obter o código de saudação

Nesse início rápido, imagens de contêiner criada previamente foram toocreate usado um serviço do Docker. Olá relacionados ao código do aplicativo, Dockerfile, e compor arquivo estão disponíveis no GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Próximas etapas

Nesse início rápido, implantado de um cluster de Docker Swarm e implantado um aplicativo de multi-contêiner tooit.

toolearn sobre a integração de Docker passiva com o Visual Studio Team Services continuar toohello CI/CD com o Docker Swarm e VSTS.

> [!div class="nextstepaction"]
> [CI/CD com Docker Swarm e VSTS](./container-service-docker-swarm-setup-ci-cd.md)