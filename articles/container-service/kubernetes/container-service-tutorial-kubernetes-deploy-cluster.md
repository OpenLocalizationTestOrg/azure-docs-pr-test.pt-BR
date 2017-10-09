---
title: "tutorial de serviço de contêiner aaaAzure - Cluster implantar | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – implantar cluster"
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
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Implantar um cluster Kubernetes no Serviço de Contêiner do Azure

Kubernetes fornece uma plataforma distribuída para aplicativos em contêineres. Com o Serviço de Contêiner do Azure, o provisionamento de um cluster Kubernetes pronto para produção é simples e rápido. Neste tutorial, parte 3 de 7, um cluster Kubernetes do Serviço de Contêiner do Azure é implantado. As etapas concluídas incluem:

> [!div class="checklist"]
> * Implantação de um cluster ACS Kubernetes
> * Instalação do hello Kubernetes CLI (kubectl)
> * Configuração de kubectl

Em tutoriais subsequentes, hello Azure voto aplicativo é implantado cluster toohello, escala, atualizado e Operations Management Suite é o cluster de Kubernetes Olá toomonitor configurado.

## <a name="before-you-begin"></a>Antes de começar

Nos tutoriais anteriores, uma imagem de contêiner foi criada e carregado tooan instância de registro de contêiner do Azure. Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Criar cluster Kubernetes

Em Olá [tutorial anterior](./container-service-tutorial-kubernetes-prepare-acr.md), um grupo de recursos denominado *myResourceGroup* foi criado. Se você não tiver feito isso, crie esse grupo de recursos agora.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Criar um cluster Kubernetes no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando. 

Olá, exemplo a seguir cria um cluster denominado *myK8sCluster* com um Linux mestre de nó e três nós de agente do Linux.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Após alguns minutos, Olá comando for concluído e formatadas em json de retorna informações sobre a implantação de saudação ACS.

## <a name="install-hello-kubectl-cli"></a>Instalar Olá kubectl CLI

tooconnect toohello Kubernetes cluster do computador cliente, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de linha de comando do hello Kubernetes. 

Se você estiver usando o Azure CloudShell, `kubectl` já estará instalado. Se você quiser tooinstall-lo localmente, use Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Se executado em Linux ou macOS, talvez seja necessário toorun com sudo. No Windows, certifique-se de que shell foi executado como administrador.

```azurecli-interactive 
az acs kubernetes install-cli 
```

No Windows, a instalação de padrão de saudação é *c:\program files (x86)\kubectl.exe*. Talvez seja necessário tooadd esse caminho do arquivo toohello Windows. 

## <a name="connect-with-kubectl"></a>Conectar-se com kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, execute Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify Olá conexão tooyour cluster executar Olá [kubectl obter nós](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.

```azurecli-interactive
kubectl get nodes
```

Saída:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

Ao concluir o tutorial, você tem um cluster ACS Kubernetes pronto para cargas de trabalho. Em tutoriais subsequentes, um aplicativo de multi-contêiner é implantado toothis cluster expandida, atualizado e monitorados.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, um cluster Kubernetes do Serviço de Contêiner do Azure foi implantado. Olá, as etapas a seguir foram concluída:

> [!div class="checklist"]
> * Implantação de um cluster ACS Kubernetes
> * Olá instalado Kubernetes CLI (kubectl)
> * Configuração de kubectl

Avançar toohello toolearn próximo de tutorial sobre como executar o aplicativo no cluster hello.

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
