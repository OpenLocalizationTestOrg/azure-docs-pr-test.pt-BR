---
title: aaaQuickstart - cluster Kubernetes do Azure para Windows | Microsoft Docs
description: "Aprenda rapidamente toocreate um cluster Kubernetes para contêineres do Windows no serviço de contêiner do Azure com hello CLI do Azure."
documentationcenter: 
author: dlepow
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
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Implantar um cluster Kubernetes para contêineres do Windows

Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts. Esses detalhes de guia usando Olá CLI do Azure toodeploy um [Kubernetes](https://kubernetes.io/docs/home/) cluster no [serviço de contêiner do Azure](../container-service-intro.md). Depois de saudação cluster for implantado, você se conectar tooit com hello Kubernetes `kubectl` ferramenta de linha de comando e se você implantar o primeiro contêiner do Windows.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> O suporte para contêineres do Windows no Kubernetes no Serviço de Contêiner do Azure está em versão prévia. 
>

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Criar cluster Kubernetes
Criar um cluster Kubernetes no serviço de contêiner do Azure com hello [az acs criar](/cli/azure/acs#create) comando. 

Olá, exemplo a seguir cria um cluster denominado *myK8sCluster* com um Linux mestre de nó e dois nós de agente do Windows. Este exemplo cria SSH mestre do Linux chaves necessárias tooconnect toohello. Este exemplo usa *azureuser* para um nome de usuário administrativo e *myPassword12* senha Olá em nós do Windows hello. Atualize ambiente de tooyour apropriado de toosomething esses valores. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Após alguns minutos, o comando de Olá for concluída e mostra informações sobre a implantação.

## <a name="install-kubectl"></a>Instalar kubectl

tooconnect toohello Kubernetes cluster do computador cliente, use [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), cliente de linha de comando do hello Kubernetes. 

Se você estiver usando o Azure CloudShell, `kubectl` já estará instalado. Se você quiser tooinstall localmente, você pode usar Olá [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.

Olá CLI do Azure instala de exemplo a seguir `kubectl` tooyour sistema. No Windows, execute este comando como administrador.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Conectar-se com kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, execute Olá [az get-credenciais do acs kubernetes](/cli/azure/acs/kubernetes#get-credentials) comando. Olá, exemplo a seguir baixa Olá configuração de cluster para o cluster Kubernetes.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

cluster de tooyour tooverify Olá conexão em seu computador, tente executar:

```azurecli-interactive
kubectl get nodes
```

`kubectl`lista nós de mestre e agente hello.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Implantar um contêiner do IIS do Windows

Você pode executar um contêiner do Docker dentro de um *pod* Kubernetes, que contém um ou mais contêineres. 

Este exemplo básico usa um arquivo JSON toospecify um contêiner do Microsoft Internet Information Server (IIS) e cria pod hello usando Olá `kubctl apply` comando. 

Crie um arquivo local chamado `iis.json` e Olá copiar texto a seguir. Este arquivo informa Kubernetes toorun IIS no Windows Server 2016 Nano Server, usando uma imagem de contêiner público de [Hub do Docker](https://hub.docker.com/r/nanoserver/iis/). contêiner de saudação usa a porta 80, mas inicialmente só está acessível na rede do cluster hello.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

pod de saudação toostart, tipo:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

implantação de saudação tootrack, tipo:
  
```azurecli-interactive
kubectl get pods
```

Quando está implantando pod hello, status de saudação é `ContainerCreating`. Pode levar alguns minutos para saudação do hello contêiner tooenter `Running` estado.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Olá exibir página de boas-vindas do IIS

tooexpose pod toohello Olá com um endereço IP público, Olá tipo comando a seguir:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Com este comando Kubernetes cria um serviço e um [regra do balanceador de carga do Azure](container-service-kubernetes-load-balancing.md) com um endereço IP público para o serviço de saudação. 

Execute Olá comando toosee Olá status Olá serviço a seguir.

```azurecli-interactive
kubectl get svc
```

Inicialmente o endereço IP hello aparece como `pending`. Depois de alguns minutos, Olá endereço IP externo de saudação `iis` pod está definido:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Você pode usar um navegador da web da página toosee choice saudação padrão IIS bem-vindo ao endereço IP externo de saudação:

![Imagem de navegação tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Excluir cluster
Ao cluster Olá não for mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, serviço de contêiner e recursos todos relacionados.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você implantou um cluster Kubernetes, conectou-o a um `kubectl`e implantou um pod com um contêiner do IIS. toolearn mais sobre o serviço de contêiner do Azure, continuar toohello Kubernetes tutorial.

> [!div class="nextstepaction"]
> [Gerenciar um cluster ACS Kubernetes](container-service-tutorial-kubernetes-prepare-app.md)
