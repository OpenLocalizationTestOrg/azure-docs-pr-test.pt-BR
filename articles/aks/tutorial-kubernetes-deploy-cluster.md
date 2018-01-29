---
title: "Tutorial do Kubernetes no Azure – Implantar cluster"
description: Tutorial do AKS - Implantar cluster
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2c2318d9a5f72800f9cfbd430dca448fd1e5746f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="deploy-an-azure-container-service-aks-cluster"></a>Implantar um cluster do AKS (Serviço de Contêiner do Azure)

Kubernetes fornece uma plataforma distribuída para aplicativos em contêineres. Com o AKS, o provisionamento de um cluster Kubernetes pronto para produção é simples e rápido. Neste tutorial, a terceira parte de oito, um cluster Kubernetes é implantado no AKS. As etapas concluídas incluem:

> [!div class="checklist"]
> * Implantação de um cluster AKS Kubernetes
> * Instalação da CLI Kubernetes (kubectl)
> * Configuração de kubectl

Nos tutoriais subsequentes, o aplicativo Azure Vote é implantado no cluster, escalado, atualizado e o Operations Management Suite é configurado para monitorar o cluster Kubernetes.

## <a name="before-you-begin"></a>Antes de começar

Nos tutoriais anteriores, uma imagem de contêiner foi criada e carregada em uma instância do Registro de Contêiner do Azure. Se você ainda não realizou essas etapas e deseja continuar acompanhando, retorne ao [Tutorial 1 – Criar imagens de contêiner][aks-tutorial-prepare-app].

## <a name="enabling-aks-preview-for-your-azure-subscription"></a>Habilitando a versão prévia do AKS para sua assinatura do Azure
Enquanto o AKS está na versão prévia, a criação de novos clusters requer um sinalizador de recurso em sua assinatura. Você pode solicitar esse recurso para qualquer número de assinaturas que deseje usar. Use o comando `az provider register` para registrar o provedor do AKS:

```azurecli-interactive
az provider register -n Microsoft.ContainerService
```

Após o registro, você estará pronto para criar um cluster do Kubernetes com o AKS.

## <a name="create-kubernetes-cluster"></a>Criar cluster Kubernetes

O exemplo a seguir cria um cluster denominado `myK8sCluster` em um Grupo de recursos denominado `myResourceGroup`. Este Grupo de recursos foi criado no [tutorial anterior][aks-tutorial-prepare-acr].

```azurecli
az aks create --resource-group myResourceGroup --name myK8sCluster --node-count 1 --generate-ssh-keys
```

Após alguns minutos, a implantação é concluída e retorna as informações formatadas em JSON sobre a implantação do AKS.

## <a name="install-the-kubectl-cli"></a>Instalar a CLI kubectl

Para se conectar ao cluster Kubernetes do computador cliente, use [kubectl][kubectl], o cliente de linha de comando do Kubernetes.

Se você estiver usando o Azure CloudShell, o kubectl já estará instalado. Se desejar instalá-lo localmente, execute este comando:

```azurecli
az aks install-cli
```

## <a name="connect-with-kubectl"></a>Conectar-se com kubectl

Para configurar o kubectl e se conectar ao cluster Kubernetes, execute este comando:

```azurecli
az aks get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

Para verificar a conexão ao seu cluster, execute o comando [kubectl get nodes][kubectl-get].

```azurecli
kubectl get nodes
```

Saída:

```
NAME                          STATUS    AGE       VERSION
k8s-myk8scluster-36346190-0   Ready     49m       v1.7.7
```

Ao concluir o tutorial, você tem um cluster AKS pronto para cargas de trabalho. Em tutoriais subsequentes, um aplicativo de multicontêiner é implantado nesse cluster, escalado horizontalmente, atualizado e monitorado.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, um cluster Kubernetes foi implantado no AKS. As etapas a seguir foram concluídas:

> [!div class="checklist"]
> * Implantação de um cluster AKS Kubernetes
> * Instalação da CLI Kubernetes (kubectl)
> * Configuração de kubectl

Avance para o próximo tutorial para saber mais sobre como executar o aplicativo no cluster.

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Kubernetes][aks-tutorial-deploy-app]

<!-- LINKS - external -->
[kubectl]: https://kubernetes.io/docs/user-guide/kubectl/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get

<!-- LINKS - internal -->
[aks-tutorial-deploy-app]: ./tutorial-kubernetes-deploy-application.md
[aks-tutorial-prepare-acr]: ./tutorial-kubernetes-prepare-acr.md
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md