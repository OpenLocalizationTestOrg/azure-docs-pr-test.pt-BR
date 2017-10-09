---
title: "variáveis de aaaAssign no SQL Data Warehouse | Microsoft Docs"
description: "Dicas para atribuir variáveis de Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a>Atribuir variáveis no SQL Data Warehouse
Variáveis no SQL Data Warehouse são definidas usando Olá `DECLARE` instrução ou hello `SET` instrução.

Olá seguinte são maneiras válidas perfeitamente tooset um valor de variável:

## <a name="setting-variables-with-declare"></a>Definição de variáveis com DECLARE
Inicializando variáveis com DECLARE é um dos tooset de maneiras mais flexível Olá um valor da variável no SQL Data Warehouse.

```sql
DECLARE @v  int = 0
;
```

Você também pode usar DECLARE tooset mais de uma variável de cada vez. Não é possível usar `SELECT` ou `UPDATE` toodo isso:

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

Você não pode inicializar e usar uma variável em Olá mesma instrução DECLARE. tooillustrate Olá ponto Olá exemplo a seguir é **não** permitido como @p1 é inicializado e usado em Olá mesma instrução DECLARE. Isso resultará em um erro.

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a>Definição de valores com SET
O SET é um método muito comum para definir uma variável.

Todos os exemplos de saudação abaixo são maneiras válidas de configuração de uma variável com o conjunto:

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

Você só pode definir uma variável por vez com SET. No entanto, como pode ser visto acima, são permitidos operadores compostos.

## <a name="limitations"></a>Limitações
Você não pode usar SELECT ou UPDATE para atribuição de variáveis.

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
