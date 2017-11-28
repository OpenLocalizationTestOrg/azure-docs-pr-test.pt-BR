---
title: "Pré-carregar ativos em um ponto de extremidade da CDN do Azure | Microsoft Docs"
description: "Saiba como pré-carregar o conteúdo armazenado em cache em um ponto de extremidade da CDN do Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="a9e2e-103">Pré-carregar ativos em um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="a9e2e-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="a9e2e-104">Por padrão, os ativos são armazenados primeiro em cache à medida que são solicitados.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="a9e2e-105">Isso significa que a primeira solicitação de cada região pode demorar mais tempo, pois os servidores de borda não terão o conteúdo armazenado em cache e precisarão encaminhar a solicitação para o servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="a9e2e-106">O pré-carregamento de conteúdo evita essa latência de primeiro acesso.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="a9e2e-107">Além de fornecer uma experiência mais adequada ao cliente, o pré-carregamento de seus ativos em cache também pode reduzir o tráfego de rede no servidor de origem.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="a9e2e-108">O pré-carregamento de ativos é útil para grandes eventos ou para conteúdo disponibilizado simultaneamente a um grande número de usuários, como o lançamento de um novo filme ou uma atualização de software.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="a9e2e-109">Esse tutorial orienta você carregando previamente o conteúdo armazenado em cache em todos os nós de borda da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="a9e2e-110">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="a9e2e-110">Walkthrough</span></span>
1. <span data-ttu-id="a9e2e-111">No [Portal do Azure](https://portal.azure.com), navegue até o perfil da CDN que contém o ponto de extremidade que você deseja pré-carregar.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="a9e2e-112">A folha do perfil é aberta.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-112">The profile blade opens.</span></span>
2. <span data-ttu-id="a9e2e-113">Clique no ponto de extremidade na lista.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="a9e2e-114">A folha do ponto de extremidade é aberta.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="a9e2e-115">Na folha do ponto de extremidade da CDN, clique no botão carregar.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Folha do ponto de extremidade da CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="a9e2e-117">A folha Carregar é aberta.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-117">The Load blade opens.</span></span>
   
    ![Folha de carregamento da CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="a9e2e-119">Insira o caminho completo de cada ativo que você deseja carregar (por exemplo, `/pictures/kitten.png`) na caixa de texto **Caminho** .</span><span class="sxs-lookup"><span data-stu-id="a9e2e-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a9e2e-120">Outras caixas de texto **Caminho** serão mostradas depois que você digitar um texto, para permitir que crie uma lista com vários ativos.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="a9e2e-121">Para excluir ativos da lista, clique no botão de reticências (...).</span><span class="sxs-lookup"><span data-stu-id="a9e2e-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="a9e2e-122">Os caminhos devem ser uma URL relativa que se adapte à seguinte [expressão regular](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="a9e2e-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="a9e2e-123">Carregar um único caminho de arquivo `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="a9e2e-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="a9e2e-124">Carregar um único arquivo com a cadeia de caracteres de consulta `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="a9e2e-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="a9e2e-125">Cada ativo deve ter seu próprio caminho.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-125">Each asset must have its own path.</span></span>  <span data-ttu-id="a9e2e-126">Não há nenhuma funcionalidade de curinga para pré-carregar ativos.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Botão Carregar](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="a9e2e-128">Clique no botão **Carregar** .</span><span class="sxs-lookup"><span data-stu-id="a9e2e-128">Click the **Load** button.</span></span>
   
    ![Botão Carregar](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="a9e2e-130">Há uma limitação de 10 solicitações de carga por minuto para cada perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="a9e2e-131">São permitidos 50 caminhos por solicitação.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-131">50 paths are allowed per request.</span></span> <span data-ttu-id="a9e2e-132">Cada caminho tem um limite de comprimento de 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a9e2e-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="a9e2e-133">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a9e2e-133">See also</span></span>
* [<span data-ttu-id="a9e2e-134">Limpar um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="a9e2e-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="a9e2e-135">Referência da API REST da CDN do Azure – limpar ou pré-carregar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="a9e2e-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

