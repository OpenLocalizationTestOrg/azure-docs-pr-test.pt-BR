---
title: aaaCreate um SQL Data Warehouse com TSQL | Microsoft Docs
description: Saiba como toocreate um Azure SQL Data Warehouse com TSQL
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
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="896ad-103">Criar um banco de dados do SQL Data Warehouse usando TSQL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="896ad-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="896ad-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="896ad-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="896ad-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="896ad-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="896ad-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="896ad-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="896ad-107">Este artigo mostra como toocreate um SQL Data Warehouse usando o T-SQL.</span><span class="sxs-lookup"><span data-stu-id="896ad-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="896ad-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="896ad-108">Prerequisites</span></span>
<span data-ttu-id="896ad-109">tooget iniciado, você precisa:</span><span class="sxs-lookup"><span data-stu-id="896ad-109">tooget started, you need:</span></span>

* <span data-ttu-id="896ad-110">**Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do Azure MSDN] [ MSDN Azure Credits] toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="896ad-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="896ad-111">**Servidor do SQL Azure**: consulte [criar um servidor lógico do banco de dados SQL com hello Portal do Azure] [criar um servidor lógico do banco de dados SQL com hello Portal do Azure] ou [criar um servidor lógico do banco de dados SQL com o PowerShell] [criar um SQL Azure Servidor lógico do banco de dados com o PowerShell] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="896ad-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="896ad-112">**Grupo de recursos**: use Olá mesmo recurso de grupo como o servidor do SQL Azure ou consulte [como um grupo de recursos de toocreate][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="896ad-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="896ad-113">**Ambiente tooexecute T-SQL**: você pode usar [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], ou [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="896ad-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="896ad-114">A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="896ad-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="896ad-115">Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes sobre preços.</span><span class="sxs-lookup"><span data-stu-id="896ad-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="896ad-116">Criar um banco de dados com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="896ad-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="896ad-117">Se você for novo tooVisual Studio, consulte o artigo de saudação [consulta Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="896ad-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="896ad-118">toostart, abra o Pesquisador de objetos do SQL Server no Visual Studio e conecte-se toohello servidor que hospedará o banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="896ad-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="896ad-119">Uma vez conectado, você pode criar um SQL Data Warehouse executando Olá após o comando SQL em relação a saudação **mestre** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="896ad-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="896ad-120">Este comando cria o banco de dados Olá MySqlDwDb com um objetivo de serviço de DW400 e permitir Olá banco de dados toogrow tooa tamanho máximo de 10 TB.</span><span class="sxs-lookup"><span data-stu-id="896ad-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="896ad-121">Criar um banco de dados com sqlcmd</span><span class="sxs-lookup"><span data-stu-id="896ad-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="896ad-122">Como alternativa, você pode executar Olá mesmo comando com sqlcmd executando Olá a seguir no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="896ad-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="896ad-123">agrupamento de padrão de saudação quando não especificado é o AGRUPAMENTO SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="896ad-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="896ad-124">Olá `MAXSIZE` pode estar entre 250 GB e TB 240.</span><span class="sxs-lookup"><span data-stu-id="896ad-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="896ad-125">Olá `SERVICE_OBJECTIVE` pode estar entre DW100 e DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="896ad-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="896ad-126">Para obter uma lista de todos os valores válidos, consulte a documentação do MSDN Olá para [criar banco de dados][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="896ad-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="896ad-127">Olá MAXSIZE e pode SERVICE_OBJECTIVE ser alterado com uma [ALTER DATABASE] [ ALTER DATABASE] comando T-SQL.</span><span class="sxs-lookup"><span data-stu-id="896ad-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="896ad-128">agrupamento de saudação do banco de dados não pode ser alterado após a criação.</span><span class="sxs-lookup"><span data-stu-id="896ad-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="896ad-129">Cuidado deve ser usado quando a alteração Olá SERVICE_OBJECTIVE como alterar DWU faz com que uma reinicialização de serviços, o que cancela todas as consultas em trânsito.</span><span class="sxs-lookup"><span data-stu-id="896ad-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="896ad-130">A alteração de MAXSIZE não reinicia os serviços, pois é apenas uma operação de metadados.</span><span class="sxs-lookup"><span data-stu-id="896ad-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="896ad-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="896ad-131">Next steps</span></span>
<span data-ttu-id="896ad-132">Depois de Data Warehouse do SQL terminou de provisionamento pode [carregar dados de amostra] [ load sample data] ou check-out como muito[desenvolver][develop], [carregar][load], ou [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="896ad-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
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
