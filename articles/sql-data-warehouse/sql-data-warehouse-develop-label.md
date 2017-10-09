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
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="fa05d-103">Usar consultas de tooinstrument de rótulos no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="fa05d-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="fa05d-104">O SQL Data Warehouse oferece suporte a um conceito chamado rótulos de consulta.</span><span class="sxs-lookup"><span data-stu-id="fa05d-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="fa05d-105">Antes de entrar em qualquer profundidade, vamos examinar um exemplo:</span><span class="sxs-lookup"><span data-stu-id="fa05d-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="fa05d-106">Essa última linha marcas de consulta de toohello em 'Meu consulta rótulo' hello cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="fa05d-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="fa05d-107">Isso é particularmente útil como rótulo de saudação é capaz de consulta por meio de saudação DMVs.</span><span class="sxs-lookup"><span data-stu-id="fa05d-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="fa05d-108">Isso fornece um tootrack mecanismo consultas de problema e também toohelp identificar andamento por meio de uma execução ETL.</span><span class="sxs-lookup"><span data-stu-id="fa05d-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="fa05d-109">Uma boa convenção de nomenclatura ajuda muito aqui.</span><span class="sxs-lookup"><span data-stu-id="fa05d-109">A good naming convention really helps here.</span></span> <span data-ttu-id="fa05d-110">Por exemplo, algo como ' projeto: procedimento: instrução: comentário ' Ajuda toouniquely identificar consulta Olá entre todos os códigos de saudação no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="fa05d-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="fa05d-111">exibições de gerenciamento dinâmico de Olá toosearch por rótulo, você pode usar o hello consulta que usa a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa05d-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="fa05d-112">É essencial encapsule colchetes ou aspas duplas em torno do rótulo de palavra hello ao consultar.</span><span class="sxs-lookup"><span data-stu-id="fa05d-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="fa05d-113">Rótulo é uma palavra reservada e causará um erro se não for delimitada.</span><span class="sxs-lookup"><span data-stu-id="fa05d-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fa05d-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa05d-114">Next steps</span></span>
<span data-ttu-id="fa05d-115">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="fa05d-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
