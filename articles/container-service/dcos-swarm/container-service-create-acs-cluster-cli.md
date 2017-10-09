---
title: "aaaDeploy um cluster de contêiner do Docker - CLI do Azure | Microsoft Docs"
description: "Implante uma solução Kubernetes, CD/SO ou Docker Swarm no Serviço de Contêiner do Azure usando a CLI 2.0 do Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a>Implantar um contêiner do Docker usando hello Azure CLI 2.0 de solução de hospedagem

Saudação de uso `az acs` comandos no toocreate Olá 2.0 do CLI do Azure e gerenciar clusters no serviço de contêiner do Azure. Você também pode implantar um cluster do serviço de contêiner do Azure usando Olá [portal do Azure](container-service-deployment.md) ou Olá APIs de serviço de contêiner do Azure.

Para obter ajuda sobre `az acs` comandos, passar Olá `-h` comando de tooany do parâmetro. Por exemplo: `az acs create -h`.



## <a name="prerequisites"></a>Pré-requisitos
toocreate um cluster do serviço de contêiner do Azure usando Olá 2.0 do CLI do Azure, você deve:
* ter uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/))
* instalar e configurar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2)

## <a name="get-started"></a>Introdução 
### <a name="log-in-tooyour-account"></a>Faça logon na conta tooyour
```azurecli
az login 
```

Siga Olá prompts toolog em interativamente. Para outros toolog métodos no, consulte [Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).

### <a name="set-your-azure-subscription"></a>Definir sua assinatura do Azure

Se você tiver mais de uma assinatura do Azure, defina a assinatura padrão de saudação. Por exemplo:

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a>Criar um grupos de recursos
Recomendamos que você crie um grupo de recursos para cada cluster. Especifique uma região do Azure no qual o serviço de contêiner do Azure é [disponível](https://azure.microsoft.com/en-us/regions/services/). Por exemplo:

```azurecli
az group create -n acsrg1 -l "westus"
```
O resultado é a seguir toohello semelhante:

![Criar um grupo de recursos](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a>Criar um cluster do Serviço de Contêiner do Azure

toocreate um cluster, use `az acs create`.
Um nome para o cluster de saudação e Olá Olá do grupo de recursos criado na etapa anterior Olá são parâmetros obrigatórios. 

Outras entradas são valores do conjunto de toodefault (consulte Olá tela a seguir), a menos que substituído usando seus respectivos comutadores. Por exemplo, o orchestrator Olá é definido por padrão tooDC/OS. E se não for especificada, um prefixo de nome DNS é criado com base no nome do cluster hello.

![az acs create usage](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a>`acs create` rápido usando padrões
Se você tiver um arquivo de chave pública RSA SSH `id_rsa.pub` no local padrão de saudação (ou criar uma para [OS X e Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use um comando como Olá a seguir:

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
Se você não tiver uma chave pública SSH, use este segundo comando. Esse comando com hello `--generate-ssh-keys` opção criará um para você.

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

Depois de inserir o comando hello, aguarde cerca de 10 minutos para Olá cluster toobe criado. saída do comando Olá inclui nomes de domínio totalmente qualificados (FQDNs) de mestre hello e nós de agente e um SSH comando tooconnect toohello primeiro mestre. Aqui está a saída abreviada:

![Criação ACS de imagem](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> Olá [Kubernetes passo a passo](../kubernetes/container-service-kubernetes-walkthrough.md) mostra como toouse `az acs create` com padrão valores toocreate um Kubernetes de cluster.
>

## <a name="manage-acs-clusters"></a>Gerenciar clusters do ACS

Use adicional `az acs` comandos toomanage seu cluster. Veja alguns exemplos.

### <a name="list-clusters-under-a-subscription"></a>Listar os clusters em uma assinatura

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a>Listar os clusters em um grupo de recursos

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a>Exibir detalhes de um cluster do serviço de contêiner

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a>Cluster de saudação de escala
A ampliação e a redução dos nós de agente são permitidas. Olá parâmetro `new-agent-count` é novo número de saudação de agentes no cluster Olá ACS.

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a>Exclui um cluster do serviço de contêiner
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
Este comando não exclui todos os recursos (rede e armazenamento) criados durante a criação de serviço de contêiner de saudação. toodelete todos os recursos facilmente, é recomendável implantar cada cluster em um grupo de recursos distintos. Em seguida, exclua o grupo de recursos de Olá ao cluster Olá não é mais necessário.

## <a name="next-steps"></a>Próximas etapas
Agora que você tem um cluster em funcionamento, confira estes documentos para obter detalhes sobre conexão e gerenciamento:

* [Conecte-se o cluster do serviço de contêiner do Azure tooan](../container-service-connect.md)
* [Trabalhar com o Serviço de Contêiner do Azure e o DC/SO](container-service-mesos-marathon-rest.md)
* [Trabalhar com o Serviço de Contêiner do Azure e o Docker Swarm](container-service-docker-swarm.md)
* [Trabalhar com o Serviço de Contêiner do Azure e o Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)