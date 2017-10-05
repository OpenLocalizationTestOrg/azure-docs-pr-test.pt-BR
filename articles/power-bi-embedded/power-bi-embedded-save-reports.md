---
title: "Salvar relatórios no Azure Power BI Embedded | Microsoft Docs"
description: "Saiba como salvar relatórios no Power BI Embedded. Isso requer as permissões apropriadas para trabalhar com êxito."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ad895004cc2972f2ded81566186325a16d401151
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="94034-104">Salvar relatórios no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="94034-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="94034-105">Saiba como salvar relatórios no Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="94034-105">Learn how to save reports within Power BI embedded.</span></span> <span data-ttu-id="94034-106">Isso requer as permissões apropriadas para trabalhar com êxito.</span><span class="sxs-lookup"><span data-stu-id="94034-106">This requires proper permissions in order to work successfully.</span></span>

<span data-ttu-id="94034-107">No Power BI Embedded, você pode editar os relatórios existentes e salvá-los.</span><span class="sxs-lookup"><span data-stu-id="94034-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="94034-108">Você também pode criar um novo relatório e salvar como um novo relatório para criar um.</span><span class="sxs-lookup"><span data-stu-id="94034-108">You can also create a new report and save as a new report to create one.</span></span>

<span data-ttu-id="94034-109">Para salvar um relatório, você precisa primeiro criar um token para o relatório específico com os escopos certos:</span><span class="sxs-lookup"><span data-stu-id="94034-109">In order to save a report you first need to create a token for the specific report with the right scopes:</span></span>

* <span data-ttu-id="94034-110">Para habilitar salvar, o escopo Report.ReadWrite é necessário</span><span class="sxs-lookup"><span data-stu-id="94034-110">To enable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="94034-111">Para habilitar salvar como, os escopos Report.Read e Workspace.Report.Copy são necessários</span><span class="sxs-lookup"><span data-stu-id="94034-111">To enable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="94034-112">Para habilitar as ações salvar e salvar como, os escopos Report.ReadWrite e Workspace.Report.Copy são necessários</span><span class="sxs-lookup"><span data-stu-id="94034-112">To enable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="94034-113">Para habilitar os botões de salvar/salvar como certos no menu Arquivo, respectivamente, você precisa fornecer a permissão certa na configuração ao inserir o relatório:</span><span class="sxs-lookup"><span data-stu-id="94034-113">Respectively in order to enable the right save/save as buttons in file menu you need to provide the right permission in the Embed configuration when you Embed the report:</span></span>

* <span data-ttu-id="94034-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="94034-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="94034-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="94034-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="94034-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="94034-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="94034-117">O token de acesso também precisa dos escopos apropriados.</span><span class="sxs-lookup"><span data-stu-id="94034-117">Your access token also needs the appropriate scopes.</span></span> <span data-ttu-id="94034-118">Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="94034-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="94034-119">Inserir o relatório no modo de edição</span><span class="sxs-lookup"><span data-stu-id="94034-119">Embed report in edit mode</span></span>

<span data-ttu-id="94034-120">Digamos que você deseja inserir um relatório em modo de edição dentro de seu aplicativo, portanto, basta passar as propriedades certas na configuração de inserção e chamar powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="94034-120">Let's say you want to Embed a report in edit mode inside your app, to do so just pass the right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="94034-121">Você precisará fornecer permissões e um viewMode para ver os botões salvar e salvar como em modo de edição.</span><span class="sxs-lookup"><span data-stu-id="94034-121">You will need to supply permissions and a viewMode in order to see the save and save as buttons when in edit mode.</span></span> <span data-ttu-id="94034-122">Para saber mais, confira [Detalhes de configuração do servidor de inserção](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="94034-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="94034-123">Por exemplo, no JavaScript:</span><span class="sxs-lookup"><span data-stu-id="94034-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used to describe the what and how to embed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference to the embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed the report and display it within the div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="94034-124">Agora, um relatório será inserido em seu aplicativo no modo de edição.</span><span class="sxs-lookup"><span data-stu-id="94034-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="94034-125">Salvar relatório</span><span class="sxs-lookup"><span data-stu-id="94034-125">Save report</span></span>

<span data-ttu-id="94034-126">Depois de inserir o relatório no modo de edição com o token e permissões certos, você pode salvar o relatório do menu Arquivo ou do JavaScript:</span><span class="sxs-lookup"><span data-stu-id="94034-126">After Embbeding the report in edit mode with the right token and permissions you can save the report from the file menu or from javascript:</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="94034-127">Salvar como</span><span class="sxs-lookup"><span data-stu-id="94034-127">Save as</span></span>

```
// Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="94034-128">Um novo relatório é criado somente depois do uso de *salvar como*.</span><span class="sxs-lookup"><span data-stu-id="94034-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="94034-129">Depois de salvar, a tela ainda mostra o antigo relatório no modo de edição e não o novo relatório.</span><span class="sxs-lookup"><span data-stu-id="94034-129">After the save, the canvas is still showing the old report in edit mode and not the new report.</span></span> <span data-ttu-id="94034-130">Você precisará inserir o novo relatório que foi criado.</span><span class="sxs-lookup"><span data-stu-id="94034-130">You will need to embed the new report that was created.</span></span> <span data-ttu-id="94034-131">Isso requer um novo token de acesso, já que eles são criados por relatório.</span><span class="sxs-lookup"><span data-stu-id="94034-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="94034-132">Em seguida, você precisará carregar o novo relatório após um *salvar como*.</span><span class="sxs-lookup"><span data-stu-id="94034-132">You will then need to load the new report after a *save as*.</span></span> <span data-ttu-id="94034-133">Isso é semelhante à inserção de qualquer relatório.</span><span class="sxs-lookup"><span data-stu-id="94034-133">This is similar to embedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="94034-134">Consulte também</span><span class="sxs-lookup"><span data-stu-id="94034-134">See also</span></span>

[<span data-ttu-id="94034-135">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="94034-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="94034-136">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="94034-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="94034-137">Criar um novo relatório de um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="94034-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="94034-138">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="94034-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="94034-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="94034-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="94034-140">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="94034-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="94034-141">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="94034-141">More questions?</span></span> [<span data-ttu-id="94034-142">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="94034-142">Try the Power BI Community</span></span>](http://community.powerbi.com/)

