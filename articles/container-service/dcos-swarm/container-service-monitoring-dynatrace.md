---
title: cluster do Azure DC/OS aaaMonitor - Dynatrace | Microsoft Docs
description: "Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com Dynatrace. Implante Olá Dynatrace OneAgent usando Olá DC/OS painel."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="6ff85-105">Monitorar um cluster de DC/sistema operacional do Serviço de Contêiner do Azure com Dynatrace SaaS/gerenciado</span><span class="sxs-lookup"><span data-stu-id="6ff85-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="6ff85-106">Neste artigo, mostramos como Olá toodeploy [Dynatrace](https://www.dynatrace.com/) Olá de OneAgent toomonitor todos os nós do agente em seu cluster de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff85-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="6ff85-107">Você precisa de uma conta com o Dynatrace SaaS/gerenciado para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="6ff85-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="6ff85-108">Dynatrace SaaS/gerenciado</span><span class="sxs-lookup"><span data-stu-id="6ff85-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="6ff85-109">O Dynatrace é uma solução de monitoramento nativa da nuvem para ambientes de cluster e contêiner altamente dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="6ff85-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="6ff85-110">Ele permite que você toobetter otimizar suas implantações de contêiner e as alocações de memória usando dados de uso em tempo real.</span><span class="sxs-lookup"><span data-stu-id="6ff85-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="6ff85-111">Ele é capaz de identificar automaticamente problemas de infraestrutura e aplicativo, fornecendo linha de base, correlação de problemas e detecção de causa-raiz automatizadas.</span><span class="sxs-lookup"><span data-stu-id="6ff85-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="6ff85-112">a seguir Olá figura mostra Olá Dynatrace UI:</span><span class="sxs-lookup"><span data-stu-id="6ff85-112">hello following figure shows hello Dynatrace UI:</span></span>

![Interface do usuário do Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="6ff85-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ff85-114">Prerequisites</span></span> 
<span data-ttu-id="6ff85-115">[Implantar](container-service-deployment.md) e [conectar](./../container-service-connect.md) tooa cluster configurado pelo serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff85-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="6ff85-116">Explorar Olá [maratona UI](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="6ff85-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="6ff85-117">Vá muito[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset uma conta Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="6ff85-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="6ff85-118">Configurar uma implantação do Dynatrace com o Marathon</span><span class="sxs-lookup"><span data-stu-id="6ff85-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="6ff85-119">Estas etapas mostram como tooconfigure e implantar Dynatrace aplicativos tooyour cluster com maratona.</span><span class="sxs-lookup"><span data-stu-id="6ff85-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="6ff85-120">Acesse a interface do usuário do DC/OS via [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="6ff85-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="6ff85-121">Uma vez no hello DC/sistema operacional da interface do usuário, navegue toohello **universo** guia e, em seguida, procure **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="6ff85-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace no universo de DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="6ff85-123">configuração de saudação toocomplete, é necessário uma conta Dynatrace SaaS ou uma conta de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="6ff85-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="6ff85-124">Quando você faz logon no painel de Dynatrace hello, selecione **implantar Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="6ff85-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Configurar integração de PaaS do Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="6ff85-126">Na página de saudação, selecione **configurar a integração de PaaS**.</span><span class="sxs-lookup"><span data-stu-id="6ff85-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Token da API do Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="6ff85-128">Insira seu token de API em Olá Dynatrace OneAgent configuração Olá universo de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6ff85-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Configuração de dynaTrace OneAgent no hello universo de DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="6ff85-130">Definir instâncias Olá toohello número de nós que você pretende toorun.</span><span class="sxs-lookup"><span data-stu-id="6ff85-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="6ff85-131">Definir um número mais alto também funciona, mas o controlador de domínio/OS continuará tentando toofind novas instâncias até que esse número, na verdade, seja atingido.</span><span class="sxs-lookup"><span data-stu-id="6ff85-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="6ff85-132">Se preferir, você também pode definir este valor tooa como 1000000.</span><span class="sxs-lookup"><span data-stu-id="6ff85-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="6ff85-133">Nesse caso, sempre que um novo nó for adicionado toohello cluster, Dynatrace implanta automaticamente um agente toothat novo nó, preço de saudação do controlador de domínio/sistema operacional tentar constantemente instâncias adicionais do toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6ff85-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Configuração de dynaTrace no hello universo de SO/DC-instâncias](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="6ff85-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ff85-135">Next steps</span></span>

<span data-ttu-id="6ff85-136">Depois de instalar pacote hello, navegue toohello back Dynatrace painel.</span><span class="sxs-lookup"><span data-stu-id="6ff85-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="6ff85-137">Você pode explorar as métricas de uso diferente de saudação para contêineres de saudação no cluster.</span><span class="sxs-lookup"><span data-stu-id="6ff85-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
