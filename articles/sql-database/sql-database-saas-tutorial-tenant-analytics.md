---
title: "Executar consultas de análise em vários bancos de dados Azure SQL | Microsoft Docs"
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
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="07d86-104">Extrair dados de bancos de dados de locatário para um banco de dados analítico para análise offline</span><span class="sxs-lookup"><span data-stu-id="07d86-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="07d86-105">Nesse tutorial é utilizado um trabalho elástico para executar consultas em cada banco de dados de locatário.</span><span class="sxs-lookup"><span data-stu-id="07d86-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="07d86-106">O trabalho extrai dados de vendas de tíquete e carrega-o em um banco de dados de análise (ou data warehouse) para análise.</span><span class="sxs-lookup"><span data-stu-id="07d86-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="07d86-107">O banco de dados de análise é, então, consultado para extrair informações sobre os dados operacionais diários de todos os locatários.</span><span class="sxs-lookup"><span data-stu-id="07d86-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="07d86-108">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="07d86-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07d86-109">Criar o banco de dados de análise de locatário</span><span class="sxs-lookup"><span data-stu-id="07d86-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="07d86-110">Criar um trabalho agendado para recuperar dados e preencher o banco de dados de análise</span><span class="sxs-lookup"><span data-stu-id="07d86-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="07d86-111">Para concluir este tutorial, certifique-se de atender a todos os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="07d86-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="07d86-112">O aplicativo SaaS Wingtip é implantado.</span><span class="sxs-lookup"><span data-stu-id="07d86-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="07d86-113">Para implantar em menos de cinco minutos, confira [Implantar e explorar o aplicativo de SaaS do Wingtip](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="07d86-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="07d86-114">O Azure PowerShell está instalado.</span><span class="sxs-lookup"><span data-stu-id="07d86-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="07d86-115">Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="07d86-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="07d86-116">A última versão do SQL Server Management Studio (SSMS) está instalada.</span><span class="sxs-lookup"><span data-stu-id="07d86-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="07d86-117">Baixar e Instalar o SSMS</span><span class="sxs-lookup"><span data-stu-id="07d86-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="07d86-118">Padrão de Análise Operacional do Locatário</span><span class="sxs-lookup"><span data-stu-id="07d86-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="07d86-119">Uma das ótimas oportunidades com aplicativos SaaS é usar os dados de locatário avançados que são armazenados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="07d86-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="07d86-120">Use esses dados para obter informações sobre a operação e o uso do aplicativo e seus locatários.</span><span class="sxs-lookup"><span data-stu-id="07d86-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="07d86-121">Esses dados podem guiar o desenvolvimento do recurso, aprimoramentos de usabilidade e outros investimentos no aplicativo e na plataforma.</span><span class="sxs-lookup"><span data-stu-id="07d86-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="07d86-122">É fácil acessar esses dados quando estiverem em um único banco de dados multilocatário, mas não tão fácil quando são distribuídos em escala por, potencialmente, milhares de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="07d86-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="07d86-123">Uma abordagem para acessar esses dados é usar os trabalhos Elásticos, que permitem resultados de consulta que retorna resultados da execução do trabalho a ser capturada em um banco de dados e tabela de saída.</span><span class="sxs-lookup"><span data-stu-id="07d86-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="07d86-124">Obter os scripts do aplicativo Wingtip</span><span class="sxs-lookup"><span data-stu-id="07d86-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="07d86-125">Os scripts de SaaS do Wingtip e o código-fonte do aplicativo estão disponíveis no repositório GitHub [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS).</span><span class="sxs-lookup"><span data-stu-id="07d86-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="07d86-126">[Etapas para baixar os scripts do SaaS Wingtip](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="07d86-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="07d86-127">Implantar um banco de dados de resultados de análise de locatário</span><span class="sxs-lookup"><span data-stu-id="07d86-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="07d86-128">Este tutorial requer que você tenha um banco de dados implantado para capturar os resultados da execução do trabalho de scripts, que contêm consultas que retornam resultados.</span><span class="sxs-lookup"><span data-stu-id="07d86-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="07d86-129">Vamos criar um banco de dados chamado tenantanalytics para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="07d86-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="07d86-130">Abra... \\Módulos de Aprendizado\\Análise Operacional\\Análise de Locatário\\*Demo-TenantAnalyticsDB.ps1* no *PowerShell ISE* e defina o seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="07d86-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="07d86-131">**$DemoScenario** = **2** *Implantar banco de dados de análise operacional*</span><span class="sxs-lookup"><span data-stu-id="07d86-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="07d86-132">Pressione **F5** para executar o script de demonstração (que chama o script *Deploy-TenantAnalyticsDB.ps1*) que cria o banco de dados de análise de locatário.</span><span class="sxs-lookup"><span data-stu-id="07d86-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="07d86-133">Criar alguns dados para a demonstração</span><span class="sxs-lookup"><span data-stu-id="07d86-133">Create some data for the demo</span></span>

1. <span data-ttu-id="07d86-134">Abra... \\Módulos de Aprendizado\\Análise Operacional\\Análise de Locatário\\*Demo-TenantAnalyticsDB.ps1* no *PowerShell ISE* e defina o seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="07d86-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="07d86-135">**$DemoScenario** = **1** *Comprar ingressos para eventos em todos os locais*</span><span class="sxs-lookup"><span data-stu-id="07d86-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="07d86-136">Pressione **F5** para executar o script e criar histórico de compras do tíquete.</span><span class="sxs-lookup"><span data-stu-id="07d86-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="07d86-137">Criar um trabalho agendado para recuperar a análise do locatário sobre compras de tíquete</span><span class="sxs-lookup"><span data-stu-id="07d86-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="07d86-138">Este script cria um trabalho para recuperar informações sobre compra do tíquete de todos os locatários.</span><span class="sxs-lookup"><span data-stu-id="07d86-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="07d86-139">Depois de agregadas em uma única tabela, você poderá obter métricas esclarecedoras avançadas sobre padrões de compra de tíquete entre os locatários.</span><span class="sxs-lookup"><span data-stu-id="07d86-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="07d86-140">Abra o SSMS e conecte-se ao servidor catalog-&lt;user&gt;.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="07d86-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="07d86-141">Abra... \\Módulos de Aprendizado\\Análise Operacional\\Locatário Análise\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="07d86-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="07d86-142">Modifique o &lt;User&gt;, utilize o nome de usuário usado quando você implantou o aplicativo de SaaS do Wingtip na parte superior do script, **sp\_add\_target\_group\_member** e **sp\_add\_jobstep**</span><span class="sxs-lookup"><span data-stu-id="07d86-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="07d86-143">Clique o botão direito do mouse, selecione **Conexão** e conecte-se ao servidor catalog-&lt;User&gt;.database.windows.net, se ainda não estiver conectado</span><span class="sxs-lookup"><span data-stu-id="07d86-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="07d86-144">Verifique se está conectado ao banco de dados **jobaccount** e pressione **F5** para executar o script</span><span class="sxs-lookup"><span data-stu-id="07d86-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="07d86-145">**sp\_add\_target\_group** cria o nome do grupo de destino *TenantGroup*, agora é preciso adicionar os membros de destino.</span><span class="sxs-lookup"><span data-stu-id="07d86-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="07d86-146">**sp\_add\_target\_group\_member** adiciona um tipo de membro de destino do *servidor*, o que considera todos os bancos de dados neste servidor (observe que esse é o servidor customer1-&lt;User&gt; que contém os bancos de dados do locatário) na hora em que a execução de trabalho deve ser incluída no trabalho.</span><span class="sxs-lookup"><span data-stu-id="07d86-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="07d86-147">**sp\_add\_job** cria um novo trabalho agendado semanalmente chamado "Compras de Tíquetes de todos os Locatários"</span><span class="sxs-lookup"><span data-stu-id="07d86-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="07d86-148">**sp\_add\_jobstep** cria a etapa de trabalho que contém o texto de comando T-SQL para recuperar todas as informações de compra de tíquete de todos os locatários e copiar o resultado de retorno definido em uma tabela chamada *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="07d86-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="07d86-149">As exibições restantes no script exibem a existência dos objetos e monitoram a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="07d86-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="07d86-150">Examine o valor de status da coluna **ciclo de vida** para monitorar o status.</span><span class="sxs-lookup"><span data-stu-id="07d86-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="07d86-151">Bem-sucedido significa que o trabalho foi concluído com êxito em todos os bancos de dados de locatário e nos dois bancos de dados adicionais que contêm a tabela de referência.</span><span class="sxs-lookup"><span data-stu-id="07d86-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="07d86-152">Executar o script com êxito deve resultar em resultados semelhantes:</span><span class="sxs-lookup"><span data-stu-id="07d86-152">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="07d86-154">Criar um trabalho para recuperar uma contagem resumida de compras de tíquete de todos os locatários</span><span class="sxs-lookup"><span data-stu-id="07d86-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="07d86-155">Este script cria um trabalho para recuperar a soma de todas as compras do tíquete de todos os locatários.</span><span class="sxs-lookup"><span data-stu-id="07d86-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="07d86-156">Abra o SSMS e conecte-se ao servidor *catalog-&lt;User&gt;.database.windows.net*</span><span class="sxs-lookup"><span data-stu-id="07d86-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="07d86-157">Abra o arquivo... \\Módulos de aprendizado\\Provisionar e Catalogar\\Análise Operacional\\Análise do Locatário\\*Results-TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="07d86-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="07d86-158">Modifique o &lt;User&gt;, utilize o nome de usuário usado quando você implantou o aplicativo de SaaS do Wingtip no script, no procedimento armazenado **sp\_add\_jobstep**</span><span class="sxs-lookup"><span data-stu-id="07d86-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="07d86-159">Clique o botão direito do mouse, selecione **Conexão** e conecte-se ao servidor catalog-&lt;User&gt;.database.windows.net, se ainda não estiver conectado</span><span class="sxs-lookup"><span data-stu-id="07d86-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="07d86-160">Verifique se está conectado ao banco de dados **tenantanalytics** e pressione **F5** para executar o script</span><span class="sxs-lookup"><span data-stu-id="07d86-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="07d86-161">Executar o script com êxito deve resultar em resultados semelhantes:</span><span class="sxs-lookup"><span data-stu-id="07d86-161">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="07d86-163">**sp\_add\_job** cria um novo trabalho agendado semanalmente chamado "ResultsTicketsOrders"</span><span class="sxs-lookup"><span data-stu-id="07d86-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="07d86-164">**sp\_add\_jobstep** cria a etapa de trabalho que contém o texto de comando T-SQL para recuperar todas as informações de compra de tíquete de todos os locatários e copiar o resultado de retorno definido em uma tabela chamada CountofTicketOrders</span><span class="sxs-lookup"><span data-stu-id="07d86-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="07d86-165">As exibições restantes no script exibem a existência dos objetos e monitoram a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="07d86-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="07d86-166">Examine o valor de status da coluna **ciclo de vida** para monitorar o status.</span><span class="sxs-lookup"><span data-stu-id="07d86-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="07d86-167">Bem-sucedido significa que o trabalho foi concluído com êxito em todos os bancos de dados de locatário e nos dois bancos de dados adicionais que contêm a tabela de referência.</span><span class="sxs-lookup"><span data-stu-id="07d86-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="07d86-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07d86-168">Next steps</span></span>

<span data-ttu-id="07d86-169">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="07d86-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07d86-170">Implantar um banco de dados de análise do locatário</span><span class="sxs-lookup"><span data-stu-id="07d86-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="07d86-171">Criar um trabalho agendado para recuperar dados analíticos entre locatários</span><span class="sxs-lookup"><span data-stu-id="07d86-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="07d86-172">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="07d86-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07d86-173">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="07d86-173">Additional resources</span></span>

* <span data-ttu-id="07d86-174">[Tutoriais adicionais que aproveitam o aplicativo de SaaS do Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="07d86-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="07d86-175">Trabalhos Elásticos</span><span class="sxs-lookup"><span data-stu-id="07d86-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
