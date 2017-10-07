---
title: comportamento do cache da CDN do Azure com cadeias de caracteres de consulta de aaaControl | Microsoft Docs
description: "Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache da cadeia de consulta do Azure CDN."
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
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="556a0-103">Controlando o comportamento de cache da CDN do Azure com cadeias de consulta</span><span class="sxs-lookup"><span data-stu-id="556a0-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="556a0-104">Standard</span><span class="sxs-lookup"><span data-stu-id="556a0-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="556a0-105">CDN Premium do Azure da Verizon</span><span class="sxs-lookup"><span data-stu-id="556a0-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="556a0-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="556a0-106">Overview</span></span>
<span data-ttu-id="556a0-107">Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="556a0-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="556a0-108">Olá, Standard e Premium CDN produtos fornecem Olá mesma funcionalidade de cache de cadeia de caracteres de consulta, mas diferente de interface do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="556a0-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="556a0-109">Este documento descreve a interface Olá para **padrão do Azure CDN do Akamai** e **Azure CDN padrão da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="556a0-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="556a0-110">Para saber mais sobre o armazenamento em cache de cadeias de caracteres de consulta com a **CDN Premium do Azure da Verizon**, confira [Controlando o comportamento do cache de solicitações de CDN com cadeias de caracteres de consulta - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="556a0-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="556a0-111">Existem três modos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="556a0-111">Three modes are available:</span></span>

* <span data-ttu-id="556a0-112">**Ignorar as cadeias de caracteres de consulta**: Este é o modo padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="556a0-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="556a0-113">nó de extremidade CDN Olá passará a cadeia de caracteres de consulta de saudação da origem do hello solicitante toohello na primeira solicitação de saudação e ativos de saudação do cache.</span><span class="sxs-lookup"><span data-stu-id="556a0-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="556a0-114">Todas as solicitações subsequentes para esse ativo são atendidas do nó de borda Olá ignorará a cadeia de caracteres de consulta de saudação até expira ativo em cache hello.</span><span class="sxs-lookup"><span data-stu-id="556a0-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="556a0-115">**Ignorar o cache para URL com cadeias de caracteres de consulta**: nesse modo, as solicitações com cadeias de caracteres de consulta não estão em cache no nó de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="556a0-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="556a0-116">nó de borda Olá recupera ativo Olá diretamente origem hello e passa toohello solicitante com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="556a0-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="556a0-117">**Armazenar em cache cada URL exclusiva**: esse modo trata cada solicitação com uma cadeia de consulta como um ativo exclusivo com seu próprio cache.</span><span class="sxs-lookup"><span data-stu-id="556a0-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="556a0-118">Por exemplo, Olá resposta origem Olá para uma solicitação para *foo.ashx?q=bar* seria armazenado em cache no nó de borda hello e retornado para caches subsequentes com essa mesma cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="556a0-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="556a0-119">Uma solicitação para *foo.ashx?q=somethingelse* deve ser armazenado em cache como um ativo separado com seu próprio tempo toolive.</span><span class="sxs-lookup"><span data-stu-id="556a0-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="556a0-120">Alterando configurações de cache de cadeia de consulta para perfis de CDN padrão</span><span class="sxs-lookup"><span data-stu-id="556a0-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="556a0-121">Na folha de perfil CDN hello, clique em ponto de extremidade CDN Olá desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="556a0-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Pontos de extremidade da folha Perfil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="556a0-123">Abre a folha de ponto de extremidade CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="556a0-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="556a0-124">Clique em Olá **configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="556a0-124">Click hello **Configure** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="556a0-126">Abre a folha de configuração de CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="556a0-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="556a0-127">Selecione uma configuração de saudação **comportamento do cache de cadeia de consulta** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="556a0-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![Opções de cache de cadeia de caracteres de consulta CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="556a0-129">Depois de fazer sua escolha, clique em Olá **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="556a0-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="556a0-130">alterações de configurações de saudação não podem ser imediatamente visíveis, como demora Olá toopropagate de registro por meio de saudação CDN.</span><span class="sxs-lookup"><span data-stu-id="556a0-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="556a0-131">Para <b>Azure CDN do Akamai</b> , a propagação geralmente é concluída em um minuto.</span><span class="sxs-lookup"><span data-stu-id="556a0-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="556a0-132">Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.</span><span class="sxs-lookup"><span data-stu-id="556a0-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

