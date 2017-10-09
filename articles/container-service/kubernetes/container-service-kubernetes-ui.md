---
title: aaaManage Kubernetes Azure cluster com a interface da web | Microsoft Docs
description: "Usando Olá Kubernetes web da interface do usuário no serviço de contêiner do Azure"
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="6cdef-103">Usando Olá Kubernetes web da interface do usuário com o serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="6cdef-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cdef-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6cdef-104">Prerequisites</span></span>
<span data-ttu-id="6cdef-105">Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="6cdef-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="6cdef-106">Ele também pressupõe que você tenha Olá 2.0 do CLI do Azure e `kubectl` ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="6cdef-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="6cdef-107">Você pode testar se você tiver Olá `az` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="6cdef-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="6cdef-108">Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="6cdef-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="6cdef-109">Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="6cdef-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="6cdef-110">Se não tem `kubectl` instalado, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="6cdef-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="6cdef-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6cdef-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="6cdef-112">Conecte-se a interface da web toohello</span><span class="sxs-lookup"><span data-stu-id="6cdef-112">Connect toohello web UI</span></span>
<span data-ttu-id="6cdef-113">Você pode iniciar a interface da web Kubernetes Olá executando:</span><span class="sxs-lookup"><span data-stu-id="6cdef-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="6cdef-114">Isso deve abrir um navegador configurado tootalk tooa segura proxy web conectar seu computador local toohello Kubernetes interface da web.</span><span class="sxs-lookup"><span data-stu-id="6cdef-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="6cdef-115">Criar e expor um serviço</span><span class="sxs-lookup"><span data-stu-id="6cdef-115">Create and expose a service</span></span>
1. <span data-ttu-id="6cdef-116">No hello Kubernetes interface da web, clique em **criar** botão na janela direita superior do hello.</span><span class="sxs-lookup"><span data-stu-id="6cdef-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Criar interface do usuário Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="6cdef-118">Isso abrirá uma caixa de diálogo em que você poderá começar a criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6cdef-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="6cdef-119">Olá nome `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="6cdef-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="6cdef-120">Saudação de uso [ `nginx` contêiner do Docker](https://hub.docker.com/_/nginx/) e implantar três réplicas do serviço web.</span><span class="sxs-lookup"><span data-stu-id="6cdef-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Caixa de diálogo Criar Pod Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="6cdef-122">Em **Serviço**, selecione **Externo** e insira a porta 80.</span><span class="sxs-lookup"><span data-stu-id="6cdef-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="6cdef-123">Essa configuração de balanceamento de carga três réplicas de toohello de tráfego.</span><span class="sxs-lookup"><span data-stu-id="6cdef-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Caixa de diálogo Criar serviço Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="6cdef-125">Clique em **implantar** toodeploy esses contêineres e serviços.</span><span class="sxs-lookup"><span data-stu-id="6cdef-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Implantar Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="6cdef-127">Exibir seus contêineres</span><span class="sxs-lookup"><span data-stu-id="6cdef-127">View your containers</span></span>
<span data-ttu-id="6cdef-128">Depois de clicar em **implantar**, Olá da interface do usuário mostra uma exibição do serviço que implanta:</span><span class="sxs-lookup"><span data-stu-id="6cdef-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Status do Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="6cdef-130">Você pode ver o status de saudação de cada objeto Kubernetes no círculo Olá no lado esquerdo de saudação da interface do usuário, em **compartimentos**.</span><span class="sxs-lookup"><span data-stu-id="6cdef-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="6cdef-131">Se for um círculo completo parcialmente, objeto Olá ainda está implantando.</span><span class="sxs-lookup"><span data-stu-id="6cdef-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="6cdef-132">Quando um objeto é totalmente implantado, ele exibe uma marca de seleção verde:</span><span class="sxs-lookup"><span data-stu-id="6cdef-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes implantado](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="6cdef-134">Quando tudo estiver em execução, clique em um dos seus detalhes de toosee compartimentos sobre Olá executando o serviço web.</span><span class="sxs-lookup"><span data-stu-id="6cdef-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Pods Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="6cdef-136">Em Olá **compartimentos** modo de exibição, você pode ver informações sobre contêineres Olá pod hello, bem como recursos de CPU e memória de saudação usados por esses contêineres:</span><span class="sxs-lookup"><span data-stu-id="6cdef-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Recursos do Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="6cdef-138">Se você não vir recursos hello, talvez seja necessário toowait alguns minutos para Olá toopropagate de dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="6cdef-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="6cdef-139">toosee Olá logs para o contêiner, clique em **exibir logs**.</span><span class="sxs-lookup"><span data-stu-id="6cdef-139">toosee hello logs for your container, click **View logs**.</span></span>

![Logs do Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="6cdef-141">Exibindo o serviço</span><span class="sxs-lookup"><span data-stu-id="6cdef-141">Viewing your service</span></span>
<span data-ttu-id="6cdef-142">Adição toorunning seus contêineres, Olá Kubernetes UI criou externo `Service` que provisiona uma carga balanceador toobring tráfego toohello dos contêineres no cluster.</span><span class="sxs-lookup"><span data-stu-id="6cdef-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="6cdef-143">No painel de navegação esquerdo hello, clique em **serviços** tooview todos os serviços (deve haver apenas um).</span><span class="sxs-lookup"><span data-stu-id="6cdef-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Serviços Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="6cdef-145">No modo de exibição, você verá um ponto de extremidade externo (endereço IP) que foi alocado tooyour serviço.</span><span class="sxs-lookup"><span data-stu-id="6cdef-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="6cdef-146">Se clicar no endereço IP, você deverá ver o contêiner nginx em execução por trás do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="6cdef-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx view](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="6cdef-148">Redimensionar o serviço</span><span class="sxs-lookup"><span data-stu-id="6cdef-148">Resizing your service</span></span>
<span data-ttu-id="6cdef-149">Em adição tooviewing seus objetos no hello da interface do usuário, você pode editar e atualizar objetos de API Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="6cdef-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="6cdef-150">Primeiro, clique em **implantações** de saudação à esquerda de implantação de Olá de toosee de painel de navegação para seu serviço.</span><span class="sxs-lookup"><span data-stu-id="6cdef-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="6cdef-151">Quando estiver no modo de exibição, clique no conjunto de réplicas hello e, em seguida, clique em **editar** na barra de navegação superior hello:</span><span class="sxs-lookup"><span data-stu-id="6cdef-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Editar Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="6cdef-153">Editar saudação `spec.replicas` campo toobe `2`e clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="6cdef-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="6cdef-154">Isso faz com que número de saudação de réplicas toodrop tootwo excluindo um de seus compartimentos.</span><span class="sxs-lookup"><span data-stu-id="6cdef-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

