---
title: aaaQuickstart - cluster CE do Docker do Azure para Linux | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster de Docker CE para contêineres do Linux no serviço de contêiner do Azure com hello CLI do Azure."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Implantar um cluster do Docker CE

Esse início rápido, um cluster de Docker CE é implantado usando Olá CLI do Azure. Um aplicativo de contêiner vários consistindo de front-end da web e uma instância do Redis, em seguida, é implantado e executado no cluster hello. Depois de concluído, o aplicativo hello está acessível pela internet de hello.

O Docker CE no Serviço de Contêiner do Azure está na versão prévia e **não deve ser usado para cargas de trabalho de produção**.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados.

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *ukwest* local.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
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

Criar um cluster de Docker CE no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando. 

Olá, exemplo a seguir cria um cluster denominado *mySwarmCluster* com um Linux mestre de nó e três nós de agente do Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Após alguns minutos, o comando de saudação for concluído e retorna informações de formatados em json sobre cluster de saudação.

## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello

Em todo este guia rápido, você precisa Olá FQDN do mestre de Docker Swarm hello e pool de agente Olá Docker. Execute Olá tooreturn ambos Olá FQDNs mestre e o agente de comando a seguir.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Saída:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Crie um SSH mestre do túnel toohello por nuvem. Substituir `MasterFQDN` com o endereço FQDN Olá mestre do hello por nuvem.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Saudação de conjunto `DOCKER_HOST` variável de ambiente. Isso permite comandos do docker toorun contra Olá Docker Swarm sem ter que toospecify Olá nome de host de saudação.

```bash
export DOCKER_HOST=localhost:2374
```

Agora você está pronto toorun serviços Docker Olá Docker Swarm.


## <a name="run-hello-application"></a>Executar o aplicativo hello

Crie um arquivo chamado `azure-vote.yaml` e Olá cópia após o conteúdo nele.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Executar Olá [implantar pilha docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) toocreate serviço de Azure voto de saudação do comando.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Saída:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Saudação de uso [docker ps de pilha](https://docs.docker.com/engine/reference/commandline/stack_ps/) comando tooreturn status de implantação de saudação do aplicativo hello.

```bash
docker stack ps azure-vote
```

Uma vez Olá `CURRENT STATE` de cada serviço é `Running`, aplicativo hello está pronto.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Testar o aplicativo hello

Procure toohello FQDN do hello por nuvem agente pool tootest out Olá aplicativo voto do Azure.

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