---
title: Investigar e compartilhar dados de uso com Workbooks interativas no Azure Application Insights | Microsoft Docs
description: "Análise demográfica dos usuários de seu aplicativo Web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="47023-103">Investigar e compartilhar dados de uso com pastas de trabalho interativas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="47023-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="47023-104">As pastas de trabalho combinam as visualizações de dados do [Azure Application Insights](app-insights-overview.md), as [consultas do Analytics](app-insights-analytics.md) e textos em documentos interativos.</span><span class="sxs-lookup"><span data-stu-id="47023-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="47023-105">As pastas de trabalho são editáveis por outros membros da equipe com acesso ao mesmo recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="47023-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="47023-106">Isso significa que as consultas e os controles usados para criar uma pasta de trabalho estão disponíveis para outras pessoas que estão lendo a pasta de trabalho, facilitando a exploração, extensão e verificação de erros.</span><span class="sxs-lookup"><span data-stu-id="47023-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="47023-107">As pastas de trabalho são úteis para cenários como:</span><span class="sxs-lookup"><span data-stu-id="47023-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="47023-108">Exploração do uso do aplicativo quando você não sabe as métricas de interesse antecipadamente: números de usuários, taxas de retenção, taxas de conversão, etc. Ao contrário de outras ferramentas de análise de uso do Application Insights, as pastas de trabalho permitem combinar vários tipos de visualizações e análises, tornando-as excelentes para esse tipo de exploração de forma livre.</span><span class="sxs-lookup"><span data-stu-id="47023-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="47023-109">Explicar para sua equipe sobre o desempenho de um recurso recém-liberado, mostrando contagens de usuário para as principais interações e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="47023-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="47023-110">Compartilhar os resultados de um experimento A/B no aplicativo com outros membros de sua equipe.</span><span class="sxs-lookup"><span data-stu-id="47023-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="47023-111">Você pode explicar as metas do experimento com um texto e, depois, mostrar cada métrica de uso e consulta do Analytics usada para avaliar o experimento, junto com textos explicativos claros que indicam se cada métrica estava acima ou abaixo da meta.</span><span class="sxs-lookup"><span data-stu-id="47023-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="47023-112">Relatar o impacto de uma interrupção no uso do aplicativo, combinando dados, explicação de texto e uma discussão das próximas etapas para prevenir interrupções no futuro.</span><span class="sxs-lookup"><span data-stu-id="47023-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="47023-113">O recurso do Application Insights deve conter exibições de página ou eventos personalizados para usar as pastas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47023-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="47023-114">[Saiba como configurar seu aplicativo para coletar exibições de página automaticamente com o SDK do JavaScript do Application Insights](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="47023-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="47023-115">Editando, reorganizando, clonando e excluindo seções da pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="47023-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="47023-116">Uma pasta de trabalho é composta por seções: visualizações de uso editáveis de forma independente, gráficos, tabelas, textos ou resultados de consultas do Analytics.</span><span class="sxs-lookup"><span data-stu-id="47023-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="47023-117">Para editar o conteúdo de uma seção da pasta de trabalho, clique no botão **Editar** abaixo e à direita da seção da pasta de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47023-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Controles de edição da seção Pastas de Trabalho do Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="47023-119">Quando terminar de editar uma seção, clique em **Edição Concluída** no canto inferior esquerdo da seção.</span><span class="sxs-lookup"><span data-stu-id="47023-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="47023-120">Para criar uma duplicata de uma seção, clique no ícone **Clonar esta seção**.</span><span class="sxs-lookup"><span data-stu-id="47023-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="47023-121">Criar seções duplicadas é uma ótima forma de iterar em uma consulta sem perder as iterações anteriores.</span><span class="sxs-lookup"><span data-stu-id="47023-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="47023-122">Para mover uma seção para cima em uma pasta de trabalho, clique no ícone **Mover para cima** ou **Mover para baixo**.</span><span class="sxs-lookup"><span data-stu-id="47023-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="47023-123">Para remover uma seção permanentemente, clique no ícone **Remover**.</span><span class="sxs-lookup"><span data-stu-id="47023-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="47023-124">Adicionando seções de visualização de dados de uso</span><span class="sxs-lookup"><span data-stu-id="47023-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="47023-125">As pastas de trabalho oferecem quatro tipos de visualizações internas de análise de uso.</span><span class="sxs-lookup"><span data-stu-id="47023-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="47023-126">Cada uma delas responde a uma pergunta comum sobre o uso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47023-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="47023-127">Para adicionar tabelas e gráficos além dessas quatro seções, adicione seções de consulta do Analytics (veja abaixo).</span><span class="sxs-lookup"><span data-stu-id="47023-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="47023-128">Para adicionar uma seção Usuários, Sessões, Eventos ou Retenção à pasta de trabalho, use o botão **Adicionar Usuários** ou outro botão correspondente na parte inferior da pasta de trabalho ou na parte inferior de qualquer seção.</span><span class="sxs-lookup"><span data-stu-id="47023-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Seção Usuários no Workbooks](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="47023-130">As seções **Usuários** respondem à pergunta “Quantos usuários exibiram alguma página ou usaram algum recurso de meu site?”</span><span class="sxs-lookup"><span data-stu-id="47023-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="47023-131">As seções **Sessões** respondem à pergunta “Quantas sessões os usuários gastaram exibindo alguma página ou usando algum recurso de meu site?”</span><span class="sxs-lookup"><span data-stu-id="47023-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="47023-132">As seções **Eventos** respondem à pergunta “Quantas vezes os usuários exibiram alguma página ou usaram algum recurso de meu site?”</span><span class="sxs-lookup"><span data-stu-id="47023-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="47023-133">Cada um desses três tipos de seção oferece os mesmos conjuntos de controles e visualizações:</span><span class="sxs-lookup"><span data-stu-id="47023-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="47023-134">Saiba mais sobre como editar as seções Usuários, Sessões e Eventos</span><span class="sxs-lookup"><span data-stu-id="47023-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="47023-135">Ative/desative o gráfico principal, as grades de histograma, as informações automáticas e as visualizações de usuários de exemplo usando as caixas de seleção **Mostrar Gráfico**, **Mostrar Grade**, **Mostrar Informações** e **Amostra Destes Usuários** na parte superior de cada seção.</span><span class="sxs-lookup"><span data-stu-id="47023-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Seção Retenção no Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="47023-137">As seções **Retenção** respondem à pergunta: “Das pessoas que exibiram alguma página ou usaram algum recurso em um dia ou uma semana, quantas voltaram no dia ou na semana seguinte?”</span><span class="sxs-lookup"><span data-stu-id="47023-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="47023-138">Saiba mais sobre como editar as seções Retenção</span><span class="sxs-lookup"><span data-stu-id="47023-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="47023-139">Ative/desative o gráfico opcional Retenção Geral usando a caixa de seleção **Mostrar gráfico de retenção geral** na parte superior da seção.</span><span class="sxs-lookup"><span data-stu-id="47023-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="47023-140">Adicionando as seções do Analytics do Application Insights</span><span class="sxs-lookup"><span data-stu-id="47023-140">Adding Application Insights Analytics sections</span></span>

