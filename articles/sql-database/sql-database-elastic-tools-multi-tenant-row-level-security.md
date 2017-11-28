---
title: "aplicativos de locatário aaaMulti com segurança em nível de linha e ferramentas de banco de dados Elástico"
description: "Saiba como ferramentas de banco de dados Elástico toouse junto com o nível de linha segurança toobuild um aplicativo com uma camada de dados altamente escalonáveis no banco de dados SQL que oferece suporte a fragmentos de multilocatários."
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
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="1f270-103">Aplicativos multilocatários com ferramentas de banco de dados elástico e segurança em nível de linha</span><span class="sxs-lookup"><span data-stu-id="1f270-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="1f270-104">[Ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md) e [RLS (segurança) de nível de linha](https://msdn.microsoft.com/library/dn765131) oferecem um conjunto avançado de recursos de forma flexível e eficiente dimensionar a camada de dados de saudação de um aplicativo multilocatário com o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1f270-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="1f270-105">Confira [Padrões de design para aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="1f270-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="1f270-106">Este artigo ilustra como toouse toobuild de juntos essas tecnologias um aplicativo com uma camada de dados altamente escalonável que dá suporte a fragmentos de multilocatários, usando **ADO.NET SqlClient** e/ou **doEntityFramework**.</span><span class="sxs-lookup"><span data-stu-id="1f270-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="1f270-107">**Ferramentas de banco de dados Elástico** permite que os desenvolvedores tooscale camada de dados de saudação de um aplicativo por meio de práticas de fragmentação padrão do setor, usando um conjunto de bibliotecas .NET e modelos de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f270-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="1f270-108">Gerenciar fragmentos com usando Olá Elástico biblioteca de cliente do banco de dados ajuda a automatizar e simplificar muitas das tarefas de base Olá geralmente associadas a fragmentação.</span><span class="sxs-lookup"><span data-stu-id="1f270-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="1f270-109">**Segurança em nível de linha** permite que os dados de toostore de desenvolvedores para vários locatários no mesmo banco de dados usando toofilter de políticas de segurança as linhas que não pertencem toohello locatário executando uma consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f270-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="1f270-110">Centralizando a lógica de acesso com a RLS dentro do banco de dados hello, em vez no aplicativo hello, simplifica a manutenção e reduz o risco de saudação de erro como a base de código de um aplicativo cresce.</span><span class="sxs-lookup"><span data-stu-id="1f270-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="1f270-111">Usando esses recursos juntos, um aplicativo pode se beneficiar de ganhos de eficiência e economia de custo ao armazenar os dados para vários locatários em Olá mesmo banco de dados de fragmento.</span><span class="sxs-lookup"><span data-stu-id="1f270-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="1f270-112">Em Olá mesmo tempo, um aplicativo ainda tem Olá flexibilidade toooffer isolado, fragmentos de único locatário para locatários "premium" que necessitam de garantias de desempenho mais rígidas como fragmentos multilocatários não garantem a distribuição de recursos igual entre locatários.</span><span class="sxs-lookup"><span data-stu-id="1f270-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="1f270-113">Em resumo, Olá da biblioteca do cliente do banco de dados Elástico [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) APIs conectar-se automaticamente locatários toohello fragmento corretas banco de dados que contém sua chave de fragmentação (geralmente um "TenantId").</span><span class="sxs-lookup"><span data-stu-id="1f270-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="1f270-114">Uma vez conectado, uma política de segurança RLS no banco de dados de saudação garante que os locatários possam acessar somente linhas que contêm seu TenantId.</span><span class="sxs-lookup"><span data-stu-id="1f270-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="1f270-115">Presume-se que todas as tabelas contêm um tooindicate de coluna TenantId quais linhas pertencem tooeach locatário.</span><span class="sxs-lookup"><span data-stu-id="1f270-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Arquitetura de aplicativo de blog][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="1f270-117">Baixe o projeto de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="1f270-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="1f270-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f270-118">Prerequisites</span></span>
* <span data-ttu-id="1f270-119">Usar o Visual Studio (2012 ou superior)</span><span class="sxs-lookup"><span data-stu-id="1f270-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="1f270-120">Criar três Bancos de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1f270-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="1f270-121">Baixar o projeto de exemplo: [Ferramentas de Banco de Dados Elástico para o SQL do Azure - Fragmentos Multilocatários](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="1f270-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="1f270-122">Preencha as informações de saudação para seus bancos de dados no início de saudação do **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="1f270-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="1f270-123">Este projeto estende Olá um descritos em [Elástico ferramentas de banco de dados do SQL Azure - integração do Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) adicionando suporte para bancos de dados de fragmento de multilocatário.</span><span class="sxs-lookup"><span data-stu-id="1f270-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="1f270-124">Ele cria um aplicativo de console simples para a criação de blogs e postagens, com quatro locatários e dois fragmentos de multilocatário bancos de dados conforme ilustrado na Olá acima do diagrama.</span><span class="sxs-lookup"><span data-stu-id="1f270-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="1f270-125">Compilar e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1f270-125">Build and run hello application.</span></span> <span data-ttu-id="1f270-126">Isso irá inicializar o Gerenciador do mapa de fragmentos de ferramentas de banco de dados Elástico hello e Olá executar testes a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f270-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="1f270-127">Usando o Entity Framework e o LINQ, crie um novo blog e exiba todos os blogs para cada locatário</span><span class="sxs-lookup"><span data-stu-id="1f270-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="1f270-128">Usando o ADO.NET SqlClient, exiba todos os blogs para um locatário</span><span class="sxs-lookup"><span data-stu-id="1f270-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="1f270-129">Tente tooinsert um blog para Olá locatário errado tooverify que um erro será lançado</span><span class="sxs-lookup"><span data-stu-id="1f270-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="1f270-130">Observe que como RLS ainda não foi habilitado em bancos de dados de fragmento hello, cada um desses testes revela um problema: locatários são toosee capaz de blogs que não pertencem toothem e aplicativo hello não será impedido de inserir um blog para locatário errado hello.</span><span class="sxs-lookup"><span data-stu-id="1f270-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="1f270-131">Olá restante deste artigo descreve como tooresolve esses problemas impondo locatário isolamento com a RLS.</span><span class="sxs-lookup"><span data-stu-id="1f270-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="1f270-132">Há duas etapas:</span><span class="sxs-lookup"><span data-stu-id="1f270-132">There are two steps:</span></span> 

1. <span data-ttu-id="1f270-133">**Camada de aplicativo**: modificar o código do aplicativo hello tooalways conjunto Olá TenantId atual em Olá SESSION_CONTEXT depois de abrir uma conexão.</span><span class="sxs-lookup"><span data-stu-id="1f270-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="1f270-134">projeto de exemplo Hello já tenha feito isso.</span><span class="sxs-lookup"><span data-stu-id="1f270-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="1f270-135">**Camada de dados**: criar uma política de segurança RLS em cada toofilter de banco de dados de fragmento linhas com base em Olá TenantId armazenadas em SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1f270-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="1f270-136">Você precisará toodo isso para cada um dos seus bancos de dados de fragmento, caso contrário linhas em fragmentos multilocatários não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="1f270-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="1f270-137">Camada de aplicativo da etapa 1): definir TenantId em Olá SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="1f270-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="1f270-138">Depois de conectar tooa fragmento banco de dados usando dados da biblioteca de cliente do banco de dados Elástico Olá que APIs de roteamentos dependentes, aplicativo hello ainda precisa de banco de dados de saudação de tootell quais TenantId está usando essa conexão para que uma política de segurança RLS pode filtrar linhas pertencente tooother locatários.</span><span class="sxs-lookup"><span data-stu-id="1f270-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="1f270-139">Olá toopass de maneira recomendada essas informações são toostore Olá TenantId atual para essa conexão em Olá [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f270-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="1f270-140">(Observação: como alternativa, você pode usar [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), mas SESSION_CONTEXT é uma opção melhor, pois é mais fácil toouse, retorna nulo por padrão e dá suporte a pares chave-valor.)</span><span class="sxs-lookup"><span data-stu-id="1f270-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="1f270-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="1f270-141">Entity Framework</span></span>
<span data-ttu-id="1f270-142">Para aplicativos usando o Entity Framework, abordagem mais fácil de saudação é Olá tooset SESSION_CONTEXT em Olá ElasticScaleContext substituir descrito em [roteamento dependente de dados usando EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="1f270-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="1f270-143">Antes de retornar conexão Olá orientada por meio do roteamento dependente de dados, criar e executar um SqlCommand que define 'TenantId' em Olá SESSION_CONTEXT toohello shardingKey especificado para essa conexão.</span><span class="sxs-lookup"><span data-stu-id="1f270-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="1f270-144">Dessa forma, você só precisa toowrite código depois tooset Olá SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1f270-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

<span data-ttu-id="1f270-145">Agora Olá SESSION_CONTEXT é definido automaticamente com hello especificado TenantId sempre que é invocado ElasticScaleContext:</span><span class="sxs-lookup"><span data-stu-id="1f270-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="1f270-146">ADO.NET SqlClient</span><span class="sxs-lookup"><span data-stu-id="1f270-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="1f270-147">Para aplicativos usando ADO.NET SqlClient hello recomendada abordagem é toocreate uma função de wrapper em torno de ShardMap.OpenConnectionForKey() que define automaticamente 'TenantId' no hello SESSION_CONTEXT toohello corrigir TenantId antes de retornar um conexão.</span><span class="sxs-lookup"><span data-stu-id="1f270-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="1f270-148">tooensure que sempre é possível definir SESSION_CONTEXT, você só deve abrir as conexões usando essa função de wrapper.</span><span class="sxs-lookup"><span data-stu-id="1f270-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="1f270-149">Etapa 2) Camada de dados: criar política de segurança no nível da linha</span><span class="sxs-lookup"><span data-stu-id="1f270-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="1f270-150">Criar linhas de que cada locatário pode acessar de uma saudação de toofilter de política de segurança</span><span class="sxs-lookup"><span data-stu-id="1f270-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="1f270-151">Agora que o aplicativo hello é definir SESSION_CONTEXT com hello TenantId atual antes de consultar, uma política de segurança RLS pode filtrar consultas e excluir linhas que têm um TenantId diferente.</span><span class="sxs-lookup"><span data-stu-id="1f270-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="1f270-152">O RLS é implementado no T-SQL: uma função definida pelo usuário define a lógica de acesso a saudação e uma política de segurança associado a essa função tooany número de tabelas.</span><span class="sxs-lookup"><span data-stu-id="1f270-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="1f270-153">Para este projeto, função hello simplesmente verificará se Olá aplicativo (em vez de algum outro usuário do SQL) é o banco de dados de toohello conectado, e esse Olá 'TenantId' armazenado em Olá SESSION_CONTEXT corresponde Olá TenantId de uma determinada linha.</span><span class="sxs-lookup"><span data-stu-id="1f270-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="1f270-154">Um predicado de filtro permitirá linhas que atendem estas condições toopass por filtro Olá para consultas SELECT, UPDATE e DELETE; e um predicado de block impedirá linhas que violam essas condições sejam inseridos ou atualizados.</span><span class="sxs-lookup"><span data-stu-id="1f270-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="1f270-155">Se não tiver sido definido SESSION_CONTEXT, ela retornará que NULL e nenhuma linha será visível ou a capacidade de toobe inserido.</span><span class="sxs-lookup"><span data-stu-id="1f270-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="1f270-156">tooenable RLS, execute Olá T-SQL a seguir em todos os fragmentos usando o Visual Studio (SSDT), SSMS, ou Olá script do PowerShell incluído no projeto hello (ou se você estiver usando [trabalhos do banco de dados Elástico](sql-database-elastic-jobs-overview.md), você pode usá-lo em execução tooautomate desse T-SQL em todos os fragmentos):</span><span class="sxs-lookup"><span data-stu-id="1f270-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="1f270-157">Para projetos mais complexos que precisam de predicado de saudação tooadd em centenas de tabelas, você pode usar um procedimento armazenado auxiliar que gera automaticamente uma política de segurança adicionando um predicado em todas as tabelas em um esquema.</span><span class="sxs-lookup"><span data-stu-id="1f270-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="1f270-158">Consulte [tabelas de tooall aplicar segurança de nível de linha - script auxiliar (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="1f270-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="1f270-159">Agora se você executar o aplicativo de exemplo hello novamente, locatários serão capaz de toosee somente as linhas que pertencem a toothem.</span><span class="sxs-lookup"><span data-stu-id="1f270-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="1f270-160">Além disso, o aplicativo hello não é possível inserir linhas que pertencem a tootenants diferente de banco de dados do hello toohello conectado no momento um fragmento e ele não é possível atualizar linhas visíveis toohave um TenantId diferente.</span><span class="sxs-lookup"><span data-stu-id="1f270-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="1f270-161">Se o aplicativo hello tentativas toodo ou, um DbUpdateException será gerado.</span><span class="sxs-lookup"><span data-stu-id="1f270-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="1f270-162">Se você adicionar uma nova tabela posteriormente, simplesmente ALTER Olá a política de segurança e adicione os predicados de filtro e bloqueio na nova tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="1f270-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="1f270-163">Adicionar padrão popular de restrições tooautomatically TenantId para inserções</span><span class="sxs-lookup"><span data-stu-id="1f270-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="1f270-164">Você pode colocar um padrão popular de restrição em cada tabela tooautomatically Olá TenantId com hello valor armazenado atualmente em SESSION_CONTEXT ao inserir linhas.</span><span class="sxs-lookup"><span data-stu-id="1f270-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="1f270-165">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1f270-165">For example:</span></span> 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="1f270-166">Agora o aplicativo hello não precisa toospecify um TenantId ao inserir linhas:</span><span class="sxs-lookup"><span data-stu-id="1f270-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="1f270-167">Se você usar restrições padrão para um projeto do Entity Framework, é recomendável que você não incluir coluna de TenantId Olá no seu modelo de dados EF.</span><span class="sxs-lookup"><span data-stu-id="1f270-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="1f270-168">Isso ocorre porque as consultas de Entity Framework fornecem valores padrão que substituirão as restrições de padrão de saudação criadas no T-SQL que usam SESSION_CONTEXT automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1f270-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="1f270-169">projeto de exemplo de restrições de padrão de toouse no hello, por exemplo, você deve remover a TenantId do DataClasses.cs (e executar Add-Migration Olá Package Manager Console) e tooensure use T-SQL que Olá campo só existe nas tabelas de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f270-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="1f270-170">Dessa forma, o EF não fornecerá valores padrão incorretos automaticamente ao inserir dados.</span><span class="sxs-lookup"><span data-stu-id="1f270-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="1f270-171">(Opcional) Habilitar todas as linhas de uma tooaccess de "superusuário"</span><span class="sxs-lookup"><span data-stu-id="1f270-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="1f270-172">Alguns aplicativos podem ser toocreate "superusuário" quem pode acessar todas as linhas, por exemplo, em ordem tooenable relatórios em todos os locatários em todos os fragmentos ou operações de divisão/mesclagem tooperform em fragmentos que envolvem mover linhas de locatário entre bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="1f270-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="1f270-173">tooenable isso, você deve criar um novo usuário SQL ("superusuário" neste exemplo) em cada banco de dados de fragmento.</span><span class="sxs-lookup"><span data-stu-id="1f270-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="1f270-174">Em seguida, altere a política de segurança de saudação com uma nova função de predicado que permite que esse usuário tooaccess todas as linhas:</span><span class="sxs-lookup"><span data-stu-id="1f270-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

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

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="1f270-175">Manutenção </span><span class="sxs-lookup"><span data-stu-id="1f270-175">Maintenance</span></span>
* <span data-ttu-id="1f270-176">**Adicionando novos fragmentos**: você deve executar Olá T-SQL script tooenable RLS em quaisquer novos fragmentos, caso contrário, consultas sobre esses fragmentos não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="1f270-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="1f270-177">**Adicionando novas tabelas**: você deve adicionar um filtro e bloquear a política de segurança de predicado toohello em todos os fragmentos sempre que uma nova tabela é criada, caso contrário, consultas na nova tabela de saudação não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="1f270-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="1f270-178">Isso pode ser automatizado usando um gatilho DDL, conforme descrito em [aplicar segurança de nível de linha toonewly criado automaticamente tabelas (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f270-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="1f270-179">Resumo</span><span class="sxs-lookup"><span data-stu-id="1f270-179">Summary</span></span>
<span data-ttu-id="1f270-180">Ferramentas de banco de dados Elástico e segurança em nível de linha podem ser usado tooscale junto camada de dados de um aplicativo com suporte para vários locatários e único locatário fragmentos.</span><span class="sxs-lookup"><span data-stu-id="1f270-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="1f270-181">Multilocatários fragmentos podem ser usados toostore dados com mais eficiência (principalmente em casos em que um grande número de locatários têm apenas algumas linhas de dados), ao único locatário fragmentos podem ser usados toosupport premium locatários com isolamento e desempenho mais rígida requisitos.</span><span class="sxs-lookup"><span data-stu-id="1f270-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="1f270-182">Para obter mais informações, confira [a referência à Segurança em Nível de Linha](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="1f270-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1f270-183">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1f270-183">Additional resources</span></span>
* [<span data-ttu-id="1f270-184">O que é um pool elástico do Azure?</span><span class="sxs-lookup"><span data-stu-id="1f270-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="1f270-185">Escalando horizontalmente com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1f270-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="1f270-186">Padrões de design para aplicativos SaaS multilocatários com o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1f270-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="1f270-187">Autenticação em aplicativos multilocatários usando o Azure AD e o OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="1f270-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="1f270-188">Aplicativo Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="1f270-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="1f270-189">Perguntas e solicitações de recursos</span><span class="sxs-lookup"><span data-stu-id="1f270-189">Questions and Feature Requests</span></span>
<span data-ttu-id="1f270-190">Para dúvidas, entre em contato toous em Olá [Fórum do banco de dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e para solicitações de recurso, adicione-toohello [Fórum de comentários do banco de dados SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="1f270-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


