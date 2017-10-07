---
title: dados de aaaLoad do SQL Server no Azure SQL Data Warehouse (bcp) | Microsoft Docs
description: "Para um tamanho de dados pequeno, usa bcp tooexport dados de arquivos do SQL Server tooflat e importar dados de saudação diretamente no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Carregar dados do SQL Server no Azure SQL Data Warehouse (arquivos simples)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Para pequenos conjuntos de dados, você pode usar Olá de utilitário de linha de comando bcp tooexport a dados do SQL Server e, em seguida, carregá-lo diretamente tooAzure SQL Data Warehouse.

Neste tutorial, você usará o bcp para:

* Exporte uma tabela a partir do SQL Server usando o bcp Olá comando (ou crie um arquivo de exemplo simples)
* Importar tabela de saudação do tooSQL arquivo simples do Data Warehouse.
* Crie estatísticas nos dados carregado de saudação.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Antes de começar
### <a name="prerequisites"></a>Pré-requisitos
toostep este tutorial, você precisa:

* Um banco de dados do SQL Data Warehouse.
* Utilitário de linha de comando do bcp Olá instalado
* Utilitário de linha de comando do sqlcmd Olá instalado

Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dados em formato ASCII ou UTF-16
Se você estiver tentando neste tutorial com seus próprios dados, os dados precisarem toouse Olá ASCII ou codificação UTF-16 como bcp não oferece suporte a UTF-8. 

O PolyBase oferece suporte a UTF-8, mas ainda não oferece suporte a UTF-16. Observe que se você quiser toocombine bcp com PolyBase você precisará tootransform Olá dados tooUTF-8 depois de ser exportado do SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Criar uma tabela de destino
Defina uma tabela no SQL Data Warehouse que será a tabela de destino Olá para carga de saudação. colunas de saudação na tabela Olá devem corresponder dados toohello em cada linha do arquivo de dados.

toocreate uma tabela, abra um prompt de comando e use o sqlcmd.exe toorun Olá comando a seguir:

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


## <a name="2-create-a-source-data-file"></a>2. Criar um arquivo de dados de origem
Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo de texto e, em seguida, salvar esse arquivo tooyour local diretório temp, C:\Temp\DimDate2.txt. Esses dados estão no formato ASCII.

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

(Opcional) tooexport seus próprios dados de um banco de dados do SQL Server, abra um prompt de comando e execute Olá comando a seguir. Substitua TableName, ServerName, DatabaseName, Username e Password por suas próprias informações.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Carregar dados de saudação
dados de saudação tooload, abra um prompt de comando e execute Olá comando a seguir, substituindo valores de saudação para o nome do servidor, nome do banco de dados, nome de usuário e senha com suas próprias informações.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Use que estes comando tooverify Olá os dados foram carregados corretamente

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

resultados de saudação devem ter esta aparência:

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

## <a name="4-create-statistics"></a>4. Criar estatísticas
O SQL Data Warehouse ainda não dá suporte à criação automática ou atualização automática de estatísticas. tooget Olá melhor desempenho de consulta, é importante toocreate estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou após a ocorrem de alterações substanciais nos dados de saudação. Para obter uma explicação detalhada das estatísticas, confira [Estatísticas][Statistics]. 

Execute Olá estatísticas de toocreate de comando a seguir em sua tabela recentemente carregada.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Exportar dados do SQL Data Warehouse
Para diversão, você pode exportar dados de saudação que carregada fora do SQL Data Warehouse.  Olá comando tooexport é exatamente Olá mesmo que a exportação do SQL Server.

No entanto, há uma diferença nos resultados da saudação. Como dados de saudação são armazenados nos locais distribuídos no SQL Data Warehouse, quando você exportar dados a cada nó de computação grava-arquivo de saída de toohello de dados. ordem de saudação de dados Olá no arquivo de saída de saudação é provavelmente toobe diferente Olá ordem dos dados de saudação no arquivo de entrada hello.

### <a name="export-a-table-and-compare-exported-results"></a>Exportar uma tabela e comparar os resultados exportados
toosee Olá dados exportados, abra um prompt de comando e execute este comando usando seus próprios parâmetros. ServerName é o nome de saudação do servidor SQL lógico do Azure.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Você pode verificar Olá dados foram exportados corretamente abrindo novo arquivo de saudação. dados de saudação no arquivo hello devem coincidir com o texto de saudação abaixo, mas provavelmente serão classificados em uma ordem diferente:

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

### <a name="export-hello-results-of-a-query"></a>Saudação de exportar resultados de uma consulta
Você pode usar o hello **queryout** função dos resultados de saudação do bcp tooexport de uma consulta em vez de exportar a tabela inteira hello. 

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].
Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].
Consulte [Visão geral da tabela][Table Overview] ou [Sintaxe CREATE TABLE][CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse.

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
