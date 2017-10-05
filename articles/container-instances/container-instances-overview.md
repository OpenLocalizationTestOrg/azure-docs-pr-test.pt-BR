---
title: "Visão geral de Instâncias de Contêiner do Azure | Azure Docs"
description: "Compreender as Instâncias de Contêiner do Azure"
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
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 3fb230c6b16a57e3650abf2000acdfe944cd633c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="3df92-103">Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="3df92-103">Azure Container Instances</span></span>

<span data-ttu-id="3df92-104">Os contêineres estão se tornando o modo preferido para empacotar, implantar e gerenciar aplicativos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3df92-104">Containers are quickly becoming the preferred way to package, deploy, and manage cloud applications.</span></span> <span data-ttu-id="3df92-105">As Instâncias de Contêiner do Azure oferecem a maneira mais rápida e simples para executar um contêiner no Azure, sem a necessidade de provisionar máquinas virtuais e adotar um serviço de nível superior.</span><span class="sxs-lookup"><span data-stu-id="3df92-105">Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to provision any virtual machines and without having to adopt a higher-level service.</span></span> 

<span data-ttu-id="3df92-106">As Instâncias de Contêiner do Azure são uma ótima solução para qualquer cenário que possa operar em contêineres isolados, incluindo aplicativos simples, automação de tarefas e criação de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="3df92-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="3df92-107">Para cenários em que você precisa de orquestração de contêiner completa, incluindo descoberta do serviço em vários contêineres, dimensionamento automático e atualizações de aplicativo coordenadas, recomendamos o [Serviço de Contêiner do Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="3df92-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="3df92-108">Inicialização mais rápida</span><span class="sxs-lookup"><span data-stu-id="3df92-108">Fast startup times</span></span>

<span data-ttu-id="3df92-109">Os contêineres oferecem vantagens significativas de inicialização em relação às máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="3df92-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="3df92-110">Com as Instâncias de Contêiner do Azure, você pode iniciar um contêiner no Azure em segundos, sem a necessidade de provisionar e gerenciar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="3df92-110">With Azure Container Instances, you can start a container in Azure in seconds without the need to provision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="3df92-111">Segurança em nível de hipervisor</span><span class="sxs-lookup"><span data-stu-id="3df92-111">Hypervisor-level security</span></span>

<span data-ttu-id="3df92-112">Historicamente, os contêineres ofereciam isolamento de dependência de aplicativo e governança de recursos, mas não eram considerados suficientemente protegidos para uso com vários locatários hostis.</span><span class="sxs-lookup"><span data-stu-id="3df92-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="3df92-113">Com as Instâncias de Contêiner do Azure, seu aplicativo fica tão isolado em um contêiner quanto ficaria em uma VM.</span><span class="sxs-lookup"><span data-stu-id="3df92-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="3df92-114">Tamanhos personalizados</span><span class="sxs-lookup"><span data-stu-id="3df92-114">Custom sizes</span></span>

<span data-ttu-id="3df92-115">Os contêineres normalmente são otimizados para executar apenas um único aplicativo, mas as necessidades exatas desses aplicativos podem variar significativamente.</span><span class="sxs-lookup"><span data-stu-id="3df92-115">Containers are typically optimized to run just a single application, but the exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="3df92-116">Com as Instâncias de Contêiner do Azure, você pode solicitar exatamente o que precisa em termos de memória e núcleos de CPU.</span><span class="sxs-lookup"><span data-stu-id="3df92-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="3df92-117">Você paga com base no que solicitar, cobrado por segundo, para poder otimizar seus gastos eficientemente com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="3df92-117">You pay based on what you request, billed by the second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="3df92-118">Conectividade IP pública</span><span class="sxs-lookup"><span data-stu-id="3df92-118">Public IP connectivity</span></span>

<span data-ttu-id="3df92-119">Com as Instâncias de Contêiner do Azure, você pode expor seus contêineres diretamente à Internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="3df92-119">With Azure Container Instances, you can expose your containers directly to the internet with a public IP address.</span></span> <span data-ttu-id="3df92-120">No futuro, vamos expandir nossos recursos de rede para incluir a integração com redes virtuais, balanceadores de carga e outras partes principais da infraestrutura de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="3df92-120">In the future, we will expand our networking capabilities to include integration with virtual networks, load balancers, and other core parts of the Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="3df92-121">Armazenamento persistente</span><span class="sxs-lookup"><span data-stu-id="3df92-121">Persistent storage</span></span>

<span data-ttu-id="3df92-122">Para recuperar e persistir estados com as Instâncias de Contêiner do Azure, nós oferecemos a montagem direta de compartilhamentos de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3df92-122">To retrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="3df92-123">Contêineres do Windows e do Linux</span><span class="sxs-lookup"><span data-stu-id="3df92-123">Linux and Windows containers</span></span>

<span data-ttu-id="3df92-124">Com as Instâncias de Contêiner do Azure, você pode agendar contêineres do Windows e do Linux com a mesma API.</span><span class="sxs-lookup"><span data-stu-id="3df92-124">With Azure Container Instances, you can schedule both Windows and Linux containers with the same API.</span></span> <span data-ttu-id="3df92-125">Basta indicar o tipo de sistema operacional base e todo o resto é idêntico.</span><span class="sxs-lookup"><span data-stu-id="3df92-125">Simply indicate the base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="3df92-126">Grupos coagendados</span><span class="sxs-lookup"><span data-stu-id="3df92-126">Co-scheduled groups</span></span>

<span data-ttu-id="3df92-127">As Instâncias de Contêiner do Azure dão suporte à programação de grupos com vários contêineres que compartilham um computador host, uma rede local, um armazenamento e um ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="3df92-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="3df92-128">Isso permite que você combine seu aplicativo principal com outros que atuam em uma função de suporte, como o registro em log.</span><span class="sxs-lookup"><span data-stu-id="3df92-128">This enables you to combine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3df92-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3df92-129">Next steps</span></span>

<span data-ttu-id="3df92-130">Tente implantar um contêiner no Azure com um único comando usando nosso [guia de início rápido](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="3df92-130">Try deploying a container to Azure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>