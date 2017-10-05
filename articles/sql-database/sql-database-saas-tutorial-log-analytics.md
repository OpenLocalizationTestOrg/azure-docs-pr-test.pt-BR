---
title: "Usar o Log Analytics com um aplicativo multilocatário de Banco de Dados SQL | Microsoft Docs"
description: Configurar e usar o Log Analytics (OMS) com o aplicativo Wingtip SaaS de exemplo do Banco de Dados SQL do Azure
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: 26f6f519ecb3abf6343dc2776aa141dff99ced15
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="setup-and-use-log-analytics-oms-with-the-wingtip-saas-app"></a><span data-ttu-id="b2c41-104">Configurar e usar o Log Analytics (OMS) com o aplicativo Wingtip SaaS</span><span class="sxs-lookup"><span data-stu-id="b2c41-104">Setup and use Log Analytics (OMS) with the Wingtip SaaS app</span></span>

<span data-ttu-id="b2c41-105">Neste tutorial, você configura e usa o *Log Analytics ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* para monitorar pools elásticos e bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="b2c41-105">In this tutorial, you set up and use *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* for monitoring elastic pools and databases.</span></span> <span data-ttu-id="b2c41-106">Ele se baseia no [Tutorial de monitoramento e gerenciamento de desempenho](sql-database-saas-tutorial-performance-monitoring.md) e mostra como usar o *Log Analytics* para ampliar o monitoramento e alerta fornecidos no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c41-106">It builds on the [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md), and shows how to use *Log Analytics* to augment the monitoring and alerting provided in the Azure portal.</span></span> <span data-ttu-id="b2c41-107">O Log Analytics é especialmente adequado para monitoramento e alertas em grande escala, porque ele dá suporte a centenas de pools e centenas de milhares de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="b2c41-107">Log Analytics is particularly suitable for monitoring and alerting at scale because it supports hundreds of pools and hundreds of thousands of databases.</span></span> <span data-ttu-id="b2c41-108">Ele também fornece uma única solução de monitoramento, que pode integrar o monitoramento de diferentes aplicativos e serviços do Azure, entre várias assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c41-108">It also provides a single monitoring solution, which can integrate monitoring of different applications and Azure services, across multiple Azure subscriptions.</span></span>

<span data-ttu-id="b2c41-109">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="b2c41-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2c41-110">Instalar e configurar o Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="b2c41-110">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="b2c41-111">Usar o Log Analytics para monitorar pools e bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b2c41-111">Use Log Analytics to monitor pools and databases</span></span>

