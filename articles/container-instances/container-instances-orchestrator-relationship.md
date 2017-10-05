---
title: "Instâncias de Contêiner do Azure e Orquestração de contêiner"
description: "Entender como as Instâncias de Contêiner do Azure interagem com orquestradores de contêiner"
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
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cbb558a92d565759c8dc7d2693960955eb053b0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="1afcc-103">Instâncias de Contêiner do Azure e orquestradores de contêiner</span><span class="sxs-lookup"><span data-stu-id="1afcc-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="1afcc-104">Devido ao seu tamanho reduzido e a orientação a aplicativos, os contêineres são adequados para ambientes de entrega com agilidade e arquiteturas baseadas em microsserviço.</span><span class="sxs-lookup"><span data-stu-id="1afcc-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="1afcc-105">A tarefa de automatizar e gerenciar um grande número de contêineres e como eles interagem é conhecida como *orquestração*.</span><span class="sxs-lookup"><span data-stu-id="1afcc-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="1afcc-106">Orquestradores de contêiner populares incluem Kubernetes, DC/SO e Docker Swarm, que estão disponíveis no [Serviço de Contêiner do Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="1afcc-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="1afcc-107">As Instâncias de Contêiner do Azure fornecem alguns dos recursos básicos de agendamento das plataformas de orquestração, mas elas não abrangem os serviços de maior valor que essas plataformas fornecem e podem realmente ser complementares com elas.</span><span class="sxs-lookup"><span data-stu-id="1afcc-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms, but it does not cover the higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="1afcc-108">Este artigo descreve o escopo do que é controlado pelas Instâncias de Contêiner do Azure e como os orquestradores de contêiner completos podem interagir com elas.</span><span class="sxs-lookup"><span data-stu-id="1afcc-108">This article describes the scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="1afcc-109">Orquestração tradicional</span><span class="sxs-lookup"><span data-stu-id="1afcc-109">Traditional orchestration</span></span>

<span data-ttu-id="1afcc-110">A definição padrão de orquestração inclui as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="1afcc-110">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="1afcc-111">**Agendamento**: dada uma imagem de contêiner e uma solicitação de recurso, localizar um computador adequado no qual executar o contêiner.</span><span class="sxs-lookup"><span data-stu-id="1afcc-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="1afcc-112">**Afinidade/Antiafinidade**: especificar que um conjunto de contêineres devem ser executados próximo uns aos outros (para desempenho) ou suficientemente distantes (para disponibilidade).</span><span class="sxs-lookup"><span data-stu-id="1afcc-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="1afcc-113">**Monitoramento de integridade**: inspecionar falhas de contêiner e automaticamente reagendá-los.</span><span class="sxs-lookup"><span data-stu-id="1afcc-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="1afcc-114">**Failover**: controlar o que está em execução em cada computador e reagendar contêineres de computadores com falha para nós íntegros.</span><span class="sxs-lookup"><span data-stu-id="1afcc-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="1afcc-115">**Dimensionamento**: adicionar ou remover instâncias de contêiner de acordo com a demanda, manualmente ou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1afcc-115">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="1afcc-116">**Rede**: fornecer uma rede de sobreposição a fim de coordenar contêineres para que se comuniquem entre vários computadores host.</span><span class="sxs-lookup"><span data-stu-id="1afcc-116">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="1afcc-117">**Descoberta de serviço**: habilitar contêineres para localizar uns aos outros automaticamente, mesmo que eles se movam entre computadores host e alterem os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="1afcc-117">**Service discovery**: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="1afcc-118">**Atualizações de aplicativo coordenadas**: gerenciar atualizações de contêiner para evitar tempo de inatividade de aplicativo e habilitar a reversão se algo der errado.</span><span class="sxs-lookup"><span data-stu-id="1afcc-118">**Coordinated application upgrades**: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="1afcc-119">Orquestração com Instâncias de Contêiner do Azure: uma abordagem em camadas</span><span class="sxs-lookup"><span data-stu-id="1afcc-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="1afcc-120">As Instâncias de Contêiner do Azure permitem uma abordagem em camadas à orquestração, fornecendo todos os recursos de agendamento e gerenciamento necessários para executar um único contêiner, permitindo ao mesmo tempo que as plataformas de orquestração gerenciem tarefas de vários contêineres sobre elas.</span><span class="sxs-lookup"><span data-stu-id="1afcc-120">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="1afcc-121">Como toda a infra-estrutura subjacente das Instâncias de Contêiner é gerenciada pelo Azure, uma plataforma de orquestração não precisa se preocupar em localizar um computador host apropriado no qual executar um único contêiner.</span><span class="sxs-lookup"><span data-stu-id="1afcc-121">Because all of the underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="1afcc-122">A elasticidade da nuvem garante que um esteja sempre disponível.</span><span class="sxs-lookup"><span data-stu-id="1afcc-122">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="1afcc-123">Em vez disso, o orquestrador pode se concentrar nas tarefas que simplificam o desenvolvimento de arquiteturas de vários contêineres, incluindo o dimensionamento e as atualizações coordenadas.</span><span class="sxs-lookup"><span data-stu-id="1afcc-123">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="1afcc-124">Cenários possíveis</span><span class="sxs-lookup"><span data-stu-id="1afcc-124">Potential scenarios</span></span>

