---
title: "políticas de indexação de banco de dados do Cosmos aaaAzure | Microsoft Docs"
description: "Entenda como funciona a indexação no Azure Cosmos DB. Saiba como tooconfigure e alteração Olá política de indexação para a indexação automática e melhor desempenho."
keywords: "como funciona a indexação, indexação automática, banco de dados de indexação"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Como o Azure Cosmos DB indexa dados?

Por padrão, todos os dados do Azure Cosmos DB são indexados. E enquanto muitos clientes estão satisfeitos toolet Azure Cosmos DB tratar automaticamente todos os aspectos da indexação, o banco de dados do Azure Cosmos também oferece suporte a especificando um personalizado **política de indexação** para coleções durante a criação. Políticas de indexação no banco de dados do Azure Cosmos são mais flexíveis e eficientes do que os índices secundários oferecidos em outras plataformas de banco de dados, porque elas permitem criar e personalizar a forma de saudação do índice de saudação sem sacrificar a flexibilidade de esquema. toolearn como indexação funciona no banco de dados do Azure Cosmos, você deve entender que, por meio do gerenciamento de política de indexação, você pode fazer refinadas compensações entre sobrecarga de armazenamento do índice, gravação e taxa de transferência de consulta e a consistência de consulta.  

Neste artigo, vamos dar uma olhada fechar o banco de dados do Azure Cosmos políticas de indexação, como você pode personalizar a política de indexação e Olá associado vantagens e desvantagens. 

Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:

* Como substituir Olá propriedades tooinclude ou excluir da indexação?
* Como configurar o índice da saudação eventual atualizações?
* Como configurar a indexação tooperform Order By ou intervalo de consultas?
* Como exibir a política de indexação da coleção de tooa alterações?
* Como posso comparar armazenamento e desempenho de políticas de indexação diferentes?

## <a id="CustomizingIndexingPolicy"></a>Personalizando a política de indexação de saudação de uma coleção
Os desenvolvedores podem personalizar Olá prós e contras armazenamento, desempenho de consulta/gravação e a consistência de consulta, substituindo a política de indexação saudação padrão em uma coleção de banco de dados do Azure Cosmos e configurando Olá aspectos a seguir.

* **Incluindo/excluindo documentos e caminhos no/do índice**. Os desenvolvedores podem escolher toobe certos documentos excluídos ou incluídos no índice de saudação em tempo de saudação de inserção ou substituí-las toohello coleção. Os desenvolvedores também podem escolher tooinclude ou excluir determinadas propriedades JSON também conhecido como toobe (incluindo padrões de curinga) de caminhos indexado em todos os documentos que são incluídos em um índice.
* **Configurando diversos tipos de índice**. Para cada um dos caminhos de saudação incluído, os desenvolvedores também podem especificar tipo de saudação do índice que precisam de uma coleção com base em seus dados e carga de trabalho de consulta esperada e Olá numérico/cadeia de caracteres "precisão" para cada caminho.
* **Configurando modos de atualização de índice**. Banco de dados do Azure Cosmos dá suporte a três modos de indexação que podem ser configurados via Olá política em uma coleção de banco de dados do Azure Cosmos de indexação: consistente, Lazy e None. 

Olá .NET mostra de trecho de código a seguir como tooset uma política personalizada de indexação durante a criação de saudação de uma coleção. Aqui vamos definir política Olá com índice de intervalo para cadeias de caracteres e números na precisão máxima da saudação. Essa política nos permite executar consultas de Ordenar por com relação a cadeias de caracteres.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> esquema JSON Olá para política de indexação foi alterada com versão de saudação da versão da API REST índices de intervalo toosupport 2015-06-03 entre cadeias de caracteres. .NET SDK 1.2.0 e Java, Python e Node.js SDKs 1.1.0 oferecem suporte a saudação nova política schema. SDKs mais antigas usam Olá versão 2015-04-08 da API REST e suportam a esquema mais antigo de saudação da política de indexação.
> 
> Por padrão, o Azure Cosmos DB indexa todas as propriedades de cadeia de caracteres nos documentos de forma consistente com um índice de Hash e as propriedades numéricas com um índice de Intervalo.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Personalizando a política de indexação hello usando o portal de saudação

