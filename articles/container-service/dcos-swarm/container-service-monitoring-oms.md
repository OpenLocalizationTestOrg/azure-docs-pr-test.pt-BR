---
title: "cluster do Azure DC/OS aaaMonitor - gerenciamento de operações | Microsoft Docs"
description: "Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Microsoft Operations Management Suite."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="9a083-103">Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="9a083-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="9a083-104">O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9a083-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="9a083-105">Contêiner é uma solução de análise de logs do OMS, que ajuda a exibir o inventário de contêiner hello, desempenho e logs em um único local.</span><span class="sxs-lookup"><span data-stu-id="9a083-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="9a083-106">Você pode auditar, solucionar problemas de contêineres exibindo Olá logs em um local centralizado e encontrar ruidosas consumindo em excesso contêiner em um host.</span><span class="sxs-lookup"><span data-stu-id="9a083-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="9a083-107">Para obter mais informações sobre solução de contêiner, consulte toothe [análise de logs de solução de contêiner](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="9a083-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="9a083-108">Configurar o OMS do universo de DC/OS Olá</span><span class="sxs-lookup"><span data-stu-id="9a083-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="9a083-109">Este artigo pressupõe que você tiver configurado um controlador de domínio/sistema operacional e implantar aplicativos de contêiner da web simples no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9a083-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="9a083-110">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="9a083-110">Pre-requisite</span></span>
- <span data-ttu-id="9a083-111">[Assinatura do Microsoft Azure](https://azure.microsoft.com/free/) - você pode obter uma gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="9a083-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="9a083-112">Configuração do espaço de trabalho do Microsoft OMS - consulte a "Etapa 3" abaixo</span><span class="sxs-lookup"><span data-stu-id="9a083-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="9a083-113">[CLI do DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) instalada.</span><span class="sxs-lookup"><span data-stu-id="9a083-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="9a083-114">No painel de DC/OS hello, clique no universo e procure 'OMS', conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a083-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="9a083-115">Clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="9a083-115">Click **Install**.</span></span> <span data-ttu-id="9a083-116">Você verá um pop backup com informações de versão do OMS hello e um **instalar pacote** ou **instalação avançada** botão.</span><span class="sxs-lookup"><span data-stu-id="9a083-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="9a083-117">Quando você clica em **instalação avançada**, o que leva toohello **propriedades de configuração específicas do OMS** página.</span><span class="sxs-lookup"><span data-stu-id="9a083-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="9a083-118">Aqui, você deverá Olá tooenter `wsid` (Olá ID do espaço de trabalho do OMS) e `wskey` (Olá OMS chave primária para a id do espaço de trabalho de saudação).</span><span class="sxs-lookup"><span data-stu-id="9a083-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="9a083-119">ambos os tooget `wsid` e `wskey` você precisa de uma conta do OMS no toocreate <https://mms.microsoft.com>. Siga etapas de saudação toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="9a083-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="9a083-120">Depois de terminar de criar conta de Olá, é necessário tooobtain seu `wsid` e `wskey` clicando **configurações**, em seguida, **fontes conectadas**e, em seguida, **servidores Linux** , conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a083-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="9a083-121">Selecione Olá número você OMS instâncias que você deseja e clique botão de 'Examine e instale' hello.</span><span class="sxs-lookup"><span data-stu-id="9a083-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="9a083-122">Normalmente, você desejará toohave número de saudação de OMS instâncias toohello igual quantos você tem em seu cluster de agente da VM.</span><span class="sxs-lookup"><span data-stu-id="9a083-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="9a083-123">Agente do OMS para Linux é instalado como contêineres individuais em cada VM que deseja toocollect informações para o monitoramento e as informações de log.</span><span class="sxs-lookup"><span data-stu-id="9a083-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="9a083-124">Configuração de um painel OMS simples</span><span class="sxs-lookup"><span data-stu-id="9a083-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="9a083-125">Depois que você instalou Olá agente do OMS para Linux em VMs hello, a próxima etapa é tooset o painel do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9a083-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="9a083-126">Há dois toodo de maneiras isso: Portal do OMS ou no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a083-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="9a083-127">Portal do OMS</span><span class="sxs-lookup"><span data-stu-id="9a083-127">OMS Portal</span></span> 

<span data-ttu-id="9a083-128">Faça logon no portal do OMS toohello (<https://mms.microsoft.com>) e vá toohello **Galeria de soluções**.</span><span class="sxs-lookup"><span data-stu-id="9a083-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="9a083-129">Quando estiver no hello **Galeria de soluções**, selecione **contêineres**.</span><span class="sxs-lookup"><span data-stu-id="9a083-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="9a083-130">Depois de selecionar Olá solução de contêiner, você verá Olá lado a lado na página do painel de visão geral do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9a083-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="9a083-131">Quando os dados do contêiner Olá incluído são indexados, você verá bloco Olá populado com informações sobre os blocos de exibição de solução.</span><span class="sxs-lookup"><span data-stu-id="9a083-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="9a083-132">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9a083-132">Azure Portal</span></span> 

<span data-ttu-id="9a083-133">Portal de tooAzure de logon em <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="9a083-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="9a083-134">Acesse **Marketplace**, selecione **Monitoramento + gerenciamento** e clique em **Ver Tudo**.</span><span class="sxs-lookup"><span data-stu-id="9a083-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="9a083-135">Em seguida, digite `containers` na pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9a083-135">Then Type `containers` in search.</span></span> <span data-ttu-id="9a083-136">Você verá nos resultados da pesquisa hello "contêineres".</span><span class="sxs-lookup"><span data-stu-id="9a083-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="9a083-137">Selecione **Contêineres** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9a083-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="9a083-138">Depois de clicar em **Criar**, ele solicitará seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9a083-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="9a083-139">Selecione seu espaço de trabalho ou, se você não tiver um, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="9a083-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="9a083-140">Depois de selecionar o espaço de trabalho, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9a083-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="9a083-141">Para obter mais informações sobre Olá solução de contêiner do OMS, consulte toothe [análise de logs de solução de contêiner](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="9a083-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="9a083-142">Como tooscale agente do OMS com o ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="9a083-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="9a083-143">No caso de precisar toohave instalado o agente do OMS com pouca contagem do nó real hello ou estão chegando VMSS adicionando mais VM, você pode fazer isso, dimensionando Olá `msoms` serviço.</span><span class="sxs-lookup"><span data-stu-id="9a083-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="9a083-144">Você pode ir de guia de serviços de interface do usuário de DC/OS tooMarathon ou hello e dimensionar sua contagem de nó.</span><span class="sxs-lookup"><span data-stu-id="9a083-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="9a083-145">Isso implantará nós tooother que ainda não tem implantado o agente do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9a083-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="9a083-146">Desinstalar o MS OMS</span><span class="sxs-lookup"><span data-stu-id="9a083-146">Uninstall MS OMS</span></span>

<span data-ttu-id="9a083-147">toouninstall MS OMS digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a083-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="9a083-148">Fale conosco!!!</span><span class="sxs-lookup"><span data-stu-id="9a083-148">Let us know!!!</span></span>
<span data-ttu-id="9a083-149">O que funciona?</span><span class="sxs-lookup"><span data-stu-id="9a083-149">What works?</span></span> <span data-ttu-id="9a083-150">O que falta?</span><span class="sxs-lookup"><span data-stu-id="9a083-150">What is missing?</span></span> <span data-ttu-id="9a083-151">O que mais você precisa para esta toobe útil para você?</span><span class="sxs-lookup"><span data-stu-id="9a083-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="9a083-152">Fale conosco em <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="9a083-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a083-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a083-153">Next steps</span></span>

 <span data-ttu-id="9a083-154">Agora que você tiver configurado o OMS toomonitor seus contêineres,[ver seu painel de contêiner](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="9a083-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
