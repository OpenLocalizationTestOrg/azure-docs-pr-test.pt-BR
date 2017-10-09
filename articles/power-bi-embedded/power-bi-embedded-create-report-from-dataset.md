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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="cf906-103">Criar um novo relatório de um conjunto de dados no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="cf906-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="cf906-104">Os relatórios do Power BI Embedded agora podem ser criados de um conjunto de dados em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf906-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="cf906-105">Olá método de autenticação é semelhante inserir toothat do relatório.</span><span class="sxs-lookup"><span data-stu-id="cf906-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="cf906-106">Ele se baseia em tokens de acesso que são o conjunto de dados tooa específico.</span><span class="sxs-lookup"><span data-stu-id="cf906-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="cf906-107">Tokens usados para o PowerBI.com são emitidos pelo AAD (Azure Active Directory) e tokens do Power BI Embedded são emitidos por seu próprio serviço.</span><span class="sxs-lookup"><span data-stu-id="cf906-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="cf906-108">Quando érmino um relatório inserido, Olá tokens emitidos são um conjunto de dados específico.</span><span class="sxs-lookup"><span data-stu-id="cf906-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="cf906-109">Tokens devem ser associados com hello inserir a URL no hello mesmo tooensure elemento cada tem um token exclusivo.</span><span class="sxs-lookup"><span data-stu-id="cf906-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="cf906-110">Em ordem toocreate um relatório inserido, *Dataset.Read e Workspace.Report.Create* escopos devem ser fornecidos no token de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf906-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="cf906-111">Criar novo relatório do access token toocreate necessários</span><span class="sxs-lookup"><span data-stu-id="cf906-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="cf906-112">O Power BI Embedded usa tokens de inserção, que são Tokens Web JSON assinados por HMAC.</span><span class="sxs-lookup"><span data-stu-id="cf906-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="cf906-113">Olá tokens são assinados com a chave de acesso Olá da coleção de espaço de trabalho do Azure Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="cf906-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="cf906-114">Inserir tokens, por padrão, são usada tooprovide ler apenas acesso tooa tooembed de relatório em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf906-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="cf906-115">Tokens de inserção são emitidos para um relatório específico e devem ser associados uma URL de inserção.</span><span class="sxs-lookup"><span data-stu-id="cf906-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="cf906-116">Tokens de acesso devem ser criados no servidor de saudação como chaves de acesso hello são usadas toosign/criptografar tokens de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf906-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="cf906-117">Para obter informações sobre como toocreate um token de acesso, consulte [autenticando e autorizar com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="cf906-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="cf906-118">Você também pode analisar Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método.</span><span class="sxs-lookup"><span data-stu-id="cf906-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="cf906-119">Aqui está um exemplo de como isso seria usando o SDK .NET de saudação do Power BI.</span><span class="sxs-lookup"><span data-stu-id="cf906-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="cf906-120">Neste exemplo, temos nosso id de conjunto de dados que queremos novo relatório do toocreat Olá no.</span><span class="sxs-lookup"><span data-stu-id="cf906-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="cf906-121">Também precisamos escopos Olá tooadd *Dataset.Read e Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="cf906-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="cf906-122">Olá *PowerBIToken classe* exige que você instale Olá [NuGut do pacote do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="cf906-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="cf906-123">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="cf906-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="cf906-124">**Código C#**</span><span class="sxs-lookup"><span data-stu-id="cf906-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="cf906-125">Criar um novo relatório em branco</span><span class="sxs-lookup"><span data-stu-id="cf906-125">Create a new blank report</span></span>

<span data-ttu-id="cf906-126">Em ordem toocreate um novo relatório, criar hello configuração deve ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="cf906-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="cf906-127">Inclua token de acesso de hello, Olá embedURL e datasetID Olá que desejamos relatório Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="cf906-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="cf906-128">Isso requer que você instalar o nuget Olá [pacote Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="cf906-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="cf906-129">Olá embedUrl será apenas https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="cf906-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="cf906-130">Você pode usar o hello [JavaScript relatório incorporar exemplo](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="cf906-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="cf906-131">Ele também fornece exemplos de código para operações diferentes de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cf906-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="cf906-132">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="cf906-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="cf906-133">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="cf906-133">**JavaScript code**</span></span>

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

<span data-ttu-id="cf906-134">Chamando *powerbi.createReport()* fará com que uma tela em branco no modo de edição apareçam em Olá *div* elemento.</span><span class="sxs-lookup"><span data-stu-id="cf906-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="cf906-135">Salvar novos relatórios</span><span class="sxs-lookup"><span data-stu-id="cf906-135">Save new reports</span></span>

<span data-ttu-id="cf906-136">relatório de saudação não será realmente criado até que você chame Olá **Salvar como** operação.</span><span class="sxs-lookup"><span data-stu-id="cf906-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="cf906-137">Isso pode ser feito do menu Arquivo ou do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cf906-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="cf906-138">Um novo relatório é criado somente depois que **salvar como** é chamada.</span><span class="sxs-lookup"><span data-stu-id="cf906-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="cf906-139">Depois de salvar, tela hello ainda mostrará Olá conjunto de dados no relatório de modo e não Olá de edição.</span><span class="sxs-lookup"><span data-stu-id="cf906-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="cf906-140">Você precisará novo relatório do tooreload hello como faria com qualquer outro relatório.</span><span class="sxs-lookup"><span data-stu-id="cf906-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="cf906-141">Saudação de carga novo relatório</span><span class="sxs-lookup"><span data-stu-id="cf906-141">Load hello new report</span></span>

<span data-ttu-id="cf906-142">Toointeract ordem com o novo relatório de saudação precisar tooembed no hello mesmo modo aplicativo hello incorpora um regular de relatório, que significa, um novo token deve ser emitido especificamente para o novo relatório de saudação e, em seguida, chamada hello incorporar o método.</span><span class="sxs-lookup"><span data-stu-id="cf906-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="cf906-143">Automatizar salvamento e carregamento de um novo relatório usando hello "Salvar" evento</span><span class="sxs-lookup"><span data-stu-id="cf906-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="cf906-144">No processo de saudação tooautomate ordem de "Salvar como" e, em seguida, carregar relatório novo hello, você pode fazer uso do hello "Salvar" evento.</span><span class="sxs-lookup"><span data-stu-id="cf906-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="cf906-145">Esse evento é acionado quando Olá operação de gravação estiver concluída e retorna um objeto Json que contém o reportId novo Olá, nome do relatório, reportId antigo hello (se houver algum) e se a operação de saudação foi saveAs ou salvar.</span><span class="sxs-lookup"><span data-stu-id="cf906-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="cf906-146">processo de saudação do tooAutomate pode escutar eventos hello "Salvar", levar reportId novo hello, criar um novo token de saudação e inserir um novo relatório de saudação com ele.</span><span class="sxs-lookup"><span data-stu-id="cf906-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="cf906-147">Consulte também</span><span class="sxs-lookup"><span data-stu-id="cf906-147">See also</span></span>

[<span data-ttu-id="cf906-148">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="cf906-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="cf906-149">Salvar relatórios</span><span class="sxs-lookup"><span data-stu-id="cf906-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="cf906-150">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="cf906-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="cf906-151">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="cf906-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="cf906-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="cf906-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="cf906-153">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="cf906-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="cf906-154">Pacote NuGet do Power BI Core</span><span class="sxs-lookup"><span data-stu-id="cf906-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="cf906-155">Pacote JavaScript do Power BI</span><span class="sxs-lookup"><span data-stu-id="cf906-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="cf906-156">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="cf906-156">More questions?</span></span> [<span data-ttu-id="cf906-157">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="cf906-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
