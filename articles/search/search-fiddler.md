---
title: aaaHow toouse Fiddler tooevaluate e testar as APIs de REST de pesquisa do Azure | Microsoft Docs
description: "Use o Fiddler para uma disponibilidade de pesquisa do Azure tooverifying abordagem sem código e experimentar Olá APIs REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="4c30a-103">Usar o Fiddler tooevaluate e testar as APIs de REST de pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="4c30a-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="4c30a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4c30a-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="4c30a-105">Gerenciador de Pesquisa</span><span class="sxs-lookup"><span data-stu-id="4c30a-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="4c30a-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="4c30a-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="4c30a-107">.NET</span><span class="sxs-lookup"><span data-stu-id="4c30a-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="4c30a-108">REST</span><span class="sxs-lookup"><span data-stu-id="4c30a-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="4c30a-109">Este artigo explica como toouse Fiddler, disponível como um [download gratuito da Telerik](http://www.telerik.com/fiddler), tooissue HTTP solicitações tooand exibir respostas usando Olá API de REST de pesquisa do Azure, sem ter que toowrite qualquer código.</span><span class="sxs-lookup"><span data-stu-id="4c30a-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="4c30a-110">A Pesquisa do Azure é um serviço de pesquisa hospedado na nuvem totalmente gerenciado no Microsoft Azure, facilmente programável por meio APIs REST e .NET.</span><span class="sxs-lookup"><span data-stu-id="4c30a-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="4c30a-111">saudação de serviço de pesquisa do Azure, APIs REST estão documentadas em [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c30a-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="4c30a-112">Olá etapas a seguir, você criar um índice, carregar documentos, índice de saudação de consulta e, em seguida, sistema de saudação de consulta para obter informações de serviço.</span><span class="sxs-lookup"><span data-stu-id="4c30a-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="4c30a-113">toocomplete essas etapas, você precisará de um serviço de pesquisa do Azure e `api-key`.</span><span class="sxs-lookup"><span data-stu-id="4c30a-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="4c30a-114">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter instruções sobre como tooget iniciada.</span><span class="sxs-lookup"><span data-stu-id="4c30a-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="4c30a-115">Crie um índice</span><span class="sxs-lookup"><span data-stu-id="4c30a-115">Create an index</span></span>
1. <span data-ttu-id="4c30a-116">Inicie o Fiddler.</span><span class="sxs-lookup"><span data-stu-id="4c30a-116">Start Fiddler.</span></span> <span data-ttu-id="4c30a-117">Em Olá **arquivo** menu desativar **capturar tráfego** toohide estranhas HTTP atividade de tarefa atual toohello não relacionados.</span><span class="sxs-lookup"><span data-stu-id="4c30a-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="4c30a-118">Em Olá **criador** guia, você vai Formula uma solicitação que se parece com hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c30a-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="4c30a-119">Selecione **PUT**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-119">Select **PUT**.</span></span>
4. <span data-ttu-id="4c30a-120">Insira uma URL que especifica a URL do serviço hello, atributos de solicitação e Olá api-version.</span><span class="sxs-lookup"><span data-stu-id="4c30a-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="4c30a-121">Alguns tookeep de ponteiros em mente:</span><span class="sxs-lookup"><span data-stu-id="4c30a-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="4c30a-122">Use o HTTPS como prefixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c30a-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="4c30a-123">O atributo de solicitação é "/indexes/hotels".</span><span class="sxs-lookup"><span data-stu-id="4c30a-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="4c30a-124">Isso informa toocreate pesquisa um índice chamado 'hotéis'.</span><span class="sxs-lookup"><span data-stu-id="4c30a-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="4c30a-125">A versão da API fica em letras minúsculas, especificada como "?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="4c30a-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="4c30a-126">As versões da API são importantes porque a Pesquisa do Azure implanta atualizações regularmente.</span><span class="sxs-lookup"><span data-stu-id="4c30a-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="4c30a-127">Em raras ocasiões, uma atualização de serviço pode apresentar uma alteração de quebra toohello API.</span><span class="sxs-lookup"><span data-stu-id="4c30a-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="4c30a-128">Por esse motivo, a Pesquisa do Azure requer uma versão de api em cada solicitação para que você tenha controle total sobre qual delas será usada.</span><span class="sxs-lookup"><span data-stu-id="4c30a-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="4c30a-129">a URL completa Olá deve ter aparência semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c30a-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="4c30a-130">Especifica o cabeçalho de solicitação hello, substituindo host hello e chave de api com valores que são válidos para o serviço.</span><span class="sxs-lookup"><span data-stu-id="4c30a-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="4c30a-131">No corpo da solicitação, cole em campos de saudação que compõem a definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c30a-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="4c30a-132">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-132">Click **Execute**.</span></span>

<span data-ttu-id="4c30a-133">Em alguns segundos, você deve ver uma resposta HTTP 201 na lista de sessão hello, indicando que o índice de saudação foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="4c30a-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="4c30a-134">Se você receber HTTP 504, verifique se o que URL Olá Especifica o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4c30a-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="4c30a-135">Se você vir HTTP 400 ou 404, verifique a solicitação de saudação corpo tooverify existe foram sem erros de copiar e colar.</span><span class="sxs-lookup"><span data-stu-id="4c30a-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="4c30a-136">Um HTTP 403 normalmente indica um problema com hello-chave de api (uma chave inválida ou um problema de sintaxe com como chave de api Olá for especificado).</span><span class="sxs-lookup"><span data-stu-id="4c30a-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="4c30a-137">Carregue os documentos</span><span class="sxs-lookup"><span data-stu-id="4c30a-137">Load documents</span></span>
<span data-ttu-id="4c30a-138">Em Olá **criador** guia documentos toopost solicitação serão semelhante a saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c30a-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="4c30a-139">corpo de saudação da solicitação de saudação contém dados de pesquisa de Olá para 4 hotéis.</span><span class="sxs-lookup"><span data-stu-id="4c30a-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="4c30a-140">Selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-140">Select **POST**.</span></span>
2. <span data-ttu-id="4c30a-141">Insira uma URL iniciada por HTTPS, seguida da URL do serviço, seguida de "/indexes/<'nomedoíndice'>/docs/index?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="4c30a-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="4c30a-142">a URL completa Olá deve ter aparência semelhante toohello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c30a-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="4c30a-143">Cabeçalho de solicitação deve ser Olá mesmo de antes.</span><span class="sxs-lookup"><span data-stu-id="4c30a-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="4c30a-144">Lembre-se de substituído host hello e chave de api com valores que são válidos para o serviço.</span><span class="sxs-lookup"><span data-stu-id="4c30a-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="4c30a-145">Olá corpo da solicitação contém quatro índice hotéis toobe toohello adicionado de documentos.</span><span class="sxs-lookup"><span data-stu-id="4c30a-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="4c30a-146">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-146">Click **Execute**.</span></span>

<span data-ttu-id="4c30a-147">Em alguns segundos, você deve ver uma resposta HTTP 200 na lista de sessão hello.</span><span class="sxs-lookup"><span data-stu-id="4c30a-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="4c30a-148">Isso indica Olá documentos foram criados com êxito.</span><span class="sxs-lookup"><span data-stu-id="4c30a-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="4c30a-149">Se você receber um 207, pelo menos um documento falha tooupload.</span><span class="sxs-lookup"><span data-stu-id="4c30a-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="4c30a-150">Se você receber um 404, você tem um erro de sintaxe no cabeçalho de saudação ou corpo de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c30a-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="4c30a-151">Índice de saudação de consulta</span><span class="sxs-lookup"><span data-stu-id="4c30a-151">Query hello index</span></span>
<span data-ttu-id="4c30a-152">Agora que o índice e os documentos foram carregados, você pode consultá-los.</span><span class="sxs-lookup"><span data-stu-id="4c30a-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="4c30a-153">Em Olá **criador** guia, uma **obter** comando que consulta o serviço terá aparência semelhante toohello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c30a-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="4c30a-154">Selecione **GET**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-154">Select **GET**.</span></span>
2. <span data-ttu-id="4c30a-155">Insira uma URL iniciada por HTTPS, seguida da URL do serviço, seguida por "/indexes/<'indexname'>/docs?", seguido de parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="4c30a-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="4c30a-156">Por exemplo, use Olá URL a seguir, substituindo o nome de host de exemplo hello por um que seja válido para o serviço.</span><span class="sxs-lookup"><span data-stu-id="4c30a-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="4c30a-157">Essa consulta pesquisa termo hello "motel" e recupera as categorias de faceta para classificações.</span><span class="sxs-lookup"><span data-stu-id="4c30a-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="4c30a-158">Cabeçalho de solicitação deve ser Olá mesmo de antes.</span><span class="sxs-lookup"><span data-stu-id="4c30a-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="4c30a-159">Lembre-se de substituído host hello e chave de api com valores que são válidos para o serviço.</span><span class="sxs-lookup"><span data-stu-id="4c30a-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="4c30a-160">código de resposta de saudação deve ser 200, e a saída de resposta hello deve parecer semelhante toohello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c30a-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="4c30a-161">Olá exemplo consulta a seguir é de saudação [a operação de índice de pesquisa (API de pesquisa do Azure)](http://msdn.microsoft.com/library/dn798927.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="4c30a-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="4c30a-162">Muitas consultas de exemplo hello neste tópico incluem espaços, que não são permitidos em Fiddler.</span><span class="sxs-lookup"><span data-stu-id="4c30a-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="4c30a-163">Substitua cada espaço com um caractere + antes de colá-lo em Olá cadeia de caracteres de consulta antes de tentar a consulta Olá Fiddler.</span><span class="sxs-lookup"><span data-stu-id="4c30a-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="4c30a-164">**Antes da substituição dos espaços:**</span><span class="sxs-lookup"><span data-stu-id="4c30a-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="4c30a-165">**Após a substituição dos espaços por +:**</span><span class="sxs-lookup"><span data-stu-id="4c30a-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="4c30a-166">Sistema de saudação de consulta</span><span class="sxs-lookup"><span data-stu-id="4c30a-166">Query hello system</span></span>
<span data-ttu-id="4c30a-167">Você também pode consultar Olá tooget documento contagens e armazenamento consumo do sistema.</span><span class="sxs-lookup"><span data-stu-id="4c30a-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="4c30a-168">Em Olá **criador** guia, sua solicitação será a aparência a seguir toohello semelhante e resposta Olá retornará uma contagem do número de saudação de documentos e o espaço usado.</span><span class="sxs-lookup"><span data-stu-id="4c30a-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="4c30a-169">Selecione **GET**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-169">Select **GET**.</span></span>
2. <span data-ttu-id="4c30a-170">Insira uma URL que inclua a URL do seu serviço, seguida por "/indexes/hotels/stats?api-version=2016-09-01":</span><span class="sxs-lookup"><span data-stu-id="4c30a-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="4c30a-171">Especifica o cabeçalho de solicitação hello, substituindo host hello e chave de api com valores que são válidos para o serviço.</span><span class="sxs-lookup"><span data-stu-id="4c30a-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="4c30a-172">Corpo da solicitação Olá deixe em branco.</span><span class="sxs-lookup"><span data-stu-id="4c30a-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="4c30a-173">Clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="4c30a-173">Click **Execute**.</span></span> <span data-ttu-id="4c30a-174">Você deve ver um código de status HTTP 200 na lista de sessão hello.</span><span class="sxs-lookup"><span data-stu-id="4c30a-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="4c30a-175">Selecione entrada hello lançada para o comando.</span><span class="sxs-lookup"><span data-stu-id="4c30a-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="4c30a-176">Clique em Olá **inspetores** , clique em Olá **cabeçalhos** guia e, em seguida, selecione Olá JSON formato.</span><span class="sxs-lookup"><span data-stu-id="4c30a-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="4c30a-177">Você deve ver Olá contagem e o armazenamento de tamanho do documento (em KB).</span><span class="sxs-lookup"><span data-stu-id="4c30a-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c30a-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c30a-178">Next steps</span></span>
<span data-ttu-id="4c30a-179">Consulte [gerenciar o serviço de pesquisa no Azure](search-manage.md) para uma abordagem sem código toomanaging e usando a pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c30a-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
