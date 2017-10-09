---
title: aaaMonitor Kubernetes um Azure cluster com CoScale | Microsoft Docs
description: "Monitorar um cluster Kubernetes no Serviço de Contêiner do Azure usando CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="6fd87-103">Monitorar um cluster Kubernetes do Serviço de Contêiner do Azure usando CoScale</span><span class="sxs-lookup"><span data-stu-id="6fd87-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="6fd87-104">Neste artigo, mostramos como Olá toodeploy [CoScale](https://www.coscale.com/) toomonitor agente todos os nós e contêineres em sua Kubernetes de cluster no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd87-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="6fd87-105">Você precisa de uma conta com CoScale para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="6fd87-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="6fd87-106">Sobre o CoScale</span><span class="sxs-lookup"><span data-stu-id="6fd87-106">About CoScale</span></span> 

<span data-ttu-id="6fd87-107">CoScale é uma plataforma de monitoramento que reúne as métricas e eventos de todos os contêineres em várias plataformas de orquestração.</span><span class="sxs-lookup"><span data-stu-id="6fd87-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="6fd87-108">CoScale oferece monitoramento de pilha completa para ambientes Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6fd87-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="6fd87-109">Ele fornece visualizações e análise para todas as camadas na pilha de saudação: Olá SO, Kubernetes, Docker e aplicativos em execução dentro de seus contêineres.</span><span class="sxs-lookup"><span data-stu-id="6fd87-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="6fd87-110">CoScale oferece vários painéis de monitoramentos internos e ele tem operadores de tooallow de detecção de anomalias internos e rápida de problemas de infraestrutura e aplicativo toofind desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="6fd87-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![Interface do usuário do CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="6fd87-112">Conforme mostrado neste artigo, você pode instalar agentes em um cluster de Kubernetes toorun CoScale como uma solução de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6fd87-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="6fd87-113">Se desejar tookeep seus dados no local, CoScale também está disponível para instalação no local.</span><span class="sxs-lookup"><span data-stu-id="6fd87-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6fd87-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6fd87-114">Prerequisites</span></span>

<span data-ttu-id="6fd87-115">É necessário primeiro muito[criar uma conta de CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="6fd87-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="6fd87-116">Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="6fd87-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="6fd87-117">Ele também pressupõe que você tenha Olá `az` CLI do Azure e `kubectl` ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="6fd87-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="6fd87-118">Você pode testar se você tiver Olá `az` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="6fd87-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="6fd87-119">Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6fd87-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="6fd87-120">Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="6fd87-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="6fd87-121">Se não tem `kubectl` instalado, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="6fd87-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="6fd87-122">Instalando o agente de CoScale Olá com um DaemonSet</span><span class="sxs-lookup"><span data-stu-id="6fd87-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="6fd87-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) são usado por Kubernetes toorun uma única instância de um contêiner em cada host no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fd87-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="6fd87-124">Eles são perfeitos para a execução de agentes de monitoramento, como o agente de CoScale hello.</span><span class="sxs-lookup"><span data-stu-id="6fd87-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="6fd87-125">Depois de efetuar login tooCoScale, vá toohello [página agente](https://app.coscale.com/) agentes de CoScale tooinstall no seu cluster usando um DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="6fd87-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="6fd87-126">Olá CoScale da interface do usuário fornece configuração interativa etapas toocreate um agente e iniciar a monitoração do seu cluster Kubernetes concluída.</span><span class="sxs-lookup"><span data-stu-id="6fd87-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configuração do agente do CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="6fd87-128">Agente de saudação toostart no cluster hello, execute o comando de saudação fornecido:</span><span class="sxs-lookup"><span data-stu-id="6fd87-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Iniciar o agente de CoScale Olá](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="6fd87-130">É isso!</span><span class="sxs-lookup"><span data-stu-id="6fd87-130">That's it!</span></span> <span data-ttu-id="6fd87-131">Quando agentes Olá estão em funcionamento, você deverá ver dados no console de saudação em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="6fd87-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="6fd87-132">Visite Olá [página agente](https://app.coscale.com/) toosee um resumo do cluster, execute etapas adicionais de configuração e ver painéis como Olá **Kubernetes visão geral do cluster**.</span><span class="sxs-lookup"><span data-stu-id="6fd87-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Visão geral do cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="6fd87-134">Agente de CoScale Olá automaticamente é implantado em novas máquinas no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fd87-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="6fd87-135">atualizações de agente Olá automaticamente quando uma nova versão for lançada.</span><span class="sxs-lookup"><span data-stu-id="6fd87-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6fd87-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fd87-136">Next steps</span></span>

<span data-ttu-id="6fd87-137">Consulte Olá [CoScale documentação](http://docs.coscale.com/) e [blog](https://www.coscale.com/blog) para obter mais informações sobre CoScale soluções de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="6fd87-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

