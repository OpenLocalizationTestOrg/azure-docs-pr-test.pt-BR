---
title: "AAA \"consultar um índice (portal - pesquisa do Azure) | Microsoft Docs\""
description: Execute uma consulta de pesquisa no Gerenciador de pesquisa do Portal do Azure hello.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="2a264-103">Consultar um índice de pesquisa do Azure usando o Gerenciador de pesquisa no hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a264-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a264-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2a264-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="2a264-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2a264-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="2a264-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2a264-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="2a264-107">REST</span><span class="sxs-lookup"><span data-stu-id="2a264-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="2a264-108">Este artigo mostra como tooquery uma pesquisa do Azure índice usando **Search Explorer** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a264-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="2a264-109">Você pode usar pesquisa Explorer toosubmit simple ou completo Lucene consulta cadeias de caracteres tooany existente índice em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="2a264-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="2a264-110">Painel de serviço abrir Olá</span><span class="sxs-lookup"><span data-stu-id="2a264-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="2a264-111">Clique em **todos os recursos** na barra de salto Olá Olá lado esquerdo da saudação [portal do Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="2a264-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="2a264-112">Selecione o serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2a264-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="2a264-113">Selecionar um índice</span><span class="sxs-lookup"><span data-stu-id="2a264-113">Select an index</span></span>

<span data-ttu-id="2a264-114">Índice Olá selecione você gostaria que toosearch de saudação **índices** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="2a264-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="2a264-115">Abrir o Search Explorer</span><span class="sxs-lookup"><span data-stu-id="2a264-115">Open Search Explorer</span></span>

<span data-ttu-id="2a264-116">Clique em Olá barra de pesquisa do Gerenciador de pesquisa bloco tooslide Olá aberto e o painel de resultados.</span><span class="sxs-lookup"><span data-stu-id="2a264-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="2a264-117">Iniciar a pesquisa</span><span class="sxs-lookup"><span data-stu-id="2a264-117">Start searching</span></span>

<span data-ttu-id="2a264-118">Ao usar o hello Explorer de pesquisa, você pode especificar [parâmetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a264-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="2a264-119">Em **Cadeia de caracteres de consulta**, digite uma consulta e então pressione **Pesquisar**.</span><span class="sxs-lookup"><span data-stu-id="2a264-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="2a264-120">cadeia de caracteres de consulta de saudação é automaticamente analisada em solicitação adequada Olá URL toosubmit uma solicitação HTTP em relação a saudação API de REST de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a264-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="2a264-121">Você pode usar qualquer válido simple ou completa Lucene sintaxe toocreate Olá solicitação de consulta.</span><span class="sxs-lookup"><span data-stu-id="2a264-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="2a264-122">Olá `*` caractere é equivalente tooan pesquisa vazia ou não especificado que retorna todos os documentos em nenhuma ordem específica.</span><span class="sxs-lookup"><span data-stu-id="2a264-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="2a264-123">Em **resultados**, resultados da consulta são apresentados em JSON bruto, carga toohello idênticos retornados em um corpo de resposta HTTP ao emitir solicitações de forma programática.</span><span class="sxs-lookup"><span data-stu-id="2a264-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="2a264-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a264-124">Next steps</span></span>

<span data-ttu-id="2a264-125">Olá recursos a seguir fornece exemplos e informações de sintaxe de consulta adicionais.</span><span class="sxs-lookup"><span data-stu-id="2a264-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="2a264-126">Sintaxe de consulta simples</span><span class="sxs-lookup"><span data-stu-id="2a264-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="2a264-127">Sintaxe de consulta Lucene</span><span class="sxs-lookup"><span data-stu-id="2a264-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="2a264-128">Exemplos de sintaxe de consulta Lucene</span><span class="sxs-lookup"><span data-stu-id="2a264-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="2a264-129">Sintaxe de expressão do filtro OData</span><span class="sxs-lookup"><span data-stu-id="2a264-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 