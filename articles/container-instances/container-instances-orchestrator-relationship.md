---
title: "Instâncias de contêiner aaaAzure e a coordenação de contêiner"
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
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="de332-103">Instâncias de Contêiner do Azure e orquestradores de contêiner</span><span class="sxs-lookup"><span data-stu-id="de332-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="de332-104">Devido ao seu tamanho reduzido e a orientação a aplicativos, os contêineres são adequados para ambientes de entrega com agilidade e arquiteturas baseadas em microsserviço.</span><span class="sxs-lookup"><span data-stu-id="de332-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="de332-105">tarefa de saudação de automatizar e gerenciar um grande número de contêineres e como eles interagem é conhecida como *orquestração*.</span><span class="sxs-lookup"><span data-stu-id="de332-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="de332-106">Orchestrators contêiner populares incluem Kubernetes, DC/OS e Docker Swarm, que estão disponíveis no hello [serviço de contêiner do Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="de332-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="de332-107">Instâncias de contêiner do Azure fornece algumas Olá básico de funcionalidades de plataformas de orquestração do agendamento, mas ele não aborda os serviços de valor mais alto Olá que essas plataformas fornecem e podem realmente ser complementares com eles.</span><span class="sxs-lookup"><span data-stu-id="de332-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="de332-108">Este artigo descreve o escopo de saudação do lida com instâncias de contêiner do Azure e quanto orchestrators de contêiner podem interagir com ele.</span><span class="sxs-lookup"><span data-stu-id="de332-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="de332-109">Orquestração tradicional</span><span class="sxs-lookup"><span data-stu-id="de332-109">Traditional orchestration</span></span>

<span data-ttu-id="de332-110">a definição padrão Olá de orquestração inclui Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="de332-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="de332-111">**Agendando**: uma imagem de contêiner e uma solicitação de recurso, localize uma máquina adequada no contêiner toorun hello.</span><span class="sxs-lookup"><span data-stu-id="de332-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="de332-112">**Afinidade/Antiafinidade**: especificar que um conjunto de contêineres devem ser executados próximo uns aos outros (para desempenho) ou suficientemente distantes (para disponibilidade).</span><span class="sxs-lookup"><span data-stu-id="de332-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="de332-113">**Monitoramento de integridade**: inspecionar falhas de contêiner e automaticamente reagendá-los.</span><span class="sxs-lookup"><span data-stu-id="de332-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="de332-114">**Failover**: controlar o que está em execução em cada computador e reagendar contêineres de nós de toohealthy máquinas com falha.</span><span class="sxs-lookup"><span data-stu-id="de332-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="de332-115">**Dimensionamento**: Adicionar ou remover a demanda de toomatch de instâncias de contêiner, manual ou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="de332-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="de332-116">**Rede**: forneça uma rede de sobreposição para coordenar contêineres toocommunicate em vários computadores de host.</span><span class="sxs-lookup"><span data-stu-id="de332-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="de332-117">**Descoberta do serviço**: habilitar toolocate contêineres uns aos outros automaticamente mesmo quando eles se mover entre computadores host e alteram os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="de332-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="de332-118">**Coordenada atualizações de aplicativo**: gerenciar aplicativo de contêiner atualizações tooavoid de tempo de inatividade e habilitar a reversão se algo der errado.</span><span class="sxs-lookup"><span data-stu-id="de332-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="de332-119">Orquestração com Instâncias de Contêiner do Azure: uma abordagem em camadas</span><span class="sxs-lookup"><span data-stu-id="de332-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="de332-120">Instâncias de contêiner do Azure permite tooorchestration uma abordagem em camadas, fornecendo todos Olá agendamento e recursos de gerenciamento necessários toorun um único contêiner, permitindo orchestrator tarefas de contêiner de várias plataformas toomanage sobre ele.</span><span class="sxs-lookup"><span data-stu-id="de332-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="de332-121">Como todos Olá infra-estrutura subjacente para instâncias de contêiner é gerenciado pelo Azure, uma plataforma orchestrator não precisa tooconcern se encontrar uma máquina de host apropriado no qual toorun um único contêiner.</span><span class="sxs-lookup"><span data-stu-id="de332-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="de332-122">elasticidade de saudação da nuvem de saudação garante que um está sempre disponível.</span><span class="sxs-lookup"><span data-stu-id="de332-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="de332-123">Em vez disso, o orchestrator Olá pode se concentrarem em tarefas de Olá que simplificam o desenvolvimento de saudação do contêiner várias arquiteturas, incluindo dimensionamento e upgrades coordenados.</span><span class="sxs-lookup"><span data-stu-id="de332-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="de332-124">Cenários possíveis</span><span class="sxs-lookup"><span data-stu-id="de332-124">Potential scenarios</span></span>

<span data-ttu-id="de332-125">Embora a integração do orquestrador com as Instâncias de Contêiner do Azure ainda seja recente, estimamos que alguns ambientes diferentes podem surgir:</span><span class="sxs-lookup"><span data-stu-id="de332-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="de332-126">Orquestração de instâncias de contêiner de maneira exclusiva</span><span class="sxs-lookup"><span data-stu-id="de332-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="de332-127">Porque eles iniciar rapidamente e cobrar pelo Olá segundo, um ambiente com base exclusivamente em instâncias de contêiner do Azure oferece iniciado Olá tooget de maneira mais rápida e toodeal com cargas de trabalho altamente variáveis.</span><span class="sxs-lookup"><span data-stu-id="de332-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="de332-128">Combinação de Instâncias de Contêiner e Contêineres em Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="de332-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="de332-129">Demoradas, cargas de trabalho estáveis, orquestrar contêineres em um cluster de máquinas virtuais dedicadas geralmente será mais baratas do que contêineres em execução Olá mesmo com instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="de332-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="de332-130">No entanto, instâncias de contêiner oferecer uma ótima solução para expandir e reduzir seu toodeal capacidade total com picos de curta duração ou inesperados no uso rapidamente.</span><span class="sxs-lookup"><span data-stu-id="de332-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="de332-131">Em vez de dimensionar número Olá de máquinas virtuais em cluster, em seguida, implantar contêineres adicionais para as máquinas, Olá orchestrator pode agendar recipientes adicionais hello, usando as instâncias de contêiner e excluí-los quando eles são simplesmente nenhum mais necessários.</span><span class="sxs-lookup"><span data-stu-id="de332-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="de332-132">Exemplo de implementação: conector de Instâncias de Contêiner do Azure para Kubernetes</span><span class="sxs-lookup"><span data-stu-id="de332-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="de332-133">toodemonstrate como integrar plataformas de orquestração de contêiner com instâncias de contêiner do Azure, começamos criando uma [conector de exemplo para Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="de332-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="de332-134">Olá conector para Kubernetes imita Olá [kubelet] [ kubelet-doc] registrando como um nó com capacidade ilimitada e expedir a criação de saudação do [compartimentos] [ pod-doc] como grupos de contêineres em instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="de332-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="de332-135">Conectores para outros orchestrators podem ser criados da mesma forma integrada com simplicidade de gerenciar contêineres em instâncias de contêiner do Azure e capacidade de saudação de toocombine de primitivos de plataforma do orchestrator Olá API com velocidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="de332-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="de332-136">Olá conector ACI é Kubernetes *experimental* e não deve ser usada na produção.</span><span class="sxs-lookup"><span data-stu-id="de332-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de332-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="de332-137">Next steps</span></span>

<span data-ttu-id="de332-138">Criar o primeiro contêiner com instâncias de contêiner do Azure usando Olá [guia de início rápido](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="de332-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/