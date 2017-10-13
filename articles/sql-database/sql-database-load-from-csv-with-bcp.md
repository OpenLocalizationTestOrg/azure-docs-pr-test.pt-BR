---
title: Carregar dados do arquivo CSV para o Banco de Dados SQL do Azure (bcp) | Microsoft Docs
description: Para um tamanho de dados pequeno, use bcp para importar dados para o Banco de Dados SQL.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Carregar dados do CSV para o Banco de Dados SQL do Azure (arquivos simples)
Você pode usar o utilitário de linha de comando bcp para importar dados de um arquivo CSV para o Banco de Dados SQL.

## <a name="before-you-begin"></a>Antes de começar
### <a name="prerequisites"></a>Pré-requisitos
Para completar as etapas neste artigo, você precisa:

* Um servidor lógico e um banco de dados do Banco de Dados SQL do Azure
* O utilitário de linha de comando bcp instalado
* O utilitário de linha de comando sqlcmd instalado

Você pode baixar os utilitários bcp e sqlcmd do [Centro de Download da Microsoft][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dados em formato ASCII ou UTF-16
Se você estiver experimentando este tutorial com seus próprios dados, eles precisarão usar a codificação ASCII ou UTF-16, já que bcp não oferece suporte a UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Criar uma tabela de destino
Defina uma tabela no Banco de Dados SQL como a tabela de destino. As colunas na tabela devem corresponder aos dados em cada linha do arquivo de dados.

Para criar uma tabela, abra um prompt de comando e use sqlcmd.exe para executar o comando a seguir:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a>2. Criar um arquivo de dados de origem
Abra o Bloco de Notas e copie as seguintes linhas de dados em um novo arquivo de texto. Em seguida, salve esse arquivo em seu diretório temporário local, c:\Temp\DimDate2.txt. Esses dados estão no formato ASCII.

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

(Opcional) Para exportar seus próprios dados de um banco de dados do SQL Server, abra um prompt de comando e execute o comando a seguir. Substitua TableName, ServerName, DatabaseName, Username e Password por suas próprias informações.

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a>3. Carregar os dados
Para carregar os dados, abra um prompt de comando e execute o comando a seguir, substituindo os valores de Nome do Servidor, Nome do Banco de Dados, Nome de Usuário e Senha por suas próprias informações.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Use este comando para verificar se os dados foram carregados corretamente

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

O resultado deve parecer com o seguinte:

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

## <a name="next-steps"></a>Próximas etapas
Para migrar um banco de dados do SQL Server, confira [Migração de banco de dados do SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
