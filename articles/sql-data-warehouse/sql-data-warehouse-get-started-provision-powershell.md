---
title: aaaCreate SQL Data Warehouse usando o PowerShell | Microsoft Docs
description: Criar SQL Data Warehouse usando o PowerShell
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>Criar um SQL Data Warehouse usando o PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este artigo mostra como toocreate um SQL Data Warehouse usando o PowerShell.

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado, você precisa:

* **Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do Azure MSDN] [ MSDN Azure Credits] toocreate uma conta.
* **Servidor do SQL Azure**: consulte [criar um banco de dados do SQL Azure no hello Azure Portal] [ Create an Azure SQL database in hello Azure Portal] ou [criar um banco de dados do SQL Azure com o PowerShell] [ Create an Azure SQL database with PowerShell] para obter mais detalhes.
* **Grupo de recursos**: use Olá mesmo recurso de grupo como o servidor do SQL Azure ou consulte [como um grupo de recursos de toocreate](../azure-resource-manager/resource-group-portal.md).
* **PowerShell versão 1.0.3 ou superior**: você pode verificar a versão executando **Get-Module -ListAvailable -Name Azure**.  versão mais recente do Hello pode ser instalado do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Para obter mais informações sobre como instalar a versão mais recente do hello, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.  Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes sobre preços.
>
>

## <a name="create-a-sql-data-warehouse"></a>Criar um SQL Data Warehouse
1. Abra o Windows PowerShell.
2. Execute este tooAzure toologin do cmdlet Gerenciador de recursos.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Selecione a assinatura de saudação desejar toouse para sua sessão atual.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Criar banco de dados. Este exemplo cria um banco de dados denominado "mynewsqldw", com objetivo nível de serviço "DW400" toohello server chamado "sqldwserver1", que está no grupo de recursos de saudação chamado "mywesteuroperesgp1".

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Os parâmetros requeridos são:

* **RequestedServiceObjectiveName**: quantidade de saudação do [DWU] [ DWU] você está solicitando.  Os valores com suporte são: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 e DW6000.
* **DatabaseName**: nome de saudação do hello SQL Data Warehouse que você está criando.
* **ServerName**: nome de saudação do servidor de saudação que você está usando para a criação de (deve ser V12).
* **ResourceGroupName**: o grupo de recursos que você está usando.  toofind grupos de recursos disponíveis em sua assinatura usarem Get-AzureResource.
* **Edição**: deve ser "Data warehouse" toocreate um SQL Data Warehouse.

Os parâmetros opcionais são:

* **CollationName**: agrupamento padrão de saudação se não especificado é SQL_Latin1_General_CP1_CI_AS.  O agrupamento não pode ser alterado em um banco de dados.
* **MaxSizeBytes**: tamanho máximo do saudação padrão de um banco de dados é de 10 GB.

Para obter mais detalhes sobre as opções de parâmetro hello, consulte [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] e [criar banco de dados (SQL Azure Data Warehouse)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Próximas etapas
Após a Data Warehouse do SQL provisionamento, você pode desejar tootry [o carregamento de dados de exemplo] [ loading sample data] ou check-out como muito[desenvolver] [ develop] , [carregar][load], ou [migrar][migrate].

Se você estiver interessado em obter mais informações sobre como toomanage SQL Data Warehouse programaticamente, consulte nosso artigo sobre como toouse [cmdlets do PowerShell e APIs REST][PowerShell cmdlets and REST APIs].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
