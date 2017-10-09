---
title: aaaQuery em nuvem bancos de dados com esquemas diferentes | Microsoft Docs
description: "como tooset as consultas de bancos de dados em partições verticais"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Consultar entre bancos de dados na nuvem com esquemas diferentes (visualização)
![Consultar tabelas em bancos de dados diferentes][1]

Bancos de dados particionados verticalmente usam diferentes conjuntos de tabelas diferentes bancos de dados. Isso significa que esse esquema Olá é diferente em bancos de dados diferentes. Por exemplo, todas as tabelas de inventário estão em um banco de dados, enquanto todas as tabelas relacionadas à contabilidade estão em um segundo banco de dados. 

## <a name="prerequisites"></a>Pré-requisitos
* usuário Olá deve ter a permissão ALTER ANY EXTERNAL DATA SOURCE. Essa permissão é incluída com a permissão ALTER DATABASE hello.
* Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.

## <a name="overview"></a>Visão geral

> [!NOTE]
> Ao contrário de com o particionamento horizontal, essas instruções de DDL não dependem de definindo uma camada de dados com um mapa do fragmento pela biblioteca de cliente do banco de dados Elástico hello.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CRIAR UMA CREDENCIAL NO ESCOPO DO BANCO DE DADOS](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Criar chave mestra do escopo do banco de dados e credenciais
Olá credencial é usada pelo Olá consulta Elástico tooconnect tooyour bancos de dados remotos.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Certifique-se de que Olá `<username>` não incluir nenhum **"@servername"** sufixo. 
>

## <a name="create-external-data-sources"></a>Criar fontes de dados externas
Sintaxe:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> parâmetro de tipo Hello deve ser definido muito**RDBMS**. 
>

### <a name="example"></a>Exemplo
Olá, exemplo a seguir ilustra uso de saudação do hello instrução CREATE para fontes de dados externas. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

lista de saudação tooretrieve atual fontes de dados externas: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Tabelas externas
Sintaxe:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Exemplo
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

saudação de exemplo a seguir mostra como tooretrieve Olá lista de tabelas externas do banco de dados atual hello: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Comentários
Consulta elástica estende Olá tabela externa sintaxe toodefine externo tabelas existentes que usam fontes de dados externas do tipo RDBMS. Uma definição de tabela externa para o particionamento vertical abrange Olá aspectos a seguir: 

* **Esquema**: tabela externa de saudação DDL define um esquema que podem usar as consultas. esquema de saudação fornecida em sua definição de tabela externa deve toomatch esquema Olá tabelas Olá Olá banco de dados remoto onde os dados reais hello estão armazenados. 
* **Referência de banco de dados remoto**: tabela externa de saudação DDL refere-se a fonte de dados externa tooan. fonte de dados externa Olá Especifica o nome de servidor lógico hello e nome de banco de dados do banco de dados remoto Olá onde são armazenados dados de tabela real hello. 

Tabelas externas do hello sintaxe toocreate usando uma fonte de dados externa, conforme descrito na seção anterior Olá, é o seguinte: 

cláusula DATA_SOURCE Olá define a fonte de dados externa da saudação (ou seja, Olá banco de dados remoto em caso de particionamento vertical) que é usado para a tabela externa hello.  

cláusulas SCHEMA_NAME e OBJECT_NAME Olá fornecem Olá capacidade toomap Olá externo definição tooa tabela em um esquema diferente no banco de dados remoto hello, ou tooa tabela com um nome diferente, respectivamente. Isso é útil se você quiser toodefine uma exibição de catálogo tooa tabela externa ou DMV em seu banco de dados remoto - ou qualquer outra situação em que nome da tabela remota Olá já existe localmente.  

Olá instrução DDL a seguir descarta uma definição de tabela externa existente do catálogo local hello. Ele não afeta o banco de dados remoto hello. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Permissões para CREATE/DROP TABLE externo**: permissões ALTER ANY EXTERNAL DATA SOURCE são necessários para a tabela externa DDL que também é necessário toorefer toohello fonte de dados.  

## <a name="security-considerations"></a>Considerações de segurança
Os usuários com a tabela externa do acesso toohello automaticamente acessar tabelas remotas subjacentes de toohello na credencial Olá especificado na definição de fonte de dados externa hello. Você deve gerenciar cuidadosamente tabela externa do access toohello em ordem tooavoid maneira indesejada de elevação de privilégios por meio de credencial de saudação da fonte de dados externa hello. Regulares permissões do SQL podem ser usado tooGRANT ou tabela externa do REVOGAR acesso tooan como se fosse uma tabela normal.  

## <a name="example-querying-vertically-partitioned-databases"></a>Exemplo: consultando bancos de dados particionados verticalmente
Olá consulta a seguir executa uma junção de três vias entre duas tabelas locais Olá para pedidos e linhas de ordem e tabela remota Olá para clientes. Este é um exemplo de caso de uso de dados de referência de Olá para consulta Elástico: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


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
Você pode usar tooconnect regular de cadeias de caracteres de conexão do SQL Server seu toodatabases de ferramentas de integração de BI e os dados no servidor de banco de dados SQL Olá com consulta elástica habilitado e tabelas externas definidas. Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta. Em seguida, consulte banco de dados de consulta Elástico toohello e suas tabelas externas, assim como quaisquer outros dados do SQL Server se conectaria toowith sua ferramenta. 

## <a name="best-practices"></a>Práticas recomendadas
* Certifique-se de que esse banco de dados do ponto de extremidade de consulta Elástico Olá tem banco de dados do access toohello remoto por habilitar o acesso de serviços do Azure em sua configuração de firewall do banco de dados SQL. Também verifique se essa credencial Olá fornecido em dados externos Olá definição de fonte pode fazer logon no banco de dados remoto hello e tem a tabela remota do Olá Olá permissões tooaccess.  
* Consulta elástica funciona melhor para consultas onde a maioria de computação Olá pode ser feita em bancos de dados remotos hello. Você normalmente obtém o melhor desempenho de consulta Olá com predicados de filtro seletivo que pode ser avaliada em bancos de dados remotos hello ou junções que podem ser executadas completamente no banco de dados remoto hello. Outros padrões de consulta podem precisar de tooload grandes quantidades de dados do banco de dados remoto hello e podem executar baixo desempenho. 

## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral de consulta elástica, veja [Visão geral de consulta elástica](sql-database-elastic-query-overview.md).
* Para obter um tutorial sobre particionamento vertical, consulte [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).
* Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
