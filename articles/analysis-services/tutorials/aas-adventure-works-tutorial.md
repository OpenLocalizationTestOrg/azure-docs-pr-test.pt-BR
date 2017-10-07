---
title: AAA "Azure Analysis Services Adventure Works Tutorial | Microsoft Docs"
description: "Apresenta um tutorial do Adventure Works Olá para o Azure Analysis Services"
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
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a><span data-ttu-id="70ac8-103">Azure Analysis Services – tutorial da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="70ac8-103">Azure Analysis Services - Adventure Works tutorial</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="70ac8-104">Este tutorial fornece lições sobre como toocreate e implantar um modelo de tabela no nível de compatibilidade Olá 1400 usando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="70ac8-104">This tutorial provides lessons on how toocreate and deploy a tabular model at hello 1400 compatibility level by using [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span>  

<span data-ttu-id="70ac8-105">Se você estiver novos serviços tooAnalysis e modelagem de tabela, concluir este tutorial é toolearn de maneira mais rápida de saudação como toocreate e implantar um modelo de tabela básico.</span><span class="sxs-lookup"><span data-stu-id="70ac8-105">If you're new tooAnalysis Services and tabular modeling, completing this tutorial is hello quickest way toolearn how toocreate and deploy a basic tabular model.</span></span> <span data-ttu-id="70ac8-106">Quando tiver Olá pré-requisitos no local, ele deve levar entre dois toocomplete de horas toothree.</span><span class="sxs-lookup"><span data-stu-id="70ac8-106">Once you have hello prerequisites in-place, it should take between two toothree hours toocomplete.</span></span>  
  
## <a name="what-you-learn"></a><span data-ttu-id="70ac8-107">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="70ac8-107">What you learn</span></span>   
  
-   <span data-ttu-id="70ac8-108">Como toocreate um novo modelo tabular do projeto em Olá **o nível de compatibilidade 1400** no SSDT.</span><span class="sxs-lookup"><span data-stu-id="70ac8-108">How toocreate a new tabular model project at hello **1400 compatibility level** in SSDT.</span></span>
  
-   <span data-ttu-id="70ac8-109">Como tooimport dados de um banco de dados relacional em um projeto de modelo de tabela.</span><span class="sxs-lookup"><span data-stu-id="70ac8-109">How tooimport data from a relational database into a tabular model project.</span></span>  
  
-   <span data-ttu-id="70ac8-110">Como toocreate e gerenciar relações entre tabelas no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="70ac8-110">How toocreate and manage relationships between tables in hello model.</span></span>  
  
-   <span data-ttu-id="70ac8-111">Como toocreate calculada colunas, medidas e indicadores chave de desempenho que ajudam os usuários analisam métricas comerciais críticas.</span><span class="sxs-lookup"><span data-stu-id="70ac8-111">How toocreate calculated columns, measures, and Key Performance Indicators that help users analyze critical business metrics.</span></span>  
  
-   <span data-ttu-id="70ac8-112">Como toocreate e gerenciar perspectivas e hierarquias que ajudam os usuários mais facilmente procurar dados de modelo, fornecendo pontos de vista específicos do aplicativo e de negócios.</span><span class="sxs-lookup"><span data-stu-id="70ac8-112">How toocreate and manage perspectives and hierarchies that help users more easily browse model data by providing business and application-specific viewpoints.</span></span>  
  
-   <span data-ttu-id="70ac8-113">Como toocreate as partições que dividem dados de tabela em partes lógicas menores que podem ser processadas de forma independente de outras partições.</span><span class="sxs-lookup"><span data-stu-id="70ac8-113">How toocreate partitions that divide table data into smaller logical parts that can be processed independent from other partitions.</span></span>  
  
-   <span data-ttu-id="70ac8-114">Como toosecure modelo de objetos e dados criando funções com membros de usuário.</span><span class="sxs-lookup"><span data-stu-id="70ac8-114">How toosecure model objects and data by creating roles with user members.</span></span>  
  
-   <span data-ttu-id="70ac8-115">Como toodeploy um modelo de tabela tooan **Azure Analysis Services** servidor ou um servidor do SQL Server de 2017 Analysis Services local.</span><span class="sxs-lookup"><span data-stu-id="70ac8-115">How toodeploy a tabular model tooan **Azure Analysis Services** server or an on-premises SQL Server 2017 Analysis Services server.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="70ac8-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="70ac8-116">Prerequisites</span></span>  
<span data-ttu-id="70ac8-117">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="70ac8-117">toocomplete this tutorial, you need:</span></span>  
  
-   <span data-ttu-id="70ac8-118">Um Azure Analysis Services ou o Analysis Services do SQL Server de 2017 instância toodeploy seu modelo.</span><span class="sxs-lookup"><span data-stu-id="70ac8-118">An Azure Analysis Services or SQL Server 2017 Analysis Services instance toodeploy your model to.</span></span> <span data-ttu-id="70ac8-119">Inscreva-se para uma [avaliação gratuita do Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) e [crie um servidor](../analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="70ac8-119">Sign up for a free [Azure Analysis Services trial](https://azure.microsoft.com/services/analysis-services/) and [create a server](../analysis-services-create-server.md).</span></span> <span data-ttu-id="70ac8-120">Ou então, inscreva-se e baixe o [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span><span class="sxs-lookup"><span data-stu-id="70ac8-120">Or, sign up and download [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp).</span></span> 

-   <span data-ttu-id="70ac8-121">Um Data Warehouse do SQL Server ou o Azure SQL Data Warehouse com hello [banco de dados de exemplo AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807).</span><span class="sxs-lookup"><span data-stu-id="70ac8-121">A SQL Server Data Warehouse or Azure SQL Data Warehouse with hello [AdventureWorksDW2014 sample database](http://go.microsoft.com/fwlink/?LinkID=335807).</span></span> <span data-ttu-id="70ac8-122">Este banco de dados de exemplo inclui Olá dados necessário toocomplete neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="70ac8-122">This sample database includes hello data necessary toocomplete this tutorial.</span></span> <span data-ttu-id="70ac8-123">Baixe as [edições gratuitas do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).</span><span class="sxs-lookup"><span data-stu-id="70ac8-123">Download [SQL Server free editions](https://www.microsoft.com/sql-server/sql-server-downloads).</span></span> <span data-ttu-id="70ac8-124">Ou então, inscreva-se para uma [avaliação gratuita do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="70ac8-124">Or, sign up for a free [Azure SQL Database trial](https://azure.microsoft.com/services/sql-database/).</span></span> 

    <span data-ttu-id="70ac8-125">**Importante:** se você instalar o banco de dados de exemplo hello em um SQL Server local e implantar o servidor do modelo tooan Azure Analysis Services, uma [gateway de dados no local](../analysis-services-gateway.md) é necessária.</span><span class="sxs-lookup"><span data-stu-id="70ac8-125">**Important:** If you install hello sample database on an on-premises SQL Server, and you deploy your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>

-   <span data-ttu-id="70ac8-126">versão mais recente de saudação do [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span><span class="sxs-lookup"><span data-stu-id="70ac8-126">hello latest version of [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).</span></span>

-   <span data-ttu-id="70ac8-127">versão mais recente de saudação do [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="70ac8-127">hello latest version of [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>    

-   <span data-ttu-id="70ac8-128">Um aplicativo cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel.</span><span class="sxs-lookup"><span data-stu-id="70ac8-128">A client application such as [Power BI Desktop](https://powerbi.microsoft.com/desktop/) or Excel.</span></span> 

## <a name="scenario"></a><span data-ttu-id="70ac8-129">Cenário</span><span class="sxs-lookup"><span data-stu-id="70ac8-129">Scenario</span></span>  
<span data-ttu-id="70ac8-130">Esse tutorial se baseia na Adventure Works Cycles, uma empresa fictícia.</span><span class="sxs-lookup"><span data-stu-id="70ac8-130">This tutorial is based on Adventure Works Cycles, a fictitious company.</span></span> <span data-ttu-id="70ac8-131">A Adventure Works é uma empresa de fabricação grande, empresa multinacional que produz e distribui Bicicletas, peças e mercados de toocommercial Acessórios na América do Norte, Europa e Ásia.</span><span class="sxs-lookup"><span data-stu-id="70ac8-131">Adventure Works is a large, multinational manufacturing company that produces and distributes bicycles, parts, and accessories toocommercial markets in North America, Europe, and Asia.</span></span> <span data-ttu-id="70ac8-132">Olá emprega 500 funcionários.</span><span class="sxs-lookup"><span data-stu-id="70ac8-132">hello company employs 500 workers.</span></span> <span data-ttu-id="70ac8-133">Além disso, a Adventure Works emprega várias equipes regionais de vendas em toda a sua base de mercado.</span><span class="sxs-lookup"><span data-stu-id="70ac8-133">Additionally, Adventure Works employs several regional sales teams throughout its market base.</span></span> <span data-ttu-id="70ac8-134">O projeto está toocreate um modelo de tabela para os usuários de vendas e marketing tooanalyze dados de vendas pela Internet no banco de dados do hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="70ac8-134">Your project is toocreate a tabular model for sales and marketing users tooanalyze Internet sales data in hello AdventureWorksDW database.</span></span>  
  
<span data-ttu-id="70ac8-135">tutorial de saudação toocomplete, você deve concluir várias lições.</span><span class="sxs-lookup"><span data-stu-id="70ac8-135">toocomplete hello tutorial, you must complete various lessons.</span></span> <span data-ttu-id="70ac8-136">Em cada lição, há tarefas.</span><span class="sxs-lookup"><span data-stu-id="70ac8-136">In each lesson, there are tasks.</span></span> <span data-ttu-id="70ac8-137">Conclusão de cada tarefa na ordem é necessária para concluir a lição hello.</span><span class="sxs-lookup"><span data-stu-id="70ac8-137">Completing each task in order is necessary for completing hello lesson.</span></span> <span data-ttu-id="70ac8-138">Embora em uma lição específica possam existir várias tarefas que geram um resultado semelhante, o modo como você conclui cada tarefa é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="70ac8-138">While in a particular lesson there may be several tasks that accomplish a similar outcome, but how you complete each task is slightly different.</span></span> <span data-ttu-id="70ac8-139">Esse método mostra normalmente, há mais de uma maneira toocomplete uma tarefa e toochallenge você usar as habilidades você aprendeu em tarefas e lições anteriores.</span><span class="sxs-lookup"><span data-stu-id="70ac8-139">This method shows there is often more than one way toocomplete a task, and toochallenge you by using skills you've learned in previous lessons and tasks.</span></span>  
  
<span data-ttu-id="70ac8-140">Olá finalidade lições Olá é tooguide você pelo processo de criação de um modelo de tabela básico usando muitos dos recursos de saudação incluído no SSDT.</span><span class="sxs-lookup"><span data-stu-id="70ac8-140">hello purpose of hello lessons is tooguide you through authoring a basic tabular model by using many of hello features included in SSDT.</span></span> <span data-ttu-id="70ac8-141">Porque cada lição é criada na lição anterior Olá, você deve concluir as lições Olá na ordem.</span><span class="sxs-lookup"><span data-stu-id="70ac8-141">Because each lesson builds upon hello previous lesson, you should complete hello lessons in order.</span></span>
  
<span data-ttu-id="70ac8-142">Este tutorial não fornece lições sobre como gerenciar um servidor no portal do Azure, gerenciar um servidor ou banco de dados usando o SSMS, ou usando um cliente de dados de modelo do aplicativo toobrowse.</span><span class="sxs-lookup"><span data-stu-id="70ac8-142">This tutorial does not provide lessons about managing a server in Azure portal, managing a server or database by using SSMS, or using a client application toobrowse model data.</span></span> 


## <a name="lessons"></a><span data-ttu-id="70ac8-143">Lições</span><span class="sxs-lookup"><span data-stu-id="70ac8-143">Lessons</span></span>  
<span data-ttu-id="70ac8-144">Este tutorial inclui Olá lições a seguir:</span><span class="sxs-lookup"><span data-stu-id="70ac8-144">This tutorial includes hello following lessons:</span></span>  
  
|<span data-ttu-id="70ac8-145">Lição</span><span class="sxs-lookup"><span data-stu-id="70ac8-145">Lesson</span></span>|<span data-ttu-id="70ac8-146">Tempo estimado toocomplete</span><span class="sxs-lookup"><span data-stu-id="70ac8-146">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="70ac8-147">1 - Criar um novo projeto de modelo tabular</span><span class="sxs-lookup"><span data-stu-id="70ac8-147">1 - Create a new tabular model project</span></span>](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|<span data-ttu-id="70ac8-148">10 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-148">10 minutes</span></span>|  
|[<span data-ttu-id="70ac8-149">2 - Obter dados</span><span class="sxs-lookup"><span data-stu-id="70ac8-149">2 - Get data</span></span>](../tutorials/aas-lesson-2-get-data.md)|<span data-ttu-id="70ac8-150">10 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-150">10 minutes</span></span>|  
|[<span data-ttu-id="70ac8-151">3 - Marcar como tabela de data</span><span class="sxs-lookup"><span data-stu-id="70ac8-151">3 - Mark as Date Table</span></span>](../tutorials/aas-lesson-3-mark-as-date-table.md)|<span data-ttu-id="70ac8-152">3 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-152">3 minutes</span></span>|  
|[<span data-ttu-id="70ac8-153">4 - Criar relações</span><span class="sxs-lookup"><span data-stu-id="70ac8-153">4 - Create relationships</span></span>](../tutorials/aas-lesson-4-create-relationships.md)|<span data-ttu-id="70ac8-154">10 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-154">10 minutes</span></span>|  
|[<span data-ttu-id="70ac8-155">5 - Criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="70ac8-155">5 - Create calculated columns</span></span>](../tutorials/aas-lesson-5-create-calculated-columns.md)|<span data-ttu-id="70ac8-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-156">15 minutes</span></span>|
|[<span data-ttu-id="70ac8-157">6 - Criar medidas</span><span class="sxs-lookup"><span data-stu-id="70ac8-157">6 - Create measures</span></span>](../tutorials/aas-lesson-6-create-measures.md)|<span data-ttu-id="70ac8-158">30 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-158">30 minutes</span></span>|  
|[<span data-ttu-id="70ac8-159">7 - Criar KPIs (indicadores chave de desempenho)</span><span class="sxs-lookup"><span data-stu-id="70ac8-159">7 - Create Key Performance Indicators (KPI)</span></span>](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|<span data-ttu-id="70ac8-160">15 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-160">15 minutes</span></span>|  
|[<span data-ttu-id="70ac8-161">8 - Criar perspectivas</span><span class="sxs-lookup"><span data-stu-id="70ac8-161">8 - Create perspectives</span></span>](../tutorials/aas-lesson-8-create-perspectives.md)|<span data-ttu-id="70ac8-162">5 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-162">5 minutes</span></span>|  
|[<span data-ttu-id="70ac8-163">9 - Criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="70ac8-163">9 - Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)|<span data-ttu-id="70ac8-164">20 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-164">20 minutes</span></span>|  
|[<span data-ttu-id="70ac8-165">10 - Criar partições</span><span class="sxs-lookup"><span data-stu-id="70ac8-165">10 - Create partitions</span></span>](../tutorials/aas-lesson-10-create-partitions.md)|<span data-ttu-id="70ac8-166">15 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-166">15 minutes</span></span>|  
|[<span data-ttu-id="70ac8-167">11 - Criar funções</span><span class="sxs-lookup"><span data-stu-id="70ac8-167">11 - Create roles</span></span>](../tutorials/aas-lesson-11-create-roles.md)|<span data-ttu-id="70ac8-168">15 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-168">15 minutes</span></span>|  
|[<span data-ttu-id="70ac8-169">12 - Analisar no Excel</span><span class="sxs-lookup"><span data-stu-id="70ac8-169">12 - Analyze in Excel</span></span>](../tutorials/aas-lesson-12-analyze-in-excel.md)|<span data-ttu-id="70ac8-170">5 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-170">5 minutes</span></span>| 
|[<span data-ttu-id="70ac8-171">13 - Implantar</span><span class="sxs-lookup"><span data-stu-id="70ac8-171">13 - Deploy</span></span>](../tutorials/aas-lesson-13-deploy.md)|<span data-ttu-id="70ac8-172">5 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-172">5 minutes</span></span>|  
  
## <a name="supplemental-lessons"></a><span data-ttu-id="70ac8-173">Lições suplementares</span><span class="sxs-lookup"><span data-stu-id="70ac8-173">Supplemental lessons</span></span>  
<span data-ttu-id="70ac8-174">Nestas lições não são tutorial de saudação toocomplete necessária, mas podem ser útil para melhor compreensão advanced criação de modelo tabular recursos.</span><span class="sxs-lookup"><span data-stu-id="70ac8-174">These lessons are not required toocomplete hello tutorial, but can be helpful in better understanding advanced tabular model authoring features.</span></span>  
  
|<span data-ttu-id="70ac8-175">Lição</span><span class="sxs-lookup"><span data-stu-id="70ac8-175">Lesson</span></span>|<span data-ttu-id="70ac8-176">Tempo estimado toocomplete</span><span class="sxs-lookup"><span data-stu-id="70ac8-176">Estimated time toocomplete</span></span>|  
|----------|------------------------------|  
|[<span data-ttu-id="70ac8-177">Linhas de Detalhes</span><span class="sxs-lookup"><span data-stu-id="70ac8-177">Detail Rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)|<span data-ttu-id="70ac8-178">10 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-178">10 minutes</span></span>|
|[<span data-ttu-id="70ac8-179">Segurança dinâmica</span><span class="sxs-lookup"><span data-stu-id="70ac8-179">Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)|<span data-ttu-id="70ac8-180">30 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-180">30 minutes</span></span>|
|[<span data-ttu-id="70ac8-181">Hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="70ac8-181">Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|<span data-ttu-id="70ac8-182">20 minutos</span><span class="sxs-lookup"><span data-stu-id="70ac8-182">20 minutes</span></span>| 

  
## <a name="next-steps"></a><span data-ttu-id="70ac8-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70ac8-183">Next steps</span></span>  
<span data-ttu-id="70ac8-184">tooget iniciado, consulte [lição 1: criar um novo projeto de modelo de tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="70ac8-184">tooget started, see [Lesson 1: Create a New Tabular Model Project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
  
  

