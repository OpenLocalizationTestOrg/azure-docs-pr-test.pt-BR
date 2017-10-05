---
title: Trabalhando com os dados geoespaciais no Azure Cosmos DB | Microsoft Docs
description: Entenda como criar, indexar e consultar objetos espaciais com o Azure Cosmos DB e a API do DocumentDB.
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="34af4-103">Trabalhando com os dados geoespaciais e de localização do GeoJSON no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="34af4-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="34af4-104">Este artigo é uma introdução à funcionalidade geoespacial do [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="34af4-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="34af4-105">Depois de ler este artigo, você poderá responder as seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="34af4-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="34af4-106">Como fazer para armazenar dados espaciais no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="34af4-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="34af4-107">Como fazer para consultar dados geoespaciais no Azure Cosmos DB, no SQL e no LINQ?</span><span class="sxs-lookup"><span data-stu-id="34af4-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="34af4-108">Como fazer para habilitar ou desabilitar a indexação espacial no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="34af4-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="34af4-109">Este artigo mostra como trabalhar com os dados espaciais com a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="34af4-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="34af4-110">Consulte este [projeto do GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para obter exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="34af4-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="34af4-111">Introdução aos dados espaciais</span><span class="sxs-lookup"><span data-stu-id="34af4-111">Introduction to spatial data</span></span>
<span data-ttu-id="34af4-112">Os dados espaciais descrevem a posição e a forma dos objetos no espaço.</span><span class="sxs-lookup"><span data-stu-id="34af4-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="34af4-113">Na maioria dos aplicativos, eles correspondem aos objetos na Terra, ou seja, dados geoespaciais.</span><span class="sxs-lookup"><span data-stu-id="34af4-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="34af4-114">Os dados espaciais podem ser usados para representar a localização de uma pessoa, um lugar de interesse ou a divisa de uma cidade ou de um lago.</span><span class="sxs-lookup"><span data-stu-id="34af4-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="34af4-115">Com frequência, os casos de uso comum envolvem consultas de proximidade, por exemplo, “encontre todas as cafeterias próximas ao local atual”.</span><span class="sxs-lookup"><span data-stu-id="34af4-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="34af4-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="34af4-116">GeoJSON</span></span>
<span data-ttu-id="34af4-117">O Azure Cosmos DB dá suporte à indexação e à consulta de dados de ponto geoespaciais representados usando a [especificação GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="34af4-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="34af4-118">As estruturas de dados GeoJSON são sempre objetos JSON válidos e, portanto, podem ser armazenadas e consultadas usando o Azure Cosmos DB sem nenhuma ferramenta ou biblioteca especializada.</span><span class="sxs-lookup"><span data-stu-id="34af4-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="34af4-119">Os SDKs do Azure Cosmos DB fornecem classes auxiliares e métodos que facilitam o trabalho com os dados espaciais.</span><span class="sxs-lookup"><span data-stu-id="34af4-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="34af4-120">Pontos, LineStrings e Polígonos</span><span class="sxs-lookup"><span data-stu-id="34af4-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="34af4-121">Um **Ponto** denota uma única posição no espaço.</span><span class="sxs-lookup"><span data-stu-id="34af4-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="34af4-122">Em dados geoespaciais, um Ponto representa o local exato, que poderia ser um endereço de um supermercado, de um quiosque, de um automóvel ou de uma cidade.</span><span class="sxs-lookup"><span data-stu-id="34af4-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="34af4-123">Um ponto é representado no GeoJSON (e no Azure Cosmos DB) usando seu par de coordenadas ou a longitude e a latitude.</span><span class="sxs-lookup"><span data-stu-id="34af4-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="34af4-124">Veja um exemplo JSON para um ponto.</span><span class="sxs-lookup"><span data-stu-id="34af4-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="34af4-125">**Pontos no Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="34af4-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="34af4-126">A especificação de GeoJSON mostra a longitude primeiro e a latitude depois.</span><span class="sxs-lookup"><span data-stu-id="34af4-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="34af4-127">Assim como acontece em outros aplicativos de mapeamento, a longitude e a latitude são ângulos e são representados em graus.</span><span class="sxs-lookup"><span data-stu-id="34af4-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="34af4-128">Os valores de longitude são medidos a partir do Meridiano Principal e estão entre -180,0 e 180,0 graus e os valores de latitude são medidos a partir do Equador e estão entre -90,0 e 90,0 graus.</span><span class="sxs-lookup"><span data-stu-id="34af4-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="34af4-129">O Azure Cosmos DB interpreta coordenadas como representadas de acordo com o sistema de referência WGS-84.</span><span class="sxs-lookup"><span data-stu-id="34af4-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="34af4-130">Consulte abaixo para obter mais detalhes sobre os sistemas de coordenadas de referência.</span><span class="sxs-lookup"><span data-stu-id="34af4-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="34af4-131">Isso pode ser inserido em um documento do Azure Cosmos DB, como mostrado neste exemplo de um perfil do usuário que contém dados de localização:</span><span class="sxs-lookup"><span data-stu-id="34af4-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="34af4-132">**Usar o perfil com a localização armazenada no Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="34af4-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="34af4-133">Além dos pontos, o GeoJSON também dá suporte a LineStrings e a polígonos.</span><span class="sxs-lookup"><span data-stu-id="34af4-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="34af4-134">**LineStrings** representam uma série de dois ou mais pontos no espaço e os segmentos de linha que os conectam.</span><span class="sxs-lookup"><span data-stu-id="34af4-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="34af4-135">Em dados geoespaciais, as LineStrings são comumente usadas para representar vias expressas ou rios.</span><span class="sxs-lookup"><span data-stu-id="34af4-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="34af4-136">Um **Polígono** é um limite de pontos conectados que formam uma LineString fechada.</span><span class="sxs-lookup"><span data-stu-id="34af4-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="34af4-137">Os polígonos são comumente usados para representar formações naturais, como lagos ou jurisdições políticas, como cidades e estados.</span><span class="sxs-lookup"><span data-stu-id="34af4-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="34af4-138">Veja a seguir um exemplo de Polígono no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34af4-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="34af4-139">**Polígonos no GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="34af4-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="34af4-140">A especificação GeoJSON exige que, para Polígonos válidos, o último par de coordenadas fornecido seja igual ao primeiro para criar uma forma fechada.</span><span class="sxs-lookup"><span data-stu-id="34af4-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="34af4-141">Os pontos em um Polígono devem ser especificados no sentido anti-horário.</span><span class="sxs-lookup"><span data-stu-id="34af4-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="34af4-142">Um Polígono especificado no sentido horário representa o inverso da região dentro dele.</span><span class="sxs-lookup"><span data-stu-id="34af4-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="34af4-143">Além de Ponto, LineString e Polígono, o GeoJSON também especifica a representação de como agrupar vários locais geoespaciais, além de como associar propriedades arbitrárias a geolocalização como um **Recurso**.</span><span class="sxs-lookup"><span data-stu-id="34af4-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="34af4-144">Como esses objetos são um JSON válido, todos eles podem ser armazenados e processados no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34af4-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="34af4-145">No entanto, o Azure Cosmos DB dá suporte apenas à indexação automática de pontos.</span><span class="sxs-lookup"><span data-stu-id="34af4-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="34af4-146">Sistemas de referência de coordenadas</span><span class="sxs-lookup"><span data-stu-id="34af4-146">Coordinate reference systems</span></span>
<span data-ttu-id="34af4-147">Como a forma da Terra é irregular, as coordenadas de dados geoespaciais são representadas em muitos sistemas de coordenadas de referência (CRS), cada um com seus próprios quadros de referência e unidades de medida.</span><span class="sxs-lookup"><span data-stu-id="34af4-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="34af4-148">Por exemplo, o "National Grid of Britain" é um sistema de referência muito preciso para o Reino Unido, mas não para fora dele.</span><span class="sxs-lookup"><span data-stu-id="34af4-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="34af4-149">O CRS mais popular em uso hoje é o Sistema Geodésico Mundial [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="34af4-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="34af4-150">Os dispositivos GPS e vários serviços de mapeamento, incluindo as APIs do Google Maps e do Bing Mapas usam WGS-84.</span><span class="sxs-lookup"><span data-stu-id="34af4-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="34af4-151">O Azure Cosmos DB dá suporte à indexação e à consulta de dados geoespaciais usando apenas o CRS WGS-84.</span><span class="sxs-lookup"><span data-stu-id="34af4-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="34af4-152">Criando documentos com dados espaciais</span><span class="sxs-lookup"><span data-stu-id="34af4-152">Creating documents with spatial data</span></span>
<span data-ttu-id="34af4-153">Quando você criar documentos que contenham valores GeoJSON, eles serão automaticamente indexados com um índice espacial de acordo com a política de indexação da coleção.</span><span class="sxs-lookup"><span data-stu-id="34af4-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="34af4-154">Se você estiver trabalhando com um SDK do Azure Cosmos DB em uma linguagem dinamicamente tipada, como Python ou Node.js, deverá criar um GeoJSON válido.</span><span class="sxs-lookup"><span data-stu-id="34af4-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="34af4-155">**Criar documentos com dados geoespaciais no Node.js**</span><span class="sxs-lookup"><span data-stu-id="34af4-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="34af4-156">Se você estiver trabalhando com as APIs do DocumentDB, use as classes `Point` e `Polygon` no namespace `Microsoft.Azure.Documents.Spatial` para inserir informações sobre localização nos objetos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34af4-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="34af4-157">Essas classes ajudam a simplificar a serialização e a desserialização de dados espaciais no GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="34af4-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="34af4-158">**Criar documentos com dados geoespaciais no .NET**</span><span class="sxs-lookup"><span data-stu-id="34af4-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="34af4-159">Se você não tiver as informações de latitude e de longitude, mas se tiver os endereços físicos ou o nome do local, como a cidade ou o país, poderá procurar as coordenadas reais usando um serviço de geocodificação, como os Serviços REST do Bing Mapas.</span><span class="sxs-lookup"><span data-stu-id="34af4-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="34af4-160">Saiba mais sobre a geocodificação do Bing Mapas [aqui](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="34af4-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="34af4-161">Consultando tipos espaciais</span><span class="sxs-lookup"><span data-stu-id="34af4-161">Querying spatial types</span></span>
<span data-ttu-id="34af4-162">Agora que já vimos como inserir dados geoespaciais, vamos dar uma olhada em como consultar esses dados usando o Azure Cosmos DB com o SQL e o LINQ.</span><span class="sxs-lookup"><span data-stu-id="34af4-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="34af4-163">Funções internas espaciais do SQL</span><span class="sxs-lookup"><span data-stu-id="34af4-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="34af4-164">O Azure Cosmos DB dá suporte às funções internas do OGC (Open Geospatial Consortium) a seguir em consultas geoespaciais.</span><span class="sxs-lookup"><span data-stu-id="34af4-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="34af4-165">Para obter mais detalhes sobre o conjunto completo de funções internas na linguagem SQL, consulte [Consultar o Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="34af4-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="34af4-166"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="34af4-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="34af4-167"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="34af4-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="34af4-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="34af4-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="34af4-169">Retorna a distância entre as duas expressões de ponto GeoJSON, Polígono ou LineString.</span><span class="sxs-lookup"><span data-stu-id="34af4-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="34af4-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="34af4-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="34af4-171">Retorna uma expressão booliana que indica se o primeiro objeto GeoJSON (Ponto, Polígono ou LineString) está em um segundo objeto GeoJSON (Ponto, Polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="34af4-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="34af4-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="34af4-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="34af4-173">Retorna uma expressão booliana que indica se os dois objetos GeoJSON especificados (Ponto, Polígono ou LineString) se cruzam.</span><span class="sxs-lookup"><span data-stu-id="34af4-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="34af4-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="34af4-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="34af4-175">Retorna um valor Booliano que indica se a expressão especificada de Ponto, Polígono ou LineString GeoJSON é válida.</span><span class="sxs-lookup"><span data-stu-id="34af4-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="34af4-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="34af4-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="34af4-177">Retorna um valor JSON que contém um valor Booliano caso a expressão especificada de Ponto, Polígono ou LineString GeoJSON é válida e, se for inválida, adicionalmente o motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="34af4-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="34af4-178">As funções espaciais podem ser usadas para executar consultas de proximidade em consultas espaciais.</span><span class="sxs-lookup"><span data-stu-id="34af4-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="34af4-179">Por exemplo, veja uma consulta que retorna todos os documentos de família que estejam em um raio de 30 km do local especificado usando a função interna ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="34af4-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="34af4-180">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="34af4-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="34af4-181">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="34af4-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="34af4-182">Se você incluir a indexação espacial em sua política de indexação, as "consultas de distância" serão servidas com eficiência por meio do índice.</span><span class="sxs-lookup"><span data-stu-id="34af4-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="34af4-183">Para obter mais detalhes sobre a indexação espacial, consulte a seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="34af4-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="34af4-184">Se você não tiver um índice espacial para os caminhos especificados, ainda poderá executar consultas espaciais especificando o cabeçalho da solicitação `x-ms-documentdb-query-enable-scan` com o valor definido como "true".</span><span class="sxs-lookup"><span data-stu-id="34af4-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="34af4-185">No .NET, isso pode ser feito passando o argumento **FeedOptions** opcional para consultas com [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) definido como true.</span><span class="sxs-lookup"><span data-stu-id="34af4-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="34af4-186">ST_WITHIN pode ser usado para verificar se um ponto está dentro de um Polígono.</span><span class="sxs-lookup"><span data-stu-id="34af4-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="34af4-187">Normalmente, os Polígonos são usados para representar limites como códigos postais, fronteiras de estado ou formações naturais.</span><span class="sxs-lookup"><span data-stu-id="34af4-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="34af4-188">Novamente, se você incluir a indexação espacial em sua política de indexação, as consultas "internas" serão servidas com eficiência por meio do índice.</span><span class="sxs-lookup"><span data-stu-id="34af4-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="34af4-189">Os argumentos do polígono no ST_WITHIN podem conter apenas um único toque, ou seja, os Polígonos não devem conter orifícios neles.</span><span class="sxs-lookup"><span data-stu-id="34af4-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="34af4-190">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="34af4-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="34af4-191">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="34af4-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="34af4-192">Da mesma forma como os tipos sem correspondência funcionam na consulta do Azure Cosmos DB, se o valor de localização especificado em um dos argumentos for malformado ou inválido, ele será avaliado como **indefinido** e o documento avaliado será ignorado nos resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="34af4-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="34af4-193">Se sua consulta não retornar resultados, execute ST_ISVALIDDETAILED para depurar o motivo pelo qual o tipo spatail é inválido.</span><span class="sxs-lookup"><span data-stu-id="34af4-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="34af4-194">O Azure Cosmos DB também dá suporte à execução de consultas inversas, ou seja, você pode indexar Polígonos ou linhas no Azure Cosmos DB e, depois, consultar as áreas que contêm um ponto especificado.</span><span class="sxs-lookup"><span data-stu-id="34af4-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="34af4-195">Esse padrão é normalmente usado em logística para identificar, por exemplo, quando um caminhão entra ou sai de uma determinada área.</span><span class="sxs-lookup"><span data-stu-id="34af4-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="34af4-196">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="34af4-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="34af4-197">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="34af4-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="34af4-198">ST_ISVALID e ST_ISVALIDDETAILED podem ser usados para verificar se um objeto espacial é válido.</span><span class="sxs-lookup"><span data-stu-id="34af4-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="34af4-199">Por exemplo, a consulta a seguir verifica a validade de um ponto com um valor de latitude fora do intervalo (-132,8).</span><span class="sxs-lookup"><span data-stu-id="34af4-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="34af4-200">ST_ISVALID retorna um valor Booliano e ST_ISVALIDDETAILED retorna o Booliano e uma cadeia de caracteres com o motivo pelo qual ele é considerado inválido.</span><span class="sxs-lookup"><span data-stu-id="34af4-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="34af4-201">** Consulta **</span><span class="sxs-lookup"><span data-stu-id="34af4-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="34af4-202">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="34af4-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="34af4-203">Essas funções também podem ser usadas para validar Polígonos.</span><span class="sxs-lookup"><span data-stu-id="34af4-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="34af4-204">Por exemplo, ST_ISVALIDDETAILED é usado aqui para validar um Polígono que não está fechado.</span><span class="sxs-lookup"><span data-stu-id="34af4-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="34af4-205">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="34af4-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="34af4-206">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="34af4-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="34af4-207">Consultas LINQ no SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="34af4-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="34af4-208">O SDK do .NET do DocumentDB também fornece métodos stub `Distance()` e `Within()` para uso em expressões LINQ.</span><span class="sxs-lookup"><span data-stu-id="34af4-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="34af4-209">O provedor LINQ do DocumentDB traduz essas chamadas do método nas chamadas de função internas do SQL equivalentes (ST_DISTANCE e ST_WITHIN, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="34af4-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="34af4-210">Veja um exemplo de uma consulta LINQ que localiza todos os documentos da coleção do Azure Cosmos DB cujo valor de “localização” está em um raio de 30 km do ponto especificado usando o LINQ.</span><span class="sxs-lookup"><span data-stu-id="34af4-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="34af4-211">**Consulta LINQ para distância**</span><span class="sxs-lookup"><span data-stu-id="34af4-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="34af4-212">Da mesma forma, veja uma consulta para localizar todos os documentos cuja "localização" seja o interior da caixa/Polígono especificada.</span><span class="sxs-lookup"><span data-stu-id="34af4-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="34af4-213">**Consulta LINQ para dentro**</span><span class="sxs-lookup"><span data-stu-id="34af4-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="34af4-214">Agora que já vimos como consultar documentos usando o LINQ e o SQL, vamos dar uma olhada em como configurar o Azure Cosmos DB para indexação espacial.</span><span class="sxs-lookup"><span data-stu-id="34af4-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="34af4-215">Indexação</span><span class="sxs-lookup"><span data-stu-id="34af4-215">Indexing</span></span>
<span data-ttu-id="34af4-216">Como descrevemos no documento [Indexação independente de esquema com o Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf), projetamos o mecanismo de banco de dados do Azure Cosmos DB para ser verdadeiramente independente de esquema e fornecer suporte de primeira classe ao JSON.</span><span class="sxs-lookup"><span data-stu-id="34af4-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="34af4-217">O mecanismo de banco de dados otimizado para gravação do Azure Cosmos DB também entende nativamente os dados espaciais (pontos, Polígonos e linhas) representados no padrão GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="34af4-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="34af4-218">Em resumo, a geometria é projetada a partir de coordenadas geodésicas em um plano 2D e então dividida progressivamente em células usando um **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="34af4-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="34af4-219">Essas células são mapeadas para 1D com base na localização da célula em uma **curva de preenchimento de espaço de Hilbert**, que preserva a localidade de pontos.</span><span class="sxs-lookup"><span data-stu-id="34af4-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="34af4-220">Além disso, quando os dados de localização são indexados, eles passam por um processo conhecido como **mosaico**, ou seja, todas as células que interseccionam uma localização são identificadas e armazenadas como chaves no índice do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34af4-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="34af4-221">No momento da consulta, argumentos como pontos e Polígonos também são incluídos no mosaico para extrair os intervalos de IDs de célula relevantes e usados para recuperar dados do índice.</span><span class="sxs-lookup"><span data-stu-id="34af4-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="34af4-222">Se você especificar uma política de indexação que inclua o índice espacial para /* (todos os caminhos), todos os pontos encontrados na coleção serão indexados para consultas espaciais eficientes (ST_WITHIN e ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="34af4-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="34af4-223">Os índices espaciais não têm um valor de precisão e sempre usam um valor de precisão padrão.</span><span class="sxs-lookup"><span data-stu-id="34af4-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="34af4-224">O Azure Cosmos DB dá suporte à indexação automática de Points, Polygons e LineStrings</span><span class="sxs-lookup"><span data-stu-id="34af4-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="34af4-225">O trecho JSON a seguir mostra uma política de indexação com indexação espacial habilitada, ou seja, qualquer ponto GeoJSON encontrado em documentos para consultas espaciais do índice.</span><span class="sxs-lookup"><span data-stu-id="34af4-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="34af4-226">Se você estiver modificando a política de indexação usando o Portal do Azure, poderá especificar o JSON a seguir para a política de indexação para habilitar a indexação espacial em sua coleção.</span><span class="sxs-lookup"><span data-stu-id="34af4-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="34af4-227">**JSON da política de indexação da coleção com espacial habilitado para pontos e Polígonos**</span><span class="sxs-lookup"><span data-stu-id="34af4-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="34af4-228">Veja um trecho de código no .NET que mostra como criar uma coleção com indexação espacial ativado para todos os caminhos que contenham pontos.</span><span class="sxs-lookup"><span data-stu-id="34af4-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="34af4-229">**Criar uma coleção com indexação espacial**</span><span class="sxs-lookup"><span data-stu-id="34af4-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="34af4-230">E veja como você pode modificar uma coleção existente para aproveitar a indexação espacial em quaisquer pontos armazenados em documentos.</span><span class="sxs-lookup"><span data-stu-id="34af4-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="34af4-231">**Modificar uma coleção existente com indexação espacial**</span><span class="sxs-lookup"><span data-stu-id="34af4-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="34af4-232">Se o valor GeoJSON de localização no documento estiver malformado ou inválido, então ele não será indexado para consultas espaciais.</span><span class="sxs-lookup"><span data-stu-id="34af4-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="34af4-233">Você pode validar valores de localização usando ST_ISVALID e ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="34af4-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="34af4-234">Caso sua definição de coleção inclua uma chave de partição, o andamento da transformação de indexação não será relatado.</span><span class="sxs-lookup"><span data-stu-id="34af4-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="34af4-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="34af4-235">Next steps</span></span>
<span data-ttu-id="34af4-236">Agora que você aprendeu a usar o suporte geoespacial no Azure Cosmos DB, poderá:</span><span class="sxs-lookup"><span data-stu-id="34af4-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="34af4-237">Começar a codificar com os [exemplos de código geoespacial .NET no GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="34af4-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="34af4-238">Experimente as consultas geoespaciais no [Espaço de Consulta do Azure Cosmos DB](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="34af4-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="34af4-239">Saiba mais sobre a [Consulta do Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="34af4-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="34af4-240">Saiba mais sobre as [Políticas de indexação do Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="34af4-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

