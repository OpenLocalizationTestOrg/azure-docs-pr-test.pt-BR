---
title: aaaWorking com dados geoespaciais no banco de dados do Azure Cosmos | Microsoft Docs
description: "Entenda como toocreate, índice e consultar objetos espaciais com o banco de dados do Azure Cosmos e Olá API DocumentDB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Trabalhando com os dados geoespaciais e de localização do GeoJSON no Azure Cosmos DB
Este artigo é uma introdução toohello geoespaciais funcionalidade [o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Depois de ler isso, você será capaz de tooanswer Olá perguntas a seguir:

* Como fazer para armazenar dados espaciais no Azure Cosmos DB?
* Como fazer para consultar dados geoespaciais no Azure Cosmos DB, no SQL e no LINQ?
* Como fazer para habilitar ou desabilitar a indexação espacial no Azure Cosmos DB?

Este artigo mostra como toowork com dados espaciais Olá API DocumentDB. Consulte este [projeto do GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para obter exemplos de código.

## <a name="introduction-toospatial-data"></a>Dados de toospatial de Introdução
Dados espaciais descrevem a posição de saudação e a forma de objetos no espaço. Na maioria dos aplicativos, elas correspondem tooobjects na Terra hello, ou seja, os dados geoespaciais. Dados espaciais podem ser usados toorepresent Olá local de uma pessoa, lugar de interesse ou limite de saudação de uma cidade ou um lake. Com frequência, os casos de uso comum envolvem consultas de proximidade, por exemplo, “encontre todas as cafeterias próximas ao local atual”. 

### <a name="geojson"></a>GeoJSON
Banco de dados do Azure Cosmos dá suporte à indexação e consulta de dados geoespaciais do ponto que são representados usando Olá [GeoJSON especificação](https://tools.ietf.org/html/rfc7946). As estruturas de dados GeoJSON são sempre objetos JSON válidos e, portanto, podem ser armazenadas e consultadas usando o Azure Cosmos DB sem nenhuma ferramenta ou biblioteca especializada. Olá SDKs do banco de dados do Azure Cosmos fornecem classes auxiliares e métodos que tornam mais fácil toowork com dados espaciais. 

### <a name="points-linestrings-and-polygons"></a>Pontos, LineStrings e Polígonos
Um **Ponto** denota uma única posição no espaço. Em dados geoespaciais, um ponto representa o local exato hello, que pode ser um endereço de uma mercearia, um quiosque, um automóvel ou uma cidade.  Um ponto é representado no GeoJSON (e no Azure Cosmos DB) usando seu par de coordenadas ou a longitude e a latitude. Veja um exemplo JSON para um ponto.

**Pontos no Azure Cosmos DB**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Olá especificação GeoJSON Especifica a longitude primeiro e latitude segundo. Assim como acontece em outros aplicativos de mapeamento, a longitude e a latitude são ângulos e são representados em graus. Valores de longitude são medidos da saudação Meridiano e estão entre -180 e 180.0 graus e latitude valores medidos a partir do Equador hello e estão entre -90,0 e 90,0 graus. 
> 
> Banco de dados do Azure Cosmos interpreta as coordenadas conforme representado por um sistema de referência de WGS 84 hello. Consulte abaixo para obter mais detalhes sobre os sistemas de coordenadas de referência.
> 
> 

Isso pode ser inserido em um documento do Azure Cosmos DB, como mostrado neste exemplo de um perfil do usuário que contém dados de localização:

**Usar o perfil com a localização armazenada no Azure Cosmos DB**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

Além disso toopoints, GeoJSON também suporta LineStrings e polígonos. **LineStrings** representar uma série de dois ou mais pontos no espaço e Olá segmentos de linha que se conectam a eles. Em dados geoespaciais, LineStrings são vias toorepresent usadas expressas ou rios. Um **Polígono** é um limite de pontos conectados que formam uma LineString fechada. Polígonos são formações natural de toorepresent usadas como Lagos ou políticas jurisdições como estados e cidades. Veja a seguir um exemplo de Polígono no Azure Cosmos DB. 

**Polígonos no GeoJSON**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Olá GeoJSON especificação requer que para polígonos válidos, hello último par de coordenadas fornecido deve ser Olá mesmo como Olá primeiro, toocreate uma forma fechada.
> 
> Os pontos em um Polígono devem ser especificados no sentido anti-horário. Um polígono especificado na ordem no sentido horário representa inverso de saudação da região hello dentro dele.
> 
> 

Adição tooPoint, LineString e polígono, GeoJSON também especifica a representação hello como toogroup vários locais de geoespaciais, bem como a propriedades arbitrárias tooassociate com localização geográfica como uma **recurso**. Como esses objetos são um JSON válido, todos eles podem ser armazenados e processados no Azure Cosmos DB. No entanto, o Azure Cosmos DB dá suporte apenas à indexação automática de pontos.

### <a name="coordinate-reference-systems"></a>Sistemas de referência de coordenadas
Como forma de saudação da Terra Olá irregular, coordenadas de dados geoespaciais são representados em muitos sistemas de coordenadas de referência (CRS), cada um com seus próprios quadros de referência e as unidades de medida. Por exemplo, hello "National grade de Britain" é um sistema de referência é bastante preciso para Olá Reino Unido, mas não fora dele. 

Olá CRS mais populares em uso hoje é hello World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Os dispositivos GPS e vários serviços de mapeamento, incluindo as APIs do Google Maps e do Bing Mapas usam WGS-84. Banco de dados do Azure Cosmos dá suporte à indexação e consulta de dados geoespaciais usando Olá WGS 84 CRS somente. 

## <a name="creating-documents-with-spatial-data"></a>Criando documentos com dados espaciais
Quando você cria documentos que contêm valores de GeoJSON, eles são automaticamente indexados com um índice espacial na política de indexação toohello acordo de coleção de saudação. Se você estiver trabalhando com um SDK do Azure Cosmos DB em uma linguagem dinamicamente tipada, como Python ou Node.js, deverá criar um GeoJSON válido.

**Criar documentos com dados geoespaciais no Node.js**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Se você estiver trabalhando com hello APIs do DocumentDB, você pode usar o hello `Point` e `Polygon` classes Olá `Microsoft.Azure.Documents.Spatial` informações de localização do namespace tooembed dentro de seus objetos de aplicativo. Essas classes ajudam a simplificar a serialização de saudação e a desserialização de dados espaciais em GeoJSON.

**Criar documentos com dados geoespaciais no .NET**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Se você não tem informações de latitude e longitude hello, mas ter endereços físicos de saudação ou o nome do local como cidade ou país, você pode procurar coordenadas real hello usando um serviço de geocodificação como serviços REST do Bing Maps. Saiba mais sobre a geocodificação do Bing Mapas [aqui](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Consultando tipos espaciais
Agora que estamos dando uma olhada em como dados geoespaciais de tooinsert, vamos dar uma olhada em como tooquery esses dados usando o banco de dados do Cosmos do Azure usando o SQL e o LINQ.

### <a name="spatial-sql-built-in-functions"></a>Funções internas espaciais do SQL
Banco de dados do Azure Cosmos dá suporte a saudação funções internas do Open Geospatial Consortium (OGC) para consultar geoespaciais a seguir. Para obter mais detalhes sobre o conjunto completo de saudação de funções internas em Olá linguagem SQL, consulte muito[consulta Azure Cosmos DB](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Uso</strong></td>
  <td><strong>Descrição</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Retorna a distância de saudação entre expressões de LineString, Polygon ou ponto GeoJSON Olá dois.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Retorna uma expressão booleana que indica se o objeto de GeoJSON primeiro Olá (ponto, polígono ou LineString) é no objeto de GeoJSON segundo hello (ponto, polígono ou LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Retorna uma expressão booleana que indica se cruzam Olá dois GeoJSON objetos especificados (ponto, polígono ou LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Retorna um valor booliano que indica se a saudação especificado LineString, Polygon ou ponto GeoJSON expressão é válida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Retorna um valor JSON que contém um valor booliano se Olá especificado expressão LineString, Polygon ou ponto GeoJSON é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.</td>
</tr>
</table>

Funções espaciais podem ser usado tooperform proximidade consultas em relação aos dados espaciais. Por exemplo, aqui está uma consulta que retorna a que família de todos os documentos que está dentro de 30 km de saudação local especificado usando Olá ST_DISTANCE função interna. 

**Consulta**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Se você incluir indexação espacial em sua política de indexação, em seguida, "consultas distância" serão servidas com eficiência por meio do índice de saudação. Para obter mais detalhes sobre indexação espacial, consulte seção hello. Se você não tiver um índice de saudação especificado caminhos, você ainda pode executar consultas espaciais, especificando `x-ms-documentdb-query-enable-scan` cabeçalho de solicitação com valor de saudação definido muito "true". No .NET, isso pode ser feito por passando Olá opcional **FeedOptions** tooqueries argumento com [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) definir tootrue. 

ST_WITHIN pode ser usado toocheck se um ponto está dentro de um polígono. Geralmente polígonos são limites de toorepresent usado como códigos postais, limites de estado ou formações naturais. Novamente se você incluir indexação espacial em sua política de indexação, em seguida, "em" consultas serão servidas com eficiência por meio do índice de saudação. 

Argumentos do polígono ST_WITHIN podem conter apenas um único toque, ou seja, Olá polígonos não deve conter buracos neles. 

**Consulta**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Resultados**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Tipos semelhantes de toohow incompatível funciona na consulta de banco de dados do Azure Cosmos se Olá local valor especificado em um argumento está malformado ou inválido, ela será avaliada muito**indefinido** e ignorados Olá avaliada documento toobe de saudação resultados da consulta. Se sua consulta não retornar resultados, execute toodebug ST_ISVALIDDETAILED por que o tipo de spatail Olá é inválido.     
> 
> 

Banco de dados do Azure Cosmos também oferece suporte ao realizar consultas inversas, ou seja, você pode indexar polígonos ou linhas no banco de dados do Azure Cosmos de consulta para as áreas de saudação que contenham um ponto especificado. Esse padrão é normalmente usado em logística tooidentify, por exemplo, quando um caminhão entra ou sai de uma determinada área. 

**Consulta**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Resultados**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID e ST_ISVALIDDETAILED podem ser usado toocheck se um objeto espacial é válido. Por exemplo, Olá consulta a seguir verifica validade Olá de um ponto com um limite de valor de latitude de intervalo (-132.8). ST_ISVALID retorna apenas um valor booliano e retorna ST_ISVALIDDETAILED Olá booliano e uma cadeia de caracteres que contém a razão Olá por que ele é considerado inválido.

** Consulta **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Resultados**

    [{
      "$1": false
    }]

Essas funções também podem ser usado toovalidate polígonos. Por exemplo, aqui usamos ST_ISVALIDDETAILED toovalidate um polígono que não está fechado. 

**Consulta**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Resultados**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>Consulta LINQ em Olá SDK .NET
Olá SDK .NET do DocumentDB também provedores stub métodos `Distance()` e `Within()` para uso em expressões LINQ. provedor LINQ DocumentDB Hello converte essas chamadas toohello equivalente SQL função interna chamadas de método (ST_DISTANCE e ST_WITHIN respectivamente). 

Aqui está um exemplo de uma consulta LINQ que localiza todos os documentos na coleção de banco de dados do Azure Cosmos Olá cujo valor de "local" está dentro de um raio de 30km de saudação especificado ponto usando LINQ.

**Consulta LINQ para distância**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Da mesma forma, aqui está uma consulta para localizar todos os documentos de saudação cujo "local" está dentro de saudação especificado caixa/polígono. 

**Consulta LINQ para dentro**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Agora que estamos dando uma olhada em como tooquery documentos usando LINQ e SQL, vamos dar uma olhada em como tooconfigure Azure Cosmos DB para indexação espacial.

## <a name="indexing"></a>Indexação
Conforme descrito na Olá [indexação independente de esquema com o banco de dados do Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papel, criamos o toobe de mecanismo de banco de dados do Azure Cosmos DB verdadeiramente independente de esquema e fornecer suporte de primeira classe para JSON. mecanismo de banco de dados de gravação otimizada saudação do banco de dados do Azure Cosmos nativamente compreende dados espaciais (pontos, linhas e polígonos) representados no padrão de GeoJSON hello.

Em resumo, geometry Olá for projetado de coordenadas geodésicos em um plano 2D, progressivamente dividido em células usando um **quadtree**. Essas células são mapeadas too1D com base na localização de saudação de célula de saudação em uma **curva de preenchimento de espaço de Hilbert**, que preserva a localidade de pontos. Além disso quando os dados de local são indexados, ele passa por um processo conhecido como **mosaico**, ou seja, todas as células de saudação que interceptam um local são identificadas e armazenadas como chaves de índice de banco de dados do Azure Cosmos hello. No momento da consulta, argumentos como pontos e polígonos também estão incluídas no mosaico tooextract Olá intervalos de ID de célula relevantes e tooretrieve dados do índice Olá usados.

Se você especificar uma política de indexação que inclui o índice espacial para / * (todos os caminhos), em seguida, todos os pontos de encontrado na coleção de saudação são indexados para consultas espaciais eficientes (ST_WITHIN e ST_DISTANCE). Os índices espaciais não têm um valor de precisão e sempre usam um valor de precisão padrão.

> [!NOTE]
> O Azure Cosmos DB dá suporte à indexação automática de Points, Polygons e LineStrings
> 
> 

Olá trecho JSON a seguir mostra uma política de indexação com indexação espacial habilitado, ou seja, qualquer ponto GeoJSON encontrado em documentos de consulta espacial do índice. Se você estiver modificando Olá indexação política usando Olá Portal do Azure, você pode especificar Olá JSON a seguir para indexação de política tooenable espacial indexação em sua coleção.

**JSON da política de indexação da coleção com espacial habilitado para pontos e Polígonos**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Aqui está um trecho de código no .NET que mostra como toocreate uma coleção com indexação espacial ativado para todos os caminhos que contenham pontos. 

**Criar uma coleção com indexação espacial**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

E aqui está como você pode modificar uma vantagem de tootake de coleção existente de indexação espacial quaisquer pontos que são armazenados dentro de documentos.

**Modificar uma coleção existente com indexação espacial**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Se o local de saudação GeoJSON valor dentro do documento hello estiver malformado ou inválido, em seguida, ele será não obter indexado para consultar espacial. Você pode validar valores de localização usando ST_ISVALID e ST_ISVALIDDETAILED.
> 
> Caso sua definição de coleção inclua uma chave de partição, o andamento da transformação de indexação não será relatado. 
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora que você já learnt sobre como tooget iniciada com o suporte de geoespaciais no banco de dados do Azure Cosmos, você pode:

* Iniciar a codificação com hello [exemplos de código geoespaciais .NET no GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Obter ponteiros em com geoespaciais consultando a saudação [parque de consulta de banco de dados do Azure Cosmos](http://www.documentdb.com/sql/demo#geospatial)
* Saiba mais sobre a [Consulta do Azure Cosmos DB](documentdb-sql-query.md)
* Saiba mais sobre as [Políticas de indexação do Azure Cosmos DB](indexing-policies.md)

