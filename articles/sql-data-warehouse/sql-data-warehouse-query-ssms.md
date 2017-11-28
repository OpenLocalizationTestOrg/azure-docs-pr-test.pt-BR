---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Microsoft Docs
description: Use o SQL Server Management Studio (SSMS) tooconnect tooand consulta Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="9deda-103">Conecte-se tooSQL Data Warehouse com o SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="9deda-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9deda-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="9deda-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="9deda-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="9deda-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="9deda-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9deda-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="9deda-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="9deda-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="9deda-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="9deda-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="9deda-109">Use o SQL Server Management Studio (SSMS) tooconnect tooand consulta Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9deda-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9deda-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9deda-110">Prerequisites</span></span>
<span data-ttu-id="9deda-111">toouse neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="9deda-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="9deda-112">Um SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="9deda-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="9deda-113">toocreate um, consulte [criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9deda-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="9deda-114">SSMS (SQL Server Management Studio) instalado.</span><span class="sxs-lookup"><span data-stu-id="9deda-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="9deda-115">[Instale o SSMS][Install SSMS] gratuitamente se você ainda não o tiver.</span><span class="sxs-lookup"><span data-stu-id="9deda-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="9deda-116">Olá totalmente qualificado o nome do SQL server.</span><span class="sxs-lookup"><span data-stu-id="9deda-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="9deda-117">toofind isso, consulte [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9deda-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="9deda-118">1. Conecte-se tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9deda-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="9deda-119">Abra o SSMS.</span><span class="sxs-lookup"><span data-stu-id="9deda-119">Open SSMS.</span></span>
2. <span data-ttu-id="9deda-120">Abrir Pesquisador de Objetos.</span><span class="sxs-lookup"><span data-stu-id="9deda-120">Open Object Explorer.</span></span> <span data-ttu-id="9deda-121">toodo, selecione **arquivo** > **conectar Pesquisador**.</span><span class="sxs-lookup"><span data-stu-id="9deda-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Pesquisador de Objetos do SQL Server][1]
3. <span data-ttu-id="9deda-123">Preencha os campos de saudação na janela de tooServer conectar hello.</span><span class="sxs-lookup"><span data-stu-id="9deda-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Conecte-se tooServer][2]
   
   * <span data-ttu-id="9deda-125">**Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="9deda-125">**Server name**.</span></span> <span data-ttu-id="9deda-126">Digite hello **nome do servidor** identificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9deda-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="9deda-127">**Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="9deda-127">**Authentication**.</span></span> <span data-ttu-id="9deda-128">Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9deda-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="9deda-129">**Nome de Usuário** e **Senha**.</span><span class="sxs-lookup"><span data-stu-id="9deda-129">**User Name** and **Password**.</span></span> <span data-ttu-id="9deda-130">Insira o nome de usuário e senha se a Autenticação do SQL Server foi selecionada acima.</span><span class="sxs-lookup"><span data-stu-id="9deda-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="9deda-131">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="9deda-131">Click **Connect**.</span></span>
4. <span data-ttu-id="9deda-132">tooexplore, expanda seu servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9deda-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="9deda-133">Você pode exibir bancos de dados de saudação associados ao servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9deda-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="9deda-134">Expanda as tabelas de saudação do AdventureWorksDW toosee em seu banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="9deda-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorar o AdventureWorksWeb][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="9deda-136">2. Executar uma consulta de exemplo</span><span class="sxs-lookup"><span data-stu-id="9deda-136">2. Run a sample query</span></span>
<span data-ttu-id="9deda-137">Agora que uma conexão foi estabelecida tooyour banco de dados, vamos escrever uma consulta.</span><span class="sxs-lookup"><span data-stu-id="9deda-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="9deda-138">Clique com o botão direito do mouse em seu banco de dados no Gerenciador de Objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9deda-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="9deda-139">Selecione **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="9deda-139">Select **New Query**.</span></span> <span data-ttu-id="9deda-140">Uma nova janela de consulta é aberta.</span><span class="sxs-lookup"><span data-stu-id="9deda-140">A new query window opens.</span></span>
   
    ![Nova Consulta][4]
3. <span data-ttu-id="9deda-142">Copie esta consulta TSQL na janela de consulta hello:</span><span class="sxs-lookup"><span data-stu-id="9deda-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="9deda-143">Execute consulta hello.</span><span class="sxs-lookup"><span data-stu-id="9deda-143">Run hello query.</span></span> <span data-ttu-id="9deda-144">toodo, clique `Execute` ou use Olá atalho a seguir: `F5`.</span><span class="sxs-lookup"><span data-stu-id="9deda-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Executar consulta][5]
5. <span data-ttu-id="9deda-146">Examine os resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="9deda-146">Look at hello query results.</span></span> <span data-ttu-id="9deda-147">Neste exemplo, a tabela de FactInternetSales de saudação tem 60398 linhas.</span><span class="sxs-lookup"><span data-stu-id="9deda-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados da consulta][6]

## <a name="next-steps"></a><span data-ttu-id="9deda-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9deda-149">Next steps</span></span>
<span data-ttu-id="9deda-150">Agora que você pode se conectar e consultar, tente [visualizando dados Olá com PowerBI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="9deda-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="9deda-151">tooconfigure seu ambiente para a autenticação do Active Directory do Azure, consulte [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9deda-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
