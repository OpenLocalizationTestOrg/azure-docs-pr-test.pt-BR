---
title: aaaSecure um banco de dados no Data Warehouse SQL | Microsoft Docs
description: "Dicas para proteger um banco de dados no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Proteger um banco de dados no SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Visão Geral da Segurança](sql-data-warehouse-overview-manage-security.md)
> * [Autenticação](sql-data-warehouse-authentication.md)
> * [Criptografia (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Criptografia (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

Este artigo explica os fundamentos de Olá de proteção de seu banco de dados do Azure SQL Data Warehouse. Especificamente, este artigo apresentará a você recursos para limitar acesso, proteger dados e monitorar atividades em um banco de dados.

## <a name="connection-security"></a>Segurança da conexão
Segurança de Conexão refere-se toohow restringir e proteger conexões tooyour banco de dados usando regras de firewall e de criptografia da conexão.

Regras de firewall são usadas por ambos os Olá Olá e servidor de banco de dados tooreject conexão tentativas de endereços IP que não foram explicitamente na lista de permissões. conexões tooallow de seu aplicativo ou o endereço IP público do computador cliente, primeiro você deve criar uma regra de firewall de nível de servidor usando Olá Portal do Azure, a API REST ou o PowerShell. Como prática recomendada, você deve restringir os intervalos de endereços IP de saudação permitidos através do firewall de servidor tanto quanto possíveis.  tooaccess Azure SQL Data Warehouse do computador local, certifique-se de firewall Olá na sua rede e o computador local permita a comunicação de saída na porta TCP 1433.  Para saber mais, confira [Firewall do Banco de Dados SQL do Azure][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Conexões tooyour SQL Data Warehouse são criptografados por padrão.  Criptografia modificando toodisable de configurações de conexão são ignorados.

## <a name="authentication"></a>Autenticação
Autenticação refere-se toohow provar sua identidade ao conectar-se o banco de dados toohello. Atualmente, o SQL Data Warehouse dá suporte à Autenticação do SQL Server com um nome de usuário e senha, bem como do Azure Active Directory. 

Quando você criou o servidor lógico Olá para seu banco de dados, você especificou um logon de "administrador do servidor" com um nome de usuário e senha. Usando essas credenciais, você pode autenticar tooany banco de dados no servidor como proprietário do banco de dados hello, ou "dbo" por meio da autenticação do SQL Server.

No entanto, como uma prática recomendada, os usuários da sua organização devem usar tooauthenticate uma conta diferente. Dessa forma, você pode limitar as permissões de saudação concedidas toohello aplicativo e reduzir os riscos de saudação de atividade mal-intencionada, caso o código do aplicativo é vulnerável tooa ataque de injeção de SQL. 

toocreate um usuário autenticado do SQL Server, conecte-se toohello **mestre** criar um novo logon de servidor e banco de dados em seu servidor com seu logon de administrador do servidor.  Além disso, é uma boa ideia toocreate um usuário no banco de dados mestre para usuários do Azure SQL Data Warehouse hello. Criando um usuário em mestre permite que um toologin de usuário usando ferramentas como o SSMS sem especificar um nome de banco de dados.  Ele também permite que toouse Olá objeto explorer tooview todos os bancos de dados em um SQL server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Em seguida, conecte-se tooyour **banco de dados do SQL Data Warehouse** com seu logon de administrador do servidor e criar um usuário de banco de dados com base no logon do servidor de saudação você acabou de criar.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Se um usuário estiver realizando operações adicionais, como criar logons ou criar novos bancos de dados, eles precisarão também toobe atribuído toohello `Loginmanager` e `dbmanager` funções no banco de dados mestre hello. Para obter mais informações sobre essas funções adicionais e autenticação tooa banco de dados SQL, consulte [Gerenciando bancos de dados e logons no banco de dados do SQL Azure][Managing databases and logins in Azure SQL Database].  Para obter mais detalhes sobre o AD do Azure SQL Data Warehouse, consulte [conexão tooSQL Data Warehouse por usando o Azure Active Directory Authentication][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Autorização
Autorização refere-se toowhat você pode fazer em um banco de dados do Azure SQL Data Warehouse, e isso é controlado por associações de função e permissões de sua conta de usuário. Como prática recomendada, você deve conceder Olá usuários privilégios mínimos necessários. SQL Data Warehouse do Azure torna esse toomanage fácil com as funções em T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

conta de administrador de servidor Olá que você está se conectando é membro de db_owner, que tem autoridade toodo nada no banco de dados de saudação. Salve essa conta para implantar atualizações de esquema e outras operações de gerenciamento. Usar conta de "ApplicationUser" hello com tooconnect mais limitado de permissões de banco de dados de toohello seu aplicativo com hello privilégios mínimos necessitados para seu aplicativo.

Há maneiras toofurther limite que um usuário pode fazer com o banco de dados do SQL Azure:

* Granular [permissões] [ Permissions] permitem que você controle quais operações você pode em colunas individuais, tabelas, exibições, procedimentos e outros objetos no banco de dados de saudação. Use permissões granulares toohave Olá maior controle e conceda Olá mínimo necessário de permissões. sistema de permissão granular Olá é um pouco complexo e exige alguns toouse estudo efetivamente.
* [Funções de banco de dados] [ Database roles] diferente de db_datareader e db_datawriter podem ser usado toocreate contas de usuário de aplicativo mais potentes ou contas menos avançadas de gerenciamento. funções de banco de dados fixa interno Olá fornecem uma maneira fácil de permissões toogrant, mas podem resultar em conceder mais permissões que são necessárias.
* [Procedimentos armazenados] [ Stored procedures] pode ser usado toolimit ações Olá que podem ser executadas no banco de dados de saudação.

Gerenciamento de bancos de dados e servidores lógicos da saudação Portal clássico do Azure ou usando Olá API do Gerenciador de recursos do Azure é controlado por atribuições de função da sua conta de usuário do portal. Para saber mais sobre esse tópico, confira [Controle de acesso baseado em função no Portal do Azure][Role-based access control in Azure Portal].

## <a name="encryption"></a>Criptografia
Azure SQL Data Warehouse de dados TDE (criptografia transparente) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia dos dados em repouso.  Quando você criptografar o banco de dados, backups associados e arquivos de log de transações são criptografados sem a necessidade de qualquer aplicativo de tooyour alterações. Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica. No banco de dados SQL a chave de criptografia de banco de dados de saudação é protegido por um certificado de servidor interno. certificado de saudação do servidor interno é exclusivo para cada servidor de banco de dados SQL. A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias. algoritmo de criptografia de saudação usado pelo SQL Data Warehouse é AES-256. Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption][Transparent Data Encryption].

Você pode criptografar o banco de dados usando Olá [Portal do Azure] [ Encryption with Portal] ou [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Próximas etapas
Para obter detalhes e exemplos sobre como conectar tooyour SQL Data Warehouse com diferentes protocolos, consulte [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
