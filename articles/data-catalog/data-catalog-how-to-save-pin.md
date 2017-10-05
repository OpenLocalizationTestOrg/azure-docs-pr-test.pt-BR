---
title: "Salva pesquisas e fixa ativos de dados no Catálogo de Dados do Azure | Microsoft Docs"
description: "Artigo de instruções que destaca recursos do Catálogo de Dados do Azure para salvar fontes de dados e ativos de dados para uso posterior."
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
ms.openlocfilehash: 8c319d0dcbe8b95af11b8be2368a9348b260446c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="5932b-103">Salva pesquisas e fixa ativos de dados no Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="5932b-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="5932b-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="5932b-104">Introduction</span></span>
<span data-ttu-id="5932b-105">O Catálogo de Dados do Azure fornece recursos para descoberta de fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="5932b-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="5932b-106">Você pode rapidamente pesquisar e filtrar o catálogo para localizar fontes de dados e entender a finalidade pretendida, facilitando a localização dos dados corretos para o trabalho em questão.</span><span class="sxs-lookup"><span data-stu-id="5932b-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="5932b-107">Porém e se você precisar trabalhar regularmente com os mesmos dados?</span><span class="sxs-lookup"><span data-stu-id="5932b-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="5932b-108">E se você e outros usuários regularmente contribuírem com conhecimento para as mesmas fontes de dados no catálogo?</span><span class="sxs-lookup"><span data-stu-id="5932b-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="5932b-109">Nessas situações, precisar emitir repetidamente as mesmas pesquisas pode ser ineficiente.</span><span class="sxs-lookup"><span data-stu-id="5932b-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="5932b-110">É aqui que pesquisas salvas e ativos de dados fixos podem ajudar.</span><span class="sxs-lookup"><span data-stu-id="5932b-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="5932b-111">Pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="5932b-111">Saved searches</span></span>
<span data-ttu-id="5932b-112">Uma pesquisa salva no Catálogo de Dados é uma definição de pesquisa reutilizável por usuário.</span><span class="sxs-lookup"><span data-stu-id="5932b-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="5932b-113">Você pode definir uma pesquisa, inclusive os termos de pesquisa, as marcas e outros filtros e, em seguida, salvá-la.</span><span class="sxs-lookup"><span data-stu-id="5932b-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="5932b-114">Você pode executar novamente a definição de pesquisa salva posteriormente para retornar quaisquer ativos de dados que correspondem aos seus critérios de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5932b-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="5932b-115">Criar uma pesquisa salva</span><span class="sxs-lookup"><span data-stu-id="5932b-115">Create a saved search</span></span>
<span data-ttu-id="5932b-116">Para criar uma pesquisa salva, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5932b-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="5932b-117">No portal do Catálogo de Dados do Azure, na janela **Pesquisa Atual**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5932b-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Configurações da Pesquisa Atual, link Salvar](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="5932b-119">Insira os critérios de pesquisa que você deseja reutilizar e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5932b-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Configurações da Pesquisa Atual, nome da pesquisa salva](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="5932b-121">Quando solicitado, insira um nome para a pesquisa salva.</span><span class="sxs-lookup"><span data-stu-id="5932b-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="5932b-122">Escolha um nome que seja significativo e descritivo dos ativos de dados que serão retornados pela pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5932b-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="5932b-123">Gerenciar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="5932b-123">Manage saved searches</span></span>
<span data-ttu-id="5932b-124">Depois de salvar uma ou mais pesquisas, uma opção **Pesquisas Salvas** é exibida abaixo da caixa **Pesquisa Atual**.</span><span class="sxs-lookup"><span data-stu-id="5932b-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="5932b-125">Quando a lista é expandida, todas as pesquisas salvas são exibidas.</span><span class="sxs-lookup"><span data-stu-id="5932b-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![Lista de pesquisas salvas](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="5932b-127">Execute um destes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="5932b-127">Do any of the following:</span></span>

* <span data-ttu-id="5932b-128">Para executar uma pesquisa, selecione uma pesquisa salva na lista.</span><span class="sxs-lookup"><span data-stu-id="5932b-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="5932b-129">Para exibir uma lista de opções de gerenciamento para uma pesquisa salva, clique na seta para baixo ao lado do nome da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5932b-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Opções para gerenciar as pesquisas salvas](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="5932b-131">Para inserir um novo nome para a pesquisa salva, selecione **Renomear**.</span><span class="sxs-lookup"><span data-stu-id="5932b-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="5932b-132">A definição de pesquisa não é alterada.</span><span class="sxs-lookup"><span data-stu-id="5932b-132">The search definition is not changed.</span></span>

* <span data-ttu-id="5932b-133">Para remover a pesquisa salva de sua lista, selecione **Excluir** e, em seguida, confirme a exclusão.</span><span class="sxs-lookup"><span data-stu-id="5932b-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="5932b-134">Para marcar a pesquisa salva como sua pesquisa padrão, selecione **Salvar como Padrão**.</span><span class="sxs-lookup"><span data-stu-id="5932b-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="5932b-135">Se você executar uma pesquisa "vazia" na home page do Catálogo de Dados do Azure, a pesquisa padrão será executada.</span><span class="sxs-lookup"><span data-stu-id="5932b-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="5932b-136">Além disso, a pesquisa marcada como padrão será exibida na parte superior da lista **Pesquisas Salvas**.</span><span class="sxs-lookup"><span data-stu-id="5932b-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="5932b-137">Pesquisas organizacionais salvas</span><span class="sxs-lookup"><span data-stu-id="5932b-137">Organizational saved searches</span></span>
<span data-ttu-id="5932b-138">Todos os usuários na sua organização podem salvar pesquisas para uso próprio.</span><span class="sxs-lookup"><span data-stu-id="5932b-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="5932b-139">Os administradores do Catálogo de Dados também podem salvar pesquisas para todos os usuários dentro da organização.</span><span class="sxs-lookup"><span data-stu-id="5932b-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="5932b-140">Quando os administradores salvam uma pesquisa, é apresentada a eles uma opção para **Compartilhar dentro da empresa**.</span><span class="sxs-lookup"><span data-stu-id="5932b-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="5932b-141">Selecionar essa opção compartilha a pesquisa salva com todos os usuários na organização.</span><span class="sxs-lookup"><span data-stu-id="5932b-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Pesquisas organizacionais salvas](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="5932b-143">Ativos de dados fixos</span><span class="sxs-lookup"><span data-stu-id="5932b-143">Pinned data assets</span></span>
<span data-ttu-id="5932b-144">Com pesquisas salvas, você pode salvar e reutilizar as definições de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5932b-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="5932b-145">Os ativos de dados que são retornados pelas pesquisas podem mudar ao longo do tempo conforme o conteúdo do catálogo muda.</span><span class="sxs-lookup"><span data-stu-id="5932b-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="5932b-146">Quando você fixa ativos de dados, pode identificar explicitamente ativos de dados específicos para facilitar o acesso a eles sem necessidade de usar uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5932b-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="5932b-147">A fixação de um ativo de dados é simples.</span><span class="sxs-lookup"><span data-stu-id="5932b-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="5932b-148">Para adicionar o ativo de dados à sua lista fixada, simplesmente clique no ícone de **fixar**.</span><span class="sxs-lookup"><span data-stu-id="5932b-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="5932b-149">O ícone é exibido no canto do bloco ativo, no modo de exibição de bloco e na coluna mais à esquerda, no modo de exibição de lista, no portal do Catálogo de Dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="5932b-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![O ícone de fixar ativo de dados](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="5932b-151">Desafixar um ativo de dados é igualmente simples.</span><span class="sxs-lookup"><span data-stu-id="5932b-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="5932b-152">Simplesmente clique no ícone **desafixar** para alternar a configuração para o ativo selecionado.</span><span class="sxs-lookup"><span data-stu-id="5932b-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![Ícone de desafixar o ativo de dados](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="5932b-154">A seção Meus Ativos</span><span class="sxs-lookup"><span data-stu-id="5932b-154">The My Assets section</span></span>
<span data-ttu-id="5932b-155">A home page do portal do Catálogo de Dados inclui uma seção **Meus Ativos** que exibe os ativos de interesse do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="5932b-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="5932b-156">Essa seção inclui os ativos fixos e as pesquisas salvas.</span><span class="sxs-lookup"><span data-stu-id="5932b-156">This section includes both pinned assets and saved searches.</span></span>

![A seção Meus ativos na home page](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="5932b-158">Resumo</span><span class="sxs-lookup"><span data-stu-id="5932b-158">Summary</span></span>
<span data-ttu-id="5932b-159">O Catálogo de Dados do Azure fornece recursos que tornam mais fácil de descobrir as fontes de dados de que você precisa para que você e outros membros da organização possam gastar menos tempo procurando dados e mais tempo trabalhando com eles.</span><span class="sxs-lookup"><span data-stu-id="5932b-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="5932b-160">As pesquisas salvas e os ativos de dados fixos aprimoram esses recursos principais para que os usuários possam facilmente identificar fontes de dados com as quais eles trabalham repetidamente.</span><span class="sxs-lookup"><span data-stu-id="5932b-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
