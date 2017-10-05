---
title: "Alternar entre o modo de exibição e modo de edição para relatórios no Azure Power BI Embedded | Microsoft Docs"
description: "Saiba como alternar entre o modo de exibição e modo de edição para seus relatórios no Power BI Embedded."
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
ms.openlocfilehash: f73bf05b41523a5833cc9366fb84cb7021b4b7a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="fc93a-103">Alternar entre o modo de exibição e modo de edição para seus relatórios no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="fc93a-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="fc93a-104">Saiba como alternar entre o modo de exibição e modo de edição para seus relatórios no Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="fc93a-104">Learn how to toggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="fc93a-105">Criação de um token de acesso</span><span class="sxs-lookup"><span data-stu-id="fc93a-105">Creating an access token</span></span>

<span data-ttu-id="fc93a-106">Você precisará criar um token de acesso que lhe permita exibir e editar um relatório.</span><span class="sxs-lookup"><span data-stu-id="fc93a-106">You will need to create an access token that gives you the ability to both view and edit a report.</span></span> <span data-ttu-id="fc93a-107">Para editar e salvar um relatório, será necessária a permissão de token **Report.ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="fc93a-107">To edit and save a report, you will need the **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="fc93a-108">Para obter mais informações, consulte [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="fc93a-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fc93a-109">Isso permitirá que você edite e salve as alterações a um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="fc93a-109">This will allow you to edit and save changes to an existing report.</span></span> <span data-ttu-id="fc93a-110">Se você também deseja a função de suporte a **Salvar Como**, você precisará fornecer permissões adicionais.</span><span class="sxs-lookup"><span data-stu-id="fc93a-110">If you would also like the function of supporting **Save As**, you will need to supply additional permissions.</span></span> <span data-ttu-id="fc93a-111">Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="fc93a-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="fc93a-112">Configuração de inserção</span><span class="sxs-lookup"><span data-stu-id="fc93a-112">Embed configuration</span></span>

<span data-ttu-id="fc93a-113">Você precisará fornecer permissões e um viewMode para ver o botão salvar em modo de edição.</span><span class="sxs-lookup"><span data-stu-id="fc93a-113">You will need to supply permissions and a viewMode in order to see the save button when in edit mode.</span></span> <span data-ttu-id="fc93a-114">Para saber mais, confira [Detalhes de configuração do servidor de inserção](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="fc93a-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="fc93a-115">Por exemplo, no JavaScript:</span><span class="sxs-lookup"><span data-stu-id="fc93a-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="fc93a-116">Isso indicará para inserir o relatório no modo de exibição com base na definição de **viewMode** para **models.ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="fc93a-116">This will indicate to embed the report in view mode based on **viewMode** being set to **models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="fc93a-117">Modo de exibição</span><span class="sxs-lookup"><span data-stu-id="fc93a-117">View mode</span></span>

<span data-ttu-id="fc93a-118">Você pode usar o seguinte JavaScript para mudar para o modo de exibição, caso esteja no modo de edição.</span><span class="sxs-lookup"><span data-stu-id="fc93a-118">You can use the following JavaScript to switch into view mode, if you are in edit mode.</span></span>

```
// Get a reference to the embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference to the embedded report.
report = powerbi.get(reportContainer);

// Switch to view mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="fc93a-119">Modo de edição</span><span class="sxs-lookup"><span data-stu-id="fc93a-119">Edit mode</span></span>

<span data-ttu-id="fc93a-120">Você pode usar o JavaScript a seguir para mudar para o modo de edição, caso esteja no modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="fc93a-120">You can use the following JavaScript to switch into edit mode, if you are in view mode.</span></span>

```
// Get a reference to the embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference to the embedded report.
report = powerbi.get(reportContainer);

// Switch to edit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="fc93a-121">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fc93a-121">See also</span></span>

[<span data-ttu-id="fc93a-122">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="fc93a-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="fc93a-123">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="fc93a-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="fc93a-124">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="fc93a-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="fc93a-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="fc93a-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="fc93a-126">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="fc93a-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="fc93a-127">Repositório de Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="fc93a-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="fc93a-128">Repositório de Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="fc93a-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="fc93a-129">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="fc93a-129">More questions?</span></span> [<span data-ttu-id="fc93a-130">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="fc93a-130">Try the Power BI Community</span></span>](http://community.powerbi.com/)
