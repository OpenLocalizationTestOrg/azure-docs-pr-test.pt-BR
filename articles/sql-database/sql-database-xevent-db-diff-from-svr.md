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
# <a name="extended-events-in-sql-database"></a>Eventos estendidos no Banco de Dados SQL
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Este tópico explica como a implementação de saudação de eventos estendidos no banco de dados do SQL Azure é eventos tooextended em comparação com um pouco diferente no Microsoft SQL Server.

- SQL Database V12 decorrente recurso eventos estendidos Olá Olá segundo metade do calendário 2015.
- O SQL Server já tem eventos estendidos desde 2008.
- conjunto de recursos de saudação de eventos estendidos no banco de dados SQL é um subconjunto robusto de recursos de saudação no SQL Server.

*XEvents* é um apelido informal usado às vezes para "eventos estendidos" em blogs e outras fontes de informações.

Informações adicionais sobre eventos estendidos, para Banco de Dados SQL e Microsoft SQL Server, estão disponíveis em:

- [Início Rápido: eventos estendidos no SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Eventos estendidos](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Pré-requisitos

Este tópico pressupõe que você já tem algum conhecimento de:

- [Serviço do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/)
- [Eventos estendidos](http://msdn.microsoft.com/library/bb630282.aspx) no Microsoft SQL Server.

- aplica-se em massa de saudação de nossa documentação sobre eventos estendidos tooboth do SQL Server e banco de dados SQL.

Exposição anterior toohello itens a seguir é útil ao escolher Olá arquivo de evento como Olá [destino](#AzureXEventsTargets):

- [Serviço de Armazenamento do Azure](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [Usando o PowerShell do Azure com o armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço de armazenamento do Azure.

## <a name="code-samples"></a>Exemplos de código

Os tópicos relacionados fornecem dois exemplos de código:


- [Código de destino do Buffer de Anéis para eventos estendidos no Banco de Dados SQL](sql-database-xevent-code-ring-buffer.md)
    - Script curto e simples de Transact-SQL.
    - Enfatizamos no tópico de exemplo de código Olá que, quando você terminar com um destino de Buffer de anel, você deve liberar seus recursos executando um drop alter `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instrução. Mais tarde, você poderá adicionar outra instância do Buffer de Anéis com `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Código de destino do Arquivo de evento para eventos estendidos no Banco de Dados SQL](sql-database-xevent-code-event-file.md)
    - Fase 1 é toocreate PowerShell um contêiner de armazenamento do Azure.
    - Fase 2 é Transact-SQL que usa o contêiner de armazenamento do Azure hello.

## <a name="transact-sql-differences"></a>Diferenças do Transact-SQL


- Quando você executa Olá [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) comando no SQL Server, use Olá **ON SERVER** cláusula. Mas no banco de dados SQL é usar Olá **ON DATABASE** cláusula em vez disso.


- Olá **ON DATABASE** cláusula também se aplica a toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) e [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) comandos Transact-SQL.


- Uma prática recomendada é a opção de sessão de evento tooinclude Olá de **STARTUP_STATE = ON** no seu **CREATE EVENT SESSION** ou **ALTER EVENT SESSION** instruções.
    - Olá **= ON** valor dá suporte a uma reinicialização automática após a reconfiguração do banco de dados lógico devido a failover tooa hello.

## <a name="new-catalog-views"></a>Novas exibições do catálogo

Olá recurso eventos estendidos tem suporte em vários [exibições do catálogo](http://msdn.microsoft.com/library/ms174365.aspx). Exibições do catálogo informam sobre *metadados ou definições* de sessões de eventos criados pelo usuário no banco de dados atual hello. exibições de saudação não retornam informações sobre as instâncias de sessões de eventos ativos.

| Nome da<br/>exibição do catálogo | Descrição |
|:--- |:--- |
| **sys.database_event_session_actions** |Retorna uma linha para cada ação em cada evento de uma sessão de eventos. |
| **sys.database_event_session_events** |Retorna uma linha para cada evento em uma sessão de eventos. |
| **sys.database_event_session_fields** |Retorna uma linha para cada coluna personalizável que foi explicitamente definida em eventos e destinos. |
| **sys.database_event_session_targets** |Retorna uma linha para cada destino de evento em uma sessão de eventos. |
| **sys.database_event_sessions** |Retorna uma linha para cada sessão de evento no banco de dados de banco de dados SQL hello. |

No Microsoft SQL Server, exibições do catálogo semelhantes têm nomes que incluem *.server\_* em vez de *.database\_*. é o padrão de nome Hello como **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>Novas exibições de gerenciamento dinâmico [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)

O Banco de Dados SQL do Azure tem [exibições de gerenciamento dinâmico (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) que dão suporte a eventos estendidos. DMVs mostram as sessões de evento *ativas* .

| Nome da DMV | Descrição |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Retorna informações sobre ações da sessão de eventos. |
| **sys.dm_xe_database_session_events** |Retorna informações sobre eventos da sessão. |
| **sys.dm_xe_database_session_object_columns** |Mostra os valores de configuração de saudação para objetos de sessão tooa associado. |
| **sys.dm_xe_database_session_targets** |Retorna informações sobre os destinos da sessão. |
| **sys.dm_xe_database_sessions** |Retorna uma linha para cada sessão de evento que é o banco de dados toohello no escopo atual. |

No Microsoft SQL Server, exibições de catálogo semelhantes são nomeadas sem Olá  *\_banco de dados* parte da saudação nome, como:

- **sys.dm_xe_sessions**, em vez de nome<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Tooboth comuns DMVs
Para eventos estendidos há DMVs adicionais que são comuns tooboth banco de dados do SQL Azure e o Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Localizar os eventos estendidos disponível hello, ações e destinos

Você pode executar um SQL simple **selecione** tooobtain uma lista de eventos disponíveis hello, ações e destino.

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


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Destinos para as sessões de evento do Banco de Dados SQL

Estes são os destinos que podem capturar resultados de suas sessões de evento no Banco de Dados SQL:

- [Destino de Buffer de Anéis](http://msdn.microsoft.com/library/ff878182.aspx) - armazena dados na memória por um curto período.
- [Destino de Contador de eventos](http://msdn.microsoft.com/library/ff878025.aspx) - conta todos os eventos que ocorrem durante uma sessão de eventos estendidos.
- [Destino de arquivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) -contêiner de armazenamento do Azure grava buffers completos tooan.

Olá [rastreamento de eventos para Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API não está disponível para eventos estendidos no banco de dados SQL.

## <a name="restrictions"></a>Restrições

Há algumas diferenças relacionadas à segurança, assumindo o ambiente de nuvem de saudação do banco de dados SQL:

- Eventos estendidos são fundamentados no modelo de isolamento de único locatário hello. Uma sessão de eventos em um banco de dados não pode acessar dados ou eventos de outro banco de dados.
- Não é possível emitir um **CREATE EVENT SESSION** instrução no contexto de saudação do hello **mestre** banco de dados.

## <a name="permission-model"></a>Modelo de permissão

Você deve ter **controle** permissão Olá banco de dados tooissue uma **CREATE EVENT SESSION** instrução. Olá proprietário de banco de dados (dbo) possui **controle** permissão.

### <a name="storage-container-authorizations"></a>Autorizações de contêiner de armazenamento

token SAS Olá gerar para seu contêiner de armazenamento do Azure deve especificar **rwl** para permissões de saudação. Olá **rwl** valor fornece Olá as seguintes permissões:

- Ler
- Gravar
- Listar

## <a name="performance-considerations"></a>Considerações sobre o desempenho

Existem cenários onde um uso intensivo de eventos estendidos pode ser acumuladas ativa mais memória do que íntegro para Olá geral do sistema. Portanto hello sistema de banco de dados SQL dinamicamente define e ajusta os limites de quantidade de saudação de memória ativa que pode ser acumulada por uma sessão de evento. Muitos fatores levam ao cálculo dinâmico Olá.

Se você receber uma mensagem de erro informando que há uma imposição de quantidade máxima de memória, estas são algumas das ações corretivas possíveis:

- Executar menos sessões simultâneas do evento.
- Por meio de seu **criar** e **ALTER** instruções para sessões de evento, reduzir a quantidade de saudação de memória que você especificar na Olá **MAX\_memória** cláusula.

### <a name="network-latency"></a>Latência da rede

Olá **arquivo de evento** destino pode experimentar latência de rede ou falhas durante a persistência tooAzure dados blobs de armazenamento. Outros eventos no banco de dados SQL podem ser atrasados enquanto esperam Olá toocomplete de comunicação de rede. Esse atraso pode retardar sua carga de trabalho.

- toomitigate esse desempenho de risco, evite definir Olá **EVENT_RETENTION_MODE** opção muito**NO_EVENT_LOSS** em suas definições de sessão de evento.

## <a name="related-links"></a>Links relacionados

- [Usando o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md).
- [Cmdlets do Armazenamento do Azure](http://msdn.microsoft.com/library/dn806401.aspx)
- [Usando o PowerShell do Azure com o armazenamento do Azure](../storage/common/storage-powershell-guide-full.md) -fornece informações abrangentes sobre o PowerShell e Olá serviço de armazenamento do Azure.
- [Como toouse armazenamento de BLOBs no .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [CREATE EVENT SESSION (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [Postagens do blog de Jonathan Kehayias sobre eventos estendidos no Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Hello Azure *atualizações de serviço* página da Web, com o parâmetro tooAzure banco de dados SQL:
    - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)


Outros tópicos de exemplo de código para eventos estendidos estão disponíveis em Olá links a seguir. No entanto, você deve verificar rotineiramente qualquer toosee de exemplo se o exemplo hello tem como alvo o Microsoft SQL Server em vez do banco de dados do SQL Azure. Em seguida, você pode decidir se alterações secundárias são exemplo hello de toorun necessários.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
