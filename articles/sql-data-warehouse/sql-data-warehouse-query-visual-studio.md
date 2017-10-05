---
title: Conectar-se ao SQL Data Warehouse do Azure - VSTS | Microsoft Docs
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
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="35265-103">Conectar-se ao SQL Data Warehouse com o Visual Studio e o SSDT</span><span class="sxs-lookup"><span data-stu-id="35265-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35265-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="35265-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="35265-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="35265-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="35265-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35265-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="35265-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="35265-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="35265-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="35265-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="35265-109">Use o Visual Studio para consultar o SQL Data Warehouse do Azure em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="35265-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="35265-110">Esse método usa a extensão SSDT (SQL Server Data Tools) no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35265-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="35265-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="35265-111">Prerequisites</span></span>
<span data-ttu-id="35265-112">Para usar este tutorial, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="35265-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="35265-113">Um SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="35265-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="35265-114">Para criar um, confira [Criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="35265-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="35265-115">SSDT para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35265-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="35265-116">Se você tiver o Visual Studio, provavelmente já terá isso.</span><span class="sxs-lookup"><span data-stu-id="35265-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="35265-117">Para obter instruções e opções de instalação, confira [Instalar o Visual Studio e o SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="35265-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="35265-118">O nome de servidor SQL totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="35265-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="35265-119">Para encontrar isso, confira [Conectar-se ao SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="35265-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="35265-120">1. Conectar-se ao SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35265-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="35265-121">Abra o Visual Studio 2013 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="35265-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="35265-122">Abra o Pesquisador de Objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="35265-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="35265-123">Para fazer isso, selecione **Exibir** > **Pesquisador de Objetos do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="35265-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Pesquisador de Objetos do SQL Server][1]
3. <span data-ttu-id="35265-125">Clique no ícone **Adicionar SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="35265-125">Click the **Add SQL Server** icon.</span></span>
   
    ![Adicionar SQL Server][2]
4. <span data-ttu-id="35265-127">Preencha os campos na janela Conectar ao Servidor.</span><span class="sxs-lookup"><span data-stu-id="35265-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Conectar-se ao servidor][3]
   
   * <span data-ttu-id="35265-129">**Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="35265-129">**Server name**.</span></span> <span data-ttu-id="35265-130">Insira o **nome do servidor** identificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="35265-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="35265-131">**Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="35265-131">**Authentication**.</span></span> <span data-ttu-id="35265-132">Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="35265-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="35265-133">**Nome de Usuário** e **Senha**.</span><span class="sxs-lookup"><span data-stu-id="35265-133">**User Name** and **Password**.</span></span> <span data-ttu-id="35265-134">Insira o nome de usuário e senha se a Autenticação do SQL Server foi selecionada acima.</span><span class="sxs-lookup"><span data-stu-id="35265-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="35265-135">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="35265-135">Click **Connect**.</span></span>
5. <span data-ttu-id="35265-136">Para explorar, expanda seu servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="35265-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="35265-137">Você pode exibir os bancos de dados associados ao servidor.</span><span class="sxs-lookup"><span data-stu-id="35265-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="35265-138">Expanda o AdventureWorksDW para ver as tabelas no banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="35265-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explorar o AdventureWorksWeb][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="35265-140">2. Executar uma consulta de exemplo</span><span class="sxs-lookup"><span data-stu-id="35265-140">2. Run a sample query</span></span>
<span data-ttu-id="35265-141">Agora que uma conexão foi estabelecida com o banco de dados, escreveremos uma consulta.</span><span class="sxs-lookup"><span data-stu-id="35265-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="35265-142">Clique com o botão direito do mouse em seu banco de dados no Gerenciador de Objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="35265-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="35265-143">Selecione **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="35265-143">Select **New Query**.</span></span> <span data-ttu-id="35265-144">Uma nova janela de consulta é aberta.</span><span class="sxs-lookup"><span data-stu-id="35265-144">A new query window opens.</span></span>
   
    ![Nova Consulta][5]
3. <span data-ttu-id="35265-146">Copie esta consulta TSQL na janela de consulta:</span><span class="sxs-lookup"><span data-stu-id="35265-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="35265-147">Execute a consulta.</span><span class="sxs-lookup"><span data-stu-id="35265-147">Run the query.</span></span> <span data-ttu-id="35265-148">Para fazer isso, clique na seta verde ou use este atalho: `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="35265-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Executar consulta][6]
5. <span data-ttu-id="35265-150">Examine os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="35265-150">Look at the query results.</span></span> <span data-ttu-id="35265-151">Neste exemplo, a tabela FactInternetSales tem 60398 linhas.</span><span class="sxs-lookup"><span data-stu-id="35265-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados da consulta][7]

## <a name="next-steps"></a><span data-ttu-id="35265-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35265-153">Next steps</span></span>
<span data-ttu-id="35265-154">Agora que você pode se conectar e consultar, tente [visualizar os dados com o PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="35265-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="35265-155">Para configurar seu ambiente para a autenticação do Azure Active Directory, confira [Autenticar no SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="35265-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
