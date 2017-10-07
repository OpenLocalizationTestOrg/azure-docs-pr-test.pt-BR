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
# <a name="save-reports-in-power-bi-embedded"></a>Salvar relatórios no Power BI Embedded

Saiba como toosave relatórios no Power BI inserido. Isso requer permissões apropriadas na ordem toowork com êxito.

No Power BI Embedded, você pode editar os relatórios existentes e salvá-los. Você também pode criar um novo relatório e salve como um novo toocreate de relatório um.

Em ordem toosave um relatório é necessário primeiro toocreate um token para relatório específico de saudação com escopos de saudação à direita:

* tooenable salvar Report.ReadWrite escopo é necessária
* tooenable Salvar como, Report.Read e Workspace.Report.Copy escopos são necessários
* tooenable salvar e salvar como, Report.ReadWrite e Workspace.Report.Copy são é necessário

Respectivamente na saudação de tooenable ordem direita salvar ou salvar como botões no menu Arquivo, você precisa tooprovide Olá direita permissão na configuração de inserção de saudação quando você incorporar Olá relatório:

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> O token de acesso também precisa de escopos apropriado hello. Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Inserir o relatório no modo de edição

Vamos supor que você queira tooEmbed um relatório no modo de edição dentro de seu aplicativo, toodo então apenas passar propriedades do direito de saudação na configuração de inserção e chame powerbi.embed(). Você precisará toosupply permissões e um viewMode em Olá toosee de ordem salvar e salve como botões quando no modo de edição. Para saber mais, confira [Detalhes de configuração do servidor de inserção](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

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

Agora, um relatório será inserido em seu aplicativo no modo de edição.

## <a name="save-report"></a>Salvar relatório

Depois que o modo com hello token à direita e permissões de edição de relatório de saudação Embbeding em você pode salvar o relatório de Olá menu arquivo hello ou de javascript:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Salvar como

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
> Um novo relatório é criado somente depois do uso de *salvar como*. Depois de salvar hello, tela hello ainda mostra relatório antigo Olá Editar modo e não hello novo relatório. Você precisará tooembed Olá novo relatório que foi criado. Isso requer um novo token de acesso, já que eles são criados por relatório.

Em seguida, você precisará tooload Olá novo relatório após um *Salvar como*. Isso é semelhante tooembedding qualquer relatório.

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

## <a name="see-also"></a>Consulte também

[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Criar um novo relatório de um conjunto de dados](power-bi-embedded-create-report-from-dataset.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)

