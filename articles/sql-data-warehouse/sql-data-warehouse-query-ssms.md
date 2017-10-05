---
title: "Conectar-se ao SQL Data Warehouse do Azure – SSMS | Microsoft Docs"
description: Use o SQL Server Management Studio (SSMS) para conectar e consultar o SQL Data Warehouse.
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
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="e10be-103">Conectar-se ao SQL Data Warehouse com o SSMS (SQL Server Management Studio)</span><span class="sxs-lookup"><span data-stu-id="e10be-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e10be-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="e10be-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * <span data-ttu-id="e10be-105">
            [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="e10be-105">[Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)</span></span>
> * [<span data-ttu-id="e10be-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e10be-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="e10be-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="e10be-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="e10be-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="e10be-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="e10be-109">Use o SQL Server Management Studio (SSMS) para conectar e consultar o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e10be-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e10be-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e10be-110">Prerequisites</span></span>
<span data-ttu-id="e10be-111">Para usar este tutorial, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="e10be-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="e10be-112">Um SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="e10be-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="e10be-113">Para criar um, confira [Criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e10be-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="e10be-114">SSMS (SQL Server Management Studio) instalado.</span><span class="sxs-lookup"><span data-stu-id="e10be-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="e10be-115">[Instale o SSMS][Install SSMS] gratuitamente se você ainda não o tiver.</span><span class="sxs-lookup"><span data-stu-id="e10be-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="e10be-116">O nome de servidor SQL totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="e10be-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="e10be-117">Para encontrar isso, confira [Conectar-se ao SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e10be-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="e10be-118">1. Conectar-se ao SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e10be-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="e10be-119">Abra o SSMS.</span><span class="sxs-lookup"><span data-stu-id="e10be-119">Open SSMS.</span></span>
2. <span data-ttu-id="e10be-120">Abrir Pesquisador de Objetos.</span><span class="sxs-lookup"><span data-stu-id="e10be-120">Open Object Explorer.</span></span> <span data-ttu-id="e10be-121">Para fazer isso, selecione **Arquivo** > **Conectar Pesquisador de Objetos**.</span><span class="sxs-lookup"><span data-stu-id="e10be-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Pesquisador de Objetos do SQL Server][1]
3. <span data-ttu-id="e10be-123">Preencha os campos na janela Conectar ao Servidor.</span><span class="sxs-lookup"><span data-stu-id="e10be-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Conectar-se ao servidor][2]
   
   * <span data-ttu-id="e10be-125">**Nome do servidor**.</span><span class="sxs-lookup"><span data-stu-id="e10be-125">**Server name**.</span></span> <span data-ttu-id="e10be-126">Insira o **nome do servidor** identificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e10be-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="e10be-127">**Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="e10be-127">**Authentication**.</span></span> <span data-ttu-id="e10be-128">Selecione **Autenticação do SQL Server** ou **Autenticação Integrada do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e10be-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="e10be-129">**Nome de Usuário** e **Senha**.</span><span class="sxs-lookup"><span data-stu-id="e10be-129">**User Name** and **Password**.</span></span> <span data-ttu-id="e10be-130">Insira o nome de usuário e senha se a Autenticação do SQL Server foi selecionada acima.</span><span class="sxs-lookup"><span data-stu-id="e10be-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="e10be-131">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="e10be-131">Click **Connect**.</span></span>
4. <span data-ttu-id="e10be-132">Para explorar, expanda seu servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e10be-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="e10be-133">Você pode exibir os bancos de dados associados ao servidor.</span><span class="sxs-lookup"><span data-stu-id="e10be-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="e10be-134">Expanda o AdventureWorksDW para ver as tabelas no banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e10be-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explorar o AdventureWorksWeb][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="e10be-136">2. Executar uma consulta de exemplo</span><span class="sxs-lookup"><span data-stu-id="e10be-136">2. Run a sample query</span></span>
<span data-ttu-id="e10be-137">Agora que uma conexão foi estabelecida com o banco de dados, escreveremos uma consulta.</span><span class="sxs-lookup"><span data-stu-id="e10be-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="e10be-138">Clique com o botão direito do mouse em seu banco de dados no Gerenciador de Objetos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e10be-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="e10be-139">Selecione **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="e10be-139">Select **New Query**.</span></span> <span data-ttu-id="e10be-140">Uma nova janela de consulta é aberta.</span><span class="sxs-lookup"><span data-stu-id="e10be-140">A new query window opens.</span></span>
   
    ![Nova Consulta][4]
3. <span data-ttu-id="e10be-142">Copie esta consulta TSQL na janela de consulta:</span><span class="sxs-lookup"><span data-stu-id="e10be-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="e10be-143">Execute a consulta.</span><span class="sxs-lookup"><span data-stu-id="e10be-143">Run the query.</span></span> <span data-ttu-id="e10be-144">Para fazer isso, clique em `Execute` ou use o atalho a seguir: `F5`.</span><span class="sxs-lookup"><span data-stu-id="e10be-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![Executar consulta][5]
5. <span data-ttu-id="e10be-146">Examine os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="e10be-146">Look at the query results.</span></span> <span data-ttu-id="e10be-147">Neste exemplo, a tabela FactInternetSales tem 60398 linhas.</span><span class="sxs-lookup"><span data-stu-id="e10be-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Resultados da consulta][6]

## <a name="next-steps"></a><span data-ttu-id="e10be-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e10be-149">Next steps</span></span>
<span data-ttu-id="e10be-150">Agora que você pode se conectar e consultar, tente [visualizar os dados com o PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="e10be-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="e10be-151">Para configurar seu ambiente para a autenticação do Azure Active Directory, confira [Autenticar no SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e10be-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
