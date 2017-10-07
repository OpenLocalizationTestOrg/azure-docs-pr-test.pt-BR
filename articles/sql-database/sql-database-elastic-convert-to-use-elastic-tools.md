---
title: aaaMigrate existente tooscale fora de bancos de dados | Microsoft Docs
description: "Converter ferramentas de banco de dados Elástico toouse bancos de dados fragmentados, criando um Gerenciador de mapa do fragmento"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Migrar tooscale-out de bancos de dados existente
Gerenciar facilmente expandido fragmentados bancos de dados existentes usando as ferramentas de banco de dados do banco de dados SQL (como Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md)). Você deve primeiro converter um conjunto existente de saudação do bancos de dados toouse [Gerenciador do mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Visão geral
toomigrate um banco de dados fragmentado existente: 

1. Preparar Olá [banco de dados do fragmento mapa manager](sql-database-elastic-scale-shard-map-management.md).
2. Crie um mapa do fragmento hello.
3. Prepare os fragmentos individuais hello.  
4. Adicione o mapa do fragmento toohello mapeamentos.

Essas técnicas podem ser implementadas usando qualquer Olá [biblioteca de cliente do .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), ou scripts do PowerShell Olá encontrado em [DB do SQL Azure - scripts de ferramentas de banco de dados Elástico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). Estes exemplos Olá usam scripts do PowerShell hello.

Para obter mais informações sobre Olá ShardMapManager, consulte [gerenciamento de mapa do fragmento](sql-database-elastic-scale-shard-map-management.md). Para obter uma visão geral das ferramentas de banco de dados Elástico hello, consulte [visão geral dos recursos de banco de dados Elástico](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Preparar o banco de dados do hello fragmento mapa manager
Gerenciador do mapa de fragmentos Olá é um banco de dados especial que contém os bancos de dados do hello dados toomanage expansíveis. Você pode usar um banco de dados existente ou criar um novo banco de dados. Observe que um banco de dados atua como o Gerenciador do mapa do fragmento não deve ser Olá mesmo banco de dados como um fragmento. Observe também que o script do PowerShell Olá não criar banco de dados de saudação para você. 

## <a name="step-1-create-a-shard-map-manager"></a>Etapa 1: criar um gerenciador de mapa de fragmentos
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>Gerenciador do mapa de fragmentos tooretrieve Olá
Após a criação, você pode recuperar o Gerenciador do mapa de fragmentos Olá com esse cmdlet. Essa etapa é necessária sempre que é necessário toouse Olá ShardMapManager objeto.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Etapa 2: criar um mapa do fragmento Olá
Você deve selecionar o tipo de saudação do toocreate de mapa do fragmento. Olá escolha depende da arquitetura de banco de dados de saudação: 

1. Único locatário por banco de dados (para termos, consulte Olá [glossário](sql-database-elastic-scale-glossary.md).) 
2. Vários locatários por banco de dados (dois tipos):
   1. Mapeamento de lista
   2. Mapeamento de intervalo

Para um modelo de locatário único, crie um mapa de fragmentos de **mapeamento de lista** . modelo de único locatário Olá atribui um banco de dados por locatário. Esse é um modelo eficaz para desenvolvedores de SaaS, pois simplifica o gerenciamento.

![Mapeamento de lista][1]

modelo de multilocatário Olá atribui vários locatários tooa único banco de dados (e você pode distribuir os grupos de locatários entre vários bancos de dados). Use este modelo quando você espera que precisam de cada locatário toohave pequenos de dados. Nesse modelo, nós atribuímos um intervalo de locatários usando o banco de dados tooa **mapeamento intervalo**. 

![Mapeamento de intervalo][2]

Ou você pode implementar um modelo de banco de dados de vários locatários usando um *mapeamento de lista* tooassign vários locatários tooa único banco de dados. Por exemplo, DB1 é usado toostore informações sobre a id de locatário 1 e 5 e DB2 armazena dados de locatário 7 e locatário 10. 

![Vários locatários em um banco de dados individual][3] 

**Com base na sua escolha, escolha uma destas opções:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Opção 1: criar um mapa de fragmentos para um mapeamento de lista
Crie um mapa do fragmento usando Olá ShardMapManager objeto. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Opção 2: criar um mapa de fragmentos para um mapeamento de intervalo
Observe que tooutilize esse padrão de mapeamento, valores de id de locatário precisa intervalos contínuos toobe e é o intervalo aceitável toohave em intervalos de saudação simplesmente ignorar o intervalo de saudação durante a criação de bancos de dados de saudação.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Opção 3: mapeamentos de lista em um banco de dados individual
A configuração desse padrão também exige a criação de um mapa de lista conforme mostrado na etapa 2, opção 1.

## <a name="step-3-prepare-individual-shards"></a>Etapa 3: preparar os fragmentos individuais
Adicione o Gerenciador do mapa de fragmento de toohello cada fragmento (banco de dados). Isso prepara os bancos de dados individuais Olá para armazenar informações de mapeamento. Execute esse método em cada fragmento.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Etapa 4: Adicionar mapeamentos
adição de saudação de mapeamentos de depende em tipo de saudação do mapa de fragmentos que você criou. Se tiver criado um mapa de lista, você adicionará mapeamentos de lista. Se tiver criado um mapa de intervalo, você adicionará mapeamentos de intervalo.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Opção 1: dados de saudação do mapa para um mapeamento de lista
Mapear dados de saudação adicionando um mapeamento de lista para cada locatário.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Opção 2: dados de saudação do mapa para um mapeamento de intervalo
Adicione mapeamentos de intervalo de saudação para todos os Olá locatário intervalo de id - associações de banco de dados:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Etapa 4 opção 3: mapear dados de saudação para vários locatários em um único banco de dados
Para cada locatário, execute Olá adicionar ListMapping (opção 1, acima). 

## <a name="checking-hello-mappings"></a>Verificando os mapeamentos de saudação
Informações sobre fragmentos existentes hello e mapeamentos de saudação associados a eles podem ser consultadas usando comandos a seguir:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Resumo
Depois de concluir a instalação hello, você pode começar a biblioteca de cliente de banco de dados Elástico toouse hello. Também é possível usar o [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) e [consulta de vários fragmentos](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Próximas etapas
Obter scripts do PowerShell de saudação do [sripts das ferramentas de banco de dados do Azure SQL DB elástica](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

Olá ferramentas também estão no GitHub: [Azure/elástica-db-tools](https://github.com/Azure/elastic-db-tools).

Use Olá ferramenta de mesclagem de divisão toomove dados tooor de um modelo de locatário único tooa modelo multilocatário. Consulte [Ferramenta de divisão e mesclagem](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Recursos adicionais
Para obter informações sobre os padrões comuns da arquitetura de dados dos aplicativos do banco de dados SaaS (software como serviço) multilocatário, consulte [Padrões de Design para Aplicativos SaaS multilocatário com o Banco de Dados SQL do Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Perguntas e solicitações de recursos
Para dúvidas, entre em contato toous em Olá [Fórum do banco de dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e para solicitações de recurso, adicione-toohello [Fórum de comentários do banco de dados SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

