---
title: "aaaUpgrading toohello API REST de serviço de pesquisa do Azure versão 2016-09-01 | Microsoft Docs"
description: "Atualizando toohello API REST de serviço de pesquisa do Azure versão 2016-09-01"
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
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="e7cac-103">Atualizando toohello API REST de serviço de pesquisa do Azure versão 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="e7cac-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="e7cac-104">Se você estiver usando a versão 2015-02-28 ou 2015-02-28-visualização de saudação [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artigo o ajudará a atualizar seu aplicativo toouse Olá próximo disponível versão da API, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="e7cac-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="e7cac-105">Versão 2016-09-01 do hello API REST contém algumas alterações de versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="e7cac-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="e7cac-106">Elas são principalmente compatíveis com versões anteriores. Portanto, a alteração do código deve exigir apenas um mínimo de esforço, dependendo da versão que você estava usando antes.</span><span class="sxs-lookup"><span data-stu-id="e7cac-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="e7cac-107">Consulte [tooupgrade etapas](#UpgradeSteps) para obter instruções sobre como toochange seu código toouse Olá nova versão da API.</span><span class="sxs-lookup"><span data-stu-id="e7cac-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="e7cac-108">Sua instância de serviço de pesquisa do Azure oferece suporte a várias versões da API REST, incluindo hello mais recente.</span><span class="sxs-lookup"><span data-stu-id="e7cac-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="e7cac-109">Você pode continuar toouse uma versão quando ela não é mais hello mais recente, mas é recomendável que você migre a sua versão mais recente do código toouse hello.</span><span class="sxs-lookup"><span data-stu-id="e7cac-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="e7cac-110">O que há de novo na versão 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="e7cac-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="e7cac-111">Versão 2016-09-01 é segunda versão disponível Olá de saudação API de REST do serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cac-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="e7cac-112">Os novos recursos nesta versão da API incluem:</span><span class="sxs-lookup"><span data-stu-id="e7cac-112">New features in this API version include:</span></span>

* <span data-ttu-id="e7cac-113">[Analisadores personalizados](https://aka.ms/customanalyzers), que permite a você tootake controle sobre o processo de saudação de conversão de texto em tokens indexáveis e pesquisáveis.</span><span class="sxs-lookup"><span data-stu-id="e7cac-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="e7cac-114">[Armazenamento de BLOBs do Azure](search-howto-indexing-azure-blob-storage.md) e [armazenamento de tabela do Azure](search-howto-indexing-azure-tables.md) indexadores, que permitem que você tooeasily importar dados do armazenamento do Azure para pesquisa do Azure em uma agenda ou sob demanda.</span><span class="sxs-lookup"><span data-stu-id="e7cac-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="e7cac-115">[Mapeamentos de campo](search-indexer-field-mappings.md), que permite a você toocustomize como o indexadores importar dados para pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cac-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="e7cac-116">ETags, que permitem que você tooupdate definições de saudação de índices, indexadores e fontes de dados de uma maneira segura de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="e7cac-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="e7cac-117">Etapas tooupgrade</span><span class="sxs-lookup"><span data-stu-id="e7cac-117">Steps tooupgrade</span></span>
<span data-ttu-id="e7cac-118">Se você estiver atualizando da versão 2015-02-28, você provavelmente não terá toomake qualquer código de tooyour alterações, diferente de número de versão do toochange hello.</span><span class="sxs-lookup"><span data-stu-id="e7cac-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="e7cac-119">situações de somente Olá em que talvez seja necessário código toochange são quando:</span><span class="sxs-lookup"><span data-stu-id="e7cac-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="e7cac-120">O código falha quando propriedades não reconhecidas são retornadas em uma resposta da API.</span><span class="sxs-lookup"><span data-stu-id="e7cac-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="e7cac-121">Por padrão, o aplicativo deve ignorar propriedades que não entende.</span><span class="sxs-lookup"><span data-stu-id="e7cac-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="e7cac-122">O código de persistir as solicitações da API e tenta tooresend-los toohello nova versão da API.</span><span class="sxs-lookup"><span data-stu-id="e7cac-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="e7cac-123">Por exemplo, isso pode acontecer se o seu aplicativo persistir tokens de continuação retornados de saudação API de pesquisa (para obter mais informações, procure `@search.nextPageParameters` em Olá [referência de API de pesquisa](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="e7cac-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="e7cac-124">Se qualquer uma destas situações aplicar tooyou, em seguida, talvez seja necessário toochange seu código adequadamente.</span><span class="sxs-lookup"><span data-stu-id="e7cac-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="e7cac-125">Caso contrário, nenhuma alteração deve ser necessária a menos que você deseje toostart usando Olá [novos recursos](#WhatsNew) da versão 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="e7cac-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="e7cac-126">Se você estiver atualizando da versão 2015-02-28-visualização, Olá acima também se aplica, mas você também deve estar ciente de que alguns recursos de visualização não estão disponíveis na versão 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="e7cac-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="e7cac-127">Suporte de indexador do Armazenamento de Blobs do Azure para arquivos CSV e blobs que contêm matrizes JSON.</span><span class="sxs-lookup"><span data-stu-id="e7cac-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="e7cac-128">Sinônimos</span><span class="sxs-lookup"><span data-stu-id="e7cac-128">Synonyms</span></span>
* <span data-ttu-id="e7cac-129">Consultas "Mais como esta"</span><span class="sxs-lookup"><span data-stu-id="e7cac-129">"More like this" queries</span></span>

<span data-ttu-id="e7cac-130">Se seu código usa esses recursos, não será capaz de tooupgrade too2016-09-01 sem remover o uso deles.</span><span class="sxs-lookup"><span data-stu-id="e7cac-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7cac-131">Lembre-se de que as APIs de visualização servem para teste e avaliação, e não devem ser usadas em ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="e7cac-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="e7cac-132">Conclusão</span><span class="sxs-lookup"><span data-stu-id="e7cac-132">Conclusion</span></span>
<span data-ttu-id="e7cac-133">Se você precisar de mais detalhes sobre o uso Olá API de REST do serviço de pesquisa do Azure, consulte Olá atualizado recentemente [referência da API](https://msdn.microsoft.com/library/azure/dn798935.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="e7cac-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="e7cac-134">Apreciamos seus comentários sobre o Azure Search.</span><span class="sxs-lookup"><span data-stu-id="e7cac-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="e7cac-135">Se você encontrar problemas, sinta-se livre tooask nos para obter ajuda sobre Olá [Fórum do MSDN de pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="e7cac-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="e7cac-136">Se você estiver fazendo uma pergunta sobre o Azure pesquisar em StackOverflow, tootag se tornar com `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="e7cac-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="e7cac-137">Obrigado por usar a Pesquisa do Azure!</span><span class="sxs-lookup"><span data-stu-id="e7cac-137">Thank you for using Azure Search!</span></span>

