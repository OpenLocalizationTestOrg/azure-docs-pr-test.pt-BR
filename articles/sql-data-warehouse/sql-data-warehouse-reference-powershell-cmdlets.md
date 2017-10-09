---
title: cmdlets de aaaPowerShell para o Azure SQL Data Warehouse
description: "Localizar Olá principais cmdlets do PowerShell para Azure SQL Data Warehouse incluindo como toopause e retomar um banco de dados."
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
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="1f0e3-103">Cmdlets do PowerShell e as APIs REST para SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1f0e3-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="1f0e3-104">Diversas tarefas de administração do SQL Data Warehouse podem ser gerenciadas usando APIs REST ou cmdlets do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="1f0e3-105">Abaixo estão alguns exemplos de como os comandos toouse PowerShell tooautomate a tarefas comuns no Data Warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="1f0e3-106">Para alguns bons exemplos REST, consulte o artigo Olá [gerenciar escalabilidade com REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="1f0e3-107">Em ordem toouse PowerShell do Azure SQL Data warehouse, é necessário que o Azure PowerShell versão 1.0.3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="1f0e3-108">Você pode verificar a versão executando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="1f0e3-109">versão mais recente do Hello pode ser instalado do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="1f0e3-110">Para obter mais informações sobre como instalar a versão mais recente do hello, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="1f0e3-111">Introdução aos cmdlets do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f0e3-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="1f0e3-112">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1f0e3-113">No prompt do PowerShell Olá, execute esses comandos toosign em toohello do Azure Resource Manager e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="1f0e3-114">Pausar Exemplo do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1f0e3-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="1f0e3-115">Pause um banco de dados denominado "Database02" hospedado em um servidor denominado "Server01."</span><span class="sxs-lookup"><span data-stu-id="1f0e3-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="1f0e3-116">servidor de saudação está em um grupo de recursos do Azure denominado "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="1f0e3-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="1f0e3-117">Uma variação, este exemplo redireciona Olá recuperado objeto muito[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="1f0e3-118">Como resultado, o banco de dados de saudação é pausado.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-118">As a result, hello database is paused.</span></span> <span data-ttu-id="1f0e3-119">comando final Olá mostra resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="1f0e3-120">Iniciar Exemplo do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1f0e3-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="1f0e3-121">Retome a operação de um banco de dados denominado "Database02" hospedado em um servidor denominado "Server01."</span><span class="sxs-lookup"><span data-stu-id="1f0e3-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="1f0e3-122">servidor de saudação está contido em um grupo de recursos denominado "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="1f0e3-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="1f0e3-123">Uma variação, este exemplo recupera um banco de dados denominado “Database02” de um servidor chamado “Server01” que está contido em um grupo de recursos denominado “ResourceGroup1”.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="1f0e3-124">Ele redireciona o objeto Olá recuperado muito[retomar AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="1f0e3-125">Observe que se o servidor for foo.database.windows.net, use "foo" como Olá - ServerName nos cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="1f0e3-126">Outros cmdlets do PowerShell com suporte</span><span class="sxs-lookup"><span data-stu-id="1f0e3-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="1f0e3-127">Esses cmdlets do PowerShell têm suporte com o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="1f0e3-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1f0e3-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="1f0e3-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="1f0e3-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1f0e3-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1f0e3-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1f0e3-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1f0e3-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="1f0e3-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="1f0e3-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f0e3-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f0e3-138">Next steps</span></span>
<span data-ttu-id="1f0e3-139">Para obter mais exemplos do PowerShell, consulte:</span><span class="sxs-lookup"><span data-stu-id="1f0e3-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="1f0e3-140">[Criar um SQL Data Warehouse usando o PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="1f0e3-141">[Restauração do banco de dados][Database restore]</span><span class="sxs-lookup"><span data-stu-id="1f0e3-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="1f0e3-142">Para outras tarefas que podem ser automatizadas com o PowerShell, consulte [Cmdlets do Banco de Dados SQL do Azure][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="1f0e3-143">Observe que nem todos os cmdlets de banco de dados SQL têm suporte do Azure SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f0e3-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="1f0e3-144">Para obter uma lista de tarefas que podem ser automatizadas com REST, consulte [Operações para Banco de Dados SQL do Azure][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="1f0e3-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
