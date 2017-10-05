---
title: "Monitorar o armazenamento na memória XTP | Microsoft Docs"
description: "Estimar e monitorar o uso do armazenamento na memória XTP, capacidade; resolver o erro de capacidade 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="41752-103">Monitorar o armazenamento OLTP na memória</span><span class="sxs-lookup"><span data-stu-id="41752-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="41752-104">Ao usar o [In-Memory OLTP](sql-database-in-memory.md), os dados em tabelas com otimização de memória e as variáveis de tabela residem no armazenamento OLTP in-memory.</span><span class="sxs-lookup"><span data-stu-id="41752-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="41752-105">Cada camada de serviço Premium tem um tamanho máximo de armazenamento OLTP in-memory, que está documentado no [artigo Camadas de serviço do Banco de Dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="41752-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="41752-106">Quando esse limite for excedido, as operações insert e update poderão começar a falhar (com o erro 41823).</span><span class="sxs-lookup"><span data-stu-id="41752-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="41752-107">Nesse ponto, você precisará excluir dados para obter memória ou atualizar a camada de desempenho do seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="41752-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="41752-108">Determinar se os dados se ajustarão ao limite de armazenamento na memória</span><span class="sxs-lookup"><span data-stu-id="41752-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="41752-109">Determine o limite de armazenamento: consulte o [artigo Camadas de serviço do Banco de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para obter os limites de armazenamento das diferentes camadas do serviço Premium.</span><span class="sxs-lookup"><span data-stu-id="41752-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="41752-110">A estimativa dos requisitos de memória para uma tabela com otimização de memória funciona no SQL Server da mesma forma como no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="41752-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="41752-111">Reserve alguns minutos para examinar este tópico no [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="41752-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="41752-112">Observe que a tabela e as linhas de variável de tabela, bem como índices, contam para o tamanho máximo dos dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="41752-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="41752-113">Além disso, ALTER TABLE precisa de espaço suficiente para criar uma nova versão da tabela inteira e de seus índices.</span><span class="sxs-lookup"><span data-stu-id="41752-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="41752-114">Monitoramento e alertas</span><span class="sxs-lookup"><span data-stu-id="41752-114">Monitoring and alerting</span></span>
<span data-ttu-id="41752-115">Você pode monitorar o uso de armazenamento na memória como uma porcentagem do [limite de armazenamento para sua camada de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) no [portal](https://portal.azure.com/) do Azure:</span><span class="sxs-lookup"><span data-stu-id="41752-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="41752-116">Na folha Banco de Dados, localize a caixa de utilização Recurso e clique em Editar.</span><span class="sxs-lookup"><span data-stu-id="41752-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="41752-117">Em seguida, selecione a métrica `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="41752-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="41752-118">Para adicionar um alerta, clique na caixa Utilização de Recursos para abrir a folha Métrica e clique em Adicionar alerta.</span><span class="sxs-lookup"><span data-stu-id="41752-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="41752-119">Ou use a consulta a seguir para mostrar a utilização de armazenamento na memória:</span><span class="sxs-lookup"><span data-stu-id="41752-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="41752-120">Corrigir situações de memória insuficiente - Erro 41823</span><span class="sxs-lookup"><span data-stu-id="41752-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="41752-121">A insuficiência de memória resulta na falha das operações INSERT, UPDATE e CREATE com a mensagem de erro 41823.</span><span class="sxs-lookup"><span data-stu-id="41752-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="41752-122">A mensagem de erro 41823 indica que as variáveis de tabela e as tabelas com otimização de memória excederam o tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="41752-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="41752-123">Para resolver esse erro:</span><span class="sxs-lookup"><span data-stu-id="41752-123">To resolve this error, either:</span></span>

* <span data-ttu-id="41752-124">Exclua os dados das tabelas com otimização de memória, potencialmente descarregando os dados em tabelas baseadas em disco tradicionais ou</span><span class="sxs-lookup"><span data-stu-id="41752-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="41752-125">Atualize a camada de serviço para uma com armazenamento na memória suficiente para os dados que você precisa manter em tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="41752-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41752-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41752-126">Next steps</span></span>
<span data-ttu-id="41752-127">Para obter diretrizes sobre monitoramento, consulte [Monitoramento de Banco de Dados SQL do Azure usando exibições de gerenciamento dinâmico](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="41752-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
