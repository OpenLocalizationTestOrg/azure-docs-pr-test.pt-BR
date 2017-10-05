---
title: Eventos estendidos no Banco de Dados SQL | Microsoft Doc
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
ms.openlocfilehash: 7e5da1c32484b0b94d2ad32ead6bb7c28f9744aa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="aea18-103">Eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="aea18-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="aea18-104">Este tópico explica como a implementação de eventos estendidos no Banco de Dados SQL do Azure é um pouco diferente em comparação aos eventos estendidos no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aea18-104">This topic explains how the implementation of extended events in Azure SQL Database is slightly different compared to extended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="aea18-105">O Banco de Dados SQL V12 recebeu o recurso de eventos estendidos na segunda metade de 2015.</span><span class="sxs-lookup"><span data-stu-id="aea18-105">SQL Database V12 gained the extended events feature in the second half of calendar 2015.</span></span>
- <span data-ttu-id="aea18-106">O SQL Server já tem eventos estendidos desde 2008.</span><span class="sxs-lookup"><span data-stu-id="aea18-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="aea18-107">O conjunto de recursos de eventos estendidos no Banco de Dados SQL é um subconjunto robusto dos recursos do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aea18-107">The feature set of extended events on SQL Database is a robust subset of the features on SQL Server.</span></span>

<span data-ttu-id="aea18-108">*XEvents* é um apelido informal usado às vezes para "eventos estendidos" em blogs e outras fontes de informações.</span><span class="sxs-lookup"><span data-stu-id="aea18-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="aea18-109">Informações adicionais sobre eventos estendidos, para Banco de Dados SQL e Microsoft SQL Server, estão disponíveis em:</span><span class="sxs-lookup"><span data-stu-id="aea18-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="aea18-110">Início Rápido: eventos estendidos no SQL Server</span><span class="sxs-lookup"><span data-stu-id="aea18-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="aea18-111">Eventos estendidos</span><span class="sxs-lookup"><span data-stu-id="aea18-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="aea18-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aea18-112">Prerequisites</span></span>

