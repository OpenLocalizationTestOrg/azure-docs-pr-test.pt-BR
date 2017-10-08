---
title: "cópia de aaaRepeatable na fábrica de dados do Azure | Microsoft Docs"
description: "Saiba como tooavoid duplicatas, embora uma fatia que copia dados é executada mais de uma vez."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Cópia repetida no Azure Data Factory

## <a name="repeatable-read-from-relational-sources"></a>Leitura repetida de fontes relacionais
Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.  
 
> [!NOTE]
> Hello exemplos a seguir são para o SQL Azure, mas são aplicáveis tooany repositório de dados que oferece suporte a conjuntos de dados retangulares. Talvez você tenha tooadjust Olá **tipo** de origem e hello **consulta** propriedade (por exemplo: consulta em vez de sqlReaderQuery) para dados Olá armazenar.   

Normalmente, ao ler de armazenamentos relacionais, você deseja tooread somente dados de saudação correspondente toothat fatia. Uma maneira toodo assim seria usando Olá WindowStart e WindowEnd variáveis de sistema disponíveis no Azure Data Factory. Leia sobre as variáveis de saudação e funções do Azure Data Factory aqui em Olá [do Azure Data Factory - funções e variáveis de sistema](data-factory-functions-variables.md) artigo. Exemplo: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Essa consulta lê os dados que se encaixa no intervalo de duração de fatias de saudação (WindowStart -> WindowEnd) da tabela Olá MyTable. Execute novamente dessa fatia sempre garantiria que Olá tais dados são lidos. 

Em outros casos, você poderá tooread Olá toda a tabela e pode definir Olá sqlReaderQuery da seguinte maneira:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Gravação REPEATABLE tooSqlSink
Ao copiar dados muito**Azure SQL do SQL Server** outros armazenamentos de dados, você precisa tookeep repetição em mente tooavoid resultados não intencionais. 

Ao copiar dados tooAzure banco de dados SQL do SQL Server, atividade de cópia Olá acrescenta a tabela de dados do coletor toohello por padrão. Significa que você está copiando dados de um CSV (valores separados por vírgula) arquivos contendo dois registros toohello em um banco de dados do Azure SQL do SQL Server a tabela a seguir. Quando uma fatia é executado, Olá dois registros são copiados toohello tabela do SQL. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Suponha que você encontrou erros no arquivo de origem e quantidade de saudação do tubo de busca de 2 too4 atualizada. Se você executar novamente a fatia de dados Olá para aquele período manualmente, você encontrará dois novos registros acrescentado tooAzure banco de dados SQL do SQL Server. Este exemplo presume que nenhuma Olá colunas na tabela de saudação tem restrição de chave primária hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid esse comportamento, você precisa semântica UPSERT toospecify usando uma saudação dois mecanismos a seguir:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Mecanismo 1: usando o sqlWriterCleanupScript
Você pode usar o hello **sqlWriterCleanupScript** tooclean propriedade backup de dados de tabela de coletor de saudação antes de inserir dados hello quando uma fatia é executada. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Quando uma fatia é executado, script de limpeza de saudação é executado primeiro dados toodelete que corresponde a fatia toohello da tabela de saudação do SQL. atividade de cópia Hello, em seguida, insere dados em Olá tabela SQL. Se a fatia de saudação for executado novamente, a quantidade de saudação é atualizada conforme desejado.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Suponha que Olá registro Arruela simples é removido do csv original hello. Em seguida, executar novamente a fatia de saudação produziria Olá resultados a seguir: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

atividade de cópia Olá ficou Olá limpeza script toodelete Olá dados correspondentes para essa fatia. Em seguida, ele lê a entrada de saudação do csv hello (que, em seguida, continha apenas um registro) e inseri-lo no hello tabela. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Mecanismo 2: usando o sliceIdentifierColumnName
> [!IMPORTANT]
> No momento, não há suporte para sliceIdentifierColumnName no SQL Data Warehouse do Azure. 

repetição do Hello segundo mecanismo tooachieve é ter uma coluna dedicada (sliceIdentifierColumnName) na tabela de destino de saudação. Essa coluna seria usada pelo Azure Data Factory tooensure Olá origem e destino fique sincronizado. Essa abordagem funciona quando há flexibilidade ao alterar ou definir o esquema de tabela SQL de destino de saudação. 

Esta coluna é usada pela fábrica de dados do Azure para fins de repetição e no processo de saudação do Azure Data Factory não faz qualquer esquema toohello tabela é alterado. Modo toouse essa abordagem:

1. Definir uma coluna do tipo **binary (32)** no destino Olá tabela SQL. Não deve haver nenhuma restrição nessa coluna. Vamos nomear esta coluna como AdfSliceIdentifier para este exemplo.


    Tabela de origem:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Tabela de destino: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Usá-lo na atividade de cópia de saudação da seguinte maneira:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

A fábrica de dados do Azure preenche essa coluna de acordo com sua necessidade tooensure Olá origem e destino permanecem sincronizados. os valores dessa coluna Olá não devem ser usados fora neste contexto. 

Semelhante toomechanism 1, atividade de cópia limpa automaticamente os dados de saudação para Olá fornecida fatia do destino Olá tabela SQL. Em seguida, insere dados de origem na tabela de destino toohello. 

## <a name="next-steps"></a>Próximas etapas
Examine Olá conector artigos para concluir os exemplos JSON a seguir: 

- [Banco de Dados SQL do Azure](data-factory-azure-sql-connector.md)
- [SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)