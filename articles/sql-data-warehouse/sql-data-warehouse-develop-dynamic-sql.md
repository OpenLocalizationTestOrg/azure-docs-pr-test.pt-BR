---
title: "SQL dinâmico no SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 29228676373aee8dbc7b1b2a7d92ffc978333804
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-sql-in-sql-data-warehouse"></a><span data-ttu-id="4acd5-103">SQL dinâmico no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4acd5-103">Dynamic SQL in SQL Data Warehouse</span></span>
<span data-ttu-id="4acd5-104">Ao desenvolver o código do aplicativo para o SQL Data Warehouse, talvez seja preciso usar um sql dinâmico para ajudar a fornecer soluções flexíveis, genéricas e modulares.</span><span class="sxs-lookup"><span data-stu-id="4acd5-104">When developing application code for SQL Data Warehouse you may need to use dynamic sql to help deliver flexible, generic and modular solutions.</span></span> <span data-ttu-id="4acd5-105">No momento, o SQL Data Warehouse não dá suporte a tipos de dados de blob.</span><span class="sxs-lookup"><span data-stu-id="4acd5-105">SQL Data Warehouse does not support blob data types at this time.</span></span> <span data-ttu-id="4acd5-106">Isso pode limitar o tamanho de suas sequências de caracteres como tipos de blob que incluem tipos varchar(max) e nvarchar(max).</span><span class="sxs-lookup"><span data-stu-id="4acd5-106">This may limit the size of your strings as blob types include both varchar(max) and nvarchar(max) types.</span></span> <span data-ttu-id="4acd5-107">Se você usou estes tipos no código do seu aplicativo ao compilar cadeias de caracteres muito grandes, você precisará dividir o código em partes e usar a instrução EXEC em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="4acd5-107">If you have used these types in your application code when building very large strings, you will need to break the code into chunks and use the EXEC statement instead.</span></span>

<span data-ttu-id="4acd5-108">Um exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="4acd5-108">A simple example:</span></span>

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

<span data-ttu-id="4acd5-109">Se a cadeia de caracteres for curta, você poderá usar [sp_executesql][sp_executesql] normalmente.</span><span class="sxs-lookup"><span data-stu-id="4acd5-109">If the string is short you can use [sp_executesql][sp_executesql] as normal.</span></span>

> [!NOTE]
> <span data-ttu-id="4acd5-110">Instruções executadas como SQL dinâmico ainda estarão sujeitas a todas as regras de validação de TSQL.</span><span class="sxs-lookup"><span data-stu-id="4acd5-110">Statements executed as dynamic SQL will still be subject to all TSQL validation rules.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4acd5-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4acd5-111">Next steps</span></span>
<span data-ttu-id="4acd5-112">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="4acd5-112">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[sp_executesql]: https://msdn.microsoft.com/library/ms188001.aspx

<!--Other Web references-->
