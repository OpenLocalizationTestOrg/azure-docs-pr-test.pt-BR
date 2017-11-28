---
title: aaaMonitor Kubernetes Azure cluster com Datadog | Microsoft Docs
description: "Monitorando o cluster Kubernetes no Serviço de Contêiner do Azure usando o DataDog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="08552-103">Monitorar um cluster do Serviço de Contêiner do Azure com o Datadog</span><span class="sxs-lookup"><span data-stu-id="08552-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08552-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08552-104">Prerequisites</span></span>
<span data-ttu-id="08552-105">Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="08552-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="08552-106">Ele também pressupõe que você tenha Olá `az` cli do Azure e `kubectl` ferramentas instaladas.</span><span class="sxs-lookup"><span data-stu-id="08552-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="08552-107">Você pode testar se você tiver Olá `az` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="08552-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="08552-108">Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="08552-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="08552-109">Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="08552-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="08552-110">Se não tem `kubectl` instalado, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="08552-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="08552-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="08552-111">DataDog</span></span>
<span data-ttu-id="08552-112">O Datadog é um serviço de monitoramento que reúne dados de monitoramento de seus contêineres em seu cluster do Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="08552-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="08552-113">O Datadog tem um Painel de Integração do Docker, onde você pode ver as métricas específicas em seus contêineres.</span><span class="sxs-lookup"><span data-stu-id="08552-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="08552-114">As métricas obtidas de seus contêineres são organizadas por CPU, Memória, Rede e E/S.</span><span class="sxs-lookup"><span data-stu-id="08552-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="08552-115">O Datadog divide as métricas em contêineres e em imagens.</span><span class="sxs-lookup"><span data-stu-id="08552-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="08552-116">É necessário primeiro muito[criar uma conta](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="08552-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="08552-117">Instalando Olá Datadog Agent com um DaemonSet</span><span class="sxs-lookup"><span data-stu-id="08552-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="08552-118">DaemonSets são usados por Kubernetes toorun uma única instância de um contêiner em cada host no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="08552-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="08552-119">Eles são perfeitos para a execução de agentes de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="08552-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="08552-120">Depois de fazer logon em Datadog, você pode seguir Olá [Datadog instruções](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agentes no seu cluster usando um DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="08552-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="08552-121">Conclusão</span><span class="sxs-lookup"><span data-stu-id="08552-121">Conclusion</span></span>
<span data-ttu-id="08552-122">É isso!</span><span class="sxs-lookup"><span data-stu-id="08552-122">That's it!</span></span> <span data-ttu-id="08552-123">Depois que os agentes de saudação estão funcionando e em execução, você deve ver os dados no console de saudação em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="08552-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="08552-124">Você pode visitar Olá integrado [kubernetes painel](https://app.datadoghq.com/screen/integration/kubernetes) toosee um resumo do cluster.</span><span class="sxs-lookup"><span data-stu-id="08552-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
