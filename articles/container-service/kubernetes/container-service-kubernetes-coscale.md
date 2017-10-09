---
title: aaaMonitor Kubernetes um Azure cluster com CoScale | Microsoft Docs
description: "Monitorar um cluster Kubernetes no Serviço de Contêiner do Azure usando CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Monitorar um cluster Kubernetes do Serviço de Contêiner do Azure usando CoScale

Neste artigo, mostramos como Olá toodeploy [CoScale](https://www.coscale.com/) toomonitor agente todos os nós e contêineres em sua Kubernetes de cluster no serviço de contêiner do Azure. Você precisa de uma conta com CoScale para essa configuração. 


## <a name="about-coscale"></a>Sobre o CoScale 

CoScale é uma plataforma de monitoramento que reúne as métricas e eventos de todos os contêineres em várias plataformas de orquestração. CoScale oferece monitoramento de pilha completa para ambientes Kubernetes. Ele fornece visualizações e análise para todas as camadas na pilha de saudação: Olá SO, Kubernetes, Docker e aplicativos em execução dentro de seus contêineres. CoScale oferece vários painéis de monitoramentos internos e ele tem operadores de tooallow de detecção de anomalias internos e rápida de problemas de infraestrutura e aplicativo toofind desenvolvedores.

![Interface do usuário do CoScale](./media/container-service-kubernetes-coscale/coscale.png)

Conforme mostrado neste artigo, você pode instalar agentes em um cluster de Kubernetes toorun CoScale como uma solução de SaaS. Se desejar tookeep seus dados no local, CoScale também está disponível para instalação no local.


## <a name="prerequisites"></a>Pré-requisitos

É necessário primeiro muito[criar uma conta de CoScale](https://www.coscale.com/free-trial).

Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).

Ele também pressupõe que você tenha Olá `az` CLI do Azure e `kubectl` ferramentas instaladas.

Você pode testar se você tiver Olá `az` ferramenta instalada executando:

```azurecli
az --version
```

Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](/cli/azure/install-azure-cli).

Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:

```bash
kubectl version
```

Se não tem `kubectl` instalado, você pode executar:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>Instalando o agente de CoScale Olá com um DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) são usado por Kubernetes toorun uma única instância de um contêiner em cada host no cluster hello.
Eles são perfeitos para a execução de agentes de monitoramento, como o agente de CoScale hello.

Depois de efetuar login tooCoScale, vá toohello [página agente](https://app.coscale.com/) agentes de CoScale tooinstall no seu cluster usando um DaemonSet. Olá CoScale da interface do usuário fornece configuração interativa etapas toocreate um agente e iniciar a monitoração do seu cluster Kubernetes concluída.

![Configuração do agente do CoScale](./media/container-service-kubernetes-coscale/installation.png)

Agente de saudação toostart no cluster hello, execute o comando de saudação fornecido:

![Iniciar o agente de CoScale Olá](./media/container-service-kubernetes-coscale/agent_script.png)

É isso! Quando agentes Olá estão em funcionamento, você deverá ver dados no console de saudação em poucos minutos. Visite Olá [página agente](https://app.coscale.com/) toosee um resumo do cluster, execute etapas adicionais de configuração e ver painéis como Olá **Kubernetes visão geral do cluster**.

![Visão geral do cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

Agente de CoScale Olá automaticamente é implantado em novas máquinas no cluster hello. atualizações de agente Olá automaticamente quando uma nova versão for lançada.


## <a name="next-steps"></a>Próximas etapas

Consulte Olá [CoScale documentação](http://docs.coscale.com/) e [blog](https://www.coscale.com/blog) para obter mais informações sobre CoScale soluções de monitoramento. 

