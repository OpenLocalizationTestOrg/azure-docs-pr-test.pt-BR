---
title: "Versão da API REST do Serviço Azure Search 2015-02-28-Preview | Microsoft Docs"
description: "A API do serviço Azure Search Versão 2015-02-28-Preview inclui recursos experimentais como analisadores de linguagem natural e pesquisas do tipo moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: e6ad5c964bfa8421be2706cb4015980e01a271b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="d6329-103">API REST do serviço Azure Search: Versão 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="d6329-104">Este artigo é a documentação de referência para a `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-105">Essa visualização estende a atual versão disponibilizada para o público geral, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornecendo os seguintes recursos experimentais:</span><span class="sxs-lookup"><span data-stu-id="d6329-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="d6329-106">`moreLikeThis` na API [Pesquisar Documentos](#SearchDocs) .</span><span class="sxs-lookup"><span data-stu-id="d6329-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="d6329-107">Ele localiza outros documentos relevantes para outro documento específico.</span><span class="sxs-lookup"><span data-stu-id="d6329-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="d6329-108">Algumas partes adicionais da API REST do `2015-02-28-Preview` são documentadas separadamente.</span><span class="sxs-lookup"><span data-stu-id="d6329-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="d6329-109">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="d6329-109">These include:</span></span>

