---
title: cluster do Azure Kubernetes aaaMonitor - Sysdig | Microsoft Docs
description: "Monitoramento do cluster Kubernetes no Serviço de Contêiner do Azure usando Sysdig"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="55026-103">Monitorar um cluster Kubernetes do Serviço de Contêiner do Azure usando Sysdig</span><span class="sxs-lookup"><span data-stu-id="55026-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55026-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="55026-104">Prerequisites</span></span>
<span data-ttu-id="55026-105">Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="55026-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="55026-106">Ele também pressupõe que você tenha ferramentas de cli e kubectl de saudação do azure instaladas.</span><span class="sxs-lookup"><span data-stu-id="55026-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="55026-107">Você pode testar se você tiver Olá `az` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="55026-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="55026-108">Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="55026-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="55026-109">Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:</span><span class="sxs-lookup"><span data-stu-id="55026-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="55026-110">Se não tem `kubectl` instalado, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="55026-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="55026-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="55026-111">Sysdig</span></span>
<span data-ttu-id="55026-112">O Sysdig é um monitoramento externo como uma empresa de serviço que pode monitorar contêineres no cluster Kubernetes em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="55026-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="55026-113">O uso do Sysdig requer uma conta ativa do Sysdig.</span><span class="sxs-lookup"><span data-stu-id="55026-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="55026-114">Você pode se inscrever para uma conta no [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="55026-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="55026-115">Depois de entrar no site de nuvem Sysdig toohello, clique em seu nome de usuário e na página hello, você verá sua "chave de acesso".</span><span class="sxs-lookup"><span data-stu-id="55026-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Chave de API d Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="55026-117">Instalando Olá Sysdig agentes tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="55026-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="55026-118">toomonitor seus contêineres, execuções de Sysdig um processo em cada computador usando um Kubernetes `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="55026-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="55026-119">Os DaemonSets são objetos da API do Kubernetes que executam uma única instância de um contêiner por computador.</span><span class="sxs-lookup"><span data-stu-id="55026-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="55026-120">Eles são perfeitos para instalar ferramentas como Olá agente de monitoramento do Sysdig.</span><span class="sxs-lookup"><span data-stu-id="55026-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="55026-121">tooinstall Olá Sysdig daemonset, você deve primeiro baixar [modelo Olá](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) de sysdig.</span><span class="sxs-lookup"><span data-stu-id="55026-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="55026-122">Salve esse arquivo como `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="55026-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="55026-123">No Linux e no OS X, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="55026-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="55026-124">No PowerShell:</span><span class="sxs-lookup"><span data-stu-id="55026-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="55026-125">Em seguida edite sua chave de acesso que você obteve da sua conta Sysdig tooinsert esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="55026-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="55026-126">Finalmente, crie Olá DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="55026-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="55026-127">Exibir o monitoramento</span><span class="sxs-lookup"><span data-stu-id="55026-127">View your monitoring</span></span>
<span data-ttu-id="55026-128">Depois de instalado e em execução, os agentes de saudação devem bomba tooSysdig de backup de dados.</span><span class="sxs-lookup"><span data-stu-id="55026-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="55026-129">Voltar toothe [sysdig painel](https://app.sysdigcloud.com) e você deverá ver informações sobre os contêineres.</span><span class="sxs-lookup"><span data-stu-id="55026-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="55026-130">Você também pode instalar painéis específicos do Kubernetes por meio do [assistente de novo painel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="55026-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
