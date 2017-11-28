---
title: Cmdlets do PowerShell para SQL Data Warehouse do Azure
description: Encontre os principais cmdlets do PowerShell para SQL Data Warehouse do Azure, inclusive sobre como pausar e retomar um banco de dados.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: ce3e11587c2e0cb92923868a4f26d7f59c7ef4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="fc56f-103">Cmdlets do PowerShell e as APIs REST para SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fc56f-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="fc56f-104">Diversas tarefas de administração do SQL Data Warehouse podem ser gerenciadas usando APIs REST ou cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc56f-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="fc56f-105">Abaixo estão alguns exemplos de como usar comandos do PowerShell para automatizar tarefas comuns no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fc56f-105">Below are some examples of how to use PowerShell commands to automate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="fc56f-106">Para obter alguns bons exemplos de REST, consulte o artigo [Gerenciar escalabilidade com REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="fc56f-106">For some good REST examples, see the article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="fc56f-107">Para usar o Azure PowerShell com o SQL Data Warehouse, você precisa do Azure PowerShell versão 1.0.3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="fc56f-107">In order to use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="fc56f-108">Você pode verificar a versão executando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="fc56f-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="fc56f-109">A versão mais recente pode ser instalada pelo [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="fc56f-109">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="fc56f-110">Para obter mais informações sobre como instalar a versão mais recente, consulte [Como instalar e configurar o Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="fc56f-110">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="fc56f-111">Introdução aos cmdlets do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc56f-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="fc56f-112">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc56f-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="fc56f-113">No prompt do PowerShell, execute estes comandos para entrar no Azure Resource Manager e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="fc56f-113">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="fc56f-114">Pausar Exemplo do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fc56f-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="fc56f-115">Pause um banco de dados denominado "Database02" hospedado em um servidor denominado "Server01."</span><span class="sxs-lookup"><span data-stu-id="fc56f-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="fc56f-116">O servidor está em um grupo de recursos do Azure denominado "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="fc56f-116">The server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="fc56f-117">Uma variação, esse exemplo redireciona o objeto recuperado para [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="fc56f-117">A variation, this example pipes the retrieved object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="fc56f-118">Como resultado, o banco de dados é pausado.</span><span class="sxs-lookup"><span data-stu-id="fc56f-118">As a result, the database is paused.</span></span> <span data-ttu-id="fc56f-119">O comando final mostra os resultados.</span><span class="sxs-lookup"><span data-stu-id="fc56f-119">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="fc56f-120">Iniciar Exemplo do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fc56f-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="fc56f-121">Retome a operação de um banco de dados denominado "Database02" hospedado em um servidor denominado "Server01."</span><span class="sxs-lookup"><span data-stu-id="fc56f-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="fc56f-122">O servidor está contido em um grupo de recursos denominado "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="fc56f-122">The server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="fc56f-123">Uma variação, este exemplo recupera um banco de dados denominado “Database02” de um servidor chamado “Server01” que está contido em um grupo de recursos denominado “ResourceGroup1”.</span><span class="sxs-lookup"><span data-stu-id="fc56f-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="fc56f-124">Ele canaliza o objeto recuperado para [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="fc56f-124">It pipes the retrieved object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="fc56f-125">Observe que, se o servidor for foo.database.windows.net, use "foo" como o -ServerName nos cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc56f-125">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="fc56f-126">Outros cmdlets do PowerShell com suporte</span><span class="sxs-lookup"><span data-stu-id="fc56f-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="fc56f-127">Esses cmdlets do PowerShell têm suporte com o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc56f-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="fc56f-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="fc56f-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="fc56f-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="fc56f-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="fc56f-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="fc56f-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="fc56f-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="fc56f-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="fc56f-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="fc56f-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="fc56f-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="fc56f-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="fc56f-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="fc56f-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc56f-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc56f-138">Next steps</span></span>
<span data-ttu-id="fc56f-139">Para obter mais exemplos do PowerShell, consulte:</span><span class="sxs-lookup"><span data-stu-id="fc56f-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="fc56f-140">[Criar um SQL Data Warehouse usando o PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fc56f-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="fc56f-141">[Restauração do banco de dados][Database restore]</span><span class="sxs-lookup"><span data-stu-id="fc56f-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="fc56f-142">Para outras tarefas que podem ser automatizadas com o PowerShell, consulte [Cmdlets do Banco de Dados SQL do Azure][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="fc56f-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="fc56f-143">Observe que nem todos os cmdlets de banco de dados SQL têm suporte do Azure SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc56f-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="fc56f-144">Para obter uma lista de tarefas que podem ser automatizadas com REST, consulte [Operações para Banco de Dados SQL do Azure][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="fc56f-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points to Select-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
