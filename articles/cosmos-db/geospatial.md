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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="73211-103">Trabalhando com os dados geoespaciais e de localização do GeoJSON no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="73211-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="73211-104">Este artigo é uma introdução toohello geoespaciais funcionalidade [o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="73211-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="73211-105">Depois de ler isso, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="73211-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="73211-106">Como fazer para armazenar dados espaciais no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="73211-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="73211-107">Como fazer para consultar dados geoespaciais no Azure Cosmos DB, no SQL e no LINQ?</span><span class="sxs-lookup"><span data-stu-id="73211-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="73211-108">Como fazer para habilitar ou desabilitar a indexação espacial no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="73211-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="73211-109">Este artigo mostra como toowork com dados espaciais Olá API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="73211-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="73211-110">Consulte este [projeto do GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) para obter exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="73211-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="73211-111">Dados de toospatial de Introdução</span><span class="sxs-lookup"><span data-stu-id="73211-111">Introduction toospatial data</span></span>
<span data-ttu-id="73211-112">Dados espaciais descrevem a posição de saudação e a forma de objetos no espaço.</span><span class="sxs-lookup"><span data-stu-id="73211-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="73211-113">Na maioria dos aplicativos, elas correspondem tooobjects na Terra hello, ou seja, os dados geoespaciais.</span><span class="sxs-lookup"><span data-stu-id="73211-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="73211-114">Dados espaciais podem ser usados toorepresent Olá local de uma pessoa, lugar de interesse ou limite de saudação de uma cidade ou um lake.</span><span class="sxs-lookup"><span data-stu-id="73211-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="73211-115">Com frequência, os casos de uso comum envolvem consultas de proximidade, por exemplo, “encontre todas as cafeterias próximas ao local atual”.</span><span class="sxs-lookup"><span data-stu-id="73211-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="73211-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="73211-116">GeoJSON</span></span>
<span data-ttu-id="73211-117">Banco de dados do Azure Cosmos dá suporte à indexação e consulta de dados geoespaciais do ponto que são representados usando Olá [GeoJSON especificação](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="73211-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="73211-118">As estruturas de dados GeoJSON são sempre objetos JSON válidos e, portanto, podem ser armazenadas e consultadas usando o Azure Cosmos DB sem nenhuma ferramenta ou biblioteca especializada.</span><span class="sxs-lookup"><span data-stu-id="73211-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="73211-119">Olá SDKs do banco de dados do Azure Cosmos fornecem classes auxiliares e métodos que tornam mais fácil toowork com dados espaciais.</span><span class="sxs-lookup"><span data-stu-id="73211-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="73211-120">Pontos, LineStrings e Polígonos</span><span class="sxs-lookup"><span data-stu-id="73211-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="73211-121">Um **Ponto** denota uma única posição no espaço.</span><span class="sxs-lookup"><span data-stu-id="73211-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="73211-122">Em dados geoespaciais, um ponto representa o local exato hello, que pode ser um endereço de uma mercearia, um quiosque, um automóvel ou uma cidade.</span><span class="sxs-lookup"><span data-stu-id="73211-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="73211-123">Um ponto é representado no GeoJSON (e no Azure Cosmos DB) usando seu par de coordenadas ou a longitude e a latitude.</span><span class="sxs-lookup"><span data-stu-id="73211-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="73211-124">Veja um exemplo JSON para um ponto.</span><span class="sxs-lookup"><span data-stu-id="73211-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="73211-125">**Pontos no Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="73211-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="73211-126">Olá especificação GeoJSON Especifica a longitude primeiro e latitude segundo.</span><span class="sxs-lookup"><span data-stu-id="73211-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="73211-127">Assim como acontece em outros aplicativos de mapeamento, a longitude e a latitude são ângulos e são representados em graus.</span><span class="sxs-lookup"><span data-stu-id="73211-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="73211-128">Valores de longitude são medidos da saudação Meridiano e estão entre -180 e 180.0 graus e latitude valores medidos a partir do Equador hello e estão entre -90,0 e 90,0 graus.</span><span class="sxs-lookup"><span data-stu-id="73211-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="73211-129">Banco de dados do Azure Cosmos interpreta as coordenadas conforme representado por um sistema de referência de WGS 84 hello.</span><span class="sxs-lookup"><span data-stu-id="73211-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="73211-130">Consulte abaixo para obter mais detalhes sobre os sistemas de coordenadas de referência.</span><span class="sxs-lookup"><span data-stu-id="73211-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="73211-131">Isso pode ser inserido em um documento do Azure Cosmos DB, como mostrado neste exemplo de um perfil do usuário que contém dados de localização:</span><span class="sxs-lookup"><span data-stu-id="73211-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="73211-132">**Usar o perfil com a localização armazenada no Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="73211-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="73211-133">Além disso toopoints, GeoJSON também suporta LineStrings e polígonos.</span><span class="sxs-lookup"><span data-stu-id="73211-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="73211-134">**LineStrings** representar uma série de dois ou mais pontos no espaço e Olá segmentos de linha que se conectam a eles.</span><span class="sxs-lookup"><span data-stu-id="73211-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="73211-135">Em dados geoespaciais, LineStrings são vias toorepresent usadas expressas ou rios.</span><span class="sxs-lookup"><span data-stu-id="73211-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="73211-136">Um **Polígono** é um limite de pontos conectados que formam uma LineString fechada.</span><span class="sxs-lookup"><span data-stu-id="73211-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="73211-137">Polígonos são formações natural de toorepresent usadas como Lagos ou políticas jurisdições como estados e cidades.</span><span class="sxs-lookup"><span data-stu-id="73211-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="73211-138">Veja a seguir um exemplo de Polígono no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="73211-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="73211-139">**Polígonos no GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="73211-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="73211-140">Olá GeoJSON especificação requer que para polígonos válidos, hello último par de coordenadas fornecido deve ser Olá mesmo como Olá primeiro, toocreate uma forma fechada.</span><span class="sxs-lookup"><span data-stu-id="73211-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="73211-141">Os pontos em um Polígono devem ser especificados no sentido anti-horário.</span><span class="sxs-lookup"><span data-stu-id="73211-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="73211-142">Um polígono especificado na ordem no sentido horário representa inverso de saudação da região hello dentro dele.</span><span class="sxs-lookup"><span data-stu-id="73211-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="73211-143">Adição tooPoint, LineString e polígono, GeoJSON também especifica a representação hello como toogroup vários locais de geoespaciais, bem como a propriedades arbitrárias tooassociate com localização geográfica como uma **recurso**.</span><span class="sxs-lookup"><span data-stu-id="73211-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="73211-144">Como esses objetos são um JSON válido, todos eles podem ser armazenados e processados no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="73211-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="73211-145">No entanto, o Azure Cosmos DB dá suporte apenas à indexação automática de pontos.</span><span class="sxs-lookup"><span data-stu-id="73211-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="73211-146">Sistemas de referência de coordenadas</span><span class="sxs-lookup"><span data-stu-id="73211-146">Coordinate reference systems</span></span>
<span data-ttu-id="73211-147">Como forma de saudação da Terra Olá irregular, coordenadas de dados geoespaciais são representados em muitos sistemas de coordenadas de referência (CRS), cada um com seus próprios quadros de referência e as unidades de medida.</span><span class="sxs-lookup"><span data-stu-id="73211-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="73211-148">Por exemplo, hello "National grade de Britain" é um sistema de referência é bastante preciso para Olá Reino Unido, mas não fora dele.</span><span class="sxs-lookup"><span data-stu-id="73211-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="73211-149">Olá CRS mais populares em uso hoje é hello World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="73211-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="73211-150">Os dispositivos GPS e vários serviços de mapeamento, incluindo as APIs do Google Maps e do Bing Mapas usam WGS-84.</span><span class="sxs-lookup"><span data-stu-id="73211-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="73211-151">Banco de dados do Azure Cosmos dá suporte à indexação e consulta de dados geoespaciais usando Olá WGS 84 CRS somente.</span><span class="sxs-lookup"><span data-stu-id="73211-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="73211-152">Criando documentos com dados espaciais</span><span class="sxs-lookup"><span data-stu-id="73211-152">Creating documents with spatial data</span></span>
<span data-ttu-id="73211-153">Quando você cria documentos que contêm valores de GeoJSON, eles são automaticamente indexados com um índice espacial na política de indexação toohello acordo de coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="73211-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="73211-154">Se você estiver trabalhando com um SDK do Azure Cosmos DB em uma linguagem dinamicamente tipada, como Python ou Node.js, deverá criar um GeoJSON válido.</span><span class="sxs-lookup"><span data-stu-id="73211-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="73211-155">**Criar documentos com dados geoespaciais no Node.js**</span><span class="sxs-lookup"><span data-stu-id="73211-155">**Create Document with Geospatial data in Node.js**</span></span>

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

<span data-ttu-id="73211-156">Se você estiver trabalhando com hello APIs do DocumentDB, você pode usar o hello `Point` e `Polygon` classes Olá `Microsoft.Azure.Documents.Spatial` informações de localização do namespace tooembed dentro de seus objetos de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73211-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="73211-157">Essas classes ajudam a simplificar a serialização de saudação e a desserialização de dados espaciais em GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="73211-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="73211-158">**Criar documentos com dados geoespaciais no .NET**</span><span class="sxs-lookup"><span data-stu-id="73211-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="73211-159">Se você não tem informações de latitude e longitude hello, mas ter endereços físicos de saudação ou o nome do local como cidade ou país, você pode procurar coordenadas real hello usando um serviço de geocodificação como serviços REST do Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="73211-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="73211-160">Saiba mais sobre a geocodificação do Bing Mapas [aqui](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="73211-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="73211-161">Consultando tipos espaciais</span><span class="sxs-lookup"><span data-stu-id="73211-161">Querying spatial types</span></span>
<span data-ttu-id="73211-162">Agora que estamos dando uma olhada em como dados geoespaciais de tooinsert, vamos dar uma olhada em como tooquery esses dados usando o banco de dados do Cosmos do Azure usando o SQL e o LINQ.</span><span class="sxs-lookup"><span data-stu-id="73211-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="73211-163">Funções internas espaciais do SQL</span><span class="sxs-lookup"><span data-stu-id="73211-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="73211-164">Banco de dados do Azure Cosmos dá suporte a saudação funções internas do Open Geospatial Consortium (OGC) para consultar geoespaciais a seguir.</span><span class="sxs-lookup"><span data-stu-id="73211-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="73211-165">Para obter mais detalhes sobre o conjunto completo de saudação de funções internas em Olá linguagem SQL, consulte muito[consulta Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="73211-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="73211-166"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="73211-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="73211-167"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="73211-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="73211-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="73211-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="73211-169">Retorna a distância de saudação entre expressões de LineString, Polygon ou ponto GeoJSON Olá dois.</span><span class="sxs-lookup"><span data-stu-id="73211-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="73211-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="73211-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="73211-171">Retorna uma expressão booleana que indica se o objeto de GeoJSON primeiro Olá (ponto, polígono ou LineString) é no objeto de GeoJSON segundo hello (ponto, polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="73211-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="73211-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="73211-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="73211-173">Retorna uma expressão booleana que indica se cruzam Olá dois GeoJSON objetos especificados (ponto, polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="73211-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="73211-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="73211-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="73211-175">Retorna um valor booliano que indica se a saudação especificado LineString, Polygon ou ponto GeoJSON expressão é válida.</span><span class="sxs-lookup"><span data-stu-id="73211-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="73211-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="73211-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="73211-177">Retorna um valor JSON que contém um valor booliano se Olá especificado expressão LineString, Polygon ou ponto GeoJSON é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="73211-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="73211-178">Funções espaciais podem ser usado tooperform proximidade consultas em relação aos dados espaciais.</span><span class="sxs-lookup"><span data-stu-id="73211-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="73211-179">Por exemplo, aqui está uma consulta que retorna a que família de todos os documentos que está dentro de 30 km de saudação local especificado usando Olá ST_DISTANCE função interna.</span><span class="sxs-lookup"><span data-stu-id="73211-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="73211-180">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="73211-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="73211-181">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="73211-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="73211-182">Se você incluir indexação espacial em sua política de indexação, em seguida, "consultas distância" serão servidas com eficiência por meio do índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="73211-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="73211-183">Para obter mais detalhes sobre indexação espacial, consulte seção hello.</span><span class="sxs-lookup"><span data-stu-id="73211-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="73211-184">Se você não tiver um índice de saudação especificado caminhos, você ainda pode executar consultas espaciais, especificando `x-ms-documentdb-query-enable-scan` cabeçalho de solicitação com valor de saudação definido muito "true".</span><span class="sxs-lookup"><span data-stu-id="73211-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="73211-185">No .NET, isso pode ser feito por passando Olá opcional **FeedOptions** tooqueries argumento com [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) definir tootrue.</span><span class="sxs-lookup"><span data-stu-id="73211-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="73211-186">ST_WITHIN pode ser usado toocheck se um ponto está dentro de um polígono.</span><span class="sxs-lookup"><span data-stu-id="73211-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="73211-187">Geralmente polígonos são limites de toorepresent usado como códigos postais, limites de estado ou formações naturais.</span><span class="sxs-lookup"><span data-stu-id="73211-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="73211-188">Novamente se você incluir indexação espacial em sua política de indexação, em seguida, "em" consultas serão servidas com eficiência por meio do índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="73211-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="73211-189">Argumentos do polígono ST_WITHIN podem conter apenas um único toque, ou seja, Olá polígonos não deve conter buracos neles.</span><span class="sxs-lookup"><span data-stu-id="73211-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="73211-190">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="73211-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="73211-191">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="73211-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="73211-192">Tipos semelhantes de toohow incompatível funciona na consulta de banco de dados do Azure Cosmos se Olá local valor especificado em um argumento está malformado ou inválido, ela será avaliada muito**indefinido** e ignorados Olá avaliada documento toobe de saudação resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="73211-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="73211-193">Se sua consulta não retornar resultados, execute toodebug ST_ISVALIDDETAILED por que o tipo de spatail Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="73211-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="73211-194">Banco de dados do Azure Cosmos também oferece suporte ao realizar consultas inversas, ou seja, você pode indexar polígonos ou linhas no banco de dados do Azure Cosmos de consulta para as áreas de saudação que contenham um ponto especificado.</span><span class="sxs-lookup"><span data-stu-id="73211-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="73211-195">Esse padrão é normalmente usado em logística tooidentify, por exemplo, quando um caminhão entra ou sai de uma determinada área.</span><span class="sxs-lookup"><span data-stu-id="73211-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="73211-196">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="73211-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="73211-197">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="73211-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="73211-198">ST_ISVALID e ST_ISVALIDDETAILED podem ser usado toocheck se um objeto espacial é válido.</span><span class="sxs-lookup"><span data-stu-id="73211-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="73211-199">Por exemplo, Olá consulta a seguir verifica validade Olá de um ponto com um limite de valor de latitude de intervalo (-132.8).</span><span class="sxs-lookup"><span data-stu-id="73211-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="73211-200">ST_ISVALID retorna apenas um valor booliano e retorna ST_ISVALIDDETAILED Olá booliano e uma cadeia de caracteres que contém a razão Olá por que ele é considerado inválido.</span><span class="sxs-lookup"><span data-stu-id="73211-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="73211-201">** Consulta **</span><span class="sxs-lookup"><span data-stu-id="73211-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="73211-202">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="73211-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="73211-203">Essas funções também podem ser usado toovalidate polígonos.</span><span class="sxs-lookup"><span data-stu-id="73211-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="73211-204">Por exemplo, aqui usamos ST_ISVALIDDETAILED toovalidate um polígono que não está fechado.</span><span class="sxs-lookup"><span data-stu-id="73211-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="73211-205">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="73211-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="73211-206">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="73211-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="73211-207">Consulta LINQ em Olá SDK .NET</span><span class="sxs-lookup"><span data-stu-id="73211-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="73211-208">Olá SDK .NET do DocumentDB também provedores stub métodos `Distance()` e `Within()` para uso em expressões LINQ.</span><span class="sxs-lookup"><span data-stu-id="73211-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="73211-209">provedor LINQ DocumentDB Hello converte essas chamadas toohello equivalente SQL função interna chamadas de método (ST_DISTANCE e ST_WITHIN respectivamente).</span><span class="sxs-lookup"><span data-stu-id="73211-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="73211-210">Aqui está um exemplo de uma consulta LINQ que localiza todos os documentos na coleção de banco de dados do Azure Cosmos Olá cujo valor de "local" está dentro de um raio de 30km de saudação especificado ponto usando LINQ.</span><span class="sxs-lookup"><span data-stu-id="73211-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="73211-211">**Consulta LINQ para distância**</span><span class="sxs-lookup"><span data-stu-id="73211-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="73211-212">Da mesma forma, aqui está uma consulta para localizar todos os documentos de saudação cujo "local" está dentro de saudação especificado caixa/polígono.</span><span class="sxs-lookup"><span data-stu-id="73211-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="73211-213">**Consulta LINQ para dentro**</span><span class="sxs-lookup"><span data-stu-id="73211-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="73211-214">Agora que estamos dando uma olhada em como tooquery documentos usando LINQ e SQL, vamos dar uma olhada em como tooconfigure Azure Cosmos DB para indexação espacial.</span><span class="sxs-lookup"><span data-stu-id="73211-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="73211-215">Indexação</span><span class="sxs-lookup"><span data-stu-id="73211-215">Indexing</span></span>
<span data-ttu-id="73211-216">Conforme descrito na Olá [indexação independente de esquema com o banco de dados do Azure Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papel, criamos o toobe de mecanismo de banco de dados do Azure Cosmos DB verdadeiramente independente de esquema e fornecer suporte de primeira classe para JSON.</span><span class="sxs-lookup"><span data-stu-id="73211-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="73211-217">mecanismo de banco de dados de gravação otimizada saudação do banco de dados do Azure Cosmos nativamente compreende dados espaciais (pontos, linhas e polígonos) representados no padrão de GeoJSON hello.</span><span class="sxs-lookup"><span data-stu-id="73211-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="73211-218">Em resumo, geometry Olá for projetado de coordenadas geodésicos em um plano 2D, progressivamente dividido em células usando um **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="73211-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="73211-219">Essas células são mapeadas too1D com base na localização de saudação de célula de saudação em uma **curva de preenchimento de espaço de Hilbert**, que preserva a localidade de pontos.</span><span class="sxs-lookup"><span data-stu-id="73211-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="73211-220">Além disso quando os dados de local são indexados, ele passa por um processo conhecido como **mosaico**, ou seja, todas as células de saudação que interceptam um local são identificadas e armazenadas como chaves de índice de banco de dados do Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="73211-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="73211-221">No momento da consulta, argumentos como pontos e polígonos também estão incluídas no mosaico tooextract Olá intervalos de ID de célula relevantes e tooretrieve dados do índice Olá usados.</span><span class="sxs-lookup"><span data-stu-id="73211-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="73211-222">Se você especificar uma política de indexação que inclui o índice espacial para / * (todos os caminhos), em seguida, todos os pontos de encontrado na coleção de saudação são indexados para consultas espaciais eficientes (ST_WITHIN e ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="73211-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="73211-223">Os índices espaciais não têm um valor de precisão e sempre usam um valor de precisão padrão.</span><span class="sxs-lookup"><span data-stu-id="73211-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="73211-224">O Azure Cosmos DB dá suporte à indexação automática de Points, Polygons e LineStrings</span><span class="sxs-lookup"><span data-stu-id="73211-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="73211-225">Olá trecho JSON a seguir mostra uma política de indexação com indexação espacial habilitado, ou seja, qualquer ponto GeoJSON encontrado em documentos de consulta espacial do índice.</span><span class="sxs-lookup"><span data-stu-id="73211-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="73211-226">Se você estiver modificando Olá indexação política usando Olá Portal do Azure, você pode especificar Olá JSON a seguir para indexação de política tooenable espacial indexação em sua coleção.</span><span class="sxs-lookup"><span data-stu-id="73211-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="73211-227">**JSON da política de indexação da coleção com espacial habilitado para pontos e Polígonos**</span><span class="sxs-lookup"><span data-stu-id="73211-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="73211-228">Aqui está um trecho de código no .NET que mostra como toocreate uma coleção com indexação espacial ativado para todos os caminhos que contenham pontos.</span><span class="sxs-lookup"><span data-stu-id="73211-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="73211-229">**Criar uma coleção com indexação espacial**</span><span class="sxs-lookup"><span data-stu-id="73211-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="73211-230">E aqui está como você pode modificar uma vantagem de tootake de coleção existente de indexação espacial quaisquer pontos que são armazenados dentro de documentos.</span><span class="sxs-lookup"><span data-stu-id="73211-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="73211-231">**Modificar uma coleção existente com indexação espacial**</span><span class="sxs-lookup"><span data-stu-id="73211-231">**Modify an existing collection with spatial indexing**</span></span>

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
> <span data-ttu-id="73211-232">Se o local de saudação GeoJSON valor dentro do documento hello estiver malformado ou inválido, em seguida, ele será não obter indexado para consultar espacial.</span><span class="sxs-lookup"><span data-stu-id="73211-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="73211-233">Você pode validar valores de localização usando ST_ISVALID e ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="73211-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="73211-234">Caso sua definição de coleção inclua uma chave de partição, o andamento da transformação de indexação não será relatado.</span><span class="sxs-lookup"><span data-stu-id="73211-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="73211-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73211-235">Next steps</span></span>
<span data-ttu-id="73211-236">Agora que você já learnt sobre como tooget iniciada com o suporte de geoespaciais no banco de dados do Azure Cosmos, você pode:</span><span class="sxs-lookup"><span data-stu-id="73211-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="73211-237">Iniciar a codificação com hello [exemplos de código geoespaciais .NET no GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="73211-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="73211-238">Obter ponteiros em com geoespaciais consultando a saudação [parque de consulta de banco de dados do Azure Cosmos](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="73211-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="73211-239">Saiba mais sobre a [Consulta do Azure Cosmos DB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="73211-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="73211-240">Saiba mais sobre as [Políticas de indexação do Azure Cosmos DB](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="73211-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

