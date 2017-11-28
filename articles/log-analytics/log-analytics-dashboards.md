---
title: aaaCreate um painel personalizado no Azure Log Analytics | Microsoft Docs
description: "Este guia ajuda você a entender como os painéis de análise de Log podem visualizar todas as pesquisas de log salvas, dando a você uma única Lente tooview seu ambiente."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="c86eb-103">Criar um painel personalizado para uso no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c86eb-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="c86eb-104">Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você não pode criar novos painéis ou editar painéis existentes.</span><span class="sxs-lookup"><span data-stu-id="c86eb-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="c86eb-105">Este guia ajuda você a entender como os painéis de análise de Log podem visualizar todas as pesquisas de log salvas, dando a você uma única Lente tooview seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c86eb-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Painel de Exemplo](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="c86eb-107">Todos os painéis de saudação personalizada que você cria no portal do OMS Olá também estão disponíveis no hello aplicativo móvel do OMS.</span><span class="sxs-lookup"><span data-stu-id="c86eb-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="c86eb-108">Consulte Olá páginas para obter mais informações sobre aplicativos Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="c86eb-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="c86eb-109">Aplicativo móvel do OMS de saudação Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="c86eb-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="c86eb-110">Aplicativo móvel do OMS no Apple iTunes</span><span class="sxs-lookup"><span data-stu-id="c86eb-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![painel móvel](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="c86eb-112">Como crio meu painel?</span><span class="sxs-lookup"><span data-stu-id="c86eb-112">How do I create my dashboard?</span></span>
<span data-ttu-id="c86eb-113">toobegin, vá toohello página de visão geral do OMS.</span><span class="sxs-lookup"><span data-stu-id="c86eb-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="c86eb-114">Você verá Olá **meu painel** bloco Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="c86eb-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="c86eb-115">Clique toodrill para baixo para seu painel.</span><span class="sxs-lookup"><span data-stu-id="c86eb-115">Click it toodrill down into your dashboard.</span></span>

![Visão geral](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="c86eb-117">Adicionando um bloco</span><span class="sxs-lookup"><span data-stu-id="c86eb-117">Adding a tile</span></span>
<span data-ttu-id="c86eb-118">Nos painéis, os blocos são ativados pelas pesquisas de log salvas.</span><span class="sxs-lookup"><span data-stu-id="c86eb-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="c86eb-119">O OMS vem com muitas pesquisas de log salvas previamente, portanto, você pode começar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="c86eb-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="c86eb-120">Use Olá as etapas a seguir essa estrutura de tópicos como toobegin.</span><span class="sxs-lookup"><span data-stu-id="c86eb-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="c86eb-121">Em Olá exibição meu painel, basta clicar **personalizar** tooenter no modo de personalização.</span><span class="sxs-lookup"><span data-stu-id="c86eb-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Ilustração](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="c86eb-123">Painel de saudação que abre Olá direita da página Olá mostra todas as pesquisas de log salvas do seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c86eb-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="c86eb-124">toovisualize pesquisar um log salvo como um bloco, passe o mouse sobre uma pesquisa salva e clique em Olá **mais** símbolo.</span><span class="sxs-lookup"><span data-stu-id="c86eb-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Adicionar Blocos 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="c86eb-126">Quando você clica em Olá **mais** símbolo, um novo bloco aparece na exibição meu painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="c86eb-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Adicionar Blocos 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="c86eb-128">Editar um bloco</span><span class="sxs-lookup"><span data-stu-id="c86eb-128">Edit a tile</span></span>
<span data-ttu-id="c86eb-129">Em Olá exibição meu painel, basta clicar **personalizar** tooenter no modo de personalização.</span><span class="sxs-lookup"><span data-stu-id="c86eb-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="c86eb-130">Clique em bloco Olá deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="c86eb-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="c86eb-131">painel direito da saudação altera tooedit e fornece uma seleção de opções:</span><span class="sxs-lookup"><span data-stu-id="c86eb-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Editar Bloco](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Editar Bloco](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="c86eb-134">Visualizações do bloco</span><span class="sxs-lookup"><span data-stu-id="c86eb-134">Tile visualizations</span></span>
<span data-ttu-id="c86eb-135">Há três tipos de toochoose de visualizações do bloco do:</span><span class="sxs-lookup"><span data-stu-id="c86eb-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="c86eb-136">tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="c86eb-136">chart type</span></span> | <span data-ttu-id="c86eb-137">o que ele faz</span><span class="sxs-lookup"><span data-stu-id="c86eb-137">what it does</span></span> |
| --- | --- |
| ![Gráfico de Barras](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="c86eb-139">Exibe uma linha do tempo dos resultados salvos da pesquisa de log como um gráfico de barras ou uma lista de resultados por campo, dependendo se sua pesquisa de log agrega os resultados por campo ou não.</span><span class="sxs-lookup"><span data-stu-id="c86eb-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![métrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="c86eb-141">Exibe as visitas totais dos resultados da pesquisa de log como um número em um bloco.</span><span class="sxs-lookup"><span data-stu-id="c86eb-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="c86eb-142">Os blocos da métrica permitem que você tooset um limite que destacará o bloco de saudação quando é atingido o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="c86eb-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="c86eb-144">Exibe uma linha do tempo das ocorrências dos resultados da pesquisa de log salva com valores como um gráfico de linhas.</span><span class="sxs-lookup"><span data-stu-id="c86eb-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="c86eb-145">Limite</span><span class="sxs-lookup"><span data-stu-id="c86eb-145">Threshold</span></span>
<span data-ttu-id="c86eb-146">Você pode criar um limite em um bloco usando a visualização métrica hello.</span><span class="sxs-lookup"><span data-stu-id="c86eb-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="c86eb-147">Selecione um valor de limite no bloco de saudação em toocreate.</span><span class="sxs-lookup"><span data-stu-id="c86eb-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="c86eb-148">Escolha se toohighlight Olá lado a lado ao valor Olá fica acima ou abaixo do limite de saudação escolhida, em seguida, defina o valor abaixo do limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="c86eb-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="c86eb-149">Organizando Olá painel</span><span class="sxs-lookup"><span data-stu-id="c86eb-149">Organizing hello dashboard</span></span>
<span data-ttu-id="c86eb-150">tooorganize seu painel, navegue toohello exibição de meu painel e clique em **personalizar** tooenter no modo de personalização.</span><span class="sxs-lookup"><span data-stu-id="c86eb-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="c86eb-151">Clique e arraste o bloco Olá desejado toomove e movê-la toowhere que você deseja que seu toobe lado a lado.</span><span class="sxs-lookup"><span data-stu-id="c86eb-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Organizar seu Painel](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="c86eb-153">Remover um bloco</span><span class="sxs-lookup"><span data-stu-id="c86eb-153">Remove a tile</span></span>
<span data-ttu-id="c86eb-154">tooremove um bloco, navegue toohello exibição de meu painel e clique em **personalizar** tooenter no modo de personalização.</span><span class="sxs-lookup"><span data-stu-id="c86eb-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="c86eb-155">Bloco Olá selecione desejado tooremove e no painel à direita da saudação selecione **remover bloco**.</span><span class="sxs-lookup"><span data-stu-id="c86eb-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Remover um bloco](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="c86eb-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c86eb-157">Next steps</span></span>
* <span data-ttu-id="c86eb-158">Criar [alertas](log-analytics-alerts.md) em notificações de toogenerate de análise de Log e tooremediate problemas.</span><span class="sxs-lookup"><span data-stu-id="c86eb-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
