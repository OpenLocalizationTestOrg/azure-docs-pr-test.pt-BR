---
title: aaaPurge um ponto de extremidade CDN do Azure | Microsoft Docs
description: "Saiba como toopurge todos armazenados em cache conteúdo de um ponto de extremidade CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="217d4-103">Limpar um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="217d4-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="217d4-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="217d4-104">Overview</span></span>
<span data-ttu-id="217d4-105">Nós de borda do Azure CDN armazenará em cache ativos até a expiração time-to-live (TTL) do ativo Olá.</span><span class="sxs-lookup"><span data-stu-id="217d4-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="217d4-106">Depois TTL do ativo Olá expira, quando um cliente solicita o ativo de saudação do nó de borda hello, nó de borda hello serão recupere uma cópia atualizada de solicitação de cliente Olá ativo tooserve hello e armazenar Olá de atualização de cache.</span><span class="sxs-lookup"><span data-stu-id="217d4-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="217d4-107">Olá melhor prática toomake-se de que os usuários sempre obtêm cópia mais recente de saudação de seus ativos é tooversion seus ativos para cada atualização e publicação-los como novas URLs.</span><span class="sxs-lookup"><span data-stu-id="217d4-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="217d4-108">CDN recuperará imediatamente novos ativos Olá Olá Avançar solicitações do cliente.</span><span class="sxs-lookup"><span data-stu-id="217d4-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="217d4-109">Às vezes, talvez você queira toopurge armazenado em cache o conteúdo de todos os nós de borda e forçar todos os tooretrieve novos atualizado ativos.</span><span class="sxs-lookup"><span data-stu-id="217d4-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="217d4-110">Isso pode ser devido a aplicativo de web tooyour tooupdates ou tooquickly ativos de atualização que contenham informações incorretas.</span><span class="sxs-lookup"><span data-stu-id="217d4-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="217d4-111">Observe que apenas limpeza limpa Olá armazenaram em cache o conteúdo nos servidores de borda CDN hello.</span><span class="sxs-lookup"><span data-stu-id="217d4-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="217d4-112">Qualquer cache downstream, como servidores proxy e caches do navegador local, ainda pode manter uma cópia armazenada em cache do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="217d4-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="217d4-113">É importante tooremember isso quando você define um arquivo de um tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="217d4-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="217d4-114">Você pode forçar uma versão cliente downstream toorequest hello mais recente do arquivo, dando a ele um nome exclusivo sempre que você atualizá-lo ou aproveitando [cache de cadeia de caracteres de consulta](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="217d4-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="217d4-115">Este tutorial o orienta durante a limpeza de ativos de todos os nós de borda de um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="217d4-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="217d4-116">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="217d4-116">Walkthrough</span></span>
1. <span data-ttu-id="217d4-117">Em Olá [Portal do Azure](https://portal.azure.com), procurar o perfil CDN toohello que contém o ponto de extremidade de saudação desejar toopurge.</span><span class="sxs-lookup"><span data-stu-id="217d4-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="217d4-118">Na folha de perfil CDN hello, clique botão de limpeza de saudação.</span><span class="sxs-lookup"><span data-stu-id="217d4-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Folha Perfil CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="217d4-120">Abre a folha de limpeza de saudação.</span><span class="sxs-lookup"><span data-stu-id="217d4-120">hello Purge blade opens.</span></span>
   
    ![Folha Limpeza da CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="217d4-122">Em Olá Limpar folha, selecione o endereço do serviço Olá desejar toopurge na lista suspensa de URL hello.</span><span class="sxs-lookup"><span data-stu-id="217d4-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Formulário de limpeza](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="217d4-124">Você também pode obter a folha de limpeza toohello clicando Olá **limpar** botão na folha de ponto de extremidade CDN hello.</span><span class="sxs-lookup"><span data-stu-id="217d4-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="217d4-125">Nesse caso, Olá **URL** campo será preenchido previamente com o endereço do serviço de saudação do ponto de extremidade específico.</span><span class="sxs-lookup"><span data-stu-id="217d4-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="217d4-126">Selecione quais recursos você deseja toopurge de saudação nós de borda.</span><span class="sxs-lookup"><span data-stu-id="217d4-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="217d4-127">Se você desejar tooclear todos os ativos, clique em Olá **Limpar tudo** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="217d4-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="217d4-128">Caso contrário, caminho de saudação do tipo de cada ativo quiser toopurge Olá **caminho** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="217d4-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="217d4-129">Abaixo formatos têm suporte no caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="217d4-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="217d4-130">**Limpeza de URL única**: limpeza de ativos individuais, especificando a URL completa hello, com ou sem a extensão de arquivo hello, por exemplo,`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="217d4-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="217d4-131">**Limpeza de caractere curinga**: o asterisco (\*) pode ser usado como um caractere curinga.</span><span class="sxs-lookup"><span data-stu-id="217d4-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="217d4-132">Limpar todas as pastas, subpastas e arquivos em um ponto de extremidade com `/*` Olá caminho ou limpar todas as subpastas e arquivos em uma pasta específica, especificando a pasta Olá seguida por `/*`, por exemplo,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="217d4-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="217d4-133">Observe que, no momento, a limpeza do caractere curinga não é compatível com a CDN do Azure do Akamai.</span><span class="sxs-lookup"><span data-stu-id="217d4-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="217d4-134">**Limpeza do domínio raiz**: limpeza de raiz de saudação do ponto de extremidade de saudação com "/" no caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="217d4-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="217d4-135">Caminhos devem ser especificados para limpeza e deve ser uma URL relativa que se ajustam a seguir Olá [expressão regular](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="217d4-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="217d4-136">Atualmente, **Limpar tudo** e **Limpeza de caractere curinga** não têm suporte na **CDN do Azure do Akamai**.</span><span class="sxs-lookup"><span data-stu-id="217d4-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="217d4-137">Limpeza de URL única `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="217d4-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="217d4-138">Cadeia de consulta `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="217d4-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="217d4-139">Limpeza de caractere curinga `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="217d4-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="217d4-140">Mais **caminho** caixas de texto aparecerá depois que você inserir texto tooallow toobuild uma lista de vários ativos.</span><span class="sxs-lookup"><span data-stu-id="217d4-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="217d4-141">Você pode excluir ativos na lista de saudação clicando o botão de reticências (...) hello.</span><span class="sxs-lookup"><span data-stu-id="217d4-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="217d4-142">Clique em Olá **limpar** botão.</span><span class="sxs-lookup"><span data-stu-id="217d4-142">Click hello **Purge** button.</span></span>
   
    ![Botão Limpar](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="217d4-144">Limpar solicitações levar aproximadamente 2 a 3 minutos tooprocess com **CDN do Azure da Verizon** (Standard e Premium) e cerca de 7 minutos com **Azure CDN do Akamai**.</span><span class="sxs-lookup"><span data-stu-id="217d4-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="217d4-145">A CDN do Azure tem um limite de 50 solicitações de limpeza simultâneas por vez.</span><span class="sxs-lookup"><span data-stu-id="217d4-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="217d4-146">Consulte também</span><span class="sxs-lookup"><span data-stu-id="217d4-146">See also</span></span>
* [<span data-ttu-id="217d4-147">Pré-carregar ativos em um ponto de extremidade da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="217d4-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="217d4-148">Referência da API REST da CDN do Azure – limpar ou pré-carregar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="217d4-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

