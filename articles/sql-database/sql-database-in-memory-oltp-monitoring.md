---
title: "armazenamento de na memória XTP aaaMonitor | Microsoft Docs"
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
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="04188-103">Monitorar o armazenamento OLTP na memória</span><span class="sxs-lookup"><span data-stu-id="04188-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="04188-104">Ao usar o [In-Memory OLTP](sql-database-in-memory.md), os dados em tabelas com otimização de memória e as variáveis de tabela residem no armazenamento OLTP in-memory.</span><span class="sxs-lookup"><span data-stu-id="04188-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="04188-105">Cada camada de serviço Premium tem um tamanho de armazenamento máximo do OLTP na memória, que está documentado na Olá [artigo de camadas de serviço de banco de dados do SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="04188-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="04188-106">Quando esse limite for excedido, as operações insert e update poderão começar a falhar (com o erro 41823).</span><span class="sxs-lookup"><span data-stu-id="04188-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="04188-107">Nesse momento você precisa de memória de tooreclaim tooeither excluir dados ou atualizar a camada de desempenho de saudação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04188-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="04188-108">Determinar se dados serão ajustadas dentro do limite de armazenamento na memória Olá</span><span class="sxs-lookup"><span data-stu-id="04188-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="04188-109">Determinar o limite de armazenamento Olá: consulte Olá [artigo de camadas de serviço de banco de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para limites de armazenamento Olá das diferentes camadas de serviço Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="04188-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="04188-110">Estimar memória requisitos para uma tabela com otimização de memória funciona Olá mesmo como para o SQL Server como ele faz no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="04188-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="04188-111">Assumir tooreview de alguns minutos esse tópico [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="04188-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="04188-112">Observe que a tabela hello e linhas de variável de tabela, bem como índices, contam para o tamanho de dados de usuário max hello.</span><span class="sxs-lookup"><span data-stu-id="04188-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="04188-113">Além disso, ALTER TABLE precisa toocreate suficiente espaço uma nova versão da tabela inteira hello e seus índices.</span><span class="sxs-lookup"><span data-stu-id="04188-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="04188-114">Monitoramento e alertas</span><span class="sxs-lookup"><span data-stu-id="04188-114">Monitoring and alerting</span></span>
<span data-ttu-id="04188-115">Você pode monitorar o uso de armazenamento na memória como uma porcentagem da saudação [limite de armazenamento para o nível de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) em hello Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="04188-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="04188-116">Na folha de banco de dados Olá, localize a caixa de utilização de recurso hello e clique em Editar.</span><span class="sxs-lookup"><span data-stu-id="04188-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="04188-117">Em seguida, selecione a métrica de saudação `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="04188-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="04188-118">tooadd um alerta, clique na folha da métrica de Olá Olá utilização de recursos caixa tooopen, clique em Adicionar alerta.</span><span class="sxs-lookup"><span data-stu-id="04188-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="04188-119">Ou use Olá utilização de armazenamento na memória consulta tooshow Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="04188-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="04188-120">Corrigir situações de memória insuficiente - Erro 41823</span><span class="sxs-lookup"><span data-stu-id="04188-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="04188-121">A insuficiência de memória resulta na falha das operações INSERT, UPDATE e CREATE com a mensagem de erro 41823.</span><span class="sxs-lookup"><span data-stu-id="04188-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="04188-122">Mensagem de erro 41823 indica que as tabelas com otimização de memória hello e variáveis de tabela excedeu o tamanho máximo de saudação.</span><span class="sxs-lookup"><span data-stu-id="04188-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="04188-123">tooresolve esse erro, ou:</span><span class="sxs-lookup"><span data-stu-id="04188-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="04188-124">Excluir dados de tabelas com otimização de memória hello, tootraditional potencialmente descarregamento de dados hello, tabelas baseadas em disco. ou,</span><span class="sxs-lookup"><span data-stu-id="04188-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="04188-125">Atualizar Olá tooone de nível de serviço com armazenamento suficiente de memória para dados de saudação é necessário tookeep nas tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="04188-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04188-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04188-126">Next steps</span></span>
<span data-ttu-id="04188-127">Para obter diretrizes sobre monitoramento, consulte [Monitoramento de Banco de Dados SQL do Azure usando exibições de gerenciamento dinâmico](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="04188-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
