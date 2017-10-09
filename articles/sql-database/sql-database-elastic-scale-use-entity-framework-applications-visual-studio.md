---
title: "biblioteca de cliente de banco de dados Elástico aaaUsing com o Entity Framework | Microsoft Docs"
description: "Usar a biblioteca de cliente do Banco de Dados Elástico e o Entity Framework para bancos de dados de codificação"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Biblioteca cliente do Banco de Dados Elástico com Entity Framework
Este documento mostra as alterações de saudação em um aplicativo do Entity Framework que são necessária toointegrate com hello [ferramentas de banco de dados Elástico](sql-database-elastic-scale-introduction.md). Olá foco é compor [gerenciamento de mapa do fragmento](sql-database-elastic-scale-shard-map-management.md) e [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) com hello Entity Framework **Code First** abordagem. Olá [código primeiro - novo banco de dados](http://msdn.microsoft.com/data/jj193542.aspx) tutorial de EF serve como exemplo de execução ao longo deste documento. código de exemplo Hello que acompanha este documento é parte das ferramentas de banco de dados Elástico conjunto de amostras Olá exemplos de código do Visual Studio.

## <a name="downloading-and-running-hello-sample-code"></a>Baixando e executando o código de exemplo de hello
código de saudação toodownload para este artigo:

* É necessário o Visual Studio 2012 ou posterior. 
* Baixar Olá [Elástico ferramentas de banco de dados do SQL Azure - exemplo de integração do Entity Framework](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) do MSDN. Descompacte Olá exemplo tooa de local de sua escolha.
* Inicie o Visual Studio. 
* No Visual Studio, selecione Arquivo -> Abrir Projeto/Solução. 
* Em Olá **Abrir projeto** caixa de diálogo, navegue toohello exemplo que você baixou e selecione **EntityFrameworkCodeFirst.sln** tooopen exemplo de hello. 

exemplo de hello toorun, é necessário toocreate três bancos de dados vazios no banco de dados do SQL Azure:

* Banco de dados do Gerenciador do mapa do fragmento
* Banco de dados do fragmento 1
* Banco de dados do fragmento 2

Depois de criar esses bancos de dados, preencha espaços reservados de saudação em **Program.cs** com o nome do seu servidor de banco de dados do Azure SQL, nomes de banco de dados de saudação e seus bancos de dados credenciais tooconnect toohello. Compile a solução Olá no Visual Studio. Visual Studio baixará os pacotes do NuGet Olá necessária para biblioteca de cliente do banco de dados Elástico hello, Entity Framework e Transient Fault handling como parte do processo de compilação de saudação. Certifique-se de que a restauração de pacotes NuGet está habilitada para sua solução. Você pode habilitar essa configuração, o botão direito no arquivo de solução Olá Olá Gerenciador de soluções do Visual Studio. 

## <a name="entity-framework-workflows"></a>Fluxos de trabalho do Entity Framework
Os desenvolvedores do Entity Framework contam com uma saudação quatro tooensure persistência para os objetos de aplicativo e aplicativos de toobuild de fluxos de trabalho a seguir: 

* **Code First (novo banco de dados)**: Olá desenvolvedor EF cria o modelo de Olá no código do aplicativo hello e, em seguida, o EF gera o banco de dados de saudação dele. 
* **Code First (banco de dados existente)**: desenvolvedor Olá permite EF gerar código do aplicativo hello para modelo de saudação do banco de dados existente.
* **Modelo primeiro**: desenvolvedor Olá cria o modelo de saudação no designer EF hello e EF cria Olá de banco de dados do modelo de saudação.
* **Banco de dados primeiro**: desenvolvedor Olá usa EF ferramentas tooinfer modelo de saudação do banco de dados existente. 

Todas essas abordagens dependem tootransparently de classe DbContext Olá gerenciam conexões de banco de dados e esquema de banco de dados para um aplicativo. Como abordaremos em mais detalhes posteriormente neste documento hello, construtores diferentes na classe base do hello DbContext permitem para diferentes níveis de controle sobre a criação de conexão, o criação de inicialização e o esquema de banco de dados. Desafios são provenientes principalmente de fato Olá gerenciamento de conexão de banco de dados de saudação fornecido pelo EF interseção com recursos de gerenciamento de conexão Olá Olá dados dependentes de interfaces de roteamento fornecidas pela biblioteca de cliente do banco de dados Elástico hello. 

## <a name="elastic-database-tools-assumptions"></a>Suposições sobre ferramentas de banco de dados elástico
Para obter definições de termos, consulte o [Glossário de ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-glossary.md).

Com a biblioteca de cliente de banco de dados elástico, você define partições dos seus dados de aplicativo chamados shardlets. Shardlets são identificados por uma chave de fragmentação e são mapeadas toospecific bancos de dados. Um aplicativo pode ter tantos bancos de dados conforme necessário e distribuir Olá shardlets tooprovide suficiente capacidade ou desempenho, considerando os requisitos de negócios atual. mapeamento de saudação de bancos de dados de toohello de valores de chave fragmentação é armazenado por um mapa do fragmento fornecido pelo cliente de banco de dados Elástico Olá APIs. Chamamos essa funcionalidade de **Gerenciamento de Mapa de Fragmentos**ou SMM (abreviada do inglês: Shard Map Management). mapa do fragmento Olá também serve como agente de saudação de conexões de banco de dados para solicitações que contêm uma chave de fragmentação. Nós nos referimos a funcionalidade de toothis como **roteamento dependente de dados**. 

Gerenciador do mapa de fragmentos Olá protege os usuários contra modos de exibição inconsistente em dados de shardlet que podem ocorrer quando as operações de gerenciamento de shardlet simultâneas (como realocando dados de um fragmento tooanother) estão ocorrendo. toodo Olá assim, mapas de fragmento gerenciados pelo Olá biblioteca broker Olá banco de dados conexões de cliente para um aplicativo. Isso permite kill do hello fragmento mapa funcionalidade tooautomatically uma conexão de banco de dados quando as operações de gerenciamento de fragmento podem afetar Olá shardlet que foi criado para a conexão de saudação. Essa abordagem deve toointegrate com algumas das funcionalidades do EF, como a criação de novas conexões de um um toocheck existente para a existência de banco de dados. Em geral, nosso Observação foi que construtores de DbContext padrão Olá só funcionam de forma confiável para conexões de banco de dados fechado que podem ser clonadas com segurança para o trabalho EF. em vez disso, o princípio de design de saudação do banco de dados Elástico é tooonly broker aberto conexões. Alguém pode pensar que fechar uma conexão orientada por biblioteca de saudação do cliente antes de enviar a ele pela toohello EF DbContext pode resolver esse problema. No entanto, ao fechar conexão hello e confiar no EF toore-open, um foregoes Olá validação e verificações de consistência executadas pela biblioteca de saudação. funcionalidade de migrações Olá no EF, no entanto, usa Olá de toomanage essas conexões subjacentes do esquema de banco de dados de forma transparente toohello aplicativo. Idealmente, podemos deseja tooretain e combinar todos esses recursos de biblioteca de cliente do banco de dados Elástico hello e EF no hello mesmo aplicativo. Olá seção a seguir descreve essas propriedades e os requisitos mais detalhadamente. 

## <a name="requirements"></a>Requisitos
Ao trabalhar com a biblioteca de cliente do banco de dados Elástico hello e APIs do Entity Framework, queremos Olá tooretain propriedades a seguir: 

* **Expansão**: tooadd ou remover bancos de dados Olá da camada de dados do aplicativo fragmentados Olá conforme necessário para atender às demandas de capacidade de saudação do aplicativo hello. Isso significa controle sobre a criação de Olá Olá e a exclusão de bancos de dados e usando Olá banco de dados Elástico fragmento mapa manager APIs toomanage bancos de dados e mapeamentos de shardlets. 
* **Consistência**: aplicativo hello emprega fragmentação e usa Olá recursos de roteamento dependente de dados da biblioteca de cliente de saudação. tooavoid corrupção ou resultados da consulta incorreta, as conexões são orientadas por meio do Gerenciador do mapa de fragmentos hello. Isso também mantém a consistência e a validação.
* **Code First**: tooretain conveniência de saudação do paradigma de primeiro do EF código. No Code First, as classes no aplicativo hello são mapeadas transparentemente toohello subjacente estruturas de banco de dados. código do aplicativo Hello interage com DbSets que mascarar a maioria dos aspectos envolvidos em Olá subjacente de processamento do banco de dados.
* **Esquema**: o Entity Framework lida com a criação de esquema do banco de dados inicial e com a evolução de esquemas subsequentes por meio de migrações. Mantendo esses recursos, é fácil Olá dados evolui adaptar seu aplicativo. 

Olá diretrizes a seguir instrui como toosatisfy esses requisitos para Code First aplicativos usando as ferramentas de banco de dados Elástico. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Roteamento dependente de dados usando o EF DbContext
Conexões de banco de dados com o Entity Framework são normalmente gerenciadas por meio de subclasses do **DbContext**. Crie essas subclasses derivando por meio do **DbContext**. Isso é onde você define o **DbSets** que implementam a coleções de saudação feito pelo banco de dados de objetos CLR para seu aplicativo. No contexto de saudação do roteamento dependente de dados, é possível identificar várias propriedades úteis que não necessariamente mantêm para outros cenários de aplicativo EF código primeiro: 

* banco de dados de saudação já existe e foi registrado no mapa de fragmento de banco de dados Elástico hello. 
* esquema de saudação do aplicativo hello já foi implantado toohello banco de dados (explicado abaixo). 
* Dependente de dados roteamento conexões toohello banco de dados são orientadas pelo mapa do fragmento hello. 

toointegrate **DbContexts** com roteamento dependente de dados de expansão:

1. Criar conexões de banco de dados físico por meio das interfaces de cliente do banco de dados Elástico saudação do Gerenciador do mapa de fragmento Olá, 
2. Encapsular conexão Olá com hello **DbContext** subclasse
3. Passar conexão Olá para baixo para Olá **DbContext** base classes tooensure todo o processamento Olá no lado do EF Olá também acontece. 

saudação de exemplo de código a seguir ilustra essa abordagem. (Esse código também é em Olá que acompanha o projeto do Visual Studio)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Principais pontos
* Um novo construtor substitui o construtor padrão de saudação de subclasse de DbContext Olá 
* Olá novo construtor usa argumentos Olá que são necessários para roteamento dependente de dados por meio da biblioteca de cliente do banco de dados Elástico:
  
  * tooaccess de mapa do fragmento Olá Olá interfaces de roteamento dependente de dados,
  * Olá fragmentação tooidentify chave Olá shardlet,
  * uma cadeia de caracteres de conexão com credenciais Olá para fragmento Olá toohello conexão, roteamento dependente de dados. 
* Construtor de classe base Olá chamada toohello leva um desvio em um método estático que executa todas as etapas de saudação necessários para roteamento dependente de dados. 
  
  * Ele usa a chamada de OpenConnectionForKey Olá das interfaces de cliente do banco de dados Elástico Olá no tooestablish de mapa de fragmento Olá uma conexão aberta.
  * mapa do fragmento Olá cria fragmento toohello do hello conexão aberta que contém o shardlet Olá para Olá recebe a chave de fragmentação.
  * Essa conexão aberta é passado toohello back construtor da classe base de DbContext tooindicate essa conexão é toobe usado pelo EF em vez de deixar que o EF criar uma nova conexão automaticamente. Esta conexão de saudação de maneira foi marcada pelo cliente de banco de dados Elástico Olá API para que ele pode garantir a consistência em operações de gerenciamento de mapa do fragmento.

Use Olá novo construtor para a subclasse DbContext em vez do construtor do saudação padrão em seu código. Aqui está um exemplo: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

construtor new Olá abre o fragmento de toohello de conexão de saudação que armazena dados de saudação do shardlet Olá identificado pelo valor de saudação do **tenantid1**. Olá código Olá **usando** bloco permanece inalterado tooaccess Olá **DbSet** para blogs usando EF no fragmento Olá para **tenantid1**. Isso altera a semântica para código Olá Olá usando o bloco de modo que todas as operações de banco de dados agora estão no escopo toohello um fragmento onde **tenantid1** é mantida. Por exemplo, uma consulta LINQ sobre Olá blogs **DbSet** seriam retornar apenas os blogs armazenado no fragmento de saudação atual, mas não Olá aqueles armazenados em outros fragmentos.  

#### <a name="transient-faults-handling"></a>Tratamento de falhas transitórias
Olá Microsoft Patterns & Practices equipe Olá publicado [Olá Transient Fault Handling Application Block](https://msdn.microsoft.com/library/dn440719.aspx). Olá biblioteca é usada com a biblioteca de cliente de escala elástica em combinação com o EF. No entanto, certifique-se de que qualquer exceção transitória retorna tooa local onde podemos garantir que esse construtor novo hello está sendo usado após uma falha temporária para que qualquer nova tentativa de conexão é feita usando construtores Olá que é ter ajustada. Caso contrário, um toohello de conexão correta fragmento não é garantido e não há nenhuma garantia conexão Olá é mantido como alterações de mapa do fragmento toohello ocorrer. 

Olá exemplo de código a seguir ilustra como uma política de repetição SQL pode ser usada em torno de saudação novo **DbContext** construtores subclasse: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** Olá código acima é definido como um **SqlDatabaseTransientErrorDetectionStrategy** com uma contagem de repetição de 10 e 5 segundos tempo de espera entre as repetições. Essa abordagem é semelhante orientação toohello EF e transações iniciadas pelo usuário (consulte [limitações com estratégias de repetição de execução (EF6 em diante)](http://msdn.microsoft.com/data/dn307226). Duas situações exigem que o programa aplicativo hello controla Olá escopo toowhich Olá exceção transitória retorna: tooeither reabrir transação hello, ou (conforme mostrado) recriar o contexto de saudação do construtor adequada de saudação usa Olá banco de dados Elástico biblioteca de cliente.

Olá necessidade toocontrol onde exceções transitórias, conduza-no escopo também impede que use Olá internos Olá **SqlAzureExecutionStrategy** que acompanha o EF. **SqlAzureExecutionStrategy** seria reabrir uma conexão, mas não use **OpenConnectionForKey** e, portanto, ignorar todas as validações de saudação que é executada como parte da saudação **OpenConnectionForKey** chamar. Em vez disso, o exemplo de código de saudação usa internas Olá **DefaultExecutionStrategy** que também vem com EF. Ao contrário do muito**SqlAzureExecutionStrategy**, ele funciona corretamente em combinação com a política de repetição de saudação do tratamento de falhas transitórias. política de execução de saudação é definida no hello **ElasticScaleDbConfiguration** classe. Observe que isso decidimos não toouse **DefaultSqlExecutionStrategy** desde que sugere toouse **SqlAzureExecutionStrategy** se ocorrerem exceções transitórias - o que poderia levar comportamento toowrong conforme discutido. Para obter mais informações sobre políticas de repetição diferente hello e EF, consulte [resiliência de Conexão no EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>O construtor reescreve
exemplos de código acima Hello ilustram padrão Olá construtor regrava necessário para seu aplicativo, dados de pedidos toouse dependentes de roteamento com saudação do Entity Framework. a tabela a seguir de saudação generaliza construtores de tooother essa abordagem. 

| Construtor atual | Construtor regravado para dados | Construtor base | Observações |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |conexão Olá precisa toobe uma função de mapa do fragmento hello e chave de roteamento do hello dependente de dados. Você precisa de criação de conexão automática tooby passa por EF e em vez disso, use conexão de Olá Olá fragmento mapa toobroker. |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |conexão de saudação é uma função de mapa do fragmento hello e chave de roteamento do hello dependente de dados. Uma cadeia de caracteres de nome ou conexão de banco de dados fixa não funcionará conforme elas validação desviar pelo mapa do fragmento hello. |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |conexão Hello serão é criada para Olá dado chave de fragmentação e mapa de fragmento com saudação do modelo fornecido. modelo compilado Hello será passado na toohello c'tor de base. |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |conexão Olá precisa toobe inferido do mapa do fragmento hello e chave de saudação. Ele não pode ser fornecido como uma entrada (a menos que essa entrada já estava usando o mapa do fragmento hello e a chave de saudação). Olá booliano será passada na. |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |conexão Olá precisa toobe inferido do mapa do fragmento hello e chave de saudação. Ele não pode ser fornecido como uma entrada (a menos que essa entrada foi usando o mapa do fragmento hello e a chave de saudação). modelo compilado Hello será passado na. |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |construtor new Olá precisa tooensure qualquer conexão no hello que ObjectContext passado como entrada é redirecionados tooa conexão gerenciado pelo escala elástica. Uma discussão detalhada da ObjectContexts está além do escopo deste documento hello. |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |conexão Olá precisa toobe inferido do mapa do fragmento hello e chave de saudação. conexão de saudação não pode ser fornecido como uma entrada (a menos que essa entrada já estava usando o mapa do fragmento hello e a chave de saudação). Modelo e Boolean são passadas no construtor de classe base toohello. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Implantação de esquema de fragmento por meio de migrações do EF
Gerenciamento automático de esquema é uma conveniência fornecida pelo saudação do Entity Framework. No contexto de saudação de aplicativos usando as ferramentas de banco de dados Elástico, queremos tooretain fragmentos de toonewly criado esse recurso tooautomatically provisionar Olá esquema quando os bancos de dados são adicionados aplicativos fragmentados toohello. caso de uso primário de saudação é tooincrease capacidade na camada de dados Olá aplicativos fragmentados usando EF. Depender de recursos do EF para gerenciamento de esquema reduz o esforço de administração de banco de dados de saudação com um aplicativo fragmentado baseado no EF. 

A implantação de esquema por meio de migrações EF funciona melhor em **conexões não abertas**. Por outro lado, esse é o cenário de toohello para roteamento dependente de dados que se baseia em conexão Olá aberto fornecido pela API do cliente do banco de dados Elástico hello. Outra diferença é o requisito de consistência Olá: ao consistência tooensure desejável para tooprotect de conexões roteamento dependente de todos os dados em relação a manipulação de mapa do fragmento simultâneas, não é um problema com o esquema inicial implantação tooa novo banco de dados que tem ainda não foi registrado no mapa do fragmento Olá e ainda não foi alocado toohold shardlets. Portanto, podemos contar com conexões de banco de dados regulares para este cenários, como roteamento de toodata dependente contrário.  

Isso leva tooan abordagem em que a implantação de esquema por meio de migrações EF está acoplada ao registro de saudação do novo banco de dados de saudação como um fragmento no mapa do fragmento do aplicativo hello. Isso se baseia em Olá pré-requisitos a seguir: 

* banco de dados de saudação já foi criado. 
* banco de dados de saudação está vazio - ele contém nenhum esquema de usuário e nenhum dado de usuário.
* banco de dados de saudação ainda não pode ser acessado por meio de APIs de cliente de banco de dados Elástico Olá para roteamento dependente de dados. 

Com esses pré-requisitos estabelecidos, podemos criar uma expressão não aberto **SqlConnection** tookick off migrações EF para implantação de esquema. saudação de exemplo de código a seguir ilustra essa abordagem. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


Este exemplo mostra o método hello **RegisterNewShard** registra Olá fragmento no mapa do fragmento hello, implanta o esquema de saudação por meio de migrações EF e armazena um mapeamento de um fragmento de toohello chave de fragmentação. Ele se baseia em um construtor de saudação **DbContext** subclasse (**ElasticScaleContext** no exemplo hello) que usa uma cadeia de caracteres de conexão SQL como entrada. código de saudação desse construtor é direta, como Olá mostrado no exemplo a seguir: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Um pode ter usado a versão Olá Olá construtor herdada da classe base hello. Mas Olá código necessidades tooensure que Olá inicializador de padrão de EF é usado na conexão. Olá, portanto, desvio curto no método estático hello antes de chamar o construtor da classe base Olá com a cadeia de caracteres de conexão de saudação. Observe que deve executar o registro de saudação de fragmentos em um tooensure aplicativos diferentes de domínio ou o processo de configurações de inicializador Olá para o EF não entrem em conflito. 

## <a name="limitations"></a>Limitações
abordagens de saudação descritas neste documento envolvem algumas limitações: 

* Aplicativos de EF que usam **LocalDb** primeiro precisa toomigrate tooa regulares do SQL Server banco de dados antes de usar a biblioteca de cliente do banco de dados Elástico. Não é possível escalar verticalmente um aplicativo por meio de fragmentação com Escala Elástica com o **LocalDb**. Observe que o desenvolvimento ainda pode usar **LocalDb**. 
* Qualquer aplicativo toohello alterações que implicam em alterações de esquema de banco de dados necessário toogo por meio de migrações EF em todos os fragmentos. código de exemplo Hello para este documento demonstra como toodo isso. Considere o uso de atualização de banco de dados com um tooiterate de parâmetro ConnectionString sobre todos os fragmentos; ou extrair Olá T-SQL script para Olá pendentes migração usando o Update-Database com hello - opção de Script e aplicar os fragmentos de tooyour script hello T-SQL.  
* Recebe uma solicitação, presume-se que todo o processamento do banco de dados está contida em um único fragmento conforme identificado pela chave de fragmentação Olá fornecida por solicitação hello. No entanto, esse pressuposto nem sempre é verdadeiro. Por exemplo, quando não é possível toomake uma chave de fragmentação disponível. tooaddress, Olá biblioteca de cliente fornece Olá **MultiShardQuery** classe que implementa uma abstração de conexão para consultas em vários fragmentos. Aprendizado Olá toouse **MultiShardQuery** em combinação com EF está além do escopo deste documento Olá

## <a name="conclusion"></a>Conclusão
Etapas Olá descritas neste documento, aplicativos de EF podem usar recursos da biblioteca de cliente do banco de dados Elástico Olá para dados dependentes de roteamento pela refatoração construtores de saudação **DbContext** subclasses usadas em Olá EF aplicativo. Essa alteração na Olá limites necessária toothose locais onde **DbContext** classes já existem. Além disso, os aplicativos de EF podem continuar toobenefit de implantação automática de esquema combinando etapas Olá que invocam Olá necessário EF migrações com registro Olá dos mapeamentos no mapa do fragmento hello e novos fragmentos. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
