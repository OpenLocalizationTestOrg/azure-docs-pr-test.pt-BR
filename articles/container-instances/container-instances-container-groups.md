---
title: "aaaAzure grupos de contêineres de instâncias de contêiner"
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
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="46bad-103">Grupos de contêineres em Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="46bad-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="46bad-104">o recurso de nível superior Olá em instâncias de contêiner do Azure é um grupo de contêiner.</span><span class="sxs-lookup"><span data-stu-id="46bad-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="46bad-105">Este artigo descreve quais são os grupos de contêineres e quais tipos de cenários que eles permitem.</span><span class="sxs-lookup"><span data-stu-id="46bad-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="46bad-106">Como um grupo de contêineres funciona</span><span class="sxs-lookup"><span data-stu-id="46bad-106">How a container group works</span></span>

<span data-ttu-id="46bad-107">Um contêiner de grupo é uma coleção de contêineres que seja agendados em Olá mesmo host de máquina e compartilhar um ciclo de vida, a rede local e volumes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46bad-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="46bad-108">É o conceito de toohello semelhantes de um *pod* na [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) e [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span><span class="sxs-lookup"><span data-stu-id="46bad-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="46bad-109">Olá diagrama a seguir mostra um exemplo de um grupo de contêiner que inclui vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="46bad-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![Exemplo de grupos de contêineres][container-groups-example]

<span data-ttu-id="46bad-111">Observe que:</span><span class="sxs-lookup"><span data-stu-id="46bad-111">Note that:</span></span>

- <span data-ttu-id="46bad-112">grupo de saudação está agendado em uma máquina de host único.</span><span class="sxs-lookup"><span data-stu-id="46bad-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="46bad-113">grupo de saudação expõe um único endereço IP público, com uma porta exposto.</span><span class="sxs-lookup"><span data-stu-id="46bad-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="46bad-114">grupo de saudação é composto por dois contêineres.</span><span class="sxs-lookup"><span data-stu-id="46bad-114">hello group is made up of two containers.</span></span> <span data-ttu-id="46bad-115">Um contêiner de escuta na porta 80, enquanto outros Olá escuta na porta 5000.</span><span class="sxs-lookup"><span data-stu-id="46bad-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="46bad-116">grupo de saudação inclui dois compartilhamentos de arquivos do Azure como montagem de volume e cada contêiner monta uma saudação compartilhamentos localmente.</span><span class="sxs-lookup"><span data-stu-id="46bad-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="46bad-117">Rede</span><span class="sxs-lookup"><span data-stu-id="46bad-117">Networking</span></span>

<span data-ttu-id="46bad-118">Grupos de contêineres compartilham um endereço IP e um namespace de porta nesse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="46bad-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="46bad-119">tooenable clientes externos tooreach um contêiner no grupo hello, você deve expor porta Olá no endereço IP hello e do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="46bad-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="46bad-120">Como contêineres no grupo Olá compartilham um namespace de porta, não há suporte para mapeamento de porta.</span><span class="sxs-lookup"><span data-stu-id="46bad-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="46bad-121">Contêineres dentro de um grupo podem acessar uns aos outros por meio de localhost em Olá portas que eles têm expostos, mesmo se essas portas não estiverem expostas externamente no endereço IP do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="46bad-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="46bad-122">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="46bad-122">Storage</span></span>

<span data-ttu-id="46bad-123">Você pode especificar volumes externo toomount dentro de um grupo de contêiner.</span><span class="sxs-lookup"><span data-stu-id="46bad-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="46bad-124">Você pode mapear os volumes para caminhos específicos dentro de contêineres de saudação individuais em um grupo.</span><span class="sxs-lookup"><span data-stu-id="46bad-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="46bad-125">Cenários comuns</span><span class="sxs-lookup"><span data-stu-id="46bad-125">Common scenarios</span></span>

<span data-ttu-id="46bad-126">Contêiner de vários grupos são úteis nos casos em que você deseja toodivide a uma única tarefa funcional em um pequeno número de imagens de contêiner, que podem ser entregues por equipes diferentes e têm requisitos de recursos separado.</span><span class="sxs-lookup"><span data-stu-id="46bad-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="46bad-127">Os exemplos de uso podem incluir:</span><span class="sxs-lookup"><span data-stu-id="46bad-127">Example usage could include:</span></span>

- <span data-ttu-id="46bad-128">Um contêiner de aplicativo e um contêiner de log.</span><span class="sxs-lookup"><span data-stu-id="46bad-128">An application container and a logging container.</span></span> <span data-ttu-id="46bad-129">contêiner de log Olá coleta logs de saudação e saída de métricas por aplicativo principal hello e os grava armazenamento toolong prazo.</span><span class="sxs-lookup"><span data-stu-id="46bad-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="46bad-130">Um aplicativo e um contêiner de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="46bad-130">An application and a monitoring container.</span></span> <span data-ttu-id="46bad-131">Olá monitoramento contêiner periodicamente faz um tooensure de aplicativo solicitação toohello que ele está em execução e respondendo corretamente e emite um alerta se não for.</span><span class="sxs-lookup"><span data-stu-id="46bad-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="46bad-132">Um contêiner que atende a um aplicativo web e um contêiner de extrair o conteúdo mais recente de saudação do controle de origem.</span><span class="sxs-lookup"><span data-stu-id="46bad-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46bad-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46bad-133">Next steps</span></span>

<span data-ttu-id="46bad-134">Saiba como muito[implantar um grupo de vários contêiner](container-instances-multi-container-group.md) com um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="46bad-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png