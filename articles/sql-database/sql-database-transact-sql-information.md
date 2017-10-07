---
title: "banco de dados SQL do T-SQL Azure de migração de diferenças de aaaResolving | Microsoft Docs"
description: "Instruções Transact-SQL que têm suporte menor que o total pelo Banco de Dados SQL"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Resolvendo diferenças de Transact-SQL durante a migração tooSQL banco de dados   
Quando [migrar seu banco de dados](sql-database-cloud-migrate.md) de tooAzure do SQL Server do SQL Server, você pode descobrir que seu banco de dados exige algum engenharia novamente antes de saudação do SQL Server podem ser migrado. Este tópico fornece orientação tooassist você executar essa reformulação tanto Compreendendo Olá subjacente motivos por que Olá reformulação é necessário. incompatibilidades de toodetect, use Olá [Assistente de migração de dados (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Visão geral
Há suporte total, tanto no Microsoft SQL Server quanto no Banco de Dados SQL do Azure, para a maioria dos aplicativos e recursos Transact-SQL. Por exemplo, Olá componentes principais do SQL, como tipos de dados, operadores, cadeia de caracteres, aritmética, lógica e funções de cursor, idêntico funcionam no SQL Server e banco de dados SQL. No entanto, existem algumas diferenças de T-SQL em DDL (linguagem de definição de dados) e elementos DML (linguagem de manipulação de dados), resultando em instruções T-SQL e consultas que têm suporte apenas parcial (o que discutiremos posteriormente neste tópico).

Além disso, há alguns recursos e sintaxe que não é suportado em todos os porque o banco de dados do SQL Azure é projetado tooisolate recursos de dependências no banco de dados mestre hello e sistema de operacional de saudação. Assim, a maioria das atividades no nível do servidor são inapropriadas para o Banco de Dados SQL. As opções e instruções Transact-SQL não estão disponíveis se elas configuram opções no nível do servidor, componentes do sistema operacional ou se especificam a configuração do sistema de arquivos. Quando essas funcionalidades são necessárias, uma alternativa apropriada costuma estar disponível de alguma forma no Banco de Dados SQL ou em outro recurso ou serviço do Azure. 

Por exemplo, alta disponibilidade é criada no Azure, configurar o AlwaysOn não é necessário (embora você talvez queira tooconfigure replicação geográfica para recuperação mais rápida em caso de saudação de um desastre). Portanto, instruções T-SQL relacionadas tooavailability grupos não são suportados pelo banco de dados SQL e modos de exibição de gerenciamento dinâmico de Olá relacionados tooAlways em também não têm suporte.

Para obter uma lista dos recursos de saudação que têm suporte e sem suporte pelo banco de dados SQL, consulte [comparação de recursos de banco de dados do Azure SQL](sql-database-features.md). Olá lista nesta página complementa o tópico Diretrizes e recursos e se concentra nas instruções Transact-SQL.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Instruções de sintaxe Transact-SQL com diferenças parciais
instruções de DDL (linguagem de definição de dados) do Hello principais estão disponíveis, mas algumas instruções DDL têm o posicionamento de toodisk relacionados de extensões e recursos sem suporte. 

- As instruções CREATE e ALTER DATABASE têm mais de três dúzias de opções. instruções de saudação incluem o posicionamento de arquivos FILESTREAM e opções do service broker que se aplicam somente a tooSQL Server. Isso pode não importa se você criar bancos de dados antes de migrar, mas se você estiver migrando o código T-SQL que cria bancos de dados você deve comparar [CREATE DATABASE (banco de dados do SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) com a sintaxe de SQL Server Olá em [criar Banco de dados (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake-se de que todas as opções de saudação você usar são suportadas. Criar banco de dados para o banco de dados do SQL Azure também tem o objetivo de serviço e opções de escala elástica que se aplicam somente tooSQL banco de dados.
- instruções CREATE e ALTER TABLE de saudação tem opções de FileTable não podem ser usados no banco de dados SQL, porque não há suporte para FILESTREAM.
- Há suporte para instruções de logon CREATE e ALTER mas banco de dados SQL não oferece todas as opções de saudação. toomake que seu banco de dados mais portáteis, banco de dados SQL usando o incentiva continha os usuários de banco de dados em vez de logons, sempre que possível. Para obter mais informações, consulte [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) e [Controle e concessão de acesso de banco de dados](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>Sintaxe do Transact-SQL sem suporte no Banco de Dados SQL   
Além disso tooTransact SQL instruções relacionadas toohello sem suporte a recursos descritos na [comparação de recursos de banco de dados SQL](sql-database-features.md), Olá seguintes grupos de instruções e declarações, não há suporte. Dessa forma, se seu banco de dados toobe migrado é usando qualquer um dos seguinte Olá recursos, projetar novamente o T-SQL tooeliminate esses recursos de T-SQL e instruções.

- Agrupamento de objetos do sistema
- Relacionado à conexão: instruções de ponto de extremidade, `ORIGINAL_DB_NAME`. Banco de dados SQL não oferece suporte a autenticação do Windows, mas dá suporte à autenticação de Active Directory do Azure semelhante hello. Alguns tipos de autenticação exigem a versão mais recente de saudação do SSMS. Para obter mais informações, consulte [tooSQL conectando banco de dados ou o SQL Data Warehouse por usando o Azure Active Directory Authentication](sql-database-aad-authentication.md).
- Consultas cruzadas de banco de dados usando nomes de três ou quatro partes. (As consultas de bancos de dados somente leitura têm suporte por meio de [consulta de banco de dados elástico](sql-database-elastic-query-overview.md).)
- encadeamento de propriedades de bancos de dados, configuração `TRUSTWORTHY`
- `DATABASEPROPERTY` Em vez disso, use `DATABASEPROPERTYEX`.
- `EXECUTE AS LOGIN` Use “EXECUTE AS USER”.
- Há suporte para criptografia, exceto para o gerenciamento extensível de chaves
- Criação de eventos: eventos, notificações de eventos, notificações de consulta
- Posicionamento de arquivos: sintaxe relacionadas toodatabase posicionamento de arquivos, tamanho e arquivos de banco de dados que são gerenciados automaticamente pelo Microsoft Azure.
- Alta disponibilidade: sintaxe relacionadas toohigh disponibilidade, que é gerenciada por meio de sua conta do Microsoft Azure. Isso inclui a sintaxe de backup, restauração, do AlwaysOn, espelhamento de banco de dados, envio de logs e dos modos de recuperação.
- Leitor de log: sintaxe que dependa do leitor de log hello, que não está disponível no banco de dados SQL: enviar por Push de replicação, Change Data Capture. O Banco de Dados SQL pode ser um assinante de um artigo de replicação de push.
- Funções: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- Tabelas temporárias globais
- Hardware: As configurações do servidor relacionadas toohardware relacionados sintaxe:, como memória, threads de trabalho, afinidade de CPU, sinalizadores de rastreamento. Em vez disso, use níveis de serviço.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE` e nomes de quatro partes
- .NET Framework: integração CLR com o SQL Server
- Pesquisa semântica
- Credenciais do Servidor: em vez disso, use [credenciais no escopo do banco de dados](https://msdn.microsoft.com/library/mt270260.aspx).
- Itens no nível do servidor: funções do servidor, `IS_SRVROLEMEMBER`, `sys.login_token`. `GRANT`, `REVOKE` e `DENY` das permissões no nível do servidor não estão disponíveis, embora algumas delas sejam substituídas por permissões no nível do banco de dados. Algumas DMVs úteis no nível do servidor têm DMVs equivalentes no nível do banco de dados.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- Opções `sp_configure` e `RECONFIGURE`. Algumas opções estão disponíveis usando [ALTERAR CONFIGURAÇÃO DE ESCOPO DO BANCO DE DADOS](https://msdn.microsoft.com/library/mt629158.aspx).
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL Server Agent: Sintaxe depende de saudação do SQL Server Agent ou hello banco de dados MSDB: alertas, operadores, servidores de gerenciamento central. Em vez disso, use scripts, como o Azure PowerShell.
- Auditoria do SQL Server: (use auditoria de Banco de Dados SQL em vez disso).
- Rastreamento do SQL Server
- Sinalizadores de rastreamento: o sinalizador de rastreamento alguns itens foram movidos toocompatibility modos.
- Depuração de Transact-SQL
- Disparadores: no escopo do servidor ou gatilhos de logon
- `USE`instrução: toochange Olá contexto tooa outro banco de dados, você deve fazer um nova conexão toohello novo banco de dados.

## <a name="full-transact-sql-reference"></a>Referência completa do Transact-SQL
Para obter mais informações sobre gramática, uso e exemplos do Transact-SQL, veja [Referência do Transact-SQL (mecanismo de banco de dados)](https://msdn.microsoft.com/library/bb510741.aspx) nos Manuais Online do SQL Server. 

### <a name="about-hello-applies-to-tags"></a>Sobre as marcas "Aplica-se a" hello
Olá referência Transact-SQL inclui tópicos relacionados tooSQL Server versões 2008 toohello presente. Abaixo do título do tópico hello, há uma barra de ícones, plataformas listagem Olá de quatro do SQL Server e aplicabilidade indica. Por exemplo, grupos de disponibilidade foram introduzidos no SQL Server 2012. O [criar grupo de disponibilidade](https://msdn.microsoft.com/library/ff878399.aspx) tópico indica que a instrução de saudação se aplica a **SQL Server (começando com o 2012)**. Olá não se aplica tooSQL Server 2008, SQL Server 2008 R2, banco de dados do SQL Azure, Azure SQL Data Warehouse ou Parallel Data Warehouse.

Em alguns casos, o assunto geral de saudação do tópico pode ser usado em um produto, mas há pequenas diferenças entre os produtos. diferenças de saudação são indicadas na pontos médios tópico Olá conforme apropriado. Em alguns casos, o assunto geral de saudação do tópico pode ser usado em um produto, mas há pequenas diferenças entre os produtos. diferenças de saudação são indicadas na pontos médios tópico Olá conforme apropriado. Por exemplo, o tópico de CREATE TRIGGER hello está disponível no banco de dados SQL. Olá, mas **ALL SERVER** opção gatilhos de nível de servidor, indica que os gatilhos de nível de servidor não podem ser usados no banco de dados SQL. Use gatilhos de nível de banco de dados em vez disso.

## <a name="next-steps"></a>Próximas etapas

Para obter uma lista dos recursos de saudação que têm suporte e sem suporte pelo banco de dados SQL, consulte [comparação de recursos de banco de dados do Azure SQL](sql-database-features.md). Olá lista nesta página complementa o tópico Diretrizes e recursos e se concentra nas instruções Transact-SQL.