* [<span data-ttu-id="d6329-110">Perfis de pontuação</span><span class="sxs-lookup"><span data-stu-id="d6329-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="d6329-111">Indexadores</span><span class="sxs-lookup"><span data-stu-id="d6329-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="d6329-112">O serviço Azure Search está disponível em várias versões.</span><span class="sxs-lookup"><span data-stu-id="d6329-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="d6329-113">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="d6329-114">APIs neste documento</span><span class="sxs-lookup"><span data-stu-id="d6329-114">APIs in this document</span></span>
<span data-ttu-id="d6329-115">A API do serviço Pesquisa do Azure dá suporte a duas sintaxes de URL para operações de API: simples e OData (consulte [Suporte a OData (API da Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="d6329-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="d6329-116">A lista a seguir mostra a sintaxe simples.</span><span class="sxs-lookup"><span data-stu-id="d6329-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="d6329-117">Criar o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-118">Atualizar o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-119">Obter o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-120">Listando índices</span><span class="sxs-lookup"><span data-stu-id="d6329-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-121">Obter estatísticas de índice</span><span class="sxs-lookup"><span data-stu-id="d6329-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-122">Analisador de teste</span><span class="sxs-lookup"><span data-stu-id="d6329-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-123">Excluir um índice</span><span class="sxs-lookup"><span data-stu-id="d6329-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-124">Adicionar, excluir e atualizar dados em um índice</span><span class="sxs-lookup"><span data-stu-id="d6329-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-125">Pesquisar documentos</span><span class="sxs-lookup"><span data-stu-id="d6329-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-126">Procurar documento</span><span class="sxs-lookup"><span data-stu-id="d6329-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="d6329-127">Contar documentos</span><span class="sxs-lookup"><span data-stu-id="d6329-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="d6329-128">Sugestões</span><span class="sxs-lookup"><span data-stu-id="d6329-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="d6329-129">Operações de índice</span><span class="sxs-lookup"><span data-stu-id="d6329-129">Index Operations</span></span>
<span data-ttu-id="d6329-130">Você pode criar e gerenciar índices no serviço Azure Search por meio de solicitações HTTP simples (POST, GET, PUT, DELETE) em relação a um recurso de índice específico.</span><span class="sxs-lookup"><span data-stu-id="d6329-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="d6329-131">Para criar um índice, primeiro execute POST para um documento JSON que descreve o esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="d6329-132">O esquema define os campos do índice, seus tipos de dados e como eles podem ser usados (por exemplo, em pesquisas de texto completo, filtros, classificação ou facetamento).</span><span class="sxs-lookup"><span data-stu-id="d6329-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="d6329-133">Ele também define os perfis de pontuação, sugestores e outros atributos para configurar o comportamento do índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="d6329-134">O exemplo a seguir fornece uma ilustração de um esquema usado para pesquisar informações de hotel com o campo Descrição definido em dois idiomas.</span><span class="sxs-lookup"><span data-stu-id="d6329-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="d6329-135">Observe como os atributos controlam como o campo é usado.</span><span class="sxs-lookup"><span data-stu-id="d6329-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="d6329-136">Por exemplo, o `hotelId` é usado como a chave do documento (`"key": true`) e é excluído de pesquisas de texto completo (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="d6329-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="d6329-137">Depois que o índice for criado, você carregará documentos que populam o índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="d6329-138">Consulte [Adicionar ou Atualizar Documentos](#AddOrUpdateDocuments) para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="d6329-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="d6329-139">Para um vídeo de introdução à indexação no Azure Search, consulte o [episódio do Cloud Cover do Channel 9 sobre o Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="d6329-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="d6329-140">Criar o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-140">Create Index</span></span>
<span data-ttu-id="d6329-141">Um índice é o principal meio de organizar e pesquisar documentos no Azure Search, de forma semelhante a como uma tabela organiza registros em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d6329-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="d6329-142">Cada índice tem uma coleção de documentos que estão todos em conformidade com o esquema do índice (nomes de campos, tipos de dados e propriedades), mas os índices também especificam constructos adicionais (sugestores, perfis de pontuação e opções de CORS) que definem outros comportamentos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="d6329-143">Você pode criar um novo índice em um serviço Azure Search usando uma solicitação HTTP POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="d6329-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="d6329-144">O corpo da solicitação é um esquema JSON que especifica as informações de configuração e de índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d6329-145">Como alternativa, você pode usar PUT e especificar o nome do índice no URI.</span><span class="sxs-lookup"><span data-stu-id="d6329-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="d6329-146">Se o índice não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="d6329-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="d6329-147">A criação de um índice determina a estrutura dos documentos armazenados e usados em operações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="d6329-148">Popular o índice é uma operação separada.</span><span class="sxs-lookup"><span data-stu-id="d6329-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="d6329-149">Nessa etapa, você pode usar um [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponível para fontes de dados com suporte) ou uma operação [Adicionar, Atualizar ou Excluir Documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="d6329-150">O índice invertido é gerado quando os documentos são postados.</span><span class="sxs-lookup"><span data-stu-id="d6329-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="d6329-151">**Observação**: o número máximo de índices permitidos varia por tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="d6329-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="d6329-152">O serviço gratuito permite até três índices.</span><span class="sxs-lookup"><span data-stu-id="d6329-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="d6329-153">O serviço padrão permite 50 índices por serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="d6329-154">Consulte [Limites e restrições](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="d6329-155">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-155">**Request**</span></span>

<span data-ttu-id="d6329-156">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d6329-157">A solicitação **Criar Índice** pode ser criada usando um método POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="d6329-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="d6329-158">Ao usar POST, você deve fornecer um nome de índice no corpo da solicitação, juntamente com a definição de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="d6329-159">Com PUT, o nome do índice é parte da URL.</span><span class="sxs-lookup"><span data-stu-id="d6329-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="d6329-160">Se o índice não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="d6329-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="d6329-161">Se já existir, ele será atualizado para a nova definição.</span><span class="sxs-lookup"><span data-stu-id="d6329-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="d6329-162">O nome do índice deve estar em letras minúsculas, começar com uma letra ou número, não conter barras ou pontos e ter menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6329-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="d6329-163">Depois de iniciar o nome do índice com uma letra ou número, o restante do nome pode incluir qualquer letra, número e traços, desde que os traços não sejam consecutivos.</span><span class="sxs-lookup"><span data-stu-id="d6329-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="d6329-164">A `api-version` é obrigatória.</span><span class="sxs-lookup"><span data-stu-id="d6329-164">The `api-version` is required.</span></span> <span data-ttu-id="d6329-165">Consulte [Controle de Versão de Serviço de Pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter uma lista das versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d6329-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="d6329-166">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-166">**Request Headers**</span></span>

<span data-ttu-id="d6329-167">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-168">`Content-Type`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-168">`Content-Type`: Required.</span></span> <span data-ttu-id="d6329-169">Defina-o como `application/json`</span><span class="sxs-lookup"><span data-stu-id="d6329-169">Set this to `application/json`</span></span>
* <span data-ttu-id="d6329-170">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-170">`api-key`: Required.</span></span> <span data-ttu-id="d6329-171">A `api-key` é usada para</span><span class="sxs-lookup"><span data-stu-id="d6329-171">The `api-key` is used to</span></span>
* <span data-ttu-id="d6329-172">autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-173">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-174">A solicitação **Criar Índice** deve incluir um cabeçalho de `api-key` definido como sua chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-175">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-176">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-177">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-178"><a name="RequestData"></a>
**Sintaxe do Corpo da Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="d6329-179">O corpo da solicitação contém uma definição de esquema, que inclui a lista de campos de dados em documentos que serão inseridos nesse índice, tipos de dados, atributos, bem como uma lista opcional de perfis de pontuação que são usados para pontuar documentos correspondentes no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="d6329-180">Observe que, para uma solicitação POST, você deve especificar o nome do índice no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="d6329-181">Pode haver somente um campo de chave no índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-181">There can only be one key field in the index.</span></span> <span data-ttu-id="d6329-182">Ele deve ser um campo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6329-182">It has to be a string field.</span></span> <span data-ttu-id="d6329-183">Esse campo representa o identificador exclusivo para cada documento armazenado no índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="d6329-184">As principais partes de um índice incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6329-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="d6329-185">`fields` que serão inseridos nesse índice, incluindo nome, tipo de dados e propriedades que definem as ações permitidas nesse campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="d6329-186">`suggesters` usados para consultas de preenchimento automático ou digitação antecipada.</span><span class="sxs-lookup"><span data-stu-id="d6329-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="d6329-187">`scoringProfiles` usados para classificação de pontuação de pesquisa personalizada.</span><span class="sxs-lookup"><span data-stu-id="d6329-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="d6329-188">Consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="d6329-189">`analyzers`, `charFilters`, `tokenizers` e `tokenFilters` usados para definir como os seus documentos/consultas são divididos em tokens indexáveis/pesquisáveis.</span><span class="sxs-lookup"><span data-stu-id="d6329-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="d6329-190">Confira [Análise na Pesquisa do Azure](https://aka.ms//azsanalysis) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="d6329-191">`defaultScoringProfile` usado para substituir os comportamentos de pontuação padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="d6329-192">`corsOptions` para permitir consultas entre origens em relação a seu índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="d6329-193">A sintaxe para estruturar a carga da solicitação é indicada a seguir.</span><span class="sxs-lookup"><span data-stu-id="d6329-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="d6329-194">Uma solicitação de exemplo é fornecida mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="d6329-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="d6329-195">**Atributos de índice**</span><span class="sxs-lookup"><span data-stu-id="d6329-195">**Index Attributes**</span></span>

<span data-ttu-id="d6329-196">Os atributos a seguir podem ser definidos ao criar um índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="d6329-197">Para obter detalhes sobre pontuação e perfis de pontuação, consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="d6329-198">`name` ‒ define o nome do campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="d6329-199">`type` ‒ define o tipo de dados do campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-199">`type` - Sets the data type for the field.</span></span>

<span data-ttu-id="d6329-200">`searchable` ‒ marca o campo como texto completo pesquisável.</span><span class="sxs-lookup"><span data-stu-id="d6329-200">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="d6329-201">Isso significa que ele será submetido a análise, como separação de palavras, durante a indexação.</span><span class="sxs-lookup"><span data-stu-id="d6329-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="d6329-202">Se você definir um campo `searchable` para um valor como "dia ensolarado", internamente ele será dividido nos tokens individuais "dia" e "ensolarado".</span><span class="sxs-lookup"><span data-stu-id="d6329-202">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="d6329-203">Isso habilita pesquisas de texto completo para esses termos.</span><span class="sxs-lookup"><span data-stu-id="d6329-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="d6329-204">Os campos dos tipos `Edm.String` ou `Collection(Edm.String)` são `searchable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="d6329-205">Campos de outros tipos não podem ser `searchable`.</span><span class="sxs-lookup"><span data-stu-id="d6329-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="d6329-206">**Observação**: os campos `searchable` consomem espaço extra no índice, pois o Azure Search armazenará uma versão com token adicional do valor do campo para pesquisas de texto completo.</span><span class="sxs-lookup"><span data-stu-id="d6329-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="d6329-207">Se você desejar economizar espaço no índice e não for necessário incluir um campo em pesquisas, defina `searchable` como `false`.</span><span class="sxs-lookup"><span data-stu-id="d6329-207">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="d6329-208">`filterable` - permite que o campo seja referenciado em consultas `$filter`.</span><span class="sxs-lookup"><span data-stu-id="d6329-208">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="d6329-209">`filterable` difere de `searchable` da maneira como cadeias de caracteres são tratadas.</span><span class="sxs-lookup"><span data-stu-id="d6329-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="d6329-210">Campos dos tipos `Edm.String` ou `Collection(Edm.String)` que são `filterable` não são submetidos à quebra de palavras. Portanto, as comparações são apenas para correspondências exatas.</span><span class="sxs-lookup"><span data-stu-id="d6329-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="d6329-211">Por exemplo, se você definir um campo `f` como "dia ensolarado", `$filter=f eq 'sunny'` não encontrará correspondências, mas `$filter=f eq 'sunny day'` as encontrará.</span><span class="sxs-lookup"><span data-stu-id="d6329-211">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="d6329-212">Todos os campos são `filterable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="d6329-213">`sortable` ‒ por padrão o sistema classifica os resultados pela pontuação, mas, em muitas experiências, os usuários desejarão classificar por campos nos documentos.</span><span class="sxs-lookup"><span data-stu-id="d6329-213">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="d6329-214">Campos do tipo `Collection(Edm.String)` não podem ser `sortable`.</span><span class="sxs-lookup"><span data-stu-id="d6329-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="d6329-215">Todos os outros campos são `sortable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="d6329-216">`facetable`‒ geralmente usado em uma apresentação dos resultados de pesquisa que inclui a contagem de ocorrências por categoria (por exemplo, pesquisar câmeras digitais e ver as ocorrências por marca, por megapixels, por preço etc.).</span><span class="sxs-lookup"><span data-stu-id="d6329-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="d6329-217">Essa opção não pode ser usada com campos do tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="d6329-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="d6329-218">Todos os outros campos são `facetable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="d6329-219">**Observação**: campos do tipo `Edm.String` que são `filterable`, `sortable` ou `facetable` podem ter no máximo 32 KB de comprimento.</span><span class="sxs-lookup"><span data-stu-id="d6329-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="d6329-220">Isso ocorre porque esses campos são tratados como um único termo de pesquisa, e o comprimento máximo de um termo no Azure Search é 32 KB.</span><span class="sxs-lookup"><span data-stu-id="d6329-220">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="d6329-221">Se precisar armazenar mais texto do que isso em um único campo de cadeia de caracteres, você precisará definir explicitamente `filterable`, `sortable` e `facetable` como `false` na definição do índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-221">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="d6329-222">**Observação**: se um campo não tiver nenhum dos atributos acima definidos como `true` (`searchable`, `filterable`, `sortable` ou `facetable`) o campo será efetivamente excluído do índice invertido.</span><span class="sxs-lookup"><span data-stu-id="d6329-222">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="d6329-223">Essa opção é útil para campos que não são usados em consultas, mas são necessários em resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="d6329-224">A exclusão desses campos do índice melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d6329-224">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="d6329-225">`key` ‒ marca o campo como contendo identificadores exclusivos para documentos no índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-225">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="d6329-226">Exatamente um campo deve ser escolhido como o campo `key`, e ele deve ser do tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="d6329-226">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="d6329-227">Campos de chave podem ser usados para pesquisar documentos diretamente por meio da [API de pesquisa](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="d6329-227">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="d6329-228">`retrievable` ‒ define se o campo pode ser retornado em um resultado de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-228">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="d6329-229">Isso é útil quando você quer usar um campo (por exemplo, margem) como mecanismo de filtro, classificação ou pontuação, mas não deseja que o campo seja visível ao usuário final.</span><span class="sxs-lookup"><span data-stu-id="d6329-229">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="d6329-230">Esse atributo deve ser `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="d6329-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="d6329-231">`analyzer` - define o nome do analisador a usar para o campo no tempo de pesquisa e de indexação.</span><span class="sxs-lookup"><span data-stu-id="d6329-231">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="d6329-232">Para o conjunto de valores permitidos, consulte [Analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-232">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="d6329-233">Essa opção pode ser usada apenas com campos `searchable`, e não pode ser definida com `searchAnalyzer` ou `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="d6329-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="d6329-234">Depois que o analisador for escolhido, ele não poderá ser alterado para o campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-234">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="d6329-235">`searchAnalyzer` - define o nome do analisador usado no tempo de pesquisa para o campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-235">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="d6329-236">Para o conjunto de valores permitidos, consulte [Analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-236">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="d6329-237">Essa opção só pode ser usada com campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="d6329-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="d6329-238">Ele deve ser definido juntamente com `indexAnalyzer` e não pode ser definido com a opção `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="d6329-238">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="d6329-239">Esse analisador pode ser atualizado em um campo existente.</span><span class="sxs-lookup"><span data-stu-id="d6329-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="d6329-240">`indexAnalyzer` - define o nome do analisador usado no tempo de indexação para o campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-240">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="d6329-241">Para o conjunto de valores permitidos, consulte [Analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-241">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="d6329-242">Essa opção só pode ser usada com campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="d6329-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="d6329-243">Ele deve ser definido juntamente com `searchAnalyzer` e não pode ser definido com a opção `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="d6329-243">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="d6329-244">Depois que o analisador for escolhido, ele não poderá ser alterado para o campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-244">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="d6329-245">`suggesters` ‒ define o modo de pesquisa e campos que são a origem do conteúdo para obter sugestões.</span><span class="sxs-lookup"><span data-stu-id="d6329-245">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="d6329-246">Consulte [Sugestores](#Suggesters) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="d6329-247">`scoringProfiles` ‒ define comportamentos de pontuação personalizados que permitem influenciam quais itens aparecem em posição mais elevada nos resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="d6329-248">Perfis de pontuação são compostos de funções e pesos de campos.</span><span class="sxs-lookup"><span data-stu-id="d6329-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="d6329-249">Consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações sobre os atributos usados em um perfil de pontuação.</span><span class="sxs-lookup"><span data-stu-id="d6329-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="d6329-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Suporte ao idioma**</span><span class="sxs-lookup"><span data-stu-id="d6329-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="d6329-251">Os campos pesquisáveis são submetidos a análise que, frequentemente, envolve quebra de palavras, normalização do texto e filtragem de termos.</span><span class="sxs-lookup"><span data-stu-id="d6329-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="d6329-252">Por padrão, os campos pesquisáveis no Azure Search são analisados com o [Analisador Apache Lucene Padrão](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html), que quebra o texto em elementos seguindo as regras de ["Segmentação de texto Unicode"](http://unicode.org/reports/tr29/).</span><span class="sxs-lookup"><span data-stu-id="d6329-252">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="d6329-253">Além disso, o analisador padrão converte todos os caracteres em sua forma em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d6329-253">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="d6329-254">Documentos indexados e termos de pesquisa são submetidos a análise durante a indexação e o processamento de consultas.</span><span class="sxs-lookup"><span data-stu-id="d6329-254">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="d6329-255">A Pesquisa do Azure oferece suporte a vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="d6329-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="d6329-256">Cada um desses idiomas requer um analisador de texto não padrão que leva em consideração as características de determinado idioma.</span><span class="sxs-lookup"><span data-stu-id="d6329-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="d6329-257">O Azure Search oferece dois tipos de analisadores:</span><span class="sxs-lookup"><span data-stu-id="d6329-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="d6329-258">35 analisadores ativados pela Lucene.</span><span class="sxs-lookup"><span data-stu-id="d6329-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="d6329-259">50 analisadores apoiados pela tecnologia de processamento de idioma natural proprietária da Microsoft usada no Office e no Bing.</span><span class="sxs-lookup"><span data-stu-id="d6329-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="d6329-260">Alguns desenvolvedores talvez prefiram a solução mais familiar, simples e aberta da Lucene.</span><span class="sxs-lookup"><span data-stu-id="d6329-260">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="d6329-261">Os analisadores Lucene são mais rápidos, mas os analisadores da Microsoft têm recursos avançados, como derivação, decomposição de palavras (em idiomas como alemão, dinamarquês, holandês, sueco, norueguês, estoniano, finlandês, húngaro, eslovaco) e reconhecimento de identidade (URLs, emails, datas, números).</span><span class="sxs-lookup"><span data-stu-id="d6329-261">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="d6329-262">Se possível, você deve executar comparações entre os analisadores da Microsoft e da Lucene para decidir qual é a melhor opção.</span><span class="sxs-lookup"><span data-stu-id="d6329-262">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="d6329-263">***Veja a comparação***</span><span class="sxs-lookup"><span data-stu-id="d6329-263">***How they compare***</span></span>

<span data-ttu-id="d6329-264">O analisador de inglês da Lucene amplia o analisador padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-264">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="d6329-265">Ele remove possessivos (apóstrofos à direita) de palavras, aplica a lematização conforme o [algoritmo de lematização de Porter](http://tartarus.org/~martin/PorterStemmer/) e remove as [palavras irrelevantes](http://en.wikipedia.org/wiki/Stop_words) do inglês.</span><span class="sxs-lookup"><span data-stu-id="d6329-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="d6329-266">Em comparação, o analisador da Microsoft executa a derivação em vez da lematização.</span><span class="sxs-lookup"><span data-stu-id="d6329-266">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="d6329-267">Isso significa que ele pode tratar muito melhor as formas irregulares e inflexivas de palavras, o que gera resultados da pesquisa mais relevantes (observe o módulo 7 da [Apresentação MVA da Pesquisa do Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obter mais detalhes).</span><span class="sxs-lookup"><span data-stu-id="d6329-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="d6329-268">A indexação com analisadores da Microsoft é, em média, de duas a três vezes mais lenta do que seus equivalentes da Lucene, dependendo do idioma.</span><span class="sxs-lookup"><span data-stu-id="d6329-268">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="d6329-269">O desempenho da pesquisa não dever significativamente afetado para consultas de tamanho médio.</span><span class="sxs-lookup"><span data-stu-id="d6329-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="d6329-270">***Configuração***</span><span class="sxs-lookup"><span data-stu-id="d6329-270">***Configuration***</span></span>

<span data-ttu-id="d6329-271">Para cada campo na definição do índice, você pode definir a propriedade `analyzer` como um nome de analisador que especifica o idioma e o fornecedor.</span><span class="sxs-lookup"><span data-stu-id="d6329-271">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="d6329-272">O mesmo analisador será aplicado durante a indexação e a pesquisa desse campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-272">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="d6329-273">Por exemplo, você pode ter campos separados para descrições de hotéis em inglês, francês e espanhol, existentes lado a lado no mesmo índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="d6329-274">Use o [parâmetro de consulta 'searchFields'](#SearchQueryParameters) para descrever qual campo específico a um idioma pesquisar em suas consultas.</span><span class="sxs-lookup"><span data-stu-id="d6329-274">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="d6329-275">Você pode examinar os exemplos de consultas que incluem a propriedade `analyzer` em [Pesquisar documentos](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="d6329-275">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="d6329-276">***Lista de analisadores***</span><span class="sxs-lookup"><span data-stu-id="d6329-276">***Analyzer list***</span></span>

<span data-ttu-id="d6329-277">Veja abaixo uma lista de idiomas com suporte juntamente com nomes de analisador da Lucene e da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d6329-277">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="d6329-278">Linguagem</span><span class="sxs-lookup"><span data-stu-id="d6329-278">Language</span></span></th>
        <th><span data-ttu-id="d6329-279">Nome do analisador da Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="d6329-280">Nome do analisador da Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-281">Árabe</span><span class="sxs-lookup"><span data-stu-id="d6329-281">Arabic</span></span></td>
        <td><span data-ttu-id="d6329-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-284">Armênia</span><span class="sxs-lookup"><span data-stu-id="d6329-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="d6329-285">hy.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="d6329-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="d6329-286">Bangla</span></span></td>
        <td><span data-ttu-id="d6329-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="d6329-288">Basco</span><span class="sxs-lookup"><span data-stu-id="d6329-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="d6329-289">Eu.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="d6329-290">Búlgaro</span><span class="sxs-lookup"><span data-stu-id="d6329-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="d6329-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-292">BG.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="d6329-293">Catalão</span><span class="sxs-lookup"><span data-stu-id="d6329-293">Catalan</span></span></td>
        <td><span data-ttu-id="d6329-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-295">CA.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="d6329-296">Chinês (simplificado)</span><span class="sxs-lookup"><span data-stu-id="d6329-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="d6329-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-299">Chinês (tradicional)</span><span class="sxs-lookup"><span data-stu-id="d6329-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="d6329-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="d6329-302">Croata</span><span class="sxs-lookup"><span data-stu-id="d6329-302">Croatian</span></span></td>
        <td><span data-ttu-id="d6329-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-304">Tcheco</span><span class="sxs-lookup"><span data-stu-id="d6329-304">Czech</span></span></td>
        <td><span data-ttu-id="d6329-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="d6329-307">Dinamarquês</span><span class="sxs-lookup"><span data-stu-id="d6329-307">Danish</span></span></td>
        <td><span data-ttu-id="d6329-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="d6329-310">Holandês</span><span class="sxs-lookup"><span data-stu-id="d6329-310">Dutch</span></span></td>
        <td><span data-ttu-id="d6329-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="d6329-313">Inglês</span><span class="sxs-lookup"><span data-stu-id="d6329-313">English</span></span></td>        
        <td><span data-ttu-id="d6329-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-316">Estoniano</span><span class="sxs-lookup"><span data-stu-id="d6329-316">Estonian</span></span></td>
        <td><span data-ttu-id="d6329-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-318">Finlandês</span><span class="sxs-lookup"><span data-stu-id="d6329-318">Finnish</span></span></td>
        <td><span data-ttu-id="d6329-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="d6329-321">Francês</span><span class="sxs-lookup"><span data-stu-id="d6329-321">French</span></span></td>
        <td><span data-ttu-id="d6329-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-324">Galego</span><span class="sxs-lookup"><span data-stu-id="d6329-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="d6329-325">GL.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="d6329-326">Alemão</span><span class="sxs-lookup"><span data-stu-id="d6329-326">German</span></span></td>
        <td><span data-ttu-id="d6329-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-329">Grego</span><span class="sxs-lookup"><span data-stu-id="d6329-329">Greek</span></span></td>
        <td><span data-ttu-id="d6329-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-332">Guzerate</span><span class="sxs-lookup"><span data-stu-id="d6329-332">Gujarati</span></span></td>
        <td><span data-ttu-id="d6329-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-334">Hebraico</span><span class="sxs-lookup"><span data-stu-id="d6329-334">Hebrew</span></span></td>
        <td><span data-ttu-id="d6329-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-336">Híndi</span><span class="sxs-lookup"><span data-stu-id="d6329-336">Hindi</span></span></td>
        <td><span data-ttu-id="d6329-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-339">Húngaro</span><span class="sxs-lookup"><span data-stu-id="d6329-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="d6329-340">hu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-342">Islandês</span><span class="sxs-lookup"><span data-stu-id="d6329-342">Icelandic</span></span></td>
        <td><span data-ttu-id="d6329-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-344">Indonésio (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="d6329-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="d6329-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-347">Irlandês</span><span class="sxs-lookup"><span data-stu-id="d6329-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="d6329-348">GA.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="d6329-349">Italian</span></span></td>
        <td><span data-ttu-id="d6329-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-352">Japonês</span><span class="sxs-lookup"><span data-stu-id="d6329-352">Japanese</span></span></td>
        <td><span data-ttu-id="d6329-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="d6329-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="d6329-355">Kannada</span></span></td>
        <td><span data-ttu-id="d6329-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="d6329-357">Korean</span></span></td>
        <td><span data-ttu-id="d6329-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-360">Letão</span><span class="sxs-lookup"><span data-stu-id="d6329-360">Latvian</span></span></td>        
        <td><span data-ttu-id="d6329-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="d6329-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="d6329-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-365">Malaiala</span><span class="sxs-lookup"><span data-stu-id="d6329-365">Malayalam</span></span></td>
        <td><span data-ttu-id="d6329-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-367">Malaio (latino)</span><span class="sxs-lookup"><span data-stu-id="d6329-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="d6329-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-369">Marati</span><span class="sxs-lookup"><span data-stu-id="d6329-369">Marathi</span></span></td>
        <td><span data-ttu-id="d6329-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-371">Norueguês</span><span class="sxs-lookup"><span data-stu-id="d6329-371">Norwegian</span></span></td>
        <td><span data-ttu-id="d6329-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="d6329-374">Persa</span><span class="sxs-lookup"><span data-stu-id="d6329-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="d6329-375">FA.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="d6329-376">Polonês</span><span class="sxs-lookup"><span data-stu-id="d6329-376">Polish</span></span></td>
        <td><span data-ttu-id="d6329-377">pl.Microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-379">Português (Brasil)</span><span class="sxs-lookup"><span data-stu-id="d6329-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="d6329-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-382">Português (Portugal)</span><span class="sxs-lookup"><span data-stu-id="d6329-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="d6329-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="d6329-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="d6329-385">Punjabi</span></span></td>
        <td><span data-ttu-id="d6329-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-387">Romeno</span><span class="sxs-lookup"><span data-stu-id="d6329-387">Romanian</span></span></td>
        <td><span data-ttu-id="d6329-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-390">Russo</span><span class="sxs-lookup"><span data-stu-id="d6329-390">Russian</span></span></td>
        <td><span data-ttu-id="d6329-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-393">Sérvio (cirílico)</span><span class="sxs-lookup"><span data-stu-id="d6329-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="d6329-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-395">Sérvio (latino)</span><span class="sxs-lookup"><span data-stu-id="d6329-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="d6329-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-397">Eslovaco</span><span class="sxs-lookup"><span data-stu-id="d6329-397">Slovak</span></span></td>
        <td><span data-ttu-id="d6329-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-399">Esloveno</span><span class="sxs-lookup"><span data-stu-id="d6329-399">Slovenian</span></span></td>
        <td><span data-ttu-id="d6329-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-401">Espanhol</span><span class="sxs-lookup"><span data-stu-id="d6329-401">Spanish</span></span></td>
        <td><span data-ttu-id="d6329-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-404">Sueco</span><span class="sxs-lookup"><span data-stu-id="d6329-404">Swedish</span></span></td>
        <td><span data-ttu-id="d6329-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="d6329-407">Tâmil</span><span class="sxs-lookup"><span data-stu-id="d6329-407">Tamil</span></span></td>
        <td><span data-ttu-id="d6329-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-409">Télugo</span><span class="sxs-lookup"><span data-stu-id="d6329-409">Telugu</span></span></td>
        <td><span data-ttu-id="d6329-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-411">Tailandês</span><span class="sxs-lookup"><span data-stu-id="d6329-411">Thai</span></span></td>
        <td><span data-ttu-id="d6329-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-414">Turco</span><span class="sxs-lookup"><span data-stu-id="d6329-414">Turkish</span></span></td>
        <td><span data-ttu-id="d6329-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="d6329-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-417">Ucraniano</span><span class="sxs-lookup"><span data-stu-id="d6329-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="d6329-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="d6329-419">Urdu</span></span></td>
        <td><span data-ttu-id="d6329-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="d6329-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="d6329-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="d6329-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="d6329-423">Além disso, o Azure Search fornece configurações do analisador que não são específicas de idiomas</span><span class="sxs-lookup"><span data-stu-id="d6329-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="d6329-424">Dobra ASCII padrão</span><span class="sxs-lookup"><span data-stu-id="d6329-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="d6329-425">standardasciifolding.Lucene</span><span class="sxs-lookup"><span data-stu-id="d6329-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="d6329-426">Segmentação de texto Unicode (Criador de Token Padrão)</span><span class="sxs-lookup"><span data-stu-id="d6329-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="d6329-427">Filtro de dobra ASCII ‒ converte caracteres Unicode que não pertencem ao conjunto dos primeiros 127 caracteres ASCII em seus equivalentes em ASCII.</span><span class="sxs-lookup"><span data-stu-id="d6329-427">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="d6329-428">Isso é útil para remover os sinais diacríticos.</span><span class="sxs-lookup"><span data-stu-id="d6329-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="d6329-429">Todos os analisadores com nomes anotados com <i>lucene</i> são da plataforma de [analisadores de idiomas do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="d6329-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="d6329-430">Mais informações sobre o filtro de dobra ASCII podem ser encontradas [aqui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="d6329-430">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="d6329-431">**Sugestores**</span><span class="sxs-lookup"><span data-stu-id="d6329-431">**Suggesters**</span></span>

<span data-ttu-id="d6329-432">Um `suggester` define quais campos em um índice são usados para oferecer suporte a auto-completar em pesquisas.</span><span class="sxs-lookup"><span data-stu-id="d6329-432">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="d6329-433">Normalmente, cadeias de caracteres de pesquisa parciais são enviadas à [API de sugestões](#Suggestions) enquanto o usuário está digitando uma consulta de pesquisa, e a API retorna um conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="d6329-433">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="d6329-434">Um sugestor que você define no índice determina quais campos são usados para construir os termos de pesquisa de preenchimento automático.</span><span class="sxs-lookup"><span data-stu-id="d6329-434">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="d6329-435">Consulte [Sugestores](#Suggesters) para obter detalhes de configuração.</span><span class="sxs-lookup"><span data-stu-id="d6329-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="d6329-436">**Perfis de pontuação**</span><span class="sxs-lookup"><span data-stu-id="d6329-436">**Scoring profiles**</span></span>

<span data-ttu-id="d6329-437">`scoringProfile` ‒ define comportamentos de pontuação personalizados que permitem influenciam quais itens aparecem em posição mais elevada nos resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="d6329-438">Perfis de pontuação são compostos de funções e pesos de campos.</span><span class="sxs-lookup"><span data-stu-id="d6329-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="d6329-439">Para usá-las, você pode especificar um perfil por nome na sequência de consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-439">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="d6329-440">Um padrão de pontuação perfil funciona nos bastidores para calcular uma pontuação para cada item em um conjunto de resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-440">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="d6329-441">Você pode usar o perfil de pontuação interno e sem o nome.</span><span class="sxs-lookup"><span data-stu-id="d6329-441">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="d6329-442">Como alternativa, defina `defaultScoringProfile` para usar um perfil personalizado como padrão, chamado sempre que um perfil personalizado não for especificado na sequência de consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-442">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="d6329-443">Consulte [Adicionar perfis de pontuação para um índice de pesquisa (API de REST de serviço de pesquisa do Azure)](search-api-scoring-profiles-2015-02-28-preview.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-443">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="d6329-444">**Opções de CORS**</span><span class="sxs-lookup"><span data-stu-id="d6329-444">**CORS Options**</span></span>

<span data-ttu-id="d6329-445">O Javascript do lado do cliente não pode chamar APIs por padrão, pois o navegador impedirá todas as solicitações entre origens.</span><span class="sxs-lookup"><span data-stu-id="d6329-445">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="d6329-446">Habilite o CORS (Compartilhamento de Recursos entre Origens) definindo o atributo `corsOptions` para permitir consultas entre origens em seu índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-446">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="d6329-447">Observe que apenas APIs de consulta dão suporte a CORS por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="d6329-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="d6329-448">As seguintes opções podem ser definidas para CORS:</span><span class="sxs-lookup"><span data-stu-id="d6329-448">The following options can be set for CORS:</span></span>

* <span data-ttu-id="d6329-449">`allowedOrigins` (obrigatório): essa é uma lista de origens às quais será concedido acesso ao índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-449">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="d6329-450">Isso significa que qualquer código Javascript fornecido por essas origens poderá consultar seu índice (supondo que ele forneça a chave de API correta).</span><span class="sxs-lookup"><span data-stu-id="d6329-450">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="d6329-451">Cada origem normalmente tem o formato `protocol://fully-qualified-domain-name:port` , embora a porta muitas vezes seja omitida.</span><span class="sxs-lookup"><span data-stu-id="d6329-451">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="d6329-452">Consulte [este artigo](http://go.microsoft.com/fwlink/?LinkId=330822) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="d6329-453">Se você quiser permitir o acesso a todas as origens, inclua `*` como um único item na matriz `allowedOrigins`.</span><span class="sxs-lookup"><span data-stu-id="d6329-453">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="d6329-454">Observe que **essa não é uma prática recomendável para serviços de pesquisa de produção.**</span><span class="sxs-lookup"><span data-stu-id="d6329-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="d6329-455">No entanto, pode ser útil para fins de depuração ou de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d6329-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="d6329-456">`maxAgeInSeconds` (opcional): navegadores usam esse valor para determinar a duração (em segundos) para respostas de simulação de CORS de cache.</span><span class="sxs-lookup"><span data-stu-id="d6329-456">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="d6329-457">Esse deve ser um inteiro não negativo.</span><span class="sxs-lookup"><span data-stu-id="d6329-457">This must be a non-negative integer.</span></span> <span data-ttu-id="d6329-458">Quanto maior for esse valor, melhor será o desempenho, porém, mais tempo levará para que as alterações de política CORS entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="d6329-458">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="d6329-459">Se ele não for definido, uma duração padrão de cinco minutos será usada.</span><span class="sxs-lookup"><span data-stu-id="d6329-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="d6329-460"><a name="CreateUpdateIndexExample"></a>
**Exemplo de Corpo de Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="d6329-461">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-461">**Response**</span></span>

<span data-ttu-id="d6329-462">Para uma solicitação bem-sucedida: "201 Criado".</span><span class="sxs-lookup"><span data-stu-id="d6329-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="d6329-463">Por padrão, o corpo da resposta conterá o JSON para a definição de índice que foi criada.</span><span class="sxs-lookup"><span data-stu-id="d6329-463">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="d6329-464">Se o cabeçalho da solicitação `Prefer` for definido como `return=minimal`, o corpo da resposta estará vazio, e o código de status de êxito será "204 Sem Conteúdo" em vez de "201 Criado".</span><span class="sxs-lookup"><span data-stu-id="d6329-464">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="d6329-465">Isso ocorre independentemente de PUT ou POST ter sido usado para criar o índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-465">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="d6329-466">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="d6329-466">**Remarks**</span></span>

<span data-ttu-id="d6329-467">Atualmente, há suporte limitado para atualizações de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="d6329-468">Atualmente, não há suporte às atualizações de esquema que exigem reindexação, como a alteração de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="d6329-469">Embora os campos existentes não possam ser alterados ou excluídos, novos campos podem ser adicionados a um índice existente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="d6329-469">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="d6329-470">Quando um novo campo é adicionado, todos os documentos existentes no índice automaticamente têm um valor nulo para esse campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-470">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="d6329-471">Nenhum espaço de armazenamento adicional será consumido até que novos documentos sejam adicionados ao índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-471">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="d6329-472">Sugestores</span><span class="sxs-lookup"><span data-stu-id="d6329-472">Suggesters</span></span>
<span data-ttu-id="d6329-473">O recurso de sugestões de pesquisa do Azure é um recurso de consulta de digitação antecipada ou preenchimento automático, fornecendo uma lista de possíveis condições de pesquisa em resposta às entradas parciais de cadeia de caracteres inseridas em uma caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-473">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="d6329-474">Você já deve ter notado sugestões de consulta ao usar mecanismos de pesquisa da web comercial: digitando ".NET" no Bing produz uma lista de termos de ".NET 4.5", ".NET Framework 3.5", e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d6329-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="d6329-475">Ao usar o serviço de pesquisa da API REST, a implementação de sugestões em um aplicativo personalizado de Pesquisa do Azure requer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6329-475">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="d6329-476">Habilite sugestões adicionando uma construção de **sugestor** em seu índice, fornecendo o nome, o modo de pesquisa e uma lista de campos para os quais a digitação antecipada é chamada.</span><span class="sxs-lookup"><span data-stu-id="d6329-476">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="d6329-477">Por exemplo, se você especificar "cityName" como um campo de origem, digite uma cadeia de caracteres de pesquisa parcial de "Sea" resultará em "Seattle", "Seaside" e "Seatac" (todos os três são nomes de cidades real) oferecidos como sugestões de consulta para o usuário.</span><span class="sxs-lookup"><span data-stu-id="d6329-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="d6329-478">Chame sugestões chamando o [API de sugestões](#Suggestions) no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d6329-478">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="d6329-479">Normalmente, cadeias de caracteres de pesquisa parciais são enviadas ao serviço enquanto o usuário está digitando uma consulta de pesquisa, e a API retorna um conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="d6329-479">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="d6329-480">Este artigo explica como configurar um **sugestor**.</span><span class="sxs-lookup"><span data-stu-id="d6329-480">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="d6329-481">Você também deve examinar o [API sugestões](#Suggestions) para obter detalhes sobre como um sugestor é usado.</span><span class="sxs-lookup"><span data-stu-id="d6329-481">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="d6329-482">**Uso**</span><span class="sxs-lookup"><span data-stu-id="d6329-482">**Usage**</span></span>

<span data-ttu-id="d6329-483">`Suggesters` são criados no índice e funcionam melhor quando usados para sugerir documentos específicos, em vez de termos ou frases flexíveis.</span><span class="sxs-lookup"><span data-stu-id="d6329-483">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="d6329-484">Os campos de melhores candidatos são títulos, nomes e outras frases relativamente curtas que podem identificar um item.</span><span class="sxs-lookup"><span data-stu-id="d6329-484">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="d6329-485">Os campos repetitivos, como categorias e marcas, ou campos muito longos, como campos de comentários ou descrições, são menos eficazes.</span><span class="sxs-lookup"><span data-stu-id="d6329-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="d6329-486">Como parte da definição do índice, você pode adicionar um único sugestor à coleção de `suggesters` .</span><span class="sxs-lookup"><span data-stu-id="d6329-486">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="d6329-487">Propriedades que definem um sugestor incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d6329-487">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="d6329-488">`name`: o nome do sugestor.</span><span class="sxs-lookup"><span data-stu-id="d6329-488">`name`: The name of the suggester.</span></span> <span data-ttu-id="d6329-489">Use o nome do sugestor ao chamar a API de `suggest` .</span><span class="sxs-lookup"><span data-stu-id="d6329-489">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="d6329-490">`searchMode`: a estratégia usada para pesquisar frases candidatas.</span><span class="sxs-lookup"><span data-stu-id="d6329-490">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="d6329-491">O único modo com suporte atualmente é `analyzingInfixMatching`, que executa a correspondência flexível de frases no início ou no meio da frase.</span><span class="sxs-lookup"><span data-stu-id="d6329-491">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="d6329-492">`sourceFields`: uma lista de um ou mais campos que são a fonte do conteúdo para obter sugestões.</span><span class="sxs-lookup"><span data-stu-id="d6329-492">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="d6329-493">Somente os campos dos tipos `Edm.String` e `Collection(Edm.String)` podem ser fontes de sugestões.</span><span class="sxs-lookup"><span data-stu-id="d6329-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="d6329-494">Somente os campos que não têm um analisador de idioma personalizado definido podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="d6329-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="d6329-495">**Exemplo de sugestor**</span><span class="sxs-lookup"><span data-stu-id="d6329-495">**Suggester Example**</span></span>

<span data-ttu-id="d6329-496">Um sugestor faz parte do índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-496">A suggester is part of the index.</span></span> <span data-ttu-id="d6329-497">Apenas um sugestor pode existir na coleção do `suggesters` na versão atual, junto com a coleção de campos e `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="d6329-497">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="d6329-498">Se você usou a versão de visualização pública do Azure Search, `suggesters` substitui uma propriedade booliana antiga (`"suggestions": false`) que dava suporte apenas a sugestões de prefixo para cadeias de caracteres curtas (3-25 caracteres).</span><span class="sxs-lookup"><span data-stu-id="d6329-498">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="d6329-499">Sua substituição, `suggesters`, dá suporte à correspondências infixas que localizam os termos correspondentes no início ou no meio do conteúdo do campo, com melhor tolerância para erros em cadeias de caracteres de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="d6329-500">Começando com a versão disponível, esta é a única implementação da API de sugestões.</span><span class="sxs-lookup"><span data-stu-id="d6329-500">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="d6329-501">A propriedade `suggestions` mais antiga que foi introduzida na `api-version=2014-07-31-Preview` continua funcionando nessa versão, mas não na versão `2015-02-28` ou posteriores da Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-501">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="d6329-502">Atualizar o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-502">Update Index</span></span>
<span data-ttu-id="d6329-503">Você pode atualizar um índice existente no Azure Search usando uma solicitação HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="d6329-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="d6329-504">As atualizações podem incluir adição de novos campos ao esquema existente, modificação de opções de CORS e modificação de perfis de pontuação.</span><span class="sxs-lookup"><span data-stu-id="d6329-504">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="d6329-505">Confira [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="d6329-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="d6329-506">Especifique o nome do índice a ser atualizado no URI da solicitação:</span><span class="sxs-lookup"><span data-stu-id="d6329-506">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d6329-507">**Importante:** o suporte para atualizações de esquema de índice é limitado às operações que não exigem a recriação do índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-507">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="d6329-508">Atualmente, não há suporte às atualizações de esquema que exigem reindexação, como a alteração de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="d6329-509">Novos campos podem ser adicionados a qualquer momento, embora os campos existentes não possam ser alterados nem excluídos.</span><span class="sxs-lookup"><span data-stu-id="d6329-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="d6329-510">O mesmo se aplica a `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="d6329-510">The same applies to `suggesters`.</span></span> <span data-ttu-id="d6329-511">Novos campos podem ser adicionados a um sugestor no momento em que os campos são adicionados, mas os campos não podem ser removidos dos `suggesters` e campos existentes não podem ser adicionados a `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="d6329-511">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="d6329-512">Ao se adicionar um novo campo a um índice, todos os documentos existentes no índice automaticamente terão um valor nulo para esse campo.</span><span class="sxs-lookup"><span data-stu-id="d6329-512">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="d6329-513">Nenhum espaço de armazenamento adicional será consumido até que novos documentos sejam adicionados ao índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-513">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="d6329-514">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-514">**Request**</span></span>

<span data-ttu-id="d6329-515">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d6329-516">A solicitação **Atualizar Índice** é criada usando HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="d6329-516">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="d6329-517">Com PUT, o nome do índice é parte da URL.</span><span class="sxs-lookup"><span data-stu-id="d6329-517">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="d6329-518">Se o índice não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="d6329-518">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="d6329-519">Se já existir, ele será atualizado para a nova definição.</span><span class="sxs-lookup"><span data-stu-id="d6329-519">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="d6329-520">O nome do índice deve estar em letras minúsculas, começar com uma letra ou número, não conter barras ou pontos e ter menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6329-520">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="d6329-521">Depois de iniciar o nome do índice com uma letra ou número, o restante do nome pode incluir qualquer letra, número e traços, desde que os traços não sejam consecutivos.</span><span class="sxs-lookup"><span data-stu-id="d6329-521">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="d6329-522">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-523">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-523">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-524">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-525">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-525">**Request Headers**</span></span>

<span data-ttu-id="d6329-526">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-526">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-527">`Content-Type`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-527">`Content-Type`: Required.</span></span> <span data-ttu-id="d6329-528">Defina-o como `application/json`</span><span class="sxs-lookup"><span data-stu-id="d6329-528">Set this to `application/json`</span></span>
* <span data-ttu-id="d6329-529">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-529">`api-key`: Required.</span></span> <span data-ttu-id="d6329-530">A `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-530">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-531">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-531">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-532">A solicitação **Atualizar Índice** deve incluir um cabeçalho `api-key` definido como sua chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-532">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-533">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-533">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-534">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-534">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-535">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-535">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-536">**Sintaxe de corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-536">**Request Body Syntax**</span></span>

<span data-ttu-id="d6329-537">Ao se atualizar um índice existente, o corpo deve incluir a definição de esquema original, além de novos campos que você está adicionando, bem como os perfis de pontuação modificados, sugestores e as opções de CORS, se houver.</span><span class="sxs-lookup"><span data-stu-id="d6329-537">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="d6329-538">Se não estiver modificando os perfis de pontuação e as opções de CORS, você deverá incluir os originais de quando o índice foi criado.</span><span class="sxs-lookup"><span data-stu-id="d6329-538">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="d6329-539">Em geral, o melhor padrão a ser usado para atualizações é recuperar a definição do índice com GET, modificá-la e atualizá-la com PUT.</span><span class="sxs-lookup"><span data-stu-id="d6329-539">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="d6329-540">A sintaxe do esquema usada para criar um índice é reproduzida aqui para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="d6329-540">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="d6329-541">Consulte [Criar Índice](#CreateIndex) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="d6329-542">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-542">**Response**</span></span>

<span data-ttu-id="d6329-543">Para uma solicitação bem-sucedida: "204 sem Conteúdo".</span><span class="sxs-lookup"><span data-stu-id="d6329-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="d6329-544">Por padrão, o corpo da resposta estará vazio.</span><span class="sxs-lookup"><span data-stu-id="d6329-544">By default the response body will be empty.</span></span> <span data-ttu-id="d6329-545">No entanto, se o cabeçalho `Prefer` da solicitação for definido como `return=representation`, o corpo da resposta conterá o JSON para a definição de índice que foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="d6329-545">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="d6329-546">Nesse caso, o código de status de êxito será "200 OK".</span><span class="sxs-lookup"><span data-stu-id="d6329-546">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="d6329-547">**Atualizando a definição de índice com analisadores personalizados**</span><span class="sxs-lookup"><span data-stu-id="d6329-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="d6329-548">Quando um analisador, um criador de token, um filtro de token ou um filtro de char é definido, ele não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="d6329-549">Outros novos poderão ser adicionados a um índice existente apenas se o sinalizador `allowIndexDowntime` estiver definido como true na solicitação de atualização de índice:</span><span class="sxs-lookup"><span data-stu-id="d6329-549">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="d6329-550">Observe que essa operação deixará seu índice offline por pelo menos alguns segundos, fazendo com que suas solicitações de indexação e de consulta falhem.</span><span class="sxs-lookup"><span data-stu-id="d6329-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="d6329-551">O desempenho e a disponibilidade de gravação do índice podem ser prejudicados por vários minutos após o índice ser atualizado, ou por mais tempo em caso de índices muito grandes.</span><span class="sxs-lookup"><span data-stu-id="d6329-551">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="d6329-552">Listar Índices</span><span class="sxs-lookup"><span data-stu-id="d6329-552">List Indexes</span></span>
<span data-ttu-id="d6329-553">A operação **Listar Índices** retorna uma lista dos índices existentes no momento em seu serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6329-553">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="d6329-554">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-554">**Request**</span></span>

<span data-ttu-id="d6329-555">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d6329-556">A solicitação **Listar Índices** pode ser criada usando o método GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-556">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="d6329-557">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-558">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-558">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-559">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-560">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-560">**Request Headers**</span></span>

<span data-ttu-id="d6329-561">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-561">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-562">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-562">`api-key`: Required.</span></span> <span data-ttu-id="d6329-563">A `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-563">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-564">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-564">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-565">A solicitação **Listar Índices** deve incluir uma `api-key` definida como uma chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-565">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-566">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-566">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-567">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-567">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-568">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-568">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-569">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-569">**Request Body**</span></span>

<span data-ttu-id="d6329-570">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="d6329-570">None.</span></span>

<span data-ttu-id="d6329-571">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-571">**Response**</span></span>

<span data-ttu-id="d6329-572">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d6329-573">Aqui está um exemplo de corpo de resposta:</span><span class="sxs-lookup"><span data-stu-id="d6329-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="d6329-574">Observe que você pode filtrar a resposta para apenas as propriedades em que está interessado.</span><span class="sxs-lookup"><span data-stu-id="d6329-574">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="d6329-575">Por exemplo, se você quiser apenas uma lista de nomes de índice, use a opção de consulta OData `$select` :</span><span class="sxs-lookup"><span data-stu-id="d6329-575">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="d6329-576">Nesse caso, a resposta do exemplo anterior seria exibida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d6329-576">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="d6329-577">Essa é uma técnica útil para economizar largura de banda se você tiver muitos índices em seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-577">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="d6329-578">Obter o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-578">Get Index</span></span>
<span data-ttu-id="d6329-579">A operação **Obter Índice** obtém a definição de índice do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6329-579">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="d6329-580">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-580">**Request**</span></span>

<span data-ttu-id="d6329-581">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="d6329-582">A solicitação **Obter Índice** pode ser criada usando o método GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-582">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="d6329-583">O [nome do índice] na solicitação URI especifica qual índice deve ser retornado da coleção de índices.</span><span class="sxs-lookup"><span data-stu-id="d6329-583">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="d6329-584">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-585">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-585">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-586">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-587">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-587">**Request Headers**</span></span>

<span data-ttu-id="d6329-588">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-588">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-589">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-589">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-590">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-590">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-591">A solicitação **Obter Índice** deve incluir uma `api-key` definida como uma chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-591">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-592">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-592">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-593">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-593">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-594">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-594">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-595">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-595">**Request Body**</span></span>

<span data-ttu-id="d6329-596">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="d6329-596">None.</span></span>

<span data-ttu-id="d6329-597">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-597">**Response**</span></span>

<span data-ttu-id="d6329-598">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d6329-599">Consulte o exemplo de JSON em [Criando e atualizando um índice](#CreateUpdateIndexExample) para obter um exemplo da carga de resposta.</span><span class="sxs-lookup"><span data-stu-id="d6329-599">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="d6329-600">Excluir o índice</span><span class="sxs-lookup"><span data-stu-id="d6329-600">Delete Index</span></span>
<span data-ttu-id="d6329-601">A operação **Excluir Índice** remove um índice e os documentos associados de seu serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6329-601">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="d6329-602">Você pode obter o nome do índice por meio do painel de serviço no Portal  do Azure ou por meio da API.</span><span class="sxs-lookup"><span data-stu-id="d6329-602">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="d6329-603">Consulte [Listar índices](#ListIndexes) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="d6329-604">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-604">**Request**</span></span>

<span data-ttu-id="d6329-605">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="d6329-606">A solicitação **Excluir Índice** pode ser criada usando o método DELETE.</span><span class="sxs-lookup"><span data-stu-id="d6329-606">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="d6329-607">O [nome do índice] no URI da solicitação especifica qual índice deve ser excluído da coleção de índices.</span><span class="sxs-lookup"><span data-stu-id="d6329-607">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="d6329-608">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-609">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-609">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-610">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-611">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-611">**Request Headers**</span></span>

<span data-ttu-id="d6329-612">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-612">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-613">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-613">`api-key`: Required.</span></span> <span data-ttu-id="d6329-614">A `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-614">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-615">É um valor de cadeia de caracteres exclusivo para a URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-615">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="d6329-616">A solicitação **Excluir Índice** deve incluir um cabeçalho de `api-key` definido como sua chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-616">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-617">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-617">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-618">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-618">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-619">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-619">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-620">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-620">**Request Body**</span></span>

<span data-ttu-id="d6329-621">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="d6329-621">None.</span></span>

<span data-ttu-id="d6329-622">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-622">**Response**</span></span>

<span data-ttu-id="d6329-623">Código de status: 204 Sem Conteúdo é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="d6329-624">Obter estatísticas de índice</span><span class="sxs-lookup"><span data-stu-id="d6329-624">Get Index Statistics</span></span>
<span data-ttu-id="d6329-625">A operação **Obter Estatísticas do Índice** retorna uma contagem de documentos do Azure Search para o índice atual, além do uso do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d6329-625">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="d6329-626">As estatísticas de tamanho de armazenamento e contagem de documentos são coletadas a cada poucos minutos, não em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d6329-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="d6329-627">Portanto, talvez as estatísticas retornadas por essa API não reflitam as alterações causadas por operações de indexação recentes.</span><span class="sxs-lookup"><span data-stu-id="d6329-627">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="d6329-628">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-628">**Request**</span></span>

<span data-ttu-id="d6329-629">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="d6329-630">A solicitação **Obter Estatísticas do Índice** pode ser criada usando o método GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-630">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="d6329-631">O [nome do índice] no URI da solicitação instrui o serviço a retornar as estatísticas de índice para o índice especificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-631">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="d6329-632">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-633">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-633">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-634">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-635">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-635">**Request Headers**</span></span>

<span data-ttu-id="d6329-636">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-636">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-637">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-637">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-638">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-638">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-639">A solicitação **Obter Estatísticas de Índice** deve incluir um `api-key` definido como uma chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-639">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-640">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-640">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-641">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-641">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-642">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-642">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-643">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-643">**Request Body**</span></span>

<span data-ttu-id="d6329-644">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="d6329-644">None.</span></span>

<span data-ttu-id="d6329-645">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-645">**Response**</span></span>

<span data-ttu-id="d6329-646">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d6329-647">O corpo da resposta está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="d6329-647">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="d6329-648">Analisador de teste</span><span class="sxs-lookup"><span data-stu-id="d6329-648">Test Analyzer</span></span>
<span data-ttu-id="d6329-649">O **Analisar API** mostra como um analisador divide o texto em tokens.</span><span class="sxs-lookup"><span data-stu-id="d6329-649">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d6329-650">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-650">**Request**</span></span>

<span data-ttu-id="d6329-651">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="d6329-652">A solicitação **Analisar API** pode ser criada usando o método POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-652">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="d6329-653">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-654">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-654">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-655">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-656">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-656">**Request Headers**</span></span>

<span data-ttu-id="d6329-657">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-657">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-658">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-658">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-659">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-659">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-660">A solicitação **Analisar API** deve incluir uma `api-key` definida como uma chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-660">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-661">Você também precisará do nome do índice e do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-661">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-662">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-662">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-663">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-663">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-664">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-664">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="d6329-665">ou o</span><span class="sxs-lookup"><span data-stu-id="d6329-665">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="d6329-666">`analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` precisam ser nomes válidos de analisadores, criadores de token, filtros de token e filtros de char predefinidos ou personalizados para o índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-666">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="d6329-667">Para saber mais sobre o processo de análise léxica, consulte [Análise na Pesquisa do Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="d6329-667">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="d6329-668">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-668">**Response**</span></span>

<span data-ttu-id="d6329-669">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d6329-670">O corpo da resposta está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="d6329-670">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="d6329-671">**Analisar exemplo de API**</span><span class="sxs-lookup"><span data-stu-id="d6329-671">**Analyze API example**</span></span>

<span data-ttu-id="d6329-672">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-672">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="d6329-673">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="d6329-674">Operações de documento</span><span class="sxs-lookup"><span data-stu-id="d6329-674">Document Operations</span></span>
<span data-ttu-id="d6329-675">Na Pesquisa do Azure, um índice é armazenado na nuvem e preenchido usando documentos JSON que você carrega no serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-675">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="d6329-676">Todos os documentos que você carrega formam o corpus de seus dados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-676">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="d6329-677">Documentos contêm campos, alguns dos quais são indexados em termos de pesquisa ao serem carregados.</span><span class="sxs-lookup"><span data-stu-id="d6329-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="d6329-678">O segmento de URL `/docs` na API do Azure Search representa a coleção de documentos em um índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-678">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="d6329-679">Todas as operações executadas na coleção, como carregar, mesclar, excluir ou consultar documentos, ocorrem no contexto de um único índice. Portanto, as URLs para essas operações sempre começarão com `/indexes/[index name]/docs` para um nome de índice específico.</span><span class="sxs-lookup"><span data-stu-id="d6329-679">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="d6329-680">O código do aplicativo deve gerar documentos JSON a serem carregados no Azure Search ou é possível usar um [indexador](https://msdn.microsoft.com/library/dn946891.aspx) para carregar documentos, caso a fonte de dados seja o Banco de Dados SQL do Azure ou o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6329-680">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="d6329-681">Normalmente, os índices são preenchidos por meio de um único conjunto de dados que você fornece.</span><span class="sxs-lookup"><span data-stu-id="d6329-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="d6329-682">Você deve planejar ter um documento para cada item que deseja pesquisar.</span><span class="sxs-lookup"><span data-stu-id="d6329-682">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="d6329-683">Um aplicativo de aluguel de filmes pode ter um documento por filme, um aplicativo de vitrine pode ter um documento por SKU, um aplicativo de cursos online pode ter um documento por curso, uma empresa de pesquisa pode ter um documento para cada artigo acadêmico em seu repositório e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d6329-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="d6329-684">Os documentos consistem em um ou mais campos.</span><span class="sxs-lookup"><span data-stu-id="d6329-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="d6329-685">Os campos podem conter texto indexado pelo Azure Search em termos de pesquisa, bem como valores não indexados ou que não são de texto, que podem ser usadas em filtros ou perfis de pontuação.</span><span class="sxs-lookup"><span data-stu-id="d6329-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="d6329-686">Os nomes, tipos de dados e recursos de pesquisa com suporte para cada campo são determinados pelo esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-686">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="d6329-687">Um dos campos em cada esquema de índice deve ser designado como uma ID, e cada documento deve ter um valor para o campo de ID que identifique de forma exclusiva o documento no índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-687">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="d6329-688">Todos os outros campos de documento são opcionais e usarão como padrão um valor nulo, se o valor não for especificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-688">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="d6329-689">Observe que os valores nulos não ocupam espaço no índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-689">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="d6329-690">Para poder carregar documentos, você precisa já ter criado o índice no serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-690">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="d6329-691">Consulte [Criar o índice](#CreateIndex) para obter detalhes sobre essa primeira etapa.</span><span class="sxs-lookup"><span data-stu-id="d6329-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="d6329-692">Adicionar, Atualizar ou Excluir Documentos</span><span class="sxs-lookup"><span data-stu-id="d6329-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="d6329-693">Você pode carregar, mesclar, mesclar ou carregar ou excluir documentos de um índice especificado usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="d6329-694">Para um grande número de atualizações, recomenda-se o processamento em lotes de documentos (até 1000 documentos ou aproximadamente 16 MB por lote).</span><span class="sxs-lookup"><span data-stu-id="d6329-694">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="d6329-695">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-695">**Request**</span></span>

<span data-ttu-id="d6329-696">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="d6329-697">Você pode carregar, mesclar, mesclar ou carregar ou excluir documentos de um índice especificado usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="d6329-698">O URI da solicitação inclui o [nome do índice], especificando em qual índice postar documentos.</span><span class="sxs-lookup"><span data-stu-id="d6329-698">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="d6329-699">Só é possível postar documentos em um índice por vez.</span><span class="sxs-lookup"><span data-stu-id="d6329-699">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="d6329-700">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-701">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-701">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-702">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-703">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-703">**Request Headers**</span></span>

<span data-ttu-id="d6329-704">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-704">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-705">`Content-Type`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-705">`Content-Type`: Required.</span></span> <span data-ttu-id="d6329-706">Defina-o como `application/json`</span><span class="sxs-lookup"><span data-stu-id="d6329-706">Set this to `application/json`</span></span>
* <span data-ttu-id="d6329-707">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d6329-707">`api-key`: Required.</span></span> <span data-ttu-id="d6329-708">A `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-708">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-709">É um valor de cadeia de caracteres exclusivo de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-709">It is a string value, unique to your service.</span></span> <span data-ttu-id="d6329-710">A solicitação **Adicionar Documentos** deve incluir um cabeçalho de `api-key` definido como sua chave de administração (em vez de uma chave de consulta).</span><span class="sxs-lookup"><span data-stu-id="d6329-710">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="d6329-711">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-711">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-712">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-712">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-713">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-713">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-714">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-714">**Request Body**</span></span>

<span data-ttu-id="d6329-715">O corpo da solicitação contém um ou mais documentos a serem indexados.</span><span class="sxs-lookup"><span data-stu-id="d6329-715">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="d6329-716">Os documentos são identificados por uma chave exclusiva.</span><span class="sxs-lookup"><span data-stu-id="d6329-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="d6329-717">Cada documento está associado uma ação: carregar, mesclar, mesclar ou carregar ou excluir.</span><span class="sxs-lookup"><span data-stu-id="d6329-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="d6329-718">As solicitações de carregamento devem incluir os dados do documento como um conjunto de pares de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="d6329-718">Upload requests must include the document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="d6329-719">As chaves de documento só podem conter letras, números, traços ("-"), sublinhados ("_") e sinais de igual ("=").</span><span class="sxs-lookup"><span data-stu-id="d6329-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="d6329-720">Para obter mais detalhes, veja [Regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="d6329-721">**Ações do documento**</span><span class="sxs-lookup"><span data-stu-id="d6329-721">**Document Actions**</span></span>

* <span data-ttu-id="d6329-722">`upload`: uma ação de carregamento é semelhante a um "upsert", em que o documento será inserido se for novo e será atualizado/substituído se ele existir.</span><span class="sxs-lookup"><span data-stu-id="d6329-722">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="d6329-723">Observe que todos os campos são substituídos no caso da atualização.</span><span class="sxs-lookup"><span data-stu-id="d6329-723">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="d6329-724">`merge`: a mesclagem atualiza um documento existente com os campos especificados.</span><span class="sxs-lookup"><span data-stu-id="d6329-724">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="d6329-725">Se o documento não existir, a mesclagem falhará.</span><span class="sxs-lookup"><span data-stu-id="d6329-725">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="d6329-726">Qualquer campo que você especificar em uma mesclagem substituirá o campo existente no documento.</span><span class="sxs-lookup"><span data-stu-id="d6329-726">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="d6329-727">Isso inclui campos do tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="d6329-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="d6329-728">Por exemplo, se o documento contiver um campo "marcas" com o valor `["budget"]` e você executar uma mesclagem com o valor `["economy", "pool"]` para "marcas", o valor final do campo "marcas" final será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="d6329-728">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="d6329-729">Ele **não** será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="d6329-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="d6329-730">`mergeOrUpload`: se comportará como `merge` se já existir um documento com a chave especificada no índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-730">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="d6329-731">Se o documento não existir, se comportará como `upload` com um novo documento.</span><span class="sxs-lookup"><span data-stu-id="d6329-731">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="d6329-732">`delete`: a exclusão remove o documento especificado do índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-732">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="d6329-733">Observe que todos os campos que você especificar em uma operação `delete` , exceto o campo de chave, serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="d6329-733">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="d6329-734">Se você quiser remover um campo individual de um documento, use `merge` em vez disso e apenas defina o campo explicitamente como `null`.</span><span class="sxs-lookup"><span data-stu-id="d6329-734">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="d6329-735">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-735">**Response**</span></span>

<span data-ttu-id="d6329-736">O código de status 200 (OK) é retornado para uma resposta bem-sucedida, indicando que todos os itens foram indexados com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6329-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="d6329-737">Isso é indicado pela propriedade `status` sendo definida como verdadeira para todos os itens, bem como a propriedade `statusCode` sendo definida como 201 (para documentos carregados recentemente) ou 200 (para documentos mesclados ou excluídos):</span><span class="sxs-lookup"><span data-stu-id="d6329-737">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="d6329-738">O código de status 207 (Multi-Status) será retornado quando pelo menos um item não tiver sido indexado com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6329-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="d6329-739">Os itens que não foram indexados têm o campo `status` definido como falso.</span><span class="sxs-lookup"><span data-stu-id="d6329-739">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="d6329-740">As propriedades `errorMessage` e `statusCode` indicarão o motivo do erro de indexação:</span><span class="sxs-lookup"><span data-stu-id="d6329-740">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="d6329-741">A tabela a seguir explica os vários códigos de status de cada documento que podem ser retornados na resposta.</span><span class="sxs-lookup"><span data-stu-id="d6329-741">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="d6329-742">Observe que alguns indicam problemas com a solicitação em si, enquanto outros indicam condições de erro temporárias.</span><span class="sxs-lookup"><span data-stu-id="d6329-742">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="d6329-743">Você deve testar o último novamente após um atraso.</span><span class="sxs-lookup"><span data-stu-id="d6329-743">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="d6329-744">Código de status</span><span class="sxs-lookup"><span data-stu-id="d6329-744">Status code</span></span></th>
        <th><span data-ttu-id="d6329-745">Significado</span><span class="sxs-lookup"><span data-stu-id="d6329-745">Meaning</span></span></th>
        <th><span data-ttu-id="d6329-746">Com nova tentativa</span><span class="sxs-lookup"><span data-stu-id="d6329-746">Retryable</span></span></th>
        <th><span data-ttu-id="d6329-747">Observações</span><span class="sxs-lookup"><span data-stu-id="d6329-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-748">200</span><span class="sxs-lookup"><span data-stu-id="d6329-748">200</span></span></td>
        <td><span data-ttu-id="d6329-749">O documento foi modificado ou excluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6329-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="d6329-750">n/d</span><span class="sxs-lookup"><span data-stu-id="d6329-750">n/a</span></span></td>
        <td><span data-ttu-id="d6329-751">As operações de exclusão são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="d6329-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="d6329-752">Ou seja, mesmo se não existir uma chave de documento no índice, a tentativa de uma operação de exclusão com essa chave resultará em um código de status 200.</span><span class="sxs-lookup"><span data-stu-id="d6329-752">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-753">201</span><span class="sxs-lookup"><span data-stu-id="d6329-753">201</span></span></td>
        <td><span data-ttu-id="d6329-754">O documento foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="d6329-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="d6329-755">n/d</span><span class="sxs-lookup"><span data-stu-id="d6329-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-756">400</span><span class="sxs-lookup"><span data-stu-id="d6329-756">400</span></span></td>
        <td><span data-ttu-id="d6329-757">Ocorreu um erro no documento que o impediu de ser indexado.</span><span class="sxs-lookup"><span data-stu-id="d6329-757">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="d6329-758">Não</span><span class="sxs-lookup"><span data-stu-id="d6329-758">No</span></span></td>
        <td><span data-ttu-id="d6329-759">A mensagem de erro na resposta indicará o que há de errado com o documento.</span><span class="sxs-lookup"><span data-stu-id="d6329-759">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-760">404</span><span class="sxs-lookup"><span data-stu-id="d6329-760">404</span></span></td>
        <td><span data-ttu-id="d6329-761">Não foi possível mesclar o documento porque a chave especificada não existe no índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-761">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="d6329-762">Não</span><span class="sxs-lookup"><span data-stu-id="d6329-762">No</span></span></td>
        <td><span data-ttu-id="d6329-763">Esse erro não ocorre em carregamentos, uma vez que eles criam novos documentos e não ocorre em exclusões porque elas são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="d6329-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-764">409</span><span class="sxs-lookup"><span data-stu-id="d6329-764">409</span></span></td>
        <td><span data-ttu-id="d6329-765">Foi detectado um conflito de versão durante a tentativa de indexar um documento.</span><span class="sxs-lookup"><span data-stu-id="d6329-765">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="d6329-766">Sim</span><span class="sxs-lookup"><span data-stu-id="d6329-766">Yes</span></span></td>
        <td><span data-ttu-id="d6329-767">Isso pode acontecer quando você está tentando indexar o mesmo documento mais de uma vez simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="d6329-767">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-768">422</span><span class="sxs-lookup"><span data-stu-id="d6329-768">422</span></span></td>
        <td><span data-ttu-id="d6329-769">O índice está temporariamente indisponível porque ele foi atualizado com o sinalizador 'allowIndexDowntime' definido como 'verdadeiro'.</span><span class="sxs-lookup"><span data-stu-id="d6329-769">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="d6329-770">Sim</span><span class="sxs-lookup"><span data-stu-id="d6329-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="d6329-771">503</span><span class="sxs-lookup"><span data-stu-id="d6329-771">503</span></span></td>
        <td><span data-ttu-id="d6329-772">O serviço de pesquisa está temporariamente indisponível, possivelmente devido a uma carga pesada.</span><span class="sxs-lookup"><span data-stu-id="d6329-772">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="d6329-773">Sim</span><span class="sxs-lookup"><span data-stu-id="d6329-773">Yes</span></span></td>
        <td><span data-ttu-id="d6329-774">Neste caso, seu código deverá ser colocado em espera antes de uma nova tentativa, sob o risco de prolongar a indisponibilidade do serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-774">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="d6329-775">**Observação**: se o seu código de cliente encontra com frequência uma resposta 207, um motivo possível para isso é que o sistema está sobrecarregado.</span><span class="sxs-lookup"><span data-stu-id="d6329-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="d6329-776">Você pode confirmar isso verificando a propriedade `statusCode` para 503.</span><span class="sxs-lookup"><span data-stu-id="d6329-776">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="d6329-777">Se esse for o caso, será recomendável a ***limitação de solicitações de indexação***.</span><span class="sxs-lookup"><span data-stu-id="d6329-777">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="d6329-778">Caso contrário, se a indexação de tráfego não diminuir, o sistema poderá começar a rejeitar todas as solicitações com erros 503.</span><span class="sxs-lookup"><span data-stu-id="d6329-778">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="d6329-779">O código de status 429 indica que você excedeu sua cota no número de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-779">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="d6329-780">Você deve criar um novo índice ou atualizar para limites de capacidade mais altos.</span><span class="sxs-lookup"><span data-stu-id="d6329-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="d6329-781">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="d6329-781">**Example:**</span></span>

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="d6329-782">Pesquisar Documentos</span><span class="sxs-lookup"><span data-stu-id="d6329-782">Search Documents</span></span>
<span data-ttu-id="d6329-783">Uma operação **Search** é emitida como uma solicitação GET ou POST e especifica parâmetros que fornecem os critérios para a seleção de documentos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="d6329-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="d6329-784">**Quando usar POST em vez de GET**</span><span class="sxs-lookup"><span data-stu-id="d6329-784">**When to use POST instead of GET**</span></span>

<span data-ttu-id="d6329-785">Quando você usa o HTTP GET para chamar a API de **Search** , é preciso estar ciente de que o comprimento da URL da solicitação não pode exceder 8 KB.</span><span class="sxs-lookup"><span data-stu-id="d6329-785">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="d6329-786">Isso costuma ser suficiente para a maioria dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d6329-786">This is usually enough for most applications.</span></span> <span data-ttu-id="d6329-787">No entanto, alguns aplicativos geram consultas muito grandes ou expressões de filtro OData.</span><span class="sxs-lookup"><span data-stu-id="d6329-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="d6329-788">Para esses aplicativos, usar HTTP POST é uma opção melhor, pois permite filtros e consultas maiores que o GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="d6329-789">Com o POST, o número de termos ou cláusulas em uma consulta é o fator limitante, não o tamanho da consulta processada, uma vez que o limite de tamanho da solicitação POST é quase 16 MB.</span><span class="sxs-lookup"><span data-stu-id="d6329-789">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-790">Embora o limite de tamanho da solicitação POST seja muito grande, consultas de pesquisa e expressões de filtro não podem ser arbitrariamente complexos.</span><span class="sxs-lookup"><span data-stu-id="d6329-790">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="d6329-791">Confira a [Sintaxe de consulta Lucene](https://msdn.microsoft.com/library/mt589323.aspx) e a [Sintaxe de expressão OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de consulta e filtro de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="d6329-792">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-792">**Request**</span></span>

<span data-ttu-id="d6329-793">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="d6329-794">A solicitação **Pesquisar** pode ser criada usando os métodos GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-794">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="d6329-795">O URI da solicitação especifica qual índice deve ser consultado para todos os documentos que correspondem aos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d6329-795">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="d6329-796">Parâmetros são especificados na cadeia de consulta no caso de solicitações GET e no corpo da solicitação no caso de solicitações POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-796">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="d6329-797">Como prática recomendada ao criar solicitações GET, lembre-se de [codificar na URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) os parâmetros de consulta específicos ao chamar a API REST diretamente.</span><span class="sxs-lookup"><span data-stu-id="d6329-797">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="d6329-798">Para operações de **Pesquisa** , isso inclui:</span><span class="sxs-lookup"><span data-stu-id="d6329-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="d6329-799">A codificação de URL é recomendada apenas nos parâmetros da consulta acima.</span><span class="sxs-lookup"><span data-stu-id="d6329-799">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="d6329-800">Se você inadvertidamente codificar na URL a cadeia de caracteres de consulta inteira (tudo após o ?), as solicitações serão interrompidas.</span><span class="sxs-lookup"><span data-stu-id="d6329-800">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="d6329-801">Além disso, a codificação de URL só é necessária ao se chamar a API REST diretamente usando GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-801">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="d6329-802">Nenhuma codificação de URL é necessária ao chamar a **Pesquisa** usando POST, ou ao usar a [biblioteca cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que processa a codificação de URL para você.</span><span class="sxs-lookup"><span data-stu-id="d6329-802">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="d6329-803"><a name="SearchQueryParameters"></a>
**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="d6329-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="d6329-804">**Search** aceita vários parâmetros que fornecem critérios de consulta e especificam o comportamento da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="d6329-805">Você fornece esses parâmetros na cadeia de consulta da URL ao chamar **Pesquisar** via GET e como propriedades JSON no corpo da solicitação ao chamar **Pesquisar** via POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-805">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="d6329-806">A sintaxe para alguns parâmetros é ligeiramente diferente entre GET e POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-806">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="d6329-807">Essas diferenças são indicadas, como aplicável, abaixo:</span><span class="sxs-lookup"><span data-stu-id="d6329-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="d6329-808">`search=[string]` (opcional) ‒ o texto a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="d6329-808">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="d6329-809">Todos os campos `searchable` são pesquisados por padrão, a menos que `searchFields` sejam especificados.</span><span class="sxs-lookup"><span data-stu-id="d6329-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="d6329-810">Ao pesquisar os campos `searchable`, é gerado um token para o próprio texto de pesquisa. Assim, vários termos podem ser separados por um espaço em branco (por exemplo: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="d6329-810">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="d6329-811">Para corresponder a qualquer termo, use `*` (isso pode ser útil para consultas de filtros boolianos).</span><span class="sxs-lookup"><span data-stu-id="d6329-811">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="d6329-812">A omissão desse parâmetro tem o mesmo efeito que sua definição como `*`.</span><span class="sxs-lookup"><span data-stu-id="d6329-812">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="d6329-813">Consulte [Sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) para obter informações específicas sobre a sintaxe de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="d6329-814">**Observação**: os resultados às vezes podem ser surpreendentes ao se consultar sobre campos `searchable`.</span><span class="sxs-lookup"><span data-stu-id="d6329-814">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="d6329-815">O criador de token inclui lógica para lidar com casos comuns para texto em inglês, como apóstrofos, vírgulas em números etc. Por exemplo, `search=123,456` corresponderá a um único termo, 123,456, em vez de cada um do termos 123 e 456, já que as vírgulas são usadas como separadores de milhar para números grandes em inglês.</span><span class="sxs-lookup"><span data-stu-id="d6329-815">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="d6329-816">Por esse motivo, recomendamos o uso de espaços em branco em vez de pontuação para separar os termos do parâmetro `search`.</span><span class="sxs-lookup"><span data-stu-id="d6329-816">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="d6329-817">`searchMode=any|all` (opcional; o padrão é `any`) ‒ se for necessária a correspondência de algum dos termos de pesquisa ou de todos eles para que o documento seja contado como uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="d6329-817">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="d6329-818">`searchFields=[string]` (opcional) ‒ a lista de nomes de campos separados por vírgulas para pesquisar o texto especificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-818">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="d6329-819">Os campos de destino devem ser marcados como `searchable`.</span><span class="sxs-lookup"><span data-stu-id="d6329-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="d6329-820">`queryType=simple|full` (opcional, o padrão é `simple`) - quando definido como texto de pesquisa "simples", é interpretado usando uma linguagem de consulta simples que permite símbolos como +, * e "".</span><span class="sxs-lookup"><span data-stu-id="d6329-820">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="d6329-821">As consultas são avaliadas em todos os campos pesquisáveis (ou nos campos indicados em `searchFields`) em cada documento por padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="d6329-822">Quando o tipo de consulta for definido como `full` , o texto de pesquisa será interpretado usando a linguagem de consulta Lucene, que permite pesquisas de campo específicos e ponderadas.</span><span class="sxs-lookup"><span data-stu-id="d6329-822">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="d6329-823">Confira [Sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) e [Sintaxe de consulta Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para obter informações específicas sobre sintaxes de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6329-824">A pesquisa do intervalo na linguagem de consulta Lucene não tem suporte a $filter, que oferece funcionalidade semelhante.</span><span class="sxs-lookup"><span data-stu-id="d6329-824">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="d6329-825">`moreLikeThis=[key]` (opcional) **Importante:** esse recurso só está disponível na `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-826">Essa opção não pode ser usada em uma consulta que contém o parâmetro de pesquisa de texto `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="d6329-826">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="d6329-827">O parâmetro `moreLikeThis` localiza os documentos que são semelhantes ao documento especificado pela chave do documento.</span><span class="sxs-lookup"><span data-stu-id="d6329-827">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="d6329-828">Quando é feita uma solicitação de pesquisa com `moreLikeThis`, uma lista de termos de pesquisa é gerada com base na frequência e raridade dos termos no documento de origem.</span><span class="sxs-lookup"><span data-stu-id="d6329-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="d6329-829">Esses termos são usados para fazer a solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-829">Those terms are then used to make the request.</span></span> <span data-ttu-id="d6329-830">Por padrão, o conteúdo de todos os campos `searchable` será considerado, a menos que `searchFields` seja usado para restringir quais campos são pesquisados.</span><span class="sxs-lookup"><span data-stu-id="d6329-830">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="d6329-831">`$skip=#` (opcional) ‒ o número de resultados da pesquisa a serem ignorados. Não pode ser superior a 100.000.</span><span class="sxs-lookup"><span data-stu-id="d6329-831">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="d6329-832">Se você precisar examinar os documentos em sequência, mas não puder usar `$skip` devido a essa limitação, considere o uso de `$orderby` em uma chave totalmente ordenada e `$filter` com um intervalo de consulta em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d6329-832">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-833">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `skip`, em vez de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="d6329-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="d6329-834">`$top=#` (opcional) ‒ o número de resultados da pesquisa a serem recuperados.</span><span class="sxs-lookup"><span data-stu-id="d6329-834">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="d6329-835">Isso pode ser usado em conjunto com `$skip` para implementar a paginação de cliente dos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-835">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-836">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `top`, em vez de `$top`.</span><span class="sxs-lookup"><span data-stu-id="d6329-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="d6329-837">`$count=true|false` (opcional; o padrão é `false`) ‒ especifica se é necessário buscar a contagem total de resultados.</span><span class="sxs-lookup"><span data-stu-id="d6329-837">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="d6329-838">Essa é a contagem de todos os documentos que correspondem aos parâmetros `search` e `$filter`, ignorando `$top` e `$skip`.</span><span class="sxs-lookup"><span data-stu-id="d6329-838">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="d6329-839">A definição desse valor como `true` pode afetar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d6329-839">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="d6329-840">Observe que a contagem retornada é uma aproximação.</span><span class="sxs-lookup"><span data-stu-id="d6329-840">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-841">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `count`, em vez de `$count`.</span><span class="sxs-lookup"><span data-stu-id="d6329-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="d6329-842">`$orderby=[string]` (opcional) ‒ uma lista de expressões separadas por vírgulas para classificar os resultados.</span><span class="sxs-lookup"><span data-stu-id="d6329-842">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="d6329-843">Cada expressão pode ser um nome de campo ou uma chamada para a função `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="d6329-843">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="d6329-844">Cada expressão pode ser seguida de `asc` para indicar a ordem crescente e `desc` para indicar a ordem decrescente.</span><span class="sxs-lookup"><span data-stu-id="d6329-844">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="d6329-845">O padrão é a ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="d6329-845">The default is ascending order.</span></span> <span data-ttu-id="d6329-846">Os empates serão resolvidos pelas pontuações de correspondência de documentos.</span><span class="sxs-lookup"><span data-stu-id="d6329-846">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="d6329-847">Se nenhum `$orderby` for especificado, a ordem de classificação padrão será decrescente de acordo com a pontuação de correspondência dos documentos.</span><span class="sxs-lookup"><span data-stu-id="d6329-847">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="d6329-848">Há um limite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d6329-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-849">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `orderby`, em vez de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d6329-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="d6329-850">`$select=[string]` (opcional) ‒ uma lista de campos separados por vírgulas a serem recuperados.</span><span class="sxs-lookup"><span data-stu-id="d6329-850">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="d6329-851">Se não for especificado, todos os campos marcados como recuperáveis no esquema serão incluídos.</span><span class="sxs-lookup"><span data-stu-id="d6329-851">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="d6329-852">Você pode solicitar explicitamente todos os campos ao definir esse parâmetro como `*`.</span><span class="sxs-lookup"><span data-stu-id="d6329-852">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-853">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `select`, em vez de `$select`.</span><span class="sxs-lookup"><span data-stu-id="d6329-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="d6329-854">`facet=[string]` (zero ou mais) ‒ um campo de acordo com o qual o facetamento deve ser realizado.</span><span class="sxs-lookup"><span data-stu-id="d6329-854">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="d6329-855">Opcionalmente, a cadeia de caracteres pode conter parâmetros para personalizar o facetamento expressado como pares separados por vírgulas `name:value` .</span><span class="sxs-lookup"><span data-stu-id="d6329-855">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="d6329-856">Os parâmetros válidos são:</span><span class="sxs-lookup"><span data-stu-id="d6329-856">Valid parameters are:</span></span>

* <span data-ttu-id="d6329-857">`count` (número máximo de termos de faceta; o padrão é 10).</span><span class="sxs-lookup"><span data-stu-id="d6329-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="d6329-858">Não há um máximo, mas os valores mais altos incorrerão em uma penalidade de desempenho correspondente, principalmente se o campo facetado contiver um grande número de termos exclusivos.</span><span class="sxs-lookup"><span data-stu-id="d6329-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="d6329-859">Por exemplo: `facet=category,count:5` obtém as cinco principais categorias nos resultados de faceta.</span><span class="sxs-lookup"><span data-stu-id="d6329-859">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="d6329-860">**Observação**: se o parâmetro `count` for menor do que o número de termos exclusivos, os resultados poderão não ser precisos.</span><span class="sxs-lookup"><span data-stu-id="d6329-860">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="d6329-861">Isso ocorre devido à maneira como as consultas de facetamento são distribuídas entre fragmentos.</span><span class="sxs-lookup"><span data-stu-id="d6329-861">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="d6329-862">O aumento de `count` geralmente aumenta a precisão da contagem de termos, mas isso prejudica o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d6329-862">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="d6329-863">`sort` (uma das `count` para classificar em ordem *decrescente* por contagem, `-count` para classificar em ordem *crescente* por contagem, `value` para classificar em ordem *crescente* por valor ou `-value` para classificar em ordem *decrescente* por valor)</span><span class="sxs-lookup"><span data-stu-id="d6329-863">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="d6329-864">Por exemplo: `facet=category,count:3,sort:count` obtém as três principais categorias nos resultados de faceta em ordem decrescente pelo número de documentos com o nome de cada cidade.</span><span class="sxs-lookup"><span data-stu-id="d6329-864">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="d6329-865">Por exemplo, se as três principais categorias forem Orçamento, Motel e Luxo, Orçamento tiver cinco ocorrências, Motel tiver seis e Luxo tiver quatro, as classificações, em ordem, serão Motel, Orçamento, Luxo.</span><span class="sxs-lookup"><span data-stu-id="d6329-865">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="d6329-866">Por exemplo: `facet=rating,sort:-value` produz todas as classificações possíveis, em ordem decrescente por valor.</span><span class="sxs-lookup"><span data-stu-id="d6329-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="d6329-867">Por exemplo, se as classificações forem de 1 a 5, as classificações serão ordenadas como 5, 4, 3, 2, 1, independentemente de quantos documentos corresponderem a cada classificação.</span><span class="sxs-lookup"><span data-stu-id="d6329-867">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="d6329-868">`values` (valores numéricos delimitados por barras verticais ou valores `Edm.DateTimeOffset` que especificam um conjunto dinâmico de valores de entrada de faceta)</span><span class="sxs-lookup"><span data-stu-id="d6329-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="d6329-869">Por exemplo: `facet=baseRate,values:10|20` produz três classificações: uma para a taxa de base 0 até 10, mas sem incluir esse valor, uma para 10 até 20, mas sem incluir esse valor e outra para 20 ou mais.</span><span class="sxs-lookup"><span data-stu-id="d6329-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="d6329-870">Por exemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produz duas classificações: uma para hotéis reformados antes de fevereiro de 2010 e outra para hotéis reformados em ou depois de 1º de fevereiro de 2010.</span><span class="sxs-lookup"><span data-stu-id="d6329-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="d6329-871">`interval` (intervalo inteiro maior que 0 para números ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para valores de tempo de data)</span><span class="sxs-lookup"><span data-stu-id="d6329-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="d6329-872">Por exemplo: `facet=baseRate,interval:100` produz classificações com base em intervalos de taxa de base de tamanho 100.</span><span class="sxs-lookup"><span data-stu-id="d6329-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="d6329-873">Por exemplo, se as taxas de base estiverem todas entre US$ 60 e US$ 600, haverá classificações para 0-100, 100-200, 200-300, 300-400, 400-500 e 500-600.</span><span class="sxs-lookup"><span data-stu-id="d6329-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="d6329-874">Por exemplo: `facet=lastRenovationDate,interval:year` produz uma classificação para cada ano em que os hotéis foram reformados.</span><span class="sxs-lookup"><span data-stu-id="d6329-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="d6329-875">`timeoffset` ([+-]hh:mm, [+-]hhmm ou [+-]hh) `timeoffset` é opcional.</span><span class="sxs-lookup"><span data-stu-id="d6329-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="d6329-876">Ele só pode ser combinado com a opção `interval` e somente quando aplicado a um campo do tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="d6329-876">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="d6329-877">O valor especifica o deslocamento de hora em relação ao UTC para compensar ao definir limites de tempo.</span><span class="sxs-lookup"><span data-stu-id="d6329-877">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="d6329-878">Por exemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa o dia limite que inicia à 01:00:00 UTC (meia-noite no fuso horário de destino)</span><span class="sxs-lookup"><span data-stu-id="d6329-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="d6329-879">**Observação**: `count` e `sort` podem ser combinados na mesma especificação de faceta, mas não podem ser combinados a `interval` ou a `values` e `interval` e `values` não podem ser combinados juntos.</span><span class="sxs-lookup"><span data-stu-id="d6329-879">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="d6329-880">**Observação**: as facetas de intervalo de data e hora serão calculadas com base na hora UTC, caso `timeoffset` não seja especificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="d6329-881">Por exemplo: para `facet=lastRenovationDate,interval:day`, o limite de dia começa à 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="d6329-881">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6329-882">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `facets`, em vez de `facet`.</span><span class="sxs-lookup"><span data-stu-id="d6329-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="d6329-883">Além disso, especifique-o como uma matriz JSON de cadeias de caracteres em que cada cadeia é uma expressão de faceta separada.</span><span class="sxs-lookup"><span data-stu-id="d6329-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="d6329-884">`$filter=[string]` (opcional) ‒ uma expressão de pesquisa estruturada na sintaxe de OData padrão.</span><span class="sxs-lookup"><span data-stu-id="d6329-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-885">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `filter`, em vez de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="d6329-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="d6329-886">`highlight=[string]` (opcional) ‒ realça um conjunto de nomes de campo separados por vírgulas usado para realçar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="d6329-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="d6329-887">Somente campos `searchable` podem ser usados para realçar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="d6329-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="d6329-888">`highlightPreTag=[string]` (opcional, o padrão é `<em>`) ‒ uma marca de cadeia de caracteres que é anexada ao início para realçar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="d6329-888">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="d6329-889">Deve ser definida com `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="d6329-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-890">Ao chamar **Pesquisa** usando GET, caracteres reservados na URL deverão ser codificados por percentual (por exemplo, %23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="d6329-890">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d6329-891">`highlightPostTag=[string]` (opcional, o padrão é `</em>`) ‒ uma marca de cadeia de caracteres que é anexada para realçar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="d6329-891">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="d6329-892">Deve ser definida com `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="d6329-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-893">Ao chamar **Pesquisa** usando GET, caracteres reservados na URL deverão ser codificados por percentual (por exemplo, %23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="d6329-893">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d6329-894">`scoringProfile=[string]` (opcional) ‒ o nome de um perfil de pontuação para avaliar pontuações de correspondência de documentos correspondentes para classificar os resultados.</span><span class="sxs-lookup"><span data-stu-id="d6329-894">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="d6329-895">`scoringParameter=[string]` (zero ou mais) ‒ indica o valor de cada parâmetro definido em uma função de pontuação (por exemplo, `referencePointParameter`) usando o formato `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="d6329-895">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="d6329-896">Por exemplo, se o perfil de pontuação definir uma função com um parâmetro chamado "mylocation", a opção de cadeia de consulta será `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="d6329-896">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="d6329-897">O primeiro traço separa o nome da lista de valores, enquanto o segundo traço faz parte do primeiro valor (longitude, neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="d6329-897">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="d6329-898">Para parâmetros de pontuação, como as marcações de aumento que podem conter vírgulas, você pode liberar todos esses valores na lista usando aspas simples.</span><span class="sxs-lookup"><span data-stu-id="d6329-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="d6329-899">Se os próprios valores contiverem aspas simples, você poderá liberá-las ao duplicar.</span><span class="sxs-lookup"><span data-stu-id="d6329-899">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="d6329-900">Por exemplo, se você tiver um parâmetro de aumento de marcação chamado "mytag" e quiser aumentá-lo nos valores de marcação "Hello, O'Brien" e "Smith", a opção de cadeia de consulta será `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="d6329-900">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="d6329-901">Observe que as aspas são necessárias apenas para os valores que contêm vírgulas.</span><span class="sxs-lookup"><span data-stu-id="d6329-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-902">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `scoringParameters`, em vez de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="d6329-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="d6329-903">Além disso, especifique-o como uma matriz de cadeias de caracteres JSON, na qual cada cadeia é um par de nome `name-values` .</span><span class="sxs-lookup"><span data-stu-id="d6329-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="d6329-904">`minimumCoverage` (opcional, o padrão até 100)-um número entre 0 e 100, indicando a porcentagem do índice deve ser coberto por uma consulta de pesquisa, para que a consulta seja relatada como sucesso.</span><span class="sxs-lookup"><span data-stu-id="d6329-904">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="d6329-905">Por padrão, o índice inteiro deve estar disponível ou `Search` retornará o código de status HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="d6329-905">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="d6329-906">Se você definir `minimumCoverage` e `Search` for bem-sucedido, retornará HTTP 200 e incluirá um valor de `@search.coverage` na resposta indicando a porcentagem do índice que foi incluído na consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-907">Definir esse parâmetro para um valor inferior a 100 pode ser útil para garantir a disponibilidade de pesquisa até mesmo para serviços com apenas uma réplica.</span><span class="sxs-lookup"><span data-stu-id="d6329-907">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="d6329-908">No entanto, não existe a garantia de que todos os documentos correspondentes estejam presentes nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-908">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="d6329-909">Se rechamada da pesquisa é mais importante para o seu aplicativo do que a disponibilidade, é melhor deixar `minimumCoverage` em seu valor padrão de 100.</span><span class="sxs-lookup"><span data-stu-id="d6329-909">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="d6329-910">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-911">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-911">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-912">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-913">Observação: para essa operação, o `api-version` é especificado como um parâmetro de consulta na URL, independentemente de você chamar **Pesquisa** com GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-913">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="d6329-914">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-914">**Request Headers**</span></span>

<span data-ttu-id="d6329-915">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-915">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-916">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-916">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-917">É um valor de cadeia de caracteres exclusivo para a URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-917">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="d6329-918">A solicitação **Pesquisar** pode especificar uma chave de administração ou a chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d6329-918">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="d6329-919">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-919">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-920">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-920">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-921">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-921">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-922">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-922">**Request Body**</span></span>

<span data-ttu-id="d6329-923">Para GET: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="d6329-923">For GET: None.</span></span>

<span data-ttu-id="d6329-924">Para POST:</span><span class="sxs-lookup"><span data-stu-id="d6329-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="d6329-925">**Continuação de respostas de pesquisa parciais**</span><span class="sxs-lookup"><span data-stu-id="d6329-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="d6329-926">Às vezes, a pesquisa do Azure não pode retornar todos os resultados solicitados em uma única resposta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-926">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="d6329-927">Isso pode ocorrer por diferentes motivos, como quando a consulta solicita muitos documentos não especificando `$top` ou especificando um valor grande demais para `$top`.</span><span class="sxs-lookup"><span data-stu-id="d6329-927">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="d6329-928">Nesses casos, a pesquisa do Azure incluirá a anotação `@odata.nextLink` no corpo da resposta e também `@search.nextPageParameters`, se for uma solicitação POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-928">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="d6329-929">Você pode usar os valores dessas anotações para formular outra solicitação Pesquisar para obter a próxima parte da resposta da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-929">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="d6329-930">Isso é chamado de ***continuação*** da solicitação Pesquisar original e as anotações geralmente são chamadas de ***tokens de continuação***.</span><span class="sxs-lookup"><span data-stu-id="d6329-930">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="d6329-931">Consulte [o exemplo a seguir](#SearchResponse) para obter detalhes sobre a sintaxe dessas anotações e onde elas aparecem no corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="d6329-931">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="d6329-932">Os motivos pelos quais a pesquisa do Azure pode retornar os tokens de continuação são específicos de implementação e estão sujeitos a alteração.</span><span class="sxs-lookup"><span data-stu-id="d6329-932">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="d6329-933">Clientes robustos devem sempre estar prontos para lidar com casos em que são retornados menos documentos do que o esperado e um token de continuação é incluído para continuar recuperando os documentos.</span><span class="sxs-lookup"><span data-stu-id="d6329-933">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="d6329-934">Observe também que você deve usar o mesmo método HTTP que a solicitação original para continuar.</span><span class="sxs-lookup"><span data-stu-id="d6329-934">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="d6329-935">Por exemplo, se você tiver enviado uma solicitação GET, quaisquer solicitações de continuação que você enviar também deverão usar GET (e da mesma forma para POST).</span><span class="sxs-lookup"><span data-stu-id="d6329-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="d6329-936"><a name="SearchResponse"></a>
**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="d6329-937">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="d6329-938">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="d6329-938">**Examples:**</span></span>

<span data-ttu-id="d6329-939">Você pode encontrar exemplos adicionais na página [Sintaxe de expressão OData para o Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d6329-939">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="d6329-940">Pesquisar o índice classificado em ordem decrescente por data.</span><span class="sxs-lookup"><span data-stu-id="d6329-940">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="d6329-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="d6329-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="d6329-943">Em uma pesquisa facetada, pesquisar o índice e recuperar facetas para categorias, classificação, marcas, bem como itens com baseRate em intervalos específicos:</span><span class="sxs-lookup"><span data-stu-id="d6329-943">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="d6329-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="d6329-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="d6329-946">Usando um filtro, restringir os resultados de consulta facetados anteriores depois que o usuário clicar na classificação 3 e na categoria "Motel":</span><span class="sxs-lookup"><span data-stu-id="d6329-946">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="d6329-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="d6329-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="d6329-949">Em uma pesquisa facetada, definir um limite superior para termos exclusivos retornados em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="d6329-950">O padrão é 10, mas você pode aumentar ou diminuir esse valor usando o parâmetro `count` no atributo `facet`:</span><span class="sxs-lookup"><span data-stu-id="d6329-950">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="d6329-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="d6329-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="d6329-953">Pesquisar o índice em campos específicos. Por exemplo, um campo específico do idioma:</span><span class="sxs-lookup"><span data-stu-id="d6329-953">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="d6329-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="d6329-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="d6329-956">Pesquisar o índice em vários campos.</span><span class="sxs-lookup"><span data-stu-id="d6329-956">Search the Index across multiple fields.</span></span> <span data-ttu-id="d6329-957">Por exemplo, você pode armazenar e consultar campos pesquisáveis em vários idiomas, todos no mesmo índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-957">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="d6329-958">Se descrições em inglês e francês coexistirem no mesmo documento, você poderá retornar qualquer uma das descrições ou todas elas nos resultados da consulta:</span><span class="sxs-lookup"><span data-stu-id="d6329-958">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="d6329-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="d6329-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="d6329-961">Observe que você pode consultar apenas um índice por vez.</span><span class="sxs-lookup"><span data-stu-id="d6329-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="d6329-962">Não crie vários índices para cada idioma, a menos que você planeje consultar um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="d6329-962">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="d6329-963">Paginar ‒ obtenha a primeira página de itens (o tamanho de página é 10):</span><span class="sxs-lookup"><span data-stu-id="d6329-963">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="d6329-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="d6329-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="d6329-966">Paginar ‒ obtenha a segunda página de itens (o tamanho de página é 10):</span><span class="sxs-lookup"><span data-stu-id="d6329-966">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="d6329-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="d6329-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="d6329-969">Recuperar um conjunto específico de campos:</span><span class="sxs-lookup"><span data-stu-id="d6329-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="d6329-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="d6329-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="d6329-972">Recupere documentos que correspondem a uma expressão de filtro específica:</span><span class="sxs-lookup"><span data-stu-id="d6329-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="d6329-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="d6329-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="d6329-975">Pesquisar o índice e retornar fragmentos com realces de ocorrências</span><span class="sxs-lookup"><span data-stu-id="d6329-975">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="d6329-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="d6329-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="d6329-978">Pesquisar o índice e retornar documentos classificados de mais próximo a mais distante em relação a um local de referência</span><span class="sxs-lookup"><span data-stu-id="d6329-978">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="d6329-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="d6329-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="d6329-981">Pesquisar o índice, supondo que haja um perfil de pontuação chamado "geo" com duas funções de pontuação de distância, uma definindo um parâmetro chamado "currentLocation" e uma definindo um parâmetro chamado "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="d6329-981">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="d6329-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="d6329-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="d6329-984">Localizar documentos no índice usando a [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-984">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="d6329-985">Esta consulta retorna hotéis em que os campos de pesquisa contêm os termos "conforto" e "local", mas não "motel":</span><span class="sxs-lookup"><span data-stu-id="d6329-985">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="d6329-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="d6329-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="d6329-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="d6329-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="d6329-988">Observe o uso de `searchMode=all` acima.</span><span class="sxs-lookup"><span data-stu-id="d6329-988">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="d6329-989">Incluir esse parâmetro substitui o padrão de `searchMode=any`, garantindo que `-motel` significa "E NÃO" em vez de "OU NÃO".</span><span class="sxs-lookup"><span data-stu-id="d6329-989">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="d6329-990">Sem `searchMode=all`, você obtém "OU NÃO", que  expande em vez de restringir os resultados de pesquisa, e isso pode ser contraintuitivo para alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="d6329-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="d6329-991">Localizar documentos no índice usando a [sintaxe de consulta lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6329-991">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="d6329-992">Essa consulta retorna hotéis onde o campo de categoria contém o termo "orçamento" e todos os campos pesquisáveis com a frase "renovado recentemente".</span><span class="sxs-lookup"><span data-stu-id="d6329-992">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="d6329-993">Os documentos com a frase "renovado recentemente" apresentam uma classificação superior como um resultado do valor de aumento de termo (3)</span><span class="sxs-lookup"><span data-stu-id="d6329-993">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="d6329-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="d6329-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="d6329-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="d6329-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="d6329-996">Procurar documento</span><span class="sxs-lookup"><span data-stu-id="d6329-996">Lookup Document</span></span>
<span data-ttu-id="d6329-997">A operação **Pesquisar Documento** recupera um documento do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6329-997">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="d6329-998">Isso é útil quando um usuário clica em um resultado de pesquisa específico e você deseja pesquisar detalhes específicos sobre esse documento.</span><span class="sxs-lookup"><span data-stu-id="d6329-998">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="d6329-999">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-999">**Request**</span></span>

<span data-ttu-id="d6329-1000">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="d6329-1001">A solicitação **Pesquisar Documento** pode ser criada da maneira a seguir.</span><span class="sxs-lookup"><span data-stu-id="d6329-1001">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="d6329-1002">Como alternativa, você pode usar a sintaxe tradicional de OData para pesquisa de chave:</span><span class="sxs-lookup"><span data-stu-id="d6329-1002">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="d6329-1003">O URI da solicitação inclui um [nome de índice] e uma [chave], especificando qual documento deve ser recuperado do índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-1003">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="d6329-1004">Você pode obter apenas um documento por vez.</span><span class="sxs-lookup"><span data-stu-id="d6329-1004">You can only get one document at a time.</span></span> <span data-ttu-id="d6329-1005">Use **Pesquisar** para obter vários documentos em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-1005">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="d6329-1006">**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="d6329-1006">**Query Parameters**</span></span>

<span data-ttu-id="d6329-1007">`$select=[string]` (opcional) ‒ uma lista de campos separados por vírgulas a serem recuperados.</span><span class="sxs-lookup"><span data-stu-id="d6329-1007">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="d6329-1008">Se não for especificado ou se for definido como `*`, todos os campos marcados como recuperáveis no esquema serão incluídos na projeção.</span><span class="sxs-lookup"><span data-stu-id="d6329-1008">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="d6329-1009">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-1010">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1010">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-1011">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-1012">Observação: para essa operação, a `api-version` é especificada como um parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-1012">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="d6329-1013">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1013">**Request Headers**</span></span>

<span data-ttu-id="d6329-1014">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-1014">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-1015">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1015">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-1016">É um valor de cadeia de caracteres exclusivo para a URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-1016">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="d6329-1017">A solicitação **Pesquisar Documento** pode especificar uma chave de administração ou a chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1017">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="d6329-1018">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-1018">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-1019">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-1019">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-1020">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-1020">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-1021">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1021">**Request Body**</span></span>

<span data-ttu-id="d6329-1022">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="d6329-1022">None.</span></span>

<span data-ttu-id="d6329-1023">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-1023">**Response**</span></span>

<span data-ttu-id="d6329-1024">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="d6329-1025">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="d6329-1025">**Example**</span></span>

<span data-ttu-id="d6329-1026">Pesquisar o documento que tem a chave '2'</span><span class="sxs-lookup"><span data-stu-id="d6329-1026">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="d6329-1027">Pesquisar o documento que tem a chave '3' usando a sintaxe de OData:</span><span class="sxs-lookup"><span data-stu-id="d6329-1027">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="d6329-1028">Contar documentos</span><span class="sxs-lookup"><span data-stu-id="d6329-1028">Count Documents</span></span>
<span data-ttu-id="d6329-1029">A operação **Contar Documentos** recupera uma contagem do número de documentos em um índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1029">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="d6329-1030">A sintaxe de `$count` faz parte do protocolo OData.</span><span class="sxs-lookup"><span data-stu-id="d6329-1030">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="d6329-1031">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1031">**Request**</span></span>

<span data-ttu-id="d6329-1032">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="d6329-1033">A solicitação **Contar Documentos** pode ser criada usando o método GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-1033">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="d6329-1034">O [nome do índice] no URI da solicitação instrui o serviço a retornar uma contagem de todos os itens da coleção de documentos do índice especificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-1034">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="d6329-1035">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-1036">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1036">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-1037">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-1038">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1038">**Request Headers**</span></span>

<span data-ttu-id="d6329-1039">A lista a seguir descreve os cabeçalhos de solicitação obrigatórios e opcionais.</span><span class="sxs-lookup"><span data-stu-id="d6329-1039">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="d6329-1040">`Accept`: esse valor deve ser definido como `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1040">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="d6329-1041">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1041">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-1042">É um valor de cadeia de caracteres exclusivo para a URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-1042">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="d6329-1043">A solicitação **Contar Documentos** pode especificar uma chave de administração ou a chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1043">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="d6329-1044">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-1044">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-1045">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-1045">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-1046">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-1046">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-1047">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1047">**Request Body**</span></span>

<span data-ttu-id="d6329-1048">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="d6329-1048">None.</span></span>

<span data-ttu-id="d6329-1049">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-1049">**Response**</span></span>

<span data-ttu-id="d6329-1050">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="d6329-1051">O corpo da resposta contém o valor da contagem como um inteiro formatado como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="d6329-1051">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="d6329-1052">Sugestões</span><span class="sxs-lookup"><span data-stu-id="d6329-1052">Suggestions</span></span>
<span data-ttu-id="d6329-1053">A operação **Sugestões** recupera sugestões com base na entrada de pesquisa parcial.</span><span class="sxs-lookup"><span data-stu-id="d6329-1053">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="d6329-1054">Ela é normalmente usada em caixas de pesquisa para fornecer sugestões de digitação antecipada à medida que os usuários inserem termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1054">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="d6329-1055">Solicitações de sugestão têm por objetivo sugerir documentos de destino, assim, o texto sugerido poderá ser repetido se a mesma pesquisa de entrada corresponder a vários documentos candidatos.</span><span class="sxs-lookup"><span data-stu-id="d6329-1055">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="d6329-1056">Você pode usar `$select` para recuperar outros campos de documento (inclusive a chave do documento) para determinar qual documento é a fonte de cada sugestão.</span><span class="sxs-lookup"><span data-stu-id="d6329-1056">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="d6329-1057">Uma operação **Suggestions** é emitida como uma solicitação GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="d6329-1058">**Quando usar POST em vez de GET**</span><span class="sxs-lookup"><span data-stu-id="d6329-1058">**When to use POST instead of GET**</span></span>

<span data-ttu-id="d6329-1059">Quando você usar HTTP GET para chamar a API de **Sugestões** , será preciso estar ciente de que o comprimento da URL da solicitação não pode exceder 8 KB.</span><span class="sxs-lookup"><span data-stu-id="d6329-1059">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="d6329-1060">Isso costuma ser suficiente para a maioria dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d6329-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="d6329-1061">No entanto, alguns aplicativos geram consultas muito grandes, especificamente expressões de filtro OData.</span><span class="sxs-lookup"><span data-stu-id="d6329-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="d6329-1062">Para esses aplicativos, usar HTTP POST é uma opção melhor, pois permite filtros maiores que o GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="d6329-1063">Com o POST, o número de cláusulas em um filtro é o fator limitante, não o tamanho da cadeia de caracteres de filtro não processada, uma vez que o limite de tamanho da solicitação POST é quase 16 MB.</span><span class="sxs-lookup"><span data-stu-id="d6329-1063">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1064">Embora o limite de tamanho da solicitação POST seja muito grande, expressões de filtro não podem ser arbitrariamente complexos.</span><span class="sxs-lookup"><span data-stu-id="d6329-1064">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="d6329-1065">Confira [Sintaxe de expressão OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de filtro.</span><span class="sxs-lookup"><span data-stu-id="d6329-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="d6329-1066">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1066">**Request**</span></span>

<span data-ttu-id="d6329-1067">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="d6329-1068">A solicitação **Sugestões** pode ser criada usando os métodos GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-1068">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="d6329-1069">O URI da solicitação especifica o nome do índice a ser consultado.</span><span class="sxs-lookup"><span data-stu-id="d6329-1069">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="d6329-1070">Parâmetros, como o termo de pesquisa inserido parcialmente, são especificados na cadeia de consulta no caso de solicitações GET e no corpo da solicitação no caso de solicitações POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-1070">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="d6329-1071">Como prática recomendada ao criar solicitações GET, lembre-se de [codificar na URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) os parâmetros de consulta específicos ao chamar a API REST diretamente.</span><span class="sxs-lookup"><span data-stu-id="d6329-1071">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="d6329-1072">Para as operações **Sugestões** , isso inclui:</span><span class="sxs-lookup"><span data-stu-id="d6329-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="d6329-1073">A codificação de URL é recomendada apenas nos parâmetros da consulta acima.</span><span class="sxs-lookup"><span data-stu-id="d6329-1073">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="d6329-1074">Se você inadvertidamente codificar na URL a cadeia de caracteres de consulta inteira (tudo após o ?), as solicitações serão interrompidas.</span><span class="sxs-lookup"><span data-stu-id="d6329-1074">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="d6329-1075">Além disso, a codificação de URL só é necessária ao se chamar a API REST diretamente usando GET.</span><span class="sxs-lookup"><span data-stu-id="d6329-1075">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="d6329-1076">Nenhuma codificação de URL é necessária ao chamar **Sugestões** usando POST, ou ao usar a [biblioteca de clientes .NET](https://msdn.microsoft.com/library/dn951165.aspx), que processa a codificação de URL para você.</span><span class="sxs-lookup"><span data-stu-id="d6329-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="d6329-1077">**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="d6329-1077">**Query Parameters**</span></span>

<span data-ttu-id="d6329-1078">**Suggestions** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="d6329-1079">Você fornece esses parâmetros na cadeia de consulta da URL ao chamar **Suggestions** via GET e como propriedades JSON no corpo da solicitação ao chamar **Sugestões** via POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-1079">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="d6329-1080">A sintaxe para alguns parâmetros é ligeiramente diferente entre GET e POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-1080">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="d6329-1081">Essas diferenças são indicadas, como aplicável, abaixo:</span><span class="sxs-lookup"><span data-stu-id="d6329-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="d6329-1082">`search=[string]` ‒ o texto de pesquisa a ser usado para sugerir consultas.</span><span class="sxs-lookup"><span data-stu-id="d6329-1082">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="d6329-1083">Deve ter pelo menos 1 e não mais que 100 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6329-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="d6329-1084">`highlightPreTag=[string]` (opcional) ‒ uma cadeia de caracteres de marca que é anexada no início para pesquisar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="d6329-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="d6329-1085">Deve ser definida com `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1086">Ao chamar **Sugestões** usando GET, os caracteres reservados na URL deverão ser codificados por percentual (por exemplo, %23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="d6329-1086">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d6329-1087">`highlightPostTag=[string]` (opcional) ‒ uma cadeia de caracteres de marca que é anexada para pesquisar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="d6329-1087">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="d6329-1088">Deve ser definida com `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1089">Ao chamar **Sugestões** usando GET, os caracteres reservados na URL deverão ser codificados por percentual (por exemplo, %23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="d6329-1089">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="d6329-1090">`suggesterName=[string]` ‒ o nome do sugestor conforme especificado na coleção `suggesters` que faz parte da definição do índice.</span><span class="sxs-lookup"><span data-stu-id="d6329-1090">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="d6329-1091">Um `suggester` determina quais campos são examinados em busca de termos de consulta sugeridos.</span><span class="sxs-lookup"><span data-stu-id="d6329-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="d6329-1092">Consulte [Sugestores](#Suggesters) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d6329-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="d6329-1093">`fuzzy=[boolean]` (opcional, padrão = falso) ‒ quando definido como verdadeiro, essa API encontrará sugestões mesmo que haja um caractere ausente ou substituído no texto de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1093">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="d6329-1094">Embora isso proporcione uma experiência melhor em alguns cenários, prejudica o desempenho, pois pesquisas com sugestões difusas são mais lentas e consumem mais recursos.</span><span class="sxs-lookup"><span data-stu-id="d6329-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="d6329-1095">`searchFields=[string]` (opcional) ‒ a lista de nomes de campos separados por vírgulas para pesquisar o texto de pesquisa especificado.</span><span class="sxs-lookup"><span data-stu-id="d6329-1095">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="d6329-1096">Os campos de destino devem ser habilitados para sugestões.</span><span class="sxs-lookup"><span data-stu-id="d6329-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="d6329-1097">`$top=#` (opcional, padrão = 5) ‒ o número de sugestões a serem recuperadas.</span><span class="sxs-lookup"><span data-stu-id="d6329-1097">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="d6329-1098">Deve ser um número entre 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="d6329-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1099">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `top` em vez de `$top`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="d6329-1100">`$filter=[string]` (opcional) par uma expressão que filtra os documentos considerados para sugestões.</span><span class="sxs-lookup"><span data-stu-id="d6329-1100">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1101">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `filter` em vez de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="d6329-1102">`$orderby=[string]` (opcional) ‒ uma lista de expressões separadas por vírgulas para classificar os resultados.</span><span class="sxs-lookup"><span data-stu-id="d6329-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="d6329-1103">Cada expressão pode ser um nome de campo ou uma chamada para a função `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="d6329-1103">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="d6329-1104">Cada expressão pode ser seguida de `asc` para indicar a ordem crescente e `desc` para indicar a ordem decrescente.</span><span class="sxs-lookup"><span data-stu-id="d6329-1104">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="d6329-1105">O padrão é a ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="d6329-1105">The default is ascending order.</span></span> <span data-ttu-id="d6329-1106">Há um limite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1107">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `orderby` em vez de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="d6329-1108">`$select=[string]` (opcional) ‒ uma lista de campos separados por vírgulas a serem recuperados.</span><span class="sxs-lookup"><span data-stu-id="d6329-1108">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="d6329-1109">Se não for especificado, somente a chave do documento e o texto de sugestão serão retornados.</span><span class="sxs-lookup"><span data-stu-id="d6329-1109">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="d6329-1110">Você pode solicitar explicitamente todos os campos ao definir esse parâmetro para `*`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1110">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1111">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `select` em vez de `$select`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="d6329-1112">`minimumCoverage` (opcional, o padrão é 80) - um número entre 0 e 100 que indica a porcentagem do índice que deve ser coberto por uma consulta de sugestões para que a consulta a seja relatada como sucesso.</span><span class="sxs-lookup"><span data-stu-id="d6329-1112">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="d6329-1113">Por padrão, pelo menos 80% do índice deve estar disponível ou `Suggest` retornará o código de status HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="d6329-1113">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="d6329-1114">Se você definir `minimumCoverage` e `Suggest` for bem-sucedido, retornará HTTP 200 e incluirá um valor de `@search.coverage` na resposta indicando a porcentagem do índice que foi incluído na consulta.</span><span class="sxs-lookup"><span data-stu-id="d6329-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="d6329-1115">Definir esse parâmetro para um valor inferior a 100 pode ser útil para garantir a disponibilidade de pesquisa até mesmo para serviços com apenas uma réplica.</span><span class="sxs-lookup"><span data-stu-id="d6329-1115">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="d6329-1116">No entanto, não há garantias de que todas as sugestões de correspondência estejam presentes nos resultados.</span><span class="sxs-lookup"><span data-stu-id="d6329-1116">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="d6329-1117">Se a rechamada for mais importante para seu aplicativo do que a disponibilidade, é melhor não diminuir `minimumCoverage` para abaixo de seu valor padrão de 80.</span><span class="sxs-lookup"><span data-stu-id="d6329-1117">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="d6329-1118">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="d6329-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="d6329-1119">A versão de visualização é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1119">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="d6329-1120">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="d6329-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="d6329-1121">Observação: para essa operação, o `api-version` é especificado como um parâmetro de consulta na URL, independentemente de você chamar **Suggestions** com GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="d6329-1121">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="d6329-1122">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1122">**Request Headers**</span></span>

<span data-ttu-id="d6329-1123">A lista a seguir descreve os cabeçalhos de solicitação necessários e opcionais</span><span class="sxs-lookup"><span data-stu-id="d6329-1123">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="d6329-1124">`api-key`: a `api-key` é usada para autenticar a solicitação para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6329-1124">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="d6329-1125">É um valor de cadeia de caracteres exclusivo para a URL do serviço.</span><span class="sxs-lookup"><span data-stu-id="d6329-1125">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="d6329-1126">A solicitação **Suggestions** pode especificar uma chave de administração ou a chave de consulta como a `api-key`.</span><span class="sxs-lookup"><span data-stu-id="d6329-1126">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="d6329-1127">Você também precisará do nome de serviço para criar a URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6329-1127">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="d6329-1128">Você pode obter o nome do serviço e a `api-key` por meio do painel de serviço no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6329-1128">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="d6329-1129">Consulte [Criar um serviço Azure Search no portal](search-create-service-portal.md) para obter ajuda sobre a navegação na página.</span><span class="sxs-lookup"><span data-stu-id="d6329-1129">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="d6329-1130">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="d6329-1130">**Request Body**</span></span>

<span data-ttu-id="d6329-1131">Para GET: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="d6329-1131">For GET: None.</span></span>

<span data-ttu-id="d6329-1132">Para POST:</span><span class="sxs-lookup"><span data-stu-id="d6329-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="d6329-1133">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="d6329-1133">**Response**</span></span>

<span data-ttu-id="d6329-1134">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d6329-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="d6329-1135">Se a opção de projeção for usada para recuperar campos, eles serão incluídos em cada elemento da matriz:</span><span class="sxs-lookup"><span data-stu-id="d6329-1135">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="d6329-1136">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="d6329-1136">**Example**</span></span>

<span data-ttu-id="d6329-1137">Recuperar cinco sugestões, em que a entrada de pesquisa parcial é 'lux'</span><span class="sxs-lookup"><span data-stu-id="d6329-1137">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
