---
title: "Gerenciar potência de computação no SQL Data Warehouse do Azure (PowerShell) | Microsoft Docs"
description: "Tarefas do PowerShell para gerenciar o poder de computação. Dimensionar recursos de computação ajustando as DWUs. Ou, para economizar custos, pause e retome os recursos de computação."
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
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="c6c3f-105">Gerenciar poder de computação no SQL Data Warehouse do Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c6c3f-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6c3f-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c6c3f-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="c6c3f-107">Portal</span><span class="sxs-lookup"><span data-stu-id="c6c3f-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="c6c3f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c3f-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="c6c3f-109">REST</span><span class="sxs-lookup"><span data-stu-id="c6c3f-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="c6c3f-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="c6c3f-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="c6c3f-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c6c3f-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="c6c3f-112">Instale a versão mais recente do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c3f-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c6c3f-113">Para usar o Azure PowerShell com o SQL Data Warehouse, você precisa instalar a versão 1.0.3 ou superior do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="c6c3f-114">Para verificar a versão atual, execute o comando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="c6c3f-115">Você pode instalar a versão mais recente do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="c6c3f-116">Para saber mais, consulte [Como instalar e configurar o Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="c6c3f-117">Introdução aos cmdlets do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c3f-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="c6c3f-118">Introdução:</span><span class="sxs-lookup"><span data-stu-id="c6c3f-118">To get started:</span></span>

1. <span data-ttu-id="c6c3f-119">Abra o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="c6c3f-120">No prompt do PowerShell, execute estes comandos para entrar no Azure Resource Manager e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="c6c3f-121">Dimensionar poder de computação</span><span class="sxs-lookup"><span data-stu-id="c6c3f-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="c6c3f-122">Para alterar as DWUs, use o cmdlet do PowerShell [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="c6c3f-123">O exemplo a seguir define o objetivo de nível de serviço como DW1000 para o banco de dados MySQLDW, que está hospedado no servidor MyServer.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="c6c3f-124">Pausar computação</span><span class="sxs-lookup"><span data-stu-id="c6c3f-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="c6c3f-125">Para pausar um banco de dados, use o cmdlet [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="c6c3f-126">O exemplo a seguir pausa um banco de dados chamado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="c6c3f-127">O servidor está em um grupo de recursos do Azure chamado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c3f-128">Observe que, se o servidor for foo.database.windows.net, use "foo" como o -ServerName nos cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="c6c3f-129">Uma variação, o próximo exemplo recupera o banco de dados para o objeto $database.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="c6c3f-130">Ele redireciona o objeto para [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="c6c3f-131">Os resultados são armazenados no objeto resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="c6c3f-132">O comando final mostra os resultados.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="c6c3f-133">Retomar a computação</span><span class="sxs-lookup"><span data-stu-id="c6c3f-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="c6c3f-134">Para iniciar um banco de dados, use o cmdlet [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="c6c3f-135">O exemplo a seguir inicia um banco de dados chamado Database02 hospedado em um servidor chamado Server01.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="c6c3f-136">O servidor está em um grupo de recursos do Azure chamado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="c6c3f-137">Uma variação, o próximo exemplo recupera o banco de dados para o objeto $database.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="c6c3f-138">Ele redireciona o objeto para [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] e armazena os resultados em $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="c6c3f-139">O comando final mostra os resultados.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="c6c3f-140">Verificar estado do banco de dados</span><span class="sxs-lookup"><span data-stu-id="c6c3f-140">Check database state</span></span>

<span data-ttu-id="c6c3f-141">Conforme mostrado nos exemplos acima, você pode usar o cmdlet [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] para obter informações sobre um banco de dados, verificando assim o status, e também usá-lo como um argumento.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="c6c3f-142">O que resultará em algo parecido com isto</span><span class="sxs-lookup"><span data-stu-id="c6c3f-142">Which will result in something like</span></span> 

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

<span data-ttu-id="c6c3f-143">Em que você pode clicar para ver o *Status* do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="c6c3f-144">Nesse caso, é possível ver que esse banco de dados está online.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="c6c3f-145">Ao executar esse comando, você deverá receber um valor de Status Online, Pausando, Retomando, Dimensionando e Pausado.</span><span class="sxs-lookup"><span data-stu-id="c6c3f-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="c6c3f-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6c3f-146">Next steps</span></span>
<span data-ttu-id="c6c3f-147">Para outras tarefas de gerenciamento, consulte [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="c6c3f-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
