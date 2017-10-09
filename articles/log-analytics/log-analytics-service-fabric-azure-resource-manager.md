---
title: "aplicativos de serviço de malha com o uso de análise de Log de aaaAssess Olá portal do Azure | Microsoft Docs"
description: "Você pode usar a solução de malha do serviço de saudação na análise de Log com o risco de saudação do hello tooassess portal do Azure e a integridade de seus aplicativos do Service Fabric, microsserviços, nós e os clusters."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="af69c-103">Avaliar microsserviços com hello portal do Azure e os aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="af69c-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="af69c-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="af69c-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="af69c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af69c-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Símbolo do Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="af69c-107">Este artigo descreve como toouse Olá solução Service Fabric na análise de Log toohelp identificar e solucionar problemas em seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af69c-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="af69c-108">Olá solução Service Fabric usa dados de diagnóstico do Azure de suas VMs de malha do serviço, coletando dados de tabelas do Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="af69c-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="af69c-109">O Log Analytics, em seguida, lê eventos da estrutura do Service Fabric, incluindo **Eventos de Serviço Confiável**, **Eventos de Ator**, **Eventos Operacionais** e **Eventos de ETW Personalizados**.</span><span class="sxs-lookup"><span data-stu-id="af69c-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="af69c-110">Com o painel de solução hello, são problemas importantes tooview capaz e eventos relevantes em seu ambiente do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af69c-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="af69c-111">tooget iniciado com a solução hello, você precisa tooconnect seu espaço de trabalho de análise de Log do Service Fabric cluster tooa.</span><span class="sxs-lookup"><span data-stu-id="af69c-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="af69c-112">Aqui estão os três tooconsider de cenários:</span><span class="sxs-lookup"><span data-stu-id="af69c-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="af69c-113">Se você não tiver implantado o cluster do Service Fabric, use as etapas de saudação em ***implantar um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa*** toodeploy um novo cluster e configurou tooreport tooLog análise.</span><span class="sxs-lookup"><span data-stu-id="af69c-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="af69c-114">Se você precisar toocollect contadores de desempenho de seu hosts toouse outras soluções do OMS, como segurança no seu Cluster de malha do serviço, siga as etapas de saudação em ***implantar um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa com extensão de VM instalado.***</span><span class="sxs-lookup"><span data-stu-id="af69c-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="af69c-115">Se você já implantou o cluster do Service Fabric e deseja tooconnect-tooLog Analytics, siga etapas Olá ***adicionando um tooLog de conta de armazenamento existente análise.***</span><span class="sxs-lookup"><span data-stu-id="af69c-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="af69c-116">Implante um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa.</span><span class="sxs-lookup"><span data-stu-id="af69c-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="af69c-117">Este modelo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="af69c-117">This template does hello following:</span></span>

