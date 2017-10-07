---
title: "tutorial de serviço de contêiner aaaAzure - aplicativo escala | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – dimensionar aplicativo"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Dimensionar pods Kubernetes e a infraestrutura do Kubernetes

Se você tiver seguindo tutoriais hello, você tem um cluster de Kubernetes de trabalho no serviço de contêiner do Azure e você tiver implantado hello Azure votação aplicativo. 

Neste tutorial, parte 5 de sete, expansão compartimentos Olá no aplicativo hello e tente autoscaling pod. Você também aprenderá como o número de saudação do tooscale de toochange de nós de agente de VM do Azure Olá capacidade do cluster para hospedar as cargas de trabalho. As tarefas concluídas incluem:

> [!div class="checklist"]
> * Dimensionamento manual de pods Kubernetes
> * Configurando o dimensionamento automático compartimentos executando front-end de aplicativo hello
> * Expandir nós de agente do Azure Kubernetes Olá

Em tutoriais subsequentes, Olá aplicativo do Azure voto é atualizado e Operations Management Suite configurado o cluster de Kubernetes toomonitor hello.

## <a name="before-you-begin"></a>Antes de começar

Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, esta imagem carregada tooAzure registro de contêiner e um cluster Kubernetes criado. aplicativo Hello, em seguida, foi executado no cluster de Kubernetes hello. Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar toohello [Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md). 

No mínimo, este tutorial requer um cluster Kubernetes com um aplicativo em execução.

## <a name="manually-scale-pods"></a>Dimensionar pods manualmente

Até agora, hello Azure voto front-end e a instância do Redis tem sido implantadas, cada um com uma única réplica. tooverify, execute Olá [kubectl obter](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```azurecli-interactive
kubectl get pods
```

Saída:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Alterar manualmente o número de saudação de compartimentos de saudação `azure-vote-front` implantação usando Olá [kubectl escala](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) comando. Este exemplo aumenta too5 número hello.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Executar [kubectl obter compartimentos](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify que Kubernetes está criando compartimentos de saudação. Após um minuto ou menos, compartimentos adicionais hello estão executando:

```azurecli-interactive
kubectl get pods
```

Saída:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Dimensionamento automático de pods

Dá suporte a Kubernetes [autoscaling pod horizontal](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust número de saudação de compartimentos em uma implantação dependendo da utilização da CPU ou outros selecionar métricas. 

toouse Olá autoscaler, seu compartimentos devem ter solicitações de CPU e os limites definidos. Em Olá `azure-vote-front` implantação, Olá CPU de solicitações 0,25 contêiner front-end, com um limite de 0,5 CPU. configurações de saudação se parecer com:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

Olá, exemplo a seguir usa Olá [kubectl AutoEscala](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) tooautoscale Olá número de compartimentos de saudação do comando `azure-vote-front` implantação. Aqui, se a utilização da CPU exceder 50%, Olá autoscaler aumenta Olá compartimentos tooa máximo, 10.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

status de saudação toosee de autoscaler hello, executar Olá comando a seguir:

```azurecli-interactive
kubectl get hpa
```

Saída:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Depois de alguns minutos, com carga mínima no aplicativo do Azure voto hello, número de saudação de réplicas pod diminui automaticamente too3.

## <a name="scale-hello-agents"></a>Agentes de saudação de escala

Se você criou seu cluster Kubernetes usando comandos padrão no tutorial anterior hello, ele tem três nós de agente. Você pode ajustar o número de saudação de agentes manualmente se você planejar mais ou menos cargas de trabalho de contêiner no cluster. Saudação de uso [az acs dimensionar](/cli/azure/acs#scale) de comando e especifique o número de saudação de agentes com hello `--new-agent-count` parâmetro.

Olá, exemplo a seguir aumenta o número de saudação do agente nós too4 Olá Kubernetes cluster denominado *myK8sCluster*. comando Olá leva alguns minutos toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Olá saída do comando mostra Olá número do agente de nós no valor de saudação do `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você usou diferentes recursos de colocação em escala em seu cluster Kubernetes. As tarefas abordadas incluíram:

> [!div class="checklist"]
> * Dimensionamento manual de pods Kubernetes
> * Configurando o dimensionamento automático compartimentos executando front-end de aplicativo hello
> * Expandir nós de agente do Azure Kubernetes Olá

Avançar toohello toolearn próximo de tutorial sobre como atualizar o aplicativo em Kubernetes.

> [!div class="nextstepaction"]
> [Atualizar um aplicativo no Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

