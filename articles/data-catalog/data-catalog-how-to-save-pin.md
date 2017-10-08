---
title: "aaaSave pesquisas e ativos de dados de pin no catálogo de dados do Azure | Microsoft Docs"
description: "Como tooarticle realce recursos no catálogo de dados do Azure para salvar as fontes de dados e ativos de dados para uso posterior."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="c0b2a-103">Salva pesquisas e fixa ativos de dados no Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="c0b2a-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="c0b2a-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="c0b2a-104">Introduction</span></span>
<span data-ttu-id="c0b2a-105">O Catálogo de Dados do Azure fornece recursos para descoberta de fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="c0b2a-106">Rapidamente pesquisar e filtrar as fontes de dados do hello catálogo toolocate e entender a finalidade pretendida, tornando-a como dados à direita do mais fácil de saudação de toofind para o trabalho de saudação à mão.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="c0b2a-107">Mas se você precisar tooregularly trabalhar com hello mesmo dados?</span><span class="sxs-lookup"><span data-stu-id="c0b2a-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="c0b2a-108">E se você e outros usuários regularmente contribuem toohello seu conhecimento mesmas fontes de dados no catálogo Olá?</span><span class="sxs-lookup"><span data-stu-id="c0b2a-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="c0b2a-109">Nessas situações, tendo problema toorepeatedly Olá mesmo pesquisas podem ser ineficientes.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="c0b2a-110">É aqui que pesquisas salvas e ativos de dados fixos podem ajudar.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="c0b2a-111">Pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="c0b2a-111">Saved searches</span></span>
<span data-ttu-id="c0b2a-112">Uma pesquisa salva no Catálogo de Dados é uma definição de pesquisa reutilizável por usuário.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="c0b2a-113">Você pode definir uma pesquisa, inclusive os termos de pesquisa, as marcas e outros filtros e, em seguida, salvá-la.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="c0b2a-114">Você pode executar novamente a definição de pesquisa Olá salvada tooreturn posterior qualquer ativos de dados que correspondem a seus critérios de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="c0b2a-115">Criar uma pesquisa salva</span><span class="sxs-lookup"><span data-stu-id="c0b2a-115">Create a saved search</span></span>
<span data-ttu-id="c0b2a-116">toocreate uma pesquisa salva, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0b2a-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="c0b2a-117">No portal do catálogo de dados do Azure de hello, na Olá **pesquisa atual** janela, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Configurações da Pesquisa Atual, link Salvar](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="c0b2a-119">Insira critérios de pesquisa de saudação que você deseja tooreuse e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Configurações da Pesquisa Atual, nome da pesquisa salva](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="c0b2a-121">Quando você for solicitado, insira um nome para a pesquisa salva de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="c0b2a-122">Escolha um nome que seja significativo e que descreve a saudação de ativos de dados que serão retornadas pela pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="c0b2a-123">Gerenciar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="c0b2a-123">Manage saved searches</span></span>
<span data-ttu-id="c0b2a-124">Depois de salvar uma ou mais pesquisas, um **pesquisas salvas** opção é exibida embaixo Olá **pesquisa atual** caixa.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="c0b2a-125">Quando a saudação lista for expandida, todas as pesquisas salvas são exibidas.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Lista de pesquisas salvas](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="c0b2a-127">Proceda do seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c0b2a-127">Do any of hello following:</span></span>

* <span data-ttu-id="c0b2a-128">tooexecute uma pesquisa, selecione uma pesquisa salva na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="c0b2a-129">tooview uma lista de opções de gerenciamento para uma pesquisa salva, clique em Olá nome de pesquisa toohello próxima seta.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Opções para gerenciar as pesquisas salvas](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="c0b2a-131">tooenter um novo nome para pesquisa de saudação salva, selecione **Renomear**.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="c0b2a-132">definição de pesquisa de saudação não é alterada.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="c0b2a-133">a pesquisa na lista, selecione Olá salvada tooremove **excluir**e, em seguida, confirme a exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="c0b2a-134">pesquisa de saudação salvada toomark como a pesquisa padrão, selecione **Salvar como padrão**.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="c0b2a-135">Se você executar uma pesquisa de "empty" na página de início do hello Data Catalog do Azure, o padrão de pesquisa é executada.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="c0b2a-136">Além disso, Olá pesquisa que está marcada como pesquisa de padrão de saudação é exibida na parte superior de saudação do hello **pesquisas salvas** lista.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="c0b2a-137">Pesquisas organizacionais salvas</span><span class="sxs-lookup"><span data-stu-id="c0b2a-137">Organizational saved searches</span></span>
<span data-ttu-id="c0b2a-138">Todos os usuários na sua organização podem salvar pesquisas para uso próprio.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="c0b2a-139">Os administradores do catálogo de dados também podem salvar pesquisas para todos os usuários dentro da organização hello.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="c0b2a-140">Quando os administradores salvar uma pesquisa, eles serão apresentados com um **compartilhamento dentro da empresa Olá** opção.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="c0b2a-141">Saudação de compartilhamentos essa opção Salvar pesquisa para todos os usuários na organização Olá a seleção.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Pesquisas organizacionais salvas](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="c0b2a-143">Ativos de dados fixos</span><span class="sxs-lookup"><span data-stu-id="c0b2a-143">Pinned data assets</span></span>
<span data-ttu-id="c0b2a-144">Com pesquisas salvas, você pode salvar e reutilizar as definições de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="c0b2a-145">ativos de dados de saudação que são retornados pelas pesquisas Olá podem ser alterado ao longo do tempo como conteúdo de saudação de alteração de catálogo hello.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="c0b2a-146">Quando você fixa ativos de dados, você pode identificar explicitamente toomake de ativos de dados específicos-los mais fácil tooaccess sem a necessidade de toouse uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="c0b2a-147">A fixação de um ativo de dados é simples.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="c0b2a-148">lista de tooadd Olá dados ativos tooyour fixado, basta clicar em Olá **pin** ícone.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="c0b2a-149">Olá ícone é exibido no canto Olá Olá ativo lado a lado na exibição lado a lado de saudação e na coluna mais à esquerda Olá Olá o modo de exibição de lista no portal do catálogo de dados do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![ícone de pino Olá ativo de dados](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="c0b2a-151">Desafixar um ativo de dados é igualmente simples.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="c0b2a-152">Basta clicar Olá **Desafixar** ícone tootoggle Olá configuração ativo selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![ativo de dados Olá Desafixar ícone](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="c0b2a-154">Olá seção Meus ativos</span><span class="sxs-lookup"><span data-stu-id="c0b2a-154">hello My Assets section</span></span>
<span data-ttu-id="c0b2a-155">Olá inclui home page do portal do catálogo de dados um **ativos Meus** seção que exibe os ativos do usuário atual do toohello de interesse.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="c0b2a-156">Essa seção inclui os ativos fixos e as pesquisas salvas.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-156">This section includes both pinned assets and saved searches.</span></span>

![Olá seção Meus ativos na home page do hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="c0b2a-158">Resumo</span><span class="sxs-lookup"><span data-stu-id="c0b2a-158">Summary</span></span>
<span data-ttu-id="c0b2a-159">Catálogo de dados do Azure fornece recursos que tornam mais fácil fontes de dados de saudação toodiscover que for necessário, para que você e outros membros da organização podem gastar menos tempo procurando dados e a hora mais trabalhar com ele.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="c0b2a-160">As pesquisas salvas e os ativos de dados fixos aprimoram esses recursos principais para que os usuários possam facilmente identificar fontes de dados com as quais eles trabalham repetidamente.</span><span class="sxs-lookup"><span data-stu-id="c0b2a-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
