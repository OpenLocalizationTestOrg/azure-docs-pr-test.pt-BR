---
title: "pools de agente aaaDC/OS para o serviço de contêiner do Azure | Microsoft Docs"
description: "Como os pools de agente públicas e privadas de saudação funcionam com um cluster do serviço de contêiner do Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="5e2f9-104">Pools de agentes DC/OS para Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="5e2f9-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="5e2f9-105">Os clusters DC/OS no Serviço de Contêiner do Azure contêm nós de agente em dois pools, um público e um privado.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="5e2f9-106">Um aplicativo pode ser implantado tooeither pool, que afetam a acessibilidade entre computadores em seu serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="5e2f9-107">Hello máquinas podem ser toohello exposto à internet (público) ou mantidos interno (privado).</span><span class="sxs-lookup"><span data-stu-id="5e2f9-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="5e2f9-108">Este artigo fornece uma visão geral sobre o motivo da existência de pools público e privado.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="5e2f9-109">**Agentes privados**: nós de agente privado são executados por meio de uma rede não roteável.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="5e2f9-110">Essa rede é acessível apenas da zona do Olá administrador ou por meio do roteador de borda de zona pública hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="5e2f9-111">Por padrão, o DC/SO inicia aplicativos em nós de agente privada.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="5e2f9-112">**Agentes públicos**: nós de agente público executam aplicativos e serviços DC/OS por meio de uma rede acessível publicamente.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="5e2f9-113">Para obter mais informações sobre segurança de rede do controlador de domínio/sistema operacional, consulte Olá [documentação do controlador de domínio/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="5e2f9-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="5e2f9-114">Implantar pools de agentes</span><span class="sxs-lookup"><span data-stu-id="5e2f9-114">Deploy agent pools</span></span>

<span data-ttu-id="5e2f9-115">Olá DC/OS agente pools no serviço de contêiner do Azure são criados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5e2f9-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="5e2f9-116">Olá **privada pool** contém Olá número de nós de agente que você especifique quando você [implantar Olá DC/OS cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5e2f9-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="5e2f9-117">Olá **pública pool** inicialmente contém um número predeterminado de nós de agente.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="5e2f9-118">Esse pool é adicionado automaticamente quando Olá DC/OS cluster for provisionado.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="5e2f9-119">Olá privada e Olá públicos são conjuntos de escala de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="5e2f9-120">Você pode redimensionar esses pools após a implantação.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="5e2f9-121">Usar pools de agentes</span><span class="sxs-lookup"><span data-stu-id="5e2f9-121">Use agent pools</span></span>
<span data-ttu-id="5e2f9-122">Por padrão, **maratona** implanta qualquer toohello aplicativo novo *privada* nós do agente.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="5e2f9-123">Ter tooexplicitly implantar Olá aplicativo toohello *pública* nós durante a criação de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="5e2f9-124">Selecione Olá **opcional** guia e digite **slave_public** para Olá **funções de recurso aceitos** valor.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="5e2f9-125">Esse processo está documentado [aqui](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) e em Olá [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentação.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e2f9-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e2f9-126">Next steps</span></span>
* <span data-ttu-id="5e2f9-127">Leia mais sobre [como gerenciar seus contêineres DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="5e2f9-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="5e2f9-128">Saiba como muito[abrir o firewall do hello](container-service-enable-public-access.md) fornecido pelos contêineres do Azure tooallow acesso público tooyour DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5e2f9-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

