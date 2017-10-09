---
title: "contêineres de aaaDeploy com o comando no Azure Kubernetes | Microsoft Docs"
description: "Use contêineres de toodeploy Olá comando empacotamento ferramenta em um cluster de Kubernetes no serviço de contêiner do Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="1f97a-103">Usar contêineres de toodeploy de comando em um cluster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1f97a-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="1f97a-104">[Comando](https://github.com/kubernetes/helm/) é uma ferramenta de empacotamento do código-fonte aberto que ajuda a instalar e gerenciar o ciclo de vida de saudação do Kubernetes aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1f97a-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="1f97a-105">Gerenciadores de pacotes de tooLinux semelhantes, como get Apt e Yum, comando é usado toomanage Kubernetes gráficos que são pacotes de recursos de Kubernetes pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="1f97a-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="1f97a-106">Este artigo mostra como toowork com o comando em um cluster Kubernetes implantados no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f97a-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="1f97a-107">O Helm tem dois componentes:</span><span class="sxs-lookup"><span data-stu-id="1f97a-107">Helm has two components:</span></span> 
* <span data-ttu-id="1f97a-108">Olá **comando CLI** é um cliente que é executado em seu computador, localmente ou na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="1f97a-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="1f97a-109">**Tiller** é um servidor que é executado no cluster de Kubernetes hello e gerencia o ciclo de vida de saudação de seus aplicativos Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1f97a-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="1f97a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f97a-110">Prerequisites</span></span>

* <span data-ttu-id="1f97a-111">[Implantar um cluster Kubernetes](container-service-kubernetes-walkthrough.md) no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="1f97a-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="1f97a-112">[Instalar e configurar o `kubectl`](../container-service-connect.md) em um computador local</span><span class="sxs-lookup"><span data-stu-id="1f97a-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="1f97a-113">[Instalar o Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) em um computador local</span><span class="sxs-lookup"><span data-stu-id="1f97a-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="1f97a-114">Noções básicas do Helm</span><span class="sxs-lookup"><span data-stu-id="1f97a-114">Helm basics</span></span> 

<span data-ttu-id="1f97a-115">informações de tooview sobre Olá Kubernetes cluster que você está instalando Tiller e implantar seus aplicativos, digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97a-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![informações do cluster kubectl](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="1f97a-117">Depois que você instalou o comando, instale Tiller em seu cluster Kubernetes digitando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="1f97a-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="1f97a-118">Quando ele for concluído com êxito, você verá a saída como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1f97a-118">When it completes successfully, you see output like hello following:</span></span>

![Instalação do Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="1f97a-120">tooview todos os Olá comando gráficos disponíveis no repositório de hello, Olá tipo a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="1f97a-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="1f97a-121">Você verá a saída como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="1f97a-121">You see output like hello following:</span></span>

![Pesquisa do Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="1f97a-123">tooupdate Olá gráficos tooget Olá versões mais recentes, digite:</span><span class="sxs-lookup"><span data-stu-id="1f97a-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="1f97a-124">Implantar um gráfico de controlador de entrada do Nginx</span><span class="sxs-lookup"><span data-stu-id="1f97a-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="1f97a-125">toodeploy um gráfico de controlador de entrada Nginx, digite um único comando:</span><span class="sxs-lookup"><span data-stu-id="1f97a-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Implantar o controlador de entrada](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="1f97a-127">Se você digitar `kubectl get svc` tooview todos os serviços que estão em execução no cluster hello, verá que um endereço IP seja atribuído toohello controlador de entrada.</span><span class="sxs-lookup"><span data-stu-id="1f97a-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="1f97a-128">(Enquanto atribuição hello está em andamento, você verá `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="1f97a-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="1f97a-129">Leva alguns minutos toocomplete.)</span><span class="sxs-lookup"><span data-stu-id="1f97a-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="1f97a-130">Depois que o endereço IP de saudação é atribuído, navegue toohello valor Olá externo IP endereço toosee Olá Nginx back-end em execução.</span><span class="sxs-lookup"><span data-stu-id="1f97a-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Endereço IP de entrada](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="1f97a-132">toosee uma lista de gráficos instalado no seu cluster, tipo:</span><span class="sxs-lookup"><span data-stu-id="1f97a-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="1f97a-133">Você pode abreviar o comando Olá muito`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="1f97a-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="1f97a-134">Implantar um cliente e um gráfico MariaDB</span><span class="sxs-lookup"><span data-stu-id="1f97a-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="1f97a-135">Agora, implante um gráfico de MariaDB e um banco de dados do MariaDB cliente tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1f97a-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="1f97a-136">gráfico do MariaDB toodeploy hello, Olá tipo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f97a-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="1f97a-137">em que `--name` é uma marcação usada para lançamentos.</span><span class="sxs-lookup"><span data-stu-id="1f97a-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="1f97a-138">Se a implantação Olá falhar, execute `helm repo update` e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="1f97a-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="1f97a-139">tooview todos os gráficos de saudação implantadas no cluster, tipo:</span><span class="sxs-lookup"><span data-stu-id="1f97a-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="1f97a-140">tooview todas as implantações em execução no seu cluster, digite:</span><span class="sxs-lookup"><span data-stu-id="1f97a-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="1f97a-141">Por fim, toorun um cliente de saudação do pod tooaccess, digite:</span><span class="sxs-lookup"><span data-stu-id="1f97a-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="1f97a-142">cliente de toohello tooconnect, Olá tipo comando a seguir, substituindo `v1-mariadb` com o nome de saudação da implantação:</span><span class="sxs-lookup"><span data-stu-id="1f97a-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="1f97a-143">Agora você pode usar o padrão SQL comandos toocreate os bancos de dados, tabelas, etc. Por exemplo, `Create DATABASE testdb1;` cria um banco de dados vazio.</span><span class="sxs-lookup"><span data-stu-id="1f97a-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="1f97a-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f97a-144">Next steps</span></span>

* <span data-ttu-id="1f97a-145">Para obter mais informações sobre como gerenciar Kubernetes gráficos, consulte Olá [comando documentação](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="1f97a-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

