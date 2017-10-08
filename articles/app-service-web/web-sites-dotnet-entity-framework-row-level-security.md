---
title: "Tutorial: Aplicativo Web com um banco de dados multilocatário usando o Entity Framework e a Segurança em Nível de Linha"
description: "Saiba como toodevelop um ASP.NET MVC 5 web aplicativo com um banco de dados SQL backent, usando o Entity Framework e segurança em nível de linha de vários locatários."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Tutorial: Aplicativo Web com um banco de dados multilocatário usando o Entity Framework e a Segurança em Nível de Linha
Este tutorial mostra como toobuild um multilocatário web aplicativo com um "[banco de dados compartilhado, o esquema compartilhada](https://msdn.microsoft.com/library/aa479086.aspx)" modelo de aluguel, usando o Entity Framework e [segurança em nível de linha](https://msdn.microsoft.com/library/dn765131.aspx). Nesse modelo, um único banco de dados contém os dados para vários locatários e cada linha de cada tabela é associada a uma "ID de Locatário". Segurança de nível de linha (RLS), um novo recurso para o banco de dados SQL Azure, é usado tooprevent locatários acessem dados de outras. Isso requer apenas um único aplicativo de toohello pequena alteração. Por centralizando Olá locatário lógica de acesso no banco de dados de saudação em si, o RLS simplifica o código do aplicativo hello e reduz o risco de saudação acidental de vazamento de dados entre locatários.

Vamos começar com um simples aplicativo de Contact Manager hello de [criar um aplicativo ASP.NET MVP com autenticação e o banco de dados SQL e implantar tooAzure do serviço de aplicativo](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Direito agora, aplicativo hello permite que todos os toosee de usuários (locatários) todos os contatos:

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Com apenas algumas pequenas alterações, adicionaremos suporte para multilocação, para que os usuários toosee capaz apenas Olá os contatos que pertencem a toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Etapa 1: Adicionar uma classe Interceptor no hello tooset de aplicativo hello SESSION_CONTEXT
Há uma alteração de aplicativo, é preciso toomake. Como conectarem todos os usuários do aplicativo Olá toohello banco de dados usando a mesma cadeia de caracteres de conexão (ou seja, mesmo logon SQL), atualmente, não há nenhuma maneira para um tooknow de política RLS usuário que ele deve filtrar. Essa abordagem é muito comum em aplicativos da web porque ela permite que o pool de conexão eficiente, mas isso significa que precisamos de outra maneira tooidentify Olá usuário atual do aplicativo no banco de dados de saudação. Olá solução é toohave Olá aplicativo conjunto um par chave-valor para Olá UserId atual no hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) imediatamente depois de abrir uma conexão, antes ele executa as consultas. SESSION_CONTEXT é um repositório de chave-valor no escopo da sessão e nossa política RLS usará Olá UserId armazenada do usuário atual do tooidentify hello.

Vamos adicionar um [interceptador](https://msdn.microsoft.com/data/dn469464.aspx) (em particular, uma [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), um novo recurso no Entity Framework (EF) 6, tooautomatically conjunto Olá UserId atual no hello SESSION_CONTEXT executando um Instrução T-SQL sempre que o EF abre uma conexão.

1. Abra o projeto de ContactManager Olá no Visual Studio.
2. Com o botão direito na pasta de modelos de saudação do hello Gerenciador de soluções e escolha Adicionar > classe.
3. Nomeie a nova classe de hello "SessionContextInterceptor.cs" e clique em Adicionar.
4. Substitua o conteúdo de saudação do SessionContextInterceptor.cs com hello código a seguir.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

Que é a alteração de aplicativo somente de saudação necessária. Vá em frente e criar e publicar o aplicativo hello.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Etapa 2: Adicionar um esquema de banco de dados de toohello de coluna de ID de usuário
Em seguida, precisamos tooadd uma UserId coluna toohello contatos tabela tooassociate cada linha com um usuário (Locatário). Podemos irá alterar esquema Olá diretamente no banco de dados Olá, para que não temos tooinclude esse campo em nosso modelo de dados EF.

Conecte-se toohello banco de dados diretamente, usando o SQL Server Management Studio ou Visual Studio e, em seguida, executar Olá T-SQL a seguir:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Isso adiciona uma tabela de contatos de toohello de coluna de ID de usuário. Usamos Olá Olá nvarchar (128) dados tipo toomatch que UserIds armazenados na tabela de AspNetUsers hello e podemos criar uma restrição DEFAULT que definirá automaticamente hello UserId para linhas recém-inseridas toobe Olá UserId atualmente armazenado no SESSION_CONTEXT.

Agora a tabela de saudação é semelhante a:

![Tabela Contatos do SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Quando são criados novos contatos, automaticamente atribuídas Olá corrigir UserId. Para fins de demonstração, no entanto, vamos atribuir alguns desses tooan contatos existentes existentes do usuário.

Se você criou alguns usuários no aplicativo hello já (por exemplo, usando o local, Google ou Facebook contas), você poderá vê-los na tabela de AspNetUsers hello. Olá captura de tela abaixo, há apenas um usuário até o momento.

![Tabela AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Saudação de cópia Id para user1@contoso.come cole-o na instrução Olá T-SQL a seguir. Execute essa instrução tooassociate três Olá contatos com esta ID de usuário.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Etapa 3: Criar uma política de segurança de nível de linha no banco de dados de saudação
Olá última etapa é toocreate uma política de segurança que usa Olá UserId SESSION_CONTEXT tooautomatically filtro Olá resultados retornados por consultas.

Ao banco de dados toohello ainda conectado, execute Olá T-SQL a seguir:

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

Esse código realiza três coisas. Primeiro, ele cria um novo esquema como uma prática recomendada para centralizar e limitando o acesso toohello RLS objetos. Em seguida, ele cria uma função de predicado que retornará '1' quando Olá UserId de uma linha corresponde a saudação UserId no SESSION_CONTEXT. Por fim, ele cria uma política de segurança que adicione essa função como um filtro e um bloco predicado na tabela de contatos de saudação. predicado de filtro Olá faz com que consultas tooreturn somente as linhas que pertencem o usuário atual toohello e predicado de block Olá atua como um aplicativo de saudação do tooprevent de proteção de nunca acidentalmente inserindo uma linha para o usuário errado Olá.

Agora execute o aplicativo hello e entre como user1@contoso.com. Agora, esse usuário vê apenas os contatos Olá atribuímos toothis UserId anteriormente:

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate isso ainda mais, tente registrar um novo usuário. Eles verão nenhum contatos, porque nenhum foram atribuídos toothem. Se criar um novo contato, será atribuído toothem e só serão toosee capaz-lo.

## <a name="next-steps"></a>Próximas etapas
É isso! aplicativo de web Hello simples entre em contato com o Gerenciador foi convertido em um multilocatário um em que cada usuário tem sua própria lista de contatos. Usando a segurança em nível de linha, podemos terá evitado complexidade Olá de aplicar a lógica de acesso de locatário em nosso código do aplicativo. Essa transparência permite Olá aplicativo toofocus problema de negócios reais Olá em questão, e isso também reduz o risco de saudação de vazamento acidental de dados como aplicativo hello da Base de código cresce.

Este tutorial tem apenas a superfície Olá riscado do que é possível com a RLS. Por exemplo, é possível toohave mais sofisticado ou lógica de acesso granular e é possível toostore mais do que apenas Olá UserId atual no hello SESSION_CONTEXT. Também é possível muito[integrar RLS com bibliotecas de cliente de ferramentas de banco de dados Elástico Olá](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport fragmentos de vários locatários em uma camada de dados de expansão.

Além dessas possibilidades, também estamos trabalhando toomake RLS ainda melhor. Se você tiver dúvidas, ideias ou coisas que você gostaria que toosee, informe-nos comentários de saudação. Agradecemos por seus comentários!

