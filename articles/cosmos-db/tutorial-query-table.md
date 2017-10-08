---
title: aaaHow tooquery dados da tabela no banco de dados do Azure Cosmos? | Microsoft Docs
description: Saiba tooquery dados da tabela no banco de dados do Azure Cosmos
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Cosmos do Azure DB: Como dados de tabela tooquery usando Olá API de tabela (visualização)?

Olá banco de dados do Azure Cosmos [API tabela](table-introduction.md) (visualização) oferece suporte a OData e [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) consultas em dados de chave/valor (tabela).  

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Consultando dados com hello API de tabela

as consultas neste artigo Hello usam Olá exemplo a seguir `People` tabela:

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Porque o banco de dados do Azure Cosmos é compatível com hello APIs de armazenamento de tabela do Azure, consulte [consultando tabelas e entidades] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) para obter detalhes sobre como tooquery usando Olá Tabela de API. 

Para obter mais informações sobre recursos premium Olá que o banco de dados do Azure Cosmos oferece, consulte [o banco de dados do Azure Cosmos: API de tabela](table-introduction.md) e [desenvolver com hello API de tabela no .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Pré-requisitos

Para toowork essas consultas, você deve ter uma conta de banco de dados do Azure Cosmos e ter dados de entidade no contêiner de saudação. Não tenho nenhum deles? Olá completa [início rápido de cinco minutos](https://aka.ms/acdbtnetqs) ou hello [tutorial de desenvolvedor](https://aka.ms/acdbtabletut) toocreate uma conta e preencher o banco de dados.

## <a name="query-on-partitionkey-and-rowkey"></a>Consultar em PartitionKey e RowKey
Como as propriedades PartitionKey e RowKey Olá constituem a chave primária da entidade, você pode usar Olá entidade de saudação tooidentify sintaxe especial a seguir: 

**Consulta**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Resultados**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Como alternativa, você pode especificar essas propriedades como parte da saudação `$filter` opção, conforme mostrado no hello seção a seguir. Observe que os nomes de propriedade de chave hello e valores constantes diferenciam maiusculas de minúsculas. Olá PartitionKey e RowKey propriedades são do tipo cadeia de caracteres. 

## <a name="query-by-using-an-odata-filter"></a>Consultar utilizando um filtro OData
Ao construir uma cadeia de caracteres de filtro, lembre-se destas regras: 

* Use operadores lógicos de saudação definidos pela Olá especificação do protocolo OData toocompare um valor da propriedade tooa. Observe que você não pode comparar um valor da propriedade tooa dinâmico. Um lado da expressão Olá deve ser uma constante. 
* nome da propriedade Hello, o operador e o valor constante devem ser separados por espaços codificados de URL. Um espaço é codificado por URL como `%20`. 
* Todas as partes da cadeia de caracteres de filtro Olá diferenciam maiusculas de minúsculas. 
* valor constante Olá deve ser de saudação mesmo tipo que propriedade Olá para que os resultados Olá filtro tooreturn válidos. Para obter mais informações sobre os tipos de propriedade com suporte, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Aqui está uma consulta de exemplo que mostra como toofilter por Olá PartitionKey e propriedades de Email usando um OData `$filter`.

**Consulta**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Para obter mais informações sobre como tooconstruct filtrar expressões para vários tipos de dados, consulte [consultar tabelas e entidades](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Resultados**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Consultar utilizando LINQ 
Você também pode consultar usando LINQ, que converte as expressões de consulta OData de toohello correspondentes. Aqui está um exemplo de como toobuild consultas usando Olá .NET SDK:

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Aprendeu como tooquery usando Olá API de tabela (visualização) 

Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.

> [!div class="nextstepaction"]
> [Distribuir os dados globalmente](tutorial-global-distribution-documentdb.md)
