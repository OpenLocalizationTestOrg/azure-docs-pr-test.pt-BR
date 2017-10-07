---
title: "aaaAzure Service Fabric cenários e padrões | Microsoft Docs"
description: "Conheça as práticas recomendadas e comprovadas toodesign padrões reutilizável, desenvolver e operar o microservices na malha do serviço."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="0530a-103">Cenários e padrões do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0530a-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="0530a-104">Se você estiver olhando criando microservices em larga escala usando o Azure Service Fabric, aprenda com especialistas de saudação que projetado e criado nesta plataforma como um serviço (PaaS).</span><span class="sxs-lookup"><span data-stu-id="0530a-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="0530a-105">Introdução à arquitetura correta e, em seguida, Aprenda como toooptimize recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0530a-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="0530a-106">Olá [Service Fabric padrões e práticas recomendadas](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) curso responde Olá perguntas com mais frequência por clientes reais sobre cenários de malha do serviço e áreas de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0530a-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="0530a-107">Descubra como toodesign, desenvolver e operar o microservices na malha do serviço usando as práticas recomendadas e padrões comprovados e reutilizáveis.</span><span class="sxs-lookup"><span data-stu-id="0530a-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="0530a-108">Obtenha uma visão geral do Service Fabric e aprofunde-se nos tópicos que abordam a otimização de cluster e segurança, migração de aplicativos herdados, IoT em grande escala, hospedagem de mecanismos de jogos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="0530a-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="0530a-109">Examinar entrega contínua para várias cargas de trabalho e até mesmo obter detalhes de saudação em suporte para Linux e contêineres.</span><span class="sxs-lookup"><span data-stu-id="0530a-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="0530a-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="0530a-110">Introduction</span></span>
<span data-ttu-id="0530a-111">Explore as práticas recomendadas e saiba mais sobre a escolha de uma plataforma como serviço (PaaS) em vez de uma infraestrutura como serviço (IaaS).</span><span class="sxs-lookup"><span data-stu-id="0530a-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="0530a-112">Obter os detalhes de saudação nos seguintes princípios de design de aplicativo comprovadas.</span><span class="sxs-lookup"><span data-stu-id="0530a-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="0530a-113">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-113">Video</span></span></th><th><span data-ttu-id="0530a-114">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introdução tooService malha</a></span><span class="sxs-lookup"><span data-stu-id="0530a-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="0530a-116">Planejamento e gerenciamento de cluster</span><span class="sxs-lookup"><span data-stu-id="0530a-116">Cluster planning and management</span></span>
<span data-ttu-id="0530a-117">Saiba mais sobre o planejamento de capacidade, otimização e segurança de cluster nesta abordagem do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0530a-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="0530a-118">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-118">Video</span></span></th><th><span data-ttu-id="0530a-119">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="0530a-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planejamento e Gerenciamento de Cluster</a></span><span class="sxs-lookup"><span data-stu-id="0530a-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="0530a-121">Hiperescala Web</span><span class="sxs-lookup"><span data-stu-id="0530a-121">Hyper-scale web</span></span>
<span data-ttu-id="0530a-122">Examine os conceitos de Web de hiperescala, incluindo disponibilidade e confiabilidade, hiperescala e gerenciamento de estado.</span><span class="sxs-lookup"><span data-stu-id="0530a-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="0530a-123">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-123">Video</span></span></th><th><span data-ttu-id="0530a-124">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hiperescala Web</a></span><span class="sxs-lookup"><span data-stu-id="0530a-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="0530a-126">IoT</span><span class="sxs-lookup"><span data-stu-id="0530a-126">IoT</span></span>
<span data-ttu-id="0530a-127">Explore Olá Internet das coisas (IoT) no contexto de saudação do Service Fabric do Azure, incluindo o pipeline do hello IoT do Azure, multilocação e IoT em escala.</span><span class="sxs-lookup"><span data-stu-id="0530a-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="0530a-128">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-128">Video</span></span></th><th><span data-ttu-id="0530a-129">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="0530a-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="0530a-131">Jogos</span><span class="sxs-lookup"><span data-stu-id="0530a-131">Gaming</span></span>
<span data-ttu-id="0530a-132">Examine jogos baseados em turno, jogos interativos e mecanismos existentes de hospedagem de jogos.</span><span class="sxs-lookup"><span data-stu-id="0530a-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="0530a-133">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-133">Video</span></span></th><th><span data-ttu-id="0530a-134">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Jogos</a></span><span class="sxs-lookup"><span data-stu-id="0530a-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="0530a-136">Entrega contínua</span><span class="sxs-lookup"><span data-stu-id="0530a-136">Continuous delivery</span></span>
<span data-ttu-id="0530a-137">Explore os conceitos, incluindo entrega/integração contínua com o Visual Studio Team Services, fluxo de trabalho de build/pacote/publicação, configuração de vários ambientes e pacote/compartilhamento do serviço.</span><span class="sxs-lookup"><span data-stu-id="0530a-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="0530a-138">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-138">Video</span></span></th><th><span data-ttu-id="0530a-139">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Entrega contínua</a></span><span class="sxs-lookup"><span data-stu-id="0530a-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="0530a-141">Migração</span><span class="sxs-lookup"><span data-stu-id="0530a-141">Migration</span></span>
<span data-ttu-id="0530a-142">Saiba mais sobre como migrar de um serviço de nuvem, além de toomigration aplicativos herdados.</span><span class="sxs-lookup"><span data-stu-id="0530a-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="0530a-143">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-143">Video</span></span></th><th><span data-ttu-id="0530a-144">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migração</a></span><span class="sxs-lookup"><span data-stu-id="0530a-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="0530a-146">Suporte para Linux e Contêineres</span><span class="sxs-lookup"><span data-stu-id="0530a-146">Containers and Linux support</span></span>
<span data-ttu-id="0530a-147">Obter pergunta com resposta toohello hello, "por que contêineres?"</span><span class="sxs-lookup"><span data-stu-id="0530a-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="0530a-148">Saiba mais sobre a visualização de saudação para contêineres do Windows e Linux dá suporte a orquestração de contêineres do Linux.</span><span class="sxs-lookup"><span data-stu-id="0530a-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="0530a-149">Além disso, descubra como tooLinux de aplicativos .NET Core toomigrate.</span><span class="sxs-lookup"><span data-stu-id="0530a-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="0530a-150">Vídeo</span><span class="sxs-lookup"><span data-stu-id="0530a-150">Video</span></span></th><th><span data-ttu-id="0530a-151">Área do PowerPoint</span><span class="sxs-lookup"><span data-stu-id="0530a-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="0530a-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Suporte para Linux e contêineres</a></span><span class="sxs-lookup"><span data-stu-id="0530a-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="0530a-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0530a-153">Next steps</span></span>
<span data-ttu-id="0530a-154">Agora que você aprendeu sobre cenários e padrões de malha do serviço, leia mais sobre como muito[criar e gerenciar clusters](service-fabric-deploy-anywhere.md), [migrar aplicativos de serviços de nuvem tooService malha](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [configurar fornecimento contínuo](service-fabric-set-up-continuous-integration.md), e [implantar contêineres](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0530a-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
