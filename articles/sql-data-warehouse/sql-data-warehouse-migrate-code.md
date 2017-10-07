---
title: "aaaMigrate tooSQL de código seu SQL Data Warehouse | Microsoft Docs"
description: "Dicas para migrar seu código SQL tooAzure SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>Migrar seu tooSQL de código do SQL Data Warehouse
Este artigo explica as alterações de código que você provavelmente precisará toomake ao migrar seu código de outro tooSQL de banco de dados do Data Warehouse. Alguns recursos do SQL Data Warehouse podem melhorar significativamente o desempenho conforme forem toowork projetado de modo distribuído. No entanto, toomaintain desempenho e escala, alguns recursos também não estão disponíveis.

## <a name="common-t-sql-limitations"></a>Limitações comuns do T-SQL
Olá lista a seguir resume os recursos de mais comuns de Olá que não oferece suporte a SQL Data Warehouse. Olá links levam tooworkarounds para recursos de saudação sem suporte:

* [Junções ANSI em atualizações][ANSI joins on updates]
* [Junções ANSI em exclusões][ANSI joins on deletes]
* [instrução merge][merge statement]
* junções entre bancos de dados
* [cursores][cursors]
* <seg>
  [INSERT..EXEC][INSERT..EXEC]</seg>
* cláusula output
* funções definidas pelo usuário embutidas
* funções com várias instruções
* [expressões de tabela comuns](#Common-table-expressions)
* [CTE (expressão de tabela comum) recursiva] (#Recursive-common-table-expressions-(CTE)
* procedimentos e funções CLR
* função $partition
* variáveis de tabela
* parâmetros de valor de tabela
* transações distribuídas
* confirmar/reverter trabalho
* salvar transação
* contextos de execução (EXECUTE AS)
* [cláusula group by com as opções rollup/cube/grouping sets][group by clause with rollup / cube / grouping sets options]
* [níveis de aninhamento superiores a 8][nesting levels beyond 8]
* [atualizando por meio de exibições][updating through views]
* [uso de select para atribuição de variável][use of select for variable assignment]
* [nenhum tipo de dados MAX para cadeias de caracteres SQL dinâmicas][no MAX data type for dynamic SQL strings]

Felizmente, a maioria dessas limitações pode ser solucionada. Explicações são fornecidas nos artigos de desenvolvimento relevantes Olá mencionados acima.

## <a name="supported-cte-features"></a>Recursos do CTE com suporte
Tabela CTEs (expressões comuns) têm suporte parcial no SQL Data Warehouse.  Olá recursos CTE a seguir é atualmente suportado:

* Uma CTE pode ser especificada em uma instrução SELECT.
* Uma CTE pode ser especificada em uma instrução CREATE VIEW.
* Uma CTE pode ser especificada em uma instrução CTAS (CREATE TABLE AS SELECT).
* Uma CTE pode ser especificada em uma instrução CRTAS (CREATE REMOTE TABLE AS SELECT).
* Uma CTE pode ser especificada em uma instrução CETAS (CREATE EXTERNAL TABLE AS SELECT).
* Uma tabela remota pode ser referenciada de uma CTE.
* Uma tabela externa pode ser referenciada de uma CTE.
* Várias definições de consulta CTE podem ser definidas em uma CTE.

## <a name="cte-limitations"></a>Limitações da CTE
As expressões de tabela comum têm algumas limitações no SQL Data Warehouse, incluindo:

* Uma CTE deve ser seguida por uma única instrução SELECT. As instruções INSERT, UPDATE, DELETE e MERGE não têm suporte.
* Não há suporte para a expressão de tabela comum que inclua referências tooitself (recursivo expressão de tabela comum) (consulte a seção abaixo).
* Não é permitido especificar mais de uma cláusula WITH em uma CTE. Por exemplo, se CTE_query_definition contiver uma subconsulta, essa subconsulta não poderá conter uma cláusula WITH aninhada que defina outra CTE.
* Uma cláusula ORDER BY não pode ser usada em Olá definições de consulta CTE, exceto quando uma cláusula TOP é especificada.
* Quando uma CTE é usada em uma instrução que faz parte de um lote, a instrução de saudação antes que ele deve ser seguida por um ponto e vírgula.
* Quando usado em instruções preparadas por sp_prepare, CTEs irão se comportar Olá mesma maneira que outras instruções SELECT do PDW. No entanto, se CTEs são usadas como parte do CETAS preparada por sp_prepare, pode adiar o comportamento de saudação do SQL Server e outras instruções do PDW devido à forma como o hello associação é implementada por sp_prepare. Se a opção selecionar que referências a que CTE é usar uma coluna incorreta que não existe na CTE, Olá sp_prepare passará sem detecção de erro hello, mas Olá um erro será gerado durante a sp_execute em vez disso.

## <a name="recursive-ctes"></a>CTEs recursivas
As CTEs recursivas não têm suporte no SQL Data Warehouse.  migração de saudação da CTE recursiva pode ser um pouco complexa e processo melhor Olá é toobreak em várias etapas. Normalmente, você pode usar um loop e popular uma tabela temporária como iterar em consultas provisória do hello recursivas. Depois de tabela temporária Olá é preenchida, em seguida, retorne dados saudação como um único conjunto de resultados. Uma abordagem semelhante foi usado toosolve `GROUP BY WITH CUBE` em Olá [Agrupar por cláusula com pacote cumulativo de atualizações / cubo / define as opções de agrupamento] [ group by clause with rollup / cube / grouping sets options] artigo.

## <a name="unsupported-system-functions"></a>Funções do sistema sem suporte
Também há algumas funções do sistema que não têm suporte. Alguns dos Olá principal que normalmente podem ser usada no data warehouse são:

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

Alguns desses problemas podem ser solucionados.

## <a name="rowcount-workaround"></a>Solução alternativa @@ROWCOUNT
toowork em torno de falta de suporte para @@ROWCOUNT, criar um procedimento armazenado que irá recuperar Olá última contagem de linhas de sys.dm_pdw_request_steps e, em seguida, execute `EXEC LastRowCount` após uma instrução DML.

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a>Próximas etapas
Para obter uma lista completa de todas as instruções T-SQL com suporte, confira [Tópicos do Transact-SQL][Transact-SQL topics].

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