1. <span data-ttu-id="af69c-118">Implanta um espaço de trabalho de análise de logs do Azure Service Fabric cluster já conectado tooa.</span><span class="sxs-lookup"><span data-stu-id="af69c-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="af69c-119">Você tem um novo espaço de trabalho Olá opção toocreate durante a implantação de modelo hello, ou nome de entrada hello de um espaço de trabalho de análise de Log já existente.</span><span class="sxs-lookup"><span data-stu-id="af69c-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="af69c-120">Adiciona o espaço de trabalho do hello armazenamento de diagnóstico conta toohello análise de Log.</span><span class="sxs-lookup"><span data-stu-id="af69c-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="af69c-121">Permite que a solução de malha do serviço de saudação em seu espaço de trabalho de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="af69c-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="af69c-122">[![Implantar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="af69c-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="af69c-123">Depois de selecionar Olá acima do botão implantar, Olá abre portal do Azure com parâmetros para você tooedit.</span><span class="sxs-lookup"><span data-stu-id="af69c-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="af69c-124">Ser toocreate-se de que um novo grupo de recursos, se você inserir um novo nome de espaço de trabalho de análise de Log:</span><span class="sxs-lookup"><span data-stu-id="af69c-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="af69c-127">Aceite os termos legais hello e clique em **criar** toostart implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="af69c-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="af69c-128">Concluída a implantação Olá, você deve ver o novo espaço de trabalho de saudação e o cluster criado e Olá WADServiceFabric * eventos, WADWindowsEventLogs e WADETWEvent tabelas adicionadas:</span><span class="sxs-lookup"><span data-stu-id="af69c-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="af69c-130">Implante um espaço de trabalho de análise de Log do Cluster do Service Fabric conectado tooa com extensão de VM instalado.</span><span class="sxs-lookup"><span data-stu-id="af69c-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="af69c-131">Este modelo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="af69c-131">This template does hello following:</span></span>

1. <span data-ttu-id="af69c-132">Implanta um espaço de trabalho de análise de logs do Azure Service Fabric cluster já conectado tooa.</span><span class="sxs-lookup"><span data-stu-id="af69c-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="af69c-133">Você pode criar um novo espaço de trabalho ou usar um existente.</span><span class="sxs-lookup"><span data-stu-id="af69c-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="af69c-134">Adiciona o espaço de trabalho do hello armazenamento de diagnóstico contas toohello análise de Log.</span><span class="sxs-lookup"><span data-stu-id="af69c-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="af69c-135">Permite que a solução de malha do serviço de Olá no espaço de trabalho de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="af69c-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="af69c-136">Instala a extensão do agente MMA Olá em cada escala de máquina virtual definida no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af69c-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="af69c-137">Com o agente MMA Olá instalado, você está tooview capaz de métricas de desempenho sobre os nós.</span><span class="sxs-lookup"><span data-stu-id="af69c-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="af69c-138">[![Implantar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="af69c-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="af69c-139">Olá as mesmas etapas acima, os parâmetros de entrada hello necessários a seguir e disparar uma implantação.</span><span class="sxs-lookup"><span data-stu-id="af69c-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="af69c-140">Novamente, você verá novo espaço de trabalho de saudação, cluster e tabelas do WAD todos criadas:</span><span class="sxs-lookup"><span data-stu-id="af69c-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="af69c-142">Exibindo dados de desempenho</span><span class="sxs-lookup"><span data-stu-id="af69c-142">Viewing Performance Data</span></span>

<span data-ttu-id="af69c-143">tooview dados de desempenho de seus nós:</span><span class="sxs-lookup"><span data-stu-id="af69c-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="af69c-144">Inicie o espaço de trabalho de análise de Log de saudação de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="af69c-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="af69c-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="af69c-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="af69c-146">Vá tooSettings no painel esquerdo do hello e selecionar dados >> contadores de desempenho do Windows >> "hello adicionar selecionado contadores de desempenho": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="af69c-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="af69c-147">Na pesquisa de Log, use Olá toodelve de consultas a seguir para as principais métricas sobre seus nós:</span><span class="sxs-lookup"><span data-stu-id="af69c-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="af69c-148">a.</span><span class="sxs-lookup"><span data-stu-id="af69c-148">a.</span></span> <span data-ttu-id="af69c-149">Comparar Olá utilização média da CPU em todos os seus nós toosee uma hora última Olá os nós que estão com problemas e no intervalo de tempo que um nó tinha um pico:</span><span class="sxs-lookup"><span data-stu-id="af69c-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="af69c-151">b.</span><span class="sxs-lookup"><span data-stu-id="af69c-151">b.</span></span> <span data-ttu-id="af69c-152">Exibir gráficos de linhas semelhantes para a memória disponível em cada nó com esta consulta:</span><span class="sxs-lookup"><span data-stu-id="af69c-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="af69c-153">tooview uma lista de todos os nós, mostrando o valor médio exato de saudação MBytes disponíveis para cada nó, use esta consulta:</span><span class="sxs-lookup"><span data-stu-id="af69c-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="af69c-155">c.</span><span class="sxs-lookup"><span data-stu-id="af69c-155">c.</span></span> <span data-ttu-id="af69c-156">No caso de Olá que você deseja toodrill para baixo em um nó específico examinando a média de hora em hora Olá, mínima, máximo e 75 percentual da CPU, você está toodo capaz de isso, usar essa consulta (substitua o campo de computador):</span><span class="sxs-lookup"><span data-stu-id="af69c-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="af69c-158">Para obter mais informações sobre as métricas de desempenho na análise de Log em Olá [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="af69c-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="af69c-159">Adicionando um tooLog de conta de armazenamento existente análise</span><span class="sxs-lookup"><span data-stu-id="af69c-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="af69c-160">Este modelo simplesmente adiciona seu armazenamento contas tooa novo ou existente a análise de Log espaço de trabalho existente.</span><span class="sxs-lookup"><span data-stu-id="af69c-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="af69c-161">[![Implantar tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="af69c-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="af69c-162">Selecionar um grupo de recursos, se você estiver trabalhando com um espaço de trabalho de análise de Log já existente, selecione "Usar existente" e pesquisa Olá para grupo de recursos que contém o espaço de trabalho de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="af69c-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="af69c-163">Caso contrário, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="af69c-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="af69c-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="af69c-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="af69c-165">Depois que este modelo foi implantado, você será capaz de toosee Olá armazenamento conta conectada tooyour análise de Log espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="af69c-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="af69c-166">Neste exemplo, adicionei um mais armazenamento conta toohello Exchange espaço de trabalho que criei acima.</span><span class="sxs-lookup"><span data-stu-id="af69c-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="af69c-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="af69c-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="af69c-168">Exibir eventos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="af69c-168">View Service Fabric events</span></span>

<span data-ttu-id="af69c-169">Depois de implantações de saudação são concluídas e Olá solução de malha do serviço foi habilitado no seu espaço de trabalho, selecionar Olá **Service Fabric** bloco no painel de controle do hello análise de Log toolaunch portal Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af69c-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="af69c-170">Painel de saudação inclui colunas de saudação de Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="af69c-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="af69c-171">Cada coluna lista top 10 eventos Olá correspondendo contagem critérios da coluna para Olá especificado intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="af69c-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="af69c-172">Você pode executar uma pesquisa de log que fornece a lista inteira de saudação clicando **ver todos os** na parte inferior direita do hello de cada coluna, ou clicando o cabeçalho da coluna hello.</span><span class="sxs-lookup"><span data-stu-id="af69c-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="af69c-173">**Evento do Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="af69c-173">**Service Fabric event**</span></span> | <span data-ttu-id="af69c-174">**description**</span><span class="sxs-lookup"><span data-stu-id="af69c-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="af69c-175">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="af69c-175">Notable Issues</span></span> |<span data-ttu-id="af69c-176">Uma exibição de problemas como RunAsyncFailures RunAsynCancellations e nós com falha.</span><span class="sxs-lookup"><span data-stu-id="af69c-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="af69c-177">Eventos operacionais</span><span class="sxs-lookup"><span data-stu-id="af69c-177">Operational Events</span></span> |<span data-ttu-id="af69c-178">Eventos operacionais importantes, como atualização de aplicativos e implantações.</span><span class="sxs-lookup"><span data-stu-id="af69c-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="af69c-179">Eventos de serviço confiável</span><span class="sxs-lookup"><span data-stu-id="af69c-179">Reliable Service Events</span></span> |<span data-ttu-id="af69c-180">Eventos importantes de serviços confiáveis como Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="af69c-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="af69c-181">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="af69c-181">Actor Events</span></span> |<span data-ttu-id="af69c-182">Eventos de ator importantes gerados pelos seus microsserviços, como exceções lançadas por um método de ator, ativações e desativações de ator e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="af69c-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="af69c-183">Eventos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="af69c-183">Application Events</span></span> |<span data-ttu-id="af69c-184">Todos os eventos de ETW personalizados gerados por seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="af69c-184">All custom ETW events generated by your applications.</span></span> |

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="af69c-187">Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para a malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="af69c-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="af69c-188">plataforma</span><span class="sxs-lookup"><span data-stu-id="af69c-188">platform</span></span> | <span data-ttu-id="af69c-189">Agente direto</span><span class="sxs-lookup"><span data-stu-id="af69c-189">Direct Agent</span></span> | <span data-ttu-id="af69c-190">Agente do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="af69c-190">Operations Manager agent</span></span> | <span data-ttu-id="af69c-191">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="af69c-191">Azure Storage</span></span> | <span data-ttu-id="af69c-192">Operations Manager necessário?</span><span class="sxs-lookup"><span data-stu-id="af69c-192">Operations Manager required?</span></span> | <span data-ttu-id="af69c-193">Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="af69c-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="af69c-194">frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="af69c-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="af69c-195">Windows</span><span class="sxs-lookup"><span data-stu-id="af69c-195">Windows</span></span> |  |  | <span data-ttu-id="af69c-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="af69c-196">&#8226;</span></span> |  |  |<span data-ttu-id="af69c-197">10 minutos</span><span class="sxs-lookup"><span data-stu-id="af69c-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="af69c-198">Você pode alterar o escopo de saudação desses eventos no hello solução Service Fabric clicando **dados com base nos últimos 7 dias** na parte superior de saudação do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="af69c-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="af69c-199">Você também pode mostrar gerados no hello últimos sete dias, um dia ou seis horas.</span><span class="sxs-lookup"><span data-stu-id="af69c-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="af69c-200">Ou, você pode selecionar **personalizado** toospecify um intervalo de datas personalizado.</span><span class="sxs-lookup"><span data-stu-id="af69c-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="af69c-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af69c-201">Next steps</span></span>

* <span data-ttu-id="af69c-202">Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de evento do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="af69c-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
