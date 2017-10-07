---
title: "tutorial de serviço de contêiner aaaAzure - Monitor Kubernetes | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – monitorar o Kubernetes com o OMS (Microsoft Operations Management Suite)"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="3142d-104">Monitorar um cluster do Kubernetes com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3142d-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="3142d-105">Monitorar seu cluster do Kubernetes e os contêineres é fundamental, principalmente ao gerenciar um cluster de produção em grande escala com vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3142d-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="3142d-106">Você pode usufruir de várias soluções de monitoramento do Kubernetes, da Microsoft ou de outros provedores.</span><span class="sxs-lookup"><span data-stu-id="3142d-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="3142d-107">Neste tutorial, você deve monitorar seu cluster Kubernetes usando a solução de contêineres de saudação em [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), solução de gerenciamento de TI baseada em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3142d-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="3142d-108">(Olá solução do OMS contêineres está na visualização).</span><span class="sxs-lookup"><span data-stu-id="3142d-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="3142d-109">Este tutorial, parte sete de sete, aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3142d-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3142d-110">Obter configurações de espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="3142d-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="3142d-111">Configurar agentes do OMS em nós de Kubernetes Olá</span><span class="sxs-lookup"><span data-stu-id="3142d-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="3142d-112">Acesso a informações de monitoramento no portal do OMS hello ou o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3142d-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3142d-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3142d-113">Before you begin</span></span>

<span data-ttu-id="3142d-114">Nos tutoriais anteriores, um aplicativo foi empacotado em imagens de contêiner, essas imagens carregadas tooAzure registro de contêiner e um cluster Kubernetes criado.</span><span class="sxs-lookup"><span data-stu-id="3142d-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="3142d-115">Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="3142d-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="3142d-116">No mínimo, este tutorial requer um cluster do Kubernetes com nós de agente do Linux e uma conta do OMS (Operations Management Suite).</span><span class="sxs-lookup"><span data-stu-id="3142d-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="3142d-117">Se necessário, inscreva-se em uma [avaliação gratuita do OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="3142d-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="3142d-118">Obter configurações de espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="3142d-118">Get Workspace settings</span></span>

<span data-ttu-id="3142d-119">Quando você pode acessar Olá [portal do OMS](https://mms.microsoft.com), ir muito**configurações** > **fontes conectadas** > **servidores Linux**.</span><span class="sxs-lookup"><span data-stu-id="3142d-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="3142d-120">Lá, você pode encontrar hello *ID do espaço de trabalho* e um primário ou secundário *chave do espaço de trabalho*.</span><span class="sxs-lookup"><span data-stu-id="3142d-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="3142d-121">Anote esses valores, que é necessário tooset agentes do OMS no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3142d-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="3142d-122">Configurar agentes do OMS</span><span class="sxs-lookup"><span data-stu-id="3142d-122">Set up OMS agents</span></span>

<span data-ttu-id="3142d-123">Aqui está um tooset de arquivo YAML agentes do OMS em nós de cluster Olá Linux.</span><span class="sxs-lookup"><span data-stu-id="3142d-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="3142d-124">Ele cria um [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) do Kubernetes, que executa um único pod idêntico em cada nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="3142d-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="3142d-125">Olá DaemonSet recurso é ideal para a implantação de um agente de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3142d-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="3142d-126">Salvar Olá seguir chamado o arquivo de texto tooa `oms-daemonset.yaml`e substitua os valores de espaço reservado Olá para *myWorkspaceID* e *myWorkspaceKey* com a ID do espaço de trabalho do OMS e a chave.</span><span class="sxs-lookup"><span data-stu-id="3142d-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="3142d-127">(Em produção, você pode codificar esses valores como segredos).</span><span class="sxs-lookup"><span data-stu-id="3142d-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="3142d-128">Crie hello DaemonSet com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3142d-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="3142d-129">toosee que Olá DaemonSet é criado, execute:</span><span class="sxs-lookup"><span data-stu-id="3142d-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="3142d-130">O resultado é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="3142d-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="3142d-131">Depois que estiver executando agentes hello, leva vários minutos para OMS tooingest e processar Olá dados.</span><span class="sxs-lookup"><span data-stu-id="3142d-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="3142d-132">Acessar dados de monitoramento</span><span class="sxs-lookup"><span data-stu-id="3142d-132">Access monitoring data</span></span>

<span data-ttu-id="3142d-133">Exibir e analisar o contêiner OMS Olá dados de monitoramento com hello [solução contêiner](../../log-analytics/log-analytics-containers.md) no portal do OMS hello ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3142d-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="3142d-134">solução de contêiner de saudação tooinstall usando Olá [portal do OMS](https://mms.microsoft.com), ir muito**Galeria de soluções**.</span><span class="sxs-lookup"><span data-stu-id="3142d-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="3142d-135">Em seguida, adicione a **solução Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="3142d-135">Then add **Container Solution**.</span></span> <span data-ttu-id="3142d-136">Como alternativa, adicionar a solução de contêineres de saudação do hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="3142d-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="3142d-137">No portal do OMS hello, procure uma **contêineres** quadro de resumo no painel do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="3142d-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="3142d-138">Clique em bloco de saudação para detalhes, incluindo: eventos de contêiner, erros, status, inventário de imagem e uso da CPU e memória.</span><span class="sxs-lookup"><span data-stu-id="3142d-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="3142d-139">Para obter informações mais detalhadas, clique em uma linha em qualquer bloco ou execute uma [pesquisa de logs](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="3142d-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Painel de contêineres no portal do OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="3142d-141">Da mesma forma, no hello portal do Azure, vá muito**análise de Log** e selecione o nome do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3142d-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="3142d-142">Olá toosee **contêineres** quadro de resumo, clique em **soluções** > **contêineres**.</span><span class="sxs-lookup"><span data-stu-id="3142d-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="3142d-143">toosee detalhes, clique em bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="3142d-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="3142d-144">Consulte Olá [documentação do Azure Log Analytics](../../log-analytics/index.md) para obter orientações detalhadas sobre consultar e analisar dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3142d-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3142d-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3142d-145">Next steps</span></span>

<span data-ttu-id="3142d-146">Neste tutorial, você monitorou o cluster do Kubernetes com o OMS.</span><span class="sxs-lookup"><span data-stu-id="3142d-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="3142d-147">As tarefas abordadas incluíram:</span><span class="sxs-lookup"><span data-stu-id="3142d-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3142d-148">Obter configurações de espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="3142d-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="3142d-149">Configurar agentes do OMS em nós de Kubernetes Olá</span><span class="sxs-lookup"><span data-stu-id="3142d-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="3142d-150">Acesso a informações de monitoramento no portal do OMS hello ou o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3142d-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="3142d-151">Siga este toosee link pré-criadas exemplos de script para o serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="3142d-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3142d-152">Exemplos de script do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="3142d-152">Azure Container Service script samples</span></span>](cli-samples.md)
