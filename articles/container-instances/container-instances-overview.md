---
title: "Visão geral de instâncias de contêiner de aaaAzure | Documentos do Azure"
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
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a><span data-ttu-id="ef002-103">Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ef002-103">Azure Container Instances</span></span>

<span data-ttu-id="ef002-104">Contêineres rapidamente estão se tornando toopackage de maneira Olá preferido, implantar e gerenciar aplicativos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ef002-104">Containers are quickly becoming hello preferred way toopackage, deploy, and manage cloud applications.</span></span> <span data-ttu-id="ef002-105">Instâncias de contêiner do Azure oferece hello mais rápido e toorun de maneira mais simples um contêiner no Azure, sem ter que tooprovision todas as máquinas virtuais e sem ter que tooadopt um serviço de nível superior.</span><span class="sxs-lookup"><span data-stu-id="ef002-105">Azure Container Instances offers hello fastest and simplest way toorun a container in Azure, without having tooprovision any virtual machines and without having tooadopt a higher-level service.</span></span> 

<span data-ttu-id="ef002-106">As Instâncias de Contêiner do Azure são uma ótima solução para qualquer cenário que possa ser usado em contêineres isolados, incluindo aplicativos simples, automação de tarefas e criação de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ef002-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="ef002-107">Para cenários em que você precisa total orquestração de contêiner, incluindo descoberta do serviço em vários contêineres, dimensionamento automático e atualizações de coordenada de aplicativo, é recomendável Olá [serviço de contêiner do Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="ef002-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="ef002-108">Inicialização mais rápida</span><span class="sxs-lookup"><span data-stu-id="ef002-108">Fast startup times</span></span>

<span data-ttu-id="ef002-109">Os contêineres oferecem vantagens significativas de inicialização em relação às máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="ef002-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="ef002-110">Com instâncias de contêiner do Azure, você pode iniciar um contêiner no Azure em segundos, sem Olá necessidade tooprovision e gerenciar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="ef002-110">With Azure Container Instances, you can start a container in Azure in seconds without hello need tooprovision and manage VMs.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="ef002-111">Segurança em nível de hipervisor</span><span class="sxs-lookup"><span data-stu-id="ef002-111">Hypervisor-level security</span></span>

<span data-ttu-id="ef002-112">Historicamente, os contêineres ofereciam isolamento de dependência de aplicativo e governança de recursos, mas não eram considerados suficientemente protegidos para uso com vários locatários hostis.</span><span class="sxs-lookup"><span data-stu-id="ef002-112">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="ef002-113">Com as Instâncias de Contêiner do Azure, seu aplicativo fica tão isolado em um contêiner quanto ficaria em uma VM.</span><span class="sxs-lookup"><span data-stu-id="ef002-113">With Azure Container Instances, your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="ef002-114">Tamanhos personalizados</span><span class="sxs-lookup"><span data-stu-id="ef002-114">Custom sizes</span></span>

<span data-ttu-id="ef002-115">Contêineres são normalmente otimizada toorun apenas um único aplicativo, mas necessidades Olá desses aplicativos podem diferir significativamente.</span><span class="sxs-lookup"><span data-stu-id="ef002-115">Containers are typically optimized toorun just a single application, but hello exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="ef002-116">Com as Instâncias de Contêiner do Azure, você pode solicitar exatamente o que precisa em termos de memória e núcleos de CPU.</span><span class="sxs-lookup"><span data-stu-id="ef002-116">With Azure Container Instances, you can request exactly what you need in terms of CPU cores and memory.</span></span> <span data-ttu-id="ef002-117">Você paga com base no qual você solicitar cobrado por Olá segundo, para que você pode otimizar eficiente seus gastos com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ef002-117">You pay based on what you request, billed by hello second, so you can finely optimize your spending based on your needs.</span></span>

## <a name="public-ip-connectivity"></a><span data-ttu-id="ef002-118">Conectividade IP pública</span><span class="sxs-lookup"><span data-stu-id="ef002-118">Public IP connectivity</span></span>

<span data-ttu-id="ef002-119">Com instâncias de contêiner do Azure, você pode expor seus contêineres toohello diretamente à internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ef002-119">With Azure Container Instances, you can expose your containers directly toohello internet with a public IP address.</span></span> <span data-ttu-id="ef002-120">Olá futuras, selecionamos expandir nossa rede recursos tooinclude a integração com redes virtuais, carregar balanceadores e outras partes do núcleo do hello infraestrutura de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef002-120">In hello future, we will expand our networking capabilities tooinclude integration with virtual networks, load balancers, and other core parts of hello Azure networking infrastructure.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="ef002-121">Armazenamento persistente</span><span class="sxs-lookup"><span data-stu-id="ef002-121">Persistent storage</span></span>

<span data-ttu-id="ef002-122">tooretrieve e persistir o estado de instâncias de contêiner do Azure, nós oferecemos compartilhamentos de arquivos de montagem direta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef002-122">tooretrieve and persist state with Azure Container Instances, we offer direct mounting of Azure files shares.</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="ef002-123">Contêineres do Windows e do Linux</span><span class="sxs-lookup"><span data-stu-id="ef002-123">Linux and Windows containers</span></span>

<span data-ttu-id="ef002-124">Com instâncias de contêiner do Azure, você pode agendar as duas janelas e contêineres do Linux com hello mesma API.</span><span class="sxs-lookup"><span data-stu-id="ef002-124">With Azure Container Instances, you can schedule both Windows and Linux containers with hello same API.</span></span> <span data-ttu-id="ef002-125">Simplesmente indicar o tipo de sistema operacional base hello e todo o resto é idêntico.</span><span class="sxs-lookup"><span data-stu-id="ef002-125">Simply indicate hello base OS type and everything else is identical.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="ef002-126">Grupos coagendados</span><span class="sxs-lookup"><span data-stu-id="ef002-126">Co-scheduled groups</span></span>

<span data-ttu-id="ef002-127">As Instâncias de Contêiner do Azure dão suporte à programação de grupos com vários contêineres que compartilham um computador host, uma rede local, um armazenamento e um ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="ef002-127">Azure Container Instances supports scheduling of multi-container groups that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="ef002-128">Isso permite que você toocombine principal do seu aplicativo com outras pessoas atuando em uma função de suporte, como o registro em log.</span><span class="sxs-lookup"><span data-stu-id="ef002-128">This enables you toocombine your main application with others acting in a supporting role, such as logging.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef002-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef002-129">Next steps</span></span>

<span data-ttu-id="ef002-130">Tente implantar tooAzure um contêiner com um único comando usando nosso [guia de início rápido](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="ef002-130">Try deploying a container tooAzure with a single command using our [quickstart guide](container-instances-quickstart.md).</span></span>
