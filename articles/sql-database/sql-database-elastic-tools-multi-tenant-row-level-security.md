---
title: "Aplicativos multilocatários com ferramentas de banco de dados elástico e segurança em nível de linha"
description: "Saiba como usar as ferramentas de banco de dados elástico com segurança em nível de linha para criar um aplicativo com uma camada de dados altamente dimensionável no Banco de Dados SQL que dá suporte a fragmentos multilocatários."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="613ce-103">Aplicativos multilocatários com ferramentas de banco de dados elástico e segurança em nível de linha</span><span class="sxs-lookup"><span data-stu-id="613ce-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="613ce-104">As [ferramentas de banco de dados elástico](sql-database-elastic-scale-get-started.md) e a [RLS (segurança em nível de linha)](https://msdn.microsoft.com/library/dn765131) oferecem um conjunto avançado de funcionalidades para escalar a camada de dados de um aplicativo multilocatário com um Banco de Dados SQL do Azure de maneira flexível e eficiente.</span><span class="sxs-lookup"><span data-stu-id="613ce-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="613ce-105">Confira [Padrões de design para aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="613ce-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="613ce-106">Este artigo ilustra como usar essas tecnologias em conjunto para criar um aplicativo com uma camada de dados altamente escalonável e que dá suporte a fragmentos multilocatários, usando o **ADO.NET SqlClient** e/ou o **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="613ce-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="613ce-107">**Ferramentas de banco de dados elástico** permitem que os desenvolvedores expandir a camada de dados de um aplicativo por meio de práticas de fragmentação padrão do setor usando um conjunto de bibliotecas .NET e modelos de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="613ce-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="613ce-108">Gerenciar fragmentos usando a Biblioteca Cliente do Banco de Dados Elástico ajuda a automatizar e simplificar muitas das tarefas infraestruturais normalmente associadas à fragmentação.</span><span class="sxs-lookup"><span data-stu-id="613ce-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="613ce-109">**segurança em nível de linha** permite aos desenvolvedores armazenar dados para vários locatários no mesmo banco de dados usando políticas de segurança para filtrar linhas que não pertencem ao locatário que está executando uma consulta.</span><span class="sxs-lookup"><span data-stu-id="613ce-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="613ce-110">Centralizar a lógica de acesso com RLS no banco de dados, em vez de no aplicativo, simplifica a manutenção e reduz o risco de erros conforme a base de código de um aplicativo é expandida.</span><span class="sxs-lookup"><span data-stu-id="613ce-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="613ce-111">Ao usar esses recursos em conjunto, um aplicativo pode desfrutar de ganhos de eficiência e economia de custo armazenando dados para vários locatários no mesmo banco de dados de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="613ce-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="613ce-112">Ao mesmo tempo, um aplicativo ainda terá a flexibilidade para oferecer fragmentos isolados de um locatário para locatários "premium" que exigem garantias de desempenho mais rígidas, já que os fragmentos multilocatários não garantem a distribuição uniforme dos recursos entre os locatários.</span><span class="sxs-lookup"><span data-stu-id="613ce-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="613ce-113">Em resumo, as APIs de [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) da biblioteca cliente do banco de dados elástico são conectadas automaticamente ao banco de dados de fragmentos correto que contém sua chave de fragmentação (geralmente um "TenantId").</span><span class="sxs-lookup"><span data-stu-id="613ce-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="613ce-114">Após o estabelecimento da conexão, uma política de segurança RLS no banco de dados garante que os locatários possam acessar somente as linhas que contêm seu TenantId.</span><span class="sxs-lookup"><span data-stu-id="613ce-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="613ce-115">Presume-se que todas as tabelas contenham uma coluna TenantId para indicar quais linhas pertencem a cada locatário.</span><span class="sxs-lookup"><span data-stu-id="613ce-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![Arquitetura de aplicativo de blog][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="613ce-117">Baixar o projeto de exemplo</span><span class="sxs-lookup"><span data-stu-id="613ce-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="613ce-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="613ce-118">Prerequisites</span></span>
* <span data-ttu-id="613ce-119">Usar o Visual Studio (2012 ou superior)</span><span class="sxs-lookup"><span data-stu-id="613ce-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="613ce-120">Criar três Bancos de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="613ce-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="613ce-121">Baixar o projeto de exemplo: [Ferramentas de Banco de Dados Elástico para o SQL do Azure - Fragmentos Multilocatários](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="613ce-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="613ce-122">Preencha as informações dos seus bancos de dados no início do **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="613ce-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="613ce-123">Esse projeto expande o descrito em [Ferramentas de Banco de Dados Elástico para o SQL do Azure - Integração com o Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) adicionando suporte para bancos de dados de fragmentos multilocatários.</span><span class="sxs-lookup"><span data-stu-id="613ce-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="613ce-124">Ele cria um aplicativo de console simples para a criação de blogs e postagens, com quatro locatários e dois bancos de dados de fragmentos multilocatários, conforme é ilustrado no diagrama acima.</span><span class="sxs-lookup"><span data-stu-id="613ce-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="613ce-125">Compile e execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="613ce-125">Build and run the application.</span></span> <span data-ttu-id="613ce-126">Isso inicializará o gerenciador de mapas de fragmentos das ferramentas de banco de dados elástico e executará os seguintes testes:</span><span class="sxs-lookup"><span data-stu-id="613ce-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="613ce-127">Usando o Entity Framework e o LINQ, crie um novo blog e exiba todos os blogs para cada locatário</span><span class="sxs-lookup"><span data-stu-id="613ce-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="613ce-128">Usando o ADO.NET SqlClient, exiba todos os blogs para um locatário</span><span class="sxs-lookup"><span data-stu-id="613ce-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="613ce-129">Tente inserir um blog para o locatário errado para verificar se um erro será gerado</span><span class="sxs-lookup"><span data-stu-id="613ce-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="613ce-130">Observe que, como a RLS ainda não foi habilitada nos bancos de dados de fragmentos, cada um desses testes revela um problema: locatários podem ver blogs que não pertencem a eles e o aplicativo não é impedido de inserir um blog para o locatário errado.</span><span class="sxs-lookup"><span data-stu-id="613ce-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="613ce-131">O restante deste artigo descreve como resolver esses problemas impondo o isolamento de locatários com RLS.</span><span class="sxs-lookup"><span data-stu-id="613ce-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="613ce-132">Há duas etapas:</span><span class="sxs-lookup"><span data-stu-id="613ce-132">There are two steps:</span></span> 

1. <span data-ttu-id="613ce-133">**Camada de aplicativo**: modifique o código do aplicativo para sempre definir a TenantId atual em SESSION_CONTEXT depois de abrir uma conexão.</span><span class="sxs-lookup"><span data-stu-id="613ce-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="613ce-134">O projeto de exemplo já fez isso.</span><span class="sxs-lookup"><span data-stu-id="613ce-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="613ce-135">**Camada de dados**: crie uma política de segurança RLS em cada banco de dados de fragmentos para filtrar as linhas com base na TenantId armazenada em SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="613ce-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="613ce-136">Você precisará fazer isso para cada um dos seus bancos de dados de fragmentos, caso contrário, linhas em fragmentos multilocatários não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="613ce-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="613ce-137">Etapa 1) Camada de aplicativo: definir a TenantId em SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="613ce-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="613ce-138">Depois de se conectar a um banco de dados de fragmentos usando dados da biblioteca cliente do banco de dados elástico que depende de APIs de roteamento, o aplicativo ainda precisa informar o banco de dados qual TenantId está usando essa conexão para que uma política de segurança RLS possa filtrar linhas pertencentes a outros locatários.</span><span class="sxs-lookup"><span data-stu-id="613ce-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="613ce-139">A maneira recomendada para passar essa informação é armazenar a TenantId atual dessa conexão em [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="613ce-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="613ce-140">(Observação: como alternativa, use também [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), mas SESSION_CONTEXT é uma opção melhor porque é mais fácil de usar, retorna NULL por padrão e dá suporte aos pares chave-valor.)</span><span class="sxs-lookup"><span data-stu-id="613ce-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="613ce-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="613ce-141">Entity Framework</span></span>
<span data-ttu-id="613ce-142">Para os aplicativos que usam o Entity Framework, a abordagem mais fácil é definir SESSION_CONTEXT na substituição de ElasticScaleContext descrita em [Roteamento dependente de dados usando o EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="613ce-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="613ce-143">Antes de retornar a conexão negociada por meio do roteamento dependente de dados, simplesmente crie e execute um SqlCommand que define 'TenantId' em SESSION_CONTEXT para o shardingKey especificado para essa conexão.</span><span class="sxs-lookup"><span data-stu-id="613ce-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="613ce-144">Dessa maneira, só é preciso gravar o código uma vez para definir SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="613ce-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

<span data-ttu-id="613ce-145">Agora, o SESSION_CONTEXT será automaticamente definido com a TenantId especificada sempre que ElasticScaleContext for chamado:</span><span class="sxs-lookup"><span data-stu-id="613ce-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a><span data-ttu-id="613ce-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="613ce-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="613ce-147">Para os aplicativos que usam o ADO.NET SqlClient, a abordagem recomendada é criar uma função de wrapper em torno de ShardMap.OpenConnectionForKey() que define automaticamente 'TenantId' em SESSION_CONTEXT para a TenantId correta antes de retornar uma conexão.</span><span class="sxs-lookup"><span data-stu-id="613ce-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="613ce-148">Para garantir que SESSION_CONTEXT seja sempre definido, você só deve abrir conexões usando essa função de wrapper.</span><span class="sxs-lookup"><span data-stu-id="613ce-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="613ce-149">Etapa 2) Camada de dados: criar política de segurança no nível da linha</span><span class="sxs-lookup"><span data-stu-id="613ce-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="613ce-150">Criar uma política de segurança para filtrar as linhas que cada locatário pode acessar</span><span class="sxs-lookup"><span data-stu-id="613ce-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="613ce-151">Agora que o aplicativo está definindo SESSION_CONTEXT com a TenantId atual antes de consultar, uma política de segurança RLS pode filtrar as consultas e excluir as linhas que têm uma TenantId diferente.</span><span class="sxs-lookup"><span data-stu-id="613ce-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="613ce-152">A RLS é implementada no T-SQL: uma função definida pelo usuário define a lógica de acesso e uma política de segurança associa essa função a qualquer quantidade de tabelas.</span><span class="sxs-lookup"><span data-stu-id="613ce-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="613ce-153">Para este projeto, a função simplesmente verificará se o aplicativo (em vez de outro usuário do SQL) está conectado ao banco de dados e se a 'TenantId' armazenada em SESSION_CONTEXT corresponde à TenantId de uma determinada linha.</span><span class="sxs-lookup"><span data-stu-id="613ce-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="613ce-154">Um predicado de filtro permitirá que as linhas que atendem a essas condições passem no filtro para as consultas SELECT, UPDATE e DELETE; e um predicado de bloco impedirá que as linhas que violam essas condições sejam inseridas ou atualizadas com INSERT ou UPDATE, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="613ce-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="613ce-155">Se SESSION_CONTEXT não tiver sido definido, retornará NULL e nenhuma linha será visível ou poderá ser inserida.</span><span class="sxs-lookup"><span data-stu-id="613ce-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="613ce-156">Para habilitar a RLS, execute o seguinte comando do T-SQL em todos os fragmentos usando Visual Studio (SSDT), SSMS ou o script do PowerShell incluído no projeto (ou, se você estiver usando [Trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-overview.md), você poderá usá-lo para automatizar a execução desse T-SQL em todos os fragmentos):</span><span class="sxs-lookup"><span data-stu-id="613ce-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> <span data-ttu-id="613ce-157">Para os projetos mais complexos que precisam adicionar o predicado a centenas de tabelas, você poderá usar um procedimento auxiliar armazenado que gera uma política de segurança automaticamente adicionando um predicado a todas as tabelas em um esquema.</span><span class="sxs-lookup"><span data-stu-id="613ce-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="613ce-158">Confira [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script) (Aplicar segurança no nível de linha a todas as tabelas – script auxiliar (blog)).</span><span class="sxs-lookup"><span data-stu-id="613ce-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="613ce-159">Agora, se você executar novamente o aplicativo de exemplo, os locatários poderão ver apenas as linhas que pertencem a eles.</span><span class="sxs-lookup"><span data-stu-id="613ce-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="613ce-160">Além disso, o aplicativo não poderá inserir as linhas que pertencem aos locatários diferentes dos atualmente conectados ao banco de dados de fragmentos e não poderá atualizar as linhas visíveis com uma TenantId diferente.</span><span class="sxs-lookup"><span data-stu-id="613ce-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="613ce-161">Se o aplicativo tentar qualquer uma dessas operações, será gerado um DbUpdateException.</span><span class="sxs-lookup"><span data-stu-id="613ce-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="613ce-162">Se você adicionar uma nova tabela posteriormente, bastará alterar com ALTER a política de segurança e adicionar predicados de filtro e bloco à nova tabela:</span><span class="sxs-lookup"><span data-stu-id="613ce-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="613ce-163">Adicionar restrições padrão para preencher automaticamente o TenantId para INSERTs</span><span class="sxs-lookup"><span data-stu-id="613ce-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="613ce-164">Você pode colocar uma restrição padrão em cada tabela para preencher automaticamente a TenantId com o valor armazenado atualmente em SESSION_CONTEXT ao inserir as linhas.</span><span class="sxs-lookup"><span data-stu-id="613ce-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="613ce-165">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="613ce-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="613ce-166">Agora, o aplicativo não precisa especificar um TenantId ao inserir linhas:</span><span class="sxs-lookup"><span data-stu-id="613ce-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> <span data-ttu-id="613ce-167">Se você usar restrições padrão para um projeto do Entity Framework, é recomendável não incluir a coluna TenantId em seu modelo de dados do EF.</span><span class="sxs-lookup"><span data-stu-id="613ce-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="613ce-168">Isso ocorre porque as consultas do Entity Framework fornecem automaticamente os valores padrão que substituirão as restrições padrão criadas no T-SQL que usa o SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="613ce-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="613ce-169">Para usar restrições padrão no projeto de exemplo, por exemplo, você deve remover TenantId de DataClasses.cs (e executar Add-Migration no Console do Gerenciador de Pacotes) e usar o T-SQL para garantir que o campo só exista nas tabelas do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="613ce-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="613ce-170">Dessa forma, o EF não fornecerá valores padrão incorretos automaticamente ao inserir dados.</span><span class="sxs-lookup"><span data-stu-id="613ce-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="613ce-171">(Opcional) Habilitar um "superusuário" acessar todas as linhas</span><span class="sxs-lookup"><span data-stu-id="613ce-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="613ce-172">Alguns aplicativos talvez queiram criar um "superusuário" que pode acessar todas as linhas, por exemplo, para permitir a emissão de relatórios em todos os locatários em todos os fragmentos ou para executar operações de divisão/mesclagem em fragmentos que envolvem a movimentação de linhas de locatário entre bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="613ce-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="613ce-173">Para habilitar isso, você deve criar um novo usuário do SQL ("superusuário" neste exemplo) em cada banco de dados do fragmento.</span><span class="sxs-lookup"><span data-stu-id="613ce-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="613ce-174">Em seguida, altere a política de segurança com uma nova função de predicado que permite que esse usuário acesse todas as linhas:</span><span class="sxs-lookup"><span data-stu-id="613ce-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="613ce-175">Manutenção</span><span class="sxs-lookup"><span data-stu-id="613ce-175">Maintenance</span></span>
* <span data-ttu-id="613ce-176">**Adicionando novos fragmentos**: você deve executar o script T-SQL para habilitar a RLS em qualquer novo fragmento; do contrário, as consultas nesses fragmentos não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="613ce-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="613ce-177">**Adicionando novas tabelas**: você deve adicionar predicados de filtro e bloco à política de segurança em todos os fragmentos sempre que uma nova tabela for criada; do contrário, as consultas na nova tabela não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="613ce-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="613ce-178">Isso pode ser automatizado usando um gatilho DDL, conforme é descrito em [Aplicar Segurança em Nível de Linha automaticamente a tabelas recém-criadas (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="613ce-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="613ce-179">Resumo</span><span class="sxs-lookup"><span data-stu-id="613ce-179">Summary</span></span>
<span data-ttu-id="613ce-180">Ferramentas de banco de dados elástico e segurança em nível de linha podem ser usadas em conjunto para expandir a camada de dados de um aplicativo com suporte para fragmentos multilocatários e de um locatário.</span><span class="sxs-lookup"><span data-stu-id="613ce-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="613ce-181">Fragmentos multilocatários podem ser usados para armazenar dados com mais eficiência (principalmente em casos em que uma grande quantidade de locatários têm apenas algumas linhas de dados), enquanto fragmentos de um locatário podem ser usados para dar suporte a locatários premium com requisitos de desempenho e isolamento mais rígidos.</span><span class="sxs-lookup"><span data-stu-id="613ce-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="613ce-182">Para obter mais informações, confira [a referência à Segurança em Nível de Linha](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="613ce-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="613ce-183">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="613ce-183">Additional resources</span></span>
* [<span data-ttu-id="613ce-184">O que é um pool elástico do Azure?</span><span class="sxs-lookup"><span data-stu-id="613ce-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="613ce-185">Escalando horizontalmente com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="613ce-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="613ce-186">Padrões de design para aplicativos SaaS multilocatários com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="613ce-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="613ce-187">Autenticação em aplicativos multilocatários usando o Azure AD e o OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="613ce-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="613ce-188">Aplicativo Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="613ce-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="613ce-189">Perguntas e solicitações de recursos</span><span class="sxs-lookup"><span data-stu-id="613ce-189">Questions and Feature Requests</span></span>
<span data-ttu-id="613ce-190">Em caso de dúvidas, entre em contato conosco pelo [fórum do Banco de Dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e, para solicitações de recursos, adicione-as ao [fórum de comentários sobre o Banco de Dados SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="613ce-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


