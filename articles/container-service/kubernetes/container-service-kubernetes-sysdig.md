---
title: cluster do Azure Kubernetes aaaMonitor - Sysdig | Microsoft Docs
description: "Monitoramento do cluster Kubernetes no Serviço de Contêiner do Azure usando Sysdig"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Monitorar um cluster Kubernetes do Serviço de Contêiner do Azure usando Sysdig

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).

Ele também pressupõe que você tenha ferramentas de cli e kubectl de saudação do azure instaladas.

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

## <a name="sysdig"></a>Sysdig
O Sysdig é um monitoramento externo como uma empresa de serviço que pode monitorar contêineres no cluster Kubernetes em execução no Azure. O uso do Sysdig requer uma conta ativa do Sysdig.
Você pode se inscrever para uma conta no [site](https://app.sysdigcloud.com).

Depois de entrar no site de nuvem Sysdig toohello, clique em seu nome de usuário e na página hello, você verá sua "chave de acesso". 

![Chave de API d Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Instalando Olá Sysdig agentes tooKubernetes
toomonitor seus contêineres, execuções de Sysdig um processo em cada computador usando um Kubernetes `DaemonSet`.
Os DaemonSets são objetos da API do Kubernetes que executam uma única instância de um contêiner por computador.
Eles são perfeitos para instalar ferramentas como Olá agente de monitoramento do Sysdig.

tooinstall Olá Sysdig daemonset, você deve primeiro baixar [modelo Olá](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) de sysdig. Salve esse arquivo como `sysdig-daemonset.yaml`.

No Linux e no OS X, você pode executar:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

No PowerShell:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Em seguida edite sua chave de acesso que você obteve da sua conta Sysdig tooinsert esse arquivo.

Finalmente, crie Olá DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>Exibir o monitoramento
Depois de instalado e em execução, os agentes de saudação devem bomba tooSysdig de backup de dados.  Voltar toothe [sysdig painel](https://app.sysdigcloud.com) e você deverá ver informações sobre os contêineres.

Você também pode instalar painéis específicos do Kubernetes por meio do [assistente de novo painel](https://app.sysdigcloud.com/#/dashboards/new).
