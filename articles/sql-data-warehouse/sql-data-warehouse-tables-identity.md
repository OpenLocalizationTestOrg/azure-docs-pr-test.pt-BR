---
title: as chaves substitutas aaaCreate usando a identidade | Microsoft Docs
description: Saiba como substituto do toouse identidade toocreate chaves em suas tabelas.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Criar chaves substitutas usando IDENTITY
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Tipos de dados][Data Types]
> * [Distribuir][Distribute]
> * [Índice][Index]
> * [Partição][Partition]
> * [Estatísticas][Statistics]
> * [Temporário][Temporary]
> * [Identidade][Identity]
> 
> 

Muitos modeladores de dados, como chaves substitutas de toocreate em suas tabelas quando criam modelos de depósito de dados. Você pode usar tooachieve de propriedade de identidade Olá essa meta simples e eficiente sem afetar o desempenho de carga. 

## <a name="get-started-with-identity"></a>Introdução ao IDENTITY
Você pode definir uma tabela como tendo a propriedade IDENTITY hello quando você cria tabela hello usando sintaxe semelhante toohello instrução a seguir:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

Você pode usar `INSERT..SELECT` toopopulate tabela de saudação.

## <a name="behavior"></a>Comportamento
Olá propriedade IDENTITY é projetado tooscale out em todas as distribuições de saudação no data warehouse de saudação sem afetar o desempenho de carga. Portanto, a implementação de saudação da identidade é orientada para atingir esses objetivos. Esta seção destaca nuances de saudação do hello implementação toohelp é compreendê-los mais detalhadamente.  

### <a name="allocation-of-values"></a>Alocação de valores
Olá a propriedade IDENTITY não garante a ordem de saudação em qual Olá valores substitutos são alocados, que refletem o comportamento de saudação do SQL Server e banco de dados do SQL Azure. No entanto, no Azure SQL Data Warehouse, ausência de saudação de uma garantia é mais pronunciada. 

saudação de exemplo a seguir é uma ilustração:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

Em Olá anterior de exemplo, duas linhas descarregou na distribuição 1. Olá primeira linha tem o valor substituto Olá 1 na coluna `C1`, e Olá segunda linha tem o valor substituto Olá 61. Ambos os valores foram gerados por Olá propriedade de identidade. No entanto, a alocação de saudação de valores de saudação não é contígua. Este comportamento ocorre por design.

### <a name="skewed-data"></a>Dados distorcidos 
Olá intervalo de valores para o tipo de dados Olá estarão distribuídos igualmente por distribuições hello. Se uma tabela distribuída tiver dados distorcidos, Olá, em seguida, o intervalo de valores de tipo de dados toohello disponíveis pode ser esgotado prematuramente. Por exemplo, se todos os dados de saudação termina em um único de distribuição, em seguida, efetivamente Olá tabela tem acesso tooonly sixtieth um dos valores de Olá Olá do tipo de dados. Por esse motivo, Olá propriedade IDENTITY é limitado muito`INT` e `BIGINT` apenas tipos de dados.

### <a name="selectinto"></a>SELECT..INTO
Quando uma coluna de identidade existente é selecionada em uma nova tabela, o hello nova coluna herda a propriedade de identidade Olá, a menos que uma saudação seguintes condições for verdadeira:
- Olá a instrução SELECT contém uma junção.
- Várias instruções SELECT são unidas usando UNION.
- coluna de identidade Hello está listada mais de uma vez na lista de seleção de saudação.
- coluna de identidade Olá faz parte de uma expressão.
    
Se qualquer uma das seguintes condições for verdadeira, a coluna de saudação é criada NOT NULL em vez de herdar a propriedade IDENTITY hello.

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
Criar tabela como selecionar (CTAS) segue Olá mesmo comportamento do SQL Server que está documentado para SELECT... EM. No entanto, você não pode especificar uma propriedade de identidade na definição de coluna de saudação do hello `CREATE TABLE` parte da instrução de saudação. Você também não é possível usar função de identidade hello em Olá `SELECT` fazem parte do hello CTAS. toopopulate uma tabela, você precisa toouse `CREATE TABLE` seguido de tabela de saudação toodefine `INSERT..SELECT` toopopulate-lo.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Insera explicitamente os valores em uma coluna IDENTITY 
O SQL Data Warehouse oferece suporte à sintaxe `SET IDENTITY_INSERT <your table> ON|OFF`. Você pode usar essa sintaxe tooexplicitly inserir os valores na coluna de identidade de saudação.

