---
title: "aaaXEvent código de Buffer de anel para o banco de dados SQL | Microsoft Docs"
description: "Fornece um exemplo de código Transact-SQL que é feito fácil e rápido pelo uso do destino de Buffer de anel hello, no banco de dados do SQL Azure."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="5654d-103">Código de destino do Buffer de Anéis para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="5654d-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="5654d-104">Desejado um exemplo de código completo para hello mais fácil maneira rápida toocapture e relatório de informações para um evento estendido durante um teste.</span><span class="sxs-lookup"><span data-stu-id="5654d-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="5654d-105">destino de Hello mais fácil para os dados de evento estendido é hello [destino de Buffer de anel](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="5654d-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="5654d-106">Este tópico apresenta um exemplo de código Transact-SQL que:</span><span class="sxs-lookup"><span data-stu-id="5654d-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="5654d-107">Cria uma tabela com dados toodemonstrate com.</span><span class="sxs-lookup"><span data-stu-id="5654d-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="5654d-108">Cria uma sessão para um evento estendido existente, ou seja, **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="5654d-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="5654d-109">evento Hello é limitado tooSQL instruções que contêm uma determinada cadeia de caracteres de atualização: **instrução '% atualização tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="5654d-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="5654d-110">Escolhe a saída de hello toosend do hello evento tooa de destino de tipo de Buffer de anel, ou seja, **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="5654d-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="5654d-111">Inicia a sessão de evento hello.</span><span class="sxs-lookup"><span data-stu-id="5654d-111">Starts hello event session.</span></span>
4. <span data-ttu-id="5654d-112">Emite algumas instruções SQL UPDATE simples.</span><span class="sxs-lookup"><span data-stu-id="5654d-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="5654d-113">Emite uma SQL SELECT instrução tooretrieve evento saída de hello Buffer de anel.</span><span class="sxs-lookup"><span data-stu-id="5654d-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="5654d-114">**sys.dm_xe_database_session_targets** e outras exibições de gerenciamento dinâmico (DMVs) são ingressadas.</span><span class="sxs-lookup"><span data-stu-id="5654d-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="5654d-115">Interrompe a sessão de evento hello.</span><span class="sxs-lookup"><span data-stu-id="5654d-115">Stops hello event session.</span></span>
7. <span data-ttu-id="5654d-116">Descarta Olá destino de Buffer de anel, toorelease seus recursos.</span><span class="sxs-lookup"><span data-stu-id="5654d-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="5654d-117">Descarta Olá event session e tabela de demonstração de saudação.</span><span class="sxs-lookup"><span data-stu-id="5654d-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5654d-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5654d-118">Prerequisites</span></span>

* <span data-ttu-id="5654d-119">Uma conta e uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5654d-119">An Azure account and subscription.</span></span> <span data-ttu-id="5654d-120">Você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5654d-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5654d-121">Qualquer banco de dados no qual você possa criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="5654d-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="5654d-122">Como alternativa, você pode [criar um banco de dados de demonstração do **AdventureWorksLT**](sql-database-get-started.md) em questão minutos.</span><span class="sxs-lookup"><span data-stu-id="5654d-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="5654d-123">O SQL Server Management Studio (ssms.exe), idealmente na sua versão de atualização mensal mais recente.</span><span class="sxs-lookup"><span data-stu-id="5654d-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="5654d-124">Você pode baixar Olá o ssms.exe mais recentes de:</span><span class="sxs-lookup"><span data-stu-id="5654d-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="5654d-125">Tópico [Baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="5654d-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="5654d-126">Download de toohello um link direto.</span><span class="sxs-lookup"><span data-stu-id="5654d-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="5654d-127">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="5654d-127">Code sample</span></span>

<span data-ttu-id="5654d-128">Com muito pequena modificação, hello seguinte exemplo de código do Buffer de anel pode ser executado no banco de dados SQL ou Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5654d-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="5654d-129">diferença de saudação é a presença de saudação do nó de saudação banco de dados' no nome de saudação de alguns modos de exibição de gerenciamento dinâmico (DMVs), usada na cláusula FROM de saudação na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="5654d-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="5654d-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5654d-130">For example:</span></span>

* <span data-ttu-id="5654d-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="5654d-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="5654d-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="5654d-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="5654d-133">Conteúdo do Buffer de Anéis</span><span class="sxs-lookup"><span data-stu-id="5654d-133">Ring Buffer contents</span></span>

<span data-ttu-id="5654d-134">Usamos o exemplo de código ssms.exe toorun hello.</span><span class="sxs-lookup"><span data-stu-id="5654d-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="5654d-135">resultados de saudação tooview, clicar célula Olá sob o cabeçalho de coluna Olá **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="5654d-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="5654d-136">Em seguida, no painel de resultados de saudação clicar célula Olá sob o cabeçalho de coluna Olá **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="5654d-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="5654d-137">Clique criado outra guia do arquivo em ssms.exe no qual Olá o conteúdo da célula de resultado Olá foi exibido, como XML.</span><span class="sxs-lookup"><span data-stu-id="5654d-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="5654d-138">Olá saída é mostrada no hello após bloco.</span><span class="sxs-lookup"><span data-stu-id="5654d-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="5654d-139">Parece longo, mas são apenas dois elementos **<event>** .</span><span class="sxs-lookup"><span data-stu-id="5654d-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="5654d-140">Liberar os recursos mantidos pelo seu Buffer de Anéis</span><span class="sxs-lookup"><span data-stu-id="5654d-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="5654d-141">Quando você concluir seu Buffer de anel, você pode removê-lo e liberar seus recursos emitir um **ALTER** Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="5654d-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="5654d-142">definição de saudação da sua sessão de evento é atualizada, mas não removida.</span><span class="sxs-lookup"><span data-stu-id="5654d-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="5654d-143">Posteriormente, você pode adicionar outra instância da sessão de evento de tooyour de Buffer de anel hello:</span><span class="sxs-lookup"><span data-stu-id="5654d-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="5654d-144">Mais informações</span><span class="sxs-lookup"><span data-stu-id="5654d-144">More information</span></span>

<span data-ttu-id="5654d-145">saudação de tópico principal para eventos estendidos no banco de dados do SQL Azure é:</span><span class="sxs-lookup"><span data-stu-id="5654d-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="5654d-146">[Considerações sobre eventos estendidos no Banco de Dados SQL](sql-database-xevent-db-diff-from-svr.md), que é diferente em alguns aspectos dos eventos estendidos que diferem entre o Banco de Dados SQL do Azure e o Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5654d-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="5654d-147">Outros tópicos de exemplo de código para eventos estendidos estão disponíveis em Olá links a seguir.</span><span class="sxs-lookup"><span data-stu-id="5654d-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="5654d-148">No entanto, você deve verificar rotineiramente qualquer toosee de exemplo se o exemplo hello tem como alvo o Microsoft SQL Server em vez do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5654d-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="5654d-149">Em seguida, você pode decidir se alterações secundárias são exemplo hello de toorun necessários.</span><span class="sxs-lookup"><span data-stu-id="5654d-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="5654d-150">Exemplo de código do Banco de Dados SQL do Azure: [código de destino do Arquivo de Evento para eventos estendidos no Banco de Dados SQL](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="5654d-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
