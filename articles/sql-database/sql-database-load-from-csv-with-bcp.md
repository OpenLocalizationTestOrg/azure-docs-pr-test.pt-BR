---
title: o arquivo de dados aaaLoad de CSV em banco de dados do SQL do Azure (bcp) | Microsoft Docs
description: Para um tamanho de dados pequeno, usa bcp tooimport dados no banco de dados do SQL Azure.
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Carregar dados do CSV para o Banco de Dados SQL do Azure (arquivos simples)
Você pode usar dados de tooimport saudação bcp utilitário de linha de comando de um arquivo CSV para o banco de dados do SQL Azure.

## <a name="before-you-begin"></a>Antes de começar
### <a name="prerequisites"></a>Pré-requisitos
Olá toocomplete as etapas neste artigo, você precisa:

* Um servidor lógico e um banco de dados do Banco de Dados SQL do Azure
* Utilitário de linha de comando do bcp Olá instalado
* Utilitário de linha de comando do sqlcmd Olá instalado

Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dados em formato ASCII ou UTF-16
Se você estiver tentando neste tutorial com seus próprios dados, os dados precisarem toouse Olá ASCII ou codificação UTF-16 como bcp não oferece suporte a UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Criar uma tabela de destino
Defina uma tabela no banco de dados SQL como tabela de destino de saudação. colunas de saudação na tabela Olá devem corresponder dados toohello em cada linha do arquivo de dados.

toocreate uma tabela, abra um prompt de comando e use o sqlcmd.exe toorun Olá comando a seguir:

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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Carregar dados de saudação
dados de saudação tooload, abra um prompt de comando e execute Olá comando a seguir, substituindo valores de saudação para o nome do servidor, nome do banco de dados, nome de usuário e senha com suas próprias informações.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Use que estes comando tooverify Olá os dados foram carregados corretamente

```bcp
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

## <a name="next-steps"></a>Próximas etapas
toomigrate um banco de dados do SQL Server, consulte [migração de banco de dados do SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
