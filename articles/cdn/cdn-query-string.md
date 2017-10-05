---
title: Controlando o comportamento de cache da CDN do Azure com cadeias de consulta | Microsoft Docs
description: "O cache da cadeia de caracteres de consulta da CDN do Azure controla como os arquivos devem ser armazenados em cache quando contêm cadeias de caracteres de consulta."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="e685a-103">Controlando o comportamento de cache da CDN do Azure com cadeias de consulta</span><span class="sxs-lookup"><span data-stu-id="e685a-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e685a-104">Standard</span><span class="sxs-lookup"><span data-stu-id="e685a-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="e685a-105">CDN Premium do Azure da Verizon</span><span class="sxs-lookup"><span data-stu-id="e685a-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e685a-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e685a-106">Overview</span></span>
<span data-ttu-id="e685a-107">O cache da cadeia de caracteres de consulta controla como os arquivos devem ser armazenados em cache quando contêm cadeias de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="e685a-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e685a-108">Os produtos CDN Standard e Premium fornecem a mesma funcionalidade de cache de cadeia de consulta, mas a interface do usuário varia.</span><span class="sxs-lookup"><span data-stu-id="e685a-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="e685a-109">Este documento descreve a interface da **CDN Standard do Azure da Akamai** e da **CDN Standard do Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="e685a-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="e685a-110">Para saber mais sobre o armazenamento em cache de cadeias de caracteres de consulta com a **CDN Premium do Azure da Verizon**, confira [Controlando o comportamento do cache de solicitações de CDN com cadeias de caracteres de consulta - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="e685a-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="e685a-111">Existem três modos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="e685a-111">Three modes are available:</span></span>

* <span data-ttu-id="e685a-112">**Ignorar cadeias de consulta**: esse é o modo padrão.</span><span class="sxs-lookup"><span data-stu-id="e685a-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="e685a-113">O nó de borda CDN passará a cadeia de caracteres de consulta do solicitante para a origem na primeira solicitação e deixará o ativo em cache.</span><span class="sxs-lookup"><span data-stu-id="e685a-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="e685a-114">Todas as solicitações subsequentes para esse ativo que são atendidas a partir do nó de borda ignorarão a cadeia de caracteres de consulta até que o ativo em cache expire.</span><span class="sxs-lookup"><span data-stu-id="e685a-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="e685a-115">**Ignorar o cache da URL com cadeias de consulta**: nesse modo, as solicitações com cadeias de consulta não são armazenadas em cache no nó de borda da CDN.</span><span class="sxs-lookup"><span data-stu-id="e685a-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="e685a-116">O nó de borda recupera o ativo diretamente da origem e passa-o para o solicitante com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="e685a-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="e685a-117">**Armazenar em cache cada URL exclusiva**: esse modo trata cada solicitação com uma cadeia de consulta como um ativo exclusivo com seu próprio cache.</span><span class="sxs-lookup"><span data-stu-id="e685a-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="e685a-118">Por exemplo, a resposta da origem de uma solicitação de *foo.ashx?q=bar* seria armazenada em cache no nó de borda e retornada para os caches subsequentes com a mesma cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="e685a-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="e685a-119">Uma solicitação de *foo.ashx?q=somethingelse* será armazenada em cache como um ativo separado com seu próprio tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="e685a-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="e685a-120">Alterando configurações de cache de cadeia de consulta para perfis de CDN padrão</span><span class="sxs-lookup"><span data-stu-id="e685a-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="e685a-121">Na folha Perfil CDN, clique no ponto de extremidade da CDN que deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="e685a-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![Pontos de extremidade da folha Perfil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="e685a-123">A folha do ponto de extremidade da CDN se abre.</span><span class="sxs-lookup"><span data-stu-id="e685a-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="e685a-124">Clique no botão **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="e685a-124">Click the **Configure** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="e685a-126">A folha Configuração da CDN se abre.</span><span class="sxs-lookup"><span data-stu-id="e685a-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="e685a-127">Selecione uma configuração da lista suspensa **Comportamento do cache da cadeia de consulta** .</span><span class="sxs-lookup"><span data-stu-id="e685a-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![Opções de cache de cadeia de caracteres de consulta CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="e685a-129">Após fazer suas seleções, clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e685a-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e685a-130">As mudanças de configuração podem não estar visíveis imediatamente, pois o registro demora um pouco para se propagar pela CDN.</span><span class="sxs-lookup"><span data-stu-id="e685a-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="e685a-131">Para <b>Azure CDN do Akamai</b> , a propagação geralmente é concluída em um minuto.</span><span class="sxs-lookup"><span data-stu-id="e685a-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="e685a-132">Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.</span><span class="sxs-lookup"><span data-stu-id="e685a-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

