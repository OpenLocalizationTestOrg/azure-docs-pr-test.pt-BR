---
title: "relatórios de aaaSave no Azure Power BI inserido | Microsoft Docs"
description: "Saiba como toosave relatórios no Power BI inserido. Isso requer permissões apropriadas na ordem toowork com êxito."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="ff76f-104">Salvar relatórios no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ff76f-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="ff76f-105">Saiba como toosave relatórios no Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="ff76f-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="ff76f-106">Isso requer permissões apropriadas na ordem toowork com êxito.</span><span class="sxs-lookup"><span data-stu-id="ff76f-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="ff76f-107">No Power BI Embedded, você pode editar os relatórios existentes e salvá-los.</span><span class="sxs-lookup"><span data-stu-id="ff76f-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="ff76f-108">Você também pode criar um novo relatório e salve como um novo toocreate de relatório um.</span><span class="sxs-lookup"><span data-stu-id="ff76f-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="ff76f-109">Em ordem toosave um relatório é necessário primeiro toocreate um token para relatório específico de saudação com escopos de saudação à direita:</span><span class="sxs-lookup"><span data-stu-id="ff76f-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="ff76f-110">tooenable salvar Report.ReadWrite escopo é necessária</span><span class="sxs-lookup"><span data-stu-id="ff76f-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="ff76f-111">tooenable Salvar como, Report.Read e Workspace.Report.Copy escopos são necessários</span><span class="sxs-lookup"><span data-stu-id="ff76f-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="ff76f-112">tooenable salvar e salvar como, Report.ReadWrite e Workspace.Report.Copy são é necessário</span><span class="sxs-lookup"><span data-stu-id="ff76f-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="ff76f-113">Respectivamente na saudação de tooenable ordem direita salvar ou salvar como botões no menu Arquivo, você precisa tooprovide Olá direita permissão na configuração de inserção de saudação quando você incorporar Olá relatório:</span><span class="sxs-lookup"><span data-stu-id="ff76f-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="ff76f-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="ff76f-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="ff76f-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="ff76f-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="ff76f-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="ff76f-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="ff76f-117">O token de acesso também precisa de escopos apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="ff76f-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="ff76f-118">Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="ff76f-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="ff76f-119">Inserir o relatório no modo de edição</span><span class="sxs-lookup"><span data-stu-id="ff76f-119">Embed report in edit mode</span></span>

<span data-ttu-id="ff76f-120">Vamos supor que você queira tooEmbed um relatório no modo de edição dentro de seu aplicativo, toodo então apenas passar propriedades do direito de saudação na configuração de inserção e chame powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="ff76f-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="ff76f-121">Você precisará toosupply permissões e um viewMode em Olá toosee de ordem salvar e salve como botões quando no modo de edição.</span><span class="sxs-lookup"><span data-stu-id="ff76f-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="ff76f-122">Para saber mais, confira [Detalhes de configuração do servidor de inserção](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="ff76f-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="ff76f-123">Por exemplo, no JavaScript:</span><span class="sxs-lookup"><span data-stu-id="ff76f-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
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

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="ff76f-124">Agora, um relatório será inserido em seu aplicativo no modo de edição.</span><span class="sxs-lookup"><span data-stu-id="ff76f-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="ff76f-125">Salvar relatório</span><span class="sxs-lookup"><span data-stu-id="ff76f-125">Save report</span></span>

<span data-ttu-id="ff76f-126">Depois que o modo com hello token à direita e permissões de edição de relatório de saudação Embbeding em você pode salvar o relatório de Olá menu arquivo hello ou de javascript:</span><span class="sxs-lookup"><span data-stu-id="ff76f-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="ff76f-127">Salvar como</span><span class="sxs-lookup"><span data-stu-id="ff76f-127">Save as</span></span>

```
// Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="ff76f-128">Um novo relatório é criado somente depois do uso de *salvar como*.</span><span class="sxs-lookup"><span data-stu-id="ff76f-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="ff76f-129">Depois de salvar hello, tela hello ainda mostra relatório antigo Olá Editar modo e não hello novo relatório.</span><span class="sxs-lookup"><span data-stu-id="ff76f-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="ff76f-130">Você precisará tooembed Olá novo relatório que foi criado.</span><span class="sxs-lookup"><span data-stu-id="ff76f-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="ff76f-131">Isso requer um novo token de acesso, já que eles são criados por relatório.</span><span class="sxs-lookup"><span data-stu-id="ff76f-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="ff76f-132">Em seguida, você precisará tooload Olá novo relatório após um *Salvar como*.</span><span class="sxs-lookup"><span data-stu-id="ff76f-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="ff76f-133">Isso é semelhante tooembedding qualquer relatório.</span><span class="sxs-lookup"><span data-stu-id="ff76f-133">This is similar tooembedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="ff76f-134">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ff76f-134">See also</span></span>

[<span data-ttu-id="ff76f-135">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="ff76f-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="ff76f-136">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="ff76f-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="ff76f-137">Criar um novo relatório de um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ff76f-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="ff76f-138">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ff76f-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="ff76f-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="ff76f-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="ff76f-140">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="ff76f-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="ff76f-141">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="ff76f-141">More questions?</span></span> [<span data-ttu-id="ff76f-142">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="ff76f-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

