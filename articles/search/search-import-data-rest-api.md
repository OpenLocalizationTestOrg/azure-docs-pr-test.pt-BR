---
title: AAA "carregar dados (API REST - pesquisa do Azure) | Microsoft Docs"
description: "Saiba como o índice de tooan tooupload dados na pesquisa do Azure usando Olá API REST."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="727cc-103">Carregar dados tooAzure pesquisa usando Olá API REST</span><span class="sxs-lookup"><span data-stu-id="727cc-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="727cc-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="727cc-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="727cc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="727cc-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="727cc-106">REST</span><span class="sxs-lookup"><span data-stu-id="727cc-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="727cc-107">Este artigo mostra como Olá toouse [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport dados em um índice de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="727cc-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="727cc-108">Antes de começar este passo a passo, você já deve ter [criado um índice de Pesquisa do Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="727cc-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="727cc-109">Em documentos de toopush ordem pra o índice usando a API REST do hello, emitirá o ponto de extremidade de URL de um HTTP POST solicitação tooyour índice.</span><span class="sxs-lookup"><span data-stu-id="727cc-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="727cc-110">corpo de saudação do hello solicitação HTTP corpo é um objeto JSON que contém documentos Olá toobe adicionada, modificada ou excluída.</span><span class="sxs-lookup"><span data-stu-id="727cc-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="727cc-111">Identificar a api-key do administrador de seu serviço do Azure Search</span><span class="sxs-lookup"><span data-stu-id="727cc-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="727cc-112">Ao emitir solicitações HTTP em seu serviço usando Olá API REST, *cada* solicitação de API deve incluir Olá api-chave que foi gerada para Olá Você provisionou do serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="727cc-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="727cc-113">Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.</span><span class="sxs-lookup"><span data-stu-id="727cc-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="727cc-114">toofind chaves de api do serviço, você pode entrar no toohello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="727cc-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="727cc-115">Vá folha do serviço de pesquisa do Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="727cc-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="727cc-116">Clique em Olá ícone "Chaves"</span><span class="sxs-lookup"><span data-stu-id="727cc-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="727cc-117">O serviço terá *chaves de administração* e *chaves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="727cc-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="727cc-118">O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="727cc-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="727cc-119">Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="727cc-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="727cc-120">O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="727cc-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="727cc-121">Para fins de saudação da importação de dados para um índice, você pode usar a chave primária ou secundária de administração.</span><span class="sxs-lookup"><span data-stu-id="727cc-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="727cc-122">Decidir quais indexação toouse de ação</span><span class="sxs-lookup"><span data-stu-id="727cc-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="727cc-123">Ao usar o hello API REST, você emitir solicitações HTTP POST com URL de ponto de extremidade do índice de pesquisa do Azure tooyour corpos JSON solicitação.</span><span class="sxs-lookup"><span data-stu-id="727cc-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="727cc-124">objeto do Hello JSON no corpo da solicitação HTTP conterá uma matriz JSON denominado "valor", que contém objetos JSON que representa os documentos que você gostaria que tooadd tooyour índice, atualizar ou excluir.</span><span class="sxs-lookup"><span data-stu-id="727cc-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="727cc-125">Cada objeto JSON na matriz de "valor" hello representa um toobe documento indexado.</span><span class="sxs-lookup"><span data-stu-id="727cc-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="727cc-126">Cada um desses objetos contém a chave do documento hello e especifica a ação de indexação Olá desejado (carregar, mesclar, excluir, etc.).</span><span class="sxs-lookup"><span data-stu-id="727cc-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="727cc-127">Dependendo de qual dos Olá ações que você escolher abaixo, somente determinados campos devem ser incluídos para cada documento:</span><span class="sxs-lookup"><span data-stu-id="727cc-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="727cc-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="727cc-128">Description</span></span> | <span data-ttu-id="727cc-129">Campos necessários para cada documento</span><span class="sxs-lookup"><span data-stu-id="727cc-129">Necessary fields for each document</span></span> | <span data-ttu-id="727cc-130">Observações</span><span class="sxs-lookup"><span data-stu-id="727cc-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="727cc-131">Um `upload` ação é similar tooan "upsert" onde documento hello será inserido se for novo e atualizado/substituído se ele existir.</span><span class="sxs-lookup"><span data-stu-id="727cc-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="727cc-132">chave, além de quaisquer outros campos que você deseja toodefine</span><span class="sxs-lookup"><span data-stu-id="727cc-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="727cc-133">Ao atualizar/substituir um documento existente, qualquer campo que não está especificado na solicitação de saudação terá seu campo definido muito`null`.</span><span class="sxs-lookup"><span data-stu-id="727cc-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="727cc-134">Isso ocorre mesmo quando o campo Olá tiver sido definido anteriormente tooa valor de não-nulo.</span><span class="sxs-lookup"><span data-stu-id="727cc-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="727cc-135">Atualizações de uma existente de documento com hello especificado campos.</span><span class="sxs-lookup"><span data-stu-id="727cc-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="727cc-136">Se o documento de saudação não existe no índice hello, mesclagem Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="727cc-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="727cc-137">chave, além de quaisquer outros campos que você deseja toodefine</span><span class="sxs-lookup"><span data-stu-id="727cc-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="727cc-138">Qualquer campo que você especificar em uma mesclagem substituirá o campo de saudação existente no documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="727cc-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="727cc-139">Isso inclui campos do tipo `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="727cc-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="727cc-140">Por exemplo, se hello documento contém um campo `tags` com valor `["budget"]` e executar uma mesclagem com valor `["economy", "pool"]` para `tags`, Olá valor final do hello `tags` campo será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="727cc-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="727cc-141">Ele não será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="727cc-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="727cc-142">Esta ação se comporta como `merge` se um documento com hello atribuída a chave já existe no índice hello.</span><span class="sxs-lookup"><span data-stu-id="727cc-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="727cc-143">Se o documento de saudação não existir, ele se comporta como `upload` com um novo documento.</span><span class="sxs-lookup"><span data-stu-id="727cc-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="727cc-144">chave, além de quaisquer outros campos que você deseja toodefine</span><span class="sxs-lookup"><span data-stu-id="727cc-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="727cc-145">Remove o documento especificado Olá do índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="727cc-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="727cc-146">somente chave</span><span class="sxs-lookup"><span data-stu-id="727cc-146">key only</span></span> |<span data-ttu-id="727cc-147">Todos os campos que você especificar que o campo de chave hello será ignorado.</span><span class="sxs-lookup"><span data-stu-id="727cc-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="727cc-148">Se você quiser tooremove um campo individual de um documento, use `merge` em vez disso e basta definir campo Olá explicitamente toonull.</span><span class="sxs-lookup"><span data-stu-id="727cc-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="727cc-149">Construir sua solicitação HTTP e o corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="727cc-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="727cc-150">Agora que você coletou valores de campo necessário Olá para suas ações de índice, são solicitação HTTP tooconstruct pronto Olá real e solicitação de JSON corpo tooimport seus dados.</span><span class="sxs-lookup"><span data-stu-id="727cc-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="727cc-151">Solicitação e cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="727cc-151">Request and Request Headers</span></span>
<span data-ttu-id="727cc-152">Saudação de URL, você precisará tooprovide seu nome de serviço, nome do índice ("hotéis" neste caso), bem como versão de API apropriada hello (Olá atual versão da API é `2016-09-01` em tempo de saudação da publicação neste documento).</span><span class="sxs-lookup"><span data-stu-id="727cc-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="727cc-153">Você precisará Olá toodefine `Content-Type` e `api-key` cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="727cc-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="727cc-154">Para Olá último, use uma das chaves de administração do serviço.</span><span class="sxs-lookup"><span data-stu-id="727cc-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="727cc-155">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="727cc-155">Request Body</span></span>
```JSON
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
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="727cc-156">Nesse caso, estamos usando `upload`, `mergeOrUpload` e `delete` como nossas ações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="727cc-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="727cc-157">Suponha que o índice de exemplo "hotels" já esteja preenchido com vários documentos.</span><span class="sxs-lookup"><span data-stu-id="727cc-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="727cc-158">Observe como não tínhamos toospecify todos os campos de documento possíveis Olá ao usar `mergeOrUpload` e como podemos só especificado de chave de documento hello (`hotelId`) ao usar `delete`.</span><span class="sxs-lookup"><span data-stu-id="727cc-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="727cc-159">Além disso, observe que você só pode incluir documentos too1000 (ou 16 MB) em uma única solicitação de indexação.</span><span class="sxs-lookup"><span data-stu-id="727cc-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="727cc-160">Compreender o código de resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="727cc-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="727cc-161">200</span><span class="sxs-lookup"><span data-stu-id="727cc-161">200</span></span>
<span data-ttu-id="727cc-162">Após enviar uma solicitação de indexação bem-sucedida, você receberá uma resposta HTTP com o código de status `200 OK`.</span><span class="sxs-lookup"><span data-stu-id="727cc-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="727cc-163">Olá corpo JSON do hello resposta HTTP será da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="727cc-163">hello JSON body of hello HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="727cc-164">207</span><span class="sxs-lookup"><span data-stu-id="727cc-164">207</span></span>
<span data-ttu-id="727cc-165">Um código de status `207` será retornado quando pelo menos um item não tiver sido indexado com êxito.</span><span class="sxs-lookup"><span data-stu-id="727cc-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="727cc-166">Olá corpo JSON de resposta HTTP de saudação conterá informações sobre documentos malsucedida hello.</span><span class="sxs-lookup"><span data-stu-id="727cc-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="727cc-167">Isso geralmente significa que a carga Olá na sua pesquisa de serviço é atingir um ponto em que solicitações de indexação começarão tooreturn `503` respostas.</span><span class="sxs-lookup"><span data-stu-id="727cc-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="727cc-168">Nesse caso, é altamente recomendável que o código do cliente faça uma pausa e aguarde antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="727cc-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="727cc-169">Isso dará sistema Olá toorecover algum tempo, aumentar as chances de saudação que as solicitações futuras serão bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="727cc-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="727cc-170">Repetir rapidamente suas solicitações só prolongará a situação de saudação.</span><span class="sxs-lookup"><span data-stu-id="727cc-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="727cc-171">429</span><span class="sxs-lookup"><span data-stu-id="727cc-171">429</span></span>
<span data-ttu-id="727cc-172">Um código de status `429` serão retornados quando você excedeu sua cota no número de saudação de documentos por índice.</span><span class="sxs-lookup"><span data-stu-id="727cc-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="727cc-173">503</span><span class="sxs-lookup"><span data-stu-id="727cc-173">503</span></span>
<span data-ttu-id="727cc-174">Um código de status `503` será retornado se nenhum dos itens de saudação na solicitação Olá foram indexados com êxito.</span><span class="sxs-lookup"><span data-stu-id="727cc-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="727cc-175">Esse erro significa que o sistema hello está sob carga pesada e sua solicitação não pode ser processada neste momento.</span><span class="sxs-lookup"><span data-stu-id="727cc-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="727cc-176">Nesse caso, é altamente recomendável que o código do cliente faça uma pausa e aguarde antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="727cc-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="727cc-177">Isso dará sistema Olá toorecover algum tempo, aumentar as chances de saudação que as solicitações futuras serão bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="727cc-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="727cc-178">Repetir rapidamente suas solicitações só prolongará a situação de saudação.</span><span class="sxs-lookup"><span data-stu-id="727cc-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="727cc-179">Para obter mais informações sobre as ações do documento e as respostas de êxito/erro, consulte [Adicionar, Atualizar ou Excluir Documentos](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="727cc-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="727cc-180">Para obter mais informações sobre outros códigos de status HTTP que podem ser retornados em caso de falha, confira [Códigos de status HTTP (Pesquisa do Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="727cc-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="727cc-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="727cc-181">Next steps</span></span>
<span data-ttu-id="727cc-182">Depois de preencher o índice de pesquisa do Azure, você será toostart pronto emitir consultas toosearch para documentos.</span><span class="sxs-lookup"><span data-stu-id="727cc-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="727cc-183">Veja [Consultar seu Índice de Pesquisa do Azure](search-query-overview.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="727cc-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
