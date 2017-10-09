---
title: "cluster aaaMonitor um serviço de contêiner do Azure com Sysdig | Microsoft Docs"
description: "Monitore um cluster do Serviço de Contêiner do Azure com Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="4790f-104">Monitorar um cluster do Serviço de Contêiner do Azure com Sysdig</span><span class="sxs-lookup"><span data-stu-id="4790f-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="4790f-105">Neste artigo, vamos implantará nós de agente de saudação Sysdig agentes tooall em seu cluster de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="4790f-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="4790f-106">Você precisa de uma conta com Sysdig para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="4790f-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4790f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4790f-107">Prerequisites</span></span>
<span data-ttu-id="4790f-108">[Implantar](container-service-deployment.md) e [conectar](../container-service-connect.md) um cluster configurado pelo Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="4790f-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="4790f-109">Explorar Olá [maratona UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="4790f-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="4790f-110">Vá muito[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset uma conta de nuvem Sysdig.</span><span class="sxs-lookup"><span data-stu-id="4790f-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="4790f-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="4790f-111">Sysdig</span></span>
<span data-ttu-id="4790f-112">Sysdig é um serviço de monitoramento que permite que você toomonitor seus contêineres dentro de seu cluster.</span><span class="sxs-lookup"><span data-stu-id="4790f-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="4790f-113">Sysdig é conhecido toohelp na solução de problemas, mas ele também tem suas métricas de monitoramentos básico de rede, CPU, memória e e/s.</span><span class="sxs-lookup"><span data-stu-id="4790f-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="4790f-114">Sysdig torna fácil toosee quais contêineres estão funcionando hello usando o máximo proveito das ou essencialmente hello mais memória e CPU.</span><span class="sxs-lookup"><span data-stu-id="4790f-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="4790f-115">Essa exibição está em Olá seção de "Visão geral", que está atualmente em beta.</span><span class="sxs-lookup"><span data-stu-id="4790f-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Interface do usuário de Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="4790f-117">Configurar uma implantação de Sysdig com Marathon</span><span class="sxs-lookup"><span data-stu-id="4790f-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="4790f-118">Estas etapas mostrarão como tooconfigure e implantar Sysdig aplicativos tooyour cluster com maratona.</span><span class="sxs-lookup"><span data-stu-id="4790f-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="4790f-119">Interface de usuário do controlador de domínio/OS por meio de acesso [http://localhost:80 /](http://localhost:80/) uma vez no hello DC/sistema operacional da interface do usuário navegue toohello "Universo", que está no hello inferior esquerda e, em seguida, procure "Sysdig".</span><span class="sxs-lookup"><span data-stu-id="4790f-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Sysdig no universo de DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="4790f-121">Agora toocomplete Olá configuração são necessários um Sysdig nuvem conta ou uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="4790f-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="4790f-122">Depois de entrar no site de nuvem Sysdig toohello, clique em seu nome de usuário e na página hello, você verá sua "chave de acesso".</span><span class="sxs-lookup"><span data-stu-id="4790f-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Chave de API d Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="4790f-124">Em seguida, digite sua chave de acesso em configuração Sysdig Olá Olá universo de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="4790f-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Configuração de Sysdig no hello universo de DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="4790f-126">Agora defina Olá instâncias too10000000 para que sempre que for adicionado um novo nó de cluster toohello Sysdig implantará automaticamente um agente toothat novo nó.</span><span class="sxs-lookup"><span data-stu-id="4790f-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="4790f-127">Este é um toomake solução temporária se que sysdig implantará tooall novos agentes em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4790f-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Configuração de Sysdig no hello universo de SO/DC-instâncias](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="4790f-129">Depois de instalar o pacote de saudação navegue back toohello Sysdig UI e você será tooexplore capaz de métricas de uso diferentes Olá para contêineres Olá no cluster.</span><span class="sxs-lookup"><span data-stu-id="4790f-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="4790f-130">Você também pode instalar painéis específicos do Mesos e do Marathon por meio do [assistente de novo painel](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="4790f-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
