---
title: "Interagir com relatórios usando a API JavaScript | Microsoft Docs"
description: "Power BI Embedded, interagir com relatórios usando a API JavaScript"
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
ms.openlocfilehash: 500462ac835674d80650c02aa7fc629b4a975857
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a><span data-ttu-id="697c4-103">Interagir com relatórios do Power BI usando a API JavaScript</span><span class="sxs-lookup"><span data-stu-id="697c4-103">Interact with Power BI reports using the JavaScript API</span></span>
<span data-ttu-id="697c4-104">A API JavaScript do Power BI permite que você insira relatórios do Power BI com facilidade em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="697c4-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span></span> <span data-ttu-id="697c4-105">Com a API, seus aplicativos podem interagir programaticamente com diferentes elementos do relatório, como páginas e filtros.</span><span class="sxs-lookup"><span data-stu-id="697c4-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="697c4-106">Essa interatividade faz com que os relatórios do Power BI sejam uma parte mais integrada do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="697c4-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="697c4-107">Você pode inserir um relatório do Power BI em seu aplicativo usando um iframe hospedado como parte do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="697c4-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span></span> <span data-ttu-id="697c4-108">O iframe age como um limite entre seu aplicativo e o relatório, como você pode ver na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="697c4-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span></span> 

![Power BI embedded iframe sem API do Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="697c4-110">O iframe torna o processo de incorporação muito mais fácil, mas sem a API JavaScript o relatório e o seu aplicativo não podem interagir entre si.</span><span class="sxs-lookup"><span data-stu-id="697c4-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span></span> <span data-ttu-id="697c4-111">Essa falta de interação pode dar impressão de que o relatório não faz realmente parte do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="697c4-111">This lack of interaction can make it feel like the report is not really part of the application.</span></span> <span data-ttu-id="697c4-112">O relatório e o aplicativo realmente precisam se comunicar, como na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="697c4-112">The report and application really need to communicate back and forth, as in the following image.</span></span>

![Power BI embedded iframe com API do Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="697c4-114">A API JavaScript do Power BI permite que você escreva código que possa passar com segurança pelo limite do iframe.</span><span class="sxs-lookup"><span data-stu-id="697c4-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span></span> <span data-ttu-id="697c4-115">Isso permite que seu aplicativo execute programaticamente uma ação em um relatório e escute eventos de ações que os usuários fazem no relatório.</span><span class="sxs-lookup"><span data-stu-id="697c4-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span></span>

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a><span data-ttu-id="697c4-116">O que você pode fazer com a API JavaScript do Power BI?</span><span class="sxs-lookup"><span data-stu-id="697c4-116">What can you do with the Power BI JavaScript API?</span></span>
<span data-ttu-id="697c4-117">Com a API JavaScript você pode gerenciar relatórios, navegar pelas páginas de um relatório, filtrar um relatório e manipular eventos de inserção.</span><span class="sxs-lookup"><span data-stu-id="697c4-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="697c4-118">O diagrama a seguir mostra a estrutura da API.</span><span class="sxs-lookup"><span data-stu-id="697c4-118">The following diagram shows the structure of the API.</span></span>

![Diagrama da API JavaScript do Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="697c4-120">Gerenciar relatórios</span><span class="sxs-lookup"><span data-stu-id="697c4-120">Manage reports</span></span>
<span data-ttu-id="697c4-121">A API Javascript permite que você gerencie o comportamento no nível de página e de relatório:</span><span class="sxs-lookup"><span data-stu-id="697c4-121">The Javascript API enables you to manage behavior at the report and page level:</span></span>

* <span data-ttu-id="697c4-122">Insira um Relatório específico do Power BI com segurança em seu aplicativo - experimente o [aplicativo de demonstração inserção](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="697c4-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="697c4-123">Definir token de acesso</span><span class="sxs-lookup"><span data-stu-id="697c4-123">Set access token</span></span>
* <span data-ttu-id="697c4-124">Configurar o relatório</span><span class="sxs-lookup"><span data-stu-id="697c4-124">Configure the report</span></span>
  * <span data-ttu-id="697c4-125">Habilite e desabilite o painel de filtro e o painel de navegação de página - experimente o [aplicativo de demonstração de configurações de atualização](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="697c4-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="697c4-126">Defina padrões para páginas e filtros - experimente o [aplicativo para definir padrões](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="697c4-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="697c4-127">Entrar e sair do modo de tela inteira</span><span class="sxs-lookup"><span data-stu-id="697c4-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="697c4-128">Saiba mais sobre como inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="697c4-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a><span data-ttu-id="697c4-129">Navegar pelas páginas de um relatório</span><span class="sxs-lookup"><span data-stu-id="697c4-129">Navigate to pages in a report</span></span>
<span data-ttu-id="697c4-130">A API JavaScript permite que você descubra todas as páginas de um relatório e defina a página atual.</span><span class="sxs-lookup"><span data-stu-id="697c4-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span></span> <span data-ttu-id="697c4-131">Experimente o [aplicativo de demonstração de navegação](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="697c4-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="697c4-132">Saiba mais sobre a navegação de página</span><span class="sxs-lookup"><span data-stu-id="697c4-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="697c4-133">Filtrar um relatório</span><span class="sxs-lookup"><span data-stu-id="697c4-133">Filter a report</span></span>
<span data-ttu-id="697c4-134">A API JavaScript fornece recursos básicos e avançados de filtragem para relatórios inseridos e páginas de relatório.</span><span class="sxs-lookup"><span data-stu-id="697c4-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="697c4-135">Experimente o [aplicativo de demonstração de filtragem](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)e examine alguns códigos introdutórios aqui.</span><span class="sxs-lookup"><span data-stu-id="697c4-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="697c4-136">Filtros básicos</span><span class="sxs-lookup"><span data-stu-id="697c4-136">Basic filters</span></span>
<span data-ttu-id="697c4-137">Um filtro básico é colocado em uma coluna ou nível hierárquico e contém uma lista de valores a serem incluídos ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="697c4-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span></span>

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


#### <a name="advanced-filters"></a><span data-ttu-id="697c4-138">Filtros avançados</span><span class="sxs-lookup"><span data-stu-id="697c4-138">Advanced filters</span></span>
<span data-ttu-id="697c4-139">Os filtros avançados usam o operador lógico E ou OU e aceitam uma ou duas condições, cada uma com seus próprios operador e valor.</span><span class="sxs-lookup"><span data-stu-id="697c4-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="697c4-140">As condições com suporte são:</span><span class="sxs-lookup"><span data-stu-id="697c4-140">Supported conditions are:</span></span>

* <span data-ttu-id="697c4-141">Nenhum</span><span class="sxs-lookup"><span data-stu-id="697c4-141">None</span></span>
* <span data-ttu-id="697c4-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="697c4-142">LessThan</span></span>
* <span data-ttu-id="697c4-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="697c4-143">LessThanOrEqual</span></span>
* <span data-ttu-id="697c4-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="697c4-144">GreaterThan</span></span>
* <span data-ttu-id="697c4-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="697c4-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="697c4-146">Contém:</span><span class="sxs-lookup"><span data-stu-id="697c4-146">Contains</span></span>
* <span data-ttu-id="697c4-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="697c4-147">DoesNotContain</span></span>
* <span data-ttu-id="697c4-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="697c4-148">StartsWith</span></span>
* <span data-ttu-id="697c4-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="697c4-149">DoesNotStartWith</span></span>
* <span data-ttu-id="697c4-150">Is</span><span class="sxs-lookup"><span data-stu-id="697c4-150">Is</span></span>
* <span data-ttu-id="697c4-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="697c4-151">IsNot</span></span>
* <span data-ttu-id="697c4-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="697c4-152">IsBlank</span></span>
* <span data-ttu-id="697c4-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="697c4-153">IsNotBlank</span></span>

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
[<span data-ttu-id="697c4-154">Saiba mais sobre filtragem</span><span class="sxs-lookup"><span data-stu-id="697c4-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="697c4-155">Manipulação de eventos</span><span class="sxs-lookup"><span data-stu-id="697c4-155">Handling events</span></span>
<span data-ttu-id="697c4-156">Além de enviar informações para o iframe, seu aplicativo também pode receber informações sobre os seguintes eventos provenientes do iframe:</span><span class="sxs-lookup"><span data-stu-id="697c4-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span></span>

* <span data-ttu-id="697c4-157">Inserir</span><span class="sxs-lookup"><span data-stu-id="697c4-157">Embed</span></span>
  * <span data-ttu-id="697c4-158">carregado</span><span class="sxs-lookup"><span data-stu-id="697c4-158">loaded</span></span>
  * <span data-ttu-id="697c4-159">error</span><span class="sxs-lookup"><span data-stu-id="697c4-159">error</span></span>
* <span data-ttu-id="697c4-160">Relatórios</span><span class="sxs-lookup"><span data-stu-id="697c4-160">Reports</span></span>
  * <span data-ttu-id="697c4-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="697c4-161">pageChanged</span></span>
  * <span data-ttu-id="697c4-162">dataSelected (em breve)</span><span class="sxs-lookup"><span data-stu-id="697c4-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="697c4-163">Saiba mais sobre a manipulação de eventos</span><span class="sxs-lookup"><span data-stu-id="697c4-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="697c4-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="697c4-164">Next steps</span></span>
<span data-ttu-id="697c4-165">Para saber mais sobre a API JavaScript do Power BI, confira os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="697c4-165">For more information about the Power BI JavaScript API, check out the following links:</span></span>

* [<span data-ttu-id="697c4-166">Wiki da API JavaScript</span><span class="sxs-lookup"><span data-stu-id="697c4-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="697c4-167">Referência de modelo de objeto</span><span class="sxs-lookup"><span data-stu-id="697c4-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="697c4-168">Exemplos</span><span class="sxs-lookup"><span data-stu-id="697c4-168">Samples</span></span>
  * [<span data-ttu-id="697c4-169">Angular</span><span class="sxs-lookup"><span data-stu-id="697c4-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="697c4-170">Ember</span><span class="sxs-lookup"><span data-stu-id="697c4-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="697c4-171">Demonstração ao vivo</span><span class="sxs-lookup"><span data-stu-id="697c4-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

