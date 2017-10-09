---
title: "aaaCreate um novo relatório de um conjunto de dados no Azure Power BI inserido | Microsoft Docs"
description: "Os relatórios do Power BI Embedded agora podem ser criados de um conjunto de dados em seu próprio aplicativo."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Criar um novo relatório de um conjunto de dados no Power BI Embedded

Os relatórios do Power BI Embedded agora podem ser criados de um conjunto de dados em seu próprio aplicativo. 

Olá método de autenticação é semelhante inserir toothat do relatório. Ele se baseia em tokens de acesso que são o conjunto de dados tooa específico. Tokens usados para o PowerBI.com são emitidos pelo AAD (Azure Active Directory) e tokens do Power BI Embedded são emitidos por seu próprio serviço.

Quando érmino um relatório inserido, Olá tokens emitidos são um conjunto de dados específico. Tokens devem ser associados com hello inserir a URL no hello mesmo tooensure elemento cada tem um token exclusivo. Em ordem toocreate um relatório inserido, *Dataset.Read e Workspace.Report.Create* escopos devem ser fornecidos no token de acesso de saudação.

## <a name="create-access-token-needed-toocreate-new-report"></a>Criar novo relatório do access token toocreate necessários

O Power BI Embedded usa tokens de inserção, que são Tokens Web JSON assinados por HMAC. Olá tokens são assinados com a chave de acesso Olá da coleção de espaço de trabalho do Azure Power BI inserido. Inserir tokens, por padrão, são usada tooprovide ler apenas acesso tooa tooembed de relatório em um aplicativo. Tokens de inserção são emitidos para um relatório específico e devem ser associados uma URL de inserção.

Tokens de acesso devem ser criados no servidor de saudação como chaves de acesso hello são usadas toosign/criptografar tokens de saudação. Para obter informações sobre como toocreate um token de acesso, consulte [autenticando e autorizar com o Power BI Embedded](power-bi-embedded-app-token-flow.md). Você também pode analisar Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método. Aqui está um exemplo de como isso seria usando o SDK .NET de saudação do Power BI.

Neste exemplo, temos nosso id de conjunto de dados que queremos novo relatório do toocreat Olá no. Também precisamos escopos Olá tooadd *Dataset.Read e Workspace.Report.Create*.

Olá *PowerBIToken classe* exige que você instale Olá [NuGut do pacote do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalar o pacote NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Código C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Criar um novo relatório em branco

Em ordem toocreate um novo relatório, criar hello configuração deve ser fornecida. Inclua token de acesso de hello, Olá embedURL e datasetID Olá que desejamos relatório Olá toocreate. Isso requer que você instalar o nuget Olá [pacote Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Olá embedUrl será apenas https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Você pode usar o hello [JavaScript relatório incorporar exemplo](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidade. Ele também fornece exemplos de código para operações diferentes de saudação que estão disponíveis.

**Instalar o pacote NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Código JavaScript**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

Chamando *powerbi.createReport()* fará com que uma tela em branco no modo de edição apareçam em Olá *div* elemento.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Salvar novos relatórios

relatório de saudação não será realmente criado até que você chame Olá **Salvar como** operação. Isso pode ser feito do menu Arquivo ou do JavaScript.

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
> Um novo relatório é criado somente depois que **salvar como** é chamada. Depois de salvar, tela hello ainda mostrará Olá conjunto de dados no relatório de modo e não Olá de edição. Você precisará novo relatório do tooreload hello como faria com qualquer outro relatório.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Saudação de carga novo relatório

Toointeract ordem com o novo relatório de saudação precisar tooembed no hello mesmo modo aplicativo hello incorpora um regular de relatório, que significa, um novo token deve ser emitido especificamente para o novo relatório de saudação e, em seguida, chamada hello incorporar o método.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Automatizar salvamento e carregamento de um novo relatório usando hello "Salvar" evento

No processo de saudação tooautomate ordem de "Salvar como" e, em seguida, carregar relatório novo hello, você pode fazer uso do hello "Salvar" evento. Esse evento é acionado quando Olá operação de gravação estiver concluída e retorna um objeto Json que contém o reportId novo Olá, nome do relatório, reportId antigo hello (se houver algum) e se a operação de saudação foi saveAs ou salvar.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

processo de saudação do tooAutomate pode escutar eventos hello "Salvar", levar reportId novo hello, criar um novo token de saudação e inserir um novo relatório de saudação com ele.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a>Consulte também

[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Salvar relatórios](power-bi-embedded-save-reports.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Pacote NuGet do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Pacote JavaScript do Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)
