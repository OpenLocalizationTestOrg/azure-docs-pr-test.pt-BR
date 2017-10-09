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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Gerenciar poder de computação no SQL Data Warehouse do Azure (PowerShell)
> [!div class="op_single_selector"]
> * [Visão geral](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>Antes de começar
### <a name="install-hello-latest-version-of-azure-powershell"></a>Instalar a versão mais recente de saudação do PowerShell do Azure
> [!NOTE]
> toouse PowerShell do Azure SQL Data warehouse, é necessário que o Azure PowerShell versão 1.0.3 ou superior.  tooverify sua versão atual executar comando Olá **Get-Module - ListAvailable-Name Azure**. Você pode instalar a versão mais recente de saudação do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Introdução aos cmdlets do Azure PowerShell
tooget iniciado:

1. Abra o PowerShell do Azure.
2. No prompt do PowerShell Olá, execute esses comandos toosign em toohello do Azure Resource Manager e selecione sua assinatura.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Dimensionar poder de computação
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Olá toochange DWUs, use Olá [conjunto AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] cmdlet do PowerShell. Olá exemplo a seguir define serviço Olá nível tooDW1000 objetivo para banco de dados Olá MySQLDW que está hospedado no servidor MyServer.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Pausar computação
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause um banco de dados, use Olá [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet. Olá exemplo a seguir faz uma pausa um banco de dados denominado Database02 hospedado em um servidor chamado Server01. em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.

> [!NOTE]
> Observe que se o servidor for foo.database.windows.net, use "foo" como Olá - ServerName nos cmdlets do PowerShell hello.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
Uma variação, o exemplo a seguir recupera o banco de dados de saudação em objeto Olá $database. Ele canaliza objeto Olá muito[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]. Olá resultados são armazenados em Olá resultDatabase de objeto. comando final Olá mostra resultados de saudação.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Retomar a computação
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart um banco de dados, use Olá [retomar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet. Olá, exemplo a seguir inicia um banco de dados denominado Database02 hospedado em um servidor chamado Server01. em um grupo de recursos do Azure, o servidor de saudação é denominado ResourceGroup1.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

Uma variação, o exemplo a seguir recupera o banco de dados de saudação em objeto Olá $database. Ele canaliza objeto Olá muito[retomar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] e armazena os resultados de saudação em $resultDatabase. comando final Olá mostra resultados de saudação.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>Verificar estado do banco de dados

Conforme mostrado na Olá acima exemplos, é possível usar [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget informações em um banco de dados, assim, verificando o status hello, mas também toouse como um argumento. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

O que resultará em algo parecido com isto 

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

Onde você pode consultar Olá toosee *Status* de banco de dados de saudação. Nesse caso, é possível ver que esse banco de dados está online. 

Ao executar esse comando, você deverá receber um valor de Status Online, Pausando, Retomando, Dimensionando e Pausado.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Próximas etapas
Para outras tarefas de gerenciamento, consulte [Visão geral de gerenciamento][Management overview].

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
