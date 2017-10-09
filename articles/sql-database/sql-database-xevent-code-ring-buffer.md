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
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a>Código de destino do Buffer de Anéis para eventos estendidos no Banco de Dados SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Desejado um exemplo de código completo para hello mais fácil maneira rápida toocapture e relatório de informações para um evento estendido durante um teste. destino de Hello mais fácil para os dados de evento estendido é hello [destino de Buffer de anel](http://msdn.microsoft.com/library/ff878182.aspx).

Este tópico apresenta um exemplo de código Transact-SQL que:

1. Cria uma tabela com dados toodemonstrate com.
2. Cria uma sessão para um evento estendido existente, ou seja, **sqlserver.sql_statement_starting**.
   
   * evento Hello é limitado tooSQL instruções que contêm uma determinada cadeia de caracteres de atualização: **instrução '% atualização tabEmployee %'**.
   * Escolhe a saída de hello toosend do hello evento tooa de destino de tipo de Buffer de anel, ou seja, **package0.ring_buffer**.
3. Inicia a sessão de evento hello.
4. Emite algumas instruções SQL UPDATE simples.
5. Emite uma SQL SELECT instrução tooretrieve evento saída de hello Buffer de anel.
   
   * **sys.dm_xe_database_session_targets** e outras exibições de gerenciamento dinâmico (DMVs) são ingressadas.
6. Interrompe a sessão de evento hello.
7. Descarta Olá destino de Buffer de anel, toorelease seus recursos.
8. Descarta Olá event session e tabela de demonstração de saudação.

## <a name="prerequisites"></a>Pré-requisitos

* Uma conta e uma assinatura do Azure. Você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Qualquer banco de dados no qual você possa criar uma tabela.
  
  * Como alternativa, você pode [criar um banco de dados de demonstração do **AdventureWorksLT**](sql-database-get-started.md) em questão minutos.
* O SQL Server Management Studio (ssms.exe), idealmente na sua versão de atualização mensal mais recente. 
  Você pode baixar Olá o ssms.exe mais recentes de:
  
  * Tópico [Baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Download de toohello um link direto.](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a>Exemplo de código

Com muito pequena modificação, hello seguinte exemplo de código do Buffer de anel pode ser executado no banco de dados SQL ou Microsoft SQL Server. diferença de saudação é a presença de saudação do nó de saudação banco de dados' no nome de saudação de alguns modos de exibição de gerenciamento dinâmico (DMVs), usada na cláusula FROM de saudação na etapa 5. Por exemplo:

* sys.dm_xe**_database**_session_targets
* sys.dm_xe_session_targets

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

## <a name="ring-buffer-contents"></a>Conteúdo do Buffer de Anéis

Usamos o exemplo de código ssms.exe toorun hello.

resultados de saudação tooview, clicar célula Olá sob o cabeçalho de coluna Olá **target_data_XML**.

Em seguida, no painel de resultados de saudação clicar célula Olá sob o cabeçalho de coluna Olá **target_data_XML**. Clique criado outra guia do arquivo em ssms.exe no qual Olá o conteúdo da célula de resultado Olá foi exibido, como XML.

Olá saída é mostrada no hello após bloco. Parece longo, mas são apenas dois elementos **<event>** .

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


#### <a name="release-resources-held-by-your-ring-buffer"></a>Liberar os recursos mantidos pelo seu Buffer de Anéis

Quando você concluir seu Buffer de anel, você pode removê-lo e liberar seus recursos emitir um **ALTER** Olá seguinte:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


definição de saudação da sua sessão de evento é atualizada, mas não removida. Posteriormente, você pode adicionar outra instância da sessão de evento de tooyour de Buffer de anel hello:

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a>Mais informações

saudação de tópico principal para eventos estendidos no banco de dados do SQL Azure é:

* [Considerações sobre eventos estendidos no Banco de Dados SQL](sql-database-xevent-db-diff-from-svr.md), que é diferente em alguns aspectos dos eventos estendidos que diferem entre o Banco de Dados SQL do Azure e o Microsoft SQL Server.

Outros tópicos de exemplo de código para eventos estendidos estão disponíveis em Olá links a seguir. No entanto, você deve verificar rotineiramente qualquer toosee de exemplo se o exemplo hello tem como alvo o Microsoft SQL Server em vez do banco de dados do SQL Azure. Em seguida, você pode decidir se alterações secundárias são exemplo hello de toorun necessários.

* Exemplo de código do Banco de Dados SQL do Azure: [código de destino do Arquivo de Evento para eventos estendidos no Banco de Dados SQL](sql-database-xevent-code-event-file.md)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
