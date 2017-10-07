---
title: "aaaIntroduction tooAzure serviço de contêiner para Kubernetes | Microsoft Docs"
description: "Serviço de contêiner do Azure para Kubernetes torna toodeploy simple e gerenciar aplicativos de contêiner no Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, Contêineres, microsserviços, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="0a74a-104">Introdução tooAzure serviço de contêiner para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0a74a-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="0a74a-105">Serviço de contêiner do Azure para Kubernetes torna toocreate simple, configurar e gerenciar um cluster de máquinas virtuais que são pré-configurados toorun em contêineres de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0a74a-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="0a74a-106">Isso permite que você toouse suas habilidades existentes, ou exploram um corpo grande e crescente de experiência da comunidade, toodeploy e gerenciar aplicativos de contêiner no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0a74a-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="0a74a-107">Usando o serviço de contêiner do Azure, você pode tirar proveito da saudação recursos empresariais do Azure, enquanto mantém a portabilidade de aplicativo por meio de Kubernetes e Olá formato de imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="0a74a-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="0a74a-108">Usando o Serviço de Contêiner do Azure para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0a74a-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="0a74a-109">Nosso objetivo com o serviço de contêiner do Azure é tooprovide um ambiente de hospedagem de contêiner usando ferramentas de código-fonte aberto e tecnologias que são comuns entre os clientes hoje.</span><span class="sxs-lookup"><span data-stu-id="0a74a-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="0a74a-110">toothis final, expomos saudação padrão Kubernetes API os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="0a74a-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="0a74a-111">Ao usar esses pontos de extremidade padrão, você pode utilizar qualquer software que é capaz de se comunicando tooa Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="0a74a-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="0a74a-112">Por exemplo, você pode escolher [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), ou [draft](https://github.com/Azure/draft).</span><span class="sxs-lookup"><span data-stu-id="0a74a-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="0a74a-113">Criando um Cluster Kubernetes usando o Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="0a74a-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="0a74a-114">toobegin usando o serviço de contêiner do Azure, implantar um cluster do serviço de contêiner do Azure com hello [2.0 do CLI do Azure](container-service-kubernetes-walkthrough.md) ou por meio do portal hello (Olá pesquisa Marketplace para **serviço de contêiner do Azure**).</span><span class="sxs-lookup"><span data-stu-id="0a74a-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="0a74a-115">Se você for um usuário avançado que precisa de mais controle sobre modelos do hello Azure Resource Manager, você pode usar o código-fonte aberto Olá [acs mecanismo](https://github.com/Azure/acs-engine) toobuild projeto seus próprios Kubernetes personalizados do cluster e implantá-lo por meio de saudação `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="0a74a-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="0a74a-116">Como usar Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0a74a-116">Using Kubernetes</span></span>
<span data-ttu-id="0a74a-117">O Kubernetes automatiza a implantação, o dimensionamento e o gerenciamento de aplicativos em contêineres.</span><span class="sxs-lookup"><span data-stu-id="0a74a-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="0a74a-118">Ele tem um conjunto avançado de recursos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="0a74a-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="0a74a-119">Binpacking automático</span><span class="sxs-lookup"><span data-stu-id="0a74a-119">Automatic binpacking</span></span>
* <span data-ttu-id="0a74a-120">Autorrecuperação</span><span class="sxs-lookup"><span data-stu-id="0a74a-120">Self-healing</span></span>
* <span data-ttu-id="0a74a-121">Dimensionamento em escala horizontal</span><span class="sxs-lookup"><span data-stu-id="0a74a-121">Horizontal scaling</span></span>
* <span data-ttu-id="0a74a-122">Descoberta de serviço e balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="0a74a-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="0a74a-123">Reversões e distribuições automatizadas</span><span class="sxs-lookup"><span data-stu-id="0a74a-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="0a74a-124">Segredos e gerenciamento de configuração</span><span class="sxs-lookup"><span data-stu-id="0a74a-124">Secret and configuration management</span></span>
* <span data-ttu-id="0a74a-125">Orquestração de armazenamento</span><span class="sxs-lookup"><span data-stu-id="0a74a-125">Storage orchestration</span></span>
* <span data-ttu-id="0a74a-126">Execução do Lote</span><span class="sxs-lookup"><span data-stu-id="0a74a-126">Batch execution</span></span>

<span data-ttu-id="0a74a-127">Diagrama da arquitetura de Kubernetes implantado por meio do Serviço de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="0a74a-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Serviço de contêiner do Azure configurado toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="0a74a-129">Vídeos</span><span class="sxs-lookup"><span data-stu-id="0a74a-129">Videos</span></span>

<span data-ttu-id="0a74a-130">Suporte a Kubernetes nos Serviços de Contêiner do Azure (Azure Friday, janeiro de 2017):</span><span class="sxs-lookup"><span data-stu-id="0a74a-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="0a74a-131">Ferramentas para desenvolver e implantar aplicativos no Kubernetes (Azure OpenDev, junho de 2017):</span><span class="sxs-lookup"><span data-stu-id="0a74a-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="0a74a-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a74a-132">Next steps</span></span>

<span data-ttu-id="0a74a-133">Explorar Olá [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin Explorando o serviço de contêiner do Azure hoje.</span><span class="sxs-lookup"><span data-stu-id="0a74a-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
