---
title: eventos de aaaExtended no banco de dados SQL | Microsoft Docs
description: "Descreve eventos estendidos (XEvents) no Banco de Dados SQL do Azure e como as sessões de eventos diferem ligeiramente das sessões de eventos no Microsoft SQL Server."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="954d8-103">Eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="954d8-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="954d8-104">Este tópico explica como a implementação de saudação de eventos estendidos no banco de dados do SQL Azure é eventos tooextended em comparação com um pouco diferente no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="954d8-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="954d8-105">SQL Database V12 decorrente recurso eventos estendidos Olá Olá segundo metade do calendário 2015.</span><span class="sxs-lookup"><span data-stu-id="954d8-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="954d8-106">O SQL Server já tem eventos estendidos desde 2008.</span><span class="sxs-lookup"><span data-stu-id="954d8-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="954d8-107">conjunto de recursos de saudação de eventos estendidos no banco de dados SQL é um subconjunto robusto de recursos de saudação no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="954d8-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="954d8-108">*XEvents* é um apelido informal usado às vezes para "eventos estendidos" em blogs e outras fontes de informações.</span><span class="sxs-lookup"><span data-stu-id="954d8-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="954d8-109">Informações adicionais sobre eventos estendidos, para Banco de Dados SQL e Microsoft SQL Server, estão disponíveis em:</span><span class="sxs-lookup"><span data-stu-id="954d8-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="954d8-110">Início Rápido: eventos estendidos no SQL Server</span><span class="sxs-lookup"><span data-stu-id="954d8-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="954d8-111">Eventos estendidos</span><span class="sxs-lookup"><span data-stu-id="954d8-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="954d8-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="954d8-112">Prerequisites</span></span>

