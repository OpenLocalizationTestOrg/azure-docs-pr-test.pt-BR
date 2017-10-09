---
title: cluster do Azure DC/OS aaaMonitor - Datadog | Microsoft Docs
description: "Monitore um cluster do Serviço de Contêiner do Azure com o Datadog. Use Olá DC/sistema operacional da web da interface do usuário toodeploy Olá Datadog agentes tooyour cluster."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="70855-105">Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com Datadog</span><span class="sxs-lookup"><span data-stu-id="70855-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="70855-106">Este artigo é implantará nós de agente de saudação Datadog agentes tooall em seu cluster de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="70855-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="70855-107">Você precisará de uma conta no Datadog para fazer esta configuração.</span><span class="sxs-lookup"><span data-stu-id="70855-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="70855-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="70855-108">Prerequisites</span></span>
<span data-ttu-id="70855-109">[Implantar](container-service-deployment.md) e [conectar](../container-service-connect.md) um cluster configurado pelo Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="70855-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="70855-110">Explorar Olá [maratona UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="70855-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="70855-111">Vá muito[http://datadoghq.com](http://datadoghq.com) tooset uma conta Datadog.</span><span class="sxs-lookup"><span data-stu-id="70855-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="70855-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="70855-112">Datadog</span></span>
<span data-ttu-id="70855-113">O Datadog é um serviço de monitoramento que reúne dados de monitoramento de seus contêineres em seu cluster do Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="70855-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="70855-114">O Datadog tem um Painel de Integração do Docker, onde você pode ver as métricas específicas em seus contêineres.</span><span class="sxs-lookup"><span data-stu-id="70855-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="70855-115">As métricas obtidas de seus contêineres são organizadas por CPU, Memória, Rede e E/S.</span><span class="sxs-lookup"><span data-stu-id="70855-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="70855-116">O Datadog divide as métricas em contêineres e em imagens.</span><span class="sxs-lookup"><span data-stu-id="70855-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="70855-117">Um exemplo de quais Olá UI parece CPU uso está abaixo.</span><span class="sxs-lookup"><span data-stu-id="70855-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Interface do usuário do Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="70855-119">Configurar uma implantação do Datadog com Marathon</span><span class="sxs-lookup"><span data-stu-id="70855-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="70855-120">Estas etapas mostrarão como tooconfigure e implantar Datadog aplicativos tooyour cluster com maratona.</span><span class="sxs-lookup"><span data-stu-id="70855-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="70855-121">Acesse a interface do usuário do DC/OS via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="70855-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="70855-122">Uma vez no hello navegue de interface do usuário do controlador de domínio/OS toohello "Universo", que está no hello inferior esquerda e, em seguida, procure "Datadog" e clique em "Instalar".</span><span class="sxs-lookup"><span data-stu-id="70855-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Pacote de Datadog dentro Olá universo de DC/OS](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="70855-124">Agora toocomplete Olá configuração você precisará de uma conta de Datadog ou uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="70855-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="70855-125">Depois de entrar no site de Datadog toohello pesquisar toohello esquerda e vá tooIntegrations ->, em seguida, [APIs](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="70855-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Chave de API do Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="70855-127">Em seguida, digite sua chave de API em configuração Datadog Olá Olá universo de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="70855-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Configuração de Datadog no hello universo de DC/OS](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="70855-129">Em Olá acima configuração instâncias são definidas too10000000 para que sempre que for adicionado um novo nó de cluster toohello Datadog implantará automaticamente um nó de toothat do agente.</span><span class="sxs-lookup"><span data-stu-id="70855-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="70855-130">Essa é uma solução temporária.</span><span class="sxs-lookup"><span data-stu-id="70855-130">This is an interim solution.</span></span> <span data-ttu-id="70855-131">Depois de instalar o pacote de saudação, você deve navegar toohello back Datadog site e localizar "[painéis](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="70855-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="70855-132">A partir daí, você verá os painéis Custom e Integration.</span><span class="sxs-lookup"><span data-stu-id="70855-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="70855-133">Olá [painel Docker](https://app.datadoghq.com/screen/integration/docker) terá todas as métricas de contêiner de saudação é necessário para o monitoramento do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="70855-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

