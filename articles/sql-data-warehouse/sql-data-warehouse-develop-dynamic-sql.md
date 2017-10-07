---
title: aaaDynamic SQL no SQL Data Warehouse | Microsoft Docs
description: "Dicas para usar SQL dinâmico no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: a948c2c3-3cd1-4373-90a9-79e59414b778
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 4d66eecb37621510f657d1ec9a2a935daaa16052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a>SQL dinâmico no SQL Data Warehouse
Ao desenvolver o código do aplicativo para o SQL Data Warehouse, você pode a toouse sql dinâmico toohelp precisa fornecer soluções modulares e flexíveis genéricas. No momento, o SQL Data Warehouse não dá suporte a tipos de dados de blob. Isso pode limitar o tamanho de saudação cadeias de caracteres como tipos blob incluem tipos varchar (max) e nvarchar (max). Se você tiver usado a esses tipos em seu código de aplicativo durante a criação de cadeias de caracteres muito grandes, será necessário código de saudação toobreak em partes e use Olá EXEC instrução em vez disso.

Um exemplo simples:

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Se a cadeia de caracteres de saudação é curta que você pode usar [sp_executesql] [ sp_executesql] como normal.

> [!NOTE]
> Instruções executadas como SQL dinâmico ainda serão as regras de validação do assunto tooall TSQL.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
