---
title: aaaScale-out de um banco de dados SQL do Azure | Microsoft Docs
description: "Como toouse Olá ShardMapManager, biblioteca de cliente do banco de dados Elástico"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Expansão de bancos de dados com o Gerenciador do mapa de fragmentos Olá
tooeasily expansão de bancos de dados no SQL Azure, use um Gerenciador de mapa do fragmento. Gerenciador do mapa de fragmentos Olá é um banco de dados especial que mantém as informações sobre todos os fragmentos (bancos de dados) em um conjunto de fragmentos de mapeamento global. Olá metadados permitem que um aplicativo tooconnect toohello banco de dados correto com base no valor Olá Olá **chave de fragmentação**. Além disso, cada fragmento no conjunto de saudação contém mapas que acompanham os dados de local de fragmento de saudação (conhecido como **shardlets**). 

![Gerenciamento de mapa de fragmentos](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Noções básicas sobre como esses mapas são construídos é tooshard essenciais de gerenciamento de mapa. Isso é feito usando Olá [ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), encontrado em Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md) toomanage fragmento é mapeado.  

## <a name="shard-maps-and-shard-mappings"></a>Mapas de fragmentos e mapeamentos de fragmentos
Para cada fragmento, você deve selecionar o tipo de saudação do toocreate de mapa do fragmento. Olá escolha depende da arquitetura de banco de dados de saudação: 

1. Um locatário único por banco de dados  
2. Vários locatários por banco de dados (dois tipos):
   1. Mapeamento de lista
   2. Mapeamento de intervalo

Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista** . modelo de único locatário Olá atribui um banco de dados por locatário. Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.

![Mapeamento de lista][1]

modelo de multilocatário Olá atribui vários locatários tooa único banco de dados (e você pode distribuir os grupos de locatários entre vários bancos de dados). Use este modelo quando você espera que precisam de cada locatário toohave pequenos de dados. Nesse modelo, nós atribuímos um intervalo de locatários usando o banco de dados tooa **mapeamento intervalo**. 

![Mapeamento de intervalo][2]

Ou você pode implementar um modelo de banco de dados de vários locatários usando um *mapeamento de lista* tooassign vários locatários tooa único banco de dados. Por exemplo, DB1 é usado toostore informações sobre a id de locatário 1 e 5 e DB2 armazena dados de locatário 7 e locatário 10. 

