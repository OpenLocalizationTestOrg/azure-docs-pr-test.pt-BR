---
title: "aaaInteract com relatórios usando Olá API JavaScript | Microsoft Docs"
description: "Power BI inserido, interagir com relatórios usando Olá API JavaScript"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="9c015-103">Interagir com relatórios do Power BI usando Olá API JavaScript</span><span class="sxs-lookup"><span data-stu-id="9c015-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="9c015-104">Olá API JavaScript do Power BI permite que você tooeasily inserir relatórios do Power BI em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9c015-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="9c015-105">Com a API do hello, seus aplicativos podem interagir programaticamente com elementos de relatório diferente como páginas e filtros.</span><span class="sxs-lookup"><span data-stu-id="9c015-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="9c015-106">Essa interatividade faz com que os relatórios do Power BI sejam uma parte mais integrada do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9c015-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="9c015-107">Você pode inserir um relatório do Power BI em seu aplicativo usando um iframe hospedado como parte do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9c015-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="9c015-108">Olá iframe funciona como um limite entre seu aplicativo e o relatório de saudação, como você pode ver no Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c015-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Power BI embedded iframe sem API do Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="9c015-110">Olá iframe torna Olá inserindo um processo muito mais fácil, mas sem Olá Olá de API JavaScript relatório e seu aplicativo não podem interagir entre si.</span><span class="sxs-lookup"><span data-stu-id="9c015-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="9c015-111">Esta falta de interação pode facilitar a sensação relatório Olá realmente não é parte de um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9c015-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="9c015-112">aplicativo e relatório Olá precisam realmente toocommunicate e para trás, como Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c015-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Power BI embedded iframe com API do Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="9c015-114">Olá API JavaScript do Power BI permite que você o código de toowrite que pode passar com segurança por limite de iframe hello.</span><span class="sxs-lookup"><span data-stu-id="9c015-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="9c015-115">Isso permite que seu aplicativo tooprogrammatically executar uma ação em um relatório e toolisten para eventos de ações que os usuários fazem no relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c015-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="9c015-116">O que você pode fazer com hello API JavaScript do Power BI?</span><span class="sxs-lookup"><span data-stu-id="9c015-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="9c015-117">Com hello API JavaScript, você pode gerenciar relatórios, navegue toopages em um relatório, filtrar um relatório e tratar eventos de inserção.</span><span class="sxs-lookup"><span data-stu-id="9c015-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="9c015-118">Olá diagrama a seguir mostra estrutura Olá Olá API.</span><span class="sxs-lookup"><span data-stu-id="9c015-118">hello following diagram shows hello structure of hello API.</span></span>

