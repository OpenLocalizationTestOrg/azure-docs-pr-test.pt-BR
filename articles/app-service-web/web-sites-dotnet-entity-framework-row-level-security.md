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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="8145f-103">Tutorial: Aplicativo Web com um banco de dados multilocatário usando o Entity Framework e a Segurança em Nível de Linha</span><span class="sxs-lookup"><span data-stu-id="8145f-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="8145f-104">Este tutorial mostra como toobuild um multilocatário web aplicativo com um "[banco de dados compartilhado, o esquema compartilhada](https://msdn.microsoft.com/library/aa479086.aspx)" modelo de aluguel, usando o Entity Framework e [segurança em nível de linha](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="8145f-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="8145f-105">Nesse modelo, um único banco de dados contém os dados para vários locatários e cada linha de cada tabela é associada a uma "ID de Locatário".</span><span class="sxs-lookup"><span data-stu-id="8145f-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="8145f-106">Segurança de nível de linha (RLS), um novo recurso para o banco de dados SQL Azure, é usado tooprevent locatários acessem dados de outras.</span><span class="sxs-lookup"><span data-stu-id="8145f-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="8145f-107">Isso requer apenas um único aplicativo de toohello pequena alteração.</span><span class="sxs-lookup"><span data-stu-id="8145f-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="8145f-108">Por centralizando Olá locatário lógica de acesso no banco de dados de saudação em si, o RLS simplifica o código do aplicativo hello e reduz o risco de saudação acidental de vazamento de dados entre locatários.</span><span class="sxs-lookup"><span data-stu-id="8145f-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="8145f-109">Vamos começar com um simples aplicativo de Contact Manager hello de [criar um aplicativo ASP.NET MVP com autenticação e o banco de dados SQL e implantar tooAzure do serviço de aplicativo](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8145f-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="8145f-110">Direito agora, aplicativo hello permite que todos os toosee de usuários (locatários) todos os contatos:</span><span class="sxs-lookup"><span data-stu-id="8145f-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="8145f-112">Com apenas algumas pequenas alterações, adicionaremos suporte para multilocação, para que os usuários toosee capaz apenas Olá os contatos que pertencem a toothem.</span><span class="sxs-lookup"><span data-stu-id="8145f-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="8145f-113">Etapa 1: Adicionar uma classe Interceptor no hello tooset de aplicativo hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="8145f-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="8145f-114">Há uma alteração de aplicativo, é preciso toomake.</span><span class="sxs-lookup"><span data-stu-id="8145f-114">There is one application change we need toomake.</span></span> <span data-ttu-id="8145f-115">Como conectarem todos os usuários do aplicativo Olá toohello banco de dados usando a mesma cadeia de caracteres de conexão (ou seja, mesmo logon SQL), atualmente, não há nenhuma maneira para um tooknow de política RLS usuário que ele deve filtrar.</span><span class="sxs-lookup"><span data-stu-id="8145f-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="8145f-116">Essa abordagem é muito comum em aplicativos da web porque ela permite que o pool de conexão eficiente, mas isso significa que precisamos de outra maneira tooidentify Olá usuário atual do aplicativo no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8145f-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="8145f-117">Olá solução é toohave Olá aplicativo conjunto um par chave-valor para Olá UserId atual no hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) imediatamente depois de abrir uma conexão, antes ele executa as consultas.</span><span class="sxs-lookup"><span data-stu-id="8145f-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="8145f-118">SESSION_CONTEXT é um repositório de chave-valor no escopo da sessão e nossa política RLS usará Olá UserId armazenada do usuário atual do tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="8145f-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="8145f-119">Vamos adicionar um [interceptador](https://msdn.microsoft.com/data/dn469464.aspx) (em particular, uma [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), um novo recurso no Entity Framework (EF) 6, tooautomatically conjunto Olá UserId atual no hello SESSION_CONTEXT executando um Instrução T-SQL sempre que o EF abre uma conexão.</span><span class="sxs-lookup"><span data-stu-id="8145f-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="8145f-120">Abra o projeto de ContactManager Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8145f-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="8145f-121">Com o botão direito na pasta de modelos de saudação do hello Gerenciador de soluções e escolha Adicionar > classe.</span><span class="sxs-lookup"><span data-stu-id="8145f-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="8145f-122">Nomeie a nova classe de hello "SessionContextInterceptor.cs" e clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="8145f-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="8145f-123">Substitua o conteúdo de saudação do SessionContextInterceptor.cs com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="8145f-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

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

<span data-ttu-id="8145f-124">Que é a alteração de aplicativo somente de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="8145f-124">That's hello only application change required.</span></span> <span data-ttu-id="8145f-125">Vá em frente e criar e publicar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8145f-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="8145f-126">Etapa 2: Adicionar um esquema de banco de dados de toohello de coluna de ID de usuário</span><span class="sxs-lookup"><span data-stu-id="8145f-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="8145f-127">Em seguida, precisamos tooadd uma UserId coluna toohello contatos tabela tooassociate cada linha com um usuário (Locatário).</span><span class="sxs-lookup"><span data-stu-id="8145f-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="8145f-128">Podemos irá alterar esquema Olá diretamente no banco de dados Olá, para que não temos tooinclude esse campo em nosso modelo de dados EF.</span><span class="sxs-lookup"><span data-stu-id="8145f-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="8145f-129">Conecte-se toohello banco de dados diretamente, usando o SQL Server Management Studio ou Visual Studio e, em seguida, executar Olá T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="8145f-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="8145f-130">Isso adiciona uma tabela de contatos de toohello de coluna de ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="8145f-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="8145f-131">Usamos Olá Olá nvarchar (128) dados tipo toomatch que UserIds armazenados na tabela de AspNetUsers hello e podemos criar uma restrição DEFAULT que definirá automaticamente hello UserId para linhas recém-inseridas toobe Olá UserId atualmente armazenado no SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="8145f-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="8145f-132">Agora a tabela de saudação é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="8145f-132">Now hello table looks like this:</span></span>

![Tabela Contatos do SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="8145f-134">Quando são criados novos contatos, automaticamente atribuídas Olá corrigir UserId.</span><span class="sxs-lookup"><span data-stu-id="8145f-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="8145f-135">Para fins de demonstração, no entanto, vamos atribuir alguns desses tooan contatos existentes existentes do usuário.</span><span class="sxs-lookup"><span data-stu-id="8145f-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="8145f-136">Se você criou alguns usuários no aplicativo hello já (por exemplo, usando o local, Google ou Facebook contas), você poderá vê-los na tabela de AspNetUsers hello.</span><span class="sxs-lookup"><span data-stu-id="8145f-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="8145f-137">Olá captura de tela abaixo, há apenas um usuário até o momento.</span><span class="sxs-lookup"><span data-stu-id="8145f-137">In hello screenshot below, there is only one user so far.</span></span>

![Tabela AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="8145f-139">Saudação de cópia Id para user1@contoso.come cole-o na instrução Olá T-SQL a seguir.</span><span class="sxs-lookup"><span data-stu-id="8145f-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="8145f-140">Execute essa instrução tooassociate três Olá contatos com esta ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="8145f-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="8145f-141">Etapa 3: Criar uma política de segurança de nível de linha no banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="8145f-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="8145f-142">Olá última etapa é toocreate uma política de segurança que usa Olá UserId SESSION_CONTEXT tooautomatically filtro Olá resultados retornados por consultas.</span><span class="sxs-lookup"><span data-stu-id="8145f-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="8145f-143">Ao banco de dados toohello ainda conectado, execute Olá T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="8145f-143">While still connected toohello database, execute hello following T-SQL:</span></span>

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

<span data-ttu-id="8145f-144">Esse código realiza três coisas.</span><span class="sxs-lookup"><span data-stu-id="8145f-144">This code does three things.</span></span> <span data-ttu-id="8145f-145">Primeiro, ele cria um novo esquema como uma prática recomendada para centralizar e limitando o acesso toohello RLS objetos.</span><span class="sxs-lookup"><span data-stu-id="8145f-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="8145f-146">Em seguida, ele cria uma função de predicado que retornará '1' quando Olá UserId de uma linha corresponde a saudação UserId no SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="8145f-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="8145f-147">Por fim, ele cria uma política de segurança que adicione essa função como um filtro e um bloco predicado na tabela de contatos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8145f-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="8145f-148">predicado de filtro Olá faz com que consultas tooreturn somente as linhas que pertencem o usuário atual toohello e predicado de block Olá atua como um aplicativo de saudação do tooprevent de proteção de nunca acidentalmente inserindo uma linha para o usuário errado Olá.</span><span class="sxs-lookup"><span data-stu-id="8145f-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="8145f-149">Agora execute o aplicativo hello e entre como user1@contoso.com. Agora, esse usuário vê apenas os contatos Olá atribuímos toothis UserId anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8145f-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="8145f-151">toovalidate isso ainda mais, tente registrar um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="8145f-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="8145f-152">Eles verão nenhum contatos, porque nenhum foram atribuídos toothem.</span><span class="sxs-lookup"><span data-stu-id="8145f-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="8145f-153">Se criar um novo contato, será atribuído toothem e só serão toosee capaz-lo.</span><span class="sxs-lookup"><span data-stu-id="8145f-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8145f-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8145f-154">Next steps</span></span>
<span data-ttu-id="8145f-155">É isso!</span><span class="sxs-lookup"><span data-stu-id="8145f-155">That's it!</span></span> <span data-ttu-id="8145f-156">aplicativo de web Hello simples entre em contato com o Gerenciador foi convertido em um multilocatário um em que cada usuário tem sua própria lista de contatos.</span><span class="sxs-lookup"><span data-stu-id="8145f-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="8145f-157">Usando a segurança em nível de linha, podemos terá evitado complexidade Olá de aplicar a lógica de acesso de locatário em nosso código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8145f-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="8145f-158">Essa transparência permite Olá aplicativo toofocus problema de negócios reais Olá em questão, e isso também reduz o risco de saudação de vazamento acidental de dados como aplicativo hello da Base de código cresce.</span><span class="sxs-lookup"><span data-stu-id="8145f-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="8145f-159">Este tutorial tem apenas a superfície Olá riscado do que é possível com a RLS.</span><span class="sxs-lookup"><span data-stu-id="8145f-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="8145f-160">Por exemplo, é possível toohave mais sofisticado ou lógica de acesso granular e é possível toostore mais do que apenas Olá UserId atual no hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="8145f-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="8145f-161">Também é possível muito[integrar RLS com bibliotecas de cliente de ferramentas de banco de dados Elástico Olá](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport fragmentos de vários locatários em uma camada de dados de expansão.</span><span class="sxs-lookup"><span data-stu-id="8145f-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="8145f-162">Além dessas possibilidades, também estamos trabalhando toomake RLS ainda melhor.</span><span class="sxs-lookup"><span data-stu-id="8145f-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="8145f-163">Se você tiver dúvidas, ideias ou coisas que você gostaria que toosee, informe-nos comentários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8145f-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="8145f-164">Agradecemos por seus comentários!</span><span class="sxs-lookup"><span data-stu-id="8145f-164">We appreciate your feedback!</span></span>

