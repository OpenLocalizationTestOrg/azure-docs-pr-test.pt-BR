---
title: "tutorial de serviço de contêiner aaaAzure - Monitor Kubernetes | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – monitorar o Kubernetes com o OMS (Microsoft Operations Management Suite)"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Monitorar um cluster do Kubernetes com o Operations Management Suite

Monitorar seu cluster do Kubernetes e os contêineres é fundamental, principalmente ao gerenciar um cluster de produção em grande escala com vários aplicativos. 

Você pode usufruir de várias soluções de monitoramento do Kubernetes, da Microsoft ou de outros provedores. Neste tutorial, você deve monitorar seu cluster Kubernetes usando a solução de contêineres de saudação em [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), solução de gerenciamento de TI baseada em nuvem da Microsoft. (Olá solução do OMS contêineres está na visualização).

Este tutorial, parte sete de sete, aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Obter configurações de espaço de trabalho do OMS
> * Configurar agentes do OMS em nós de Kubernetes Olá
> * Acesso a informações de monitoramento no portal do OMS hello ou o portal do Azure

## <a name="before-you-begin"></a>Antes de começar

Nos tutoriais anteriores, um aplicativo foi empacotado em imagens de contêiner, essas imagens carregadas tooAzure registro de contêiner e um cluster Kubernetes criado. Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md). 

No mínimo, este tutorial requer um cluster do Kubernetes com nós de agente do Linux e uma conta do OMS (Operations Management Suite). Se necessário, inscreva-se em uma [avaliação gratuita do OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Obter configurações de espaço de trabalho

Quando você pode acessar Olá [portal do OMS](https://mms.microsoft.com), ir muito**configurações** > **fontes conectadas** > **servidores Linux**. Lá, você pode encontrar hello *ID do espaço de trabalho* e um primário ou secundário *chave do espaço de trabalho*. Anote esses valores, que é necessário tooset agentes do OMS no cluster hello.

## <a name="set-up-oms-agents"></a>Configurar agentes do OMS

Aqui está um tooset de arquivo YAML agentes do OMS em nós de cluster Olá Linux. Ele cria um [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) do Kubernetes, que executa um único pod idêntico em cada nó de cluster. Olá DaemonSet recurso é ideal para a implantação de um agente de monitoramento. 

Salvar Olá seguir chamado o arquivo de texto tooa `oms-daemonset.yaml`e substitua os valores de espaço reservado Olá para *myWorkspaceID* e *myWorkspaceKey* com a ID do espaço de trabalho do OMS e a chave. (Em produção, você pode codificar esses valores como segredos).

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Crie hello DaemonSet com hello comando a seguir:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee que Olá DaemonSet é criado, execute:

```azurecli-interactive
kubectl get daemonset
```

O resultado é a seguir toohello semelhante:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Depois que estiver executando agentes hello, leva vários minutos para OMS tooingest e processar Olá dados.

## <a name="access-monitoring-data"></a>Acessar dados de monitoramento

Exibir e analisar o contêiner OMS Olá dados de monitoramento com hello [solução contêiner](../../log-analytics/log-analytics-containers.md) no portal do OMS hello ou Olá portal do Azure. 

solução de contêiner de saudação tooinstall usando Olá [portal do OMS](https://mms.microsoft.com), ir muito**Galeria de soluções**. Em seguida, adicione a **solução Contêiner**. Como alternativa, adicionar a solução de contêineres de saudação do hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

No portal do OMS hello, procure uma **contêineres** quadro de resumo no painel do OMS hello. Clique em bloco de saudação para detalhes, incluindo: eventos de contêiner, erros, status, inventário de imagem e uso da CPU e memória. Para obter informações mais detalhadas, clique em uma linha em qualquer bloco ou execute uma [pesquisa de logs](../../log-analytics/log-analytics-log-searches.md).

![Painel de contêineres no portal do OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Da mesma forma, no hello portal do Azure, vá muito**análise de Log** e selecione o nome do espaço de trabalho. Olá toosee **contêineres** quadro de resumo, clique em **soluções** > **contêineres**. toosee detalhes, clique em bloco de saudação.

Consulte Olá [documentação do Azure Log Analytics](../../log-analytics/index.md) para obter orientações detalhadas sobre consultar e analisar dados de monitoramento.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você monitorou o cluster do Kubernetes com o OMS. As tarefas abordadas incluíram:

> [!div class="checklist"]
> * Obter configurações de espaço de trabalho do OMS
> * Configurar agentes do OMS em nós de Kubernetes Olá
> * Acesso a informações de monitoramento no portal do OMS hello ou o portal do Azure


Siga este toosee link pré-criadas exemplos de script para o serviço de contêiner.

> [!div class="nextstepaction"]
> [Exemplos de script do Serviço de Contêiner do Azure](cli-samples.md)
