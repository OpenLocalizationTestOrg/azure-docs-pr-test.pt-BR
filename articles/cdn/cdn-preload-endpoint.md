---
title: carga aaaPre ativos em um ponto de extremidade CDN do Azure | Microsoft Docs
description: "Saiba como carga toopre armazenada em cache o conteúdo em um ponto de extremidade CDN do Azure."
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="e6d2d-103">Pré-carregar ativos em um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="e6d2d-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="e6d2d-104">Por padrão, os ativos são armazenados primeiro em cache à medida que são solicitados.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="e6d2d-105">Isso significa que a primeira solicitação saudação de cada região pode levar mais tempo, como servidores de borda de saudação não terá conteúdo Olá armazenadas em cache e será necessário um servidor de origem tooforward Olá solicitação toohello.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="e6d2d-106">O pré-carregamento de conteúdo evita essa latência de primeiro acesso.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="e6d2d-107">Além disso tooproviding uma melhor experiência do cliente, pré-carregar seus ativos em cache também pode reduzir o tráfego de rede no servidor de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="e6d2d-108">Pré-carregar ativos é útil para eventos grandes ou conteúdo que se torna disponível simultaneamente tooa grande número de usuários, como uma nova versão de filme ou uma atualização de software.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="e6d2d-109">Esse tutorial orienta você carregando previamente o conteúdo armazenado em cache em todos os nós de borda da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="e6d2d-110">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="e6d2d-110">Walkthrough</span></span>
1. <span data-ttu-id="e6d2d-111">Em Olá [Portal do Azure](https://portal.azure.com), procure o perfil CDN toohello que contém o ponto de extremidade de saudação desejar carregar toopre.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="e6d2d-112">Abre a folha de perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="e6d2d-113">Clique em ponto de extremidade de saudação na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="e6d2d-114">Abre a folha de ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="e6d2d-115">Na folha de ponto de extremidade CDN hello, clique botão de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Folha do ponto de extremidade da CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="e6d2d-117">Abre a folha de carga Hello.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-117">hello Load blade opens.</span></span>
   
    ![Folha de carregamento da CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="e6d2d-119">Digite o caminho completo da saudação de cada ativo desejar tooload (por exemplo, `/pictures/kitten.png`) no hello **caminho** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e6d2d-120">Mais **caminho** caixas de texto aparecerá depois que você inserir texto tooallow toobuild uma lista de vários ativos.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="e6d2d-121">Você pode excluir ativos na lista de saudação clicando o botão de reticências (...) hello.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="e6d2d-122">Caminhos devem ser uma URL relativa que atenda às seguintes Olá [expressão regular](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="e6d2d-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="e6d2d-123">Carregar um único caminho de arquivo `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="e6d2d-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="e6d2d-124">Carregar um único arquivo com a cadeia de caracteres de consulta `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="e6d2d-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="e6d2d-125">Cada ativo deve ter seu próprio caminho.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-125">Each asset must have its own path.</span></span>  <span data-ttu-id="e6d2d-126">Não há nenhuma funcionalidade de curinga para pré-carregar ativos.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Botão Carregar](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="e6d2d-128">Clique em Olá **carga** botão.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-128">Click hello **Load** button.</span></span>
   
    ![Botão Carregar](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="e6d2d-130">Há uma limitação de 10 solicitações de carga por minuto para cada perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="e6d2d-131">São permitidos 50 caminhos por solicitação.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-131">50 paths are allowed per request.</span></span> <span data-ttu-id="e6d2d-132">Cada caminho tem um limite de comprimento de 1024 caracteres.</span><span class="sxs-lookup"><span data-stu-id="e6d2d-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="e6d2d-133">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e6d2d-133">See also</span></span>
* [<span data-ttu-id="e6d2d-134">Limpar um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="e6d2d-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="e6d2d-135">Referência da API REST da CDN do Azure – limpar ou pré-carregar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="e6d2d-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

