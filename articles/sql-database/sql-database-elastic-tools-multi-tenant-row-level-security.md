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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Aplicativos multilocatários com ferramentas de banco de dados elástico e segurança em nível de linha
[Ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md) e [RLS (segurança) de nível de linha](https://msdn.microsoft.com/library/dn765131) oferecem um conjunto avançado de recursos de forma flexível e eficiente dimensionar a camada de dados de saudação de um aplicativo multilocatário com o banco de dados do SQL Azure. Confira [Padrões de design para aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) para saber mais. 

Este artigo ilustra como toouse toobuild de juntos essas tecnologias um aplicativo com uma camada de dados altamente escalonável que dá suporte a fragmentos de multilocatários, usando **ADO.NET SqlClient** e/ou **doEntityFramework**.  

* **Ferramentas de banco de dados Elástico** permite que os desenvolvedores tooscale camada de dados de saudação de um aplicativo por meio de práticas de fragmentação padrão do setor, usando um conjunto de bibliotecas .NET e modelos de serviço do Azure. Gerenciar fragmentos com usando Olá Elástico biblioteca de cliente do banco de dados ajuda a automatizar e simplificar muitas das tarefas de base Olá geralmente associadas a fragmentação. 
* **Segurança em nível de linha** permite que os dados de toostore de desenvolvedores para vários locatários no mesmo banco de dados usando toofilter de políticas de segurança as linhas que não pertencem toohello locatário executando uma consulta de saudação. Centralizando a lógica de acesso com a RLS dentro do banco de dados hello, em vez no aplicativo hello, simplifica a manutenção e reduz o risco de saudação de erro como a base de código de um aplicativo cresce. 

Usando esses recursos juntos, um aplicativo pode se beneficiar de ganhos de eficiência e economia de custo ao armazenar os dados para vários locatários em Olá mesmo banco de dados de fragmento. Em Olá mesmo tempo, um aplicativo ainda tem Olá flexibilidade toooffer isolado, fragmentos de único locatário para locatários "premium" que necessitam de garantias de desempenho mais rígidas como fragmentos multilocatários não garantem a distribuição de recursos igual entre locatários.  

Em resumo, Olá da biblioteca do cliente do banco de dados Elástico [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) APIs conectar-se automaticamente locatários toohello fragmento corretas banco de dados que contém sua chave de fragmentação (geralmente um "TenantId"). Uma vez conectado, uma política de segurança RLS no banco de dados de saudação garante que os locatários possam acessar somente linhas que contêm seu TenantId. Presume-se que todas as tabelas contêm um tooindicate de coluna TenantId quais linhas pertencem tooeach locatário. 

![Arquitetura de aplicativo de blog][1]

## <a name="download-hello-sample-project"></a>Baixe o projeto de exemplo hello
### <a name="prerequisites"></a>Pré-requisitos
* Usar o Visual Studio (2012 ou superior) 
* Criar três Bancos de Dados SQL do Azure 
* Baixar o projeto de exemplo: [Ferramentas de Banco de Dados Elástico para o SQL do Azure - Fragmentos Multilocatários](http://go.microsoft.com/?linkid=9888163)
  * Preencha as informações de saudação para seus bancos de dados no início de saudação do **Program.cs** 

Este projeto estende Olá um descritos em [Elástico ferramentas de banco de dados do SQL Azure - integração do Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) adicionando suporte para bancos de dados de fragmento de multilocatário. Ele cria um aplicativo de console simples para a criação de blogs e postagens, com quatro locatários e dois fragmentos de multilocatário bancos de dados conforme ilustrado na Olá acima do diagrama. 

Compilar e executar o aplicativo hello. Isso irá inicializar o Gerenciador do mapa de fragmentos de ferramentas de banco de dados Elástico hello e Olá executar testes a seguir: 

1. Usando o Entity Framework e o LINQ, crie um novo blog e exiba todos os blogs para cada locatário
2. Usando o ADO.NET SqlClient, exiba todos os blogs para um locatário
3. Tente tooinsert um blog para Olá locatário errado tooverify que um erro será lançado  

Observe que como RLS ainda não foi habilitado em bancos de dados de fragmento hello, cada um desses testes revela um problema: locatários são toosee capaz de blogs que não pertencem toothem e aplicativo hello não será impedido de inserir um blog para locatário errado hello. Olá restante deste artigo descreve como tooresolve esses problemas impondo locatário isolamento com a RLS. Há duas etapas: 

1. **Camada de aplicativo**: modificar o código do aplicativo hello tooalways conjunto Olá TenantId atual em Olá SESSION_CONTEXT depois de abrir uma conexão. projeto de exemplo Hello já tenha feito isso. 
2. **Camada de dados**: criar uma política de segurança RLS em cada toofilter de banco de dados de fragmento linhas com base em Olá TenantId armazenadas em SESSION_CONTEXT. Você precisará toodo isso para cada um dos seus bancos de dados de fragmento, caso contrário linhas em fragmentos multilocatários não serão filtradas. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Camada de aplicativo da etapa 1): definir TenantId em Olá SESSION_CONTEXT
Depois de conectar tooa fragmento banco de dados usando dados da biblioteca de cliente do banco de dados Elástico Olá que APIs de roteamentos dependentes, aplicativo hello ainda precisa de banco de dados de saudação de tootell quais TenantId está usando essa conexão para que uma política de segurança RLS pode filtrar linhas pertencente tooother locatários. Olá toopass de maneira recomendada essas informações são toostore Olá TenantId atual para essa conexão em Olá [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Observação: como alternativa, você pode usar [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), mas SESSION_CONTEXT é uma opção melhor, pois é mais fácil toouse, retorna nulo por padrão e dá suporte a pares chave-valor.)

### <a name="entity-framework"></a>Entity Framework
Para aplicativos usando o Entity Framework, abordagem mais fácil de saudação é Olá tooset SESSION_CONTEXT em Olá ElasticScaleContext substituir descrito em [roteamento dependente de dados usando EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Antes de retornar conexão Olá orientada por meio do roteamento dependente de dados, criar e executar um SqlCommand que define 'TenantId' em Olá SESSION_CONTEXT toohello shardingKey especificado para essa conexão. Dessa forma, você só precisa toowrite código depois tooset Olá SESSION_CONTEXT. 

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

Agora Olá SESSION_CONTEXT é definido automaticamente com hello especificado TenantId sempre que é invocado ElasticScaleContext: 

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

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
Para aplicativos usando ADO.NET SqlClient hello recomendada abordagem é toocreate uma função de wrapper em torno de ShardMap.OpenConnectionForKey() que define automaticamente 'TenantId' no hello SESSION_CONTEXT toohello corrigir TenantId antes de retornar um conexão. tooensure que sempre é possível definir SESSION_CONTEXT, você só deve abrir as conexões usando essa função de wrapper.

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Etapa 2) Camada de dados: criar política de segurança no nível da linha
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Criar linhas de que cada locatário pode acessar de uma saudação de toofilter de política de segurança
Agora que o aplicativo hello é definir SESSION_CONTEXT com hello TenantId atual antes de consultar, uma política de segurança RLS pode filtrar consultas e excluir linhas que têm um TenantId diferente.  

O RLS é implementado no T-SQL: uma função definida pelo usuário define a lógica de acesso a saudação e uma política de segurança associado a essa função tooany número de tabelas. Para este projeto, função hello simplesmente verificará se Olá aplicativo (em vez de algum outro usuário do SQL) é o banco de dados de toohello conectado, e esse Olá 'TenantId' armazenado em Olá SESSION_CONTEXT corresponde Olá TenantId de uma determinada linha. Um predicado de filtro permitirá linhas que atendem estas condições toopass por filtro Olá para consultas SELECT, UPDATE e DELETE; e um predicado de block impedirá linhas que violam essas condições sejam inseridos ou atualizados. Se não tiver sido definido SESSION_CONTEXT, ela retornará que NULL e nenhuma linha será visível ou a capacidade de toobe inserido. 

tooenable RLS, execute Olá T-SQL a seguir em todos os fragmentos usando o Visual Studio (SSDT), SSMS, ou Olá script do PowerShell incluído no projeto hello (ou se você estiver usando [trabalhos do banco de dados Elástico](sql-database-elastic-jobs-overview.md), você pode usá-lo em execução tooautomate desse T-SQL em todos os fragmentos): 

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
> Para projetos mais complexos que precisam de predicado de saudação tooadd em centenas de tabelas, você pode usar um procedimento armazenado auxiliar que gera automaticamente uma política de segurança adicionando um predicado em todas as tabelas em um esquema. Consulte [tabelas de tooall aplicar segurança de nível de linha - script auxiliar (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Agora se você executar o aplicativo de exemplo hello novamente, locatários serão capaz de toosee somente as linhas que pertencem a toothem. Além disso, o aplicativo hello não é possível inserir linhas que pertencem a tootenants diferente de banco de dados do hello toohello conectado no momento um fragmento e ele não é possível atualizar linhas visíveis toohave um TenantId diferente. Se o aplicativo hello tentativas toodo ou, um DbUpdateException será gerado.

Se você adicionar uma nova tabela posteriormente, simplesmente ALTER Olá a política de segurança e adicione os predicados de filtro e bloqueio na nova tabela de saudação: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Adicionar padrão popular de restrições tooautomatically TenantId para inserções
Você pode colocar um padrão popular de restrição em cada tabela tooautomatically Olá TenantId com hello valor armazenado atualmente em SESSION_CONTEXT ao inserir linhas. Por exemplo: 

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

Agora o aplicativo hello não precisa toospecify um TenantId ao inserir linhas: 

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
> Se você usar restrições padrão para um projeto do Entity Framework, é recomendável que você não incluir coluna de TenantId Olá no seu modelo de dados EF. Isso ocorre porque as consultas de Entity Framework fornecem valores padrão que substituirão as restrições de padrão de saudação criadas no T-SQL que usam SESSION_CONTEXT automaticamente. projeto de exemplo de restrições de padrão de toouse no hello, por exemplo, você deve remover a TenantId do DataClasses.cs (e executar Add-Migration Olá Package Manager Console) e tooensure use T-SQL que Olá campo só existe nas tabelas de banco de dados de saudação. Dessa forma, o EF não fornecerá valores padrão incorretos automaticamente ao inserir dados. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Opcional) Habilitar todas as linhas de uma tooaccess de "superusuário"
Alguns aplicativos podem ser toocreate "superusuário" quem pode acessar todas as linhas, por exemplo, em ordem tooenable relatórios em todos os locatários em todos os fragmentos ou operações de divisão/mesclagem tooperform em fragmentos que envolvem mover linhas de locatário entre bancos de dados. tooenable isso, você deve criar um novo usuário SQL ("superusuário" neste exemplo) em cada banco de dados de fragmento. Em seguida, altere a política de segurança de saudação com uma nova função de predicado que permite que esse usuário tooaccess todas as linhas:

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


### <a name="maintenance"></a>Manutenção 
* **Adicionando novos fragmentos**: você deve executar Olá T-SQL script tooenable RLS em quaisquer novos fragmentos, caso contrário, consultas sobre esses fragmentos não serão filtradas.
* **Adicionando novas tabelas**: você deve adicionar um filtro e bloquear a política de segurança de predicado toohello em todos os fragmentos sempre que uma nova tabela é criada, caso contrário, consultas na nova tabela de saudação não serão filtradas. Isso pode ser automatizado usando um gatilho DDL, conforme descrito em [aplicar segurança de nível de linha toonewly criado automaticamente tabelas (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Resumo
Ferramentas de banco de dados Elástico e segurança em nível de linha podem ser usado tooscale junto camada de dados de um aplicativo com suporte para vários locatários e único locatário fragmentos. Multilocatários fragmentos podem ser usados toostore dados com mais eficiência (principalmente em casos em que um grande número de locatários têm apenas algumas linhas de dados), ao único locatário fragmentos podem ser usados toosupport premium locatários com isolamento e desempenho mais rígida requisitos.  Para obter mais informações, confira [a referência à Segurança em Nível de Linha](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Recursos adicionais
* [O que é um pool elástico do Azure?](sql-database-elastic-pool.md)
* [Escalando horizontalmente com o Banco de Dados SQL do Azure](sql-database-elastic-scale-introduction.md)
* [Padrões de design para aplicativos SaaS multilocatários com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Autenticação em aplicativos multilocatários usando o Azure AD e o OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Aplicativo Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Perguntas e solicitações de recursos
Para dúvidas, entre em contato toous em Olá [Fórum do banco de dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e para solicitações de recurso, adicione-toohello [Fórum de comentários do banco de dados SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


