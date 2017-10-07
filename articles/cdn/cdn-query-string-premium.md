---
title: aaaControl o comportamento de cache do Azure CDN com cadeias de caracteres de consulta - Premium | Microsoft Docs
description: "Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache da cadeia de consulta do Azure CDN."
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
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="07697-103">Controle o comportamento do caching da CDN do Azure com cadeias de consulta - Premium</span><span class="sxs-lookup"><span data-stu-id="07697-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07697-104">Standard</span><span class="sxs-lookup"><span data-stu-id="07697-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="07697-105">CDN Premium do Azure da Verizon</span><span class="sxs-lookup"><span data-stu-id="07697-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="07697-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="07697-106">Overview</span></span>
<span data-ttu-id="07697-107">Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="07697-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07697-108">Olá, Standard e Premium CDN produtos fornecem Olá mesma funcionalidade de cache de cadeia de caracteres de consulta, mas diferente de interface do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="07697-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="07697-109">Este documento descreve a interface Olá para **Premium do Azure CDN da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="07697-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="07697-110">Para o cache da cadeia de consulta com a **CDN Standard do Azure da Akamai** e a **CDN Standard do Azure da Verizon**, consulte [Controlar o comportamento de cache das solicitações CDN com cadeias de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="07697-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="07697-111">Existem três modos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="07697-111">Three modes are available:</span></span>

* <span data-ttu-id="07697-112">**Standard-cache**: Este é o modo padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="07697-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="07697-113">nó de extremidade CDN Olá passará a cadeia de caracteres de consulta de saudação da origem do hello solicitante toohello na primeira solicitação de saudação e ativos de saudação do cache.</span><span class="sxs-lookup"><span data-stu-id="07697-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="07697-114">Todas as solicitações subsequentes para esse ativo são atendidas do nó de borda Olá ignorará a cadeia de caracteres de consulta de saudação até expira ativo em cache hello.</span><span class="sxs-lookup"><span data-stu-id="07697-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="07697-115">**sem cache**: nesse modo, as solicitações com cadeias de caracteres de consulta não estão em cache no nó de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="07697-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="07697-116">nó de borda Olá recupera ativo Olá diretamente origem hello e passa toohello solicitante com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="07697-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="07697-117">**unique-cache**: este modo trata cada solicitação com uma cadeia de consulta como um ativo exclusivo com seu próprio cache.</span><span class="sxs-lookup"><span data-stu-id="07697-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="07697-118">Por exemplo, Olá resposta origem Olá para uma solicitação para *foo.ashx?q=bar* seria armazenado em cache no nó de borda hello e retornado para caches subsequentes com essa mesma cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="07697-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="07697-119">Uma solicitação para *foo.ashx?q=somethingelse* deve ser armazenado em cache como um ativo separado com seu próprio tempo toolive.</span><span class="sxs-lookup"><span data-stu-id="07697-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="07697-120">Alterando as configurações de cache da cadeia de consulta para perfis de CDN Premium</span><span class="sxs-lookup"><span data-stu-id="07697-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="07697-121">Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.</span><span class="sxs-lookup"><span data-stu-id="07697-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="07697-123">portal de gerenciamento de CDN Olá é aberto.</span><span class="sxs-lookup"><span data-stu-id="07697-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="07697-124">Passe o mouse sobre Olá **HTTP grande** guia, em seguida, passe o mouse sobre Olá **as configurações de Cache** flutuante.</span><span class="sxs-lookup"><span data-stu-id="07697-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="07697-125">Clique em **Cache de Cadeia de Caracteres de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="07697-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="07697-126">As opções de cache de cadeia de caracteres de consulta são exibidas.</span><span class="sxs-lookup"><span data-stu-id="07697-126">Query string caching options are displayed.</span></span>
   
    ![Opções de cache de cadeia de caracteres de consulta CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="07697-128">Depois de fazer sua escolha, clique em Olá **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="07697-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07697-129">alterações de configurações de saudação não podem ser imediatamente visíveis, como demora Olá toopropagate de registro por meio de saudação CDN.</span><span class="sxs-lookup"><span data-stu-id="07697-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="07697-130">Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.</span><span class="sxs-lookup"><span data-stu-id="07697-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

