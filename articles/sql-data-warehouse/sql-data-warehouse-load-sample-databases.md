---
title: dados de exemplo aaaLoad no SQL Data Warehouse | Microsoft Docs
description: Carregar dados de amostra no SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>Carregar dados de amostra no SQL Data Warehouse
Siga essas tooload etapas simples e consultar banco de dados de exemplo do Adventure Works de saudação. Esses scripts primeiro usam sqlcmd toorun SQL que criará tabelas e exibições. Depois que as tabelas foram criadas, scripts Olá usará dados de tooload de bcp.  Se você ainda não tiver sqlcmd e bcp instalado, siga estes links muito[instalar bcp] [ install bcp] e muito[instalar sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Carregar dados de exemplo
1. Baixar Olá [Scripts de exemplo Adventure Works para SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] arquivo zip.
2. Extraia os arquivos de saudação do diretório de tooa zip baixado em seu computador local.
3. Edite aw_create.bat do arquivo hello extraído e defina Olá encontradas na parte superior de saudação do arquivo hello variáveis a seguir.  Não ser tooleave-se de que nenhum espaço em branco entre hello "=" e o parâmetro hello.  A seguir estão exemplos de como poderão ficar suas edições.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. Em um prompt de comando do Windows, execute aw_create.bat Olá editado.  Certifique-se de que você está no diretório Olá onde você salvou sua versão editada do aw_create.bat.
   Este script...
   
   * Descartará todas as tabelas da Adventure Works ou exibições que já existem no banco de dados
   * Criar exibições e tabelas do Adventure Works Olá
   * Carregará cada tabela da Adventure Works usando o bcp
   * Validar Olá contagens de linha para cada tabela do Adventure Works
   * Coletará estatísticas sobre cada coluna para cada tabela da Adventure Works

## <a name="query-sample-data"></a>Consultar dados de exemplo
Agora que você carregou alguns dados de exemplo no SQL Data Warehouse, poderá executar rapidamente algumas consultas.  toorun uma consulta, conecte-se tooyour recém-criado banco de dados Adventure Works no Azure SQL DW usando Visual Studio e SSDT, conforme descrito em Olá [consulta com o Visual Studio] [ query with Visual Studio] documento.

Exemplo de simples select instrução tooget todas as informações de saudação de funcionários hello:

```sql
SELECT * FROM DimEmployee;
```

Exemplo de uma consulta mais complexa usando construções, como GROUP BY toolook quantidade total de saudação para todas as vendas em cada dia:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Exemplo de uma seleção com um toofilter de cláusula WHERE ordens de antes de uma determinada data:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

O SQL Data Warehouse oferece suporte a quase todas as construções T-SQL para as quais o SQL Server oferece suporte.  Todas as diferenças estão documentadas em nossa documentação sobre como [migrar o código][migrate code].

## <a name="next-steps"></a>Próximas etapas
Agora que você teve uma chance tootry algumas consultas com dados de exemplo, check-out como muito[desenvolver][develop], [carregar][load], ou [ migrar] [ migrate] tooSQL Data Warehouse.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
