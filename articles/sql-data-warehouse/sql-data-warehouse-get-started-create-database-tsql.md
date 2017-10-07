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
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Criar um banco de dados do SQL Data Warehouse usando TSQL (Transact-SQL)
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este artigo mostra como toocreate um SQL Data Warehouse usando o T-SQL.

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado, você precisa:

* **Conta do Azure**: visite [avaliação gratuita do Azure] [ Azure Free Trial] ou [créditos do Azure MSDN] [ MSDN Azure Credits] toocreate uma conta.
* **Servidor do SQL Azure**: consulte [criar um servidor lógico do banco de dados SQL com hello Portal do Azure] [criar um servidor lógico do banco de dados SQL com hello Portal do Azure] ou [criar um servidor lógico do banco de dados SQL com o PowerShell] [criar um SQL Azure Servidor lógico do banco de dados com o PowerShell] para obter mais detalhes.
* **Grupo de recursos**: use Olá mesmo recurso de grupo como o servidor do SQL Azure ou consulte [como um grupo de recursos de toocreate][how toocreate a resource group].
* **Ambiente tooexecute T-SQL**: você pode usar [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], ou [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.  Confira [Preços do SQL Data Warehouse][SQL Data Warehouse pricing] para obter mais detalhes sobre preços.
>
>

## <a name="create-a-database-with-visual-studio"></a>Criar um banco de dados com o Visual Studio
Se você for novo tooVisual Studio, consulte o artigo de saudação [consulta Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, abra o Pesquisador de objetos do SQL Server no Visual Studio e conecte-se toohello servidor que hospedará o banco de dados do SQL Data Warehouse.  Uma vez conectado, você pode criar um SQL Data Warehouse executando Olá após o comando SQL em relação a saudação **mestre** banco de dados.  Este comando cria o banco de dados Olá MySqlDwDb com um objetivo de serviço de DW400 e permitir Olá banco de dados toogrow tooa tamanho máximo de 10 TB.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Criar um banco de dados com sqlcmd
Como alternativa, você pode executar Olá mesmo comando com sqlcmd executando Olá a seguir no prompt de comando.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

agrupamento de padrão de saudação quando não especificado é o AGRUPAMENTO SQL_Latin1_General_CP1_CI_AS.  Olá `MAXSIZE` pode estar entre 250 GB e TB 240.  Olá `SERVICE_OBJECTIVE` pode estar entre DW100 e DW2000 [DWU][DWU].  Para obter uma lista de todos os valores válidos, consulte a documentação do MSDN Olá para [criar banco de dados][CREATE DATABASE].  Olá MAXSIZE e pode SERVICE_OBJECTIVE ser alterado com uma [ALTER DATABASE] [ ALTER DATABASE] comando T-SQL.  agrupamento de saudação do banco de dados não pode ser alterado após a criação.   Cuidado deve ser usado quando a alteração Olá SERVICE_OBJECTIVE como alterar DWU faz com que uma reinicialização de serviços, o que cancela todas as consultas em trânsito.  A alteração de MAXSIZE não reinicia os serviços, pois é apenas uma operação de metadados.

## <a name="next-steps"></a>Próximas etapas
Depois de Data Warehouse do SQL terminou de provisionamento pode [carregar dados de amostra] [ load sample data] ou check-out como muito[desenvolver][develop], [carregar][load], ou [migrar][migrate].

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
