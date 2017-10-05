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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="da6e1-103">Tutorial: Aplicativo Web com um banco de dados multilocatário usando o Entity Framework e a Segurança em Nível de Linha</span><span class="sxs-lookup"><span data-stu-id="da6e1-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="da6e1-104">Este tutorial mostra como compilar um aplicativo Web multilocatário com um modelo de locatário "[banco de dados compartilhado, esquema compartilhado](https://msdn.microsoft.com/library/aa479086.aspx)", usando o Entity Framework e a [Segurança em Nível de Linha](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="da6e1-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="da6e1-105">Nesse modelo, um único banco de dados contém os dados para vários locatários e cada linha de cada tabela é associada a uma "ID de Locatário".</span><span class="sxs-lookup"><span data-stu-id="da6e1-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="da6e1-106">O RLS (Segurança em nível de linha), um novo recurso do Banco de Dados SQL do Azure, é usado para impedir que locatários acessem os dados uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="da6e1-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="da6e1-107">Isso exige apenas uma pequena alteração no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da6e1-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="da6e1-108">Ao centralizar a lógica de acesso do locatário no próprio banco de dados, o RLS simplifica o código do aplicativo e reduz o risco de perda acidental de dados entre locatários.</span><span class="sxs-lookup"><span data-stu-id="da6e1-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="da6e1-109">Vamos começar com o aplicativo simples Gerenciador de Contatos de [Criar um aplicativo MVP em ASP.NET com autenticação e o Banco de Dados SQL e implantar no Serviço de Aplicativo do Azure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="da6e1-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="da6e1-110">Neste instante, o aplicativo permite que todos os usuários (locatários) vejam todos os contatos:</span><span class="sxs-lookup"><span data-stu-id="da6e1-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="da6e1-112">Com apenas algumas pequenas alterações, adicionaremos o suporte para multilocatários, para que os usuários possam ver somente os contatos que pertencem a eles.</span><span class="sxs-lookup"><span data-stu-id="da6e1-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="da6e1-113">Etapa 1: Adicionar uma classe Interceptor no aplicativo para definir o SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="da6e1-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="da6e1-114">Há uma mudança de aplicativo necessária.</span><span class="sxs-lookup"><span data-stu-id="da6e1-114">There is one application change we need to make.</span></span> <span data-ttu-id="da6e1-115">Como todos os usuários do aplicativo se conectam ao banco de dados usando a mesma cadeia de conexão (ou seja, mesmo logon SQL), não há atualmente um modo para uma política de RLS saber para qual usuários deve filtrar.</span><span class="sxs-lookup"><span data-stu-id="da6e1-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="da6e1-116">Essa abordagem é muito comum em aplicativos Web, pois permite que um pool eficiente de conexões, mas isso significa que precisamos de outra maneira de identificar o usuário atual do aplicativo no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="da6e1-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="da6e1-117">A solução é fazer com que o aplicativo defina um par chave-valor para a UserId atual no [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) imediatamente após abrir uma conexão, antes de executar qualquer consulta.</span><span class="sxs-lookup"><span data-stu-id="da6e1-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="da6e1-118">SESSION_CONTEXT é um repositório de chave-valor no escopo da sessão, e nossa política de RLS usará o UserId armazenado para identificar o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="da6e1-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="da6e1-119">Adicionaremos um [interceptador](https://msdn.microsoft.com/data/dn469464.aspx) (especificamente, um [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), um novo recurso no Entity Framework (EF) 6, para definir automaticamente a UserId atual no SESSION_CONTEXT executando uma instrução T-SQL sempre que o EF abrir uma conexão.</span><span class="sxs-lookup"><span data-stu-id="da6e1-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="da6e1-120">Abra o projeto ContactManager no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da6e1-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="da6e1-121">Clique com o botão direito do mouse na pasta Modelos no Gerenciador de Soluções e escolha Adicionar > Classe.</span><span class="sxs-lookup"><span data-stu-id="da6e1-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="da6e1-122">Nomeie a nova classe "SessionContextInterceptor.cs" e clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="da6e1-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="da6e1-123">Substitua o conteúdo do arquivo SessionContextInterceptor.cs pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="da6e1-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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

<span data-ttu-id="da6e1-124">Essa é a única alteração necessária no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da6e1-124">That's the only application change required.</span></span> <span data-ttu-id="da6e1-125">Vá em frente e compile e publique o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da6e1-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="da6e1-126">Etapa 2: Adicionar uma coluna UserId ao esquema de banco de dados</span><span class="sxs-lookup"><span data-stu-id="da6e1-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="da6e1-127">Em seguida, precisamos adicionar uma coluna UserId à tabela Contatos para associar cada linha a um usuário (locatário).</span><span class="sxs-lookup"><span data-stu-id="da6e1-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="da6e1-128">Alteraremos o esquema diretamente no banco de dados, para que não tenhamos que incluir esse campo em nosso modelo de dados do EF.</span><span class="sxs-lookup"><span data-stu-id="da6e1-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="da6e1-129">Conecte-se diretamente ao banco de dados, usando o SQL Server Management Studio ou o Visual Studio e, em seguida, execute o T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="da6e1-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="da6e1-130">Isso adiciona uma coluna UserId à tabela Contatos.</span><span class="sxs-lookup"><span data-stu-id="da6e1-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="da6e1-131">Usamos o tipo de dados nvarchar (128) para corresponder as UserIds armazenadas na tabela AspNetUsers, e criamos uma restrição DEFAULT que definirá automaticamente a UserId para linhas recentemente inseridas como a UserId armazenada atualmente em SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="da6e1-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="da6e1-132">Agora, a tabela tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="da6e1-132">Now the table looks like this:</span></span>

![Tabela Contatos do SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="da6e1-134">Quando novos contatos forem criados, eles receberão automaticamente a UserId correta.</span><span class="sxs-lookup"><span data-stu-id="da6e1-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="da6e1-135">Para fins de demonstração, no entanto, vamos atribuir alguns destes contatos existentes a um usuário existente.</span><span class="sxs-lookup"><span data-stu-id="da6e1-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="da6e1-136">Se você já tiver criado alguns usuários no aplicativo (por exemplo, usando contas locais, do Google ou do Facebook), os verá na tabela AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="da6e1-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="da6e1-137">Na captura de tela abaixo, há apenas um usuário até o momento.</span><span class="sxs-lookup"><span data-stu-id="da6e1-137">In the screenshot below, there is only one user so far.</span></span>

![Tabela AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="da6e1-139">Copie a ID para user1@contoso.com e cole-a na instrução T-SQL a seguir.</span><span class="sxs-lookup"><span data-stu-id="da6e1-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="da6e1-140">Execute esta instrução para associar três Contatos a esta UserId.</span><span class="sxs-lookup"><span data-stu-id="da6e1-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="da6e1-141">Etapa 3: Criar uma política de Segurança em nível de linha no banco de dados</span><span class="sxs-lookup"><span data-stu-id="da6e1-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="da6e1-142">A etapa final é criar uma política de segurança que usa a UserId no SESSION_CONTEXT para filtrar automaticamente os resultados retornados pelas consultas.</span><span class="sxs-lookup"><span data-stu-id="da6e1-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="da6e1-143">Enquanto ainda está conectado ao banco de dados, execute a seguinte instrução T-SQL:</span><span class="sxs-lookup"><span data-stu-id="da6e1-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="da6e1-144">Esse código realiza três coisas.</span><span class="sxs-lookup"><span data-stu-id="da6e1-144">This code does three things.</span></span> <span data-ttu-id="da6e1-145">Primeiro, ele cria um novo esquema como uma prática recomendada para centralizar e limitar o acesso aos objetos de RLS.</span><span class="sxs-lookup"><span data-stu-id="da6e1-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="da6e1-146">Em seguida, ele cria uma função de predicado que retornará “1” quando a UserId de uma linha corresponder à UserId em SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="da6e1-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="da6e1-147">Por fim, ele cria uma política de segurança que adiciona essa função como um filtro e predicado de bloco na tabela Contatos.</span><span class="sxs-lookup"><span data-stu-id="da6e1-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="da6e1-148">O predicado do filtro faz com que as consultas retornem somente as linhas que pertencem ao usuário atual, e o predicado de bloco atua como uma medida de segurança para impedir que o aplicativo insira nunca acidentalmente uma linha para o usuário errado.</span><span class="sxs-lookup"><span data-stu-id="da6e1-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="da6e1-149">Agora execute o aplicativo e entre como user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="da6e1-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="da6e1-150">Esse usuário agora vê somente os Contatos que atribuímos anteriormente a essa UserId:</span><span class="sxs-lookup"><span data-stu-id="da6e1-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Aplicativo Contact Manager antes de habilitar o RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="da6e1-152">Para uma validação extra, tente registrar um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="da6e1-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="da6e1-153">Ele não verá qualquer contato, pois nenhum foi atribuído a ele.</span><span class="sxs-lookup"><span data-stu-id="da6e1-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="da6e1-154">Se esse usuário criar um novo contato, ele será atribuído ao usuário e apenas o usuário poderá vê-lo.</span><span class="sxs-lookup"><span data-stu-id="da6e1-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da6e1-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da6e1-155">Next steps</span></span>
<span data-ttu-id="da6e1-156">É isso!</span><span class="sxs-lookup"><span data-stu-id="da6e1-156">That's it!</span></span> <span data-ttu-id="da6e1-157">O aplicativo Web simples Gerenciador de Contatos foi convertido em um multilocatário, no qual cada usuário tem sua própria lista de contatos.</span><span class="sxs-lookup"><span data-stu-id="da6e1-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="da6e1-158">Ao usar a Segurança em nível de linha, evitamos a complexidade que é aplicar a lógica de acesso do locatário ao código de nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="da6e1-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="da6e1-159">Essa transparência permite que o aplicativo se concentre no verdadeiro problema, e também reduz o risco de vazamento acidental dos dados à medida que a base de código do aplicativo cresce.</span><span class="sxs-lookup"><span data-stu-id="da6e1-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="da6e1-160">Este tutorial forneceu apenas uma pequena amostra do que é possível fazer com RLS.</span><span class="sxs-lookup"><span data-stu-id="da6e1-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="da6e1-161">Por exemplo, é possível ter mais uma lógico de acesso mais sofisticada ou granular, e é possível armazenar mais do que apenas a UserId atual no SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="da6e1-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="da6e1-162">Também é possível [integrar o RLS com as bibliotecas de cliente das ferramentas de banco de dados elástico](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) a fim de oferecer suporte a fragmentos de multilocatários em uma camada de dados de expansão.</span><span class="sxs-lookup"><span data-stu-id="da6e1-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="da6e1-163">Além dessas possibilidades, também estamos trabalhando para melhorar ainda mais o RLS.</span><span class="sxs-lookup"><span data-stu-id="da6e1-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="da6e1-164">Se você tiver alguma dúvida, ideias ou coisas que gostaria de ver, envie nos comentários.</span><span class="sxs-lookup"><span data-stu-id="da6e1-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="da6e1-165">Agradecemos por seus comentários!</span><span class="sxs-lookup"><span data-stu-id="da6e1-165">We appreciate your feedback!</span></span>