<span data-ttu-id="1afcc-125">Embora a integração do orquestrador com as Instâncias de Contêiner do Azure ainda seja recente, estimamos que alguns ambientes diferentes podem surgir:</span><span class="sxs-lookup"><span data-stu-id="1afcc-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="1afcc-126">Orquestração de instâncias de contêiner de maneira exclusiva</span><span class="sxs-lookup"><span data-stu-id="1afcc-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="1afcc-127">Como elas são iniciadas rapidamente e são cobradas pelo segundo, um ambiente baseado exclusivamente em Instâncias de Contêiner do Azure oferece a maneira mais rápida para começar e para lidar com cargas de trabalho altamente variáveis.</span><span class="sxs-lookup"><span data-stu-id="1afcc-127">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="1afcc-128">Combinação de Instâncias de Contêiner e Contêineres em Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="1afcc-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="1afcc-129">Para cargas de trabalho estáveis de longa execução, orquestrar contêineres em um cluster de máquinas virtuais dedicadas geralmente será mais barato do que executar os mesmos contêineres com Instâncias de Contêiner.</span><span class="sxs-lookup"><span data-stu-id="1afcc-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running the same containers with Container Instances.</span></span> <span data-ttu-id="1afcc-130">No entanto, as Instâncias de Contêiner oferecem uma ótima solução para expandir e reduzir rapidamente a capacidade total para lidar com picos de curta duração ou inesperados no uso.</span><span class="sxs-lookup"><span data-stu-id="1afcc-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="1afcc-131">Em vez de expandir o número de máquinas virtuais em seu cluster e, em seguida, implantar contêineres adicionais nessas máquinas, o orquestrador pode simplesmente agendar os contêineres adicionais usando as Instâncias de Contêiner e excluí-los quando não forem mais necessários.</span><span class="sxs-lookup"><span data-stu-id="1afcc-131">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="1afcc-132">Exemplo de implementação: conector de Instâncias de Contêiner do Azure para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1afcc-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="1afcc-133">Para demonstrar como as plataformas de orquestração de contêiner podem se integrar com as Instâncias de Contêiner do Azure, começamos a criar um [conector de exemplo para Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="1afcc-133">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="1afcc-134">O conector para Kubernetes imita a [kubelet][kubelet-doc] ao registrar-se como um nó com capacidade ilimitada e expedir a criação de [pods][pod-doc] como grupos de contêineres nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="1afcc-134">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="1afcc-135">Os conectores para outros orquestradores podem ser criados da mesma forma, integrados com primitivos de plataforma para combinar a potência da API de orquestrador com a velocidade e a simplicidade do gerenciamento de contêineres nas Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="1afcc-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="1afcc-136">O conector ACI para Kubernetes é *experimental* e não deve ser usado em produção.</span><span class="sxs-lookup"><span data-stu-id="1afcc-136">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1afcc-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1afcc-137">Next steps</span></span>

<span data-ttu-id="1afcc-138">Crie seu primeiro contêiner com as Instâncias de Contêiner do Azure usando o [guia de início rápido](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="1afcc-138">Create your first container with Azure Container Instances using the [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/