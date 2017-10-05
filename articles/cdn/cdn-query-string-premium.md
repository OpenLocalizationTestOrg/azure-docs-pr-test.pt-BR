---
title: Controlando o comportamento de cache da CDN do Azure com cadeias de consulta - Premium | Microsoft Docs
description: "O cache da cadeia de caracteres de consulta da CDN do Azure controla como os arquivos devem ser armazenados em cache quando contêm cadeias de caracteres de consulta."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="9a23c-103">Controle o comportamento do caching da CDN do Azure com cadeias de consulta - Premium</span><span class="sxs-lookup"><span data-stu-id="9a23c-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a23c-104">Standard</span><span class="sxs-lookup"><span data-stu-id="9a23c-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="9a23c-105">CDN Premium do Azure da Verizon</span><span class="sxs-lookup"><span data-stu-id="9a23c-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9a23c-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9a23c-106">Overview</span></span>
<span data-ttu-id="9a23c-107">O cache da cadeia de caracteres de consulta controla como os arquivos devem ser armazenados em cache quando contêm cadeias de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="9a23c-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a23c-108">Os produtos CDN Standard e Premium fornecem a mesma funcionalidade de cache de cadeia de consulta, mas a interface do usuário varia.</span><span class="sxs-lookup"><span data-stu-id="9a23c-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="9a23c-109">Este documento descreve a interface da **CDN Premium do Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="9a23c-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="9a23c-110">Para o cache da cadeia de consulta com a **CDN Standard do Azure da Akamai** e a **CDN Standard do Azure da Verizon**, consulte [Controlar o comportamento de cache das solicitações CDN com cadeias de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="9a23c-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="9a23c-111">Existem três modos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="9a23c-111">Three modes are available:</span></span>

* <span data-ttu-id="9a23c-112">**standard-cache**: este é o modo padrão.</span><span class="sxs-lookup"><span data-stu-id="9a23c-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="9a23c-113">O nó de borda CDN passará a cadeia de caracteres de consulta do solicitante para a origem na primeira solicitação e deixará o ativo em cache.</span><span class="sxs-lookup"><span data-stu-id="9a23c-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="9a23c-114">Todas as solicitações subsequentes para esse ativo que são atendidas a partir do nó de borda ignorarão a cadeia de caracteres de consulta até que o ativo em cache expire.</span><span class="sxs-lookup"><span data-stu-id="9a23c-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="9a23c-115">**no-cache**: nesse modo, as solicitações com cadeias de consulta não estão em cache no nó de borda da CDN.</span><span class="sxs-lookup"><span data-stu-id="9a23c-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="9a23c-116">O nó de borda recupera o ativo diretamente da origem e passa-o para o solicitante com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="9a23c-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="9a23c-117">**unique-cache**: este modo trata cada solicitação com uma cadeia de consulta como um ativo exclusivo com seu próprio cache.</span><span class="sxs-lookup"><span data-stu-id="9a23c-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="9a23c-118">Por exemplo, a resposta da origem de uma solicitação de *foo.ashx?q=bar* seria armazenada em cache no nó de borda e retornada para os caches subsequentes com a mesma cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="9a23c-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="9a23c-119">Uma solicitação de *foo.ashx?q=somethingelse* será armazenada em cache como um ativo separado com seu próprio tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="9a23c-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="9a23c-120">Alterando as configurações de cache da cadeia de consulta para perfis de CDN Premium</span><span class="sxs-lookup"><span data-stu-id="9a23c-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="9a23c-121">Na folha do perfil CDN, clique no botão **Gerenciar** .</span><span class="sxs-lookup"><span data-stu-id="9a23c-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="9a23c-123">O portal de gerenciamento da CDN é aberto.</span><span class="sxs-lookup"><span data-stu-id="9a23c-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="9a23c-124">Passe o mouse sobre a guia **HTTP Grande**, em seguida, sobre o submenu **Configurações do Cache**.</span><span class="sxs-lookup"><span data-stu-id="9a23c-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="9a23c-125">Clique em **Cache de Cadeia de Caracteres de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="9a23c-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="9a23c-126">As opções de cache de cadeia de caracteres de consulta são exibidas.</span><span class="sxs-lookup"><span data-stu-id="9a23c-126">Query string caching options are displayed.</span></span>
   
    ![Opções de cache de cadeia de caracteres de consulta CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="9a23c-128">Após fazer a seleção, clique no botão **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="9a23c-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a23c-129">As mudanças de configuração podem não estar visíveis imediatamente, pois o registro demora um pouco para se propagar pela CDN.</span><span class="sxs-lookup"><span data-stu-id="9a23c-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="9a23c-130">Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.</span><span class="sxs-lookup"><span data-stu-id="9a23c-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