<span data-ttu-id="954d8-113">Este tópico pressupõe que você já tem algum conhecimento de:</span><span class="sxs-lookup"><span data-stu-id="954d8-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="954d8-114">[Serviço do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="954d8-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="954d8-115">[Eventos estendidos](http://msdn.microsoft.com/library/bb630282.aspx) no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="954d8-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="954d8-116">aplica-se em massa de saudação de nossa documentação sobre eventos estendidos tooboth do SQL Server e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="954d8-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="954d8-117">Exposição anterior toohello itens a seguir é útil ao escolher Olá arquivo de evento como Olá [destino](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="954d8-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="954d8-118">Serviço de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="954d8-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="954d8-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="954d8-119">PowerShell</span></span>
    - <span data-ttu-id="954d8-120">[Usando o PowerShell do Azure com o armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="954d8-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="954d8-121">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="954d8-121">Code samples</span></span>

<span data-ttu-id="954d8-122">Os tópicos relacionados fornecem dois exemplos de código:</span><span class="sxs-lookup"><span data-stu-id="954d8-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="954d8-123">Código de destino do Buffer de Anéis para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="954d8-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="954d8-124">Script curto e simples de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="954d8-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="954d8-125">Enfatizamos no tópico de exemplo de código Olá que, quando você terminar com um destino de Buffer de anel, você deve liberar seus recursos executando um drop alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrução.</span><span class="sxs-lookup"><span data-stu-id="954d8-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="954d8-126">Mais tarde, você poderá adicionar outra instância do Buffer de Anéis com `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="954d8-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="954d8-127">Código de destino do Arquivo de evento para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="954d8-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="954d8-128">Fase 1 é toocreate PowerShell um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="954d8-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="954d8-129">Fase 2 é Transact-SQL que usa o contêiner de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="954d8-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="954d8-130">Diferenças do Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="954d8-130">Transact-SQL differences</span></span>


- <span data-ttu-id="954d8-131">Quando você executa Olá [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) comando no SQL Server, use Olá **ON SERVER** cláusula.</span><span class="sxs-lookup"><span data-stu-id="954d8-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="954d8-132">Mas no banco de dados SQL é usar Olá **ON DATABASE** cláusula em vez disso.</span><span class="sxs-lookup"><span data-stu-id="954d8-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="954d8-133">Olá **ON DATABASE** cláusula também se aplica a toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) e [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) comandos Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="954d8-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="954d8-134">Uma prática recomendada é a opção de sessão de evento tooinclude Olá de **STARTUP_STATE = ON** no seu **CREATE EVENT SESSION** ou **ALTER EVENT SESSION** instruções.</span><span class="sxs-lookup"><span data-stu-id="954d8-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="954d8-135">Olá **= ON** valor dá suporte a uma reinicialização automática após a reconfiguração do banco de dados lógico devido a failover tooa hello.</span><span class="sxs-lookup"><span data-stu-id="954d8-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="954d8-136">Novas exibições do catálogo</span><span class="sxs-lookup"><span data-stu-id="954d8-136">New catalog views</span></span>

<span data-ttu-id="954d8-137">Olá recurso eventos estendidos tem suporte em vários [exibições do catálogo](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="954d8-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="954d8-138">Exibições do catálogo informam sobre *metadados ou definições* de sessões de eventos criados pelo usuário no banco de dados atual hello.</span><span class="sxs-lookup"><span data-stu-id="954d8-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="954d8-139">exibições de saudação não retornam informações sobre as instâncias de sessões de eventos ativos.</span><span class="sxs-lookup"><span data-stu-id="954d8-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="954d8-140">Nome da</span><span class="sxs-lookup"><span data-stu-id="954d8-140">Name of</span></span><br/><span data-ttu-id="954d8-141">exibição do catálogo</span><span class="sxs-lookup"><span data-stu-id="954d8-141">catalog view</span></span> | <span data-ttu-id="954d8-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="954d8-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="954d8-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="954d8-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="954d8-144">Retorna uma linha para cada ação em cada evento de uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="954d8-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="954d8-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="954d8-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="954d8-146">Retorna uma linha para cada evento em uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="954d8-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="954d8-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="954d8-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="954d8-148">Retorna uma linha para cada coluna personalizável que foi explicitamente definida em eventos e destinos.</span><span class="sxs-lookup"><span data-stu-id="954d8-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="954d8-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="954d8-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="954d8-150">Retorna uma linha para cada destino de evento em uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="954d8-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="954d8-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="954d8-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="954d8-152">Retorna uma linha para cada sessão de evento no banco de dados de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="954d8-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="954d8-153">No Microsoft SQL Server, exibições do catálogo semelhantes têm nomes que incluem *.server\_* em vez de *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="954d8-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="954d8-154">é o padrão de nome Hello como **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="954d8-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="954d8-155">Novas exibições de gerenciamento dinâmico [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="954d8-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="954d8-156">O Banco de Dados SQL do Azure tem [exibições de gerenciamento dinâmico (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) que dão suporte a eventos estendidos.</span><span class="sxs-lookup"><span data-stu-id="954d8-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="954d8-157">DMVs mostram as sessões de evento *ativas* .</span><span class="sxs-lookup"><span data-stu-id="954d8-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="954d8-158">Nome da DMV</span><span class="sxs-lookup"><span data-stu-id="954d8-158">Name of DMV</span></span> | <span data-ttu-id="954d8-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="954d8-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="954d8-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="954d8-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="954d8-161">Retorna informações sobre ações da sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="954d8-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="954d8-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="954d8-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="954d8-163">Retorna informações sobre eventos da sessão.</span><span class="sxs-lookup"><span data-stu-id="954d8-163">Returns information about session events.</span></span> |
| <span data-ttu-id="954d8-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="954d8-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="954d8-165">Mostra os valores de configuração de saudação para objetos de sessão tooa associado.</span><span class="sxs-lookup"><span data-stu-id="954d8-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="954d8-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="954d8-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="954d8-167">Retorna informações sobre os destinos da sessão.</span><span class="sxs-lookup"><span data-stu-id="954d8-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="954d8-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="954d8-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="954d8-169">Retorna uma linha para cada sessão de evento que é o banco de dados toohello no escopo atual.</span><span class="sxs-lookup"><span data-stu-id="954d8-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="954d8-170">No Microsoft SQL Server, exibições de catálogo semelhantes são nomeadas sem Olá  *\_banco de dados* parte da saudação nome, como:</span><span class="sxs-lookup"><span data-stu-id="954d8-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="954d8-171">**sys.dm_xe_sessions**, em vez de nome</span><span class="sxs-lookup"><span data-stu-id="954d8-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="954d8-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="954d8-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="954d8-173">Tooboth comuns DMVs</span><span class="sxs-lookup"><span data-stu-id="954d8-173">DMVs common tooboth</span></span>
<span data-ttu-id="954d8-174">Para eventos estendidos há DMVs adicionais que são comuns tooboth banco de dados do SQL Azure e o Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="954d8-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="954d8-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="954d8-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="954d8-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="954d8-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="954d8-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="954d8-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="954d8-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="954d8-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="954d8-179">Localizar os eventos estendidos disponível hello, ações e destinos</span><span class="sxs-lookup"><span data-stu-id="954d8-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="954d8-180">Você pode executar um SQL simple **selecione** tooobtain uma lista de eventos disponíveis hello, ações e destino.</span><span class="sxs-lookup"><span data-stu-id="954d8-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="954d8-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="954d8-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="954d8-182">Destinos para as sessões de evento do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="954d8-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="954d8-183">Estes são os destinos que podem capturar resultados de suas sessões de evento no Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="954d8-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="954d8-184">[Destino de Buffer de Anéis](http://msdn.microsoft.com/library/ff878182.aspx) - armazena dados na memória por um curto período.</span><span class="sxs-lookup"><span data-stu-id="954d8-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="954d8-185">[Destino de Contador de eventos](http://msdn.microsoft.com/library/ff878025.aspx) - conta todos os eventos que ocorrem durante uma sessão de eventos estendidos.</span><span class="sxs-lookup"><span data-stu-id="954d8-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="954d8-186">[Destino de arquivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) -contêiner de armazenamento do Azure grava buffers completos tooan.</span><span class="sxs-lookup"><span data-stu-id="954d8-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="954d8-187">Olá [rastreamento de eventos para Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API não está disponível para eventos estendidos no banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="954d8-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="954d8-188">Restrições</span><span class="sxs-lookup"><span data-stu-id="954d8-188">Restrictions</span></span>

<span data-ttu-id="954d8-189">Há algumas diferenças relacionadas à segurança, assumindo o ambiente de nuvem de saudação do banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="954d8-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="954d8-190">Eventos estendidos são fundamentados no modelo de isolamento de único locatário hello.</span><span class="sxs-lookup"><span data-stu-id="954d8-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="954d8-191">Uma sessão de eventos em um banco de dados não pode acessar dados ou eventos de outro banco de dados.</span><span class="sxs-lookup"><span data-stu-id="954d8-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="954d8-192">Não é possível emitir um **CREATE EVENT SESSION** instrução no contexto de saudação do hello **mestre** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="954d8-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="954d8-193">Modelo de permissão</span><span class="sxs-lookup"><span data-stu-id="954d8-193">Permission model</span></span>

<span data-ttu-id="954d8-194">Você deve ter **controle** permissão Olá banco de dados tooissue uma **CREATE EVENT SESSION** instrução.</span><span class="sxs-lookup"><span data-stu-id="954d8-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="954d8-195">Olá proprietário de banco de dados (dbo) possui **controle** permissão.</span><span class="sxs-lookup"><span data-stu-id="954d8-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="954d8-196">Autorizações de contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="954d8-196">Storage container authorizations</span></span>

<span data-ttu-id="954d8-197">token SAS Olá gerar para seu contêiner de armazenamento do Azure deve especificar **rwl** para permissões de saudação.</span><span class="sxs-lookup"><span data-stu-id="954d8-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="954d8-198">Olá **rwl** valor fornece Olá as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="954d8-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="954d8-199">Ler</span><span class="sxs-lookup"><span data-stu-id="954d8-199">Read</span></span>
- <span data-ttu-id="954d8-200">Gravar</span><span class="sxs-lookup"><span data-stu-id="954d8-200">Write</span></span>
- <span data-ttu-id="954d8-201">Listar</span><span class="sxs-lookup"><span data-stu-id="954d8-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="954d8-202">Considerações sobre o desempenho</span><span class="sxs-lookup"><span data-stu-id="954d8-202">Performance considerations</span></span>

<span data-ttu-id="954d8-203">Existem cenários onde um uso intensivo de eventos estendidos pode ser acumuladas ativa mais memória do que íntegro para Olá geral do sistema.</span><span class="sxs-lookup"><span data-stu-id="954d8-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="954d8-204">Portanto hello sistema de banco de dados SQL dinamicamente define e ajusta os limites de quantidade de saudação de memória ativa que pode ser acumulada por uma sessão de evento.</span><span class="sxs-lookup"><span data-stu-id="954d8-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="954d8-205">Muitos fatores levam ao cálculo dinâmico Olá.</span><span class="sxs-lookup"><span data-stu-id="954d8-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="954d8-206">Se você receber uma mensagem de erro informando que há uma imposição de quantidade máxima de memória, estas são algumas das ações corretivas possíveis:</span><span class="sxs-lookup"><span data-stu-id="954d8-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="954d8-207">Executar menos sessões simultâneas do evento.</span><span class="sxs-lookup"><span data-stu-id="954d8-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="954d8-208">Por meio de seu **criar** e **ALTER** instruções para sessões de evento, reduzir a quantidade de saudação de memória que você especificar na Olá **MAX\_memória** cláusula.</span><span class="sxs-lookup"><span data-stu-id="954d8-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="954d8-209">Latência da rede</span><span class="sxs-lookup"><span data-stu-id="954d8-209">Network latency</span></span>

<span data-ttu-id="954d8-210">Olá **arquivo de evento** destino pode experimentar latência de rede ou falhas durante a persistência tooAzure dados blobs de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="954d8-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="954d8-211">Outros eventos no banco de dados SQL podem ser atrasados enquanto esperam Olá toocomplete de comunicação de rede.</span><span class="sxs-lookup"><span data-stu-id="954d8-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="954d8-212">Esse atraso pode retardar sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="954d8-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="954d8-213">toomitigate esse desempenho de risco, evite definir Olá **EVENT_RETENTION_MODE** opção muito**NO_EVENT_LOSS** em suas definições de sessão de evento.</span><span class="sxs-lookup"><span data-stu-id="954d8-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="954d8-214">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="954d8-214">Related links</span></span>

- <span data-ttu-id="954d8-215">[Usando o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="954d8-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="954d8-216">Cmdlets do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="954d8-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="954d8-217">[Usando o PowerShell do Azure com o armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="954d8-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="954d8-218">Como toouse armazenamento de BLOBs no .NET</span><span class="sxs-lookup"><span data-stu-id="954d8-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="954d8-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="954d8-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="954d8-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="954d8-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="954d8-221">Postagens do blog de Jonathan Kehayias sobre eventos estendidos no Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="954d8-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="954d8-222">Hello Azure *atualizações de serviço* página da Web, com o parâmetro tooAzure banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="954d8-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="954d8-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="954d8-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="954d8-224">Outros tópicos de exemplo de código para eventos estendidos estão disponíveis em Olá links a seguir.</span><span class="sxs-lookup"><span data-stu-id="954d8-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="954d8-225">No entanto, você deve verificar rotineiramente qualquer toosee de exemplo se o exemplo hello tem como alvo o Microsoft SQL Server em vez do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="954d8-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="954d8-226">Em seguida, você pode decidir se alterações secundárias são exemplo hello de toorun necessários.</span><span class="sxs-lookup"><span data-stu-id="954d8-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