![Diagrama da API JavaScript do Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="9c015-120">Gerenciar relatórios</span><span class="sxs-lookup"><span data-stu-id="9c015-120">Manage reports</span></span>
<span data-ttu-id="9c015-121">Olá API Javascript permite que você toomanage comportamento no nível de página e relatório hello:</span><span class="sxs-lookup"><span data-stu-id="9c015-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="9c015-122">Inserir um relatório específico do Power BI com segurança em seu aplicativo - tente Olá [incorporar o aplicativo de demonstração](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="9c015-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="9c015-123">Definir token de acesso</span><span class="sxs-lookup"><span data-stu-id="9c015-123">Set access token</span></span>
* <span data-ttu-id="9c015-124">Configurar o relatório de saudação</span><span class="sxs-lookup"><span data-stu-id="9c015-124">Configure hello report</span></span>
  * <span data-ttu-id="9c015-125">Habilitar e desabilitar o painel de filtro hello e painel de navegação de página - tente Olá [atualizar o aplicativo de demonstração de configurações](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="9c015-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="9c015-126">Definir padrões para páginas e filtros - tente Olá [demonstração do conjunto de padrões](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="9c015-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="9c015-127">Entrar e sair do modo de tela inteira</span><span class="sxs-lookup"><span data-stu-id="9c015-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="9c015-128">Saiba mais sobre como inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="9c015-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="9c015-129">Navegue toopages em um relatório</span><span class="sxs-lookup"><span data-stu-id="9c015-129">Navigate toopages in a report</span></span>
<span data-ttu-id="9c015-130">Olá API JavaScript enbales você toodiscover todas as páginas em uma página atual de Olá do relatório e tooset.</span><span class="sxs-lookup"><span data-stu-id="9c015-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="9c015-131">Tente Olá [aplicativo de demonstração de navegação](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="9c015-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="9c015-132">Saiba mais sobre a navegação de página</span><span class="sxs-lookup"><span data-stu-id="9c015-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="9c015-133">Filtrar um relatório</span><span class="sxs-lookup"><span data-stu-id="9c015-133">Filter a report</span></span>
<span data-ttu-id="9c015-134">Olá API JavaScript fornece básicos e avançados recursos de relatórios inseridos e páginas de relatório de filtragem.</span><span class="sxs-lookup"><span data-stu-id="9c015-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="9c015-135">Tente Olá [filtragem de aplicativo de demonstração](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)e examinar alguns códigos introdução aqui.</span><span class="sxs-lookup"><span data-stu-id="9c015-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="9c015-136">Filtros básicos</span><span class="sxs-lookup"><span data-stu-id="9c015-136">Basic filters</span></span>
<span data-ttu-id="9c015-137">Um filtro básico é colocado em um coluna ou nível hierárquico e contém uma lista de valores tooinclude ou excluir.</span><span class="sxs-lookup"><span data-stu-id="9c015-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="9c015-138">Filtros avançados</span><span class="sxs-lookup"><span data-stu-id="9c015-138">Advanced filters</span></span>
<span data-ttu-id="9c015-139">Filtros avançados usam o operador lógico hello e ou ou e aceitar uma ou duas condições, cada um com suas próprias operador e um valor.</span><span class="sxs-lookup"><span data-stu-id="9c015-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="9c015-140">As condições com suporte são:</span><span class="sxs-lookup"><span data-stu-id="9c015-140">Supported conditions are:</span></span>

* <span data-ttu-id="9c015-141">Nenhum</span><span class="sxs-lookup"><span data-stu-id="9c015-141">None</span></span>
* <span data-ttu-id="9c015-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="9c015-142">LessThan</span></span>
* <span data-ttu-id="9c015-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="9c015-143">LessThanOrEqual</span></span>
* <span data-ttu-id="9c015-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="9c015-144">GreaterThan</span></span>
* <span data-ttu-id="9c015-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="9c015-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="9c015-146">Contém:</span><span class="sxs-lookup"><span data-stu-id="9c015-146">Contains</span></span>
* <span data-ttu-id="9c015-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="9c015-147">DoesNotContain</span></span>
* <span data-ttu-id="9c015-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="9c015-148">StartsWith</span></span>
* <span data-ttu-id="9c015-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="9c015-149">DoesNotStartWith</span></span>
* <span data-ttu-id="9c015-150">Is</span><span class="sxs-lookup"><span data-stu-id="9c015-150">Is</span></span>
* <span data-ttu-id="9c015-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="9c015-151">IsNot</span></span>
* <span data-ttu-id="9c015-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="9c015-152">IsBlank</span></span>
* <span data-ttu-id="9c015-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="9c015-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="9c015-154">Saiba mais sobre filtragem</span><span class="sxs-lookup"><span data-stu-id="9c015-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="9c015-155">Manipulação de eventos</span><span class="sxs-lookup"><span data-stu-id="9c015-155">Handling events</span></span>
<span data-ttu-id="9c015-156">Além disso toosending informações em iframe hello, seu aplicativo pode também receber informações sobre Olá eventos provenientes iframe Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c015-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="9c015-157">Inserir</span><span class="sxs-lookup"><span data-stu-id="9c015-157">Embed</span></span>
  * <span data-ttu-id="9c015-158">carregado</span><span class="sxs-lookup"><span data-stu-id="9c015-158">loaded</span></span>
  * <span data-ttu-id="9c015-159">error</span><span class="sxs-lookup"><span data-stu-id="9c015-159">error</span></span>
* <span data-ttu-id="9c015-160">Relatórios</span><span class="sxs-lookup"><span data-stu-id="9c015-160">Reports</span></span>
  * <span data-ttu-id="9c015-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="9c015-161">pageChanged</span></span>
  * <span data-ttu-id="9c015-162">dataSelected (em breve)</span><span class="sxs-lookup"><span data-stu-id="9c015-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="9c015-163">Saiba mais sobre a manipulação de eventos</span><span class="sxs-lookup"><span data-stu-id="9c015-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="9c015-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c015-164">Next steps</span></span>
<span data-ttu-id="9c015-165">Para obter mais informações sobre Olá API JavaScript do Power BI, confira Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c015-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="9c015-166">Wiki da API JavaScript</span><span class="sxs-lookup"><span data-stu-id="9c015-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="9c015-167">Referência de modelo de objeto</span><span class="sxs-lookup"><span data-stu-id="9c015-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="9c015-168">Exemplos</span><span class="sxs-lookup"><span data-stu-id="9c015-168">Samples</span></span>
  * [<span data-ttu-id="9c015-169">Angular</span><span class="sxs-lookup"><span data-stu-id="9c015-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="9c015-170">Ember</span><span class="sxs-lookup"><span data-stu-id="9c015-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="9c015-171">Demonstração ao vivo</span><span class="sxs-lookup"><span data-stu-id="9c015-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

