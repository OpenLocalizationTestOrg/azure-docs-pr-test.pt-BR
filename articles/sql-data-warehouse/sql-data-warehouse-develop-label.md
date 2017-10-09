---
title: "aaaUse rótulos tooinstrument consultas no Data Warehouse SQL | Microsoft Docs"
description: "Dicas para usar rótulos tooinstrument consultas no Data Warehouse do Azure SQL para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a>Usar consultas de tooinstrument de rótulos no SQL Data Warehouse
O SQL Data Warehouse oferece suporte a um conceito chamado rótulos de consulta. Antes de entrar em qualquer profundidade, vamos examinar um exemplo:

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

Essa última linha marcas de consulta de toohello em 'Meu consulta rótulo' hello cadeia de caracteres. Isso é particularmente útil como rótulo de saudação é capaz de consulta por meio de saudação DMVs. Isso fornece um tootrack mecanismo consultas de problema e também toohelp identificar andamento por meio de uma execução ETL.

Uma boa convenção de nomenclatura ajuda muito aqui. Por exemplo, algo como ' projeto: procedimento: instrução: comentário ' Ajuda toouniquely identificar consulta Olá entre todos os códigos de saudação no controle de origem.

exibições de gerenciamento dinâmico de Olá toosearch por rótulo, você pode usar o hello consulta que usa a seguir:

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> É essencial encapsule colchetes ou aspas duplas em torno do rótulo de palavra hello ao consultar. Rótulo é uma palavra reservada e causará um erro se não for delimitada.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
