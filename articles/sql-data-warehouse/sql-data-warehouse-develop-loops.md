---
title: aaaLeverage loops de T-SQL no SQL Data Warehouse do Azure | Microsoft Docs
description: "Dicas para execução de loops do Transact_SQL e substituição de cursores no SQL Data Warehouse Azure para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>Executar loops no SQL Data Warehouse
SQL Data Warehouse dá suporte a saudação [ENQUANTO][ENQUANTO] loop para repetidamente executar blocos de instrução. Isso continuará para como Olá especificado condições forem verdadeiras, ou até que o código Olá finaliza especificamente loop de hello usando Olá `BREAK` palavra-chave. A execução de loops é particularmente útil para a substituição de cursores definidos no código SQL. Felizmente, quase todos os cursores que são escritos em código SQL são de saudação rápida, leitura apenas variedade. Portanto, [ENQUANTO] loops são uma excelente alternativa, se você estiver tendo tooreplace um.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Aproveitando a execução de loops e substituindo cursores no SQL Data Warehouse
No entanto, antes de se aprofundar no cabeçalho primeiro você deve estar se perguntando Olá seguinte pergunta: "foi gravado nesse cursor toouse operações baseadas em conjunto?". Em muitos casos resposta Olá será Sim e é geralmente a melhor abordagem de saudação. Uma operação baseada em conjunto geralmente terá um desempenho consideravelmente mais rápido do que uma abordagem iterativa de linha por linha.

Os cursores somente leitura de avanço rápido podem ser facilmente substituídos por um constructo de looping. Veja abaixo um exemplo simples. Este exemplo de código atualiza estatísticas de saudação para cada tabela no banco de dados de saudação. Pela iteração em tabelas de saudação em loop Olá nós é tooexecute capaz de cada comando em sequência.

Primeiro, crie uma tabela temporária que contém uma linha exclusiva usada tooidentify Olá individuais instruções de número:

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

Em segundo lugar, inicialize o loop de Olá Olá variáveis tooperform necessária:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Agora, execute um loop sobre as instruções para executar uma por vez:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Por fim Descartar tabela temporária de saudação criada na primeira etapa de saudação

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[ENQUANTO]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