<span data-ttu-id="b2c41-112">Para concluir este tutorial, verifique se todos os pré-requisitos a seguir são atendidos:</span><span class="sxs-lookup"><span data-stu-id="b2c41-112">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="b2c41-113">O aplicativo SaaS Wingtip é implantado.</span><span class="sxs-lookup"><span data-stu-id="b2c41-113">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="b2c41-114">Para implantar em menos de cinco minutos, confira [Implantar e explorar o aplicativo de SaaS do Wingtip](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b2c41-114">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="b2c41-115">O Azure PowerShell está instalado.</span><span class="sxs-lookup"><span data-stu-id="b2c41-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="b2c41-116">Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="b2c41-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

<span data-ttu-id="b2c41-117">Consulte o [Tutorial de monitoramento e gerenciamento de desempenho](sql-database-saas-tutorial-performance-monitoring.md) para uma discussão sobre padrões e cenários de SaaS, e como eles afetam os requisitos de uma solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="b2c41-117">See the [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md) for a discussion of the SaaS scenarios and patterns, and how they affect the requirements on a monitoring solution.</span></span>

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a><span data-ttu-id="b2c41-118">Monitoramento e gerenciamento de desempenho com o Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="b2c41-118">Monitoring and managing performance with Log Analytics (OMS)</span></span>

<span data-ttu-id="b2c41-119">Para o Banco de Dados SQL, o monitoramento e o alerta estão disponíveis em bancos de dados e pools.</span><span class="sxs-lookup"><span data-stu-id="b2c41-119">For SQL Database, monitoring and alerting is available on databases and pools.</span></span> <span data-ttu-id="b2c41-120">Esse monitoramento e alerta internos são específicos de recursos e são convenientes para pequenas quantidades de recursos, mas menos adequados para monitoramento de grandes instalações ou para fornecer uma exibição unificada entre diferentes assinaturas e recursos.</span><span class="sxs-lookup"><span data-stu-id="b2c41-120">This built-in monitoring and alerting is resource-specific and convenient for small numbers of resources, but is less well suited to monitoring large installations or for providing a unified view across different resources and subscriptions.</span></span>

<span data-ttu-id="b2c41-121">Para cenários de alto volume, o Log Analytics pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="b2c41-121">For high-volume scenarios Log Analytics can be used.</span></span> <span data-ttu-id="b2c41-122">Esse é um serviço separado do Azure que fornece análise sobre telemetria e logs de diagnóstico emitidos, coletados em um espaço de trabalho de Log Analytics, que pode coletar a telemetria de muitos serviços e ser usado para consultar e definir alertas.</span><span class="sxs-lookup"><span data-stu-id="b2c41-122">This is a separate Azure service that provides analytics over emitted diagnostic logs and telemetry gathered in a log analytics workspace, which can collect telemetry from many services and be used to query and set alerts.</span></span> <span data-ttu-id="b2c41-123">O Log Analytics fornece uma linguagem de consulta e ferramentas de visualização de dados internas que permitem a visualização e análise de dados operacionais.</span><span class="sxs-lookup"><span data-stu-id="b2c41-123">Log Analytics provides a built-in query language and data visualization tools allowing operational data analytics and visualization.</span></span> <span data-ttu-id="b2c41-124">A solução de Análise de SQL fornece várias exibições e consultas de monitoramento e alertas predefinidos de pool elástico e de banco de dados de e permite que você adicione suas próprias consultas ad hoc e salve-as conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="b2c41-124">The SQL Analytics solution provides several pre-defined elastic pool and database monitoring and alerting views and queries, and lets you add your own ad-hoc queries and save these as needed.</span></span> <span data-ttu-id="b2c41-125">O OMS também fornece um designer de exibição personalizado.</span><span class="sxs-lookup"><span data-stu-id="b2c41-125">OMS also provides a custom view designer.</span></span>

<span data-ttu-id="b2c41-126">Os espaços de trabalho e as soluções de análise do Log Analytics podem ser abertos no Portal do Azure e no OMS.</span><span class="sxs-lookup"><span data-stu-id="b2c41-126">Log Analytics workspaces and analytics solutions can be opened both in the Azure portal and in OMS.</span></span> <span data-ttu-id="b2c41-127">O Portal do Azure é o ponto de acesso mais recente, mas pode estar por trás do portal do OMS em algumas áreas.</span><span class="sxs-lookup"><span data-stu-id="b2c41-127">The Azure portal is the newer access point but may be behind the OMS portal in some areas.</span></span>

### <a name="start-the-load-generator-to-create-data-to-analyze"></a><span data-ttu-id="b2c41-128">Iniciar o gerador de carga para criar dados para analisar</span><span class="sxs-lookup"><span data-stu-id="b2c41-128">Start the load generator to create data to analyze</span></span>

1. <span data-ttu-id="b2c41-129">Abra **Demo-PerformanceMonitoringAndManagement.ps1** no **ISE do PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b2c41-129">Open **Demo-PerformanceMonitoringAndManagement.ps1** in the **PowerShell ISE**.</span></span> <span data-ttu-id="b2c41-130">Mantenha esse script aberto pois você talvez queira executar vários dos cenários de geração de carga durante este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b2c41-130">Keep this script open as you may want to run several of the load generation scenarios during this tutorial.</span></span>
1. <span data-ttu-id="b2c41-131">Se você tem menos de cinco locatários, provisione um lote de locatários para proporcionar um contexto de monitoramento mais interessante:</span><span class="sxs-lookup"><span data-stu-id="b2c41-131">If you have less than five tenants, provision a batch of tenants to provide a more interesting monitoring context:</span></span>
   1. <span data-ttu-id="b2c41-132">Defina **$DemoScenario = 1,** **Provisionar um lote de locatários**</span><span class="sxs-lookup"><span data-stu-id="b2c41-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span></span>
   1. <span data-ttu-id="b2c41-133">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="b2c41-133">Press **F5** to run the script.</span></span>

1. <span data-ttu-id="b2c41-134">Defina **$DemoScenario** = 2, **Gerar carga de intensidade normal (aproximadamente 40 DTU)**.</span><span class="sxs-lookup"><span data-stu-id="b2c41-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**.</span></span>
1. <span data-ttu-id="b2c41-135">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="b2c41-135">Press **F5** to run the script.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="b2c41-136">Obter os scripts do aplicativo Wingtip</span><span class="sxs-lookup"><span data-stu-id="b2c41-136">Get the Wingtip application scripts</span></span>

<span data-ttu-id="b2c41-137">Os scripts do Wingtip Tickets e o código-fonte do aplicativo estão disponíveis no repositório GitHub [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS).</span><span class="sxs-lookup"><span data-stu-id="b2c41-137">The Wingtip Tickets scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="b2c41-138">Os arquivos de script estão localizados na [pasta de Módulos de Aprendizado](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span><span class="sxs-lookup"><span data-stu-id="b2c41-138">Script files are located in the [Learning Modules folder](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span></span> <span data-ttu-id="b2c41-139">Baixe a pasta **Módulos de Aprendizado** em seu computador local, mantendo a estrutura de pastas.</span><span class="sxs-lookup"><span data-stu-id="b2c41-139">Download the **Learning Modules** folder to your local computer, maintaining its folder structure.</span></span>

## <a name="installing-and-configuring-log-analytics-and-the-azure-sql-analytics-solution"></a><span data-ttu-id="b2c41-140">Instalando e configurando o Log Analytics e a solução Análise de SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b2c41-140">Installing and configuring Log Analytics and the Azure SQL Analytics solution</span></span>

<span data-ttu-id="b2c41-141">O Log Analytics é um serviço separado que precisa ser configurado.</span><span class="sxs-lookup"><span data-stu-id="b2c41-141">Log Analytics is a separate service that needs to be configured.</span></span> <span data-ttu-id="b2c41-142">O Log Analytics coleta dados de log e telemetria e métrica em um espaço de trabalho de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b2c41-142">Log Analytics collects log data and telemetry and metrics in a log analytics workspace.</span></span> <span data-ttu-id="b2c41-143">Um espaço de trabalho é um recurso, assim como outros recursos no Azure e deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="b2c41-143">A workspace is a resource, just like other resources in Azure, and must be created.</span></span> <span data-ttu-id="b2c41-144">Embora o espaço de trabalho não precise ser criado no mesmo grupo de recursos que o(s) aplicativo(s) que ele está monitorando, isso geralmente faz mais sentido.</span><span class="sxs-lookup"><span data-stu-id="b2c41-144">While the workspace doesn’t need to be created in the same resource group as the application(s) it is monitoring, this often makes the most sense.</span></span> <span data-ttu-id="b2c41-145">No caso do aplicativo Wingtip SaaS, isso permite que o espaço de trabalho seja excluído facilmente com o aplicativo ao simplesmente excluir o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b2c41-145">In the case of the Wingtip SaaS app, this enables the workspace to be easily deleted with the application by simply deleting the resource group.</span></span>

1. <span data-ttu-id="b2c41-146">Abra ...\\Módulos de aprendizado\\Monitoramento e gerenciamento de desempenho\\Log Analytics\\*Demo-LogAnalytics.ps1* no **ISE do PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b2c41-146">Open ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1* in the **PowerShell ISE**.</span></span>
1. <span data-ttu-id="b2c41-147">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="b2c41-147">Press **F5** to run the script.</span></span>

<span data-ttu-id="b2c41-148">Nesse ponto, você deve ser capaz de abrir o Log Analytics no Portal do Azure (ou no portal do OMS).</span><span class="sxs-lookup"><span data-stu-id="b2c41-148">At this point you should be able open Log Analytics in the Azure portal (or the OMS portal).</span></span> <span data-ttu-id="b2c41-149">Levará alguns minutos para que a telemetria seja coletada no espaço de trabalho do Log Analytics e se torne visível.</span><span class="sxs-lookup"><span data-stu-id="b2c41-149">It will take a few minutes for telemetry to be collected in the Log Analytics workspace and to become visible.</span></span> <span data-ttu-id="b2c41-150">Quanto mais tempo você deixar o sistema coletando de dados, mais interessante será a experiência.</span><span class="sxs-lookup"><span data-stu-id="b2c41-150">The longer you leave the system gathering data the more interesting the experience will be.</span></span> <span data-ttu-id="b2c41-151">Agora é um bom momento para pegar algo pra beber. Só dê uma olhadinha para ter certeza de que o gerador de carga ainda está em execução!</span><span class="sxs-lookup"><span data-stu-id="b2c41-151">Now's a good time to grab a beverage - just make sure the load generator is still running!</span></span>


## <a name="use-log-analytics-and-the-sql-analytics-solution-to-monitor-pools-and-databases"></a><span data-ttu-id="b2c41-152">Usar o Log Analytics e a solução de Análise de SQL para monitorar pools e bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b2c41-152">Use Log Analytics and the SQL Analytics solution to monitor pools and databases</span></span>


<span data-ttu-id="b2c41-153">Neste exercício, abra o Log Analytics e o portal do OMS para examinar a telemetria que está sendo coletada para os bancos de dados e pools.</span><span class="sxs-lookup"><span data-stu-id="b2c41-153">In this exercise, open Log Analytics and the OMS portal to look at the telemetry being gathered for the databases and pools.</span></span>

1. <span data-ttu-id="b2c41-154">Navegue até o [Portal do Azure](https://portal.azure.com) e abra o Log Analytics clicando em Mais serviços e, em seguida, pesquise o Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="b2c41-154">Browse to the [Azure portal](https://portal.azure.com) and open Log Analytics by clicking More services, then search for Log Analytics:</span></span>

   ![abrir log analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. <span data-ttu-id="b2c41-156">Selecione o espaço de trabalho chamado *wtploganalytics-&lt;USER&gt;*.</span><span class="sxs-lookup"><span data-stu-id="b2c41-156">Select the workspace named *wtploganalytics-&lt;USER&gt;*.</span></span>

1. <span data-ttu-id="b2c41-157">Selecione **Visão geral** para abrir a solução Log Analytics no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c41-157">Select **Overview** to open the Log Analytics solution in the Azure portal.</span></span>
   <span data-ttu-id="b2c41-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span><span class="sxs-lookup"><span data-stu-id="b2c41-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span></span>

    <span data-ttu-id="b2c41-159">**IMPORTANTE**: pode levar alguns minutos até que a solução esteja ativa.</span><span class="sxs-lookup"><span data-stu-id="b2c41-159">**IMPORTANT**: It may take a couple of minutes before the solution is active.</span></span> <span data-ttu-id="b2c41-160">Tenha paciência!</span><span class="sxs-lookup"><span data-stu-id="b2c41-160">Be patient!</span></span>

1. <span data-ttu-id="b2c41-161">Clique no bloco Análise de SQL do Azure para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="b2c41-161">Click on the Azure SQL Analytics tile to open it.</span></span>

    ![visão geral](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![análise](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. <span data-ttu-id="b2c41-164">A exibição na folha da solução rola para os lados através da sua própria barra de rolagem na parte inferior (atualize a folha se necessário).</span><span class="sxs-lookup"><span data-stu-id="b2c41-164">The view in the solution blade scrolls sideways, with its own scroll bar at the bottom (refresh the blade if needed).</span></span>

1. <span data-ttu-id="b2c41-165">Explore as várias exibições clicando nelas ou em recursos individuais para abrir um gerenciador de detalhamento, no qual você pode usar o controle deslizante de tempo na parte superior esquerda ou clicar em uma barra vertical para focalizar em uma fração de tempo mais estreita.</span><span class="sxs-lookup"><span data-stu-id="b2c41-165">Explore the various views by clicking on them or on individual resources to open a drill-down explorer, where you can use the time-slider in the top left or click on a vertical bar to focus in on a narrower time slice.</span></span> <span data-ttu-id="b2c41-166">Com esta exibição, você pode selecionar bancos de dados individuais ou pools para se concentrar em recursos específicos:</span><span class="sxs-lookup"><span data-stu-id="b2c41-166">With this view, you can select individual databases or pools to focus on specific resources:</span></span>

    ![gráfico](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. <span data-ttu-id="b2c41-168">De volta na folha da solução, se você rolar para a extrema direita, verá algumas consultas salvas nas quais você pode clicar para abrir e explorar.</span><span class="sxs-lookup"><span data-stu-id="b2c41-168">Back on the solution blade, if you scroll to the far right you will see some saved queries that you can click on to open and explore.</span></span> <span data-ttu-id="b2c41-169">Você pode tentar modificar essas consultas e salvar as consultas interessantes que produzir, as quais você poderá abrir novamente e usar com outros recursos.</span><span class="sxs-lookup"><span data-stu-id="b2c41-169">You can experiment with modifying these, and save any interesting queries you produce, which you can then re-open and use with other resources.</span></span>

1. <span data-ttu-id="b2c41-170">Voltando para a folha do espaço de trabalho do Log Analytics, selecione Portal do OMS para abrir a solução nele.</span><span class="sxs-lookup"><span data-stu-id="b2c41-170">Back on the Log Analytics workspace blade, select OMS Portal to open the solution there.</span></span>

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. <span data-ttu-id="b2c41-172">No portal do OMS, você pode configurar alertas.</span><span class="sxs-lookup"><span data-stu-id="b2c41-172">In the OMS portal, you can configure alerts.</span></span> <span data-ttu-id="b2c41-173">Clique na parte de alertas do modo de exibição de DTU do Banco de Dados.</span><span class="sxs-lookup"><span data-stu-id="b2c41-173">Click on the alert portion of the database DTU view.</span></span>

1. <span data-ttu-id="b2c41-174">Na exibição Pesquisa de Logs que aparece, você verá um gráfico de barras com as métricas que estão sendo representadas.</span><span class="sxs-lookup"><span data-stu-id="b2c41-174">In the Log Search view that appears you will see a bar graph of the metrics being represented.</span></span>

    ![pesquisa do log](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. <span data-ttu-id="b2c41-176">Ao clicar em Alerta na barra de ferramentas, você verá a configuração de alertas e poderá alterá-la.</span><span class="sxs-lookup"><span data-stu-id="b2c41-176">If you click on Alert in the toolbar you will be able to see the alert configuration and can change it.</span></span>

    ![adicionar regra de alerta](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

<span data-ttu-id="b2c41-178">O monitoramento e os alertas no Log Analytics e no OMS baseiam-se em consultas sobre os dados no espaço de trabalho, ao contrário dos alertas em cada folha de recursos, que são específicos de recursos.</span><span class="sxs-lookup"><span data-stu-id="b2c41-178">The monitoring and alerting in Log Analytics and OMS is based on queries over the data in the workspace, unlike the alerting on each resource blade, which is resource-specific.</span></span> <span data-ttu-id="b2c41-179">Portanto, você pode definir um alerta que examina todos os bancos de dados, digamos, em vez de definir um alerta por banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b2c41-179">Thus, you can define an alert that looks over all databases, say, rather than defining one per database.</span></span> <span data-ttu-id="b2c41-180">Ou escrever um alerta que usa uma consulta composta sobre vários tipos de recurso.</span><span class="sxs-lookup"><span data-stu-id="b2c41-180">Or write an alert that uses a composite query over multiple resource types.</span></span> <span data-ttu-id="b2c41-181">As consultas são limitadas apenas pelos dados disponíveis no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b2c41-181">Queries are only limited by the data available in the workspace.</span></span>

<span data-ttu-id="b2c41-182">O Log Analytics para o Banco de Dados SQL é cobrado com base no volume de dados no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b2c41-182">Log Analytics for SQL Database is charged for based on the data volume in the workspace.</span></span> <span data-ttu-id="b2c41-183">Nesse tutorial, você criou um espaço de trabalho Gratuito, que é limitado a 500 MB por dia.</span><span class="sxs-lookup"><span data-stu-id="b2c41-183">In this tutorial, you created a Free workspace, which is limited to 500MB per day.</span></span> <span data-ttu-id="b2c41-184">Quando esse limite é atingido, os dados não são mais adicionados ao espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b2c41-184">Once that limit is reached data is no longer added to the workspace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2c41-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2c41-185">Next steps</span></span>

<span data-ttu-id="b2c41-186">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="b2c41-186">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2c41-187">Instalar e configurar o Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="b2c41-187">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="b2c41-188">Usar o Log Analytics para monitorar pools e bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b2c41-188">Use Log Analytics to monitor pools and databases</span></span>

[<span data-ttu-id="b2c41-189">Tutorial de análise de locatário</span><span class="sxs-lookup"><span data-stu-id="b2c41-189">Tenant analytics tutorial</span></span>](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a><span data-ttu-id="b2c41-190">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b2c41-190">Additional resources</span></span>

* [<span data-ttu-id="b2c41-191">Tutoriais adicionais que aproveitam a implantação de aplicativo SaaS Wingtip inicial</span><span class="sxs-lookup"><span data-stu-id="b2c41-191">Additional tutorials that build upon the initial Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="b2c41-192">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b2c41-192">Azure Log Analytics</span></span>](../log-analytics/log-analytics-azure-sql.md)
* [<span data-ttu-id="b2c41-193">OMS</span><span class="sxs-lookup"><span data-stu-id="b2c41-193">OMS</span></span>](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
