---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Microsoft Docs
description: Consultar o SQL Data Warehouse com o Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="a0f47-103">Conecte-se tooSQL Data Warehouse com o Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="a0f47-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0f47-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="a0f47-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="a0f47-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="a0f47-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="a0f47-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0f47-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="a0f47-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="a0f47-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="a0f47-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="a0f47-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="a0f47-109">Use o Visual Studio tooquery Azure SQL Data Warehouse em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a0f47-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="a0f47-110">Esse método usa a extensão do SQL Server Data Tools (SSDT) Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0f47-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a0f47-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a0f47-111">Prerequisites</span></span>
<span data-ttu-id="a0f47-112">toouse neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="a0f47-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="a0f47-113">Um SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="a0f47-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="a0f47-114">toocreate um, consulte [criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a0f47-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="a0f47-115">SSDT para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0f47-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="a0f47-116">Se você tiver o Visual Studio, provavelmente já terá isso.</span><span class="sxs-lookup"><span data-stu-id="a0f47-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="a0f47-117">Para obter instruções e opções de instalação, confira [Instalar o Visual Studio e o SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="a0f47-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="a0f47-118">Olá totalmente qualificado o nome do SQL server.</span><span class="sxs-lookup"><span data-stu-id="a0f47-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="a0f47-119">toofind isso, consulte [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a0f47-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="a0f47-120">1. Conecte-se tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a0f47-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="a0f47-121">Abra o Visual Studio 2013 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="a0f47-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="a0f47-122">Abra o Pesquisador de Objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a0f47-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="a0f47-123">toodo, selecione **exibição** > **Pesquisador de objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Pesquisador de Objetos do SQL Server][1]
3. <span data-ttu-id="a0f47-125">Clique em Olá **adicionar SQL Server** ícone.</span><span class="sxs-lookup"><span data-stu-id="a0f47-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Adicionar SQL Server][2]
4. <span data-ttu-id="a0f47-127">Preencha os campos de saudação na janela de tooServer conectar hello.</span><span class="sxs-lookup"><span data-stu-id="a0f47-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Conecte-se tooServer][3]
   
   * <span data-ttu-id="a0f47-129">**Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-129">**Server name**.</span></span> <span data-ttu-id="a0f47-130">Digite hello **nome do servidor** identificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a0f47-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="a0f47-131">**Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-131">**Authentication**.</span></span> <span data-ttu-id="a0f47-132">Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="a0f47-133">**Nome de Usuário** e **Senha**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-133">**User Name** and **Password**.</span></span> <span data-ttu-id="a0f47-134">Insira o nome de usuário e senha se a Autenticação do SQL Server foi selecionada acima.</span><span class="sxs-lookup"><span data-stu-id="a0f47-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="a0f47-135">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-135">Click **Connect**.</span></span>
5. <span data-ttu-id="a0f47-136">tooexplore, expanda seu servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0f47-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="a0f47-137">Você pode exibir bancos de dados de saudação associados ao servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0f47-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="a0f47-138">Expanda as tabelas de saudação do AdventureWorksDW toosee em seu banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a0f47-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorar o AdventureWorksWeb][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="a0f47-140">2. Executar uma consulta de exemplo</span><span class="sxs-lookup"><span data-stu-id="a0f47-140">2. Run a sample query</span></span>
<span data-ttu-id="a0f47-141">Agora que uma conexão foi estabelecida tooyour banco de dados, vamos escrever uma consulta.</span><span class="sxs-lookup"><span data-stu-id="a0f47-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="a0f47-142">Clique com o botão direito do mouse em seu banco de dados no Gerenciador de Objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a0f47-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="a0f47-143">Selecione **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="a0f47-143">Select **New Query**.</span></span> <span data-ttu-id="a0f47-144">Uma nova janela de consulta é aberta.</span><span class="sxs-lookup"><span data-stu-id="a0f47-144">A new query window opens.</span></span>
   
    ![Nova Consulta][5]
3. <span data-ttu-id="a0f47-146">Copie esta consulta TSQL na janela de consulta hello:</span><span class="sxs-lookup"><span data-stu-id="a0f47-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="a0f47-147">Execute consulta hello.</span><span class="sxs-lookup"><span data-stu-id="a0f47-147">Run hello query.</span></span> <span data-ttu-id="a0f47-148">toodo isso, clique em seta Olá verde ou use Olá atalho a seguir: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="a0f47-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Executar consulta][6]
5. <span data-ttu-id="a0f47-150">Examine os resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="a0f47-150">Look at hello query results.</span></span> <span data-ttu-id="a0f47-151">Neste exemplo, a tabela de FactInternetSales de saudação tem 60398 linhas.</span><span class="sxs-lookup"><span data-stu-id="a0f47-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados da consulta][7]

## <a name="next-steps"></a><span data-ttu-id="a0f47-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0f47-153">Next steps</span></span>
<span data-ttu-id="a0f47-154">Agora que você pode se conectar e consultar, tente [visualizando dados Olá com PowerBI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="a0f47-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="a0f47-155">tooconfigure seu ambiente para a autenticação do Active Directory do Azure, consulte [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a0f47-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
