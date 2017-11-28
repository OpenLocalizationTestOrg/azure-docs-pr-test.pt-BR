---
title: API REST de pesquisa de log do Log Analytics | Microsoft Docs
description: "Este guia fornece um tutorial básico que descreve como você pode usar a API REST da Pesquisa do Log Analytics no OMS (Operations Management Suite) e fornece exemplos que mostram como usar os comandos."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 78afb2f065dde4a3e7a3ab787c939b3c52b72cc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="63f55-103">API REST de pesquisa de log do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="63f55-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="63f55-104">Este guia fornece um tutorial básico, incluindo exemplos de como você pode usar a API REST do Log Analytics Search.</span><span class="sxs-lookup"><span data-stu-id="63f55-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="63f55-105">O Log Analytics faz parte do OMS (Operations Management Suite).</span><span class="sxs-lookup"><span data-stu-id="63f55-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="63f55-106">Se o espaço de trabalho tiver sido atualizado para a [nova linguagem de consulta do Log Analytics](log-analytics-log-search-upgrade.md), você deverá continuar usando a linguagem de consulta herdada com a API da pesquisa de logs, conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="63f55-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue to use the legacy query language with the log search API as described in this article.</span></span>  <span data-ttu-id="63f55-107">Uma nova API será liberada para espaços de trabalho atualizados e a documentação será atualizada nessa ocasião.</span><span class="sxs-lookup"><span data-stu-id="63f55-107">A new API will be released for upgraded workspaces, and the documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="63f55-108">O Log Analytics chamava-se Operational Insights e é por isso que esse é o nome usado nos no provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="63f55-108">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="63f55-109">Visão geral da API REST de pesquisa de log</span><span class="sxs-lookup"><span data-stu-id="63f55-109">Overview of the Log Search REST API</span></span>
<span data-ttu-id="63f55-110">A API REST de Pesquisa do Log Analytics é RESTful e pode ser acessada por meio da API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63f55-110">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="63f55-111">Este artigo fornece exemplo de como acessar a API por meio do [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação da API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63f55-111">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="63f55-112">O uso do ARMClient é uma das muitas opções para acessar a API do Log Analytics Search.</span><span class="sxs-lookup"><span data-stu-id="63f55-112">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="63f55-113">Outra opção é usar o módulo do Azure PowerShell para OperationalInsights, que inclui cmdlets para acessar a pesquisa.</span><span class="sxs-lookup"><span data-stu-id="63f55-113">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="63f55-114">Com essas ferramentas, você pode utilizar a API do Azure Resource Manager para fazer chamadas aos espaços de trabalho do OMS e executar comandos de pesquisa dentro deles.</span><span class="sxs-lookup"><span data-stu-id="63f55-114">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="63f55-115">A API produz resultados da pesquisa no formato JSON, permitindo que você use os resultados da pesquisa de diferentes maneiras por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="63f55-115">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="63f55-116">O Azure Resource Manager pode ser usado por meio de uma [Biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx), bem como por meio da [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="63f55-116">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="63f55-117">Para saber mais, leia as páginas da Web vinculadas.</span><span class="sxs-lookup"><span data-stu-id="63f55-117">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="63f55-118">Se você usar um comando de agregação como `|measure count()` ou `distinct`, cada chamada de pesquisa poderá retornar até 500.000 registros.</span><span class="sxs-lookup"><span data-stu-id="63f55-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="63f55-119">Pesquisas que não incluem um comando de agregação retornam até 5.000 registros.</span><span class="sxs-lookup"><span data-stu-id="63f55-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="63f55-120">Tutorial básico da API REST de Pesquisa do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="63f55-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="63f55-121">Para usar o ARMClient</span><span class="sxs-lookup"><span data-stu-id="63f55-121">To use ARMClient</span></span>
1. <span data-ttu-id="63f55-122">Instale o [Chocolatey](https://chocolatey.org/), que é um gerenciador de pacotes de software livre para Windows.</span><span class="sxs-lookup"><span data-stu-id="63f55-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="63f55-123">Abra uma janela do prompt de comando como administrador e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="63f55-123">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="63f55-124">Instale o ARMClient executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="63f55-124">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="63f55-125">Para realizar uma pesquisa usando o ARMClient</span><span class="sxs-lookup"><span data-stu-id="63f55-125">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="63f55-126">Entre usando a conta da Microsoft ou sua conta corporativa ou de estudante:</span><span class="sxs-lookup"><span data-stu-id="63f55-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="63f55-127">Um logon bem-sucedido lista todas as assinaturas vinculadas à conta especificada:</span><span class="sxs-lookup"><span data-stu-id="63f55-127">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="63f55-128">Obtenha os espaços de trabalho do Operations Management Suite:</span><span class="sxs-lookup"><span data-stu-id="63f55-128">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="63f55-129">Uma chamada Get bem-sucedida geraria todos os espaços de trabalho associados à assinatura:</span><span class="sxs-lookup"><span data-stu-id="63f55-129">A successful Get call would output all workspaces tied to the subscription:</span></span>

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. <span data-ttu-id="63f55-130">Crie sua variável de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="63f55-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="63f55-131">Pesquise usando sua nova variável de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="63f55-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="63f55-132">Exemplos de referência da API REST de Pesquisa do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="63f55-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="63f55-133">Os exemplos a seguir mostram como você pode usar a API de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="63f55-133">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="63f55-134">Pesquisa - ação/leitura</span><span class="sxs-lookup"><span data-stu-id="63f55-134">Search - Action/Read</span></span>
<span data-ttu-id="63f55-135">**Url de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="63f55-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="63f55-136">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="63f55-136">**Request:**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
<span data-ttu-id="63f55-137">A tabela a seguir descreve as propriedades que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="63f55-137">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="63f55-138">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="63f55-138">**Property**</span></span> | <span data-ttu-id="63f55-139">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="63f55-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="63f55-140">top</span><span class="sxs-lookup"><span data-stu-id="63f55-140">top</span></span> |<span data-ttu-id="63f55-141">O número máximo de resultados a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="63f55-141">The maximum number of results to return.</span></span> |
| <span data-ttu-id="63f55-142">highlight</span><span class="sxs-lookup"><span data-stu-id="63f55-142">highlight</span></span> |<span data-ttu-id="63f55-143">Contém parâmetros anteriores e subsequentes, geralmente usados para realçar campos correspondentes</span><span class="sxs-lookup"><span data-stu-id="63f55-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="63f55-144">pre</span><span class="sxs-lookup"><span data-stu-id="63f55-144">pre</span></span> |<span data-ttu-id="63f55-145">Usado como prefixo da cadeia de caracteres específica para os campos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="63f55-145">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="63f55-146">post</span><span class="sxs-lookup"><span data-stu-id="63f55-146">post</span></span> |<span data-ttu-id="63f55-147">Acrescenta a cadeia de caracteres específica para os campos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="63f55-147">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="63f55-148">query</span><span class="sxs-lookup"><span data-stu-id="63f55-148">query</span></span> |<span data-ttu-id="63f55-149">A consulta de pesquisa usada para coletar e retornar os resultados.</span><span class="sxs-lookup"><span data-stu-id="63f55-149">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="63f55-150">iniciar</span><span class="sxs-lookup"><span data-stu-id="63f55-150">start</span></span> |<span data-ttu-id="63f55-151">O início da janela de tempo em que você deseja que os resultados sejam encontrados.</span><span class="sxs-lookup"><span data-stu-id="63f55-151">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="63f55-152">end</span><span class="sxs-lookup"><span data-stu-id="63f55-152">end</span></span> |<span data-ttu-id="63f55-153">O fim da janela de tempo em que você deseja que os resultados sejam encontrados.</span><span class="sxs-lookup"><span data-stu-id="63f55-153">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="63f55-154">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="63f55-154">**Response:**</span></span>

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a><span data-ttu-id="63f55-155">Pesquisa/{ID} - ação/leitura</span><span class="sxs-lookup"><span data-stu-id="63f55-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="63f55-156">**Solicite o conteúdo de uma pesquisa salva:**</span><span class="sxs-lookup"><span data-stu-id="63f55-156">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="63f55-157">Se a pesquisa retornar com um status 'Pendente', a sondagem dos resultados atualizados poderá ser feita por essa API.</span><span class="sxs-lookup"><span data-stu-id="63f55-157">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="63f55-158">Após seis minutos, o resultado da pesquisa será eliminado do cache e HTTP Gone será retornado.</span><span class="sxs-lookup"><span data-stu-id="63f55-158">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="63f55-159">Se a solicitação inicial de pesquisa retornar um status “Bem-sucedido” imediatamente, os resultados não serão adicionados ao cache, fazendo essa API retornar HTTP Gone se consultada.</span><span class="sxs-lookup"><span data-stu-id="63f55-159">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="63f55-160">O conteúdo de um resultado de HTTP 200 estará no mesmo formato que a solicitação inicial de pesquisa, apenas com valores atualizados.</span><span class="sxs-lookup"><span data-stu-id="63f55-160">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="63f55-161">Pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="63f55-161">Saved searches</span></span>
<span data-ttu-id="63f55-162">**Solicite a lista de pesquisas salvas:**</span><span class="sxs-lookup"><span data-stu-id="63f55-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="63f55-163">Métodos com suporte: GET, PUT e DELETE</span><span class="sxs-lookup"><span data-stu-id="63f55-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="63f55-164">Métodos de coleção com suporte: GET</span><span class="sxs-lookup"><span data-stu-id="63f55-164">Supported collection methods: GET</span></span>

<span data-ttu-id="63f55-165">A tabela a seguir descreve as propriedades que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="63f55-165">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="63f55-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="63f55-166">Property</span></span> | <span data-ttu-id="63f55-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="63f55-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63f55-168">ID</span><span class="sxs-lookup"><span data-stu-id="63f55-168">Id</span></span> |<span data-ttu-id="63f55-169">O identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="63f55-169">The unique identifier.</span></span> |
| <span data-ttu-id="63f55-170">Etag</span><span class="sxs-lookup"><span data-stu-id="63f55-170">Etag</span></span> |<span data-ttu-id="63f55-171">**Obrigatório para o Patch**.</span><span class="sxs-lookup"><span data-stu-id="63f55-171">**Required for Patch**.</span></span> <span data-ttu-id="63f55-172">Atualizado pelo servidor em cada gravação.</span><span class="sxs-lookup"><span data-stu-id="63f55-172">Updated by server on each write.</span></span> <span data-ttu-id="63f55-173">O valor deve ser igual ao valor armazenado atual ou '*' para atualizar.</span><span class="sxs-lookup"><span data-stu-id="63f55-173">Value must be equal to the current stored value or ‘*’ to update.</span></span> <span data-ttu-id="63f55-174">409 retornado para valores antigos ou inválidos.</span><span class="sxs-lookup"><span data-stu-id="63f55-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="63f55-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="63f55-175">properties.query</span></span> |<span data-ttu-id="63f55-176">**Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="63f55-176">**Required**.</span></span> <span data-ttu-id="63f55-177">A consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="63f55-177">The search query.</span></span> |
| <span data-ttu-id="63f55-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="63f55-178">properties.displayName</span></span> |<span data-ttu-id="63f55-179">**Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="63f55-179">**Required**.</span></span> <span data-ttu-id="63f55-180">O nome de exibição da consulta definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="63f55-180">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="63f55-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="63f55-181">properties.category</span></span> |<span data-ttu-id="63f55-182">**Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="63f55-182">**Required**.</span></span> <span data-ttu-id="63f55-183">A categoria definida pelo usuário para a consulta.</span><span class="sxs-lookup"><span data-stu-id="63f55-183">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="63f55-184">A API de pesquisa do Log Analytics atualmente retorna pesquisas salvas criadas pelo usuário quando sondada para pesquisas salvas em um espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="63f55-184">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="63f55-185">A API não retorna pesquisas salvas fornecidas por soluções.</span><span class="sxs-lookup"><span data-stu-id="63f55-185">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="63f55-186">Criar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="63f55-186">Create saved searches</span></span>
<span data-ttu-id="63f55-187">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="63f55-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="63f55-188">O nome para todas as pesquisas, agendas e ações salvas criadas com a API do Log Analytics deve estar em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="63f55-188">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="63f55-189">Excluir pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="63f55-189">Delete saved searches</span></span>
<span data-ttu-id="63f55-190">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="63f55-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="63f55-191">Atualizar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="63f55-191">Update saved searches</span></span>
 <span data-ttu-id="63f55-192">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="63f55-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="63f55-193">Metadados - somente JSON</span><span class="sxs-lookup"><span data-stu-id="63f55-193">Metadata - JSON only</span></span>
<span data-ttu-id="63f55-194">Eis aqui uma maneira de ver os campos para todos os tipos de log para os dados coletados em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="63f55-194">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="63f55-195">Por exemplo, se você quiser saber se o tipo de Evento tiver um campo chamado Computador, essa consulta será uma maneira de verificar.</span><span class="sxs-lookup"><span data-stu-id="63f55-195">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="63f55-196">**Solicitação por campos:**</span><span class="sxs-lookup"><span data-stu-id="63f55-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="63f55-197">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="63f55-197">**Response:**</span></span>

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

<span data-ttu-id="63f55-198">A tabela a seguir descreve as propriedades que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="63f55-198">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="63f55-199">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="63f55-199">**Property**</span></span> | <span data-ttu-id="63f55-200">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="63f55-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="63f55-201">name</span><span class="sxs-lookup"><span data-stu-id="63f55-201">name</span></span> |<span data-ttu-id="63f55-202">Nome do campo.</span><span class="sxs-lookup"><span data-stu-id="63f55-202">Field name.</span></span> |
| <span data-ttu-id="63f55-203">displayName</span><span class="sxs-lookup"><span data-stu-id="63f55-203">displayName</span></span> |<span data-ttu-id="63f55-204">O nome de exibição do campo.</span><span class="sxs-lookup"><span data-stu-id="63f55-204">The display name of the field.</span></span> |
| <span data-ttu-id="63f55-205">type</span><span class="sxs-lookup"><span data-stu-id="63f55-205">type</span></span> |<span data-ttu-id="63f55-206">O tipo do valor do campo.</span><span class="sxs-lookup"><span data-stu-id="63f55-206">The Type of the field value.</span></span> |
| <span data-ttu-id="63f55-207">facetable</span><span class="sxs-lookup"><span data-stu-id="63f55-207">facetable</span></span> |<span data-ttu-id="63f55-208">Combinação das propriedades 'indexed', 'stored' e 'facet' atuais.</span><span class="sxs-lookup"><span data-stu-id="63f55-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="63f55-209">display</span><span class="sxs-lookup"><span data-stu-id="63f55-209">display</span></span> |<span data-ttu-id="63f55-210">Propriedade 'display' atual.</span><span class="sxs-lookup"><span data-stu-id="63f55-210">Current ‘display’ property.</span></span> <span data-ttu-id="63f55-211">True se o campo está visível na pesquisa.</span><span class="sxs-lookup"><span data-stu-id="63f55-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="63f55-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="63f55-212">ownerType</span></span> |<span data-ttu-id="63f55-213">Reduzido a somente aqueles tipos que pertencem a endereços IP incorporados.</span><span class="sxs-lookup"><span data-stu-id="63f55-213">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="63f55-214">Parâmetros opcionais</span><span class="sxs-lookup"><span data-stu-id="63f55-214">Optional parameters</span></span>
<span data-ttu-id="63f55-215">As informações a seguir descrevem os parâmetros opcionais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="63f55-215">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="63f55-216">Realce</span><span class="sxs-lookup"><span data-stu-id="63f55-216">Highlighting</span></span>
<span data-ttu-id="63f55-217">O parâmetro "Highlight" é um parâmetro opcional que você pode usar para solicitar que o subsistema de pesquisa inclua um conjunto de marcadores em sua resposta.</span><span class="sxs-lookup"><span data-stu-id="63f55-217">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="63f55-218">Esses marcadores indicam o início e término do texto realçado que coincide com os termos fornecidos na consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="63f55-218">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="63f55-219">Você pode especificar os marcadores de início e término que serão usados pela pesquisa para encapsular o termo realçado.</span><span class="sxs-lookup"><span data-stu-id="63f55-219">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="63f55-220">**Exemplo de consulta de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="63f55-220">**Example search query**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

<span data-ttu-id="63f55-221">**Resultado de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="63f55-221">**Sample result:**</span></span>

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

<span data-ttu-id="63f55-222">Observe que o resultado anterior contém uma mensagem de erro que foi acrescida de um prefixo e anexada.</span><span class="sxs-lookup"><span data-stu-id="63f55-222">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="63f55-223">Grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="63f55-223">Computer groups</span></span>
<span data-ttu-id="63f55-224">Grupos de computadores são pesquisas especiais salvas que retornam um conjunto de computadores.</span><span class="sxs-lookup"><span data-stu-id="63f55-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="63f55-225">Você pode usar um grupo de computadores em outras consultas para limitar os resultados para os computadores no grupo.</span><span class="sxs-lookup"><span data-stu-id="63f55-225">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="63f55-226">Um grupo de computadores é implementado como uma pesquisa salva com uma marca de Grupo com um valor de Computador.</span><span class="sxs-lookup"><span data-stu-id="63f55-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="63f55-227">A seguir está um exemplo de resposta para um grupo de computadores.</span><span class="sxs-lookup"><span data-stu-id="63f55-227">Following is a sample response for a computer group.</span></span>

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a><span data-ttu-id="63f55-228">Recuperando grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="63f55-228">Retrieving computer groups</span></span>
<span data-ttu-id="63f55-229">Para recuperar um grupo de computadores, use o método Get com a ID do grupo.</span><span class="sxs-lookup"><span data-stu-id="63f55-229">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="63f55-230">Criar ou atualizar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="63f55-230">Creating or updating a computer group</span></span>
<span data-ttu-id="63f55-231">Para criar um grupo de computadores, use o método Put com uma ID de pesquisa salva exclusiva.</span><span class="sxs-lookup"><span data-stu-id="63f55-231">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="63f55-232">Se você usar uma ID de grupo de computador existente, ela será modificada.</span><span class="sxs-lookup"><span data-stu-id="63f55-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="63f55-233">Quando você cria um grupo de computadores no portal do Log Analytics, a ID é criada por meio do grupo e do nome.</span><span class="sxs-lookup"><span data-stu-id="63f55-233">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="63f55-234">A consulta usada para a definição de grupo deve retornar um conjunto de computadores para o grupo funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="63f55-234">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="63f55-235">É recomendável terminar sua consulta com `| Distinct Computer` para garantir que os dados corretos sejam retornados.</span><span class="sxs-lookup"><span data-stu-id="63f55-235">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="63f55-236">A definição da pesquisa salva deve incluir uma marca chamada Grupo com um valor de Computador para a pesquisa ser classificada como um grupo de computadores.</span><span class="sxs-lookup"><span data-stu-id="63f55-236">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="63f55-237">Excluindo grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="63f55-237">Deleting computer groups</span></span>
<span data-ttu-id="63f55-238">Para excluir um grupo de computadores, use o método Delete com a ID do grupo.</span><span class="sxs-lookup"><span data-stu-id="63f55-238">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="63f55-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63f55-239">Next steps</span></span>
* <span data-ttu-id="63f55-240">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) para criar consultas usando campos personalizados para os critérios.</span><span class="sxs-lookup"><span data-stu-id="63f55-240">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
