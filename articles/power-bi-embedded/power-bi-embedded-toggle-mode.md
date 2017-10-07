---
title: "aaaToggle entre o modo de exibição e edição para relatórios no Azure Power BI inserido | Microsoft Docs"
description: "Saiba como tootoggle entre o modo de exibição e edição para seus relatórios no Power BI inserido."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>Alternar entre o modo de exibição e modo de edição para seus relatórios no Power BI Embedded

Saiba como tootoggle entre o modo de exibição e edição para seus relatórios no Power BI inserido.

## <a name="creating-an-access-token"></a>Criação de um token de acesso

Você precisará toocreate um token de acesso que oferece exibição de tooboth capacidade hello e editar um relatório. tooedit e salvar um relatório, você precisará Olá **Report.ReadWrite** permissão de token. Para obter mais informações, consulte [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md).

> [!NOTE]
> Isso será permitem tooedit e salvar as alterações de relatório existente tooan. Se você também deseja a função hello de dar suporte a **Salvar como**, você precisará de permissões adicionais toosupply. Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes).

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>Configuração de inserção

Você precisará toosupply permissões e um viewMode na saudação de toosee ordem Salvar botão quando no modo de edição. Para saber mais, confira [Detalhes de configuração do servidor de inserção](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

Por exemplo, no JavaScript:

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

Isso indicará o relatório de saudação tooembed no modo de exibição com base em **viewMode** sendo definido muito**modelos. ViewMode.View**.

## <a name="view-mode"></a>Modo de exibição

Você pode usar o hello tooswitch JavaScript a seguir no modo de exibição, se você estiver no modo de edição.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>Modo de edição

Você pode usar o hello tooswitch JavaScript a seguir no modo de edição, se você estiver no modo de exibição modo.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>Consulte também

[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Repositório de Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repositório de Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)
