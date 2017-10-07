---
title: aaaData dependente de roteamento com o banco de dados do SQL Azure | Microsoft Docs
description: "Como toouse Olá classe ShardMapManager em aplicativos .NET para roteamento, um recurso de bancos de dados fragmentados no banco de dados do SQL Azure dependente de dados"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="c59f5-103">Roteamento dependente de dados</span><span class="sxs-lookup"><span data-stu-id="c59f5-103">Data dependent routing</span></span>
<span data-ttu-id="c59f5-104">**Roteamento dependente de dados** Olá capacidade toouse Olá dados em um consulta tooroute Olá solicitação tooan banco de dados apropriado.</span><span class="sxs-lookup"><span data-stu-id="c59f5-104">**Data dependent routing** is hello ability toouse hello data in a query tooroute hello request tooan appropriate database.</span></span> <span data-ttu-id="c59f5-105">Trata-se de um padrão fundamental ao trabalhar com bancos de dados fragmentados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="c59f5-106">contexto de solicitação Olá também pode ser usado tooroute solicitação de hello, especialmente se a chave de fragmentação Olá não é parte da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c59f5-106">hello request context may also be used tooroute hello request, especially if hello sharding key is not part of hello query.</span></span> <span data-ttu-id="c59f5-107">Cada consulta específica ou a transação em um aplicativo usando o encaminhamento dependente de dados é restrito tooaccessing um único banco de dados por solicitação.</span><span class="sxs-lookup"><span data-stu-id="c59f5-107">Each specific query or transaction in an application using data dependent routing is restricted tooaccessing a single database per request.</span></span> <span data-ttu-id="c59f5-108">Para as ferramentas do hello Elástico de banco de dados de SQL do Azure, este roteamento é feito com hello  **[ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  em aplicativos do ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="c59f5-108">For hello Azure SQL Database Elastic tools, this routing is accomplished with hello **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="c59f5-109">aplicativo Hello não precisa tootrack várias cadeias de caracteres de conexão ou locais de banco de dados associados a diferentes subconjuntos de dados no ambiente de saudação fragmentados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-109">hello application does not need tootrack various connection strings or DB locations associated with different slices of data in hello sharded environment.</span></span> <span data-ttu-id="c59f5-110">Em vez disso, Olá [Gerenciador do mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md) abre conexões toohello correto bancos de dados quando necessário, com base nos dados de saudação no mapa do fragmento hello e valor de saudação da chave de fragmentação Olá Olá destino da solicitação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c59f5-110">Instead, hello [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections toohello correct databases when needed, based on hello data in hello shard map and hello value of hello sharding key that is hello target of hello application’s request.</span></span> <span data-ttu-id="c59f5-111">chave Olá normalmente é hello *customer_id*, *tenant_id*, *date_key*, ou outro identificador específico que é um parâmetro fundamental da solicitação de banco de dados de saudação).</span><span class="sxs-lookup"><span data-stu-id="c59f5-111">hello key is typically hello *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of hello database request).</span></span> 

