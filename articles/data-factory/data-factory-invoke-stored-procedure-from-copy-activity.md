---
title: "aaaInvoke procedimento armazenado de atividade de cópia de fábrica de dados do Azure | Microsoft Docs"
description: "Saiba como atividade de cópia tooinvoke um procedimento armazenado no banco de dados SQL ou SQL Server a partir de uma fábrica de dados do Azure."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Invocar procedimento armazenado de atividade de cópia no Azure Data Factory
Ao copiar dados no [do SQL Server](data-factory-sqlserver-connector.md) ou [banco de dados do SQL Azure](data-factory-azure-sql-connector.md), você pode configurar Olá **SqlSink** na atividade de cópia tooinvoke um procedimento armazenado. Talvez você queira toouse Olá armazenado procedimento tooperform qualquer processamento adicional (mesclagem de colunas, pesquisar valores de inserção em várias tabelas, etc.) é necessária antes de inserir dados na tabela de destino toohello. Esse recurso se beneficia de [parâmetros com valores de tabela](https://msdn.microsoft.com/library/bb675163.aspx). 

saudação de exemplo a seguir mostra como tooinvoke um procedimento armazenado em um SQL Server do banco de dados de um pipeline da fábrica de dados (Copiar atividade):  

## <a name="output-dataset-json"></a>JSON do conjunto de dados de saída
Olá saída conjunto de dados JSON, defina Olá **tipo** para: **SqlServerTable**. Defina-o muito**AzureSqlTable** toouse com um banco de dados do SQL Azure. Olá valor **tableName** propriedade deve corresponder saudação do primeiro parâmetro do procedimento armazenado de saudação.  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a>Seção SqlSink na atividade de cópia JSON
Definir Olá **SqlSink** seção na atividade de cópia Olá JSON da seguinte maneira. tooinvoke um procedimento armazenado ao inserir dados no banco de dados de destino/coletor hello, especifique valores para os dois **SqlWriterStoredProcedureName** e **SqlWriterTableType** propriedades. Para obter descrições dessas propriedades, consulte [do SqlSink seção no artigo de conector do SQL Server Olá](data-factory-sqlserver-connector.md#sqlsink).

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a>Definição do procedimento armazenado 
No banco de dados, definir o procedimento de saudação armazenado com hello mesmo nome como **SqlWriterStoredProcedureName**. procedimento armazenado de saudação lida com dados de entrada de repositório de dados de origem hello e insere dados em uma tabela no banco de dados de destino de saudação. nome de saudação do primeiro parâmetro hello de procedimento armazenado deve corresponder tableName Olá definido no conjunto de dados Olá JSON (Marketing).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Definição de tipo de tabela
No banco de dados, definir o tipo de tabela de saudação com hello mesmo nome como **SqlWriterTableType**. esquema Olá Olá do tipo de tabela deve corresponder o esquema de saudação do conjunto de dados de entrada hello.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Próximas etapas
Examine Olá conector artigos para concluir os exemplos JSON a seguir: 

- [Banco de Dados SQL do Azure](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
