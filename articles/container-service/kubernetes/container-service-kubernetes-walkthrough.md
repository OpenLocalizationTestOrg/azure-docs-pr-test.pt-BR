---
title: aaaQuickstart - cluster Kubernetes do Azure para Linux | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster Kubernetes para contêineres do Linux no serviço de contêiner do Azure com hello CLI do Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a>Implantar um cluster Kubernetes para contêineres do Linux

Esse início rápido, um cluster Kubernetes é implantado usando Olá CLI do Azure. Um aplicativo de contêiner vários consistindo de front-end da web e uma instância do Redis, em seguida, é implantado e executado no cluster hello. Depois de concluído, o aplicativo hello está acessível pela internet de hello. 

aplicativo de exemplo Hello usado neste documento é gravado em Python. conceitos de saudação e as etapas descritas aqui podem ser usado toodeploy qualquer contêiner da imagem em um cluster de Kubernetes. Hello código, Dockerfile e projeto de toothis relacionados de arquivos de manifesto Kubernetes pré-criados estão disponíveis em [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).

![Imagem de navegação tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)

Esse início rápido pressupõe uma compreensão básica dos conceitos de Kubernetes, para obter informações detalhadas sobre Kubernetes consulte Olá [Kubernetes documentação]( https://kubernetes.io/docs/home/).

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

Saída:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a>Criar cluster Kubernetes

Criar um cluster Kubernetes no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando. Olá, exemplo a seguir cria um cluster denominado *myK8sCluster* com um Linux mestre de nó e três nós de agente do Linux.

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

Após alguns minutos, o comando de saudação for concluído e retorna informações de formatados em json sobre cluster de saudação. 

## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello

use toomanage um cluster de Kubernetes [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), cliente de linha de comando do hello Kubernetes. 

Se você estiver usando o Azure CloudShell, o kubectl já estará instalado. Se você quiser tooinstall localmente, você pode usar Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

tooconfigure kubectl tooconnect tooyour Kubernetes cluster, execute Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando. Esta etapa baixa credenciais e configura Olá toouse Kubernetes CLI-los.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify Olá conexão tooyour cluster use Olá [kubectl obter](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooreturn comando uma lista de nós de cluster de saudação.

```azurecli-interactive
kubectl get nodes
```

Saída:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a>Executar o aplicativo hello

Um arquivo de manifesto Kubernetes define o estado desejado para cluster hello, incluindo quais imagens de contêiner devem estar em execução. Neste exemplo, um manifesto é usada toocreate todos os objetos necessários toorun Olá aplicativo voto do Azure. 

Crie um arquivo chamado `azure-vote.yml` e copie nele Olá YAML a seguir. Se você estiver trabalhando no Azure Cloud Shell, esse arquivo poderá ser criado usando o vi ou Nano, como se estivesse trabalhando em um sistema físico ou virtual.

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

Saudação de uso [kubectl criar](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicativo hello de toorun de comando.

```azurecli-interactive
kubectl create -f azure-vote.yml
```

Saída:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a>Testar o aplicativo hello

Como o aplicativo hello é executado, uma [Kubernetes serviço](https://kubernetes.io/docs/concepts/services-networking/service/) é criado que expõe Olá toohello de front-end do aplicativo à internet. Esse processo pode levar alguns toocomplete de minutos. 

toomonitor andamento, use Olá [kubectl obter serviço](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) com hello `--watch` argumento.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Olá inicialmente **IP externo** para Olá *front do azure-voto* serviço aparece como *pendente*. Depois que o endereço IP externo de saudação foi alterado de *pendente* tooan *endereço IP*, use `CTRL-C` processo de inspeção de kubectl toostop hello. 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

Agora você pode procurar toohello externo toosee hello Azure voto de aplicativo do IP endereço.

![Imagem de navegação tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a>Excluir cluster
Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Obter o código de saudação

Nesse início rápido, imagens de contêiner criada previamente foram usada toocreate uma implantação Kubernetes. Olá relacionados ao código do aplicativo, Dockerfile, e o arquivo de manifesto Kubernetes estão disponíveis no GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Próximas etapas

Nesse início rápido, implantado um cluster Kubernetes e implantado um aplicativo de multi-contêiner tooit. 

toolearn mais sobre o serviço de contêiner do Azure e passo a passo de um exemplo de código completo a toodeployment, continuar tutorial de cluster Kubernetes toohello.

> [!div class="nextstepaction"]
> [Gerenciar um cluster ACS Kubernetes](./container-service-tutorial-kubernetes-prepare-app.md)
