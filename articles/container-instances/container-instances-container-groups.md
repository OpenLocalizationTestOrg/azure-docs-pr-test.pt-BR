---
title: "Grupos de contêineres das Instâncias de Contêiner do Azure"
description: "Entenda como funcionam os grupos de contêineres em Instâncias de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="396f6-103">Grupos de contêineres em Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="396f6-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="396f6-104">O recurso de nível superior em Instâncias de Contêiner do Azure é um grupo de contêiner.</span><span class="sxs-lookup"><span data-stu-id="396f6-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="396f6-105">Este artigo descreve quais são os grupos de contêineres e quais tipos de cenários que eles permitem.</span><span class="sxs-lookup"><span data-stu-id="396f6-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="396f6-106">Como um grupo de contêineres funciona</span><span class="sxs-lookup"><span data-stu-id="396f6-106">How a container group works</span></span>

<span data-ttu-id="396f6-107">Um grupo de contêineres é uma coleção de contêineres que são agendados no mesmo computador host e compartilham um ciclo de vida, uma rede local e volumes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="396f6-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="396f6-108">Ele é semelhante ao conceito de um *pod* no [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) e [DC/SO](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="396f6-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="396f6-109">O diagrama a seguir mostra um exemplo de um grupo de contêineres que inclui vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="396f6-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![Exemplo de grupos de contêineres][container-groups-example]

<span data-ttu-id="396f6-111">Observe que:</span><span class="sxs-lookup"><span data-stu-id="396f6-111">Note that:</span></span>

- <span data-ttu-id="396f6-112">O grupo está agendado em um único computador host.</span><span class="sxs-lookup"><span data-stu-id="396f6-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="396f6-113">O grupo expõe um único endereço IP público, com uma porta exposta.</span><span class="sxs-lookup"><span data-stu-id="396f6-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="396f6-114">O grupo é composto por dois contêineres.</span><span class="sxs-lookup"><span data-stu-id="396f6-114">The group is made up of two containers.</span></span> <span data-ttu-id="396f6-115">Um contêiner escuta na porta 80, enquanto o outro escuta na porta 5000.</span><span class="sxs-lookup"><span data-stu-id="396f6-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="396f6-116">O grupo inclui dois compartilhamentos de arquivos do Azure como montagens de volume e cada contêiner monta um dos compartilhamentos localmente.</span><span class="sxs-lookup"><span data-stu-id="396f6-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="396f6-117">Rede</span><span class="sxs-lookup"><span data-stu-id="396f6-117">Networking</span></span>

<span data-ttu-id="396f6-118">Grupos de contêineres compartilham um endereço IP e um namespace de porta nesse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="396f6-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="396f6-119">Para permitir que clientes externos alcancem um contêiner dentro do grupo, você deve expor a porta no endereço IP e do contêiner.</span><span class="sxs-lookup"><span data-stu-id="396f6-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="396f6-120">Já que contêineres dentro do grupo compartilham um namespace de porta, não há suporte para mapeamento de porta.</span><span class="sxs-lookup"><span data-stu-id="396f6-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="396f6-121">Contêineres dentro de um grupo podem acessar uns aos outros por meio de localhost nas portas que eles têm expostos, mesmo se essas portas não estão expostas externamente no endereço IP do grupo.</span><span class="sxs-lookup"><span data-stu-id="396f6-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="396f6-122">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="396f6-122">Storage</span></span>

<span data-ttu-id="396f6-123">Você pode especificar volumes externos para montar dentro de um grupo de contêineres.</span><span class="sxs-lookup"><span data-stu-id="396f6-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="396f6-124">Você pode mapear os volumes para caminhos específicos dentro dos contêineres individuais em um grupo.</span><span class="sxs-lookup"><span data-stu-id="396f6-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="396f6-125">Cenários comuns</span><span class="sxs-lookup"><span data-stu-id="396f6-125">Common scenarios</span></span>

<span data-ttu-id="396f6-126">Grupos de vários contêineres são úteis em casos nos quais você deseja dividir uma única tarefa funcional em um pequeno número de imagens de contêiner, que podem ser entregues por equipes diferentes e têm requisitos de recursos separados.</span><span class="sxs-lookup"><span data-stu-id="396f6-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="396f6-127">Os exemplos de uso podem incluir:</span><span class="sxs-lookup"><span data-stu-id="396f6-127">Example usage could include:</span></span>

- <span data-ttu-id="396f6-128">Um contêiner de aplicativo e um contêiner de log.</span><span class="sxs-lookup"><span data-stu-id="396f6-128">An application container and a logging container.</span></span> <span data-ttu-id="396f6-129">O contêiner de log coleta logs e métricas de saída do aplicativo principal e grava-as em armazenamento de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="396f6-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="396f6-130">Um aplicativo e um contêiner de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="396f6-130">An application and a monitoring container.</span></span> <span data-ttu-id="396f6-131">O contêiner de monitoramento faz uma solicitação periodicamente para o aplicativo para garantir que ele esteja em execução e respondendo corretamente e emite um alerta em caso negativo.</span><span class="sxs-lookup"><span data-stu-id="396f6-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="396f6-132">Um contêiner que atende a um aplicativo Web e um contêiner efetuando pull do conteúdo mais recente do controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="396f6-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="396f6-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="396f6-133">Next steps</span></span>

<span data-ttu-id="396f6-134">Saiba como [implantar um grupo de vários contêineres](container-instances-multi-container-group.md) com um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="396f6-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png