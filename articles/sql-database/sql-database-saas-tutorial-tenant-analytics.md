---
title: "consultas de análise de aaaRun em vários bancos de dados SQL do Azure | Microsoft Docs"
description: "Extrair dados de bancos de dados de locatário para um banco de dados analítico para análise offline"
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="259f2-104">Extrair dados de bancos de dados de locatário para um banco de dados analítico para análise offline</span><span class="sxs-lookup"><span data-stu-id="259f2-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="259f2-105">Neste tutorial, você deve usar um trabalho de Elástico toorun consulta cada banco de dados de locatário.</span><span class="sxs-lookup"><span data-stu-id="259f2-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="259f2-106">trabalho de saudação extrai dados de vendas de tíquete e carrega-os em um banco de dados de análise (ou data warehouse) para análise.</span><span class="sxs-lookup"><span data-stu-id="259f2-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="259f2-107">Olá banco de dados de análise é então consultada insights tooextract dos dados operacionais diários de todos os locatários.</span><span class="sxs-lookup"><span data-stu-id="259f2-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="259f2-108">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="259f2-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="259f2-109">Criar banco de dados de análise de locatário Olá</span><span class="sxs-lookup"><span data-stu-id="259f2-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="259f2-110">Criar um trabalho agendado de tooretrieve de dados e popular o banco de dados de análise de saudação</span><span class="sxs-lookup"><span data-stu-id="259f2-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="259f2-111">toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir forem atendidas:</span><span class="sxs-lookup"><span data-stu-id="259f2-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="259f2-112">Olá Wingtip SaaS aplicativo é implantado.</span><span class="sxs-lookup"><span data-stu-id="259f2-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="259f2-113">toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="259f2-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="259f2-114">O Azure PowerShell está instalado.</span><span class="sxs-lookup"><span data-stu-id="259f2-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="259f2-115">Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="259f2-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="259f2-116">versão mais recente de saudação do SQL Server Management Studio (SSMS) está instalado.</span><span class="sxs-lookup"><span data-stu-id="259f2-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="259f2-117">Baixar e Instalar o SSMS</span><span class="sxs-lookup"><span data-stu-id="259f2-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="259f2-118">Padrão de Análise Operacional do Locatário</span><span class="sxs-lookup"><span data-stu-id="259f2-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="259f2-119">Um dos grandes oportunidades Olá com aplicativos SaaS é dados de locatário sofisticado de saudação toouse que são armazenados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="259f2-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="259f2-120">Use este insights toogain de dados em operação hello e uso de seu aplicativo e seus locatários.</span><span class="sxs-lookup"><span data-stu-id="259f2-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="259f2-121">Esses dados podem guia de desenvolvimento de recursos, aprimoramentos de usabilidade e outros investimentos em aplicativo hello e plataforma.</span><span class="sxs-lookup"><span data-stu-id="259f2-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="259f2-122">É fácil acessar esses dados quando estiverem em um único banco de dados multilocatário, mas não tão fácil quando são distribuídos em escala por, potencialmente, milhares de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="259f2-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="259f2-123">Tooaccessing de uma abordagem esses dados são trabalhos Elástico toouse, que permitem que os resultados da consulta retorna resultados de toobe de execução do trabalho capturados em um banco de dados de saída e a tabela.</span><span class="sxs-lookup"><span data-stu-id="259f2-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="259f2-124">Obter scripts de aplicativo hello Wingtip</span><span class="sxs-lookup"><span data-stu-id="259f2-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="259f2-125">Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github.</span><span class="sxs-lookup"><span data-stu-id="259f2-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="259f2-126">[As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="259f2-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="259f2-127">Implantar um banco de dados de resultados de análise de locatário</span><span class="sxs-lookup"><span data-stu-id="259f2-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="259f2-128">Este tutorial requer toohave que Olá de toocapture implantado um banco de dados resultante da execução do trabalho de scripts, que contêm consultas retornam resultados.</span><span class="sxs-lookup"><span data-stu-id="259f2-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="259f2-129">Vamos criar um banco de dados chamado tenantanalytics para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="259f2-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="259f2-130">Abrir... \\Módulos de aprendizado\\análise operacional\\locatário análise\\*demonstração TenantAnalyticsDB.ps1* em Olá *PowerShell ISE* e defina Olá seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="259f2-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="259f2-131">**$DemoScenario** = **2** *Implantar banco de dados de análise operacional*</span><span class="sxs-lookup"><span data-stu-id="259f2-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="259f2-132">Pressione **F5** script de demonstração toorun hello (Olá que chamadas *TenantAnalyticsDB.ps1 implantar* script) que cria o banco de dados de análise de locatário hello.</span><span class="sxs-lookup"><span data-stu-id="259f2-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="259f2-133">Criar alguns dados de demonstração de Olá</span><span class="sxs-lookup"><span data-stu-id="259f2-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="259f2-134">Abrir... \\Módulos de aprendizado\\análise operacional\\locatário análise\\*demonstração TenantAnalyticsDB.ps1* em Olá *PowerShell ISE* e defina Olá seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="259f2-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="259f2-135">**$DemoScenario** = **1** *Comprar ingressos para eventos em todos os locais*</span><span class="sxs-lookup"><span data-stu-id="259f2-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="259f2-136">Pressione **F5** toorun Olá script e criar o tíquete de histórico de compras.</span><span class="sxs-lookup"><span data-stu-id="259f2-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="259f2-137">Criar uma análise de locatário do trabalho agendado tooretrieve sobre compras de tíquete</span><span class="sxs-lookup"><span data-stu-id="259f2-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="259f2-138">Esse script cria um informações de compra de tíquete de tooretrieve de trabalho de todos os locatários.</span><span class="sxs-lookup"><span data-stu-id="259f2-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="259f2-139">Quando agregados em uma única tabela, você pode obter métricas criteriosos avançadas sobre padrões de compra por locatários Olá de tíquete.</span><span class="sxs-lookup"><span data-stu-id="259f2-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="259f2-140">Abra o SSMS e conecte-se toohello catálogo -&lt;usuário&gt;. servidor t</span><span class="sxs-lookup"><span data-stu-id="259f2-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="259f2-141">Abra... \\Módulos de Aprendizado\\Análise Operacional\\Locatário Análise\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="259f2-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="259f2-142">Modificar &lt;usuário&gt;, use o nome de usuário de Olá usado quando você implantou o aplicativo de SaaS Wingtip Olá na parte superior de saudação do script hello, **sp\_adicionar\_destino\_grupo\_membro** e **sp\_adicionar\_jobstep**</span><span class="sxs-lookup"><span data-stu-id="259f2-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="259f2-143">Clique com botão direito, selecione **Conexão**e conecte-se toohello catálogo -&lt;usuário&gt;. t server, se ainda não estiver conectado</span><span class="sxs-lookup"><span data-stu-id="259f2-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="259f2-144">Certifique-se de que você está conectado toohello **jobaccount** banco de dados e pressione **F5** para executar o script hello</span><span class="sxs-lookup"><span data-stu-id="259f2-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="259f2-145">**SP\_adicionar\_destino\_grupo** cria o nome do grupo de destino Olá *TenantGroup*, agora precisamos tooadd membros de destino.</span><span class="sxs-lookup"><span data-stu-id="259f2-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="259f2-146">**SP\_adicionar\_destino\_grupo\_membro** adiciona um *server* tipo de membro, o que considerar todos os bancos de dados nesse servidor (note que esta é Olá customer1 - de destino &lt;Usuário&gt; que contém os bancos de dados de locatário de saudação do servidor) em tempo de trabalho de execução deve ser incluída no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="259f2-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="259f2-147">**sp\_add\_job** cria um novo trabalho agendado semanalmente chamado "Compras de Tíquetes de todos os Locatários"</span><span class="sxs-lookup"><span data-stu-id="259f2-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="259f2-148">**SP\_adicionar\_jobstep** cria todas as informações de compra de tíquete de saudação de etapa de trabalho de saudação contendo tooretrieve de texto do comando T-SQL de todos os locatários e Olá cópia retornando o conjunto de resultados em uma tabela chamada  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="259f2-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="259f2-149">Olá restantes no script hello exibem existência de saudação de objetos hello e execução do trabalho de monitor.</span><span class="sxs-lookup"><span data-stu-id="259f2-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="259f2-150">Examine o valor de status de saudação do hello **ciclo de vida** status da coluna toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="259f2-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="259f2-151">Uma vez, foi bem-sucedida, trabalho de saudação foi concluído com êxito em todos os bancos de dados de locatário e dois bancos de dados adicionais contendo Olá Olá referenciam tabela.</span><span class="sxs-lookup"><span data-stu-id="259f2-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="259f2-152">Executado com êxito o script hello deve resultar em resultados semelhantes:</span><span class="sxs-lookup"><span data-stu-id="259f2-152">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="259f2-154">Criar um tooretrieve de trabalho, um resumo da contagem de tíquete de compras de todos os locatários</span><span class="sxs-lookup"><span data-stu-id="259f2-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="259f2-155">Esse script cria uma soma de tooretrieve de trabalho de todas as aquisições do tíquete de todos os locatários.</span><span class="sxs-lookup"><span data-stu-id="259f2-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="259f2-156">Abra o SSMS e conecte-se toohello *catálogo -&lt;usuário&gt;. t* server</span><span class="sxs-lookup"><span data-stu-id="259f2-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="259f2-157">Arquivo hello abrir... \\Módulos de aprendizado\\provisionar e catálogo\\análise operacional\\locatário análise\\*TicketPurchasesfromAllTenants.sql resultados*</span><span class="sxs-lookup"><span data-stu-id="259f2-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="259f2-158">Modificar &lt;usuário&gt;, use o nome de usuário Olá usado quando você implantou o aplicativo de SaaS Wingtip Olá no script hello, em hello **sp\_adicionar\_jobstep** procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="259f2-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="259f2-159">Clique com botão direito, selecione **Conexão**e conecte-se toohello catálogo -&lt;usuário&gt;. t server, se ainda não estiver conectado</span><span class="sxs-lookup"><span data-stu-id="259f2-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="259f2-160">Certifique-se de que você está conectado toohello **tenantanalytics** banco de dados e pressione **F5** para executar o script hello</span><span class="sxs-lookup"><span data-stu-id="259f2-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="259f2-161">Executado com êxito o script hello deve resultar em resultados semelhantes:</span><span class="sxs-lookup"><span data-stu-id="259f2-161">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="259f2-163">**sp\_add\_job** cria um novo trabalho agendado semanalmente chamado "ResultsTicketsOrders"</span><span class="sxs-lookup"><span data-stu-id="259f2-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="259f2-164">**SP\_adicionar\_jobstep** cria todas as informações de compra de tíquete de saudação de etapa de trabalho de saudação contendo tooretrieve de texto do comando T-SQL de todos os locatários e retornando o conjunto de resultados em uma tabela chamada CountofTicketOrders de saudação de cópia</span><span class="sxs-lookup"><span data-stu-id="259f2-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="259f2-165">Olá restantes no script hello exibem existência de saudação de objetos hello e execução do trabalho de monitor.</span><span class="sxs-lookup"><span data-stu-id="259f2-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="259f2-166">Examine o valor de status de saudação do hello **ciclo de vida** status da coluna toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="259f2-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="259f2-167">Uma vez, foi bem-sucedida, trabalho de saudação foi concluído com êxito em todos os bancos de dados de locatário e dois bancos de dados adicionais contendo Olá Olá referenciam tabela.</span><span class="sxs-lookup"><span data-stu-id="259f2-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="259f2-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="259f2-168">Next steps</span></span>

<span data-ttu-id="259f2-169">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="259f2-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="259f2-170">Implantar um banco de dados de análise do locatário</span><span class="sxs-lookup"><span data-stu-id="259f2-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="259f2-171">Criar uma tarefa agendada tooretrieve de dados analíticos por locatários</span><span class="sxs-lookup"><span data-stu-id="259f2-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="259f2-172">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="259f2-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="259f2-173">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="259f2-173">Additional resources</span></span>

* <span data-ttu-id="259f2-174">Adicionais [tutoriais que se baseiam na Olá aplicativo SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="259f2-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="259f2-175">Trabalhos Elásticos</span><span class="sxs-lookup"><span data-stu-id="259f2-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
