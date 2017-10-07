---
title: "biblioteca de cliente de banco de dados Elástico aaaUsing com Dapper | Microsoft Docs"
description: "Usar a biblioteca de cliente de banco de dados elástico com Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Usando a biblioteca de cliente do banco de dados elástico com Dapper
Este documento é para desenvolvedores que dependem de aplicativos toobuild Dapper, mas também quer tooembrace [ferramentas de banco de dados Elástico](sql-database-elastic-scale-introduction.md) toocreate aplicativos que implementam a camada de dados de fragmentação tooscale-out.  Este documento ilustra as alterações de saudação em aplicativos baseados em Dapper que são necessária toointegrate com ferramentas de banco de dados Elástico. Nosso foco está na composição de dados dependentes e gerenciamento de fragmento de banco de dados Elástico Olá roteamento com Dapper. 

**Código de exemplo**: [ferramentas de banco de dados elástico para o Banco de Dados SQL do Azure - integração com o Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

Integrando **Dapper** e **DapperExtensions** com hello biblioteca de cliente do banco de dados Elástico de banco de dados do SQL Azure é fácil. Os aplicativos podem usar dados dependentes de roteamento alterando criação hello e abertura de novos [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) Olá de toouse objetos [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) chamar de saudação [cliente biblioteca](http://msdn.microsoft.com/library/azure/dn765902.aspx). Isso limita as alterações no seu tooonly de aplicativo em que novas conexões são criadas e abertos. 

## <a name="dapper-overview"></a>Visão geral do Dapper
**Dapper** é um mapeador relacional de objetos. Ele mapeia objetos do .NET Framework do aplicativo tooa banco de dados relacional (e vice-versa). a primeira parte Olá Olá códigos de exemplo ilustra como você pode integrar a biblioteca de cliente do banco de dados Elástico Olá com aplicativos baseados em Dapper. Olá segunda parte do código de exemplo hello ilustra como toointegrate ao usar Dapper e DapperExtensions.  

funcionalidade de mapeador de saudação em Dapper fornece métodos de extensão em conexões de banco de dados que simplificam enviando instruções T-SQL para execução ou consultar banco de dados de saudação. Por exemplo, Dapper torna fácil toomap entre seus objetos .NET e os parâmetros de saudação de instruções SQL para **Execute** chamadas ou resultados de saudação tooconsume de suas consultas SQL em objetos .NET usando **consulta**chamadas de Dapper. 

Ao usar DapperExtensions, você não precisa mais instruções de SQL tooprovide hello. Métodos de extensões como **GetList** ou **inserir** pela conexão de banco de dados de saudação criar hello instruções SQL em segundo plano da saudação.

Outro benefício de Dapper e também DapperExtensions é controles de aplicativo Olá Olá criação de conexão de banco de dados de saudação. Isso ajuda a interagir com a biblioteca de cliente do banco de dados Elástico Olá qual agentes com base no mapeamento de saudação do toodatabases shardlets de conexões de banco de dados.

tooget Olá Dapper módulos (assemblies), consulte [Dapper dot net](http://www.nuget.org/packages/Dapper/). Para as extensões de saudação Dapper, consulte [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Uma visão geral de biblioteca de cliente do banco de dados Elástico Olá
Com a biblioteca de cliente do banco de dados Elástico Olá, você definir partições de dados do aplicativo chamados *shardlets* , mapeá-los toodatabases e identificá-los por *as chaves de fragmentação*. Você pode ter quantos bancos de dados conforme necessário e distribuir seu shardlets entre esses bancos de dados. mapeamento de saudação de bancos de dados de toohello de valores de chave fragmentação é armazenado por um mapa do fragmento fornecido pelas APIs da biblioteca hello. Essa funcionalidade é chamada de **gerenciamento de mapa de fragmentos**. mapa do fragmento Olá também serve como agente de saudação de conexões de banco de dados para solicitações que contêm uma chave de fragmentação. Esse recurso é chamado de tooas **roteamento dependente de dados**.

![Mapas de fragmentos e roteamento dependente de dados][1]

Gerenciador do mapa de fragmentos Olá protege os usuários contra modos de exibição inconsistente em dados de shardlet que podem ocorrer quando as operações de gerenciamento de shardlet simultâneas estão ocorrendo nos bancos de dados de saudação. toodo Olá assim, mapas de fragmento broker conexões de banco de dados Olá para um aplicativo compilado com a biblioteca de saudação. Olá shardlet podem afetar as operações de gerenciamento de fragmento, permite que kill do hello fragmento mapa funcionalidade tooautomatically uma conexão de banco de dados. 

Em vez de usar conexões de toocreate de maneira tradicional de saudação para Dapper, precisamos Olá toouse [OpenConnectionForKey método](http://msdn.microsoft.com/library/azure/dn824099.aspx). Isso garante que todas as validações de saudação ocorre e conexões são gerenciadas corretamente quando nenhum dado é movido entre fragmentos.

### <a name="requirements-for-dapper-integration"></a>Requisitos para a integração do Dapper
Ao trabalhar com a biblioteca de cliente do banco de dados Elástico hello e Olá APIs Dapper, queremos Olá tooretain propriedades a seguir:

* **Expansão**: deseja tooadd ou remover bancos de dados Olá da camada de dados do aplicativo fragmentados Olá conforme necessário para atender às demandas de capacidade de saudação do aplicativo hello. 
* **Consistência**: desde que o aplicativo é expandido usando a fragmentação, precisamos de roteamento dependente de dados do tooperform. Queremos toouse Olá dados dependentes capacidades de roteamento de saudação biblioteca toodo assim. Em particular, queremos que a validação de saudação tooretain e garante a consistência fornecida pelas conexões que são orientadas por meio do Gerenciador do mapa de fragmentos Olá nos resultados de consulta incorreto ou corrupção de tooavoid de ordem. Isso garante que tooa conexões dado shardlet são rejeitadas ou interrompido se (por exemplo) Olá shardlet está sendo movido tooa fragmento diferente usando APIs de divisão/mesclagem.
* **Mapeamento de objeto**: queremos tooretain conveniência de saudação de mapeamentos de saudação fornecidos pelo tootranslate Dapper entre classes no aplicativo hello e hello subjacente estruturas de banco de dados. 

Olá, seção a seguir fornece orientação para esses requisitos para aplicativos com base em **Dapper** e **DapperExtensions**.

## <a name="technical-guidance"></a>Orientações técnicas
### <a name="data-dependent-routing-with-dapper"></a>Roteamento dependente de dados com Dapper
Com Dapper, o aplicativo hello é geralmente, responsável por criar e abrir Olá conexões toohello subjacente do banco de dados. Dado um tipo T pelo aplicativo hello, Dapper retorna resultados da consulta como coleções de .NET do tipo T. Dapper executa o mapeamento de saudação de objetos Olá T-SQL resultado linhas toohello do tipo T. Da mesma forma, Dapper mapeia objetos .NET em valores SQL ou parâmetros para instruções de DML (linguagem) de manipulação de dados. Dapper oferece essa funcionalidade por meio de métodos de extensão em Olá regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objeto das bibliotecas de cliente de SQL do ADO .NET hello. Olá conexão SQL retornado pelo Olá APIs de dimensionamento Elástico para DDR também são regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objetos. Isso nos permite toodirectly use Dapper extensões sobre o tipo de saudação retornado pela API de DDR da biblioteca de cliente hello, como também é uma conexão de cliente SQL simple.

Essas observações tornam toouse simples conexões orientadas pela biblioteca de cliente do banco de dados Elástico Olá para Dapper.

Este exemplo de código (de saudação que acompanha o exemplo) ilustra a abordagem de saudação onde chave de fragmentação de saudação é fornecido por Olá aplicativo toohello biblioteca toobroker Olá conexão toohello direita fragmento.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Olá chamada toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API substitui a criação de padrão de saudação e abertura de uma conexão de cliente SQL. Olá [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) chamada utiliza argumentos de saudação que são necessários para encaminhamento dependente de dados: 

* tooaccess de mapa do fragmento Olá Olá interfaces de roteamento dependente de dados
* Olá fragmentação tooidentify chave Olá shardlet
* fragmento de toohello de tooconnect Olá credenciais (nome de usuário e senha)

objeto de mapa do fragmento Olá cria um fragmento de toohello de conexão que contém o shardlet Olá para Olá recebe a chave de fragmentação. APIs de cliente de banco de dados Elástico Olá também marca Olá conexão tooimplement garante sua consistência. Desde Olá chamar muito[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) retorna um objeto de conexão SQL Client regular, Olá chamada subsequente toohello **Execute** método de extensão de maneira Dapper Olá Dapper padrão prática.

Consultas de trabalho muito Olá mesmo maneira - você primeiro abre Olá conexão usando [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) da API do cliente hello. Em seguida, usar o hello regular extensão Dapper métodos toomap Olá resultados sua consulta SQL em objetos .NET:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Observe que Olá **usando** bloco com escopos de conexão de DDR Olá todas as operações de banco de dados dentro de saudação bloco toohello um fragmento onde tenantId1 é mantida. consulta de saudação somente retorna blogs armazenado no fragmento atual hello, mas não Olá arquivos armazenados em quaisquer outros fragmentos. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Roteamento dependente de dados com Dapper e DapperExtensions
Dapper vem com um ecossistema de extensões adicionais que podem fornecer mais conveniência e a abstração de banco de dados de saudação ao desenvolver aplicativos de banco de dados. O DapperExtensions é um exemplo. 

O uso do DapperExtensions em seu aplicativo não muda como conexões de banco de dados são criadas e gerenciadas. Ainda é conexões de tooopen de responsabilidade do aplicativo hello e objetos de conexão SQL Client regulares são esperados pelos métodos de extensão de saudação. Podemos contar com hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) conforme descrito acima. Como Olá exemplos de código seguintes mostram, Olá única alteração é que não temos mais toowrite instruções de saudação T-SQL:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

E aqui está o exemplo de código Olá para consulta hello: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Tratamento de falhas transitórias
Olá Microsoft Patterns & Practices equipe Olá publicado [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) os desenvolvedores de aplicativos toohelp reduzir condições comuns de falha transitória durante a execução na nuvem hello. Para obter mais informações, consulte [Perseverance, o segredo de todos os Triumphs: usando Olá Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).

exemplo de código Hello depende Olá falhas transitórias biblioteca tooprotect contra falhas transitórias. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** Olá código acima é definido como um **SqlDatabaseTransientErrorDetectionStrategy** com uma contagem de repetição de 10 e 5 segundos tempo de espera entre as repetições. Se você estiver usando transações, certifique-se de que o escopo de repetição vai voltar toohello início da transação Olá no caso de saudação de uma falha temporária.

## <a name="limitations"></a>Limitações
abordagens de saudação descritas neste documento envolvem algumas limitações:

* código de exemplo Hello para este documento demonstra como esquema toomanage em fragmentos.
* Recebe uma solicitação, vamos supor que todo o processamento de seu banco de dados está contido em um único fragmento conforme identificado pela chave de fragmentação Olá fornecida por solicitação hello. No entanto, essa suposição sempre mantém, por exemplo, quando não é possível toomake uma chave de fragmentação disponível. tooaddress, Olá biblioteca de cliente do banco de dados Elástico inclui Olá [MultiShardQuery classe](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). classe Olá implementa uma abstração de conexão para consultas em vários fragmentos. Usar MultiShardQuery em combinação com Dapper está além do escopo deste documento hello.

## <a name="conclusion"></a>Conclusão
Aplicativos que usam Dapper e DapperExtensions podem aproveitar facilmente as ferramentas de banco de dados elástico para o Banco de Dados SQL do Azure. Por meio de Olá as etapas descritas neste documento, esses aplicativos podem usar recurso da ferramenta Olá para dados dependentes de roteamento alterando criação hello e abertura de novos [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) Olá de toouse objetos [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) chamada da biblioteca de cliente do banco de dados Elástico hello. Isso limita Olá aplicativo alterações toothose necessário locais onde novas conexões são criadas e abertos. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
