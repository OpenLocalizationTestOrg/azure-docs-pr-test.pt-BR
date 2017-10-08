---
title: aaaMonitor Kubernetes Azure cluster com Datadog | Microsoft Docs
description: "Monitorando o cluster Kubernetes no Serviço de Contêiner do Azure usando o DataDog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Monitorar um cluster do Serviço de Contêiner do Azure com o Datadog

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).

Ele também pressupõe que você tenha Olá `az` cli do Azure e `kubectl` ferramentas instaladas.

Você pode testar se você tiver Olá `az` ferramenta instalada executando:

```console
$ az --version
```

Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).

Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:

```console
$ kubectl version
```

Se não tem `kubectl` instalado, você pode executar:

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>DataDog
O Datadog é um serviço de monitoramento que reúne dados de monitoramento de seus contêineres em seu cluster do Serviço de Contêiner do Azure. O Datadog tem um Painel de Integração do Docker, onde você pode ver as métricas específicas em seus contêineres. As métricas obtidas de seus contêineres são organizadas por CPU, Memória, Rede e E/S. O Datadog divide as métricas em contêineres e em imagens.

É necessário primeiro muito[criar uma conta](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>Instalando Olá Datadog Agent com um DaemonSet
DaemonSets são usados por Kubernetes toorun uma única instância de um contêiner em cada host no cluster hello.
Eles são perfeitos para a execução de agentes de monitoramento.

Depois de fazer logon em Datadog, você pode seguir Olá [Datadog instruções](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agentes no seu cluster usando um DaemonSet.

## <a name="conclusion"></a>Conclusão
É isso! Depois que os agentes de saudação estão funcionando e em execução, você deve ver os dados no console de saudação em poucos minutos. Você pode visitar Olá integrado [kubernetes painel](https://app.datadoghq.com/screen/integration/kubernetes) toosee um resumo do cluster.