![Vários locatários em um banco de dados individual][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Tipos .Net com suporte para chaves de fragmentação
Elástico Olá de suporte de escala após o .net Framework tipos como chaves de fragmentação:

* inteiro
* longo
* guid
* byte[]  
* datetime
* timespan
* datetimeoffset

### <a name="list-and-range-shard-maps"></a>Mapas de fragmentos de lista e intervalo
Mapas de fragmentos podem ser construídos usando **listas de valores de chave de fragmentação individuais** ou **intervalos de valores de chave de fragmentação**. 

### <a name="list-shard-maps"></a>Mapas de fragmentos de lista
**Fragmentos** contêm **shardlets** e mapeamento de saudação do shardlets tooshards é mantido por um mapa do fragmento. Um **mapa do fragmento lista** é uma associação entre Olá individuais valores de chave que identificam Olá shardlets e bancos de dados de saudação que servem como fragmentos.  **Lista de mapeamentos de** são explícita e diferentes valores de chave podem ser mapeada toohello mesmo banco de dados. Por exemplo, a chave 1 mapeia tooDatabase A e B. o banco de dados de referência de valores de chave 3 e 6

| Chave | Local de fragmento |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Mapas de fragmentos de intervalo
Em um **mapa do fragmento intervalo**, intervalo de chave Olá é descrito por um par de **[valor baixo, alto valor)** onde Olá *valor baixo* Olá de chave mínimo no intervalo de saudação e Olá *Valor alto* é Olá primeiro valor maior do que o intervalo de saudação. 

Por exemplo, **(0, 100)** inclui todos os números inteiros iguais ou maiores que 0 e menores que 100. Observe que várias toohello intervalos da ponto pode mesmo banco de dados e intervalos de separação têm suporte (por exemplo, [100,200) e [400,600) ambos os ponto tooDatabase C exemplo hello abaixo.)

| Chave | Local de fragmento |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

Cada uma das tabelas de saudação mostradas acima é um exemplo conceitual de um **ShardMap** objeto. Cada linha é um exemplo simplificado de um indivíduo **PointMapping** (para o mapa do fragmento lista Olá) ou **RangeMapping** (para o mapa do fragmento de intervalo de saudação) objeto.

## <a name="shard-map-manager"></a>Gerenciador de mapa de fragmentos
Na biblioteca de cliente Olá, o Gerenciador do mapa de fragmentos Olá é uma coleção de mapas de fragmento. Olá dados gerenciados por um **ShardMapManager** instância é mantida em três locais: 

1. **Mapa de fragmento global (GSM)**: especificar um tooserve de banco de dados como repositório Olá para todos os seus mapas de fragmento e mapeamentos. Procedimentos armazenados e tabelas especiais são criados automaticamente informações de saudação toomanage. Isso geralmente é um banco de dados pequeno e pouco acessados e não deve ser usado para outras necessidades de aplicativo hello. Olá tabelas estão em um esquema especial chamado **__ShardManagement**. 
2. **Mapa de fragmento local (LSM)**: cada banco de dados que você especificar toobe um fragmento é modificado toocontain várias tabelas pequenas e procedimentos armazenados especiais que contêm e gerenciar o fragmento do fragmento mapa informações toothat específico. Essas informações são redundantes com informações Olá Olá GSM e permite que informações de mapa de fragmento do hello aplicativo toovalidate armazenado em cache sem colocar nenhuma carga no hello GSM; aplicativo Hello usa Olá LSM toodetermine se um mapeamento em cache ainda é válido. Olá tabelas correspondente toohello LSM em cada fragmento também estão no esquema de saudação **__ShardManagement**.
3. **Cache do aplicativo**: cada instância do aplicativo que acessa um objeto **ShardMapManager** mantém um cache na memória local dos seus mapeamentos. Ele armazena informações de roteamento que recentemente foi recuperadas. 

## <a name="constructing-a-shardmapmanager"></a>Construindo um ShardMapManager
Um objeto **ShardMapManager** é construído usando um padrão [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) . Olá  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  método usa as credenciais (incluindo o nome do servidor de saudação e nome de banco de dados, mantendo a saudação GSM) na forma de saudação de um  **ConnectionString** e retorna uma instância de um **ShardMapManager**.  

**Observação:** Olá **ShardMapManager** deve ser instanciada somente uma vez por domínio de aplicativo, no código de inicialização de saudação para um aplicativo. Criação de instâncias adicionais do ShardMapManager em Olá mesmo appdomain, resultará em maior utilização de memória e CPU do aplicativo hello. Um **ShardMapManager** pode conter diversos mapas de fragmento. Enquanto um mapa do fragmento único pode ser suficiente para muitos aplicativos, há vezes quando conjuntos diferentes de bancos de dados são usados para esquemas diferentes ou para fins exclusivos e, nesses casos, vários mapas de fragmentação podem ser preferíveis. 

Nesse código, um aplicativo tenta tooopen existente **ShardMapManager** com hello [TryGetSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Se objetos que representam um Global **ShardMapManager** (GSM) ainda não existe no banco de dados de saudação, biblioteca de saudação do cliente cria existe usando Olá [CreateSqlShardMapManager método](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

Como alternativa, você pode usar o Powershell toocreate um novo Gerenciador de mapa do fragmento. Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Obter um RangeShardMap ou ListShardMap
Depois de criar um fragmento Gerenciador do mapa, você pode obter Olá [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) usando Olá [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Olá [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Credenciais de administração de mapa de fragmentos
Aplicativos que administrarem e manipulam os mapas de fragmento são diferentes daqueles que usam conexões de tooroute de mapas de fragmento hello. 

mapas de fragmento tooadminister (Adicionar ou alterar os fragmentos, mapas de fragmento, mapeamentos de fragmento, etc.) você deve instanciar Olá **ShardMapManager** usando **leitura/gravação de credenciais que tenham privilégios em ambos os banco de dados GSM hello e em cada banco de dados que serve como um fragmento**. credenciais de saudação devem permitir gravações nas tabelas de saudação em ambos os Olá GSM e LSM como informações de mapa do fragmento são inseridas ou alteradas, bem como para criar tabelas LSM em novos fragmentos.  

Consulte [as credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Apenas os metadados afetados
Métodos usados para popular ou alterando Olá **ShardMapManager** dados não alteram os dados de usuário Olá armazenados em fragmentos Olá próprios. Por exemplo, os métodos como **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. afetam Olá fragmento mapa somente metadados. Não remova, adicionar ou alterar os dados de usuário contidos em fragmentos hello. Em vez disso, esses métodos são projetada toobe usada em conjunto com operações separadas realizar toocreate ou remover bancos de dados reais, ou que você mova as linhas de um fragmento tooanother toorebalance um ambiente fragmentado.  (Olá **divisão mesclagem** ferramenta incluída com as ferramentas de banco de dados Elástico faz uso dessas APIs junto com orquestrar a movimentação de dados real entre fragmentos.) Consulte [dimensionamento usando a ferramenta Olá direta de divisão de banco de dados Elástico](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Popular um mapa de fragmentos: exemplo
Abaixo está um exemplo de sequência de operações toopopulate um mapa de fragmentos específicos. código de saudação executa estas etapas: 

1. Um novo mapa de fragmento é criado dentro de um Gerenciador de mapa do fragmento. 
2. metadados de saudação para dois fragmentos de diferentes são adicionados toohello mapa do fragmento. 
3. Uma variedade de mapeamentos de intervalo de chave são adicionados e hello conteúdo geral do mapa do fragmento Olá é exibido. 

código de saudação é gravado para que o método hello pode ser executado novamente, se ocorrer um erro. Cada solicitação testa se um fragmento ou mapeamento já existe, antes de tentar toocreate-lo. Olá código assume que os bancos de dados chamado **sample_shard_0**, **sample_shard_1** e **sample_shard_2** já foram criados no servidor de saudação referenciada pela cadeia de caracteres **shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Como alternativa você pode usar o PowerShell scripts tooachieve Olá mesmo resultado. Alguns dos exemplos do PowerShell de exemplo hello estão disponíveis [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Depois que foram populados mapas de fragmento, aplicativos de acesso de dados podem ser criados ou adaptado toowork com hello mapas. Popular ou manipulando Olá maps não precisa ocorrer novamente até que **layout de mapa** precisa toochange.  

## <a name="data-dependent-routing"></a>Roteamento dependente de dados
Gerenciador do mapa de fragmentos Hello mais será usado em aplicativos que requerem operações de dados específicos de aplicativo do banco de dados conexões tooperform hello. Essas conexões devem ser associadas ao banco de dados correto hello. Isso é conhecido como **Roteamento Dependente de Dados**. Para esses aplicativos, instanciar um objeto do Gerenciador do mapa de fragmento da fábrica de saudação usando as credenciais que possuem acesso somente leitura no banco de dados do hello GSM. Solicitações individuais para conexões posteriores fornecem as credenciais necessárias para conectar o banco de dados do toohello fragmento apropriado.

Observe que esses aplicativos (usando **ShardMapManager** aberta com as credenciais de somente leitura) não é possível fazer alterações toohello mapas ou mapeamentos. Para essas necessidades, crie aplicativos administrativos específicos ou scripts do PowerShell que fornecem credenciais de privilégios mais altos, conforme discutido anteriormente. Consulte [as credenciais usadas biblioteca de cliente de banco de dados Elástico tooaccess Olá](sql-database-elastic-scale-manage-credentials.md).

Para obter mais detalhes, consulte [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Modificar um mapa de fragmentos
Um mapa do fragmento pode ser alterado de diferentes maneiras. Todos os métodos a seguir de saudação modificar Olá metadados descrevendo fragmentos hello e seus mapeamentos, mas eles não modificam dados em fragmentos Olá fisicamente, nem criar ou excluir bancos de dados real hello.  Algumas das operações de saudação no mapa do fragmento Olá descrito a seguir podem ser necessário toobe coordenado com ações administrativas que mover fisicamente os dados, ou adicionar e remover bancos de dados que serve como fragmentos.

Esses métodos funcionam em conjunto como blocos de construção de saudação disponíveis para modificar Olá distribuição geral de dados em seu ambiente de banco de dados fragmentado.  

* tooadd ou remover fragmentos: usar  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  e  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  de saudação [Shardmap classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Olá servidor e banco de dados que representa o fragmento de destino Olá já devem existir para tooexecute essas operações. Esses métodos não têm qualquer impacto Olá bancos de dados, somente em metadados no mapa do fragmento hello.
* toocreate ou remover pontos ou intervalos que são mapeados toohello fragmentos: usar  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  de saudação [RangeShardMapping classe](https://msdn.microsoft.com/library/azure/dn807318.aspx), e  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  de saudação [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Muitos pontos diferentes ou intervalos podem ser mapeada toohello mesmo fragmento. Esses métodos afetam somente metadados – eles não afetam os dados que podem já estar presentes em fragmentos. Se é necessário toobe removido do banco de dados de saudação em ordem toobe consistente com dados **DeleteMapping** operações, você precisará tooperform essas operações separadamente, mas em conjunto com o uso desses métodos.  
* intervalos de toosplit existentes em dois ou intervalos adjacentes de mesclagem em uma: usar  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  e  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Observe que a divisão e mesclagem operações **não altere a chave de toowhich de fragmento Olá valores são mapeados**. Uma divisão divide um intervalo existente em duas partes, mas deixa como toohello mapeada mesmo fragmento. Uma mesclagem opera em dois intervalos adjacentes que já estão mapeada toohello mesmo fragmento, união-los em um único intervalo.  movimentação de pontos ou intervalos próprios entre fragmentos Hello precisa toobe coordenada usando **UpdateMapping** em conjunto com a movimentação de dados real.  Você pode usar o hello **divisão/mesclagem** ferramentas de serviço que faz parte do banco de dados Elástico toocoordinate alterações no mapa de fragmentos com movimentação de dados, quando a movimentação é necessária. 
* mapa de toore (ou mover) pontos ou intervalos toodifferent fragmentos individuais: usar  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Desde que os dados podem ter toobe movido de um fragmento tooanother em ordem toobe consistente com **UpdateMapping** operações, você precisará tooperform essa movimentação separadamente, mas em conjunto com o uso desses métodos.
* mapeamentos de tootake online e offline: usar  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  e  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol Olá estado online de um mapeamento. 
  
    Algumas operações nos mapeamentos de fragmentos são permitidas apenas quando um mapeamento está em um estado “offline”, incluindo **UpdateMapping** e **DeleteMapping**. Quando um mapeamento estiver offline, uma solicitação dependente de dados com base em uma chave incluída nesse mapeamento retornará um erro. Além disso, quando um intervalo primeiro é colocado offline, todos os fragmentos de toohello afetado conexões serão eliminados automaticamente nos resultados de inconsistente ou incompleta de tooprevent de ordem para consultas direcionadas a intervalos que está sendo alterados. 

Mapeamentos são objetos imutáveis no .Net.  Todos os métodos de saudação acima que alterar os mapeamentos de invalidam também qualquer toothem referências no seu código. toomake it sequências de tooperform mais fácil de operações que alteram o estado do mapeamento, todos os métodos de saudação que alterar um mapeamento de retornam um novo mapeamento de referência, para que as operações podem ser encadeadas. Por exemplo, toodelete um mapeamento no sm shardmap que contém a chave de saudação 25 existente, você pode executar Olá a seguir: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Adicionar um fragmento
Aplicativos geralmente precisa toosimply adicionar novos fragmentos toohandle dados que são esperados de novas chaves ou intervalos de chaves para um mapa do fragmento que já existe. Por exemplo, um aplicativo fragmentado por ID de locatário pode ser necessário tooprovision um novo fragmento para um novo locatário ou mensal de dados fragmentados talvez seja necessário um novo fragmento provisionado antes do início da saudação de cada novo mês. 

Se o novo intervalo de valores de chave de Olá não ainda estiver parte de um mapeamento existente e nenhuma movimentação de dados é necessária, o que é novo fragmento saudação do tooadd muito simples e associar a nova chave de saudação ou fragmento de toothat do intervalo. Para obter detalhes sobre como adicionar novos fragmentos, veja [Adicionar um novo fragmento](sql-database-elastic-scale-add-a-shard.md).

No entanto, para cenários que exigem a movimentação de dados, ferramenta de mesclagem de divisão de saudação é tooorchestrate necessário Olá a movimentação de dados entre fragmentos em combinação com atualizações de mapa de fragmento necessários hello. Para obter detalhes sobre como usar o hello yool de divisão de mesclagem, consulte [visão geral da divisão de mesclagem](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
