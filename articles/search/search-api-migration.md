---
title: "Atualização para a API REST do Serviço Azure Search versão 2016-09-01 | Microsoft Docs"
description: "Atualização para a API de REST do serviço de Pesquisa do Azure versão 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="6c3d3-103">Atualização para a API de REST do serviço de Pesquisa do Azure versão 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="6c3d3-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="6c3d3-104">Se você estiver usando a versão 2015-02-28 ou 2015-02-28-Preview da [API REST do serviço Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artigo o ajudará a atualizar o aplicativo para usar a próxima versão da API disponível, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="6c3d3-105">A versão 2016-09-01 da API REST contém algumas alterações em relação a versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="6c3d3-106">Elas são principalmente compatíveis com versões anteriores. Portanto, a alteração do código deve exigir apenas um mínimo de esforço, dependendo da versão que você estava usando antes.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="6c3d3-107">Confira [Etapas da atualização](#UpgradeSteps) para obter instruções sobre como alterar o código para usar a nova versão da API.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3d3-108">Sua instância de serviço do Azure Search dá suporte a várias versões da API REST, incluindo a última.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="6c3d3-109">Você pode continuar usando uma versão quando ela não for mais a última, mas aconselhamos a migrar seu código para usar a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="6c3d3-110">O que há de novo na versão 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="6c3d3-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="6c3d3-111">A versão 2016-09-01 é a segunda versão com disponibilidade geral da API REST do Serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="6c3d3-112">Os novos recursos nesta versão da API incluem:</span><span class="sxs-lookup"><span data-stu-id="6c3d3-112">New features in this API version include:</span></span>

* <span data-ttu-id="6c3d3-113">[Analisadores personalizados](https://aka.ms/customanalyzers), que permitem assumir o controle do processo de conversão de texto para tokens indexáveis e pesquisáveis.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="6c3d3-114">Os indexadores de [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) e [Armazenamento de Tabelas do Azure](search-howto-indexing-azure-tables.md), que permitem que você importe facilmente dados do armazenamento do Azure para o Azure Search em um agendamento ou sob demanda.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="6c3d3-115">[Mapeamentos de campo](search-indexer-field-mappings.md), que permitem que você personalize como os indexadores importam dados para o Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="6c3d3-116">ETags, que permitem atualizar as definições de índices, indexadores e fontes de dados com segurança para simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="6c3d3-117">Etapas da atualização</span><span class="sxs-lookup"><span data-stu-id="6c3d3-117">Steps to upgrade</span></span>
<span data-ttu-id="6c3d3-118">Se estiver atualizando da versão 2015-02-28, você provavelmente não precisará fazer alterações no código, exceto a alteração do número de versão.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="6c3d3-119">As únicas situações em que talvez seja necessário alterar o código ocorrem quando:</span><span class="sxs-lookup"><span data-stu-id="6c3d3-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="6c3d3-120">O código falha quando propriedades não reconhecidas são retornadas em uma resposta da API.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="6c3d3-121">Por padrão, o aplicativo deve ignorar propriedades que não entende.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="6c3d3-122">O código persiste solicitações de API e tenta reenviá-las à nova versão da API.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="6c3d3-123">Por exemplo, isso poderá acontecer se o aplicativo persistir tokens de continuação retornados da API de Pesquisa (para obter mais informações, procure `@search.nextPageParameters` na [Referência de API de Pesquisa](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="6c3d3-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="6c3d3-124">Se alguma dessas situações se aplicar a você, talvez seja necessário alterar o código da maneira adequada.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="6c3d3-125">Caso contrário, nenhuma alteração será necessária, a menos que você deseje começar a usar os [novos recursos](#WhatsNew) da versão 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="6c3d3-126">Se você estiver atualizando da versão 2015-02-28-Preview, os itens acima também serão aplicáveis, mas esteja ciente de que alguns recursos de visualização não estão disponíveis na versão 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="6c3d3-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="6c3d3-127">Suporte de indexador do Armazenamento de Blobs do Azure para arquivos CSV e blobs que contêm matrizes JSON.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="6c3d3-128">Sinônimos</span><span class="sxs-lookup"><span data-stu-id="6c3d3-128">Synonyms</span></span>
* <span data-ttu-id="6c3d3-129">Consultas "Mais como esta"</span><span class="sxs-lookup"><span data-stu-id="6c3d3-129">"More like this" queries</span></span>

<span data-ttu-id="6c3d3-130">Se o código usar esses recursos, você não poderá atualizar para a versão 2016-09-01 sem parar de usá-los.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c3d3-131">Lembre-se de que as APIs de visualização servem para teste e avaliação, e não devem ser usadas em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="6c3d3-132">Conclusão</span><span class="sxs-lookup"><span data-stu-id="6c3d3-132">Conclusion</span></span>
<span data-ttu-id="6c3d3-133">Se precisar de mais detalhes sobre como usar a API REST do Serviço Azure Search, confira a [Referência da API](https://msdn.microsoft.com/library/azure/dn798935.aspx) recém-atualizada no MSDN.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="6c3d3-134">Apreciamos seus comentários sobre o Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="6c3d3-135">Se tiver problemas, fique à vontade para solicitar ajuda no [Fórum do MSDN sobre a Pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou o [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="6c3d3-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="6c3d3-136">Se você estiver fazendo uma pergunta sobre o Azure Search no StackOverflow, marque-a com `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="6c3d3-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="6c3d3-137">Obrigado por usar a Pesquisa do Azure!</span><span class="sxs-lookup"><span data-stu-id="6c3d3-137">Thank you for using Azure Search!</span></span>

