---
title: Monitorar cluster Kubernetes do Azure - Sysdig | Microsoft Docs
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
ms.openlocfilehash: afe22b84015526f901111238e36baaa94694ccbf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="1906a-103">Monitorar um cluster Kubernetes do Serviço de Contêiner do Azure usando Sysdig</span><span class="sxs-lookup"><span data-stu-id="1906a-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1906a-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1906a-104">Prerequisites</span></span>
<span data-ttu-id="1906a-105">Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1906a-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="1906a-106">Isso também pressupõe que você tenha as ferramentas cli e kubectl do Azure instaladas.</span><span class="sxs-lookup"><span data-stu-id="1906a-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="1906a-107">Você pode testar se tem a ferramenta `az` instalada executando:</span><span class="sxs-lookup"><span data-stu-id="1906a-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="1906a-108">Se você não tem a ferramenta `az` instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="1906a-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="1906a-109">Você pode testar se tem a ferramenta `kubectl` instalada executando:</span><span class="sxs-lookup"><span data-stu-id="1906a-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="1906a-110">Se não tem `kubectl` instalado, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="1906a-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="1906a-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="1906a-111">Sysdig</span></span>
<span data-ttu-id="1906a-112">O Sysdig é um monitoramento externo como uma empresa de serviço que pode monitorar contêineres no cluster Kubernetes em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="1906a-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="1906a-113">O uso do Sysdig requer uma conta ativa do Sysdig.</span><span class="sxs-lookup"><span data-stu-id="1906a-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="1906a-114">Você pode se inscrever para uma conta no [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="1906a-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="1906a-115">Quando estiver conectado ao site de nuvem de Sysdig, clique em seu nome de usuário e, na página, você deverá ver a "Chave de acesso".</span><span class="sxs-lookup"><span data-stu-id="1906a-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Chave de API d Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="1906a-117">Instalação dos agentes do Sysdig para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1906a-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="1906a-118">Para monitorar seus contêineres, o Sysdig executa um processo em cada computador usando um `DaemonSet` Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1906a-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="1906a-119">Os DaemonSets são objetos da API do Kubernetes que executam uma única instância de um contêiner por computador.</span><span class="sxs-lookup"><span data-stu-id="1906a-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="1906a-120">Eles são perfeitos para instalar ferramentas como o agente de monitoramento do Sysdig.</span><span class="sxs-lookup"><span data-stu-id="1906a-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="1906a-121">Para instalar o daemonset Sysdig, você deve primeiro baixar [o modelo](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) de sysdig.</span><span class="sxs-lookup"><span data-stu-id="1906a-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="1906a-122">Salve esse arquivo como `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="1906a-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="1906a-123">No Linux e no OS X, você pode executar:</span><span class="sxs-lookup"><span data-stu-id="1906a-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="1906a-124">No PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1906a-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="1906a-125">Em seguida, edite esse arquivo para inserir sua chave de acesso que você adquiriu da sua conta de Sysdig.</span><span class="sxs-lookup"><span data-stu-id="1906a-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="1906a-126">Por fim, crie o DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="1906a-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="1906a-127">Exibir o monitoramento</span><span class="sxs-lookup"><span data-stu-id="1906a-127">View your monitoring</span></span>
<span data-ttu-id="1906a-128">Depois de instalados e em execução, os agentes devem bombear os dados de volta ao Sysdig.</span><span class="sxs-lookup"><span data-stu-id="1906a-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="1906a-129">Volte para o [painel sysdig](https://app.sysdigcloud.com) e você verá informações sobre seus contêineres.</span><span class="sxs-lookup"><span data-stu-id="1906a-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="1906a-130">Você também pode instalar painéis específicos do Kubernetes por meio do [assistente de novo painel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="1906a-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