<span data-ttu-id="c59f5-112">Para obter mais informações, consulte [Dimensionamento do SQL Server com roteamento dependente de dados](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="c59f5-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-hello-client-library"></a><span data-ttu-id="c59f5-113">Baixar a biblioteca de saudação do cliente</span><span class="sxs-lookup"><span data-stu-id="c59f5-113">Download hello client library</span></span>
<span data-ttu-id="c59f5-114">classe tooget Olá Olá install [biblioteca de cliente de banco de dados Elástico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="c59f5-114">tooget hello class, install hello [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="c59f5-115">Usando um ShardMapManager em um aplicativo de roteamento dependente de dados</span><span class="sxs-lookup"><span data-stu-id="c59f5-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="c59f5-116">Aplicativos devem instanciar Olá **ShardMapManager** durante a inicialização, usando a chamada de fábrica Olá  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="c59f5-116">Applications should instantiate hello **ShardMapManager** during initialization, using hello factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="c59f5-117">Neste exemplo, tanto um **ShardMapManager** quanto um **ShardMap** específico que ele contém são inicializados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="c59f5-118">Este exemplo mostra Olá GetSqlShardMapManager e [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) métodos.</span><span class="sxs-lookup"><span data-stu-id="c59f5-118">This example shows hello GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a><span data-ttu-id="c59f5-119">Usar credenciais de privilégio mais baixas possível para obtenção de mapa do fragmento Olá</span><span class="sxs-lookup"><span data-stu-id="c59f5-119">Use lowest privilege credentials possible for getting hello shard map</span></span>
<span data-ttu-id="c59f5-120">Se um aplicativo não está manipulando o mapa do fragmento Olá em si, credenciais Olá usadas no método de fábrica Olá devem ter permissões de somente leitura apenas na Olá **Global mapa do fragmento** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-120">If an application is not manipulating hello shard map itself, hello credentials used in hello factory method should have just read-only permissions on hello **Global Shard Map** database.</span></span> <span data-ttu-id="c59f5-121">Essas credenciais são normalmente diferentes do Gerenciador do mapa de credenciais usadas tooopen conexões toohello fragmentos.</span><span class="sxs-lookup"><span data-stu-id="c59f5-121">These credentials are typically different from credentials used tooopen connections toohello shard map manager.</span></span> <span data-ttu-id="c59f5-122">Consulte também [as credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="c59f5-122">See also [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-hello-openconnectionforkey-method"></a><span data-ttu-id="c59f5-123">Chame o método de OpenConnectionForKey hello</span><span class="sxs-lookup"><span data-stu-id="c59f5-123">Call hello OpenConnectionForKey method</span></span>
<span data-ttu-id="c59f5-124">Olá  **[ShardMap.OpenConnectionForKey método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  retorna uma conexão ADO.Net pronto para emitir comandos toohello banco de dados apropriado com base no valor Olá Olá **chave**parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c59f5-124">hello **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands toohello appropriate database based on hello value of hello **key** parameter.</span></span> <span data-ttu-id="c59f5-125">Informações de fragmento é armazenado em cache no aplicativo hello por Olá **ShardMapManager**, portanto, essas solicitações normalmente não envolvem uma pesquisa de banco de dados em Olá **Global mapa do fragmento** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-125">Shard information is cached in hello application by hello **ShardMapManager**, so these requests do not typically involve a database lookup against hello **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="c59f5-126">Olá **chave** parâmetro é usado como uma chave de pesquisa em Olá fragmento mapa toodetermine Olá banco de dados apropriado para a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c59f5-126">hello **key** parameter is used as a lookup key into hello shard map toodetermine hello appropriate database for hello request.</span></span> 
* <span data-ttu-id="c59f5-127">Olá **connectionString** é toopass usadas somente credenciais de usuário de saudação para conexão Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="c59f5-127">hello **connectionString** is used toopass only hello user credentials for hello desired connection.</span></span> <span data-ttu-id="c59f5-128">Nenhum nome de banco de dados ou o nome do servidor estão incluídos neste *connectionString* desde que o método hello determinará banco de dados de saudação e servidor usando Olá **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="c59f5-128">No database name or server name are included in this *connectionString* since hello method will determine hello database and server using hello **ShardMap**.</span></span> 
* <span data-ttu-id="c59f5-129">Olá  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  deve ser definido muito**ConnectionOptions.Validate** se um ambiente em que mapeia o fragmento pode mudar e linhas podem mover bancos de dados de tooother como um resultado de operações de divisão ou mesclagem.</span><span class="sxs-lookup"><span data-stu-id="c59f5-129">hello **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set too**ConnectionOptions.Validate** if an environment where shard maps may change and rows may move tooother databases as a result of split or merge operations.</span></span> <span data-ttu-id="c59f5-130">Isso envolve um mapa de fragmento local toohello breve de consulta no banco de dados do hello destino (não toohello global fragmento map) antes da conexão Olá é entregue toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c59f5-130">This involves a brief query toohello local shard map on hello target database (not toohello global shard map) before hello connection is delivered toohello application.</span></span> 

<span data-ttu-id="c59f5-131">Se a validação de saudação de mapa do fragmento local Olá falhar (indicando que o cache de saudação está incorreta), Olá Gerenciador do mapa de fragmentos consultará Olá fragmento global mapa tooobtain Olá novo valor correto para pesquisa de Olá, atualizar o cache de Olá e como obter e retornar Olá conexão de banco de dados apropriado.</span><span class="sxs-lookup"><span data-stu-id="c59f5-131">If hello validation against hello local shard map fails (indicating that hello cache is incorrect), hello Shard Map Manager will query hello global shard map tooobtain hello new correct value for hello lookup, update hello cache, and obtain and return hello appropriate database connection.</span></span> 

<span data-ttu-id="c59f5-132">Use **ConnectionOptions.None** somente quando as alterações de mapeamento de fragmentos não são esperadas enquanto um aplicativo estiver online.</span><span class="sxs-lookup"><span data-stu-id="c59f5-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="c59f5-133">Nesse caso, os valores hello armazenado em cache podem pressupor tooalways estejam corretas e banco de dados do hello validação de ida e volta extra chamada toohello destino pode ser ignorado com segurança.</span><span class="sxs-lookup"><span data-stu-id="c59f5-133">In that case, hello cached values can be assumed tooalways be correct, and hello extra round-trip validation call toohello target database can be safely skipped.</span></span> <span data-ttu-id="c59f5-134">Isso reduz o tráfego de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-134">That reduces database traffic.</span></span> <span data-ttu-id="c59f5-135">Olá **connectionOptions** também pode ser definido por meio de um valor em uma tooindicate do arquivo de configuração, se as alterações de fragmentação são esperadas ou não durante um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="c59f5-135">hello **connectionOptions** may also be set via a value in a configuration file tooindicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="c59f5-136">Este exemplo usa o valor de saudação de uma chave de inteiro **CustomerID**usando um **ShardMap** objeto chamado **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="c59f5-136">This example uses hello value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="c59f5-137">Olá **OpenConnectionForKey** método retorna um nova conexão já aberta toohello banco de dados correto.</span><span class="sxs-lookup"><span data-stu-id="c59f5-137">hello **OpenConnectionForKey** method returns a new already-open connection toohello correct database.</span></span> <span data-ttu-id="c59f5-138">Conexões utilizados dessa forma ainda se beneficiar do pool de conexões do ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="c59f5-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="c59f5-139">Como as transações e solicitações podem ser atendidas por um fragmento por vez, isso deve ser Olá única modificação necessária em um aplicativo já usando o ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="c59f5-139">As long as transactions and requests can be satisfied by one shard at a time, this should be hello only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="c59f5-140">Olá  **[OpenConnectionForKeyAsync método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  também está disponível se seu aplicativo usar a programação assíncrona com o ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="c59f5-140">hello **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="c59f5-141">Seu comportamento é dados saudação dependentes de roteamento equivalente do ADO. Do NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  método.</span><span class="sxs-lookup"><span data-stu-id="c59f5-141">Its behavior is hello data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="c59f5-142">Integrando a manipulação de falhas transitórias</span><span class="sxs-lookup"><span data-stu-id="c59f5-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="c59f5-143">Uma prática recomendada no desenvolvimento de aplicativos de acesso de dados na nuvem Olá é tooensure que falhas transitórias são detectadas por aplicativo hello e que operações de saudação são repetidas várias vezes antes de gerar um erro.</span><span class="sxs-lookup"><span data-stu-id="c59f5-143">A best practice in developing data access applications in hello cloud is tooensure that transient faults are caught by hello app, and that hello operations are retried several times before throwing an error.</span></span> <span data-ttu-id="c59f5-144">O tratamento de falha transitória para aplicativos em nuvem é discutido em [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="c59f5-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="c59f5-145">Tratamento de falhas transitórias pode coexistir, naturalmente, com padrão de saudação encaminhamento dependente de dados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-145">Transient fault handling can coexist naturally with hello Data Dependent Routing pattern.</span></span> <span data-ttu-id="c59f5-146">Olá, requisito de chave é tooretry Olá inteiro de dados acesso solicitação incluindo Olá **usando** bloco que obteve a conexão de roteamento do hello dependente de dados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-146">hello key requirement is tooretry hello entire data access request including hello **using** block that obtained hello data-dependent routing connection.</span></span> <span data-ttu-id="c59f5-147">exemplo Hello acima poderia ser reescrito da seguinte maneira (Observe a alteração realçada).</span><span class="sxs-lookup"><span data-stu-id="c59f5-147">hello example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="c59f5-148">Exemplo – roteamento com falhas transitórias manipulação dependentes dos dados</span><span class="sxs-lookup"><span data-stu-id="c59f5-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="c59f5-149">Pacotes de tratamento de falhas transitórias tooimplement necessários são baixados automaticamente quando você cria o aplicativo de exemplo hello Elástico de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c59f5-149">Packages necessary tooimplement transient fault handling are downloaded automatically when you build hello elastic database sample application.</span></span> <span data-ttu-id="c59f5-150">Pacotes também estão disponíveis separadamente na [Biblioteca Corporativa - Bloco de aplicativo de tratamento de falha transitória](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="c59f5-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="c59f5-151">Use a versão 6.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c59f5-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="c59f5-152">Consistência transacional</span><span class="sxs-lookup"><span data-stu-id="c59f5-152">Transactional consistency</span></span>
<span data-ttu-id="c59f5-153">Propriedades transacionais estão garantidas para todos os fragmentos de tooa locais de operações.</span><span class="sxs-lookup"><span data-stu-id="c59f5-153">Transactional properties are guaranteed for all operations local tooa shard.</span></span> <span data-ttu-id="c59f5-154">Por exemplo, transações enviadas por meio de roteamento dependente de dados execute no escopo de saudação de fragmento de destino Olá para conexão hello.</span><span class="sxs-lookup"><span data-stu-id="c59f5-154">For example, transactions submitted through data-dependent routing execute within hello scope of hello target shard for hello connection.</span></span> <span data-ttu-id="c59f5-155">Neste momento, não há nenhum recurso fornecido para inscrever-se várias conexões em uma transação e, portanto, não há nenhuma garantia transacional para operações executadas pelos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="c59f5-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c59f5-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c59f5-156">Next steps</span></span>
<span data-ttu-id="c59f5-157">toodetach um fragmento ou tooreattach um fragmento, consulte [usando problemas de mapa de fragmento Olá RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="c59f5-157">toodetach a shard, or tooreattach a shard, see [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

