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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>Cmdlets do PowerShell e as APIs REST para SQL Data Warehouse
Diversas tarefas de administração do SQL Data Warehouse podem ser gerenciadas usando APIs REST ou cmdlets do Azure PowerShell.  Abaixo estão alguns exemplos de como os comandos toouse PowerShell tooautomate a tarefas comuns no Data Warehouse do SQL.  Para alguns bons exemplos REST, consulte o artigo Olá [gerenciar escalabilidade com REST][Manage scalability with REST].

> [!NOTE]
> Em ordem toouse PowerShell do Azure SQL Data warehouse, é necessário que o Azure PowerShell versão 1.0.3 ou superior.  Você pode verificar a versão executando **Get-Module -ListAvailable -Name Azure**.  versão mais recente do Hello pode ser instalado do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Para obter mais informações sobre como instalar a versão mais recente do hello, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Introdução aos cmdlets do Azure PowerShell
1. Abra o Windows PowerShell.
2. No prompt do PowerShell Olá, execute esses comandos toosign em toohello do Azure Resource Manager e selecione sua assinatura.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Pausar Exemplo do SQL Data Warehouse
Pause um banco de dados denominado "Database02" hospedado em um servidor denominado "Server01."  servidor de saudação está em um grupo de recursos do Azure denominado "ResourceGroup1".

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Uma variação, este exemplo redireciona Olá recuperado objeto muito[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  Como resultado, o banco de dados de saudação é pausado. comando final Olá mostra resultados de saudação.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Iniciar Exemplo do SQL Data Warehouse
Retome a operação de um banco de dados denominado "Database02" hospedado em um servidor denominado "Server01." servidor de saudação está contido em um grupo de recursos denominado "ResourceGroup1".

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Uma variação, este exemplo recupera um banco de dados denominado “Database02” de um servidor chamado “Server01” que está contido em um grupo de recursos denominado “ResourceGroup1”. Ele redireciona o objeto Olá recuperado muito[retomar AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Observe que se o servidor for foo.database.windows.net, use "foo" como Olá - ServerName nos cmdlets do PowerShell hello.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Outros cmdlets do PowerShell com suporte
Esses cmdlets do PowerShell têm suporte com o SQL Data Warehouse do Azure.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Próximas etapas
Para obter mais exemplos do PowerShell, consulte:

* [Criar um SQL Data Warehouse usando o PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Restauração do banco de dados][Database restore]

Para outras tarefas que podem ser automatizadas com o PowerShell, consulte [Cmdlets do Banco de Dados SQL do Azure][Azure SQL Database Cmdlets]. Observe que nem todos os cmdlets de banco de dados SQL têm suporte do Azure SQL Data Warehouse do Azure.  Para obter uma lista de tarefas que podem ser automatizadas com REST, consulte [Operações para Banco de Dados SQL do Azure][Operations for Azure SQL Databases].

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
