---
title: "pesquisa de log de análise de aaaLog API REST | Microsoft Docs"
description: "Este guia fornece um tutorial básico que descreve como você pode usar o hello REST API de pesquisa de análise de Log em Olá Operations Management Suite (OMS) e fornece exemplos que mostram como comandos de saudação toouse."
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
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="fe918-103">API REST de pesquisa de log do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fe918-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="fe918-104">Este guia fornece um tutorial básico, incluindo exemplos de como você pode usar o hello API de REST de pesquisa de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="fe918-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="fe918-105">Análise de log é parte da saudação Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="fe918-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="fe918-106">Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você deve continuar a linguagem de consulta herdados de saudação do toouse com a API de pesquisa de log de saudação conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fe918-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="fe918-107">Uma nova API será liberada para espaços de trabalho atualizados e documentação hello será atualizada no momento.</span><span class="sxs-lookup"><span data-stu-id="fe918-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="fe918-108">Análise de log foi chamada anteriormente os Insights operacionais, por isso é o nome de saudação usado no provedor de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="fe918-109">Visão geral da API de REST de pesquisa de Log de saudação</span><span class="sxs-lookup"><span data-stu-id="fe918-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="fe918-110">Olá API de REST de pesquisa de análise de Log é RESTful e pode ser acessado via Olá API do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe918-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="fe918-111">Este artigo fornece exemplos de como acessar por meio da API Olá [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comando de software livre que simplifica a invocação Olá API do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe918-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="fe918-112">uso de saudação do cliente do ARM é um dos muitos Olá de tooaccess opções API de pesquisa de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="fe918-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="fe918-113">Outra opção é toouse hello Azure PowerShell para OperationalInsights, que inclui cmdlets para acessar a pesquisa.</span><span class="sxs-lookup"><span data-stu-id="fe918-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="fe918-114">Com essas ferramentas, você pode utilizar Olá API do Gerenciador de recursos do Azure toomake chamadas tooOMS espaços de trabalho e executar comandos de pesquisa dentro deles.</span><span class="sxs-lookup"><span data-stu-id="fe918-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="fe918-115">Olá API produz resultados da pesquisa no formato JSON, permitindo que você resultados da pesquisa Olá toouse de diferentes maneiras por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="fe918-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="fe918-116">Hello Azure Resource Manager pode ser usado por meio de um [biblioteca para .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) e hello [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe918-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="fe918-117">toolearn mais, examine a páginas da web de saudação vinculada.</span><span class="sxs-lookup"><span data-stu-id="fe918-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="fe918-118">Se você usar um comando de agregação, como `|measure count()` ou `distinct`, cada chamada toosearch pode retornar até 500.000 registros.</span><span class="sxs-lookup"><span data-stu-id="fe918-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="fe918-119">Pesquisas que não incluem um comando de agregação retornam até 5.000 registros.</span><span class="sxs-lookup"><span data-stu-id="fe918-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="fe918-120">Tutorial básico da API REST de Pesquisa do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fe918-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="fe918-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="fe918-121">toouse ARMClient</span></span>
1. <span data-ttu-id="fe918-122">Instale o [Chocolatey](https://chocolatey.org/), que é um gerenciador de pacotes de software livre para Windows.</span><span class="sxs-lookup"><span data-stu-id="fe918-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="fe918-123">Abra uma janela de prompt de comando como administrador e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe918-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="fe918-124">Instale o cliente do ARM executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fe918-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="fe918-125">tooperform uma pesquisa usando o ARMClient</span><span class="sxs-lookup"><span data-stu-id="fe918-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="fe918-126">Entre usando a conta da Microsoft ou sua conta corporativa ou de estudante:</span><span class="sxs-lookup"><span data-stu-id="fe918-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="fe918-127">Um logon bem-sucedido lista todas as toohello assinaturas vinculadas dado conta:</span><span class="sxs-lookup"><span data-stu-id="fe918-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="fe918-128">Obter espaços de trabalho do hello Operations Management Suite:</span><span class="sxs-lookup"><span data-stu-id="fe918-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="fe918-129">Uma chamada Get bem-sucedida geraria que todos os espaços de trabalho vinculado toohello assinatura:</span><span class="sxs-lookup"><span data-stu-id="fe918-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="fe918-130">Crie sua variável de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="fe918-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="fe918-131">Pesquise usando sua nova variável de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="fe918-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="fe918-132">Exemplos de referência da API REST de Pesquisa do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fe918-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="fe918-133">Olá exemplos a seguir mostra como você pode usar o hello API de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="fe918-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="fe918-134">Pesquisa - ação/leitura</span><span class="sxs-lookup"><span data-stu-id="fe918-134">Search - Action/Read</span></span>
<span data-ttu-id="fe918-135">**Url de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="fe918-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="fe918-136">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="fe918-136">**Request:**</span></span>

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
<span data-ttu-id="fe918-137">Olá, a tabela a seguir descreve as propriedades de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fe918-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="fe918-138">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="fe918-138">**Property**</span></span> | <span data-ttu-id="fe918-139">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="fe918-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fe918-140">top</span><span class="sxs-lookup"><span data-stu-id="fe918-140">top</span></span> |<span data-ttu-id="fe918-141">número máximo de saudação do tooreturn de resultados.</span><span class="sxs-lookup"><span data-stu-id="fe918-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="fe918-142">highlight</span><span class="sxs-lookup"><span data-stu-id="fe918-142">highlight</span></span> |<span data-ttu-id="fe918-143">Contém parâmetros anteriores e subsequentes, geralmente usados para realçar campos correspondentes</span><span class="sxs-lookup"><span data-stu-id="fe918-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="fe918-144">pre</span><span class="sxs-lookup"><span data-stu-id="fe918-144">pre</span></span> |<span data-ttu-id="fe918-145">Prefixos Olá fornecido campos de tooyour correspondida de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="fe918-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="fe918-146">post</span><span class="sxs-lookup"><span data-stu-id="fe918-146">post</span></span> |<span data-ttu-id="fe918-147">Acrescenta Olá fornecido campos de tooyour correspondida de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="fe918-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="fe918-148">query</span><span class="sxs-lookup"><span data-stu-id="fe918-148">query</span></span> |<span data-ttu-id="fe918-149">consulta de pesquisa Olá usado toocollect e retornar resultados.</span><span class="sxs-lookup"><span data-stu-id="fe918-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="fe918-150">iniciar</span><span class="sxs-lookup"><span data-stu-id="fe918-150">start</span></span> |<span data-ttu-id="fe918-151">partir do Olá Olá da janela de tempo que você deseja toobe resultados encontrado.</span><span class="sxs-lookup"><span data-stu-id="fe918-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="fe918-152">end</span><span class="sxs-lookup"><span data-stu-id="fe918-152">end</span></span> |<span data-ttu-id="fe918-153">fim de Olá Olá da janela de tempo que você deseja toobe resultados encontrado.</span><span class="sxs-lookup"><span data-stu-id="fe918-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="fe918-154">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="fe918-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="fe918-155">Pesquisa/{ID} - ação/leitura</span><span class="sxs-lookup"><span data-stu-id="fe918-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="fe918-156">**Olá o conteúdo da solicitação de uma pesquisa salva:**</span><span class="sxs-lookup"><span data-stu-id="fe918-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="fe918-157">Se a pesquisa de saudação retornar com um status 'Pendente', resultados de saudação atualizado de sondagem podem ser feitos por essa API.</span><span class="sxs-lookup"><span data-stu-id="fe918-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="fe918-158">Após 6 minutos, Olá resultado da pesquisa de saudação será eliminado do cache de saudação e HTTP Gone será retornado.</span><span class="sxs-lookup"><span data-stu-id="fe918-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="fe918-159">Se a solicitação inicial de pesquisa de saudação retorna um status 'Bem-sucedido' imediatamente, resultados de saudação não são adicionados toohello cache causando esse tooreturn API HTTP Gone se consultada.</span><span class="sxs-lookup"><span data-stu-id="fe918-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="fe918-160">conteúdo de saudação de um resultado de HTTP 200 está no mesmo formato que a solicitação inicial de pesquisa de saudação apenas com valores atualizados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="fe918-161">Pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="fe918-161">Saved searches</span></span>
<span data-ttu-id="fe918-162">**Solicite a lista de pesquisas salvas:**</span><span class="sxs-lookup"><span data-stu-id="fe918-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="fe918-163">Métodos com suporte: GET, PUT e DELETE</span><span class="sxs-lookup"><span data-stu-id="fe918-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="fe918-164">Métodos de coleção com suporte: GET</span><span class="sxs-lookup"><span data-stu-id="fe918-164">Supported collection methods: GET</span></span>

<span data-ttu-id="fe918-165">Olá, a tabela a seguir descreve as propriedades de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fe918-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="fe918-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fe918-166">Property</span></span> | <span data-ttu-id="fe918-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="fe918-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe918-168">ID</span><span class="sxs-lookup"><span data-stu-id="fe918-168">Id</span></span> |<span data-ttu-id="fe918-169">Identificador exclusivo da saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-169">hello unique identifier.</span></span> |
| <span data-ttu-id="fe918-170">Etag</span><span class="sxs-lookup"><span data-stu-id="fe918-170">Etag</span></span> |<span data-ttu-id="fe918-171">**Obrigatório para o Patch**.</span><span class="sxs-lookup"><span data-stu-id="fe918-171">**Required for Patch**.</span></span> <span data-ttu-id="fe918-172">Atualizado pelo servidor em cada gravação.</span><span class="sxs-lookup"><span data-stu-id="fe918-172">Updated by server on each write.</span></span> <span data-ttu-id="fe918-173">O valor deve ser o valor armazenado atual de toohello igual ou ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="fe918-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="fe918-174">409 retornado para valores antigos ou inválidos.</span><span class="sxs-lookup"><span data-stu-id="fe918-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="fe918-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="fe918-175">properties.query</span></span> |<span data-ttu-id="fe918-176">**Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="fe918-176">**Required**.</span></span> <span data-ttu-id="fe918-177">consulta de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-177">hello search query.</span></span> |
| <span data-ttu-id="fe918-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="fe918-178">properties.displayName</span></span> |<span data-ttu-id="fe918-179">**Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="fe918-179">**Required**.</span></span> <span data-ttu-id="fe918-180">nome para exibição definidos pelo usuário Olá de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="fe918-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="fe918-181">properties.category</span></span> |<span data-ttu-id="fe918-182">**Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="fe918-182">**Required**.</span></span> <span data-ttu-id="fe918-183">categoria definida pelo usuário Olá de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="fe918-184">Olá API de pesquisa de análise de Log atualmente retorna criados pelo usuário pesquisas salvas quando sondada para pesquisas salvas em um espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fe918-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="fe918-185">Olá API não retornará pesquisas salvas fornecidas por soluções.</span><span class="sxs-lookup"><span data-stu-id="fe918-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="fe918-186">Criar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="fe918-186">Create saved searches</span></span>
<span data-ttu-id="fe918-187">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="fe918-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="fe918-188">nome de saudação para pesquisas salvas todas as agendas e ações criadas com hello API de análise de Log deve ser em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fe918-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="fe918-189">Excluir pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="fe918-189">Delete saved searches</span></span>
<span data-ttu-id="fe918-190">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="fe918-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="fe918-191">Atualizar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="fe918-191">Update saved searches</span></span>
 <span data-ttu-id="fe918-192">**Solicitação:**</span><span class="sxs-lookup"><span data-stu-id="fe918-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="fe918-193">Metadados - somente JSON</span><span class="sxs-lookup"><span data-stu-id="fe918-193">Metadata - JSON only</span></span>
<span data-ttu-id="fe918-194">Aqui está um campos do modo toosee Olá para todos os tipos de log para dados de saudação coletados em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fe918-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="fe918-195">Por exemplo, se você quiser que saber se o tipo de evento de saudação tem um campo chamado computador, essa consulta é uma maneira toocheck.</span><span class="sxs-lookup"><span data-stu-id="fe918-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="fe918-196">**Solicitação por campos:**</span><span class="sxs-lookup"><span data-stu-id="fe918-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="fe918-197">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="fe918-197">**Response:**</span></span>

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

<span data-ttu-id="fe918-198">Olá, a tabela a seguir descreve as propriedades de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fe918-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="fe918-199">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="fe918-199">**Property**</span></span> | <span data-ttu-id="fe918-200">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="fe918-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="fe918-201">name</span><span class="sxs-lookup"><span data-stu-id="fe918-201">name</span></span> |<span data-ttu-id="fe918-202">Nome do campo.</span><span class="sxs-lookup"><span data-stu-id="fe918-202">Field name.</span></span> |
| <span data-ttu-id="fe918-203">displayName</span><span class="sxs-lookup"><span data-stu-id="fe918-203">displayName</span></span> |<span data-ttu-id="fe918-204">Olá exibir nome do campo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="fe918-205">type</span><span class="sxs-lookup"><span data-stu-id="fe918-205">type</span></span> |<span data-ttu-id="fe918-206">Tipo de valor de campo de saudação do Hello.</span><span class="sxs-lookup"><span data-stu-id="fe918-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="fe918-207">facetable</span><span class="sxs-lookup"><span data-stu-id="fe918-207">facetable</span></span> |<span data-ttu-id="fe918-208">Combinação das propriedades 'indexed', 'stored' e 'facet' atuais.</span><span class="sxs-lookup"><span data-stu-id="fe918-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="fe918-209">display</span><span class="sxs-lookup"><span data-stu-id="fe918-209">display</span></span> |<span data-ttu-id="fe918-210">Propriedade 'display' atual.</span><span class="sxs-lookup"><span data-stu-id="fe918-210">Current ‘display’ property.</span></span> <span data-ttu-id="fe918-211">True se o campo está visível na pesquisa.</span><span class="sxs-lookup"><span data-stu-id="fe918-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="fe918-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="fe918-212">ownerType</span></span> |<span data-ttu-id="fe918-213">Tipos de tooonly reduzido que pertencem a endereços IP tooonboarded.</span><span class="sxs-lookup"><span data-stu-id="fe918-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="fe918-214">Parâmetros opcionais</span><span class="sxs-lookup"><span data-stu-id="fe918-214">Optional parameters</span></span>
<span data-ttu-id="fe918-215">Olá informações a seguir descreve os parâmetros opcionais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="fe918-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="fe918-216">Realce</span><span class="sxs-lookup"><span data-stu-id="fe918-216">Highlighting</span></span>
<span data-ttu-id="fe918-217">Olá "Highlight" é um parâmetro opcional que você pode usar o subsistema da pesquisa toorequest Olá inclua um conjunto de marcadores em sua resposta.</span><span class="sxs-lookup"><span data-stu-id="fe918-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="fe918-218">Esses marcadores indicam Olá início e término do texto realçado que coincide com os termos de saudação fornecidos na consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="fe918-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="fe918-219">Você pode especificar o início de saudação e terminar marcadores que são usados por um termo da pesquisa toowrap Olá realçado.</span><span class="sxs-lookup"><span data-stu-id="fe918-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="fe918-220">**Exemplo de consulta de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="fe918-220">**Example search query**</span></span>

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

<span data-ttu-id="fe918-221">**Resultado de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="fe918-221">**Sample result:**</span></span>

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

<span data-ttu-id="fe918-222">Observe que Olá resultado acima contém uma mensagem de erro que o prefixo e anexada.</span><span class="sxs-lookup"><span data-stu-id="fe918-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="fe918-223">Grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="fe918-223">Computer groups</span></span>
<span data-ttu-id="fe918-224">Grupos de computadores são pesquisas especiais salvas que retornam um conjunto de computadores.</span><span class="sxs-lookup"><span data-stu-id="fe918-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="fe918-225">Você pode usar um grupo de computadores em outros computadores consultas toolimit Olá resultados toohello no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="fe918-226">Um grupo de computadores é implementado como uma pesquisa salva com uma marca de Grupo com um valor de Computador.</span><span class="sxs-lookup"><span data-stu-id="fe918-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="fe918-227">A seguir está um exemplo de resposta para um grupo de computadores.</span><span class="sxs-lookup"><span data-stu-id="fe918-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="fe918-228">Recuperando grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="fe918-228">Retrieving computer groups</span></span>
<span data-ttu-id="fe918-229">ID de um grupo de computadores, use Olá método Get com grupo hello. tooretrieve</span><span class="sxs-lookup"><span data-stu-id="fe918-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="fe918-230">Criar ou atualizar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="fe918-230">Creating or updating a computer group</span></span>
<span data-ttu-id="fe918-231">toocreate um grupo de computadores, use Olá método Put com uma ID de pesquisa salva exclusivo.</span><span class="sxs-lookup"><span data-stu-id="fe918-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="fe918-232">Se você usar uma ID de grupo de computador existente, ela será modificada.</span><span class="sxs-lookup"><span data-stu-id="fe918-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="fe918-233">Quando você cria um grupo de computadores no portal de análise de Log hello, Olá ID é criado de nome e grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe918-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="fe918-234">consulta Olá usada para definição de grupo Olá deve retornar um conjunto de computadores para Olá grupo toofunction corretamente.</span><span class="sxs-lookup"><span data-stu-id="fe918-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="fe918-235">É recomendável que você encerrar sua consulta com `| Distinct Computer` tooensure Olá correto de dados são retornados.</span><span class="sxs-lookup"><span data-stu-id="fe918-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="fe918-236">definição de saudação do hello pesquisa salva deve incluir uma marca chamada grupo com um valor de computador para Olá pesquisa toobe classificado como um grupo de computadores.</span><span class="sxs-lookup"><span data-stu-id="fe918-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="fe918-237">Excluindo grupos de computadores</span><span class="sxs-lookup"><span data-stu-id="fe918-237">Deleting computer groups</span></span>
<span data-ttu-id="fe918-238">ID de um grupo de computadores, use Olá método Delete com grupo hello. toodelete</span><span class="sxs-lookup"><span data-stu-id="fe918-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="fe918-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe918-239">Next steps</span></span>
* <span data-ttu-id="fe918-240">Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) toobuild consultas usando campos personalizados para os critérios.</span><span class="sxs-lookup"><span data-stu-id="fe918-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