Muitos modeladores de dados como negativo predefinidos toouse para determinados valores de linhas em suas dimensões. Um exemplo é Olá -1 ou linha "membro desconhecido". 

próximo de script Hello mostra como tooexplicitly adicionar essa linha usando SET IDENTITY_INSERT:

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>Carregar dados em uma tabela com IDENTITY

presença Olá Olá propriedade IDENTITY tem código de carregamento de dados de tooyour algumas implicações. Esta seção destaca alguns padrões básicos para carregar dados em tabelas usando IDENTITY. 

### <a name="load-data-with-polybase"></a>Carregar dados com o PolyBase
dados tooload em uma tabela e gerar uma chave substituta, usando a identidade, criar tabela hello e, em seguida, usar INSERT... SELECT ou INSERT... VALORES tooperform Olá carga.

Olá, exemplo a seguir destaca padrão básico hello:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> Não é possível toouse `CREATE TABLE AS SELECT` atualmente ao carregar dados em uma tabela com uma coluna de identidade.
> 

Para obter mais informações sobre carregar dados usando a ferramenta de BCP (programa) de cópia em massa hello, consulte Olá artigos a seguir:

- [Carregar com PolyBase][]
- [Práticas recomendadas do PolyBase][]

### <a name="load-data-with-bcp"></a>Carregar dados com o BCP
O BCP é uma ferramenta de linha de comando que você pode usar dados tooload no SQL Data Warehouse. Um de seus parâmetros (-E) controles Olá comportamento de BCP ao carregar dados em uma tabela com uma coluna de identidade. 

Quando -E também for especificado, os valores de saudação mantidos no arquivo de entrada hello para coluna Olá com identidade serão retidos. Se -E é *não* especificado, Olá valores nessa coluna são ignorados. Se a coluna de identidade de saudação não for incluída, dados de saudação são carregados como normal. valores Hello são gerados de acordo com a política de incremento e semente toohello da propriedade hello.

Para obter mais informações sobre carregar dados usando BCP, consulte Olá artigos a seguir:

- [Carregar com BCP][]
- [BCP no MSDN][]

## <a name="catalog-views"></a>Exibições do catálogo
SQL Data Warehouse dá suporte a saudação `sys.identity_columns` exibição do catálogo. Este modo de exibição pode ser usado tooidentify uma coluna que tem a propriedade de identidade hello.

toohelp você entender melhor o esquema de banco de dados hello, este exemplo mostra como toointegrate `sys.identity_columns` com outros modos de exibição de catálogo do sistema:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Limitações
Olá a propriedade IDENTITY não pode ser usado Olá os seguintes cenários:
- Qual tipo de dados de coluna Olá não é INT ou BIGINT
- Onde a coluna Olá também é chave de distribuição de saudação
- Onde a tabela de saudação é uma tabela externa 

Olá funções relacionadas a seguir não têm suporte no SQL Data Warehouse:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Tarefas

Esta seção fornece um exemplo de código você pode usar tarefas comuns de tooperform quando você trabalha com colunas de identidade.

> [!NOTE] 
> Coluna C1 é hello identidade no hello todas as tarefas a seguir.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Localize o valor de hello mais alta alocada para uma tabela
Saudação de uso `MAX()` função toodetermine Olá maior valor alocado para uma tabela distribuída:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Localizar Olá semente e incremento para Olá propriedade de identidade
Você pode usar o hello catálogo exibições toodiscover Olá identity incremento e semente valores de configuração para uma tabela usando Olá consulta a seguir: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre o desenvolvimento de tabelas, consulte [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de índice][Index], [particionar uma tabela][Partition], e [ Tabelas temporárias][Temporary]. 
* Para saber mais sobre as práticas recomendadas, consulte [Práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Carregar com BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Carregar com PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Práticas recomendadas do PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP no MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
