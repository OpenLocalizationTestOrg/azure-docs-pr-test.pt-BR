---
title: "Monitorar consultas de usuário no SQL Data Warehouse do Azure| Microsoft Docs"
description: "Visão geral sobre considerações, melhores práticas e tarefas para monitoramento de consultas de usuário no SQL Data Warehouse do Azure"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 65509a65c2b34553822cc02d7a7fa5a614adc57f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="12f22-103">Monitorar consultas de usuário no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="12f22-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="12f22-104">Visão geral sobre considerações, melhores práticas e tarefas para monitoramento de consultas de usuário no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12f22-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="12f22-105">Categoria</span><span class="sxs-lookup"><span data-stu-id="12f22-105">Category</span></span> | <span data-ttu-id="12f22-106">Tarefa ou consideração</span><span class="sxs-lookup"><span data-stu-id="12f22-106">Task or consideration</span></span> | <span data-ttu-id="12f22-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="12f22-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="12f22-108">Desempenho lento</span><span class="sxs-lookup"><span data-stu-id="12f22-108">Slow performance</span></span> |<span data-ttu-id="12f22-109">Localizar uma consulta de usuário com execução longa</span><span class="sxs-lookup"><span data-stu-id="12f22-109">Find a long-running user query</span></span> |<span data-ttu-id="12f22-110">[Localizar consultas com execução longa][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="12f22-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="12f22-111">Simultaneidade</span><span class="sxs-lookup"><span data-stu-id="12f22-111">Concurrency</span></span> |<span data-ttu-id="12f22-112">Atribuir recursos simultâneos para consultas de usuário</span><span class="sxs-lookup"><span data-stu-id="12f22-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="12f22-113">[Gerenciamento de simultaneidade e carga de trabalho][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="12f22-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12f22-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12f22-114">Next steps</span></span>
<span data-ttu-id="12f22-115">Para obter mais dicas de gerenciamento, acesse a [Visão geral de gerenciamento][Management overview].</span><span class="sxs-lookup"><span data-stu-id="12f22-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
