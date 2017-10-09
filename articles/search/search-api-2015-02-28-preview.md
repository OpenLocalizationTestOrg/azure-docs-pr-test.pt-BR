---
title: "aaaAzure pesquisa serviço REST API Versão 2015-02-28-visualização | Microsoft Docs"
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
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="9b031-103">API REST do serviço Azure Search: Versão 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="9b031-104">Este artigo é uma documentação de referência Olá para `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-105">Essa visualização estende a versão disponível atual de hello, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornecendo Olá recursos experimentais a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b031-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="9b031-106">`moreLikeThis`consulta parâmetro hello [procurar documentos](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="9b031-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="9b031-107">Encontrar outros documentos que são documentos específicos tooanother relevantes.</span><span class="sxs-lookup"><span data-stu-id="9b031-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="9b031-108">Algumas partes adicionais de saudação `2015-02-28-Preview` API REST estão documentados separadamente.</span><span class="sxs-lookup"><span data-stu-id="9b031-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="9b031-109">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="9b031-109">These include:</span></span>

* [<span data-ttu-id="9b031-110">Perfis de pontuação</span><span class="sxs-lookup"><span data-stu-id="9b031-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="9b031-111">Indexadores</span><span class="sxs-lookup"><span data-stu-id="9b031-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="9b031-112">O serviço Azure Search está disponível em várias versões.</span><span class="sxs-lookup"><span data-stu-id="9b031-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="9b031-113">Consulte também[controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="9b031-114">APIs neste documento</span><span class="sxs-lookup"><span data-stu-id="9b031-114">APIs in this document</span></span>
<span data-ttu-id="9b031-115">A API do serviço Pesquisa do Azure dá suporte a duas sintaxes de URL para operações de API: simples e OData (consulte [Suporte a OData (API da Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="9b031-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="9b031-116">Olá lista a seguir mostra a saudação simples sintaxe.</span><span class="sxs-lookup"><span data-stu-id="9b031-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="9b031-117">Criar o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-118">Atualizar o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-119">Obter o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-120">Listando índices</span><span class="sxs-lookup"><span data-stu-id="9b031-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-121">Obter estatísticas de índice</span><span class="sxs-lookup"><span data-stu-id="9b031-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-122">Analisador de teste</span><span class="sxs-lookup"><span data-stu-id="9b031-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-123">Excluir um índice</span><span class="sxs-lookup"><span data-stu-id="9b031-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-124">Adicionar, excluir e atualizar dados em um índice</span><span class="sxs-lookup"><span data-stu-id="9b031-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-125">Pesquisar documentos</span><span class="sxs-lookup"><span data-stu-id="9b031-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-126">Procurar documento</span><span class="sxs-lookup"><span data-stu-id="9b031-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="9b031-127">Contar documentos</span><span class="sxs-lookup"><span data-stu-id="9b031-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="9b031-128">Sugestões</span><span class="sxs-lookup"><span data-stu-id="9b031-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="9b031-129">Operações de índice</span><span class="sxs-lookup"><span data-stu-id="9b031-129">Index Operations</span></span>
<span data-ttu-id="9b031-130">Você pode criar e gerenciar índices no serviço Azure Search por meio de solicitações HTTP simples (POST, GET, PUT, DELETE) em relação a um recurso de índice específico.</span><span class="sxs-lookup"><span data-stu-id="9b031-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="9b031-131">toocreate um índice, você primeiro lançar um documento JSON que descreve o esquema de índice hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="9b031-132">esquema de saudação define campos de saudação do índice hello, seus tipos de dados e como eles podem ser usados (por exemplo, em pesquisas de texto completo, filtros, classificação ou facetas).</span><span class="sxs-lookup"><span data-stu-id="9b031-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="9b031-133">Ele também define os perfis de pontuação, sugestões e outros comportamentos de saudação do tooconfigure de atributos de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="9b031-134">Olá, exemplo a seguir fornece uma ilustração de um esquema usado para pesquisar informações de hotel com campo de descrição de saudação definido em dois idiomas.</span><span class="sxs-lookup"><span data-stu-id="9b031-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="9b031-135">Observe como atributos controlam como o campo de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="9b031-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="9b031-136">Por exemplo hello `hotelId` é usada como chave de documento hello (`"key": true`) e é excluído do pesquisas de texto completo (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="9b031-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="9b031-137">Após a criação de índice hello, você vai carregar documentos que preenchem o índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="9b031-138">Consulte [Adicionar ou Atualizar Documentos](#AddOrUpdateDocuments) para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="9b031-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="9b031-139">Para um tooindexing de vídeo de Introdução na pesquisa do Azure, consulte Olá [episódio de cobertura de nuvem do Channel 9 na pesquisa do Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="9b031-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="9b031-140">Criar o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-140">Create Index</span></span>
<span data-ttu-id="9b031-141">Um índice é o meio principal de saudação de organizar e pesquisar documentos na pesquisa do Azure, semelhante toohow uma tabela organiza registros em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9b031-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="9b031-142">Cada índice tem uma coleção de documentos que todos estejam de acordo com o esquema de índice toohello (nomes de campo, tipos de dados e propriedades), mas índices também especificam outras construções (sugestões, perfis de pontuação e opções de CORS) que definem outros comportamentos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="9b031-143">Você pode criar um novo índice em um serviço Azure Search usando uma solicitação HTTP POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="9b031-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="9b031-144">corpo de saudação da solicitação de saudação é um esquema JSON que especifica as informações de configuração e de índice hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9b031-145">Como alternativa, você pode usar PUT e especificar o nome do índice Olá em Olá URI.</span><span class="sxs-lookup"><span data-stu-id="9b031-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="9b031-146">Se o índice de saudação não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="9b031-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="9b031-147">Criando um índice determina a estrutura Olá Olá documentos armazenados e usados em operações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="9b031-148">Índice de saudação popular é uma operação separada.</span><span class="sxs-lookup"><span data-stu-id="9b031-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="9b031-149">Nessa etapa, você pode usar um [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponível para fontes de dados com suporte) ou uma operação [Adicionar, Atualizar ou Excluir Documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="9b031-150">índice de saudação invertida é gerado quando Olá documentos são publicados.</span><span class="sxs-lookup"><span data-stu-id="9b031-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="9b031-151">**Observação**: número máximo de saudação de índices permitidos varia por tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="9b031-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="9b031-152">serviço gratuito Olá permite que até too3 índices.</span><span class="sxs-lookup"><span data-stu-id="9b031-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="9b031-153">O serviço padrão permite 50 índices por serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="9b031-154">Consulte [Limites e restrições](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="9b031-155">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-155">**Request**</span></span>

<span data-ttu-id="9b031-156">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9b031-157">Olá **Create Index** solicitação pode ser criada usando um método POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="9b031-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="9b031-158">Ao usar POST, você deve fornecer um nome de índice no corpo da solicitação de saudação junto com a definição de esquema de índice hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="9b031-159">Com PUT, o nome do índice Olá é parte da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="9b031-160">Se o índice Olá não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="9b031-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="9b031-161">Se já existir, é atualizado toohello nova definição.</span><span class="sxs-lookup"><span data-stu-id="9b031-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="9b031-162">nome do índice Olá deve estar em letras minúsculas, começar com uma letra ou número, não ter barras ou pontos e ter menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9b031-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="9b031-163">Depois de iniciar o nome do índice Olá com uma letra ou número, restante de saudação do nome hello pode incluir qualquer letra, número e traços, como Olá traços não sejam consecutivos.</span><span class="sxs-lookup"><span data-stu-id="9b031-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="9b031-164">Olá `api-version` é necessária.</span><span class="sxs-lookup"><span data-stu-id="9b031-164">hello `api-version` is required.</span></span> <span data-ttu-id="9b031-165">Consulte [Controle de Versão de Serviço de Pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter uma lista das versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9b031-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="9b031-166">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-166">**Request Headers**</span></span>

<span data-ttu-id="9b031-167">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-168">`Content-Type`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-168">`Content-Type`: Required.</span></span> <span data-ttu-id="9b031-169">Defina esta opção muito`application/json`</span><span class="sxs-lookup"><span data-stu-id="9b031-169">Set this too`application/json`</span></span>
* <span data-ttu-id="9b031-170">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-170">`api-key`: Required.</span></span> <span data-ttu-id="9b031-171">Olá `api-key` é usado para</span><span class="sxs-lookup"><span data-stu-id="9b031-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="9b031-172">autenticar o serviço de pesquisa do hello solicitação tooyour.</span><span class="sxs-lookup"><span data-stu-id="9b031-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-173">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-174">Olá **Create Index** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-175">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-176">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-177">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-178"><a name="RequestData"></a>
**Sintaxe do Corpo da Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="9b031-179">corpo de saudação da solicitação Olá contém uma definição de esquema, que inclui Olá lista de campos de dados em documentos que serão inseridos nesse índice, atributos, tipos de dados, bem como uma lista opcional de perfis de pontuação é usado tooscore correspondência documentos em tempo de consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="9b031-180">Observe que, para uma solicitação POST, você deve especificar o nome do índice Olá no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="9b031-181">Pode haver apenas um campo de chave no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="9b031-182">Ele tem toobe um campo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9b031-182">It has toobe a string field.</span></span> <span data-ttu-id="9b031-183">Este campo representa o identificador exclusivo de saudação para cada documento armazenado no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="9b031-184">partes principais de saudação de um índice incluem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9b031-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="9b031-185">`fields` que serão inseridos nesse índice, incluindo nome, tipo de dados e propriedades que definem as ações permitidas nesse campo.</span><span class="sxs-lookup"><span data-stu-id="9b031-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="9b031-186">`suggesters` usados para consultas de preenchimento automático ou digitação antecipada.</span><span class="sxs-lookup"><span data-stu-id="9b031-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="9b031-187">`scoringProfiles` usados para classificação de pontuação de pesquisa personalizada.</span><span class="sxs-lookup"><span data-stu-id="9b031-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="9b031-188">Consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="9b031-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` usado toodefine como documentos/consultas são divididas em tokens indexáveis pesquisável.</span><span class="sxs-lookup"><span data-stu-id="9b031-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="9b031-190">Confira [Análise na Pesquisa do Azure](https://aka.ms//azsanalysis) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="9b031-191">`defaultScoringProfile`usado o padrão de saudação toooverwrite comportamentos de pontuação.</span><span class="sxs-lookup"><span data-stu-id="9b031-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="9b031-192">`corsOptions`consultas entre origens de tooallow em seu índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="9b031-193">sintaxe de saudação para estruturar a carga de solicitação de saudação é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="9b031-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="9b031-194">Uma solicitação de exemplo é fornecida mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="9b031-194">A sample request is provided further on in this topic.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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

<span data-ttu-id="9b031-195">**Atributos de índice**</span><span class="sxs-lookup"><span data-stu-id="9b031-195">**Index Attributes**</span></span>

