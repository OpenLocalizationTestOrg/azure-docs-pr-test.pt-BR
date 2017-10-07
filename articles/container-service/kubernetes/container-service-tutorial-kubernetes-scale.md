---
title: "tutorial de serviço de contêiner aaaAzure - aplicativo escala | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – dimensionar aplicativo"
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="c45ae-104">Dimensionar pods Kubernetes e a infraestrutura do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c45ae-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="c45ae-105">Se você tiver seguindo tutoriais hello, você tem um cluster de Kubernetes de trabalho no serviço de contêiner do Azure e você tiver implantado hello Azure votação aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c45ae-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="c45ae-106">Neste tutorial, parte 5 de sete, expansão compartimentos Olá no aplicativo hello e tente autoscaling pod.</span><span class="sxs-lookup"><span data-stu-id="c45ae-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="c45ae-107">Você também aprenderá como o número de saudação do tooscale de toochange de nós de agente de VM do Azure Olá capacidade do cluster para hospedar as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c45ae-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="c45ae-108">As tarefas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="c45ae-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c45ae-109">Dimensionamento manual de pods Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c45ae-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="c45ae-110">Configurando o dimensionamento automático compartimentos executando front-end de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="c45ae-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="c45ae-111">Expandir nós de agente do Azure Kubernetes Olá</span><span class="sxs-lookup"><span data-stu-id="c45ae-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="c45ae-112">Em tutoriais subsequentes, Olá aplicativo do Azure voto é atualizado e Operations Management Suite configurado o cluster de Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="c45ae-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c45ae-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c45ae-113">Before you begin</span></span>

<span data-ttu-id="c45ae-114">Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, esta imagem carregada tooAzure registro de contêiner e um cluster Kubernetes criado.</span><span class="sxs-lookup"><span data-stu-id="c45ae-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="c45ae-115">aplicativo Hello, em seguida, foi executado no cluster de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="c45ae-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="c45ae-116">Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar toohello [Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="c45ae-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="c45ae-117">No mínimo, este tutorial requer um cluster Kubernetes com um aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="c45ae-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="c45ae-118">Dimensionar pods manualmente</span><span class="sxs-lookup"><span data-stu-id="c45ae-118">Manually scale pods</span></span>

<span data-ttu-id="c45ae-119">Até agora, hello Azure voto front-end e a instância do Redis tem sido implantadas, cada um com uma única réplica.</span><span class="sxs-lookup"><span data-stu-id="c45ae-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="c45ae-120">tooverify, execute Olá [kubectl obter](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="c45ae-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="c45ae-121">Saída:</span><span class="sxs-lookup"><span data-stu-id="c45ae-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="c45ae-122">Alterar manualmente o número de saudação de compartimentos de saudação `azure-vote-front` implantação usando Olá [kubectl escala](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) comando.</span><span class="sxs-lookup"><span data-stu-id="c45ae-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="c45ae-123">Este exemplo aumenta too5 número hello.</span><span class="sxs-lookup"><span data-stu-id="c45ae-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="c45ae-124">Executar [kubectl obter compartimentos](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify que Kubernetes está criando compartimentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c45ae-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="c45ae-125">Após um minuto ou menos, compartimentos adicionais hello estão executando:</span><span class="sxs-lookup"><span data-stu-id="c45ae-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="c45ae-126">Saída:</span><span class="sxs-lookup"><span data-stu-id="c45ae-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="c45ae-127">Dimensionamento automático de pods</span><span class="sxs-lookup"><span data-stu-id="c45ae-127">Autoscale pods</span></span>

<span data-ttu-id="c45ae-128">Dá suporte a Kubernetes [autoscaling pod horizontal](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust número de saudação de compartimentos em uma implantação dependendo da utilização da CPU ou outros selecionar métricas.</span><span class="sxs-lookup"><span data-stu-id="c45ae-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="c45ae-129">toouse Olá autoscaler, seu compartimentos devem ter solicitações de CPU e os limites definidos.</span><span class="sxs-lookup"><span data-stu-id="c45ae-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="c45ae-130">Em Olá `azure-vote-front` implantação, Olá CPU de solicitações 0,25 contêiner front-end, com um limite de 0,5 CPU.</span><span class="sxs-lookup"><span data-stu-id="c45ae-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="c45ae-131">configurações de saudação se parecer com:</span><span class="sxs-lookup"><span data-stu-id="c45ae-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="c45ae-132">Olá, exemplo a seguir usa Olá [kubectl AutoEscala](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) tooautoscale Olá número de compartimentos de saudação do comando `azure-vote-front` implantação.</span><span class="sxs-lookup"><span data-stu-id="c45ae-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="c45ae-133">Aqui, se a utilização da CPU exceder 50%, Olá autoscaler aumenta Olá compartimentos tooa máximo, 10.</span><span class="sxs-lookup"><span data-stu-id="c45ae-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="c45ae-134">status de saudação toosee de autoscaler hello, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c45ae-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="c45ae-135">Saída:</span><span class="sxs-lookup"><span data-stu-id="c45ae-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="c45ae-136">Depois de alguns minutos, com carga mínima no aplicativo do Azure voto hello, número de saudação de réplicas pod diminui automaticamente too3.</span><span class="sxs-lookup"><span data-stu-id="c45ae-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="c45ae-137">Agentes de saudação de escala</span><span class="sxs-lookup"><span data-stu-id="c45ae-137">Scale hello agents</span></span>

<span data-ttu-id="c45ae-138">Se você criou seu cluster Kubernetes usando comandos padrão no tutorial anterior hello, ele tem três nós de agente.</span><span class="sxs-lookup"><span data-stu-id="c45ae-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="c45ae-139">Você pode ajustar o número de saudação de agentes manualmente se você planejar mais ou menos cargas de trabalho de contêiner no cluster.</span><span class="sxs-lookup"><span data-stu-id="c45ae-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="c45ae-140">Saudação de uso [az acs dimensionar](/cli/azure/acs#scale) de comando e especifique o número de saudação de agentes com hello `--new-agent-count` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c45ae-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="c45ae-141">Olá, exemplo a seguir aumenta o número de saudação do agente nós too4 Olá Kubernetes cluster denominado *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="c45ae-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="c45ae-142">comando Olá leva alguns minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c45ae-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="c45ae-143">Olá saída do comando mostra Olá número do agente de nós no valor de saudação do `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="c45ae-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="c45ae-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c45ae-144">Next steps</span></span>

<span data-ttu-id="c45ae-145">Neste tutorial, você usou diferentes recursos de colocação em escala em seu cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c45ae-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="c45ae-146">As tarefas abordadas incluíram:</span><span class="sxs-lookup"><span data-stu-id="c45ae-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c45ae-147">Dimensionamento manual de pods Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c45ae-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="c45ae-148">Configurando o dimensionamento automático compartimentos executando front-end de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="c45ae-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="c45ae-149">Expandir nós de agente do Azure Kubernetes Olá</span><span class="sxs-lookup"><span data-stu-id="c45ae-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="c45ae-150">Avançar toohello toolearn próximo de tutorial sobre como atualizar o aplicativo em Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c45ae-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c45ae-151">Atualizar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c45ae-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

