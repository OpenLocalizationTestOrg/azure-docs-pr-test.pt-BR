---
title: dados de aaaLoad do SQL Server no Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: "Usa bcp tooexport dados de arquivos de tooflat do SQL Server, o armazenamento de blob do AZCopy tooimport dados tooAzure e dados Olá tooingest no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a>Carregar dados do SQL Server no Azure SQL Data Warehouse (AZCopy)
Usar o bcp e dados de tooload AZCopy utilitários de linha de comando do SQL Server tooAzure do armazenamento de blob. Use dados de saudação tooload PolyBase ou fábrica de dados do Azure no Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Pré-requisitos
toostep este tutorial, você precisa:

* Um banco de dados do SQL Data Warehouse.
* Utilitário de linha de comando bcp Olá instalado
* Olá utilitário de linha de comando SQLCMD instalado

> [!NOTE]
> Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Importar dados no SQL Data Warehouse
Neste tutorial, você criará uma tabela no Azure SQL Data Warehouse e importar dados em tabela hello.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Etapa 1: Criar uma tabela no SQL Data Warehouse do Azure
Em um prompt de comando, use sqlcmd toorun Olá toocreate consulta uma tabela a seguir na instância do:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> Consulte [visão geral da tabela] [ Table Overview] ou [sintaxe CREATE TABLE] [ CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e hello  opções disponíveis na cláusula WITH de saudação.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Etapa 2: Criar um arquivo de dados de origem
Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo de texto e, em seguida, salvar esse arquivo tooyour local diretório temp, C:\Temp\DimDate2.txt.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> É importante tooremember que bcp.exe não oferece suporte para a codificação do arquivo hello UTF-8. Use arquivos ASCII ou arquivos codificados em UTF-16 ao usar o bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Etapa 3: Conectar e importar dados de saudação
Usando o bcp, você pode conectar e importar dados de saudação usando Olá a seguir substituindo valores de saudação comando conforme apropriado:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Você pode verificar Olá dados foram carregados executando hello usando o sqlcmd de consulta a seguir:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Isso deve retornar Olá resultados a seguir:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Etapa 4: criar estatísticas sobre os dados recém-carregados
O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática. Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação. Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos. Abaixo está um exemplo rápido de como toocreate estatísticas na tabela de saudação carregados neste exemplo

Execute Olá seguindo as instruções CREATE STATISTICS em um prompt de sqlcmd:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Exportar dados do SQL Data Warehouse
Neste tutorial, você criará um arquivo de dados de uma tabela no SQL Data Warehouse. Podemos exporta os dados de saudação que criamos acima tooa novo arquivo de dados chamado DimDate2_export.txt.

### <a name="step-1-export-hello-data"></a>Etapa 1: Exportar dados de saudação
Usando o utilitário bcp de saudação, você pode se conectar e exportar dados usando Olá a seguir substituindo valores de saudação comando conforme apropriado:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Você pode verificar Olá dados foram exportados corretamente abrindo novo arquivo de saudação. dados Olá no arquivo hello devem coincidir com o texto de saudação abaixo:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> Devido a natureza toohello dos sistemas distribuídos, ordem de saudação de dados não pode ser Olá mesmo em bancos de dados do SQL Data Warehouse. Outra opção é Olá toouse **queryout** função de bcp toowrite uma consulta extrair, em vez de exportar a tabela inteira hello.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].
Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