<span data-ttu-id="9b031-196">Olá seguintes atributos podem ser definidos ao criar um índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="9b031-197">Para obter detalhes sobre pontuação e perfis de pontuação, consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="9b031-198">`name`-Conjuntos de Olá nome do campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="9b031-199">`type`-Conjuntos de Olá tipo de dados para o campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="9b031-200">`searchable`-Marca Olá campo como texto completo pode ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="9b031-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="9b031-201">Isso significa que ele será submetido a análise, como separação de palavras, durante a indexação.</span><span class="sxs-lookup"><span data-stu-id="9b031-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="9b031-202">Se você definir um `searchable` campo tooa valor como "dia ensolarado", internamente ele será dividido em tokens individuais hello "Ensolarado" e "dia".</span><span class="sxs-lookup"><span data-stu-id="9b031-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="9b031-203">Isso habilita pesquisas de texto completo para esses termos.</span><span class="sxs-lookup"><span data-stu-id="9b031-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="9b031-204">Os campos dos tipos `Edm.String` ou `Collection(Edm.String)` são `searchable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b031-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="9b031-205">Campos de outros tipos não podem ser `searchable`.</span><span class="sxs-lookup"><span data-stu-id="9b031-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="9b031-206">**Observação**: `searchable` campos consomem espaço extra no índice, desde que a pesquisa do Azure armazenará uma versão com token adicional do valor do campo Olá para pesquisas de texto completo.</span><span class="sxs-lookup"><span data-stu-id="9b031-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="9b031-207">Se você quiser toosave espaço no seu índice e não é necessário um toobe campo incluído nas pesquisas, defina `searchable` muito`false`.</span><span class="sxs-lookup"><span data-stu-id="9b031-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="9b031-208">`filterable`-Permite Olá campo toobe referenciado em `$filter` consultas.</span><span class="sxs-lookup"><span data-stu-id="9b031-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="9b031-209">`filterable` difere de `searchable` da maneira como cadeias de caracteres são tratadas.</span><span class="sxs-lookup"><span data-stu-id="9b031-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="9b031-210">Campos dos tipos `Edm.String` ou `Collection(Edm.String)` que são `filterable` não são submetidos à quebra de palavras. Portanto, as comparações são apenas para correspondências exatas.</span><span class="sxs-lookup"><span data-stu-id="9b031-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="9b031-211">Por exemplo, se você definir um campo `f` muito "dia ensolarado", `$filter=f eq 'sunny'` encontrará nenhuma correspondência, mas `$filter=f eq 'sunny day'` será.</span><span class="sxs-lookup"><span data-stu-id="9b031-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="9b031-212">Todos os campos são `filterable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b031-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="9b031-213">`sortable`-Por padrão Olá sistema classifica os resultados pela pontuação, mas em muitas experiências os usuários desejarão toosort por campos nos documentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="9b031-214">Campos do tipo `Collection(Edm.String)` não podem ser `sortable`.</span><span class="sxs-lookup"><span data-stu-id="9b031-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="9b031-215">Todos os outros campos são `sortable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b031-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="9b031-216">`facetable`‒ geralmente usado em uma apresentação dos resultados de pesquisa que inclui a contagem de ocorrências por categoria (por exemplo, pesquisar câmeras digitais e ver as ocorrências por marca, por megapixels, por preço etc.).</span><span class="sxs-lookup"><span data-stu-id="9b031-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="9b031-217">Essa opção não pode ser usada com campos do tipo `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="9b031-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="9b031-218">Todos os outros campos são `facetable` por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b031-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="9b031-219">**Observação**: campos do tipo `Edm.String` que são `filterable`, `sortable` ou `facetable` podem ter no máximo 32 KB de comprimento.</span><span class="sxs-lookup"><span data-stu-id="9b031-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="9b031-220">Isso ocorre porque esses campos são tratados como um termo de pesquisa único e o comprimento máximo de saudação de um termo na pesquisa do Azure é de 32KB.</span><span class="sxs-lookup"><span data-stu-id="9b031-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="9b031-221">Se você precisar toostore mais texto que isso em um campo de cadeia de caracteres único, você precisará tooexplicitly definir `filterable`, `sortable`, e `facetable` muito`false` na definição do índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="9b031-222">**Observação**: se um campo não tiver nenhum Olá acima atributos definidos muito`true` (`searchable`, `filterable`, `sortable`, ou`facetable`) campo Olá será excluído efetivamente do índice Olá invertido.</span><span class="sxs-lookup"><span data-stu-id="9b031-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="9b031-223">Essa opção é útil para campos que não são usados em consultas, mas são necessários em resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="9b031-224">Excluir esses campos do índice Olá melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="9b031-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="9b031-225">`key`-As marcas Olá campo como contendo identificadores exclusivos para documentos no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="9b031-226">Exatamente um campo deve ser escolhido como Olá `key` campo e ele devem ser do tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="9b031-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="9b031-227">Campos de chave podem ser usado toolook documentos diretamente por meio de saudação [API de pesquisa](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="9b031-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="9b031-228">`retrievable`-Define se o campo Olá pode ser retornado em um resultado de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="9b031-229">Isso é útil quando você deseja toouse um campo (por exemplo, margem) como um filtro, classificação ou mecanismo de pontuação, mas não deseja usuário final do hello campo toobe toohello visível.</span><span class="sxs-lookup"><span data-stu-id="9b031-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="9b031-230">Esse atributo deve ser `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="9b031-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="9b031-231">`analyzer`-Define Olá nome da saudação analisador toouse Olá campo em tempo de pesquisa e indexação de hora.</span><span class="sxs-lookup"><span data-stu-id="9b031-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="9b031-232">Para Olá conjunto de valores permitido consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="9b031-233">Essa opção pode ser usada apenas com campos `searchable`, e não pode ser definida com `searchAnalyzer` ou `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="9b031-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="9b031-234">Depois que o analisador de saudação for escolhido, não pode ser alterado para o campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="9b031-235">`searchAnalyzer`-Conjuntos de Olá nome do analisador Olá usado em tempo de pesquisa para o campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="9b031-236">Para Olá conjunto de valores permitido consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="9b031-237">Essa opção só pode ser usada com campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="9b031-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="9b031-238">Ele deve ser definido em conjunto com `indexAnalyzer` e não pode ser definida com hello `analyzer` opção.</span><span class="sxs-lookup"><span data-stu-id="9b031-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="9b031-239">Esse analisador pode ser atualizado em um campo existente.</span><span class="sxs-lookup"><span data-stu-id="9b031-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="9b031-240">`indexAnalyzer`-Conjuntos de Olá nome do analisador de saudação usada no momento da indexação para o campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="9b031-241">Para Olá conjunto de valores permitido consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="9b031-242">Essa opção só pode ser usada com campos `searchable` .</span><span class="sxs-lookup"><span data-stu-id="9b031-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="9b031-243">Ele deve ser definido em conjunto com `searchAnalyzer` e não pode ser definida com hello `analyzer` opção.</span><span class="sxs-lookup"><span data-stu-id="9b031-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="9b031-244">Depois que o analisador de saudação for escolhido, não pode ser alterado para o campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="9b031-245">`suggesters`-Conjuntos de Olá modo de pesquisa e campos de origem de saudação do conteúdo de saudação para obter sugestões.</span><span class="sxs-lookup"><span data-stu-id="9b031-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="9b031-246">Consulte [Sugestores](#Suggesters) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="9b031-247">`scoringProfiles` ‒ define comportamentos de pontuação personalizados que permitem influenciam quais itens aparecem em posição mais elevada nos resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="9b031-248">Perfis de pontuação são compostos de funções e pesos de campos.</span><span class="sxs-lookup"><span data-stu-id="9b031-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="9b031-249">Consulte [adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações sobre atributos de saudação usados em um perfil de pontuação.</span><span class="sxs-lookup"><span data-stu-id="9b031-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="9b031-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Suporte ao idioma**</span><span class="sxs-lookup"><span data-stu-id="9b031-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="9b031-251">Os campos pesquisáveis são submetidos a análise que, frequentemente, envolve quebra de palavras, normalização do texto e filtragem de termos.</span><span class="sxs-lookup"><span data-stu-id="9b031-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="9b031-252">Por padrão, os campos de pesquisa na pesquisa do Azure são analisados com hello [analisador padrão do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que quebra o texto em elementos seguindo o["Segmentação de texto Unicode"](http://unicode.org/reports/tr29/) regras.</span><span class="sxs-lookup"><span data-stu-id="9b031-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="9b031-253">Além disso, analisador padrão Olá converte a forma de letras minúsculas do todos os caracteres tootheir.</span><span class="sxs-lookup"><span data-stu-id="9b031-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="9b031-254">Os documentos indexados e termos de pesquisa percorrer analysis Olá durante a indexação e processamento de consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="9b031-255">A Pesquisa do Azure oferece suporte a vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="9b031-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="9b031-256">Cada um desses idiomas requer um analisador de texto não padrão que leva em consideração as características de determinado idioma.</span><span class="sxs-lookup"><span data-stu-id="9b031-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="9b031-257">O Azure Search oferece dois tipos de analisadores:</span><span class="sxs-lookup"><span data-stu-id="9b031-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="9b031-258">35 analisadores ativados pela Lucene.</span><span class="sxs-lookup"><span data-stu-id="9b031-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="9b031-259">50 analisadores apoiados pela tecnologia de processamento de idioma natural proprietária da Microsoft usada no Office e no Bing.</span><span class="sxs-lookup"><span data-stu-id="9b031-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="9b031-260">Alguns desenvolvedores talvez prefira Olá solução mais familiar, simple de código-fonte aberto do Lucene.</span><span class="sxs-lookup"><span data-stu-id="9b031-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="9b031-261">Analisadores Lucene são mais rápidas, mas analisadores de Microsoft hello têm recursos avançados, como lematização, decompounding (nos idiomas alemão, dinamarquês, holandês, sueco, norueguês, estoniano, concluir, húngaro, Eslovaco) e reconhecimento de entidade (URLs de palavras emails, datas, números).</span><span class="sxs-lookup"><span data-stu-id="9b031-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="9b031-262">Se possível, você deve executar comparações de ambos os Olá Lucene e Microsoft analisadores toodecide qual é a melhor opção.</span><span class="sxs-lookup"><span data-stu-id="9b031-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="9b031-263">***Veja a comparação***</span><span class="sxs-lookup"><span data-stu-id="9b031-263">***How they compare***</span></span>

<span data-ttu-id="9b031-264">Analisador do Lucene Olá para inglês estende o analisador padrão hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="9b031-265">Ele remove possessivos (apóstrofos à direita) de palavras, aplica a lematização conforme o [algoritmo de lematização de Porter](http://tartarus.org/~martin/PorterStemmer/) e remove as [palavras irrelevantes](http://en.wikipedia.org/wiki/Stop_words) do inglês.</span><span class="sxs-lookup"><span data-stu-id="9b031-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="9b031-266">Em comparação, o analisador do Microsoft hello executa lematização em vez de lematização.</span><span class="sxs-lookup"><span data-stu-id="9b031-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="9b031-267">Isso significa que ele pode tratar muito melhor as formas irregulares e inflexivas de palavras, o que gera resultados da pesquisa mais relevantes (observe o módulo 7 da [Apresentação MVA da Pesquisa do Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obter mais detalhes).</span><span class="sxs-lookup"><span data-stu-id="9b031-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="9b031-268">A indexação com analisadores da Microsoft em média é duas vezes toothree mais lentos que seus equivalentes do Lucene, dependendo da linguagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="9b031-269">O desempenho da pesquisa não dever significativamente afetado para consultas de tamanho médio.</span><span class="sxs-lookup"><span data-stu-id="9b031-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="9b031-270">***Configuração***</span><span class="sxs-lookup"><span data-stu-id="9b031-270">***Configuration***</span></span>

<span data-ttu-id="9b031-271">Para cada campo na definição de índice hello, você pode definir Olá `analyzer` nome da propriedade tooan analisador que especifica o idioma e o fornecedor.</span><span class="sxs-lookup"><span data-stu-id="9b031-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="9b031-272">Olá analisador mesmo será aplicada quando a indexação e pesquisa para esse campo.</span><span class="sxs-lookup"><span data-stu-id="9b031-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="9b031-273">Por exemplo, você pode ter campos separados para descrições de hotel em inglês, francês e espanhol que existem lado a lado no hello mesmo índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="9b031-274">Saudação de uso [parâmetro de consulta 'searchFields'](#SearchQueryParameters) toospecify que toosearch campo específico do idioma contra em suas consultas.</span><span class="sxs-lookup"><span data-stu-id="9b031-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="9b031-275">Você pode examinar os exemplos de consultas que incluem hello `analyzer` propriedade [procurar documentos](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="9b031-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="9b031-276">***Lista de analisadores***</span><span class="sxs-lookup"><span data-stu-id="9b031-276">***Analyzer list***</span></span>

<span data-ttu-id="9b031-277">Abaixo está a lista de saudação de idiomas com suporte, juntamente com os nomes de analisador Lucene e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9b031-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="9b031-278">idioma</span><span class="sxs-lookup"><span data-stu-id="9b031-278">Language</span></span></th>
        <th><span data-ttu-id="9b031-279">Nome do analisador da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="9b031-280">Nome do analisador da Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-281">Árabe</span><span class="sxs-lookup"><span data-stu-id="9b031-281">Arabic</span></span></td>
        <td><span data-ttu-id="9b031-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-284">Armênia</span><span class="sxs-lookup"><span data-stu-id="9b031-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="9b031-285">hy.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="9b031-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="9b031-286">Bangla</span></span></td>
        <td><span data-ttu-id="9b031-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="9b031-288">Basco</span><span class="sxs-lookup"><span data-stu-id="9b031-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="9b031-289">Eu.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="9b031-290">Búlgaro</span><span class="sxs-lookup"><span data-stu-id="9b031-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="9b031-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-292">BG.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="9b031-293">Catalão</span><span class="sxs-lookup"><span data-stu-id="9b031-293">Catalan</span></span></td>
        <td><span data-ttu-id="9b031-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-295">CA.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="9b031-296">Chinês (simplificado)</span><span class="sxs-lookup"><span data-stu-id="9b031-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="9b031-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-299">Chinês (tradicional)</span><span class="sxs-lookup"><span data-stu-id="9b031-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="9b031-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="9b031-302">Croata</span><span class="sxs-lookup"><span data-stu-id="9b031-302">Croatian</span></span></td>
        <td><span data-ttu-id="9b031-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-304">Tcheco</span><span class="sxs-lookup"><span data-stu-id="9b031-304">Czech</span></span></td>
        <td><span data-ttu-id="9b031-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="9b031-307">Dinamarquês</span><span class="sxs-lookup"><span data-stu-id="9b031-307">Danish</span></span></td>
        <td><span data-ttu-id="9b031-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="9b031-310">Holandês</span><span class="sxs-lookup"><span data-stu-id="9b031-310">Dutch</span></span></td>
        <td><span data-ttu-id="9b031-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="9b031-313">Inglês</span><span class="sxs-lookup"><span data-stu-id="9b031-313">English</span></span></td>        
        <td><span data-ttu-id="9b031-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-316">Estoniano</span><span class="sxs-lookup"><span data-stu-id="9b031-316">Estonian</span></span></td>
        <td><span data-ttu-id="9b031-317">et.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-318">Finlandês</span><span class="sxs-lookup"><span data-stu-id="9b031-318">Finnish</span></span></td>
        <td><span data-ttu-id="9b031-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="9b031-321">Francês</span><span class="sxs-lookup"><span data-stu-id="9b031-321">French</span></span></td>
        <td><span data-ttu-id="9b031-322">fr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-324">Galego</span><span class="sxs-lookup"><span data-stu-id="9b031-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="9b031-325">GL.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="9b031-326">Alemão</span><span class="sxs-lookup"><span data-stu-id="9b031-326">German</span></span></td>
        <td><span data-ttu-id="9b031-327">de.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-329">Grego</span><span class="sxs-lookup"><span data-stu-id="9b031-329">Greek</span></span></td>
        <td><span data-ttu-id="9b031-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-332">Guzerate</span><span class="sxs-lookup"><span data-stu-id="9b031-332">Gujarati</span></span></td>
        <td><span data-ttu-id="9b031-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-334">Hebraico</span><span class="sxs-lookup"><span data-stu-id="9b031-334">Hebrew</span></span></td>
        <td><span data-ttu-id="9b031-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-336">Híndi</span><span class="sxs-lookup"><span data-stu-id="9b031-336">Hindi</span></span></td>
        <td><span data-ttu-id="9b031-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-339">Húngaro</span><span class="sxs-lookup"><span data-stu-id="9b031-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="9b031-340">hu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-342">Islandês</span><span class="sxs-lookup"><span data-stu-id="9b031-342">Icelandic</span></span></td>
        <td><span data-ttu-id="9b031-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-344">Indonésio (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="9b031-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="9b031-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-347">Irlandês</span><span class="sxs-lookup"><span data-stu-id="9b031-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="9b031-348">GA.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-349">Italiano</span><span class="sxs-lookup"><span data-stu-id="9b031-349">Italian</span></span></td>
        <td><span data-ttu-id="9b031-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-352">Japonês</span><span class="sxs-lookup"><span data-stu-id="9b031-352">Japanese</span></span></td>
        <td><span data-ttu-id="9b031-353">ja.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="9b031-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="9b031-355">Kannada</span></span></td>
        <td><span data-ttu-id="9b031-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-357">Coreano</span><span class="sxs-lookup"><span data-stu-id="9b031-357">Korean</span></span></td>
        <td><span data-ttu-id="9b031-358">ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-360">Letão</span><span class="sxs-lookup"><span data-stu-id="9b031-360">Latvian</span></span></td>        
        <td><span data-ttu-id="9b031-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-363">Lituano</span><span class="sxs-lookup"><span data-stu-id="9b031-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="9b031-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-365">Malaiala</span><span class="sxs-lookup"><span data-stu-id="9b031-365">Malayalam</span></span></td>
        <td><span data-ttu-id="9b031-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-367">Malaio (latino)</span><span class="sxs-lookup"><span data-stu-id="9b031-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="9b031-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-369">Marati</span><span class="sxs-lookup"><span data-stu-id="9b031-369">Marathi</span></span></td>
        <td><span data-ttu-id="9b031-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-371">Norueguês</span><span class="sxs-lookup"><span data-stu-id="9b031-371">Norwegian</span></span></td>
        <td><span data-ttu-id="9b031-372">nb.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="9b031-374">Persa</span><span class="sxs-lookup"><span data-stu-id="9b031-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="9b031-375">FA.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="9b031-376">Polonês</span><span class="sxs-lookup"><span data-stu-id="9b031-376">Polish</span></span></td>
        <td><span data-ttu-id="9b031-377">pl.Microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-379">Português (Brasil)</span><span class="sxs-lookup"><span data-stu-id="9b031-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="9b031-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-382">Português (Portugal)</span><span class="sxs-lookup"><span data-stu-id="9b031-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="9b031-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="9b031-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-385">Punjabi</span><span class="sxs-lookup"><span data-stu-id="9b031-385">Punjabi</span></span></td>
        <td><span data-ttu-id="9b031-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-387">Romeno</span><span class="sxs-lookup"><span data-stu-id="9b031-387">Romanian</span></span></td>
        <td><span data-ttu-id="9b031-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-390">Russo</span><span class="sxs-lookup"><span data-stu-id="9b031-390">Russian</span></span></td>
        <td><span data-ttu-id="9b031-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-393">Sérvio (cirílico)</span><span class="sxs-lookup"><span data-stu-id="9b031-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="9b031-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-395">Sérvio (latino)</span><span class="sxs-lookup"><span data-stu-id="9b031-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="9b031-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-397">Eslovaco</span><span class="sxs-lookup"><span data-stu-id="9b031-397">Slovak</span></span></td>
        <td><span data-ttu-id="9b031-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-399">Esloveno</span><span class="sxs-lookup"><span data-stu-id="9b031-399">Slovenian</span></span></td>
        <td><span data-ttu-id="9b031-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-401">Espanhol</span><span class="sxs-lookup"><span data-stu-id="9b031-401">Spanish</span></span></td>
        <td><span data-ttu-id="9b031-402">es.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-404">Sueco</span><span class="sxs-lookup"><span data-stu-id="9b031-404">Swedish</span></span></td>
        <td><span data-ttu-id="9b031-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="9b031-407">Tâmil</span><span class="sxs-lookup"><span data-stu-id="9b031-407">Tamil</span></span></td>
        <td><span data-ttu-id="9b031-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-409">Télugo</span><span class="sxs-lookup"><span data-stu-id="9b031-409">Telugu</span></span></td>
        <td><span data-ttu-id="9b031-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-411">Tailandês</span><span class="sxs-lookup"><span data-stu-id="9b031-411">Thai</span></span></td>
        <td><span data-ttu-id="9b031-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-414">Turco</span><span class="sxs-lookup"><span data-stu-id="9b031-414">Turkish</span></span></td>
        <td><span data-ttu-id="9b031-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="9b031-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-417">Ucraniano</span><span class="sxs-lookup"><span data-stu-id="9b031-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="9b031-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="9b031-419">Urdu</span></span></td>
        <td><span data-ttu-id="9b031-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-421">Vietnamita</span><span class="sxs-lookup"><span data-stu-id="9b031-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="9b031-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="9b031-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="9b031-423">Além disso, o Azure Search fornece configurações do analisador que não são específicas de idiomas</span><span class="sxs-lookup"><span data-stu-id="9b031-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="9b031-424">Dobra ASCII padrão</span><span class="sxs-lookup"><span data-stu-id="9b031-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="9b031-425">standardasciifolding.Lucene</span><span class="sxs-lookup"><span data-stu-id="9b031-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="9b031-426">Segmentação de texto Unicode (Criador de Token Padrão)</span><span class="sxs-lookup"><span data-stu-id="9b031-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="9b031-427">Filtro de dobra em ASCII - converte caracteres Unicode que não pertencem a toohello conjunto dos primeiros 127 caracteres ASCII em seus equivalentes em ASCII.</span><span class="sxs-lookup"><span data-stu-id="9b031-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="9b031-428">Isso é útil para remover os sinais diacríticos.</span><span class="sxs-lookup"><span data-stu-id="9b031-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="9b031-429">Todos os analisadores com nomes anotados com <i>lucene</i> são da plataforma de [analisadores de idiomas do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="9b031-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="9b031-430">Para obter mais informações sobre o filtro de dobra em ASCII Olá podem ser encontradas [aqui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="9b031-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="9b031-431">**Sugestores**</span><span class="sxs-lookup"><span data-stu-id="9b031-431">**Suggesters**</span></span>

<span data-ttu-id="9b031-432">Um `suggester` define quais campos em um índice são usada toosupport preenchimento automático em pesquisas.</span><span class="sxs-lookup"><span data-stu-id="9b031-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="9b031-433">Normalmente, cadeias de caracteres de pesquisa parciais são enviadas toohello [API de sugestões](#Suggestions) enquanto o usuário hello está digitando uma consulta de pesquisa e Olá API retorna um conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="9b031-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="9b031-434">Uma sugestão que você definir no índice Olá determina quais campos são os termos de pesquisa de preenchimento automático de saudação do toobuild usado.</span><span class="sxs-lookup"><span data-stu-id="9b031-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="9b031-435">Consulte [Sugestores](#Suggesters) para obter detalhes de configuração.</span><span class="sxs-lookup"><span data-stu-id="9b031-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="9b031-436">**Perfis de pontuação**</span><span class="sxs-lookup"><span data-stu-id="9b031-436">**Scoring profiles**</span></span>

<span data-ttu-id="9b031-437">Um `scoringProfile` define os comportamentos de pontuação personalizados que lhe permitem influenciar quais itens aparecerão nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="9b031-438">Perfis de pontuação são compostos de funções e pesos de campos.</span><span class="sxs-lookup"><span data-stu-id="9b031-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="9b031-439">toouse-los, especifique um perfil por nome na cadeia de caracteres de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="9b031-440">Um perfil de pontuação padrão funciona por trás Olá cenas toocompute uma pontuação de pesquisa para cada item em um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="9b031-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="9b031-441">Você pode usar o perfil de pontuação interno e sem nome hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="9b031-442">Como alternativa, defina `defaultScoringProfile` toouse um perfil personalizado como padrão hello, invocado sempre que um perfil personalizado não for especificado na cadeia de caracteres de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="9b031-443">Consulte [tooa índice de pesquisa (API de REST do serviço de pesquisa do Azure) de perfis de pontuação adicionar](search-api-scoring-profiles-2015-02-28-preview.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="9b031-444">**Opções de CORS**</span><span class="sxs-lookup"><span data-stu-id="9b031-444">**CORS Options**</span></span>

<span data-ttu-id="9b031-445">Javascript do lado do cliente não é possível chamar quaisquer APIs por padrão, desde que o navegador Olá impedirá que todas as solicitações entre origens.</span><span class="sxs-lookup"><span data-stu-id="9b031-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="9b031-446">Habilitar o CORS (Cross-Origin Resource Sharing) por configuração Olá `corsOptions` índice de tooyour do atributo tooallow consultas entre origens.</span><span class="sxs-lookup"><span data-stu-id="9b031-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="9b031-447">Observe que apenas APIs de consulta dão suporte a CORS por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="9b031-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="9b031-448">Olá, as opções a seguir pode ser definida para CORS:</span><span class="sxs-lookup"><span data-stu-id="9b031-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="9b031-449">`allowedOrigins`(obrigatório): esta é uma lista de origens que terão o índice de tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="9b031-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="9b031-450">Isso significa que qualquer código Javascript servido dessas origens terá permissão tooquery seu índice (assumindo que fornece Olá chave de API correta).</span><span class="sxs-lookup"><span data-stu-id="9b031-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="9b031-451">Cada origem é geralmente do formulário Olá `protocol://fully-qualified-domain-name:port` embora Olá porta seja frequentemente omitida.</span><span class="sxs-lookup"><span data-stu-id="9b031-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="9b031-452">Consulte [este artigo](http://go.microsoft.com/fwlink/?LinkId=330822) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="9b031-453">Origens de tooall acesso tooallow, inclua `*` como um único item no hello `allowedOrigins` matriz.</span><span class="sxs-lookup"><span data-stu-id="9b031-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="9b031-454">Observe que **essa não é uma prática recomendável para serviços de pesquisa de produção.**</span><span class="sxs-lookup"><span data-stu-id="9b031-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="9b031-455">No entanto, pode ser útil para fins de depuração ou de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9b031-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="9b031-456">`maxAgeInSeconds`(opcional): os navegadores usam esse valor toodetermine Olá duração (em segundos) toocache CORS respostas de simulação.</span><span class="sxs-lookup"><span data-stu-id="9b031-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="9b031-457">Esse deve ser um inteiro não negativo.</span><span class="sxs-lookup"><span data-stu-id="9b031-457">This must be a non-negative integer.</span></span> <span data-ttu-id="9b031-458">Olá maior que esse valor é Olá desempenho será melhor, mas hello mais tempo levará para efeito de tootake de alterações de política CORS.</span><span class="sxs-lookup"><span data-stu-id="9b031-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="9b031-459">Se ele não for definido, uma duração padrão de cinco minutos será usada.</span><span class="sxs-lookup"><span data-stu-id="9b031-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="9b031-460"><a name="CreateUpdateIndexExample"></a>
**Exemplo de Corpo de Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-460"><a name="CreateUpdateIndexExample"></a>
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

