---
title: "aaaManage computação power no Azure SQL Data Warehouse (PowerShell) | Microsoft Docs"
description: "Capacidade de computação toomanage de tarefas do PowerShell. Dimensionar recursos de computação ajustando as DWUs. Ou, pausar e retomar os custos de toosave de recursos de computação."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="107dc-105">Gerenciar poder de computação no SQL Data Warehouse do Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="107dc-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="107dc-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="107dc-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="107dc-107">Portal</span><span class="sxs-lookup"><span data-stu-id="107dc-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="107dc-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="107dc-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="107dc-109">REST</span><span class="sxs-lookup"><span data-stu-id="107dc-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="107dc-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="107dc-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="107dc-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="107dc-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="107dc-112">Instalar a versão mais recente de saudação do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="107dc-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="107dc-113">toouse PowerShell do Azure SQL Data warehouse, é necessário que o Azure PowerShell versão 1.0.3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="107dc-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="107dc-114">tooverify sua versão atual executar comando Olá **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="107dc-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="107dc-115">Você pode instalar a versão mais recente de saudação do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="107dc-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="107dc-116">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="107dc-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="107dc-117">Introdução aos cmdlets do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="107dc-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="107dc-118">tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="107dc-118">tooget started:</span></span>

1. <span data-ttu-id="107dc-119">Abra o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="107dc-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="107dc-120">No prompt do PowerShell Olá, execute esses comandos toosign em toohello do Azure Resource Manager e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="107dc-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="107dc-121">Dimensionar poder de computação</span><span class="sxs-lookup"><span data-stu-id="107dc-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="107dc-122">Olá toochange DWUs, use Olá [conjunto AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="107dc-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="107dc-123">Olá exemplo a seguir define serviço Olá nível tooDW1000 objetivo para banco de dados Olá MySQLDW que está hospedado no servidor MyServer.</span><span class="sxs-lookup"><span data-stu-id="107dc-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="107dc-124">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="107dc-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="107dc-125">toopause um banco de dados, use Olá [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="107dc-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="107dc-126">Olá exemplo a seguir faz uma pausa um banco de dados denominado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="107dc-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="107dc-127">em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="107dc-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="107dc-128">Observe que se o servidor for foo.database.windows.net, use "foo" como Olá - ServerName nos cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="107dc-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="107dc-129">Uma variação, o exemplo a seguir recupera o banco de dados de saudação em objeto Olá $database.</span><span class="sxs-lookup"><span data-stu-id="107dc-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="107dc-130">Ele canaliza objeto Olá muito[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="107dc-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="107dc-131">Olá resultados são armazenados em Olá resultDatabase de objeto.</span><span class="sxs-lookup"><span data-stu-id="107dc-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="107dc-132">comando final Olá mostra resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="107dc-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="107dc-133">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="107dc-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="107dc-134">toostart um banco de dados, use Olá [retomar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="107dc-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="107dc-135">Olá, exemplo a seguir inicia um banco de dados denominado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="107dc-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="107dc-136">em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="107dc-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="107dc-137">Uma variação, o exemplo a seguir recupera o banco de dados de saudação em objeto Olá $database.</span><span class="sxs-lookup"><span data-stu-id="107dc-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="107dc-138">Ele canaliza objeto Olá muito[retomar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] e armazena os resultados de saudação em $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="107dc-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="107dc-139">comando final Olá mostra resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="107dc-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="107dc-140">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="107dc-140">Check database state</span></span>

<span data-ttu-id="107dc-141">Conforme mostrado na Olá acima exemplos, é possível usar [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget informações em um banco de dados, assim, verificando o status hello, mas também toouse como um argumento.</span><span class="sxs-lookup"><span data-stu-id="107dc-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="107dc-142">O que resultará em algo parecido com isto</span><span class="sxs-lookup"><span data-stu-id="107dc-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="107dc-143">Onde você pode consultar Olá toosee *Status* de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="107dc-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="107dc-144">Nesse caso, é possível ver que esse banco de dados está online.</span><span class="sxs-lookup"><span data-stu-id="107dc-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="107dc-145">Ao executar esse comando, você deverá receber um valor de Status Online, Pausando, Retomando, Dimensionando e Pausado.</span><span class="sxs-lookup"><span data-stu-id="107dc-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="107dc-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="107dc-146">Next steps</span></span>
<span data-ttu-id="107dc-147">Para outras tarefas de gerenciamento, consulte [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="107dc-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
