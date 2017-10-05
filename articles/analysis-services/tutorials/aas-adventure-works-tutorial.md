---
title: Tutorial da Adventure Works do Azure Analysis Services | Microsoft Docs
description: Apresenta o tutorial da Adventure Works para o Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 257e0bc442f29bfe6683fb0511deac50d92c1720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="4a3d4-103">Azure Analysis Services – tutorial da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="4a3d4-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4a3d4-104">Este tutorial fornece lições sobre como criar e implantar um modelo tabular no nível de compatibilidade 1.400 usando [SSDT (SQL Server Data Tools)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-104">This tutorial provides lessons on how to create and deploy a tabular model at the 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="4a3d4-105">Se você estiver pouco familiarizado com o Analysis Services e a modelagem tabular, concluir este tutorial é a maneira mais rápida de aprender a criar e a implantar um modelo tabular básico.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-105">If you're new to Analysis Services and tabular modeling, completing this tutorial is the quickest way to learn how to create and deploy a basic tabular model.</span></span> <span data-ttu-id="4a3d4-106">Uma vez satisfeitos todos o pré-requisitos, ele deverá levar cerca de duas ou três horas para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-106">Once you have the prerequisites in-place, it should take between two to three hours to complete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="4a3d4-107">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4a3d4-107">What you learn</span></span>   
  
-   <span data-ttu-id="4a3d4-108">Como criar um novo projeto de modelo tabular no **nível de compatibilidade 1.400** no SSDT.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-108">How to create a new tabular model project at the **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="4a3d4-109">Como importar dados de um banco de dados relacional para um projeto de modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-109">How to import data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="4a3d4-110">Como criar e gerenciar relações entre tabelas no modelo.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-110">How to create and manage relationships between tables in the model.</span></span>  
  
-   <span data-ttu-id="4a3d4-111">Como criar colunas calculadas, medidas e indicadores chave de desempenho que ajudam os usuários a analisar as métricas de negócios críticas.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-111">How to create calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="4a3d4-112">Como criar e gerenciar perspectivas e hierarquias que ajudam os usuários a procurar dados de modelo mais facilmente, fornecendo pontos de vista específicos de aplicativos e de negócios.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-112">How to create and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="4a3d4-113">Como criar partições que dividem dados de tabela em partes lógicas menores que podem ser processadas independentemente de outras partições.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-113">How to create partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="4a3d4-114">Como proteger os dados e objetos de modelo criando funções com membros de usuário.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-114">How to secure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="4a3d4-115">Como implantar um modelo tabular para um servidor do **Azure Analysis Services** ou um servidor local do SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-115">How to deploy a tabular model to an **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4a3d4-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-116">Prerequisites</span></span>  
<span data-ttu-id="4a3d4-117">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="4a3d4-117">To complete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="4a3d4-118">Uma instância do Azure Analysis Services ou SQL Server 2017 Analysis Services na qual implantar seu modelo.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance to deploy your model to.</span></span> <span data-ttu-id="4a3d4-119">Inscreva-se para uma [avaliação gratuita do Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) e [crie um servidor](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="4a3d4-120">Ou então, inscreva-se e baixe o [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="4a3d4-121">Um SQL Server Data Warehouse ou SQL Data Warehouse do Azure com o [banco de dados de exemplo AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with the [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="4a3d4-122">Esse banco de dados de exemplo inclui os dados necessários para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-122">This sample database includes the data necessary to complete this tutorial.</span></span> <span data-ttu-id="4a3d4-123">Baixe as [edições gratuitas do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="4a3d4-124">Ou então, inscreva-se para uma [avaliação gratuita do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="4a3d4-125">**Importante:** se você instalou o banco de dados de exemplo em um SQL Server local e você está implantando seu modelo em um servidor do Azure Analysis Services, um [gateway de dados local](../analysis-services-gateway.md) é necessário.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-125">**Important:** If you install the sample database on an on-premises SQL Server, and you deploy your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="4a3d4-126">A versão mais recente do [SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-126">The latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="4a3d4-127">A versão mais recente do [SSMS (SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-127">The latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="4a3d4-128">Um aplicativo cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="4a3d4-129">Cenário</span><span class="sxs-lookup"><span data-stu-id="4a3d4-129">Scenario</span></span>  
<span data-ttu-id="4a3d4-130">Esse tutorial se baseia na Adventure Works Cycles, uma empresa fictícia.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="4a3d4-131">A Adventure Works é uma empresa multinacional de grande porte de manufatura, que produz e distribui bicicletas, peças e acessórios para mercados comerciais na América do Norte, Europa e Ásia.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories to commercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="4a3d4-132">A empresa emprega 500 trabalhadores.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-132">The company employs 500 workers.</span></span> <span data-ttu-id="4a3d4-133">Além disso, a Adventure Works emprega várias equipes regionais de vendas em toda a sua base de mercado.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="4a3d4-134">Seu projeto deve criar um modelo tabular para usuários de vendas e marketing analisarem dados de vendas pela Internet no banco de dados AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-134">Your project is to create a tabular model for sales and marketing users to analyze Internet sales data in the AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="4a3d4-135">Para concluir o tutorial, você deverá concluir várias lições.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-135">To complete the tutorial, you must complete various lessons.</span></span> <span data-ttu-id="4a3d4-136">Em cada lição, há tarefas.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="4a3d4-137">A conclusão de cada tarefa na ordem é necessária para concluir a lição.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-137">Completing each task in order is necessary for completing the lesson.</span></span> <span data-ttu-id="4a3d4-138">Embora em uma lição específica possam existir várias tarefas que geram um resultado semelhante, o modo como você conclui cada tarefa é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="4a3d4-139">Este método mostra que geralmente há mais de uma maneira de concluir uma tarefa e de desafiar você usando as habilidades aprendidas em tarefas e lições anteriores.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-139">This method shows there is often more than one way to complete a task, and to challenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="4a3d4-140">A finalidade das lições é orientá-lo na criação de um modelo tabular básico usando muitos dos recursos incluídos no SSDT.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-140">The purpose of the lessons is to guide you through authoring a basic tabular model by using many of the features included in SSDT.</span></span> <span data-ttu-id="4a3d4-141">Já que cada lição faz uso do conteúdo da lição anterior, você deve concluir as lições em ordem.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-141">Because each lesson builds upon the previous lesson, you should complete the lessons in order.</span></span>
  
<span data-ttu-id="4a3d4-142">Este tutorial não fornece lições sobre como gerenciar um servidor no portal do Azure, gerenciar um servidor ou banco de dados usando o SSMS ou usando um aplicativo cliente para procurar dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application to browse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="4a3d4-143">Lições</span><span class="sxs-lookup"><span data-stu-id="4a3d4-143">Lessons</span></span>  
<span data-ttu-id="4a3d4-144">Este tutorial inclui as seguintes lições:</span><span class="sxs-lookup"><span data-stu-id="4a3d4-144">This tutorial includes the following lessons:</span></span>  
  
|<span data-ttu-id="4a3d4-145">Lição</span><span class="sxs-lookup"><span data-stu-id="4a3d4-145">Lesson</span></span>|<span data-ttu-id="4a3d4-146">Tempo estimado para conclusão</span><span class="sxs-lookup"><span data-stu-id="4a3d4-146">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="4a3d4-147">1 - Criar um novo projeto de modelo tabular</span><span class="sxs-lookup"><span data-stu-id="4a3d4-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="4a3d4-148">10 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-148">10 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-149">2 - Obter dados</span><span class="sxs-lookup"><span data-stu-id="4a3d4-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="4a3d4-150">10 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-150">10 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-151">3 - Marcar como tabela de data</span><span class="sxs-lookup"><span data-stu-id="4a3d4-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="4a3d4-152">3 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-152">3 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-153">4 - Criar relações</span><span class="sxs-lookup"><span data-stu-id="4a3d4-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="4a3d4-154">10 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-154">10 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-155">5 - Criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="4a3d4-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="4a3d4-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-156">15 minutes</span></span>|
|[<span data-ttu-id="4a3d4-157">6 - Criar medidas</span><span class="sxs-lookup"><span data-stu-id="4a3d4-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="4a3d4-158">30 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-158">30 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-159">7 - Criar KPIs (indicadores chave de desempenho)</span><span class="sxs-lookup"><span data-stu-id="4a3d4-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="4a3d4-160">15 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-160">15 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-161">8 - Criar perspectivas</span><span class="sxs-lookup"><span data-stu-id="4a3d4-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="4a3d4-162">5 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-162">5 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-163">9 - Criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="4a3d4-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="4a3d4-164">20 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-164">20 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-165">10 - Criar partições</span><span class="sxs-lookup"><span data-stu-id="4a3d4-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="4a3d4-166">15 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-166">15 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-167">11 - Criar funções</span><span class="sxs-lookup"><span data-stu-id="4a3d4-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="4a3d4-168">15 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-168">15 minutes</span></span>|  
|[<span data-ttu-id="4a3d4-169">12 - Analisar no Excel</span><span class="sxs-lookup"><span data-stu-id="4a3d4-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="4a3d4-170">5 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-170">5 minutes</span></span>| 
|[<span data-ttu-id="4a3d4-171">13 - Implantar</span><span class="sxs-lookup"><span data-stu-id="4a3d4-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="4a3d4-172">5 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="4a3d4-173">Lições suplementares</span><span class="sxs-lookup"><span data-stu-id="4a3d4-173">Supplemental lessons</span></span>  
<span data-ttu-id="4a3d4-174">Essas lições não são necessárias para concluir este tutorial, mas podem ser úteis para uma melhor compreensão dos recursos avançados de criação de modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="4a3d4-174">These lessons are not required to complete the tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="4a3d4-175">Lição</span><span class="sxs-lookup"><span data-stu-id="4a3d4-175">Lesson</span></span>|<span data-ttu-id="4a3d4-176">Tempo estimado para conclusão</span><span class="sxs-lookup"><span data-stu-id="4a3d4-176">Estimated time to complete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="4a3d4-177">Linhas de Detalhes</span><span class="sxs-lookup"><span data-stu-id="4a3d4-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="4a3d4-178">10 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-178">10 minutes</span></span>|
|[<span data-ttu-id="4a3d4-179">Segurança dinâmica</span><span class="sxs-lookup"><span data-stu-id="4a3d4-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="4a3d4-180">30 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-180">30 minutes</span></span>|
|[<span data-ttu-id="4a3d4-181">Hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="4a3d4-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="4a3d4-182">20 minutos</span><span class="sxs-lookup"><span data-stu-id="4a3d4-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="4a3d4-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a3d4-183">Next steps</span></span>  
<span data-ttu-id="4a3d4-184">Para uma introdução, veja [Lição 1: criar um novo projeto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="4a3d4-184">To get started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

