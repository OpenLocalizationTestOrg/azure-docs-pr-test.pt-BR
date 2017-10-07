---
title: acesso de aaaGranting tooAzure banco de dados SQL | Microsoft Docs
description: Saiba mais sobre como conceder acesso tooMicrosoft banco de dados do SQL Azure.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Controle de acesso do Banco de Dados SQL do Azure
tooprovide segurança, o banco de dados SQL controla o acesso com regras de firewall limitando conectividade por endereço IP, os mecanismos de autenticação que requerem usuários tooprove sua identidade e mecanismos de autorização, limitando os usuários toospecific ações e dados. 

> [!IMPORTANT]
> Para obter uma visão geral dos recursos de segurança de banco de dados SQL hello, consulte [visão geral de segurança do SQL](sql-database-security-overview.md). Para obter um tutorial, consulte [Proteger o Banco de Dados SQL do Azure](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Firewall e regras de firewall
O Banco de Dados SQL do Microsoft Azure fornece um serviço de banco de dados relacional para o Azure e outros aplicativos baseados na Internet. toohelp proteger seus dados, firewalls impedir que todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão. firewall de saudação concede acesso toodatabases com base em Olá endereços IP de cada solicitação de origem. Para saber mais, veja [Visão geral de regras de firewall do Banco de Dados SQL](sql-database-firewall-configure.md)

Olá serviço de banco de dados SQL está disponível somente pela porta TCP 1433. tooaccess um banco de dados SQL do seu computador, verifique se o firewall do computador cliente permite a comunicação TCP de saída na porta TCP 1433. Se não for necessário a outros aplicativos, bloqueie as conexões de entrada na porta TCP 1433. 

Como parte do processo de conexão de hello, conexões de máquinas virtuais do Azure são tooa redirecionado a outro endereço IP e porta exclusiva para cada função de trabalho. número da porta Hello está no intervalo de saudação do too11999 11000. Para obter mais informações sobre portas TCP, consulte [Portas além da 1433 para o ADO.NET 4.5 e o Banco de Dados SQL 2](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Autenticação

O Banco de Dados SQL dá suporte a dois tipos de autenticação:

* **Autenticação do SQL**, que usa um nome de usuário e senha. Quando você criou o servidor lógico Olá para seu banco de dados, você especificou um logon de "administrador do servidor" com um nome de usuário e senha. Usando essas credenciais, você pode autenticar tooany banco de dados no servidor como proprietário do banco de dados hello, ou "dbo". 
* **Autenticação do Azure Active Directory**, que usa identidades gerenciadas pelo Azure Active Directory e que tem suporte para domínios gerenciados e integrados. Use autenticação do Active Directory (segurança integrada) [sempre que possível](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode). Se você quiser toouse autenticação do Active Directory do Azure, você deve criar outro administrador de servidor chamado hello "Administrador do AD do Azure", que é permitido grupos e usuários do AD do Azure tooadminister. Este administrador também pode executar todas as operações executadas por um administrador de servidor comum. Consulte [conexão tooSQL banco de dados, usando o Azure Active Directory Authentication](sql-database-aad-authentication.md) para obter uma explicação de como toocreate uma tooenable de administração do AD do Azure autenticação do Active Directory do Azure.

saudação de mecanismo de banco de dados fecha as conexões que permanecem ociosas por mais de 30 minutos. Olá conexão deve logon novamente antes de ser usada. Continuamente conexões ativas tooSQL banco de dados exigir autorização (executada pelo mecanismo de banco de dados de saudação) pelo menos a cada 10 horas. mecanismo de banco de dados de saudação tentativas de autorização usando a senha enviada originalmente hello e nenhuma entrada do usuário é necessária. Por motivos de desempenho, quando uma senha é redefinida no banco de dados SQL, conexão Olá não é ser reautenticado, mesmo se a conexão de saudação é redefinido devido a pooling de tooconnection. Isso é diferente do comportamento de saudação do SQL Server no local. Se Olá senha foi alterada desde que a conexão Olá inicialmente foi autorizado, conexão Olá deve ser terminada e uma nova conexão feita usando Olá nova senha. Um usuário com hello `KILL DATABASE CONNECTION` permissão explicitamente pode encerrar uma conexão tooSQL banco de dados usando Olá [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) comando.

Contas de usuário podem ser criadas no banco de dados mestre hello e podem ser concedidas permissões em todos os bancos de dados no servidor de saudação, ou eles podem ser criados no banco de dados de saudação em si (chamado usuários independentes). Para saber mais sobre a criação e o gerenciamento de logons, veja [Gerenciar logons](sql-database-manage-logins.md). portabilidade tooenhance e scalabilty, use a escalabilidade de tooenhance de usuários de banco de dados independente. Para saber mais sobre usuários independentes, veja [Usuários de bancos de dados independentes – tornando seu banco de dados portátil](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) e [Bancos de dados independentes](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

Como prática recomendada a seu aplicativo deve usar tooauthenticate uma conta dedicada – dessa forma, você pode limitar as permissões de saudação concedidas toohello aplicativo e reduzir os riscos de saudação de atividade mal-intencionada, caso o código do aplicativo é vulnerável tooa injeção de SQL ataque. Olá recomendado abordagem é toocreate uma [usuário de banco de dados independente](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), que permite que seu aplicativo tooauthenticate diretamente toohello banco de dados. 

## <a name="authorization"></a>Autorização

Autorização refere-se toowhat um usuário pode fazer em um banco de dados do SQL Azure, e isso é controlado pelo banco de dados da sua conta de usuário [associações de função](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) e [permissões no nível do objeto](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Como prática recomendada, você deve conceder Olá usuários privilégios mínimos necessários. conta de administrador de servidor Olá que você está se conectando é membro de db_owner, que tem autoridade toodo nada no banco de dados de saudação. Salve essa conta para implantar atualizações de esquema e outras operações de gerenciamento. Usar conta de "ApplicationUser" hello com tooconnect mais limitado de permissões de banco de dados de toohello seu aplicativo com hello privilégios mínimos necessitados para seu aplicativo. Para saber mais, veja [Gerenciar logons](sql-database-manage-logins.md).

Normalmente, somente os administradores precisam acessar toohello `master` banco de dados. Banco de dados de usuário do access rotina tooeach deve ser por meio de usuários de banco de dados independente não-administrador criados em cada banco de dados. Quando você usa usuários de banco de dados independente, não é necessário toocreate logons Olá `master` banco de dados. Para obter mais informações, consulte [Usuários do banco de dados independente - Tornando o banco de dados portátil](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

Você deve familiarizar com hello recursos que podem ser usado toolimit ou elevar as permissões a seguir:   
* [Representação](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) e [assinatura de módulo](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) pode ser usado toosecurely elevar as permissões temporariamente.
* [Segurança em nível de linha](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) pode ser usado para limitar quais linhas de um usuário pode acessar.
* [O mascaramento de dados](sql-database-dynamic-data-masking-get-started.md) pode ser usado toolimit exposição de dados confidenciais.
* [Procedimentos armazenados](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) pode ser usado toolimit ações Olá que podem ser executadas no banco de dados de saudação.

## <a name="next-steps"></a>Próximas etapas

- Para obter uma visão geral dos recursos de segurança de banco de dados SQL hello, consulte [visão geral de segurança do SQL](sql-database-security-overview.md).
- toolearn mais informações sobre regras de firewall, consulte [as regras de Firewall](sql-database-firewall-configure.md).
- toolearn sobre usuários e logons, consulte [gerenciar logons](sql-database-manage-logins.md). 
- Para obter uma discussão sobre monitoramento proativo, confira [Auditoria do Banco de Dados](sql-database-auditing.md) e [Detecção de Ameaças do Banco de Dados SQL](sql-database-threat-detection.md).
- Para obter um tutorial, consulte [Proteger o Banco de Dados SQL do Azure](sql-database-security-tutorial.md).
