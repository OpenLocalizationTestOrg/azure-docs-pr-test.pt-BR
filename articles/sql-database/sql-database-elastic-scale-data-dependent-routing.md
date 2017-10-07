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
# <a name="data-dependent-routing"></a>Roteamento dependente de dados
**Roteamento dependente de dados** Olá capacidade toouse Olá dados em um consulta tooroute Olá solicitação tooan banco de dados apropriado. Trata-se de um padrão fundamental ao trabalhar com bancos de dados fragmentados. contexto de solicitação Olá também pode ser usado tooroute solicitação de hello, especialmente se a chave de fragmentação Olá não é parte da consulta de saudação. Cada consulta específica ou a transação em um aplicativo usando o encaminhamento dependente de dados é restrito tooaccessing um único banco de dados por solicitação. Para as ferramentas do hello Elástico de banco de dados de SQL do Azure, este roteamento é feito com hello  **[ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  em aplicativos do ADO.NET.

aplicativo Hello não precisa tootrack várias cadeias de caracteres de conexão ou locais de banco de dados associados a diferentes subconjuntos de dados no ambiente de saudação fragmentados. Em vez disso, Olá [Gerenciador do mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md) abre conexões toohello correto bancos de dados quando necessário, com base nos dados de saudação no mapa do fragmento hello e valor de saudação da chave de fragmentação Olá Olá destino da solicitação do aplicativo hello. chave Olá normalmente é hello *customer_id*, *tenant_id*, *date_key*, ou outro identificador específico que é um parâmetro fundamental da solicitação de banco de dados de saudação). 

Para obter mais informações, consulte [Dimensionamento do SQL Server com roteamento dependente de dados](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-hello-client-library"></a>Baixar a biblioteca de saudação do cliente
classe tooget Olá Olá install [biblioteca de cliente de banco de dados Elástico](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Usando um ShardMapManager em um aplicativo de roteamento dependente de dados
Aplicativos devem instanciar Olá **ShardMapManager** durante a inicialização, usando a chamada de fábrica Olá  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. Neste exemplo, tanto um **ShardMapManager** quanto um **ShardMap** específico que ele contém são inicializados. Este exemplo mostra Olá GetSqlShardMapManager e [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) métodos.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Usar credenciais de privilégio mais baixas possível para obtenção de mapa do fragmento Olá
Se um aplicativo não está manipulando o mapa do fragmento Olá em si, credenciais Olá usadas no método de fábrica Olá devem ter permissões de somente leitura apenas na Olá **Global mapa do fragmento** banco de dados. Essas credenciais são normalmente diferentes do Gerenciador do mapa de credenciais usadas tooopen conexões toohello fragmentos. Consulte também [as credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Chame o método de OpenConnectionForKey hello
Olá  **[ShardMap.OpenConnectionForKey método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  retorna uma conexão ADO.Net pronto para emitir comandos toohello banco de dados apropriado com base no valor Olá Olá **chave**parâmetro. Informações de fragmento é armazenado em cache no aplicativo hello por Olá **ShardMapManager**, portanto, essas solicitações normalmente não envolvem uma pesquisa de banco de dados em Olá **Global mapa do fragmento** banco de dados. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Olá **chave** parâmetro é usado como uma chave de pesquisa em Olá fragmento mapa toodetermine Olá banco de dados apropriado para a solicitação de saudação. 
* Olá **connectionString** é toopass usadas somente credenciais de usuário de saudação para conexão Olá desejado. Nenhum nome de banco de dados ou o nome do servidor estão incluídos neste *connectionString* desde que o método hello determinará banco de dados de saudação e servidor usando Olá **ShardMap**. 
* Olá  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  deve ser definido muito**ConnectionOptions.Validate** se um ambiente em que mapeia o fragmento pode mudar e linhas podem mover bancos de dados de tooother como um resultado de operações de divisão ou mesclagem. Isso envolve um mapa de fragmento local toohello breve de consulta no banco de dados do hello destino (não toohello global fragmento map) antes da conexão Olá é entregue toohello aplicativo. 

Se a validação de saudação de mapa do fragmento local Olá falhar (indicando que o cache de saudação está incorreta), Olá Gerenciador do mapa de fragmentos consultará Olá fragmento global mapa tooobtain Olá novo valor correto para pesquisa de Olá, atualizar o cache de Olá e como obter e retornar Olá conexão de banco de dados apropriado. 

Use **ConnectionOptions.None** somente quando as alterações de mapeamento de fragmentos não são esperadas enquanto um aplicativo estiver online. Nesse caso, os valores hello armazenado em cache podem pressupor tooalways estejam corretas e banco de dados do hello validação de ida e volta extra chamada toohello destino pode ser ignorado com segurança. Isso reduz o tráfego de banco de dados. Olá **connectionOptions** também pode ser definido por meio de um valor em uma tooindicate do arquivo de configuração, se as alterações de fragmentação são esperadas ou não durante um período de tempo.  

Este exemplo usa o valor de saudação de uma chave de inteiro **CustomerID**usando um **ShardMap** objeto chamado **customerShardMap**.  

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

Olá **OpenConnectionForKey** método retorna um nova conexão já aberta toohello banco de dados correto. Conexões utilizados dessa forma ainda se beneficiar do pool de conexões do ADO.Net. Como as transações e solicitações podem ser atendidas por um fragmento por vez, isso deve ser Olá única modificação necessária em um aplicativo já usando o ADO.Net. 

Olá  **[OpenConnectionForKeyAsync método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  também está disponível se seu aplicativo usar a programação assíncrona com o ADO.Net. Seu comportamento é dados saudação dependentes de roteamento equivalente do ADO. Do NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  método.

## <a name="integrating-with-transient-fault-handling"></a>Integrando a manipulação de falhas transitórias
Uma prática recomendada no desenvolvimento de aplicativos de acesso de dados na nuvem Olá é tooensure que falhas transitórias são detectadas por aplicativo hello e que operações de saudação são repetidas várias vezes antes de gerar um erro. O tratamento de falha transitória para aplicativos em nuvem é discutido em [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Tratamento de falhas transitórias pode coexistir, naturalmente, com padrão de saudação encaminhamento dependente de dados. Olá, requisito de chave é tooretry Olá inteiro de dados acesso solicitação incluindo Olá **usando** bloco que obteve a conexão de roteamento do hello dependente de dados. exemplo Hello acima poderia ser reescrito da seguinte maneira (Observe a alteração realçada). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Exemplo – roteamento com falhas transitórias manipulação dependentes dos dados
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


Pacotes de tratamento de falhas transitórias tooimplement necessários são baixados automaticamente quando você cria o aplicativo de exemplo hello Elástico de banco de dados. Pacotes também estão disponíveis separadamente na [Biblioteca Corporativa - Bloco de aplicativo de tratamento de falha transitória](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Use a versão 6.0 ou posterior. 

## <a name="transactional-consistency"></a>Consistência transacional
Propriedades transacionais estão garantidas para todos os fragmentos de tooa locais de operações. Por exemplo, transações enviadas por meio de roteamento dependente de dados execute no escopo de saudação de fragmento de destino Olá para conexão hello. Neste momento, não há nenhum recurso fornecido para inscrever-se várias conexões em uma transação e, portanto, não há nenhuma garantia transacional para operações executadas pelos fragmentos.

## <a name="next-steps"></a>Próximas etapas
toodetach um fragmento ou tooreattach um fragmento, consulte [usando problemas de mapa de fragmento Olá RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

