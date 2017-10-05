---
title: Criar um SQL Data Warehouse com o TSQL | Microsoft Docs
description: Saiba como criar um SQL Data Warehouse do Azure com o TSQL
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 10d8aa2b3ab8d7d8a9b91e95ffccf03faa89d237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="d6b72-103">Criar um banco de dados do SQL Data Warehouse usando TSQL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="d6b72-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6b72-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d6b72-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="d6b72-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="d6b72-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="d6b72-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6b72-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="d6b72-107">Este artigo mostra como criar um SQL Data Warehouse usando o T-SQL.</span><span class="sxs-lookup"><span data-stu-id="d6b72-107">This article shows you how to create a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b72-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6b72-108">Prerequisites</span></span>
<span data-ttu-id="d6b72-109">Para começar, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6b72-109">To get started, you need:</span></span>

* <span data-ttu-id="d6b72-110">**Conta do Azure**: visite [Avaliação gratuita do Azure][Azure Free Trial] ou [Créditos do Azure no MSDN][MSDN Azure Credits] para criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="d6b72-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="d6b72-111">**Servidor do SQL Azure**: consulte [criar um servidor lógico do banco de dados SQL com o Portal do Azure] [criar um servidor lógico do banco de dados SQL com o Portal do Azure] ou [criar um servidor lógico do banco de dados SQL com o PowerShell] [criar um SQL Azure Servidor lógico do banco de dados com o PowerShell] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6b72-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with the Azure Portal][Create an Azure SQL Database logical server with the Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="d6b72-112">**Grupo de recursos**: use o mesmo grupo de recursos do servidor SQL do Azure ou veja [como criar um grupo de recursos][how to create a resource group].</span><span class="sxs-lookup"><span data-stu-id="d6b72-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group][how to create a resource group].</span></span>
* <span data-ttu-id="d6b72-113">**Ambiente para executar o T-SQL**: você pode usar o [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd] ou [SSMS][SSMS] para executar o T-SQL.</span><span class="sxs-lookup"><span data-stu-id="d6b72-113">**Environment to execute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] to execute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="d6b72-114">A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="d6b72-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="d6b72-115">Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes sobre preços.</span><span class="sxs-lookup"><span data-stu-id="d6b72-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="d6b72-116">Criar um banco de dados com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6b72-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="d6b72-117">Se você for novo no Visual Studio, confira o artigo [Consultar o Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="d6b72-117">If you are new to Visual Studio, see the article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="d6b72-118">Para começar, abra o Pesquisador de Objetos do SQL Server no Visual Studio e conecte-se ao servidor que hospedará seu banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d6b72-118">To start, open SQL Server Object Explorer in Visual Studio and connect to the server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="d6b72-119">Quando estiver conectado, você poderá criar um SQL Data Warehouse executando o seguinte comando SQL no banco de dados **mestre** .</span><span class="sxs-lookup"><span data-stu-id="d6b72-119">Once connected, you can create a SQL Data Warehouse by running the following SQL command against the **master** database.</span></span>  <span data-ttu-id="d6b72-120">Este comando cria o banco de dados MySqlDwDb com um Objetivo de Serviço de DW400 e permite que o banco de dados aumente até um tamanho máximo de 10 TB.</span><span class="sxs-lookup"><span data-stu-id="d6b72-120">This command creates the database MySqlDwDb with a Service Objective of DW400 and allow the database to grow to a maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="d6b72-121">Criar um banco de dados com sqlcmd</span><span class="sxs-lookup"><span data-stu-id="d6b72-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="d6b72-122">Como alternativa, você pode executar o mesmo comando com sqlcmd executando o seguinte em um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="d6b72-122">Alternatively, you can run the same command with sqlcmd by running the following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="d6b72-123">O agrupamento padrão quando não especificado é COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="d6b72-123">The default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="d6b72-124">O `MAXSIZE` pode ter entre 250 GB e 240 TB.</span><span class="sxs-lookup"><span data-stu-id="d6b72-124">The `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="d6b72-125">O `SERVICE_OBJECTIVE` pode estar entre DW100 e DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="d6b72-125">The `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="d6b72-126">Para obter uma lista de todos os valores válidos, confira a documentação do MSDN para [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="d6b72-126">For a list of all valid values, see the MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="d6b72-127">MAXSIZE e SERVICE_OBJECTIVE podem ser alterados com um comando T-SQL [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="d6b72-127">Both the MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="d6b72-128">O agrupamento de um banco de dados não pode ser alterado após a criação.</span><span class="sxs-lookup"><span data-stu-id="d6b72-128">The collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="d6b72-129">É necessário ter cuidado ao alterar o SERVICE_OBJECTIVE, pois alterar um DWU causa uma reinicialização dos serviços, cancelando todas as consultas em trânsito.</span><span class="sxs-lookup"><span data-stu-id="d6b72-129">Caution should be used when changing the SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="d6b72-130">A alteração de MAXSIZE não reinicia os serviços, pois é apenas uma operação de metadados.</span><span class="sxs-lookup"><span data-stu-id="d6b72-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6b72-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6b72-131">Next steps</span></span>
<span data-ttu-id="d6b72-132">Após o provisionamento do SQL Data Warehouse, você pode [carregar dados de exemplo][load sample data] ou conferir como [desenvolvê-los][develop], [carregar][load] ou [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="d6b72-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how to create a SQL Data Warehouse from the Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