<span data-ttu-id="9b031-461">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-461">**Response**</span></span>

<span data-ttu-id="9b031-462">Para uma solicitação bem-sucedida: "201 Criado".</span><span class="sxs-lookup"><span data-stu-id="9b031-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="9b031-463">Por padrão a corpo da resposta Olá conterá hello JSON para definição de índice de saudação que foi criada.</span><span class="sxs-lookup"><span data-stu-id="9b031-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="9b031-464">Se hello `Prefer` cabeçalho de solicitação está definido muito`return=minimal`, Olá corpo de resposta estará vazio e código de status de êxito Olá será "204 sem conteúdo" em vez de "201 criado".</span><span class="sxs-lookup"><span data-stu-id="9b031-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="9b031-465">Isso é verdadeiro independentemente se PUT ou POST foi índice de saudação toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="9b031-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="9b031-466">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="9b031-466">**Remarks**</span></span>

<span data-ttu-id="9b031-467">Atualmente, há suporte limitado para atualizações de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="9b031-468">Atualmente, não há suporte às atualizações de esquema que exigem reindexação, como a alteração de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="9b031-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="9b031-469">Embora os campos existentes não podem ser alterados ou excluídos, novos campos podem ser adicionados índice existente tooan a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="9b031-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="9b031-470">Quando um novo campo for adicionado, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo.</span><span class="sxs-lookup"><span data-stu-id="9b031-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="9b031-471">Não há espaço de armazenamento adicional será consumido até novos documentos são adicionados toohello índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="9b031-472">Sugestores</span><span class="sxs-lookup"><span data-stu-id="9b031-472">Suggesters</span></span>
<span data-ttu-id="9b031-473">recurso de sugestões de saudação na pesquisa do Azure é um recurso de consulta de preenchimento automático ou AutoCompletar, fornecendo uma lista de possíveis condições de pesquisa na entrada de cadeia de caracteres toopartial resposta inserida em uma caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="9b031-474">Você já deve ter notado sugestões de consulta ao usar mecanismos de pesquisa da web comercial: digitando ".NET" no Bing produz uma lista de termos de ".NET 4.5", ".NET Framework 3.5", e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="9b031-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="9b031-475">Ao usar a API REST do serviço de pesquisa hello, implementar sugestões em um aplicativo de pesquisa do Azure personalizado requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9b031-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="9b031-476">Habilitar sugestões adicionando uma **sugestão** construção em seu índice, fornecendo nome hello, no modo de pesquisa e uma lista de campos para a qual adiantado é invocada.</span><span class="sxs-lookup"><span data-stu-id="9b031-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="9b031-477">Por exemplo, se você especificar "cityName" como um campo de origem, digitar uma cadeia de caracteres de pesquisa parciais de "Sea" resultará em "Seattle", "Seaside" e "Seatac" (todos os três são nomes de cidades reais) oferecidos como usuário de toohello de sugestões de consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="9b031-478">Invocar sugestões chamando Olá [API de sugestões](#Suggestions) no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b031-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="9b031-479">Normalmente, cadeias de caracteres de pesquisa parciais são enviadas toohello serviço enquanto o usuário hello está digitando uma consulta de pesquisa, e essa API retorna um conjunto de frases sugeridas.</span><span class="sxs-lookup"><span data-stu-id="9b031-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="9b031-480">Este artigo explica como tooconfigure uma **sugestão**.</span><span class="sxs-lookup"><span data-stu-id="9b031-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="9b031-481">Você também deve revisar Olá [API de sugestões](#Suggestions) para obter detalhes sobre como uma sugestão é usada.</span><span class="sxs-lookup"><span data-stu-id="9b031-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="9b031-482">**Uso**</span><span class="sxs-lookup"><span data-stu-id="9b031-482">**Usage**</span></span>

<span data-ttu-id="9b031-483">`Suggesters`são criados no índice hello e funcionam melhor quando usadas documentos toosuggest específico em vez de perder termos ou frases.</span><span class="sxs-lookup"><span data-stu-id="9b031-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="9b031-484">campos de candidato Olá recomendados são títulos, nomes e outras frases relativamente curtas que podem identificar um item.</span><span class="sxs-lookup"><span data-stu-id="9b031-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="9b031-485">Os campos repetitivos, como categorias e marcas, ou campos muito longos, como campos de comentários ou descrições, são menos eficazes.</span><span class="sxs-lookup"><span data-stu-id="9b031-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="9b031-486">Como parte da definição de índice Olá, você pode adicionar um único sugestão toohello `suggesters` coleção.</span><span class="sxs-lookup"><span data-stu-id="9b031-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="9b031-487">As propriedades que definem uma sugestão incluem seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9b031-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="9b031-488">`name`: nome de saudação do encarregado da sugestão hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="9b031-489">Você usa o nome de saudação do encarregado da sugestão Olá ao chamar hello `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="9b031-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="9b031-490">`searchMode`: Olá toosearch estratégia usada para frases do candidato.</span><span class="sxs-lookup"><span data-stu-id="9b031-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="9b031-491">Olá único modo atualmente suportado é `analyzingInfixMatching`, que executa uma correspondência flexível de frases no início de saudação ou no meio de saudação das frases.</span><span class="sxs-lookup"><span data-stu-id="9b031-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="9b031-492">`sourceFields`: Uma lista de um ou mais campos que são Olá origem de conteúdo Olá para obter sugestões.</span><span class="sxs-lookup"><span data-stu-id="9b031-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="9b031-493">Somente os campos dos tipos `Edm.String` e `Collection(Edm.String)` podem ser fontes de sugestões.</span><span class="sxs-lookup"><span data-stu-id="9b031-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="9b031-494">Somente os campos que não têm um analisador de idioma personalizado definido podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="9b031-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="9b031-495">**Exemplo de sugestor**</span><span class="sxs-lookup"><span data-stu-id="9b031-495">**Suggester Example**</span></span>

<span data-ttu-id="9b031-496">Uma sugestão é parte do índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-496">A suggester is part of hello index.</span></span> <span data-ttu-id="9b031-497">Apenas uma sugestão pode existir em Olá `suggesters` coleção de campos da coleção na versão atual do hello, juntamente com hello e `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="9b031-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="9b031-498">Se você usou a versão de visualização pública de saudação da pesquisa do Azure, `suggesters` substitui uma propriedade booliana mais antiga (`"suggestions": false`) que suporte apenas sugestões de prefixo para cadeias de caracteres curtas (de 3 a 25 caracteres).</span><span class="sxs-lookup"><span data-stu-id="9b031-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="9b031-499">Sua substituição, `suggesters`, dá suporte a correspondência infixo que localiza os termos correspondentes no início de saudação ou no meio de saudação do conteúdo do campo, com melhor tolerância para erros em cadeias de caracteres de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="9b031-500">A partir da versão disponível hello, isso é agora Olá única implementação de API de sugestões de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="9b031-501">Olá antigo `suggestions` propriedade foi introduzida no `api-version=2014-07-31-Preview` continua toowork nessa versão, mas não está operacional no hello `2015-02-28` ou versões posteriores da pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="9b031-502">Atualizar o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-502">Update Index</span></span>
<span data-ttu-id="9b031-503">Você pode atualizar um índice existente no Azure Search usando uma solicitação HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="9b031-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="9b031-504">As atualizações podem incluir a adição de novos campos toohello esquema existente, modificando as opções de CORS e modificar perfis de pontuação.</span><span class="sxs-lookup"><span data-stu-id="9b031-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="9b031-505">Confira [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="9b031-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="9b031-506">Especifique o nome de Olá de saudação índice tooupdate no URI de solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="9b031-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9b031-507">**Importante:** suporte para atualizações de esquema de índice é limitado toooperations que não requerem a recriação do índice de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="9b031-508">Atualmente, não há suporte às atualizações de esquema que exigem reindexação, como a alteração de tipos de campo.</span><span class="sxs-lookup"><span data-stu-id="9b031-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="9b031-509">Novos campos podem ser adicionados a qualquer momento, embora os campos existentes não possam ser alterados nem excluídos.</span><span class="sxs-lookup"><span data-stu-id="9b031-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="9b031-510">Olá mesmo se aplica muito`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="9b031-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="9b031-511">Novos campos podem ser adicionados sugestão tooa em campos de Olá Olá hora são adicionados, mas não não possível remover campos `suggesters` e os campos existentes não podem ser adicionados muito`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="9b031-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="9b031-512">Ao adicionar um novo índice tooan campo, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo.</span><span class="sxs-lookup"><span data-stu-id="9b031-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="9b031-513">Não há espaço de armazenamento adicional será consumido até novos documentos são adicionados toohello índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="9b031-514">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-514">**Request**</span></span>

<span data-ttu-id="9b031-515">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9b031-516">Olá **índice de atualização** solicitação é construída usando HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="9b031-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="9b031-517">Com PUT, o nome do índice Olá é parte da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="9b031-518">Se o índice Olá não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="9b031-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="9b031-519">Se já existir um índice de Olá, é atualizado toohello nova definição.</span><span class="sxs-lookup"><span data-stu-id="9b031-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="9b031-520">nome do índice Olá deve estar em letras minúsculas, começar com uma letra ou número, não ter barras ou pontos e ter menos de 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9b031-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="9b031-521">Depois de iniciar o nome do índice Olá com uma letra ou número, restante de saudação do nome hello pode incluir qualquer letra, número e traços, como Olá traços não sejam consecutivos.</span><span class="sxs-lookup"><span data-stu-id="9b031-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="9b031-522">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-523">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-524">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-525">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-525">**Request Headers**</span></span>

<span data-ttu-id="9b031-526">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-527">`Content-Type`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-527">`Content-Type`: Required.</span></span> <span data-ttu-id="9b031-528">Defina esta opção muito`application/json`</span><span class="sxs-lookup"><span data-stu-id="9b031-528">Set this too`application/json`</span></span>
* <span data-ttu-id="9b031-529">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-529">`api-key`: Required.</span></span> <span data-ttu-id="9b031-530">Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-531">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-532">Olá **índice de atualização** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-533">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-534">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-535">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-536">**Sintaxe de corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-536">**Request Body Syntax**</span></span>

<span data-ttu-id="9b031-537">Ao atualizar um índice existente, corpo Olá deve incluir a definição de esquema original hello, além de adicionar novos campos de hello, bem como Olá modificado perfis de pontuação, sugestões e opções de CORS, se houver.</span><span class="sxs-lookup"><span data-stu-id="9b031-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="9b031-538">Se você não estiver modificando os perfis de pontuação hello e opções de CORS, você deve incluir originais de saudação do quando o índice de saudação foi criado.</span><span class="sxs-lookup"><span data-stu-id="9b031-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="9b031-539">Em geral Olá melhor padrão toouse atualizações é definição de índice de saudação tooretrieve com um GET, modificá-lo e atualizá-la com PUT.</span><span class="sxs-lookup"><span data-stu-id="9b031-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="9b031-540">sintaxe de esquema Olá usado toocreate que um índice é reproduzido aqui por conveniência.</span><span class="sxs-lookup"><span data-stu-id="9b031-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="9b031-541">Consulte [Criar Índice](#CreateIndex) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-541">See [Create Index](#CreateIndex) for more details.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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


<span data-ttu-id="9b031-542">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-542">**Response**</span></span>

<span data-ttu-id="9b031-543">Para uma solicitação bem-sucedida: "204 sem Conteúdo".</span><span class="sxs-lookup"><span data-stu-id="9b031-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="9b031-544">Por padrão, o corpo de resposta Olá estará vazio.</span><span class="sxs-lookup"><span data-stu-id="9b031-544">By default hello response body will be empty.</span></span> <span data-ttu-id="9b031-545">No entanto, se hello `Prefer` cabeçalho de solicitação está definido muito`return=representation`, corpo da resposta Olá conterá Olá JSON para definição de índice de saudação que foi atualizada.</span><span class="sxs-lookup"><span data-stu-id="9b031-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="9b031-546">Nesse caso, o código de status de êxito Olá será "200 Okey".</span><span class="sxs-lookup"><span data-stu-id="9b031-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="9b031-547">**Atualizando a definição de índice com analisadores personalizados**</span><span class="sxs-lookup"><span data-stu-id="9b031-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="9b031-548">Quando um analisador, um criador de token, um filtro de token ou um filtro de char é definido, ele não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="9b031-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="9b031-549">Novos podem ser adicionados índice existente tooan somente se hello `allowIndexDowntime` sinalizador é definido tootrue na solicitação de atualização do índice hello:</span><span class="sxs-lookup"><span data-stu-id="9b031-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="9b031-550">Observe que essa operação colocará seu índice offline pelo menos alguns segundos, fazendo com que a indexação e consulta solicita toofail.</span><span class="sxs-lookup"><span data-stu-id="9b031-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="9b031-551">Disponibilidade de desempenho e a gravação de índice Olá pode ser afetado por vários minutos após a atualização do índice de hello, ou mais índices muito grandes.</span><span class="sxs-lookup"><span data-stu-id="9b031-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="9b031-552">Listar Índices</span><span class="sxs-lookup"><span data-stu-id="9b031-552">List Indexes</span></span>
<span data-ttu-id="9b031-553">Olá **lista índices** operação retorna uma lista de índices de saudação atualmente em seu serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="9b031-554">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-554">**Request**</span></span>

<span data-ttu-id="9b031-555">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9b031-556">Olá **lista índices** solicitação pode ser criada usando o método GET hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9b031-557">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-558">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-559">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-560">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-560">**Request Headers**</span></span>

<span data-ttu-id="9b031-561">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-562">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-562">`api-key`: Required.</span></span> <span data-ttu-id="9b031-563">Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-564">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-565">Olá **lista índices** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-566">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-567">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-568">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-569">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-569">**Request Body**</span></span>

<span data-ttu-id="9b031-570">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="9b031-570">None.</span></span>

<span data-ttu-id="9b031-571">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-571">**Response**</span></span>

<span data-ttu-id="9b031-572">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9b031-573">Aqui está um exemplo de corpo de resposta:</span><span class="sxs-lookup"><span data-stu-id="9b031-573">Here is an example response body:</span></span>

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

<span data-ttu-id="9b031-574">Observe que você pode filtrar a resposta Olá para propriedades de saudação toojust em que você estiver interessado.</span><span class="sxs-lookup"><span data-stu-id="9b031-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="9b031-575">Por exemplo, se você quiser apenas uma lista de nomes de índice, use Olá OData `$select` opção de consulta:</span><span class="sxs-lookup"><span data-stu-id="9b031-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="9b031-576">Nesse caso, resposta Olá Olá acima exemplo seria exibida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9b031-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="9b031-577">Isso é uma largura de banda de toosave técnica útil se você tiver muitos índices em seu serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="9b031-578">Obter o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-578">Get Index</span></span>
<span data-ttu-id="9b031-579">Olá **obter índice** operação obtém a definição de índice de saudação da pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="9b031-580">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-580">**Request**</span></span>

<span data-ttu-id="9b031-581">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="9b031-582">Olá **obter índice** solicitação pode ser criada usando o método GET hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9b031-583">Olá [nome do índice] no URI de solicitação de saudação especifica quais tooreturn de índice da coleção de índices de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="9b031-584">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-585">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-586">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-587">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-587">**Request Headers**</span></span>

<span data-ttu-id="9b031-588">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-589">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-590">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-591">Olá **obter índice** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-592">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-593">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-594">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-595">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-595">**Request Body**</span></span>

<span data-ttu-id="9b031-596">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="9b031-596">None.</span></span>

<span data-ttu-id="9b031-597">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-597">**Response**</span></span>

<span data-ttu-id="9b031-598">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9b031-599">Consulte o exemplo hello JSON em [criação e atualização de um índice](#CreateUpdateIndexExample) para obter um exemplo da carga de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="9b031-600">Excluir o índice</span><span class="sxs-lookup"><span data-stu-id="9b031-600">Delete Index</span></span>
<span data-ttu-id="9b031-601">Olá **Excluir índice** operação remove um índice e os documentos associados do seu serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="9b031-602">Você pode obter o nome do índice Olá Olá no painel de serviço no portal do Azure de saudação ou Olá API.</span><span class="sxs-lookup"><span data-stu-id="9b031-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="9b031-603">Consulte [Listar índices](#ListIndexes) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="9b031-604">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-604">**Request**</span></span>

<span data-ttu-id="9b031-605">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="9b031-606">Olá **Excluir índice** solicitação pode ser criada usando o método de exclusão hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="9b031-607">Olá [nome do índice] no URI de solicitação de saudação especifica quais toodelete de índice da coleção de índices de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="9b031-608">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-609">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-610">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-611">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-611">**Request Headers**</span></span>

<span data-ttu-id="9b031-612">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-613">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-613">`api-key`: Required.</span></span> <span data-ttu-id="9b031-614">Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-615">É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9b031-616">Olá **Excluir índice** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-617">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-618">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-619">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-620">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-620">**Request Body**</span></span>

<span data-ttu-id="9b031-621">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="9b031-621">None.</span></span>

<span data-ttu-id="9b031-622">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-622">**Response**</span></span>

<span data-ttu-id="9b031-623">Código de status: 204 Sem Conteúdo é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="9b031-624">Obter estatísticas de índice</span><span class="sxs-lookup"><span data-stu-id="9b031-624">Get Index Statistics</span></span>
<span data-ttu-id="9b031-625">Olá **obter estatísticas de índice** operação retorna uma contagem de documento de índice atual hello, além de utilização de armazenamento da pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="9b031-626">As estatísticas de tamanho de armazenamento e contagem de documentos são coletadas a cada poucos minutos, não em tempo real.</span><span class="sxs-lookup"><span data-stu-id="9b031-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="9b031-627">Portanto, estatísticas de hello retornadas pela API podem não refletir as alterações causadas por operações de indexação recentes.</span><span class="sxs-lookup"><span data-stu-id="9b031-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="9b031-628">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-628">**Request**</span></span>

<span data-ttu-id="9b031-629">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="9b031-630">Olá **obter estatísticas de índice** solicitação pode ser criada usando o método GET hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9b031-631">Olá [nome do índice] no URI de solicitação Olá informa Olá serviço tooreturn as estatísticas de índice para o índice especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="9b031-632">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-633">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-634">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-635">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-635">**Request Headers**</span></span>

<span data-ttu-id="9b031-636">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-637">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-638">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-639">Olá **obter estatísticas de índice** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-640">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-641">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-642">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-643">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-643">**Request Body**</span></span>

<span data-ttu-id="9b031-644">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="9b031-644">None.</span></span>

<span data-ttu-id="9b031-645">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-645">**Response**</span></span>

<span data-ttu-id="9b031-646">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9b031-647">corpo da resposta Hello está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b031-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="9b031-648">Analisador de teste</span><span class="sxs-lookup"><span data-stu-id="9b031-648">Test Analyzer</span></span>
<span data-ttu-id="9b031-649">Olá **API analisar** mostra como um analisador quebra o texto em tokens.</span><span class="sxs-lookup"><span data-stu-id="9b031-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9b031-650">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-650">**Request**</span></span>

<span data-ttu-id="9b031-651">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="9b031-652">Olá **API analisar** solicitação pode ser criada usando o método de POSTAGEM hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="9b031-653">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-654">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-655">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-656">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-656">**Request Headers**</span></span>

<span data-ttu-id="9b031-657">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-658">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-659">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-660">Olá **API analisar** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-661">Nome do índice hello e URL de solicitação de Olá Olá serviço nome tooconstruct também será necessário.</span><span class="sxs-lookup"><span data-stu-id="9b031-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-662">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-663">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-664">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="9b031-665">ou o</span><span class="sxs-lookup"><span data-stu-id="9b031-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="9b031-666">Olá `analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` necessários toobe os nomes válidos de analisadores predefinidas ou personalizadas, tokenizers, filtros de token e filtros de char para índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="9b031-667">toolearn mais informações sobre o processo de saudação de análise lexical consulte [análise na pesquisa do Azure](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="9b031-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="9b031-668">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-668">**Response**</span></span>

<span data-ttu-id="9b031-669">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9b031-670">corpo da resposta Hello está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b031-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="9b031-671">**Analisar exemplo de API**</span><span class="sxs-lookup"><span data-stu-id="9b031-671">**Analyze API example**</span></span>

<span data-ttu-id="9b031-672">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="9b031-673">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="9b031-674">Operações de documento</span><span class="sxs-lookup"><span data-stu-id="9b031-674">Document Operations</span></span>
<span data-ttu-id="9b031-675">Na pesquisa do Azure, um índice é armazenado na nuvem hello e preenchido usando documentos JSON que você carregue toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="9b031-676">Todos os documentos de saudação que você carregar incluem corpo de saudação de seus dados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="9b031-677">Documentos contêm campos, alguns dos quais são indexados em termos de pesquisa ao serem carregados.</span><span class="sxs-lookup"><span data-stu-id="9b031-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="9b031-678">Olá `/docs` segmento de URL no hello API de pesquisa do Azure representa a coleção de saudação de documentos em um índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="9b031-679">Todas as operações executadas na coleção de saudação, como carregar, mesclar, excluir ou consultar documentos ocorrem no contexto de saudação de um único índice, portanto URLs de saudação para essas operações sempre começam com `/indexes/[index name]/docs` para um nome de índice fornecido.</span><span class="sxs-lookup"><span data-stu-id="9b031-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="9b031-680">O código do aplicativo deve gerar JSON documentos tooupload tooAzure pesquisa ou você pode usar um [indexador](https://msdn.microsoft.com/library/dn946891.aspx) tooload documentos se a fonte de dados de saudação é o banco de dados SQL ou banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9b031-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="9b031-681">Normalmente, os índices são preenchidos por meio de um único conjunto de dados que você fornece.</span><span class="sxs-lookup"><span data-stu-id="9b031-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="9b031-682">Você deve planejar ter um documento para cada item que você deseja toosearch.</span><span class="sxs-lookup"><span data-stu-id="9b031-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="9b031-683">Um aplicativo de aluguel de filmes pode ter um documento por filme, um aplicativo de vitrine pode ter um documento por SKU, um aplicativo de cursos online pode ter um documento por curso, uma empresa de pesquisa pode ter um documento para cada artigo acadêmico em seu repositório e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="9b031-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="9b031-684">Os documentos consistem em um ou mais campos.</span><span class="sxs-lookup"><span data-stu-id="9b031-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="9b031-685">Os campos podem conter texto indexado pelo Azure Search em termos de pesquisa, bem como valores não indexados ou que não são de texto, que podem ser usadas em filtros ou perfis de pontuação.</span><span class="sxs-lookup"><span data-stu-id="9b031-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="9b031-686">Olá nomes, tipos de dados e recursos de pesquisa com suporte para cada campo são determinados pelo esquema de índice hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="9b031-687">Um dos campos de saudação em cada esquema de índice deve ser designado como uma ID e cada documento deve ter um valor para o campo de ID de saudação que identifica exclusivamente o documento no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="9b031-688">Todos os outros campos de documento são opcionais e assumirá o valor nulo tooa se não especificado.</span><span class="sxs-lookup"><span data-stu-id="9b031-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="9b031-689">Observe que valores nulos não ocupam espaço no índice de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="9b031-690">Antes de poder carregar documentos, você já deve ter criado o índice de saudação no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="9b031-691">Consulte [Criar o índice](#CreateIndex) para obter detalhes sobre essa primeira etapa.</span><span class="sxs-lookup"><span data-stu-id="9b031-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="9b031-692">Adicionar, Atualizar ou Excluir Documentos</span><span class="sxs-lookup"><span data-stu-id="9b031-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="9b031-693">Você pode carregar, mesclar, mesclar ou carregar ou excluir documentos de um índice especificado usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="9b031-694">Para um grande número de atualizações, recomenda-se o processamento em lotes de documentos (too1000 documentos por lote) ou aproximadamente 16 MB por lote.</span><span class="sxs-lookup"><span data-stu-id="9b031-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="9b031-695">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-695">**Request**</span></span>

<span data-ttu-id="9b031-696">HTTPS é necessário para todas as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="9b031-697">Você pode carregar, mesclar, mesclar ou carregar ou excluir documentos de um índice especificado usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="9b031-698">Olá URI da solicitação inclui [nome do índice], especificando quais documentos toopost de índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="9b031-699">Só é possível publicar o índice de tooone documentos por vez.</span><span class="sxs-lookup"><span data-stu-id="9b031-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="9b031-700">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-701">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-702">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-703">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-703">**Request Headers**</span></span>

<span data-ttu-id="9b031-704">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-705">`Content-Type`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-705">`Content-Type`: Required.</span></span> <span data-ttu-id="9b031-706">Defina esta opção muito`application/json`</span><span class="sxs-lookup"><span data-stu-id="9b031-706">Set this too`application/json`</span></span>
* <span data-ttu-id="9b031-707">`api-key`: obrigatório.</span><span class="sxs-lookup"><span data-stu-id="9b031-707">`api-key`: Required.</span></span> <span data-ttu-id="9b031-708">Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-709">É um valor de cadeia de caracteres, o serviço de tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="9b031-710">Olá **adicionar documentos** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).</span><span class="sxs-lookup"><span data-stu-id="9b031-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="9b031-711">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-712">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-713">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-714">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-714">**Request Body**</span></span>

<span data-ttu-id="9b031-715">corpo de saudação da solicitação de saudação contém um ou mais toobe de documentos indexados.</span><span class="sxs-lookup"><span data-stu-id="9b031-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="9b031-716">Os documentos são identificados por uma chave exclusiva.</span><span class="sxs-lookup"><span data-stu-id="9b031-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="9b031-717">Cada documento está associado uma ação: carregar, mesclar, mesclar ou carregar ou excluir.</span><span class="sxs-lookup"><span data-stu-id="9b031-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="9b031-718">Solicitações de carregamento devem incluir dados de documento hello como um conjunto de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="9b031-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="9b031-719">As chaves de documento só podem conter letras, números, traços ("-"), sublinhados ("_") e sinais de igual ("=").</span><span class="sxs-lookup"><span data-stu-id="9b031-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="9b031-720">Para obter mais detalhes, veja [Regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="9b031-721">**Ações do documento**</span><span class="sxs-lookup"><span data-stu-id="9b031-721">**Document Actions**</span></span>

* <span data-ttu-id="9b031-722">`upload`: Uma ação de carregamento é semelhante tooan "upsert" onde documento hello será inserido se for novo e atualizado/substituído se ele existir.</span><span class="sxs-lookup"><span data-stu-id="9b031-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="9b031-723">Observe que todos os campos são substituídos no caso de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="9b031-724">`merge`: Merge atualiza uma existente de documento com hello especificado campos.</span><span class="sxs-lookup"><span data-stu-id="9b031-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="9b031-725">Se o documento de saudação não existir, a mesclagem de Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="9b031-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="9b031-726">Qualquer campo que você especificar em uma mesclagem substituirá o campo de saudação existente no documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="9b031-727">Isso inclui campos do tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="9b031-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="9b031-728">Por exemplo, se hello documento contém um campo "tags" com valor `["budget"]` e executar uma mesclagem com valor `["economy", "pool"]` para "tags", o valor final de saudação do campo "tags" hello será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="9b031-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="9b031-729">Ele **não** será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="9b031-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="9b031-730">`mergeOrUpload`: se comporta como `merge` se um documento com hello atribuída a chave já existe no índice hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="9b031-731">Se o documento de saudação não existir, ela se comporta como `upload` com um novo documento.</span><span class="sxs-lookup"><span data-stu-id="9b031-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="9b031-732">`delete`: Excluir remove o documento especificado de saudação do índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="9b031-733">Observe que todos os campos que você especificar em uma `delete` operação diferente de campo de chave hello será ignorada.</span><span class="sxs-lookup"><span data-stu-id="9b031-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="9b031-734">Se você quiser tooremove um campo individual de um documento, use `merge` em vez disso e basta definir campo Olá explicitamente muito`null`.</span><span class="sxs-lookup"><span data-stu-id="9b031-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="9b031-735">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-735">**Response**</span></span>

<span data-ttu-id="9b031-736">O código de status 200 (OK) é retornado para uma resposta bem-sucedida, indicando que todos os itens foram indexados com êxito.</span><span class="sxs-lookup"><span data-stu-id="9b031-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="9b031-737">Isso é indicado por Olá `status` propriedade sendo definida tootrue para todos os itens, bem como Olá `statusCode` propriedade sendo definida tooeither 201 (para documentos recentemente carregados) ou 200 (para documentos mesclados ou excluídos):</span><span class="sxs-lookup"><span data-stu-id="9b031-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="9b031-738">O código de status 207 (Multi-Status) será retornado quando pelo menos um item não tiver sido indexado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9b031-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="9b031-739">Itens que não tenham sido indexados possuem Olá `status` toofalse do conjunto de campos.</span><span class="sxs-lookup"><span data-stu-id="9b031-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="9b031-740">Olá `errorMessage` e `statusCode` propriedades indicará o motivo Olá Olá erro de indexação:</span><span class="sxs-lookup"><span data-stu-id="9b031-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
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
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="9b031-741">Olá, a tabela a seguir explica Olá vários por documento códigos de status que podem ser retornados em resposta hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="9b031-742">Observe que alguns indicam problemas com solicitação hello, enquanto outros indicam as condições de erro temporário.</span><span class="sxs-lookup"><span data-stu-id="9b031-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="9b031-743">Olá último que deve tentar novamente após um atraso.</span><span class="sxs-lookup"><span data-stu-id="9b031-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="9b031-744">Código de status</span><span class="sxs-lookup"><span data-stu-id="9b031-744">Status code</span></span></th>
        <th><span data-ttu-id="9b031-745">Significado</span><span class="sxs-lookup"><span data-stu-id="9b031-745">Meaning</span></span></th>
        <th><span data-ttu-id="9b031-746">Com nova tentativa</span><span class="sxs-lookup"><span data-stu-id="9b031-746">Retryable</span></span></th>
        <th><span data-ttu-id="9b031-747">Observações</span><span class="sxs-lookup"><span data-stu-id="9b031-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-748">200</span><span class="sxs-lookup"><span data-stu-id="9b031-748">200</span></span></td>
        <td><span data-ttu-id="9b031-749">O documento foi modificado ou excluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="9b031-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="9b031-750">n/d</span><span class="sxs-lookup"><span data-stu-id="9b031-750">n/a</span></span></td>
        <td><span data-ttu-id="9b031-751">As operações de exclusão são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="9b031-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="9b031-752">Ou seja, mesmo se não existir uma chave de documento no índice hello, a tentativa de uma operação de exclusão com essa chave resultará em um código de 200 status.</span><span class="sxs-lookup"><span data-stu-id="9b031-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-753">201</span><span class="sxs-lookup"><span data-stu-id="9b031-753">201</span></span></td>
        <td><span data-ttu-id="9b031-754">O documento foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9b031-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="9b031-755">n/d</span><span class="sxs-lookup"><span data-stu-id="9b031-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-756">400</span><span class="sxs-lookup"><span data-stu-id="9b031-756">400</span></span></td>
        <td><span data-ttu-id="9b031-757">Ocorreu um erro no documento de saudação que impediu a serem indexados.</span><span class="sxs-lookup"><span data-stu-id="9b031-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="9b031-758">Não</span><span class="sxs-lookup"><span data-stu-id="9b031-758">No</span></span></td>
        <td><span data-ttu-id="9b031-759">mensagem de erro de saudação em resposta Olá indicará o que há de errado com o documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-760">404</span><span class="sxs-lookup"><span data-stu-id="9b031-760">404</span></span></td>
        <td><span data-ttu-id="9b031-761">documento de saudação não pode ser mesclado porque Olá recebe a chave não existe no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="9b031-762">Não</span><span class="sxs-lookup"><span data-stu-id="9b031-762">No</span></span></td>
        <td><span data-ttu-id="9b031-763">Esse erro não ocorre em carregamentos, uma vez que eles criam novos documentos e não ocorre em exclusões porque elas são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="9b031-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-764">409</span><span class="sxs-lookup"><span data-stu-id="9b031-764">409</span></span></td>
        <td><span data-ttu-id="9b031-765">Foi detectado um conflito de versão durante a tentativa de tooindex um documento.</span><span class="sxs-lookup"><span data-stu-id="9b031-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="9b031-766">Sim</span><span class="sxs-lookup"><span data-stu-id="9b031-766">Yes</span></span></td>
        <td><span data-ttu-id="9b031-767">Isso pode acontecer quando você estiver tentando Olá tooindex mesmo documento mais de uma vez simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9b031-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-768">422</span><span class="sxs-lookup"><span data-stu-id="9b031-768">422</span></span></td>
        <td><span data-ttu-id="9b031-769">índice de saudação está temporariamente indisponível porque ele foi atualizado com too'true de conjunto de sinalizador Olá 'allowIndexDowntime' '.</span><span class="sxs-lookup"><span data-stu-id="9b031-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="9b031-770">Sim</span><span class="sxs-lookup"><span data-stu-id="9b031-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="9b031-771">503</span><span class="sxs-lookup"><span data-stu-id="9b031-771">503</span></span></td>
        <td><span data-ttu-id="9b031-772">O serviço de pesquisa está temporariamente indisponível, possivelmente devido a carga de tooheavy.</span><span class="sxs-lookup"><span data-stu-id="9b031-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="9b031-773">Sim</span><span class="sxs-lookup"><span data-stu-id="9b031-773">Yes</span></span></td>
        <td><span data-ttu-id="9b031-774">Seu código deve aguardar antes de tentar novamente neste caso ou prolongando indisponibilidade de serviço Olá o risco.</span><span class="sxs-lookup"><span data-stu-id="9b031-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="9b031-775">**Observação**: se o seu código de cliente com frequência encontrar uma resposta 207, um motivo possível é que o sistema hello está sob carga.</span><span class="sxs-lookup"><span data-stu-id="9b031-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="9b031-776">Você pode confirmar isso verificando Olá `statusCode` propriedade 503.</span><span class="sxs-lookup"><span data-stu-id="9b031-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="9b031-777">Se esse for o caso de Olá, é recomendável ***limitação de solicitações de indexação***.</span><span class="sxs-lookup"><span data-stu-id="9b031-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="9b031-778">Caso contrário, se o tráfego de indexação não diminuir, o sistema Olá pode iniciar a rejeição de todas as solicitações com 503 erros.</span><span class="sxs-lookup"><span data-stu-id="9b031-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="9b031-779">O código de status 429 indica que você excedeu sua cota no número de saudação de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="9b031-780">Você deve criar um novo índice ou atualizar para limites de capacidade mais altos.</span><span class="sxs-lookup"><span data-stu-id="9b031-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="9b031-781">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="9b031-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="9b031-782">Pesquisar Documentos</span><span class="sxs-lookup"><span data-stu-id="9b031-782">Search Documents</span></span>
<span data-ttu-id="9b031-783">Um **pesquisa** operação é emitida como uma solicitação GET ou POST e especifica os parâmetros que fornecem os critérios de saudação para seleção de documentos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="9b031-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="9b031-784">**Quando toouse POST em vez de obter**</span><span class="sxs-lookup"><span data-stu-id="9b031-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="9b031-785">Quando você usa o HTTP GET toocall Olá **pesquisa** API, você precisa toobe ciente de que o comprimento Olá Olá URL da solicitação não pode exceder 8 KB.</span><span class="sxs-lookup"><span data-stu-id="9b031-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="9b031-786">Isso costuma ser suficiente para a maioria dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9b031-786">This is usually enough for most applications.</span></span> <span data-ttu-id="9b031-787">No entanto, alguns aplicativos geram consultas muito grandes ou expressões de filtro OData.</span><span class="sxs-lookup"><span data-stu-id="9b031-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="9b031-788">Para esses aplicativos, usar HTTP POST é uma opção melhor, pois permite filtros e consultas maiores que o GET.</span><span class="sxs-lookup"><span data-stu-id="9b031-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="9b031-789">Com o POST, o número de saudação de cláusulas em uma consulta ou termos Olá limitar fator, não o tamanho de saudação de consulta brutos de saudação desde que o limite de tamanho de solicitação de saudação do POST é aproximadamente 16 MB.</span><span class="sxs-lookup"><span data-stu-id="9b031-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-790">Mesmo que o limite de tamanho de solicitação POST Olá for muito grande, as consultas de pesquisa e as expressões de filtro não podem ser arbitrariamente complexas.</span><span class="sxs-lookup"><span data-stu-id="9b031-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="9b031-791">Confira a [Sintaxe de consulta Lucene](https://msdn.microsoft.com/library/mt589323.aspx) e a [Sintaxe de expressão OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de consulta e filtro de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="9b031-792">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-792">**Request**</span></span>

<span data-ttu-id="9b031-793">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="9b031-794">Olá **pesquisa** solicitação pode ser criada usando Olá GET ou métodos POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="9b031-795">URI de solicitação de saudação especifica quais tooquery de índice, para todos os documentos que correspondam a parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="9b031-796">Parâmetros são especificados na cadeia de caracteres de consulta de saudação no caso de saudação de solicitações GET e na solicitação Olá solicitações de corpo no caso de saudação de POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="9b031-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="9b031-797">Como uma prática recomendada, ao criar solicitações GET, lembre-se muito[a codificação de URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parâmetros ao chamar hello API REST diretamente.</span><span class="sxs-lookup"><span data-stu-id="9b031-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="9b031-798">Para operações de **Pesquisa** , isso inclui:</span><span class="sxs-lookup"><span data-stu-id="9b031-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="9b031-799">Codificação de URL é recomendada apenas nos Olá acima parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="9b031-800">Se você inadvertidamente a codificação de URL hello cadeia de caracteres de consulta inteira (tudo após Olá?), as solicitações são interrompidas.</span><span class="sxs-lookup"><span data-stu-id="9b031-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="9b031-801">Além disso, a codificação de URL só é necessária ao chamar hello API REST diretamente usando obter.</span><span class="sxs-lookup"><span data-stu-id="9b031-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="9b031-802">Nenhuma codificação de URL é necessária ao chamar **pesquisa** usando POST, ou ao usar o hello [biblioteca cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que trata de codificação de URL para você.</span><span class="sxs-lookup"><span data-stu-id="9b031-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="9b031-803"><a name="SearchQueryParameters"></a>
**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="9b031-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="9b031-804">**Search** aceita vários parâmetros que fornecem critérios de consulta e especificam o comportamento da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="9b031-805">Você fornecer esses parâmetros na URL Olá cadeia de caracteres de consulta ao chamar **pesquisa** por meio de GET e como propriedades JSON no corpo da solicitação Olá ao chamar **pesquisa** por meio de POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="9b031-806">sintaxe de saudação para alguns parâmetros é ligeiramente diferente entre GET e POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="9b031-807">Essas diferenças são indicadas, como aplicável, abaixo:</span><span class="sxs-lookup"><span data-stu-id="9b031-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="9b031-808">`search=[string]`(opcional) - Olá toosearch de texto para.</span><span class="sxs-lookup"><span data-stu-id="9b031-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="9b031-809">Todos os campos `searchable` são pesquisados por padrão, a menos que `searchFields` sejam especificados.</span><span class="sxs-lookup"><span data-stu-id="9b031-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="9b031-810">Ao pesquisar `searchable` campos, Olá texto de pesquisa é indexado para vários termos podem ser separados por espaços em branco (por exemplo: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="9b031-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="9b031-811">toomatch qualquer termo, use `*` (Isso pode ser útil para consultas de filtro booliano).</span><span class="sxs-lookup"><span data-stu-id="9b031-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="9b031-812">Omitir esse parâmetro tem o mesmo efeito que defini-lo muito de saudação`*`.</span><span class="sxs-lookup"><span data-stu-id="9b031-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="9b031-813">Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) para obter informações específicas sobre a sintaxe de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="9b031-814">**Observação**: resultados Olá às vezes podem ser surpreendentes ao consultar sobre `searchable` campos.</span><span class="sxs-lookup"><span data-stu-id="9b031-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="9b031-815">tokenizer Olá inclui lógica toohandle casos comuns tooEnglish texto como apóstrofes, vírgulas nos números, etc. Por exemplo, `search=123,456` corresponderá a um único termo 123,456, em vez de termos individuais de saudação 123 e 456, já que as vírgulas são usadas como separadores de milhar para números grandes em inglês.</span><span class="sxs-lookup"><span data-stu-id="9b031-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="9b031-816">Por esse motivo, recomendamos o uso de espaço em branco em vez de termos de tooseparate de pontuação em Olá `search` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9b031-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="9b031-817">`searchMode=any|all`(opcional, padrão é muito`any`): se qualquer ou todos os termos de pesquisa Olá devem ser iguais em ordem toocount Olá documento uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="9b031-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="9b031-818">`searchFields=[string]`(opcional) - lista de saudação do toosearch de nomes de campos separados por vírgulas para Olá o texto especificado.</span><span class="sxs-lookup"><span data-stu-id="9b031-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="9b031-819">Os campos de destino devem ser marcados como `searchable`.</span><span class="sxs-lookup"><span data-stu-id="9b031-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="9b031-820">`queryType=simple|full`(opcional, padrão é muito`simple`) - ao definir o texto de pesquisa muito "simples" é interpretado usando uma linguagem de consulta simples que permite símbolos, como +, * e "".</span><span class="sxs-lookup"><span data-stu-id="9b031-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="9b031-821">As consultas são avaliadas em todos os campos pesquisáveis (ou nos campos indicados em `searchFields`) em cada documento por padrão.</span><span class="sxs-lookup"><span data-stu-id="9b031-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="9b031-822">Quando o tipo de consulta de saudação está definido muito`full` texto de pesquisa é interpretado usando linguagem de consulta do Lucene Olá que permite que as pesquisas de campo específicos e ponderadas.</span><span class="sxs-lookup"><span data-stu-id="9b031-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="9b031-823">Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) e [sintaxe de consulta do Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para obter informações específicas sobre sintaxes de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="9b031-824">Intervalo de pesquisa no hello Lucene, não há suporte para a linguagem de consulta em favor $filter que oferece funcionalidade semelhante.</span><span class="sxs-lookup"><span data-stu-id="9b031-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="9b031-825">`moreLikeThis=[key]` (opcional) **Importante:** esse recurso só está disponível na `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-826">Essa opção não pode ser usada em uma consulta que contém o parâmetro de pesquisa de texto de saudação, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="9b031-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="9b031-827">Olá `moreLikeThis` parâmetro localiza os documentos que são semelhantes documento toohello especificado pela chave do documento hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="9b031-828">Quando uma solicitação de pesquisa é feita com `moreLikeThis`, uma lista de termos de pesquisa é gerada com base em frequência hello e raridade termos no documento de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="9b031-829">Esses termos são usado toomake Olá solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="9b031-830">Por padrão, Olá conteúdo de todos os `searchable` campos serão considerados, a menos que `searchFields` é usado toorestrict quais campos são pesquisados.</span><span class="sxs-lookup"><span data-stu-id="9b031-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="9b031-831">`$skip=#`(opcional) - número de saudação de pesquisa resulta tooskip; Não pode ser superior a 100.000.</span><span class="sxs-lookup"><span data-stu-id="9b031-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="9b031-832">Se você precisar tooscan documentos em sequência, mas não é possível usar `$skip` devido a limitação de toothis, considere o uso de `$orderby` em uma chave totalmente ordenada e `$filter` com um intervalo de consulta em vez disso.</span><span class="sxs-lookup"><span data-stu-id="9b031-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-833">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `skip`, em vez de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="9b031-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="9b031-834">`$top=#`(opcional) - número de saudação de pesquisa resulta tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9b031-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="9b031-835">Isso pode ser usado em conjunto com `$skip` tooimplement cliente paginação de resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-836">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `top`, em vez de `$top`.</span><span class="sxs-lookup"><span data-stu-id="9b031-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="9b031-837">`$count=true|false`(opcional, padrão é muito`false`)-Especifica se toofetch Olá contagem total de resultados.</span><span class="sxs-lookup"><span data-stu-id="9b031-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="9b031-838">É Olá contagem de todos os documentos que correspondam a saudação `search` e `$filter` parâmetros, ignorando `$top` e `$skip`.</span><span class="sxs-lookup"><span data-stu-id="9b031-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="9b031-839">Definir esse valor muito`true` pode ter um impacto de desempenho.</span><span class="sxs-lookup"><span data-stu-id="9b031-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="9b031-840">Observe que a contagem de saudação retornada é uma aproximação.</span><span class="sxs-lookup"><span data-stu-id="9b031-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-841">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `count`, em vez de `$count`.</span><span class="sxs-lookup"><span data-stu-id="9b031-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="9b031-842">`$orderby=[string]`(opcional) - uma lista de expressões separadas por vírgulas toosort Olá resultados por.</span><span class="sxs-lookup"><span data-stu-id="9b031-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="9b031-843">Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função.</span><span class="sxs-lookup"><span data-stu-id="9b031-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="9b031-844">Cada expressão pode ser seguido por `asc` tooindicated em ordem crescente e `desc` tooindicate em ordem decrescente.</span><span class="sxs-lookup"><span data-stu-id="9b031-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="9b031-845">saudação padrão é a ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="9b031-845">hello default is ascending order.</span></span> <span data-ttu-id="9b031-846">As ligações são rompidas pelas pontuações de correspondência de saudação de documentos.</span><span class="sxs-lookup"><span data-stu-id="9b031-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="9b031-847">Se nenhum `$orderby` for especificado, ordem de classificação saudação padrão é decrescente pela pontuação de correspondência do documento.</span><span class="sxs-lookup"><span data-stu-id="9b031-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="9b031-848">Há um limite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9b031-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-849">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `orderby`, em vez de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9b031-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="9b031-850">`$select=[string]`(opcional) - uma lista de campos separados por vírgula tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9b031-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="9b031-851">Se não for especificado, todos os campos marcados como recuperáveis no esquema de saudação são incluídos.</span><span class="sxs-lookup"><span data-stu-id="9b031-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="9b031-852">Você pode solicitar explicitamente todos os campos ao definir esse parâmetro muito`*`.</span><span class="sxs-lookup"><span data-stu-id="9b031-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-853">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `select`, em vez de `$select`.</span><span class="sxs-lookup"><span data-stu-id="9b031-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="9b031-854">`facet=[string]`(zero ou mais) - toofacet um campo por.</span><span class="sxs-lookup"><span data-stu-id="9b031-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="9b031-855">Opcionalmente, cadeia de caracteres de saudação pode conter facetas de saudação toocustomize parâmetros expressada como separados por vírgula `name:value` pares.</span><span class="sxs-lookup"><span data-stu-id="9b031-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="9b031-856">Os parâmetros válidos são:</span><span class="sxs-lookup"><span data-stu-id="9b031-856">Valid parameters are:</span></span>

* <span data-ttu-id="9b031-857">`count` (número máximo de termos de faceta; o padrão é 10).</span><span class="sxs-lookup"><span data-stu-id="9b031-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="9b031-858">Não há nenhum máximo, mas os valores mais altos incorrem em uma penalidade de desempenho correspondente, especialmente se o campo Facetado Olá contiver um grande número de termos exclusivos.</span><span class="sxs-lookup"><span data-stu-id="9b031-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="9b031-859">Por exemplo: `facet=category,count:5` obtém Olá principais cinco categorias nos resultados da faceta.</span><span class="sxs-lookup"><span data-stu-id="9b031-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="9b031-860">**Observação**: se hello `count` parâmetro for menor que o número de saudação de termos exclusivos, Olá resultados podem não ser precisos.</span><span class="sxs-lookup"><span data-stu-id="9b031-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="9b031-861">Isso é devido a maneira toohello consultas de faceta são distribuídas em fragmentos.</span><span class="sxs-lookup"><span data-stu-id="9b031-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="9b031-862">Aumentar `count` geralmente aumenta Olá precisão Olá das contagens de termos, mas a um custo de desempenho.</span><span class="sxs-lookup"><span data-stu-id="9b031-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="9b031-863">`sort`(um dos `count` toosort *decrescente* por contagem, `-count` toosort *crescente* por contagem, `value` toosort *crescente* por valor, ou `-value` toosort *decrescente* por valor)</span><span class="sxs-lookup"><span data-stu-id="9b031-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="9b031-864">Por exemplo: `facet=category,count:3,sort:count` obtém Olá três categorias principais nos resultados da faceta em ordem decrescente pelo número de saudação de documentos com o nome de cada cidade.</span><span class="sxs-lookup"><span data-stu-id="9b031-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="9b031-865">Por exemplo, se três categorias de saudação principais forem orçamento, Motel e luxo e orçamento tiver 5 ocorrências, Motel tiver 6 e luxo tiver 4, em seguida, hello buckets será em ordem Olá Motel, orçamento, luxo.</span><span class="sxs-lookup"><span data-stu-id="9b031-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="9b031-866">Por exemplo: `facet=rating,sort:-value` produz todas as classificações possíveis, em ordem decrescente por valor.</span><span class="sxs-lookup"><span data-stu-id="9b031-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="9b031-867">Por exemplo, se as classificações de saudação são de 1 too5, Olá buckets são ordenados 5, 4, 3, 2, 1, independentemente de quantos documentos correspondem cada classificação.</span><span class="sxs-lookup"><span data-stu-id="9b031-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="9b031-868">`values` (valores numéricos delimitados por barras verticais ou valores `Edm.DateTimeOffset` que especificam um conjunto dinâmico de valores de entrada de faceta)</span><span class="sxs-lookup"><span data-stu-id="9b031-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="9b031-869">Por exemplo: `facet=baseRate,values:10|20` produz três buckets: um para a taxa de base 0 backup toobut não incluindo, 10, um para 10 backup toobut não incluindo, 20 e um para 20 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9b031-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="9b031-870">Por exemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produz duas classificações: uma para hotéis reformados antes de fevereiro de 2010 e outra para hotéis reformados em ou depois de 1º de fevereiro de 2010.</span><span class="sxs-lookup"><span data-stu-id="9b031-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="9b031-871">`interval` (intervalo inteiro maior que 0 para números ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para valores de tempo de data)</span><span class="sxs-lookup"><span data-stu-id="9b031-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="9b031-872">Por exemplo: `facet=baseRate,interval:100` produz classificações com base em intervalos de taxa de base de tamanho 100.</span><span class="sxs-lookup"><span data-stu-id="9b031-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="9b031-873">Por exemplo, se as taxas de base estiverem todas entre US$ 60 e US$ 600, haverá classificações para 0-100, 100-200, 200-300, 300-400, 400-500 e 500-600.</span><span class="sxs-lookup"><span data-stu-id="9b031-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="9b031-874">Por exemplo: `facet=lastRenovationDate,interval:year` produz uma classificação para cada ano em que os hotéis foram reformados.</span><span class="sxs-lookup"><span data-stu-id="9b031-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="9b031-875">`timeoffset` ([+-]hh:mm, [+-]hhmm ou [+-]hh) `timeoffset` é opcional.</span><span class="sxs-lookup"><span data-stu-id="9b031-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="9b031-876">Só podem ser combinada com hello `interval` opção e somente quando aplicada tooa campo do tipo `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="9b031-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="9b031-877">valor de saudação especifica tooaccount de deslocamento de hora Olá UTC na configuração de limites de tempo.</span><span class="sxs-lookup"><span data-stu-id="9b031-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="9b031-878">Por exemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa Olá limites de dia que inicia em UTC 01:00:00 (meia-noite no fuso horário Olá destino)</span><span class="sxs-lookup"><span data-stu-id="9b031-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="9b031-879">**Observação**: `count` e `sort` podem ser combinados em Olá mesma especificação de faceta, mas eles não podem ser combinados com `interval` ou `values`, e `interval` e `values` não podem ser combinados.</span><span class="sxs-lookup"><span data-stu-id="9b031-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="9b031-880">**Observação**: as facetas de intervalo de data e hora serão calculadas com base na hora UTC, caso `timeoffset` não seja especificado.</span><span class="sxs-lookup"><span data-stu-id="9b031-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="9b031-881">Por exemplo: para `facet=lastRenovationDate,interval:day`, limites de dia de saudação inicia às 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="9b031-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="9b031-882">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `facets`, em vez de `facet`.</span><span class="sxs-lookup"><span data-stu-id="9b031-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="9b031-883">Além disso, especifique-o como uma matriz JSON de cadeias de caracteres em que cada cadeia é uma expressão de faceta separada.</span><span class="sxs-lookup"><span data-stu-id="9b031-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="9b031-884">`$filter=[string]` (opcional) ‒ uma expressão de pesquisa estruturada na sintaxe de OData padrão.</span><span class="sxs-lookup"><span data-stu-id="9b031-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-885">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `filter`, em vez de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="9b031-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="9b031-886">`highlight=[string]` (opcional) ‒ realça um conjunto de nomes de campo separados por vírgulas usado para realçar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="9b031-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="9b031-887">Somente campos `searchable` podem ser usados para realçar ocorrências.</span><span class="sxs-lookup"><span data-stu-id="9b031-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="9b031-888">`highlightPreTag=[string]`(opcional, padrão é muito`<em>`) - uma cadeia de caracteres que precede toohit destaques.</span><span class="sxs-lookup"><span data-stu-id="9b031-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="9b031-889">Deve ser definida com `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="9b031-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-890">Ao chamar **pesquisa** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="9b031-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9b031-891">`highlightPostTag=[string]`(opcional, padrão é muito`</em>`)-uma marca de cadeia de caracteres que anexa toohit destaques.</span><span class="sxs-lookup"><span data-stu-id="9b031-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="9b031-892">Deve ser definida com `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="9b031-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-893">Ao chamar **pesquisa** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="9b031-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9b031-894">`scoringProfile=[string]`(opcional) - nome hello uma pontuação tooevaluate de perfil corresponde pontuações para documentos correspondentes nos resultados da ordem toosort hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="9b031-895">`scoringParameter=[string]`(zero ou mais) - indica valores hello para cada parâmetro definido em uma função de pontuação (por exemplo, `referencePointParameter`) usando o formato de saudação `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="9b031-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="9b031-896">Por exemplo, se o perfil de pontuação de saudação define uma função com um parâmetro chamado "mylocation" opção de cadeia de caracteres de consulta de saudação seria `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="9b031-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="9b031-897">traço primeiro Olá separa o nome de saudação da lista de valores hello, enquanto o traço segundo Olá faz parte do primeiro valor de saudação (longitude neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="9b031-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="9b031-898">Para parâmetros de pontuação, como marca de aumento que pode conter vírgulas, escape qualquer esses valores na lista de saudação usando aspas simples.</span><span class="sxs-lookup"><span data-stu-id="9b031-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="9b031-899">Se os próprios valores hello contiverem aspas, você pode reservá-los ao duplicar.</span><span class="sxs-lookup"><span data-stu-id="9b031-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="9b031-900">Por exemplo, se você tiver uma marca de aumento parâmetro chamado "mytag" e você desejar tooboost na marca de saudação valores "Olá, o ' Brien" e "Smith" consulta Olá opção de cadeia de caracteres seria `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="9b031-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="9b031-901">Observe que as aspas são necessárias apenas para os valores que contêm vírgulas.</span><span class="sxs-lookup"><span data-stu-id="9b031-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-902">Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `scoringParameters`, em vez de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="9b031-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="9b031-903">Além disso, especifique-o como uma matriz de cadeias de caracteres JSON, na qual cada cadeia é um par de nome `name-values` .</span><span class="sxs-lookup"><span data-stu-id="9b031-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="9b031-904">`minimumCoverage`(opcional, padrão é too100) - um número entre 0 e 100 que indica a porcentagem saudação do índice de saudação que deve ser abordada por uma consulta de pesquisa na ordem para Olá consulta toobe relatados como sucesso.</span><span class="sxs-lookup"><span data-stu-id="9b031-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="9b031-905">Por padrão, o índice inteiro Olá deve estar disponível ou `Search` retornará o código de status HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="9b031-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="9b031-906">Se você definir `minimumCoverage` e `Search` for bem-sucedida, ela retornará HTTP 200 e incluir um `@search.coverage` valor na resposta de saudação indicando a porcentagem de saudação do índice de saudação que foi incluído na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-907">Definir esse valor do parâmetro tooa menor que 100 pode ser útil para garantir a disponibilidade de pesquisa mesmo para os serviços com apenas uma réplica.</span><span class="sxs-lookup"><span data-stu-id="9b031-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="9b031-908">No entanto, nem todos os documentos correspondentes são garantia toobe presente nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="9b031-909">Se lembre-se de pesquisa é mais importante do aplicativo tooyour de disponibilidade, é melhor tooleave `minimumCoverage` com seu valor padrão de 100.</span><span class="sxs-lookup"><span data-stu-id="9b031-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="9b031-910">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-911">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-912">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-913">Observação: Para essa operação, Olá `api-version` é especificado como um parâmetro de consulta na URL de saudação independentemente se você chamar **pesquisa** com GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="9b031-914">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-914">**Request Headers**</span></span>

<span data-ttu-id="9b031-915">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-916">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-917">É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9b031-918">Olá **pesquisa** solicitação pode especificar uma chave de administração ou a chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9b031-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="9b031-919">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-920">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-921">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-922">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-922">**Request Body**</span></span>

<span data-ttu-id="9b031-923">Para GET: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="9b031-923">For GET: None.</span></span>

<span data-ttu-id="9b031-924">Para POST:</span><span class="sxs-lookup"><span data-stu-id="9b031-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
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

<span data-ttu-id="9b031-925">**Continuação de respostas de pesquisa parciais**</span><span class="sxs-lookup"><span data-stu-id="9b031-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="9b031-926">Às vezes, pesquisa do Azure não pode retornar que todos os Olá solicitada resulta em uma única resposta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="9b031-927">Isso pode ocorrer por diferentes motivos, por exemplo, quando a consulta Olá solicita muitos documentos não especificando `$top` ou especificando um valor para `$top` que é muito grande.</span><span class="sxs-lookup"><span data-stu-id="9b031-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="9b031-928">Nesses casos, a pesquisa do Azure incluirá Olá `@odata.nextLink` anotação no corpo de resposta Olá e também `@search.nextPageParameters` se fosse uma solicitação POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="9b031-929">Você pode usar valores de saudação do tooformulate anotações outra pesquisa solicitação tooget Olá próxima parte da resposta da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="9b031-930">Isso é chamado de um ***continuação*** de solicitação de pesquisa original hello e hello anotações são geralmente chamadas ***tokens de acompanhamento***.</span><span class="sxs-lookup"><span data-stu-id="9b031-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="9b031-931">Consulte [exemplo hello abaixo](#SearchResponse) para obter detalhes sobre a sintaxe de saudação dessas anotações e onde eles aparecem no corpo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="9b031-932">os motivos Olá porque a pesquisa do Azure pode retornar tokens de acompanhamento são toochange específicos de implementação e o assunto.</span><span class="sxs-lookup"><span data-stu-id="9b031-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="9b031-933">Clientes robustos devem sempre ser toohandle pronto casos em que são retornados documentos menos que o esperado e um token de continuação é incluído toocontinue recuperar documentos.</span><span class="sxs-lookup"><span data-stu-id="9b031-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="9b031-934">Também Observe que você deve usar Olá mesmo método HTTP a solicitação original Olá em ordem toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9b031-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="9b031-935">Por exemplo, se você tiver enviado uma solicitação GET, quaisquer solicitações de continuação que você enviar também deverão usar GET (e da mesma forma para POST).</span><span class="sxs-lookup"><span data-stu-id="9b031-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="9b031-936"><a name="SearchResponse"></a>
**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="9b031-937">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
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
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
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
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="9b031-938">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="9b031-938">**Examples:**</span></span>

<span data-ttu-id="9b031-939">Você pode encontrar exemplos adicionais no hello [sintaxe de expressão do OData para pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="9b031-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="9b031-940">Saudação de pesquisa índice classificado em ordem decrescente por data.</span><span class="sxs-lookup"><span data-stu-id="9b031-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="9b031-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="9b031-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="9b031-943">Em uma pesquisa de faceta, pesquise o índice de saudação e recupere facetas para categorias, classificação, marcas, bem como os itens com baseRate em intervalos específicos:</span><span class="sxs-lookup"><span data-stu-id="9b031-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="9b031-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="9b031-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="9b031-946">Usando um filtro, limitar resultados de consulta de faceta anterior Olá depois Olá usuário clica em classificação 3 e a categoria "Motel":</span><span class="sxs-lookup"><span data-stu-id="9b031-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="9b031-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="9b031-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="9b031-949">Em uma pesquisa facetada, definir um limite superior para termos exclusivos retornados em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="9b031-950">saudação padrão é 10, mas você pode aumentar ou diminuir esse valor usando Olá `count` parâmetro hello `facet` atributo:</span><span class="sxs-lookup"><span data-stu-id="9b031-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="9b031-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="9b031-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="9b031-953">Saudação de pesquisa índice de campos específicos; Por exemplo, um campo específico do idioma:</span><span class="sxs-lookup"><span data-stu-id="9b031-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="9b031-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="9b031-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="9b031-956">Saudação de índice em vários campos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="9b031-957">Por exemplo, você pode armazenar e Olá de campos de pesquisa de consulta em vários idiomas, tudo isso no mesmo índice.</span><span class="sxs-lookup"><span data-stu-id="9b031-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="9b031-958">Se as descrições de inglês e francês coexistam em Olá mesmo documento, você pode retornar hello em qualquer ou todos os resultados da consulta:</span><span class="sxs-lookup"><span data-stu-id="9b031-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="9b031-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="9b031-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="9b031-961">Observe que você pode consultar apenas um índice por vez.</span><span class="sxs-lookup"><span data-stu-id="9b031-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="9b031-962">Não crie vários índices para cada idioma, a menos que você planejar tooquery um por vez.</span><span class="sxs-lookup"><span data-stu-id="9b031-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="9b031-963">Paginação – obter Olá 1ª página de itens (o tamanho da página é 10):</span><span class="sxs-lookup"><span data-stu-id="9b031-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="9b031-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="9b031-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="9b031-966">Paginação – página de 2º Get hello de itens (o tamanho da página é 10):</span><span class="sxs-lookup"><span data-stu-id="9b031-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="9b031-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="9b031-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="9b031-969">Recuperar um conjunto específico de campos:</span><span class="sxs-lookup"><span data-stu-id="9b031-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="9b031-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="9b031-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="9b031-972">Recupere documentos que correspondem a uma expressão de filtro específica:</span><span class="sxs-lookup"><span data-stu-id="9b031-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="9b031-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="9b031-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="9b031-975">Pesquise o índice de saudação e retorne fragmentos com realces de ocorrências</span><span class="sxs-lookup"><span data-stu-id="9b031-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="9b031-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="9b031-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="9b031-978">Pesquise o índice de saudação e retorne documentos classificados do toofarther mais próximo para fora do local de referência</span><span class="sxs-lookup"><span data-stu-id="9b031-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="9b031-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="9b031-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="9b031-981">Pesquisa Olá índice supondo que não há é um perfil de pontuação chamado "geo" com duas funções de pontuação de distância, uma definição de um parâmetro chamada "currentLocation" e uma definição de um parâmetro chamado "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="9b031-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="9b031-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="9b031-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="9b031-984">Localizar documentos no índice de saudação usando [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="9b031-985">Esta consulta retorna hotéis onde os campos de pesquisa contêm Olá termos "conforto" e "local", mas não "motel":</span><span class="sxs-lookup"><span data-stu-id="9b031-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="9b031-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="9b031-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="9b031-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="9b031-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="9b031-988">Observe o uso de saudação do `searchMode=all` acima.</span><span class="sxs-lookup"><span data-stu-id="9b031-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="9b031-989">Incluindo esse parâmetro substitui o padrão de saudação do `searchMode=any`, garantindo que `-motel` significa "AND NOT" em vez de "OR NOT".</span><span class="sxs-lookup"><span data-stu-id="9b031-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="9b031-990">Sem `searchMode=all`, você obtém "OR NOT" que expande em vez de restringir os resultados da pesquisa, e isso pode ser contrário à intuição toosome usuários.</span><span class="sxs-lookup"><span data-stu-id="9b031-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="9b031-991">Localizar documentos no índice de saudação usando [sintaxe de consulta do lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b031-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="9b031-992">Essa consulta retorna hotéis onde o campo de categoria de saudação contém termo hello "budget" e campos de pesquisa todos os que contêm a frase hello "recentemente renovado".</span><span class="sxs-lookup"><span data-stu-id="9b031-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="9b031-993">Documentos que contêm a frase hello "recentemente renovado" são com classificação mais alta como resultado do valor de aumento de termo hello (3)</span><span class="sxs-lookup"><span data-stu-id="9b031-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="9b031-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="9b031-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="9b031-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="9b031-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="9b031-996">Procurar documento</span><span class="sxs-lookup"><span data-stu-id="9b031-996">Lookup Document</span></span>
<span data-ttu-id="9b031-997">Olá **pesquisar documento** operação recupera um documento da pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="9b031-998">Isso é útil quando um usuário clica em um resultado de pesquisa específico e desejar toolook detalhes específicos sobre esse documento.</span><span class="sxs-lookup"><span data-stu-id="9b031-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="9b031-999">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-999">**Request**</span></span>

<span data-ttu-id="9b031-1000">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="9b031-1001">Olá **pesquisar documento** solicitação pode ser construída da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="9b031-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="9b031-1002">Como alternativa, você pode usar a sintaxe tradicional do OData Olá para pesquisa de chave:</span><span class="sxs-lookup"><span data-stu-id="9b031-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="9b031-1003">Olá URI da solicitação inclui um [nome do índice] e [chave], especificando quais tooretrieve documento de índice que.</span><span class="sxs-lookup"><span data-stu-id="9b031-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="9b031-1004">Você pode obter apenas um documento por vez.</span><span class="sxs-lookup"><span data-stu-id="9b031-1004">You can only get one document at a time.</span></span> <span data-ttu-id="9b031-1005">Use **pesquisa** tooget vários documentos em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="9b031-1006">**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="9b031-1006">**Query Parameters**</span></span>

<span data-ttu-id="9b031-1007">`$select=[string]`(opcional) - uma lista de campos separados por vírgula tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9b031-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="9b031-1008">Se não for especificado ou definido muito`*`, todos os campos marcados como recuperáveis no esquema de saudação são incluídos na projeção de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="9b031-1009">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-1010">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-1011">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-1012">Observação: Para essa operação, Olá `api-version` é especificado como um parâmetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="9b031-1013">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1013">**Request Headers**</span></span>

<span data-ttu-id="9b031-1014">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-1015">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-1016">É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9b031-1017">Olá **pesquisar documento** solicitação pode especificar uma chave de administração ou a chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="9b031-1018">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-1019">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-1020">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-1021">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1021">**Request Body**</span></span>

<span data-ttu-id="9b031-1022">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="9b031-1022">None.</span></span>

<span data-ttu-id="9b031-1023">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-1023">**Response**</span></span>

<span data-ttu-id="9b031-1024">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="9b031-1025">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="9b031-1025">**Example**</span></span>

<span data-ttu-id="9b031-1026">Pesquisar documento hello que tem a chave '2'</span><span class="sxs-lookup"><span data-stu-id="9b031-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="9b031-1027">Pesquisar documento hello que tem a chave '3' usando a sintaxe do OData:</span><span class="sxs-lookup"><span data-stu-id="9b031-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="9b031-1028">Contar documentos</span><span class="sxs-lookup"><span data-stu-id="9b031-1028">Count Documents</span></span>
<span data-ttu-id="9b031-1029">Olá **contar documentos** operação recupera uma contagem do número de saudação de documentos em um índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="9b031-1030">Olá `$count` sintaxe é parte da saudação protocolo OData.</span><span class="sxs-lookup"><span data-stu-id="9b031-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="9b031-1031">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1031">**Request**</span></span>

<span data-ttu-id="9b031-1032">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="9b031-1033">Olá **contar documentos** solicitação pode ser criada usando o método GET hello.</span><span class="sxs-lookup"><span data-stu-id="9b031-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="9b031-1034">Olá [nome do índice] no URI de solicitação Olá informa Olá serviço tooreturn uma contagem de todos os itens na coleção de documentos de saudação do índice especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="9b031-1035">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-1036">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-1037">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-1038">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1038">**Request Headers**</span></span>

<span data-ttu-id="9b031-1039">Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="9b031-1040">`Accept`: Esse valor deve ser definido muito`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="9b031-1041">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-1042">É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9b031-1043">Olá **contar documentos** solicitação pode especificar uma chave de administração ou a chave de consulta para `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="9b031-1044">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-1045">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-1046">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-1047">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1047">**Request Body**</span></span>

<span data-ttu-id="9b031-1048">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="9b031-1048">None.</span></span>

<span data-ttu-id="9b031-1049">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-1049">**Response**</span></span>

<span data-ttu-id="9b031-1050">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="9b031-1051">corpo da resposta Olá contém o valor de contagem de saudação como um inteiro em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="9b031-1052">Sugestões</span><span class="sxs-lookup"><span data-stu-id="9b031-1052">Suggestions</span></span>
<span data-ttu-id="9b031-1053">Olá **sugestões** operação recupera as sugestões com base na entrada de pesquisa parcial.</span><span class="sxs-lookup"><span data-stu-id="9b031-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="9b031-1054">Ela é normalmente usada em sugestões de preenchimento automático pesquisa caixas tooprovide como os usuários inserem termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="9b031-1055">Solicitações de sugestões focalizam a sugestão de documentos de destino, para que Olá sugerido de texto pode ser repetido se vários documentos de candidato correspondem Olá mesmo entrada de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="9b031-1056">Você pode usar `$select` tooretrieve outros documentos campos (incluindo a chave de documento hello) para que você possa determinar qual documento é a fonte Olá para cada sugestão.</span><span class="sxs-lookup"><span data-stu-id="9b031-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="9b031-1057">Uma operação **Suggestions** é emitida como uma solicitação GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="9b031-1058">**Quando toouse POST em vez de obter**</span><span class="sxs-lookup"><span data-stu-id="9b031-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="9b031-1059">Quando você usa o HTTP GET toocall Olá **sugestões** API, você precisa toobe ciente de que o comprimento Olá Olá URL da solicitação não pode exceder 8 KB.</span><span class="sxs-lookup"><span data-stu-id="9b031-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="9b031-1060">Isso costuma ser suficiente para a maioria dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9b031-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="9b031-1061">No entanto, alguns aplicativos geram consultas muito grandes, especificamente expressões de filtro OData.</span><span class="sxs-lookup"><span data-stu-id="9b031-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="9b031-1062">Para esses aplicativos, usar HTTP POST é uma opção melhor, pois permite filtros maiores que o GET.</span><span class="sxs-lookup"><span data-stu-id="9b031-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="9b031-1063">Com o POST, Olá número cláusulas em um filtro é fator limitante hello, Olá não tamanho da cadeia de caracteres de filtro bruto Olá desde que o limite de tamanho de solicitação de saudação do POST é aproximadamente 16 MB.</span><span class="sxs-lookup"><span data-stu-id="9b031-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1064">Mesmo que o limite de tamanho de solicitação POST Olá for muito grande, as expressões de filtro não podem ser arbitrariamente complexas.</span><span class="sxs-lookup"><span data-stu-id="9b031-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="9b031-1065">Confira [Sintaxe de expressão OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de filtro.</span><span class="sxs-lookup"><span data-stu-id="9b031-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="9b031-1066">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1066">**Request**</span></span>

<span data-ttu-id="9b031-1067">HTTPS é necessário para as solicitações de serviço.</span><span class="sxs-lookup"><span data-stu-id="9b031-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="9b031-1068">Olá **sugestões** solicitação pode ser criada usando Olá GET ou métodos POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="9b031-1069">URI de solicitação de saudação especifica o nome de saudação do hello índice tooquery.</span><span class="sxs-lookup"><span data-stu-id="9b031-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="9b031-1070">Parâmetros, como o termo de pesquisa de entrada parcial hello, são especificados na cadeia de caracteres de consulta de saudação no caso de saudação de solicitações GET e na solicitação Olá solicitações de corpo no caso de saudação de POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="9b031-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="9b031-1071">Como uma prática recomendada, ao criar solicitações GET, lembre-se muito[a codificação de URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parâmetros ao chamar hello API REST diretamente.</span><span class="sxs-lookup"><span data-stu-id="9b031-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="9b031-1072">Para as operações **Sugestões** , isso inclui:</span><span class="sxs-lookup"><span data-stu-id="9b031-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="9b031-1073">Codificação de URL é recomendada apenas nos Olá acima parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="9b031-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="9b031-1074">Se você inadvertidamente a codificação de URL hello cadeia de caracteres de consulta inteira (tudo após Olá?), as solicitações são interrompidas.</span><span class="sxs-lookup"><span data-stu-id="9b031-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="9b031-1075">Além disso, a codificação de URL só é necessária ao chamar hello API REST diretamente usando obter.</span><span class="sxs-lookup"><span data-stu-id="9b031-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="9b031-1076">Nenhuma codificação de URL é necessária ao chamar **sugestões** usando POST, ou ao usar o hello [biblioteca cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que trata de codificação de URL para você.</span><span class="sxs-lookup"><span data-stu-id="9b031-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="9b031-1077">**Parâmetros de consulta**</span><span class="sxs-lookup"><span data-stu-id="9b031-1077">**Query Parameters**</span></span>

<span data-ttu-id="9b031-1078">**Suggestions** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="9b031-1079">Você fornecer esses parâmetros na URL Olá cadeia de caracteres de consulta ao chamar **sugestões** por meio de GET e como propriedades JSON no corpo da solicitação Olá ao chamar **sugestões** por meio de POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="9b031-1080">sintaxe de saudação para alguns parâmetros é ligeiramente diferente entre GET e POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="9b031-1081">Essas diferenças são indicadas, como aplicável, abaixo:</span><span class="sxs-lookup"><span data-stu-id="9b031-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="9b031-1082">`search=[string]`-Olá consultas de pesquisa de texto toouse toosuggest.</span><span class="sxs-lookup"><span data-stu-id="9b031-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="9b031-1083">Deve ter pelo menos 1 e não mais que 100 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9b031-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="9b031-1084">`highlightPreTag=[string]`(opcional) - uma marca de cadeia de caracteres que precede toosearch ocorrências.</span><span class="sxs-lookup"><span data-stu-id="9b031-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="9b031-1085">Deve ser definida com `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1086">Ao chamar **sugestões** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="9b031-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9b031-1087">`highlightPostTag=[string]`(opcional) - uma marca de cadeia de caracteres que anexa toosearch ocorrências.</span><span class="sxs-lookup"><span data-stu-id="9b031-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="9b031-1088">Deve ser definida com `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1089">Ao chamar **sugestões** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).</span><span class="sxs-lookup"><span data-stu-id="9b031-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="9b031-1090">`suggesterName=[string]`-nome de saudação da sugestão, Olá conforme especificado no hello `suggesters` coleção que faz parte da definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="9b031-1091">Um `suggester` determina quais campos são examinados em busca de termos de consulta sugeridos.</span><span class="sxs-lookup"><span data-stu-id="9b031-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="9b031-1092">Consulte [Sugestores](#Suggesters) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9b031-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="9b031-1093">`fuzzy=[boolean]`(opcional, padrão = false)-quando definido tootrue essa API encontrará sugestões mesmo se houver um caractere ausente ou substituído no texto de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="9b031-1094">Embora isso proporcione uma experiência melhor em alguns cenários, prejudica o desempenho, pois pesquisas com sugestões difusas são mais lentas e consumem mais recursos.</span><span class="sxs-lookup"><span data-stu-id="9b031-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="9b031-1095">`searchFields=[string]`(opcional) - lista de saudação do toosearch de nomes de campos separados por vírgulas para hello especificada texto de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="9b031-1096">Os campos de destino devem ser habilitados para sugestões.</span><span class="sxs-lookup"><span data-stu-id="9b031-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="9b031-1097">`$top=#`(opcional, padrão = 5)-Olá número de sugestões tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9b031-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="9b031-1098">Deve ser um número entre 1 e 100.</span><span class="sxs-lookup"><span data-stu-id="9b031-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1099">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `top` em vez de `$top`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="9b031-1100">`$filter=[string]`(opcional) - uma expressão que filtra os documentos Olá considerados para obter sugestões.</span><span class="sxs-lookup"><span data-stu-id="9b031-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1101">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `filter` em vez de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="9b031-1102">`$orderby=[string]`(opcional) - uma lista de expressões separadas por vírgulas toosort Olá resultados por.</span><span class="sxs-lookup"><span data-stu-id="9b031-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="9b031-1103">Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função.</span><span class="sxs-lookup"><span data-stu-id="9b031-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="9b031-1104">Cada expressão pode ser seguido por `asc` tooindicated em ordem crescente e `desc` tooindicate em ordem decrescente.</span><span class="sxs-lookup"><span data-stu-id="9b031-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="9b031-1105">saudação padrão é a ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="9b031-1105">hello default is ascending order.</span></span> <span data-ttu-id="9b031-1106">Há um limite de 32 cláusulas para `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1107">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `orderby` em vez de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="9b031-1108">`$select=[string]`(opcional) - uma lista de campos separados por vírgula tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="9b031-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="9b031-1109">Se não for especificado, Olá apenas a chave de documento e texto de sugestão é retornado.</span><span class="sxs-lookup"><span data-stu-id="9b031-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="9b031-1110">Você pode solicitar explicitamente todos os campos ao definir esse parâmetro muito`*`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1111">Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `select` em vez de `$select`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="9b031-1112">`minimumCoverage`(opcional, padrão é too80) - um número entre 0 e 100 que indica a porcentagem saudação do índice de saudação que deve ser abordada por uma consulta de sugestões na ordem para Olá consulta toobe relatados como sucesso.</span><span class="sxs-lookup"><span data-stu-id="9b031-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="9b031-1113">Por padrão, pelo menos 80% do índice Olá deve estar disponível ou `Suggest` retornará o código de status HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="9b031-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="9b031-1114">Se você definir `minimumCoverage` e `Suggest` for bem-sucedida, ela retornará HTTP 200 e incluir um `@search.coverage` valor na resposta de saudação indicando a porcentagem de saudação do índice de saudação que foi incluído na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="9b031-1115">Definir esse valor do parâmetro tooa menor que 100 pode ser útil para garantir a disponibilidade de pesquisa mesmo para os serviços com apenas uma réplica.</span><span class="sxs-lookup"><span data-stu-id="9b031-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="9b031-1116">No entanto, nem todas as sugestões de correspondência são garantidas toobe presente nos resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b031-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="9b031-1117">Se a recuperação é mais importante do aplicativo tooyour de disponibilidade, é melhor não toolower `minimumCoverage` abaixo de seu valor padrão 80.</span><span class="sxs-lookup"><span data-stu-id="9b031-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="9b031-1118">`api-version=[string]` (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="9b031-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="9b031-1119">versão de visualização de saudação é `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="9b031-1120">Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.</span><span class="sxs-lookup"><span data-stu-id="9b031-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="9b031-1121">Observação: Para essa operação, Olá `api-version` é especificado como um parâmetro de consulta na URL de saudação independentemente se você chamar **sugestões** com GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="9b031-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="9b031-1122">**Cabeçalhos da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1122">**Request Headers**</span></span>

<span data-ttu-id="9b031-1123">Olá lista a seguir descreve hello necessárias e cabeçalhos de solicitação opcional</span><span class="sxs-lookup"><span data-stu-id="9b031-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="9b031-1124">`api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9b031-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="9b031-1125">É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9b031-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="9b031-1126">Olá **sugestões** solicitação pode especificar uma chave de administração ou a chave de consulta como Olá `api-key`.</span><span class="sxs-lookup"><span data-stu-id="9b031-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="9b031-1127">Você também precisará Olá serviço nome tooconstruct Olá solicitação URL.</span><span class="sxs-lookup"><span data-stu-id="9b031-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="9b031-1128">Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b031-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="9b031-1129">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.</span><span class="sxs-lookup"><span data-stu-id="9b031-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="9b031-1130">**Corpo da solicitação**</span><span class="sxs-lookup"><span data-stu-id="9b031-1130">**Request Body**</span></span>

<span data-ttu-id="9b031-1131">Para GET: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="9b031-1131">For GET: None.</span></span>

<span data-ttu-id="9b031-1132">Para POST:</span><span class="sxs-lookup"><span data-stu-id="9b031-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="9b031-1133">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="9b031-1133">**Response**</span></span>

<span data-ttu-id="9b031-1134">Código de status: 200 OK é retornado para uma resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9b031-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="9b031-1135">Se a opção de projeção Olá for tooretrieve usados campos que estão incluídos em cada elemento da matriz de saudação:</span><span class="sxs-lookup"><span data-stu-id="9b031-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="9b031-1136">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="9b031-1136">**Example**</span></span>

<span data-ttu-id="9b031-1137">Recupere 5 sugestões, onde a entrada de pesquisa parcial Olá é "lux"</span><span class="sxs-lookup"><span data-stu-id="9b031-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