Você pode alterar Olá indexação de política de uma coleção usando Olá portal do Azure. Abra sua conta do Azure Cosmos DB Olá portal do Azure, selecione sua coleção no hello de navegação à esquerda, clique em menu **configurações**e, em seguida, clique em **política de indexação**. Em Olá **política de indexação** folha, altere sua política de indexação e, em seguida, clique em **Okey** toosave suas alterações. 

### <a id="indexing-modes"></a>Modos de indexação do banco de dados
Banco de dados do Azure Cosmos oferece suporte a três indexação modos que podem ser configurados por meio de saudação indexação política em uma coleção de banco de dados do Azure Cosmos – consistente, Lazy e nenhum.

**Consistente**: se a política de uma coleção banco de dados do Azure Cosmos é designada como "consistente", consultas de saudação em um determinado acompanhamento de coleção do banco de dados do Azure Cosmos Olá mesmo nível de consistência especificado para o ponto-leituras de hello (ou seja, forte,-envelhecimento limitado, sessão ou eventual). índice de saudação é atualizado de modo síncrono como parte da atualização de documento hello (ou seja, inserção, substituição, update e delete de um documento em uma coleção de banco de dados do Azure Cosmos).  Indexação consistente dá suporte a consultas consistentes ao custo de saudação de redução possíveis na taxa de transferência de gravação. Essa redução é uma função de caminhos Olá exclusivo necessário toobe indexado e hello "nível de consistência". O modo de indexação consistente foi projetado para cargas de trabalho de "gravação rápida, consulta imediata”.

**Lento**: tooallow throughput de inclusão de documento máximo, uma coleção de banco de dados do Azure Cosmos pode ser configurada com consistência lenta; consultas significado são finalmente consistentes. índice de Olá é atualizado de forma assíncrona quando uma coleção de banco de dados do Azure Cosmos está inativa ou seja, quando a capacidade de taxa de transferência da coleção Olá não é totalmente utilizados tooserve solicitações do usuário. Para cargas de trabalho "ingerir agora, consultar depois" que exijam a ingestão ilimitada de documentos, o modo de indexação “lento” será mais adequado.

**Nenhum**: uma coleção marcada com o modo de índice "Nenhum" não tem nenhum índice associado a ela. Isso é geralmente usado se o Azure Cosmos DB é utilizado como um armazenamento de chave/valor e os documentos são acessados apenas pela sua propriedade de ID. 

> [!NOTE]
> Olá configurar indexação de política com "None" tem Olá efeito colateral o descarte de um índice existente. Use essa opção se os padrões de acesso forem somente exigir a “id” e/ou o “self-link”.
> 
> 

Olá apresentação de exemplo a seguir como cria uma coleção de banco de dados do Azure Cosmos usando Olá .NET SDK com a indexação automática consistente em todas as inserções de documento.

Olá, a tabela a seguir mostra a consistência Olá para consultas baseadas em Olá modo de indexação (consistente e Lazy) configurado para Olá coleta e hello consistência nível especificado para a solicitação de consulta de saudação. Isso se aplica tooqueries feitas usando SDKs qualquer interface - API REST, ou de dentro procedimentos armazenados e gatilhos. 

|Consistência|Modo de indexação: Consistente|Modo de indexação: Lento|
|---|---|---|
|Strong|Strong|Eventual|
|Bounded staleness|Bounded staleness|Eventual|
|Session|Session|Eventual|
|Eventual|Eventual|Eventual|

O Azure Cosmos DB retorna um erro para consultas feitas em coleções com o modo de indexação Nenhum. Consultas ainda podem ser executadas como verificações via Olá explícita `x-ms-documentdb-enable-scan` cabeçalho Olá API REST ou hello `EnableScanInQuery` opção usando Olá SDK .NET de solicitação. Alguns recursos de consulta como ORDER BY não têm suporte como verificações com `EnableScanInQuery`.

Olá, tabela a seguir mostra a consistência Olá para consultas com base no modo de indexação de saudação (consistente, Lazy e nenhum) quando EnableScanInQuery é especificado.

|Consistência|Modo de indexação: Consistente|Modo de indexação: Lento|Modo de indexação: Nenhum|
|---|---|---|---|
|Strong|Strong|Eventual|Strong|
|Bounded staleness|Bounded staleness|Eventual|Bounded staleness|
|Session|Session|Eventual|Session|
|Eventual|Eventual|Eventual|Eventual|

