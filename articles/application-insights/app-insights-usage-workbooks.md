---
title: aaaInvestigate e compartilhamento de dados de uso com pastas de trabalho interativas no Azure Application Insights | Documentos da Microsoft
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
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="fa891-103">Investigar e compartilhar dados de uso com pastas de trabalho interativas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa891-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="fa891-104">As pastas de trabalho combinam as visualizações de dados do [Azure Application Insights](app-insights-overview.md), as [consultas do Analytics](app-insights-analytics.md) e textos em documentos interativos.</span><span class="sxs-lookup"><span data-stu-id="fa891-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="fa891-105">Pastas de trabalho são editáveis por outros membros da equipe com acesso toohello mesmo recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa891-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="fa891-106">Isso significa Olá controles e consultas usado toocreate uma pasta de trabalho são tooother disponível pessoas lendo a pasta de trabalho hello, tornando-os tooexplore fácil, estender e verificar se há erros.</span><span class="sxs-lookup"><span data-stu-id="fa891-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="fa891-107">As pastas de trabalho são úteis para cenários como:</span><span class="sxs-lookup"><span data-stu-id="fa891-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="fa891-108">Explorando o uso de saudação do seu aplicativo quando não souber com antecedência métricas de saudação de interesse: números de usuários, as taxas de retenção, taxas de conversão, etc. Ao contrário de outras ferramentas de análise de uso do Application Insights, as pastas de trabalho permitem combinar vários tipos de visualizações e análises, tornando-as excelentes para esse tipo de exploração de forma livre.</span><span class="sxs-lookup"><span data-stu-id="fa891-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="fa891-109">Explicar team tooyour como um recurso recém-lançado está funcionando, por usuário mostra contagens de interações de chave e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="fa891-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="fa891-110">Compartilhar os resultados de saudação de um A / B experiências em seu aplicativo com outros membros da equipe.</span><span class="sxs-lookup"><span data-stu-id="fa891-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="fa891-111">Você pode explicar metas Olá para Olá fazer experiências com texto e mostram cada métrica de uso e consulta de análise usado experiência de saudação tooevaluate, junto com as transferências de chamada claras para se cada métrica foi acima ou abaixo do destino.</span><span class="sxs-lookup"><span data-stu-id="fa891-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="fa891-112">Relatório impacto de saudação de uma interrupção no uso de saudação do seu aplicativo, combinando dados explicação de texto e uma discussão das interrupções de tooprevent etapas Avançar no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="fa891-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="fa891-113">O recurso do Application Insights deve conter modos de exibição de página ou pastas de trabalho de toouse eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="fa891-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="fa891-114">[Saiba como tooset sua página de toocollect aplicativo exibe automaticamente com hello SDK de JavaScript do Application Insights](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="fa891-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="fa891-115">Editando, reorganizando, clonando e excluindo seções da pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="fa891-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="fa891-116">Uma pasta de trabalho é composta por seções: visualizações de uso editáveis de forma independente, gráficos, tabelas, textos ou resultados de consultas do Analytics.</span><span class="sxs-lookup"><span data-stu-id="fa891-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="fa891-117">conteúdo de saudação tooedit de uma seção de pasta de trabalho, clique em Olá **editar** botão abaixo e toohello à direita da seção de pasta de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa891-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Controles de edição da seção Pastas de Trabalho do Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="fa891-119">Quando você terminar uma seção de edição, clique em **feito editando** na Olá inferior esquerda da seção de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa891-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="fa891-120">toocreate uma duplicata de uma seção, clique em Olá **clonar nesta seção** ícone.</span><span class="sxs-lookup"><span data-stu-id="fa891-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="fa891-121">Criando seções duplicadas é um tooiterate tooway grande em uma consulta sem perder iterações anteriores.</span><span class="sxs-lookup"><span data-stu-id="fa891-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="fa891-122">toomove uma seção em uma pasta de trabalho, clique em Olá **mover para cima** ou **mover para baixo** ícone.</span><span class="sxs-lookup"><span data-stu-id="fa891-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="fa891-123">tooremove uma seção permanentemente, clique em Olá **remover** ícone.</span><span class="sxs-lookup"><span data-stu-id="fa891-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="fa891-124">Adicionando seções de visualização de dados de uso</span><span class="sxs-lookup"><span data-stu-id="fa891-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="fa891-125">As pastas de trabalho oferecem quatro tipos de visualizações internas de análise de uso.</span><span class="sxs-lookup"><span data-stu-id="fa891-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="fa891-126">Cada responde a uma pergunta comum sobre o uso de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fa891-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="fa891-127">tooadd tabelas e gráficos diferentes quatro seções, adicione seções de consulta de análise (veja abaixo).</span><span class="sxs-lookup"><span data-stu-id="fa891-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="fa891-128">tooadd aos usuários, sessões, eventos ou retenção seção tooyour de pasta de trabalho, use Olá **adicionar usuários** ou outro botão correspondente na parte inferior da saudação da pasta de trabalho hello, ou na parte inferior da saudação de qualquer seção.</span><span class="sxs-lookup"><span data-stu-id="fa891-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![Seção Usuários no Workbooks](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="fa891-130">As seções **Usuários** respondem à pergunta “Quantos usuários exibiram alguma página ou usaram algum recurso de meu site?”</span><span class="sxs-lookup"><span data-stu-id="fa891-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="fa891-131">As seções **Sessões** respondem à pergunta “Quantas sessões os usuários gastaram exibindo alguma página ou usando algum recurso de meu site?”</span><span class="sxs-lookup"><span data-stu-id="fa891-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="fa891-132">As seções **Eventos** respondem à pergunta “Quantas vezes os usuários exibiram alguma página ou usaram algum recurso de meu site?”</span><span class="sxs-lookup"><span data-stu-id="fa891-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="fa891-133">Cada um desses tipos de três seção oferece Olá mesmos conjuntos de controles e visualizações:</span><span class="sxs-lookup"><span data-stu-id="fa891-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="fa891-134">Saiba mais sobre como editar as seções Usuários, Sessões e Eventos</span><span class="sxs-lookup"><span data-stu-id="fa891-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="fa891-135">Alternar de gráfico principal hello, grades de histograma, insights automática e visualizações de usuários de exemplo usando Olá **Mostrar gráfico**, **Mostrar grade de**, **Insights Mostrar**e **De esses usuários de exemplo** caixas de seleção na parte superior de saudação de cada seção.</span><span class="sxs-lookup"><span data-stu-id="fa891-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![Seção Retenção no Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="fa891-137">As seções **Retenção** respondem à pergunta: “Das pessoas que exibiram alguma página ou usaram algum recurso em um dia ou uma semana, quantas voltaram no dia ou na semana seguinte?”</span><span class="sxs-lookup"><span data-stu-id="fa891-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="fa891-138">Saiba mais sobre como editar as seções Retenção</span><span class="sxs-lookup"><span data-stu-id="fa891-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="fa891-139">Ativar/desativar Olá opcional retenção geral gráfico usando Olá **Mostrar gráfico de retenção geral** caixa de seleção na parte superior de saudação da seção de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa891-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="fa891-140">Adicionando as seções do Analytics do Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa891-140">Adding Application Insights Analytics sections</span></span>

![Seção do Analytics no Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="fa891-142">tooadd uma análise do aplicativo Insights consulta seção tooyour pasta de trabalho, use Olá **consulta analítica adicionar** botão na parte inferior da saudação da pasta de trabalho hello, ou na parte inferior da saudação de qualquer seção.</span><span class="sxs-lookup"><span data-stu-id="fa891-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="fa891-143">As seções de consulta do Analytics permitem que você adicione consultas arbitrárias dos dados do Application Insights a pastas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="fa891-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="fa891-144">Essa flexibilidade mostra seções de consulta de análise devem ser o go-toofor responder perguntas sobre seu site além daquele Olá quatro listados acima para usuários, sessões, eventos e retenção, como:</span><span class="sxs-lookup"><span data-stu-id="fa891-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="fa891-145">Como muitas exceções foram throw seu site durante a saudação mesmo tempo como uma recusa de uso?</span><span class="sxs-lookup"><span data-stu-id="fa891-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="fa891-146">Qual foi a distribuição de saudação de tempos de carregamento de página para que os usuários exibindo alguma página?</span><span class="sxs-lookup"><span data-stu-id="fa891-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="fa891-147">Quantos usuários exibiram algum conjunto de páginas no site, mas não algum outro conjunto de páginas?</span><span class="sxs-lookup"><span data-stu-id="fa891-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="fa891-148">Isso pode ser útil toounderstand se você tiver clusters de usuários que usam diferentes subconjuntos de funcionalidade do site (use Olá `join` operador com hello `kind=leftanti` modificador Olá linguagem de consulta de análise de Log).</span><span class="sxs-lookup"><span data-stu-id="fa891-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="fa891-149">Saudação de uso [referência de linguagem de consulta de análise de Log](https://docs.loganalytics.io/) toolearn mais sobre a escrita de consultas.</span><span class="sxs-lookup"><span data-stu-id="fa891-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="fa891-150">Adicionando texto e seções de Markdown</span><span class="sxs-lookup"><span data-stu-id="fa891-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="fa891-151">Adicionar títulos, explicações e pastas de trabalho comentários tooyour ajuda a transformar um conjunto de tabelas e gráficos em uma narrativa.</span><span class="sxs-lookup"><span data-stu-id="fa891-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="fa891-152">Suportam a seções de texto em pastas de trabalho Olá [sintaxe de Markdown](https://daringfireball.net/projects/markdown/) para formatação de texto, como títulos, negrito, itálico e listas com marcadores.</span><span class="sxs-lookup"><span data-stu-id="fa891-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="fa891-153">tooadd uma pasta de trabalho de tooyour seção texto, use Olá **adicionar texto** botão na parte inferior da saudação da pasta de trabalho hello, ou na parte inferior da saudação de qualquer seção.</span><span class="sxs-lookup"><span data-stu-id="fa891-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="fa891-154">Salvando e compartilhando pastas de trabalho com sua equipe</span><span class="sxs-lookup"><span data-stu-id="fa891-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="fa891-155">Pastas de trabalho são salvos em um recurso do Application Insights, em Olá **meus relatórios** seção tooyou privada ou em Olá **relatórios compartilhados** seção que é acessível tooeveryone com acesso toohello recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fa891-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="fa891-156">tooview todas as pastas de trabalho de saudação no recurso Olá, clique em Olá **abrir** botão na barra de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa891-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="fa891-157">tooshare uma pasta de trabalho está atualmente em **meus relatórios**:</span><span class="sxs-lookup"><span data-stu-id="fa891-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="fa891-158">Clique em **abrir** na barra de ação Olá</span><span class="sxs-lookup"><span data-stu-id="fa891-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="fa891-159">Clique no botão "…" hello ao lado da pasta de trabalho Olá deseja tooshare</span><span class="sxs-lookup"><span data-stu-id="fa891-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="fa891-160">Clique em **mover relatórios tooShared**.</span><span class="sxs-lookup"><span data-stu-id="fa891-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="fa891-161">tooshare uma pasta de trabalho com um link ou por meio de email, clique em **compartilhamento** na barra de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa891-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="fa891-162">Tenha em mente que os destinatários do link de saudação precisam acessar o recurso de toothis na pasta de trabalho de saudação do hello tooview portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa891-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="fa891-163">edições toomake, os destinatários precisarão pelo menos permissões de Colaborador para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa891-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="fa891-164">toopin um tooan de pasta de trabalho do link tooa painel do Azure:</span><span class="sxs-lookup"><span data-stu-id="fa891-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="fa891-165">Clique em **abrir** na barra de ação Olá</span><span class="sxs-lookup"><span data-stu-id="fa891-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="fa891-166">Clique no botão "…" hello ao lado da pasta de trabalho Olá deseja toopin</span><span class="sxs-lookup"><span data-stu-id="fa891-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="fa891-167">Clique em **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="fa891-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa891-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa891-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa891-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa891-169">Next steps</span></span>
- <span data-ttu-id="fa891-170">uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="fa891-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="fa891-171">Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="fa891-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="fa891-172">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="fa891-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="fa891-173">Funis</span><span class="sxs-lookup"><span data-stu-id="fa891-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="fa891-174">Retenção</span><span class="sxs-lookup"><span data-stu-id="fa891-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="fa891-175">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="fa891-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="fa891-176">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="fa891-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
