---
title: "Tutorial do Serviço de Contêiner do Azure – monitorar o Kubernetes | Microsoft Docs"
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
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="3c346-104">Monitorar um cluster do Kubernetes com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3c346-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="3c346-105">Monitorar seu cluster do Kubernetes e os contêineres é fundamental, principalmente ao gerenciar um cluster de produção em grande escala com vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3c346-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="3c346-106">Você pode usufruir de várias soluções de monitoramento do Kubernetes, da Microsoft ou de outros provedores.</span><span class="sxs-lookup"><span data-stu-id="3c346-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="3c346-107">Neste tutorial, você deve monitorar Contêineres no [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), a solução de gerenciamento de TI baseada em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c346-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="3c346-108">(A solução Contêineres do OMS está na versão prévia).</span><span class="sxs-lookup"><span data-stu-id="3c346-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="3c346-109">Este tutorial, parte sete de sete, aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="3c346-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c346-110">Obter configurações de espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="3c346-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="3c346-111">Configurar agentes do OMS nos nós do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3c346-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="3c346-112">Acessar informações de monitoramento no portal do OMS ou no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c346-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3c346-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3c346-113">Before you begin</span></span>

<span data-ttu-id="3c346-114">Nos tutoriais anteriores, um aplicativo foi empacotado em um cluster de contêiner, essas imagens foram carregadas no Registro de Contêiner do Azure e um cluster do Kubernetes foi criado.</span><span class="sxs-lookup"><span data-stu-id="3c346-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="3c346-115">Se você ainda não realizou essas etapas e deseja continuar acompanhando, retorne ao [Tutorial 1 – Criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="3c346-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="3c346-116">No mínimo, este tutorial requer um cluster do Kubernetes com nós de agente do Linux e uma conta do OMS (Operations Management Suite).</span><span class="sxs-lookup"><span data-stu-id="3c346-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="3c346-117">Se necessário, inscreva-se em uma [avaliação gratuita do OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="3c346-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="3c346-118">Obter configurações de espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="3c346-118">Get Workspace settings</span></span>

<span data-ttu-id="3c346-119">Quando você puder acessar o [portal do OMS](https://mms.microsoft.com), acesse **Configurações** > **Fontes Conectadas** > **Servidores Linux**.</span><span class="sxs-lookup"><span data-stu-id="3c346-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="3c346-120">Lá, você poderá encontrar a *ID do Espaço de Trabalho* e uma *Chave do Espaço de Trabalho* primária ou secundária.</span><span class="sxs-lookup"><span data-stu-id="3c346-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="3c346-121">Anote esses valores, que serão necessários para configurar os agentes do OMS no cluster.</span><span class="sxs-lookup"><span data-stu-id="3c346-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="3c346-122">Configurar agentes do OMS</span><span class="sxs-lookup"><span data-stu-id="3c346-122">Set up OMS agents</span></span>

<span data-ttu-id="3c346-123">Aqui está um arquivo YAML para configurar agentes do OMS em nós de cluster do Linux.</span><span class="sxs-lookup"><span data-stu-id="3c346-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="3c346-124">Ele cria um [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) do Kubernetes, que executa um único pod idêntico em cada nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="3c346-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="3c346-125">O recurso DaemonSet é ideal para a implantação de um agente de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3c346-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="3c346-126">Salve o texto a seguir em um arquivo chamado `oms-daemonset.yaml` e substitua os valores de espaço reservado *myWorkspaceID* e *myWorkspaceKey* pela ID e a chave do espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="3c346-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="3c346-127">(Em produção, você pode codificar esses valores como segredos).</span><span class="sxs-lookup"><span data-stu-id="3c346-127">(In production, you can encode these values as secrets.)</span></span>

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

<span data-ttu-id="3c346-128">Crie o DaemonSet com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3c346-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="3c346-129">Para ver se o DaemonSet foi criado, execute:</span><span class="sxs-lookup"><span data-stu-id="3c346-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="3c346-130">A saída deverá ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="3c346-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="3c346-131">Depois que os agentes estiverem em execução, levará vários minutos para que o OMS ingira e processe os dados.</span><span class="sxs-lookup"><span data-stu-id="3c346-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="3c346-132">Acessar dados de monitoramento</span><span class="sxs-lookup"><span data-stu-id="3c346-132">Access monitoring data</span></span>

<span data-ttu-id="3c346-133">Exiba e analise os dados de monitoramento com o contêiner do OMS com a [solução Contêiner](../../log-analytics/log-analytics-containers.md) no portal do OMS ou no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c346-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="3c346-134">Para instalar a solução Contêiner usando o [portal do OMS](https://mms.microsoft.com), acesse a **Galeria de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="3c346-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="3c346-135">Em seguida, adicione a **solução Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="3c346-135">Then add **Container Solution**.</span></span> <span data-ttu-id="3c346-136">Como alternativa, adicione a solução Contêineres por meio do [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="3c346-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="3c346-137">No portal do OMS, procure um bloco de resumo **Contêineres** no painel do OMS.</span><span class="sxs-lookup"><span data-stu-id="3c346-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="3c346-138">Clique no bloco para obter detalhes, incluindo: eventos de contêiner, erros, status, inventário de imagem e uso da CPU e de memória.</span><span class="sxs-lookup"><span data-stu-id="3c346-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="3c346-139">Para obter informações mais detalhadas, clique em uma linha em qualquer bloco ou execute uma [pesquisa de logs](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="3c346-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Painel de contêineres no portal do OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="3c346-141">Da mesma forma, no portal do Azure, acesse o **Log Analytics** e selecione o nome do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3c346-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="3c346-142">Para ver o bloco de resumo **Contêineres** clique em **Soluções** > **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="3c346-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="3c346-143">Para ver os detalhes, clique no bloco.</span><span class="sxs-lookup"><span data-stu-id="3c346-143">To see details, click the tile.</span></span>

<span data-ttu-id="3c346-144">Consulte a [documentação do Azure Log Analytics](../../log-analytics/index.md) para obter orientações detalhadas de como consultar e analisar dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="3c346-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c346-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c346-145">Next steps</span></span>

<span data-ttu-id="3c346-146">Neste tutorial, você monitorou o cluster do Kubernetes com o OMS.</span><span class="sxs-lookup"><span data-stu-id="3c346-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="3c346-147">As tarefas abordadas incluíram:</span><span class="sxs-lookup"><span data-stu-id="3c346-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c346-148">Obter configurações de espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="3c346-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="3c346-149">Configurar agentes do OMS nos nós do Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3c346-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="3c346-150">Acessar informações de monitoramento no portal do OMS ou no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c346-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="3c346-151">Siga este link para ver exemplos de scripts criados previamente para o Serviço de Contêiner.</span><span class="sxs-lookup"><span data-stu-id="3c346-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c346-152">Exemplos de script do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="3c346-152">Azure Container Service script samples</span></span>](cli-samples.md)