Olá apresentação de exemplo de código a seguir como cria uma coleção de banco de dados do Azure Cosmos usando Olá SDK .NET com indexação consistente em todas as inserções de documento.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Caminhos de índice
Banco de dados do Azure Cosmos modelos de documentos JSON e índice hello como árvores e permite toopolicies tootune para caminhos de árvore de saudação. Nos documentos, você pode escolher quais caminhos devem ser incluídos ou excluídos da indexação. Isso pode oferecer desempenho aprimorado de gravação e armazenamento de índice inferior para cenários quando os padrões de consulta Olá são conhecidos com antecedência.

Caminhos de índice começam com raiz hello (/) e normalmente terminam com Olá? operador de caractere curinga, indicando que há vários valores possíveis para o prefixo de saudação. Por exemplo, tooserve selecione * de famílias F WHERE F.familyName = "Andersen", você deve incluir um caminho de índice para /familyName/? na política de índice da coleção de saudação.

Caminhos de índice também podem usar o hello * comportamento de saudação do curinga operador toospecify caminhos recursivamente sob prefixo hello. Por exemplo, carga / * pode ser usado tooexclude tudo na propriedade de carga de saudação da indexação.

Aqui estão os padrões comuns de saudação para especificar caminhos de índice:

| Caminho                | Descrição/caso de uso                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Caminho padrão para coleta. Recursivo e aplica-se a árvore do documento toowhole.                                                                                                                                                                                                                                   |
| /prop/?             | Caminho do índice necessário tooserve consultas como Olá seguinte (com Hash ou Range tipos respectivamente):<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /prop/*             | Caminho de índice para todos os caminhos no rótulo especificado hello. Funciona com hello consultas a seguir<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | Caminho do índice necessário tooserve iteração e consultas de junção em matrizes de escalares como ["a", "b", "c"]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | Caminho do índice necessário tooserve iteração e consultas de junção em relação a matrizes de objetos, como [{subprop: "a"}, {subprop: "b"}]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | Caminho do índice necessário tooserve consultas (com Hash ou Range tipos respectivamente):<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Ao configurar caminhos do índice personalizado, será necessário toospecify Olá indexação regra padrão Olá todo o documento árvore indicado pelo caminho especial hello "/ *". 
> 
> 

Olá exemplo a seguir configura um caminho específico com a indexação de intervalo e um valor de precisão personalizado de 20 bytes:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Tipos, modelos e precisões de dados
Agora que estamos dando uma olhada em como caminhos toospecify, vamos dar uma olhada opções hello, podemos usar tooconfigure Olá política de indexação para um caminho. Você pode especificar uma ou mais definições de indexação para cada caminho:

* Tipo de dados: **String**, **Number**, **Point**, **Polygon** ou **LineString** (pode conter somente uma entrada por tipo de dados por caminho)
* Tipo de índice: **Hash** (consultas de igualdade), **Intervalo** (consultas de igualdade, de intervalo ou Order By) ou **Espacial** (consultas espaciais) 
* Precisão: Para índice de hash varia de 1 too8 para cadeias de caracteres e números com padrão como 3. Para o índice de intervalo, esse valor pode ser -1 (precisão máxima) e variar entre 1 e 100 (precisão máxima) para a cadeia de caracteres ou valores numéricos.

#### <a name="index-kind"></a>Tipo de índice
O Azure Cosmos DB dá suporte a tipos de índice Hash e Intervalo em todos os caminhos (que podem ser configurados para cadeias de caracteres, números ou ambos).

* **Hash** dá suporte a consultas JOIN e de igualdade eficientes. Na maioria dos casos de uso, os índices de hash não é necessário uma maior precisão que saudação padrão de 3 bytes. DataType pode ser String ou Number.
* **Intervalo** dá suporte a consultas de igualdade eficientes, a consultas de intervalo (usando >, <, >=, <=, !=) e a consultas Order By. Por padrão, as consultas Ordenar por também exigem a precisão máxima de índice (-1). DataType pode ser String ou Number.

Banco de dados do Azure Cosmos também oferece suporte a tipo de índice espacial Olá para cada caminho, o que pode ser especificado para tipos de saudação LineString, Polygon ou ponto de dados. valor de saudação no caminho especificado Olá deve ser um fragmento GeoJSON válido como `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Espacial** dá suporte a consultas espaciais (interna e de distância) eficientes. DataType pode ser Point, Polygon ou LineString.

> [!NOTE]
> O Azure Cosmos DB dá suporte à indexação automática de Points, Polygons e LineStrings.
> 
> 

Aqui estão os tipos de índice Olá com suporte e exemplos de consultas que podem ser usado tooserve:

| Tipo de índice | Descrição/caso de uso                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hash       | O hash em /prop/? (ou /) pode ser usado tooserve Olá seguir consultas com eficiência:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Hash em /props/[]/? (ou / ou/propriedades /) pode ser usado tooserve Olá seguir consultas com eficiência:<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| Intervalo      | O intervalo em over /prop/? (ou /) pode ser usado tooserve Olá seguir consultas com eficiência:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| Espacial     | O intervalo em over /prop/? (ou /) pode ser usado tooserve Olá seguir consultas com eficiência:<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --com indexação nos pontos habilitada<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --com indexação em polígonos habilitada              |

Por padrão, um erro será retornado para consultas com operadores de intervalo como > = Se não houver nenhum índice de intervalo (de qualquer precisão) em ordem toosignal que uma verificação pode ser necessário tooserve consulta de saudação. Consultas de intervalo podem ser executadas sem um índice de intervalo usando o cabeçalho x-ms-documentdb-enable-scan Olá Olá API REST ou a opção de solicitação de EnableScanInQuery hello usando Olá .NET SDK. Se houver quaisquer outros filtros na consulta Olá que o banco de dados do Azure Cosmos pode usar o hello índice toofilter contra, nenhum erro será retornado.

Olá mesmas regras se aplicam para consultas espaciais. Por padrão, um erro é retornado para consultas espaciais se não houver nenhum índice espacial e existem outros filtros que podem ser servidos de índice hello. Elas podem ser executadas como um exame usando x-ms-documentdb-enable-scan/EnableScanInQuery.

#### <a name="index-precision"></a>Precisão de índice
A precisão de índice permite definir um equilíbrio entre a sobrecarga de armazenamento de índice e o desempenho da consulta. Para números, é recomendável usar configuração de precisão saudação padrão de -1 ("máximo"). Como os números são 8 bytes em JSON, essa é a configuração de tooa equivalente de 8 bytes. Escolhendo um valor mais baixo de precisão, como 1-7, significa que valores dentro de alguns toohello de mapa de intervalos de mesma entrada de índice. Portanto, você reduzirá o espaço de armazenamento do índice, mas a execução da consulta pode ter tooprocess mais documentos e, consequentemente, consumir mais taxa de transferência, ou seja, unidades de solicitação.

A configuração de precisão do índice tem mais aplicação prática com intervalos de cadeia de caracteres. Como cadeias de caracteres podem ser qualquer comprimento arbitrário, escolha Olá de precisão de índice Olá pode afetar o desempenho de saudação de consultas de intervalo de cadeia de caracteres e a quantidade de saudação do impacto de espaço de armazenamento do índice necessário. Os índices de intervalo de cadeia de caracteres podem ser configurados com 1-100 ou -1 (“máximo”). Se você quiser tooperform Order By consultas em Propriedades de cadeia de caracteres, você deve especificar uma precisão de -1 para caminhos correspondentes hello.

Índices espaciais sempre usam a precisão de índice saudação padrão para todos os tipos (pontos, LineStrings e polígonos) e não podem ser substituída. 

saudação de exemplo a seguir mostra como tooincrease precisão de saudação para intervalo de índices em uma coleção usando o SDK .NET de saudação. 

**Criar uma coleção com uma precisão de índice personalizada**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Banco de dados do Azure Cosmos retornará um erro quando uma consulta usa Order By, mas não tem um índice de intervalo com caminho de saudação consultados com precisão máxima da saudação. 
> 
> 

Da mesma forma, caminhos podem ser excluídos completamente da indexação. Olá próximo exemplo mostra como tooexclude uma seção inteira de saudação documentos (também conhecido como subárvore) de indexação usando hello "*" curinga.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Aceitando e recusando a indexação
Você pode escolher se deseja tooautomatically índice da coleção de saudação todos os documentos. Por padrão, todos os documentos são indexados automaticamente, mas você pode escolher tooturn-la. Quando a indexação estiver desativada, documentos podem ser acessados somente por meio de seus self links ou através de consultas usando um ID.

Com indexação automática desativado, você pode adicionar ainda seletivamente apenas o índice de toohello documentos específicos. Por outro lado, você pode deixar automática de indexação em e escolha seletivamente tooexclude documentos específicos. A indexação de ativar/desativar configurações são úteis quando você tem apenas um subconjunto de documentos que precisam de toobe consultada.

Por exemplo, Olá exemplo a seguir mostra como tooinclude um documento explicitamente usando Olá [SDK .NET do DocumentDB API](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) e hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) propriedade.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Modificando a política de indexação de saudação de uma coleção
Banco de dados do Azure Cosmos permite que você toomake alterações toohello política de indexação de uma coleção em funcionamento hello. Uma alteração na política em uma coleção de banco de dados do Azure Cosmos de indexação pode gerar tooa alteração na forma de saudação do índice Olá incluindo Olá caminhos podem ser indexados, sua precisão, bem como modelo de consistência de saudação do próprio índice hello. Assim, uma alteração na política de indexação, efetivamente requer uma transformação de índice antigo Olá para um novo. 

**Transformações de índice online**

![Como funciona a indexação – Transformações de índice online do Azure Cosmos DB](./media/indexing-policies/index-transformations.png)

Transformações de índice são feitas online, o que significa que documentos hello indexados por política antigo Olá com eficiência são transformados por nova política de saudação **sem afetar a disponibilidade de gravação da saudação ou a taxa de transferência fornecida Olá** de coleção de saudação. Olá consistência de leitura e feitas usando Olá API REST, SDKs de operações de gravação ou de dentro de procedimentos armazenados e gatilhos não é afetado durante a transformação de índice. Isso significa que não há nenhum desempenho aplicativos de tooyour degradação ou tempo de inatividade quando você alterar uma política de indexação.

No entanto, durante o tempo de saudação que a transformação de índice é o andamento, as consultas são finalmente consistentes, independentemente da saudação (consistente ou Lazy) de configuração do modo de indexação. Isso também se aplica a tooqueries de todas as interfaces – API REST, SDKs e no procedimentos armazenados e gatilhos. Assim como com Lazy indexação, transformação de índice é executada de forma assíncrona no plano de fundo de saudação em réplicas de saudação usando recursos de reposição de saudação disponíveis para uma determinada réplica. 

Transformações de índice também ficam **na situ** (no local), ou seja, o banco de dados do Azure Cosmos não mantém duas cópias do hello e troca Olá antigo índice out com hello uma nova. Isso significa que o espaço em disco adicional não será necessário ou consumido em suas coleções durante a execução de transformações de índice.

Quando você alterar a política de indexação, como alterações de saudação são aplicada toomove de saudação antigo índice toohello novo um dependem principalmente Olá configurações do modo de indexação mais para que Olá outros valores como caminhos incluído/excluído, os tipos de índice e precisões. Caso a política antiga e a nova usem a indexação consistente, o Azure Cosmos DB executará uma transformação de índice online. Você não pode aplicar outra alteração de política de indexação com modo de indexação consistente enquanto transformação hello está em andamento.

No entanto, você pode mover tooLazy ou nenhum modo de indexação enquanto uma transformação está em andamento. 

* Quando você move tooLazy, Olá índice política são alteradas efetiva imediatamente e o banco de dados do Azure Cosmos inicia recriar índice de saudação de forma assíncrona. 
* Quando você move tooNone, em seguida, Olá índice é descartado efetiva imediatamente. Movendo tooNone é útil quando você deseja toocancel uma em andamento transformação e iniciar nova com uma política de indexação diferente. 

Se você estiver usando o SDK .NET de hello, pode disparar uma alteração de política de indexação usando Olá novo **ReplaceDocumentCollectionAsync** método e rastrear Olá percentual de andamento da transformação de índice hello usando Olá  **IndexTransformationProgress** propriedade de resposta de um **ReadDocumentCollectionAsync** chamar. Outros SDKs e hello API REST suportam equivalentes propriedades e métodos para fazer alterações de política de indexação.

Aqui está um trecho de código que mostra como uma coleção de toomodify da política de indexação de tooLazy de modo de indexação consistente.

**Modificar a política de indexação de tooLazy consistente**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


Você pode verificar o progresso de saudação de uma transformação de índice por chamada ReadDocumentCollectionAsync, por exemplo, conforme mostrado abaixo.

**Acompanhar o andamento da transformação de índice**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

Você pode descartar o índice de saudação para uma coleção movendo toohello nenhum modo de indexação. Isso pode ser uma ferramenta operacional útil se você quiser toocancel uma transformação em andamento e iniciar um novo imediatamente.

**Descartar índice Olá para uma coleção**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

Quando você faria alterações de política de indexação coleções do banco de dados do Azure Cosmos tooyour? Olá seguem casos de uso mais comuns de saudação:

* Fornecendo resultados consistentes durante a operação normal, mas que retorne toolazy indexação durante a importação de dados em massa
* Começar a usar os novos recursos de indexação no seu banco de dados do Azure Cosmos coleções atual, por exemplo, como geoespaciais consultar que exigem tipo de índice espacial hello, ou Order By / consultas de intervalo que exigem a cadeia de caracteres de saudação tipo de índice de intervalo de cadeia de caracteres
* Selecione de mão Olá toobe propriedades indexada e alterá-los ao longo do tempo
* Ajustar o desempenho da consulta tooimprove precisão indexação ou reduzir o consumo de armazenamento

> [!NOTE]
> toomodify política de indexação usando ReplaceDocumentCollectionAsync, você precisa de versão > = 1.3.0 de saudação SDK .NET
> 
> Para toocomplete de transformação de índice com êxito, você deve garantir que há espaço livre de armazenamento suficiente disponível na coleção de saudação. Se a coleção de saudação atingir sua cota de armazenamento, a transformação de índice Olá será pausada. A transformação do índice será retomada automaticamente quando houver espaço em armazenamento disponível, por exemplo, se você excluir alguns documentos.
> 
> 

## <a name="performance-tuning"></a>Ajuste de desempenho
Olá APIs do DocumentDB fornecem informações sobre métricas de desempenho, como Olá o armazenamento de índice usado e taxa de transferência da saudação (unidades de solicitação) de custo para cada operação. Essas informações pode ser usada toocompare várias políticas de indexação e de ajuste de desempenho.

cota de armazenamento do toocheck hello e uso de uma coleção, executar uma solicitação HEAD ou GET no recurso de coleção hello e inspecionar Olá x-ms-solicitação-quota e cabeçalhos de x-ms-solicitação-usage hello. No SDK .NET de hello, Olá [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) e [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) propriedades [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) contêm esses valores correspondentes .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


sobrecarga de saudação do toomeasure de indexação em cada operação de gravação (criar, atualizar ou excluir), inspecionar o cabeçalho x-ms-taxa de solicitação de hello (ou hello equivalente [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) propriedade [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) em Olá .NET SDK) toomeasure número de saudação de unidades de solicitação consumida por essas operações.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Especificação da política de indexação de toohello de alterações
Uma alteração no esquema de saudação para política de indexação foi introduzida em 7 de julho de 2015 com a API de REST versão 2015-06-03. classe correspondente Olá versões do SDK Olá tem novo esquema de saudação toomatch implementações. 

Olá, as seguintes alterações foram implementada no hello especificação JSON:

* A política de indexação dá suporte a índices de intervalo para cadeias de caracteres
* Cada caminho pode ter várias definições de índice, um para cada tipo de dados
* A indexação de precisão dá suporte a 1-8 para números de 1-100 para cadeias de caracteres e -1 (precisão máxima)
* Segmentos de caminhos não exigem um tooescape aspas duplas cada caminho. Por exemplo, você pode adicionar um caminho /title/? em vez de /"title"/?
* caminho de raiz de saudação que representa "todos os caminhos" pode ser representado como / * (além de muito /)

Se você tiver um código que provisiona coleções com uma política personalizada de indexação gravada com versão 1.1.0 do hello SDK .NET ou anterior, você precisará toochange toohandle de código do seu aplicativo essas alterações na versão de tooSDK ordem toomove 1.2.0. Se você não tiver um código que configura a política de indexação ou planejar toocontinue usando uma versão mais antiga do SDK, nenhuma alteração é necessária.

Para obter uma comparação prática, aqui está um exemplo de política personalizada de indexação escrita usando Olá versão 2015-06-03 da API REST, bem como Olá anterior versão 2015-04-08.

**Política de indexação anterior do JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**Política de indexação atual do JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Próximas etapas
Siga links Olá abaixo para exemplos de política de gerenciamento de índice e toolearn mais sobre a linguagem de consulta do Azure Cosmos DB.

1. [Exemplos de código do Gerenciamento de Índice do .NET na API do DocumentDB](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [Operações de coleção da API REST no DocumentDB](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [Consulta com SQL](documentdb-sql-query.md)