![Seção do Analytics no Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="47023-142">Para adicionar uma seção de consulta do Analytics do Application Insights à pasta de trabalho, use o botão **Adicionar consulta do Analytics** na parte inferior da pasta de trabalho ou na parte inferior de qualquer seção.</span><span class="sxs-lookup"><span data-stu-id="47023-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="47023-143">As seções de consulta do Analytics permitem que você adicione consultas arbitrárias dos dados do Application Insights a pastas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47023-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="47023-144">Essa flexibilidade indica que as seções de consulta do Analytics devem ser a opção para a qual você deve ir para responder a qualquer pergunta sobre seu site que não seja as quatro listadas acima de Usuários, Sessões, Eventos e Retenção, como:</span><span class="sxs-lookup"><span data-stu-id="47023-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="47023-145">Quantas exceções seu site gerou durante o mesmo período como um declínio no uso?</span><span class="sxs-lookup"><span data-stu-id="47023-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="47023-146">Qual foi a distribuição dos tempos de carregamento de página para os usuários que exibiram alguma página?</span><span class="sxs-lookup"><span data-stu-id="47023-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="47023-147">Quantos usuários exibiram algum conjunto de páginas no site, mas não algum outro conjunto de páginas?</span><span class="sxs-lookup"><span data-stu-id="47023-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="47023-148">Isso poderá ser útil para entender se você tiver clusters de usuários que usam diferentes subconjuntos da funcionalidade do site (use o operador `join` com o modificador `kind=leftanti` na linguagem de consulta do Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="47023-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="47023-149">Use a [referência de linguagem de consulta do Log Analytics](https://docs.loganalytics.io/) para saber mais sobre como escrever consultas.</span><span class="sxs-lookup"><span data-stu-id="47023-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="47023-150">Adicionando texto e seções de Markdown</span><span class="sxs-lookup"><span data-stu-id="47023-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="47023-151">Adicionar cabeçalhos, explicações e comentários às pastas de trabalho ajuda a transformar um conjunto de tabelas e gráficos em uma narrativa.</span><span class="sxs-lookup"><span data-stu-id="47023-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="47023-152">As seções de texto nas pastas de trabalho dão suporte à [sintaxe de Markdown](https://daringfireball.net/projects/markdown/) na formatação de texto, como cabeçalhos, negrito, itálico e listas com marcadores.</span><span class="sxs-lookup"><span data-stu-id="47023-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="47023-153">Para adicionar uma seção de texto à pasta de trabalho, use o botão **Adicionar texto** na parte inferior da pasta de trabalho ou na parte inferior de qualquer seção.</span><span class="sxs-lookup"><span data-stu-id="47023-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="47023-154">Salvando e compartilhando pastas de trabalho com sua equipe</span><span class="sxs-lookup"><span data-stu-id="47023-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="47023-155">As pastas de trabalho são salvas em um recurso do Application Insights, na seção **Meus Relatórios**, que é particular a você ou na seção **Relatórios Compartilhados**, que é acessível a todos com acesso ao recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="47023-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="47023-156">Para exibir todas as pastas de trabalho no recurso, clique no botão **Abrir** na barra de ações.</span><span class="sxs-lookup"><span data-stu-id="47023-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="47023-157">Para compartilhar uma pasta de trabalho que atualmente está em **Meus Relatórios**:</span><span class="sxs-lookup"><span data-stu-id="47023-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="47023-158">Clique em **Abrir** na barra de ações</span><span class="sxs-lookup"><span data-stu-id="47023-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="47023-159">Clique no botão “...” ao lado da pasta de trabalho que você deseja compartilhar</span><span class="sxs-lookup"><span data-stu-id="47023-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="47023-160">Clique em **Mover para Relatórios Compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="47023-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="47023-161">Para compartilhar uma pasta de trabalho com um link ou por email, clique em **Compartilhar** na barra de ações.</span><span class="sxs-lookup"><span data-stu-id="47023-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="47023-162">Tenha em mente que os destinatários do link precisam ter acesso a esse recurso no portal do Azure para exibir a pasta de trabalho.</span><span class="sxs-lookup"><span data-stu-id="47023-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="47023-163">Para fazer edições, os destinatários precisam de, pelo menos, permissões de Colaborador ao recurso.</span><span class="sxs-lookup"><span data-stu-id="47023-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="47023-164">Para fixar um link em uma pasta de trabalho em um Painel do Azure:</span><span class="sxs-lookup"><span data-stu-id="47023-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="47023-165">Clique em **Abrir** na barra de ações</span><span class="sxs-lookup"><span data-stu-id="47023-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="47023-166">Clique no botão “...” ao lado da pasta de trabalho que você deseja fixar</span><span class="sxs-lookup"><span data-stu-id="47023-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="47023-167">Clique em **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="47023-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47023-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47023-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="47023-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47023-169">Next steps</span></span>
- <span data-ttu-id="47023-170">Para habilitar as experiências de uso, comece enviando [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="47023-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="47023-171">Se você já envia eventos personalizados ou exibições de página, explore as ferramentas de uso para saber como os usuários utilizam o seu serviço.</span><span class="sxs-lookup"><span data-stu-id="47023-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="47023-172">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="47023-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="47023-173">Funis</span><span class="sxs-lookup"><span data-stu-id="47023-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="47023-174">Retenção</span><span class="sxs-lookup"><span data-stu-id="47023-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="47023-175">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="47023-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="47023-176">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="47023-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