<span data-ttu-id="aea18-113">Este tópico pressupõe que você já tem algum conhecimento de:</span><span class="sxs-lookup"><span data-stu-id="aea18-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="aea18-114">[Serviço do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="aea18-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="aea18-115">[Eventos estendidos](http://msdn.microsoft.com/library/bb630282.aspx) no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aea18-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="aea18-116">A maior parte da nossa documentação sobre eventos estendidos se aplica ao SQL Server e ao Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="aea18-116">The bulk of our documentation about extended events applies to both SQL Server and SQL Database.</span></span>

<span data-ttu-id="aea18-117">A exposição prévia aos itens a seguir é útil ao escolher o Arquivo de Evento como o [destino](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="aea18-117">Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="aea18-118">Serviço de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="aea18-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="aea18-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aea18-119">PowerShell</span></span>
    - <span data-ttu-id="aea18-120">[Usando o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) - fornece informações abrangentes sobre o PowerShell e o serviço de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aea18-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="aea18-121">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="aea18-121">Code samples</span></span>

<span data-ttu-id="aea18-122">Os tópicos relacionados fornecem dois exemplos de código:</span><span class="sxs-lookup"><span data-stu-id="aea18-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="aea18-123">Código de destino do Buffer de Anéis para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="aea18-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="aea18-124">Script curto e simples de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="aea18-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="aea18-125">Enfatizamos no tópico do exemplo de código que, quando você concluir um destino de Buffer de Anéis, será necessário liberar seus recursos executando uma instrução alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` .</span><span class="sxs-lookup"><span data-stu-id="aea18-125">We emphasize in the code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="aea18-126">Mais tarde, você poderá adicionar outra instância do Buffer de Anéis com `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="aea18-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="aea18-127">Código de destino do Arquivo de evento para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="aea18-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="aea18-128">A Fase 1 é PowerShell a fim de criar o contêiner de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="aea18-128">Phase 1 is PowerShell to create an Azure Storage container.</span></span>
    - <span data-ttu-id="aea18-129">Fase 2 é Transact-SQL que usa o contêiner de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aea18-129">Phase 2 is Transact-SQL that uses the Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="aea18-130">Diferenças do Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="aea18-130">Transact-SQL differences</span></span>


- <span data-ttu-id="aea18-131">Ao executar o comando [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) no SQL Server, você usa a cláusula **ON SERVER** .</span><span class="sxs-lookup"><span data-stu-id="aea18-131">When you execute the [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use the **ON SERVER** clause.</span></span> <span data-ttu-id="aea18-132">Mas, no Banco de Dados SQL, você usa a cláusula **ON DATABASE** .</span><span class="sxs-lookup"><span data-stu-id="aea18-132">But on SQL Database you use the **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="aea18-133">A cláusula **ON DATABASE** também se aplica aos comandos Transact-SQL [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) e [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx).</span><span class="sxs-lookup"><span data-stu-id="aea18-133">The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="aea18-134">Uma prática recomendada é incluir a opção de sessão de evento de **STARTUP_STATE = ON** em sua instrução **CREATE EVENT SESSION** ou **ALTER EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="aea18-134">A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="aea18-135">O valor **= ON** oferece suporte à reinicialização automática após a reconfiguração do banco de dados lógico devido a um failover.</span><span class="sxs-lookup"><span data-stu-id="aea18-135">The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="aea18-136">Novas exibições do catálogo</span><span class="sxs-lookup"><span data-stu-id="aea18-136">New catalog views</span></span>

<span data-ttu-id="aea18-137">O recurso de eventos estendidos recebe suporte de várias [exibições do catálogo](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="aea18-137">The extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="aea18-138">As exibições do catálogo mostram *metadados ou definições* de sessões de eventos criadas pelo usuário no banco de dados atual.</span><span class="sxs-lookup"><span data-stu-id="aea18-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database.</span></span> <span data-ttu-id="aea18-139">As exibições não retornam informações sobre as instâncias de sessões de eventos ativas.</span><span class="sxs-lookup"><span data-stu-id="aea18-139">The views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="aea18-140">Nome da</span><span class="sxs-lookup"><span data-stu-id="aea18-140">Name of</span></span><br/><span data-ttu-id="aea18-141">exibição do catálogo</span><span class="sxs-lookup"><span data-stu-id="aea18-141">catalog view</span></span> | <span data-ttu-id="aea18-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="aea18-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="aea18-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="aea18-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="aea18-144">Retorna uma linha para cada ação em cada evento de uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="aea18-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="aea18-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="aea18-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="aea18-146">Retorna uma linha para cada evento em uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="aea18-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="aea18-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="aea18-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="aea18-148">Retorna uma linha para cada coluna personalizável que foi explicitamente definida em eventos e destinos.</span><span class="sxs-lookup"><span data-stu-id="aea18-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="aea18-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="aea18-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="aea18-150">Retorna uma linha para cada destino de evento em uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="aea18-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="aea18-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="aea18-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="aea18-152">Retorna uma linha para cada sessão de eventos no banco de dados do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="aea18-152">Returns a row for each event session in the SQL Database database.</span></span> |

<span data-ttu-id="aea18-153">No Microsoft SQL Server, exibições do catálogo semelhantes têm nomes que incluem *.server\_* em vez de *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="aea18-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="aea18-154">O nome padrão é **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="aea18-154">The name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="aea18-155">Novas exibições de gerenciamento dinâmico [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="aea18-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="aea18-156">O Banco de Dados SQL do Azure tem [exibições de gerenciamento dinâmico (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) que dão suporte a eventos estendidos.</span><span class="sxs-lookup"><span data-stu-id="aea18-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="aea18-157">DMVs mostram as sessões de evento *ativas* .</span><span class="sxs-lookup"><span data-stu-id="aea18-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="aea18-158">Nome da DMV</span><span class="sxs-lookup"><span data-stu-id="aea18-158">Name of DMV</span></span> | <span data-ttu-id="aea18-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="aea18-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="aea18-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="aea18-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="aea18-161">Retorna informações sobre ações da sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="aea18-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="aea18-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="aea18-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="aea18-163">Retorna informações sobre eventos da sessão.</span><span class="sxs-lookup"><span data-stu-id="aea18-163">Returns information about session events.</span></span> |
| <span data-ttu-id="aea18-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="aea18-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="aea18-165">Mostra os valores de configuração para objetos associados a uma sessão.</span><span class="sxs-lookup"><span data-stu-id="aea18-165">Shows the configuration values for objects that are bound to a session.</span></span> |
| <span data-ttu-id="aea18-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="aea18-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="aea18-167">Retorna informações sobre os destinos da sessão.</span><span class="sxs-lookup"><span data-stu-id="aea18-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="aea18-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="aea18-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="aea18-169">Retorna uma linha para cada sessão de evento com escopo no banco de dados atual.</span><span class="sxs-lookup"><span data-stu-id="aea18-169">Returns a row for each event session that is scoped to the current database.</span></span> |

<span data-ttu-id="aea18-170">No Microsoft SQL Server, as exibições de catálogo semelhantes recebem um nome sem a parte *\_database*, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aea18-170">In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:</span></span>

- <span data-ttu-id="aea18-171">**sys.dm_xe_sessions**, em vez de nome</span><span class="sxs-lookup"><span data-stu-id="aea18-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="aea18-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="aea18-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-to-both"></a><span data-ttu-id="aea18-173">DMVs comuns a ambos</span><span class="sxs-lookup"><span data-stu-id="aea18-173">DMVs common to both</span></span>
<span data-ttu-id="aea18-174">Para eventos estendidos, há DMVs adicionais que são comuns ao Banco de Dados SQL do Azure e ao Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="aea18-174">For extended events there are additional DMVs that are common to both Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="aea18-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="aea18-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="aea18-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="aea18-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="aea18-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="aea18-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="aea18-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="aea18-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-the-available-extended-events-actions-and-targets"></a><span data-ttu-id="aea18-179">Localizar os eventos estendidos, ações e destinos disponíveis</span><span class="sxs-lookup"><span data-stu-id="aea18-179">Find the available extended events, actions, and targets</span></span>

<span data-ttu-id="aea18-180">Você pode executar um simples SQL **SELECT** para obter uma lista dos evento, ações e destino disponíveis.</span><span class="sxs-lookup"><span data-stu-id="aea18-180">You can run a simple SQL **SELECT** to obtain a list of the available events, actions, and target.</span></span>

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


<span data-ttu-id="aea18-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="aea18-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="aea18-182">Destinos para as sessões de evento do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="aea18-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="aea18-183">Estes são os destinos que podem capturar resultados de suas sessões de evento no Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="aea18-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="aea18-184">[Destino de Buffer de Anéis](http://msdn.microsoft.com/library/ff878182.aspx) - armazena dados na memória por um curto período.</span><span class="sxs-lookup"><span data-stu-id="aea18-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="aea18-185">[Destino de Contador de eventos](http://msdn.microsoft.com/library/ff878025.aspx) - conta todos os eventos que ocorrem durante uma sessão de eventos estendidos.</span><span class="sxs-lookup"><span data-stu-id="aea18-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="aea18-186">[Destino de Arquivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) - grava buffers completos em um contêiner de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aea18-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers to an Azure Storage container.</span></span>

<span data-ttu-id="aea18-187">A API [Rastreamento de Eventos para Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) não está disponível para eventos estendidos no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="aea18-187">The [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="aea18-188">Restrições</span><span class="sxs-lookup"><span data-stu-id="aea18-188">Restrictions</span></span>

<span data-ttu-id="aea18-189">Há algumas diferenças relacionadas à segurança condizentes com o ambiente de nuvem do Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="aea18-189">There are a couple of security-related differences befitting the cloud environment of SQL Database:</span></span>

- <span data-ttu-id="aea18-190">Os eventos estendidos são baseados no modelo de isolamento de locatário único.</span><span class="sxs-lookup"><span data-stu-id="aea18-190">Extended events are founded on the single-tenant isolation model.</span></span> <span data-ttu-id="aea18-191">Uma sessão de eventos em um banco de dados não pode acessar dados ou eventos de outro banco de dados.</span><span class="sxs-lookup"><span data-stu-id="aea18-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="aea18-192">Não é possível emitir uma instrução **CREATE EVENT SESSION** no contexto do banco de dados **mestre**.</span><span class="sxs-lookup"><span data-stu-id="aea18-192">You cannot issue a **CREATE EVENT SESSION** statement in the context of the **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="aea18-193">Modelo de permissão</span><span class="sxs-lookup"><span data-stu-id="aea18-193">Permission model</span></span>

<span data-ttu-id="aea18-194">Você deve ter permissão de **Controle** no banco de dados para emitir uma instrução **CREATE EVENT SESSION**.</span><span class="sxs-lookup"><span data-stu-id="aea18-194">You must have **Control** permission on the database to issue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="aea18-195">O proprietário do banco de dados (dbo) tem a permissão de **Controle** .</span><span class="sxs-lookup"><span data-stu-id="aea18-195">The database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="aea18-196">Autorizações de contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="aea18-196">Storage container authorizations</span></span>

<span data-ttu-id="aea18-197">O token SAS gerado para o contêiner de Armazenamento do Azure deve especificar **rwl** para as permissões.</span><span class="sxs-lookup"><span data-stu-id="aea18-197">The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions.</span></span> <span data-ttu-id="aea18-198">O valor **rwl** fornece as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="aea18-198">The **rwl** value provides the following permissions:</span></span>

- <span data-ttu-id="aea18-199">Ler</span><span class="sxs-lookup"><span data-stu-id="aea18-199">Read</span></span>
- <span data-ttu-id="aea18-200">Gravar</span><span class="sxs-lookup"><span data-stu-id="aea18-200">Write</span></span>
- <span data-ttu-id="aea18-201">Listar</span><span class="sxs-lookup"><span data-stu-id="aea18-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="aea18-202">Considerações sobre o desempenho</span><span class="sxs-lookup"><span data-stu-id="aea18-202">Performance considerations</span></span>

<span data-ttu-id="aea18-203">Há situações nas quais o uso intensivo de eventos estendidos pode acumular mais memória ativa do que o recomendado para a integridade geral do sistema.</span><span class="sxs-lookup"><span data-stu-id="aea18-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system.</span></span> <span data-ttu-id="aea18-204">Portanto, o sistema do Banco de Dados SQL do Azure define e ajusta dinamicamente os limites para a quantidade de memória ativa que pode ser acumulada por uma sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="aea18-204">Therefore the Azure SQL Database system dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="aea18-205">Muitos fatores pesam no cálculo dinâmico.</span><span class="sxs-lookup"><span data-stu-id="aea18-205">Many factors go into the dynamic calculation.</span></span>

<span data-ttu-id="aea18-206">Se você receber uma mensagem de erro informando que há uma imposição de quantidade máxima de memória, estas são algumas das ações corretivas possíveis:</span><span class="sxs-lookup"><span data-stu-id="aea18-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="aea18-207">Executar menos sessões simultâneas do evento.</span><span class="sxs-lookup"><span data-stu-id="aea18-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="aea18-208">Por meio das instruções **CREATE** e **ALTER** das sessões de evento, reduza a quantidade de memória que você especifica na cláusula **MAX\_MEMORY**.</span><span class="sxs-lookup"><span data-stu-id="aea18-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="aea18-209">Latência da rede</span><span class="sxs-lookup"><span data-stu-id="aea18-209">Network latency</span></span>

<span data-ttu-id="aea18-210">O destino **Arquivo de Evento** pode enfrentar latência de rede ou falhas ao persistir dados para blobs de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aea18-210">The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs.</span></span> <span data-ttu-id="aea18-211">Outros eventos no Banco de Dados SQL podem ser atrasados enquanto esperam a conclusão da comunicação de rede.</span><span class="sxs-lookup"><span data-stu-id="aea18-211">Other events in SQL Database might be delayed while they wait for the network communication to complete.</span></span> <span data-ttu-id="aea18-212">Esse atraso pode retardar sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="aea18-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="aea18-213">Para reduzir esse risco de desempenho, evite configurar a opção **EVENT_RETENTION_MODE** como **NO_EVENT_LOSS** nas definições de sua sessão de eventos.</span><span class="sxs-lookup"><span data-stu-id="aea18-213">To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="aea18-214">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="aea18-214">Related links</span></span>

- <span data-ttu-id="aea18-215">[Usando o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="aea18-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="aea18-216">Cmdlets do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="aea18-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="aea18-217">[Usando o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) - fornece informações abrangentes sobre o PowerShell e o serviço de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aea18-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and the Azure Storage service.</span></span>
- [<span data-ttu-id="aea18-218">Como usar o Armazenamento de blob do .NET</span><span class="sxs-lookup"><span data-stu-id="aea18-218">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="aea18-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="aea18-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="aea18-220">CREATE EVENT SESSION (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="aea18-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="aea18-221">Postagens do blog de Jonathan Kehayias sobre eventos estendidos no Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="aea18-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="aea18-222">A página Web *Atualizações de Serviço* do Azure, limitada com o parâmetro para o Banco de Dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="aea18-222">The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:</span></span>
    - [<span data-ttu-id="aea18-223">https://azure.microsoft.com/updates/?service=sql-database</span><span class="sxs-lookup"><span data-stu-id="aea18-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="aea18-224">Outros tópicos com exemplos de código para eventos estendidos estão disponíveis nos links a seguir.</span><span class="sxs-lookup"><span data-stu-id="aea18-224">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="aea18-225">No entanto, você deve verificar regularmente os exemplos para ver se eles se destinam ao Microsoft SQL Server ou ao Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="aea18-225">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="aea18-226">Assim você pode decidir se pequenas alterações são necessárias para a execução do exemplo.</span><span class="sxs-lookup"><span data-stu-id="aea18-226">Then you can decide whether minor changes are needed to run the sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
