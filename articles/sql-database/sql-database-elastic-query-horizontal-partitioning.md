---
title: "aaaReporting em bancos de dados de nuvem expansíveis | Microsoft Docs"
description: "como tooset Elástico consultas sobre partições horizontais"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Relatórios entre bancos de dados em nuvem expandidos (visualização)
![Consultar em fragmentos][1]

Bancos de dados fragmentados distribuem linhas em uma camada de dados expandida. esquema de saudação é idêntica em todos os bancos de dados participantes, também conhecidos como o particionamento horizontal. Usando uma consulta elástica, você pode criar relatórios que abrangem todos os bancos de dados em um banco de dados fragmentado.

Para um início rápido, confira [Relatórios entre bancos de dados em nuvem expandidos](sql-database-elastic-query-getting-started.md).

Para bancos de dados não fragmentados, consulte [Query across cloud databases with different schemas (Consulta entre bancos de dados na nuvem com esquemas diferentes)](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Crie um mapa do fragmento usando a biblioteca de cliente do banco de dados Elástico hello. Confira [Gerenciamento de mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md). Ou use o aplicativo de exemplo hello no [Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).
* Como alternativa, consulte [existente Migrar bancos de dados de bancos de dados de saída tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).
* usuário Olá deve ter a permissão ALTER ANY EXTERNAL DATA SOURCE. Essa permissão é incluída com a permissão ALTER DATABASE hello.
* Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.

## <a name="overview"></a>Visão geral
Essas instruções criam representação de metadados de saudação de sua camada de dados fragmentado no banco de dados de consulta Elástico hello. 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 Criar chave mestra do escopo do banco de dados e credenciais
Olá credencial é usada pelo Olá consulta Elástico tooconnect tooyour bancos de dados remotos.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Certifique-se de que Olá *"\<username\>"* não incluir nenhum *"@servername"* sufixo. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 Criar fontes de dados externas
Sintaxe:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Exemplo
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Recupere a lista de saudação de fontes de dados externas atual: 

    select * from sys.external_data_sources; 

fonte de dados externa Olá faz referência a seu mapa de fragmento. Uma consulta elástica usa fonte de dados externa hello e Olá subjacente fragmento mapa tooenumerate Olá bancos de dados que participam da camada de dados de saudação. Olá, mesmo credenciais são mapa do fragmento Olá tooread usado e tooaccess Olá dados em fragmentos Olá durante o processamento de saudação de uma consulta Elástico. 

## <a name="13-create-external-tables"></a>1.3 Criar tabelas externas
Sintaxe:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Exemplo**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Recupere a lista de saudação de tabelas externas do banco de dados atual hello: 

    SELECT * from sys.external_tables; 

tabelas externas toodrop:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Comentários
Olá dados\_cláusula de fonte define a fonte de dados externa da saudação (um mapa do fragmento) que é usado para a tabela externa hello.  

Olá esquema\_nome e o objeto\_cláusulas de nome mapeiam a tabela de tooa de definição de tabela externa de saudação em um esquema diferente. Se omitido, o esquema de saudação do objeto remoto Olá é considerada toobe "dbo" e seu nome é considerado o nome da tabela externa toobe toohello idênticos que está sendo definido. Isso é útil se Olá nome da tabela remota já existe no banco de dados de saudação onde deseja que a tabela externa do toocreate hello. Por exemplo, você deseja toodefine tooget uma tabela externa uma exibição agregada de exibições do catálogo ou DMVs em seus dados de expansão de camada. Como DMVs e modos de exibição de catálogo já existem localmente, você não pode usar seus nomes de definição de tabela externa hello. Em vez disso, use um nome diferente e usar da exibição de catálogo hello ou Olá nome DMVS no esquema de saudação\_nome e/ou objeto\_cláusulas de nome. (Consulte o exemplo hello abaixo). 

cláusula de distribuição de saudação especifica a distribuição de dados Olá usada para esta tabela. processador de consultas Olá utiliza informações Olá fornecidas Olá distribuição cláusula toobuild hello mais eficientes planos de consulta.  

1. **FRAGMENTADA** significa que dados são particionados horizontalmente em bancos de dados de saudação. Olá, chave de particionamento para distribuição de dados Olá Olá **< sharding_column_name >** parâmetro.
2. **REPLICADAS** significa que cópias idênticas de tabela Olá estão presentes em cada banco de dados. É o tooensure responsabilidade réplicas Olá são idênticas em bancos de dados de saudação.
3. **ROUND\_ROBIN** significa que essa tabela Olá é particionada horizontalmente usando um método de distribuição do aplicativo dependente. 

**Referência da camada de dados**: tabela externa de saudação DDL refere-se a fonte de dados externa tooan. fonte de dados externa Olá Especifica um mapa do fragmento que fornece tabela externa Olá Olá informações necessárias toolocate todos os bancos de dados de saudação em sua camada de dados. 

### <a name="security-considerations"></a>Considerações de segurança
Os usuários com a tabela externa do acesso toohello automaticamente acessar tabelas remotas subjacentes de toohello na credencial Olá especificado na definição de fonte de dados externa hello. Evite indesejada elevação de privilégios por meio de credencial Olá Olá externo de fonte de dados. Use GRANT ou REVOKE para uma tabela externa como se fosse uma tabela normal.  

Depois de definir a fonte de dados externa e as tabelas externas, agora você poderá usar o T-SQL completo nas tabelas externas.

## <a name="example-querying-horizontal-partitioned-databases"></a>Exemplo: consultando bancos de dados particionados horizontais
Olá consulta a seguir executa uma junção de três vias entre depósitos, pedidos e linhas de ordem e usa várias agregações e um filtro seletivo. Ele assume o particionamento horizontal (1) (fragmentação) e (2) que depósitos, pedidos e linhas de ordem são fragmentadas pela coluna de id de warehouse hello e consulta Elástico Olá pode posicionar Olá junções em fragmentos hello e processar parte caro Olá consulta Olá Olá fragmentos em paralelo. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Procedimento armazenado para a execução remota de T-SQL: sp\_execute_remote
Consulta elástica também apresenta um procedimento armazenado que fornece acesso direto toohello fragmentos. Olá procedimento armazenado é chamado [sp\_executar \_remoto](https://msdn.microsoft.com/library/mt703714) e pode ser usado tooexecute procedimentos armazenados ou código T-SQL em bancos de dados remotos hello. Ele usa Olá parâmetros a seguir: 

* Nome da fonte de dados (nvarchar): nome de saudação da fonte de dados externa de saudação do tipo RDBMS. 
* Consulta (nvarchar): toobe de consulta Olá T-SQL executado em cada fragmento. 
* Declaração de parâmetro (nvarchar) - opcional: cadeia de caracteres com definições de tipo de dados para parâmetros de saudação usadas no parâmetro de consulta de saudação (como sp_executesql). 
* Lista de valores de parâmetro - opcional: lista separada por vírgulas de valores de parâmetro (como sp_executesql).

Olá sp\_executar\_remota usa Olá fornecida na seguinte instrução T-SQL em bancos de dados remotos Olá Olá invocação parâmetros tooexecute Olá de fonte de dados externa. Ele usa credenciais Olá Olá dados externos fonte tooconnect toohello shardmap manager banco de dados e bancos de dados remotos hello.  

Exemplo: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Conectividade de ferramentas
Use tooconnect regular de cadeias de caracteres de conexão do SQL Server seu aplicativo, dados e BI integração ferramentas toohello banco de dados com suas definições de tabela externa. Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta. Em seguida, fazer referência Olá Elástico consultar banco de dados como qualquer outra ferramenta de toohello conectado de banco de dados do SQL Server e use tabelas externas de seu aplicativo ou uma ferramenta como se fossem tabelas locais. 

## <a name="best-practices"></a>Práticas recomendadas
* Certifique-se de que esse banco de dados do ponto de extremidade de consulta Elástico Olá tem o banco de dados do access toohello shardmap e todos os fragmentos por meio de saudação que firewalls de banco de dados SQL.  
* Validar ou impor a distribuição de dados Olá definida pela tabela externa hello. Se a distribuição de dados real é diferente de distribuição de saudação especificada na definição de tabela, as consultas podem produzir resultados inesperados. 
* Elástica consulta atualmente não executar eliminação de fragmento quando predicados de chave de fragmentação Olá permitiria que toosafely excluir determinados fragmentos do processamento.
* Consulta elástica funciona melhor para consultas onde a maioria de computação Olá pode ser feita em fragmentos hello. Você normalmente obtém melhor desempenho de consulta Olá com predicados de filtro seletivo que pode ser avaliada em fragmentos hello ou junções em Olá chaves que podem ser executadas de forma alinhado por partição em todos os fragmentos de particionamento. Outros padrões de consulta podem precisar de tooload grandes quantidades de dados do nó principal do toohello Olá fragmentos e podem executar mal

## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).
* Para obter um tutorial sobre particionamento vertical, veja [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)
* Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
