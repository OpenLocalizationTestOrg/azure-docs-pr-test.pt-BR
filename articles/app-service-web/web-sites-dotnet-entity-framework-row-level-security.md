---
title: "Tutorial: Aplicativo Web com um banco de dados multilocatário usando o Entity Framework e a Segurança em Nível de Linha"
description: "Aprenda a desenvolver um aplicativo Web ASP.NET MVC 5 com um Banco de Dados SQL multilocatário backend, usando o Entity Framework e a Segurança em nível de linha."
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Tutorial: Aplicativo Web com um banco de dados multilocatário usando o Entity Framework e a Segurança em Nível de Linha
Este tutorial mostra como compilar um aplicativo Web multilocatário com um modelo de locatário "[banco de dados compartilhado, esquema compartilhado](https://msdn.microsoft.com/library/aa479086.aspx)", usando o Entity Framework e a [Segurança em Nível de Linha](https://msdn.microsoft.com/library/dn765131.aspx). Nesse modelo, um único banco de dados contém os dados para vários locatários e cada linha de cada tabela é associada a uma "ID de Locatário". O RLS (Segurança em nível de linha), um novo recurso do Banco de Dados SQL do Azure, é usado para impedir que locatários acessem os dados uns dos outros. Isso exige apenas uma pequena alteração no aplicativo. Ao centralizar a lógica de acesso do locatário no próprio banco de dados, o RLS simplifica o código do aplicativo e reduz o risco de perda acidental de dados entre locatários.

Vamos começar com o aplicativo simples Gerenciador de Contatos de [Criar um aplicativo MVP em ASP.NET com autenticação e o Banco de Dados SQL e implantar no Serviço de Aplicativo do Azure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Neste instante, o aplicativo permite que todos os usuários (locatários) vejam todos os contatos:

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Com apenas algumas pequenas alterações, adicionaremos o suporte para multilocatários, para que os usuários possam ver somente os contatos que pertencem a eles.

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a>Etapa 1: Adicionar uma classe Interceptor no aplicativo para definir o SESSION_CONTEXT
Há uma mudança de aplicativo necessária. Como todos os usuários do aplicativo se conectam ao banco de dados usando a mesma cadeia de conexão (ou seja, mesmo logon SQL), não há atualmente um modo para uma política de RLS saber para qual usuários deve filtrar. Essa abordagem é muito comum em aplicativos Web, pois permite que um pool eficiente de conexões, mas isso significa que precisamos de outra maneira de identificar o usuário atual do aplicativo no banco de dados. A solução é fazer com que o aplicativo defina um par chave-valor para a UserId atual no [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) imediatamente após abrir uma conexão, antes de executar qualquer consulta. SESSION_CONTEXT é um repositório de chave-valor no escopo da sessão, e nossa política de RLS usará o UserId armazenado para identificar o usuário atual.

Adicionaremos um [interceptador](https://msdn.microsoft.com/data/dn469464.aspx) (especificamente, um [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), um novo recurso no Entity Framework (EF) 6, para definir automaticamente a UserId atual no SESSION_CONTEXT executando uma instrução T-SQL sempre que o EF abrir uma conexão.

1. Abra o projeto ContactManager no Visual Studio.
2. Clique com o botão direito do mouse na pasta Modelos no Gerenciador de Soluções e escolha Adicionar > Classe.
3. Nomeie a nova classe "SessionContextInterceptor.cs" e clique em Adicionar.
4. Substitua o conteúdo do arquivo SessionContextInterceptor.cs pelo código a seguir:

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

Essa é a única alteração necessária no aplicativo. Vá em frente e compile e publique o aplicativo.

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a>Etapa 2: Adicionar uma coluna UserId ao esquema de banco de dados
Em seguida, precisamos adicionar uma coluna UserId à tabela Contatos para associar cada linha a um usuário (locatário). Alteraremos o esquema diretamente no banco de dados, para que não tenhamos que incluir esse campo em nosso modelo de dados do EF.

Conecte-se diretamente ao banco de dados, usando o SQL Server Management Studio ou o Visual Studio e, em seguida, execute o T-SQL a seguir:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Isso adiciona uma coluna UserId à tabela Contatos. Usamos o tipo de dados nvarchar (128) para corresponder as UserIds armazenadas na tabela AspNetUsers, e criamos uma restrição DEFAULT que definirá automaticamente a UserId para linhas recentemente inseridas como a UserId armazenada atualmente em SESSION_CONTEXT.

Agora, a tabela tem esta aparência:

![Tabela Contatos do SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Quando novos contatos forem criados, eles receberão automaticamente a UserId correta. Para fins de demonstração, no entanto, vamos atribuir alguns destes contatos existentes a um usuário existente.

Se você já tiver criado alguns usuários no aplicativo (por exemplo, usando contas locais, do Google ou do Facebook), os verá na tabela AspNetUsers. Na captura de tela abaixo, há apenas um usuário até o momento.

![Tabela AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Copie a ID para user1@contoso.com e cole-a na instrução T-SQL a seguir. Execute esta instrução para associar três Contatos a esta UserId.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a>Etapa 3: Criar uma política de Segurança em nível de linha no banco de dados
A etapa final é criar uma política de segurança que usa a UserId no SESSION_CONTEXT para filtrar automaticamente os resultados retornados pelas consultas.

Enquanto ainda está conectado ao banco de dados, execute a seguinte instrução T-SQL:

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

Esse código realiza três coisas. Primeiro, ele cria um novo esquema como uma prática recomendada para centralizar e limitar o acesso aos objetos de RLS. Em seguida, ele cria uma função de predicado que retornará “1” quando a UserId de uma linha corresponder à UserId em SESSION_CONTEXT. Por fim, ele cria uma política de segurança que adiciona essa função como um filtro e predicado de bloco na tabela Contatos. O predicado do filtro faz com que as consultas retornem somente as linhas que pertencem ao usuário atual, e o predicado de bloco atua como uma medida de segurança para impedir que o aplicativo insira nunca acidentalmente uma linha para o usuário errado.

Agora execute o aplicativo e entre como user1@contoso.com. Esse usuário agora vê somente os Contatos que atribuímos anteriormente a essa UserId:

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

Para uma validação extra, tente registrar um novo usuário. Ele não verá qualquer contato, pois nenhum foi atribuído a ele. Se esse usuário criar um novo contato, ele será atribuído ao usuário e apenas o usuário poderá vê-lo.

## <a name="next-steps"></a>Próximas etapas
É isso! O aplicativo Web simples Gerenciador de Contatos foi convertido em um multilocatário, no qual cada usuário tem sua própria lista de contatos. Ao usar a Segurança em nível de linha, evitamos a complexidade que é aplicar a lógica de acesso do locatário ao código de nosso aplicativo. Essa transparência permite que o aplicativo se concentre no verdadeiro problema, e também reduz o risco de vazamento acidental dos dados à medida que a base de código do aplicativo cresce.

Este tutorial forneceu apenas uma pequena amostra do que é possível fazer com RLS. Por exemplo, é possível ter mais uma lógico de acesso mais sofisticada ou granular, e é possível armazenar mais do que apenas a UserId atual no SESSION_CONTEXT. Também é possível [integrar o RLS com as bibliotecas de cliente das ferramentas de banco de dados elástico](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) a fim de oferecer suporte a fragmentos de multilocatários em uma camada de dados de expansão.

Além dessas possibilidades, também estamos trabalhando para melhorar ainda mais o RLS. Se você tiver alguma dúvida, ideias ou coisas que gostaria de ver, envie nos comentários. Agradecemos por seus comentários!

