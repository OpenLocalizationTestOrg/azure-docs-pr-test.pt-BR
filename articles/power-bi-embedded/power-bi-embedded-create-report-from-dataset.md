---
title: "Criar um novo relatório de um conjunto de dados no Azure Power BI Embedded | Microsoft Docs"
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="01b4f-103">Criar um novo relatório de um conjunto de dados no Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="01b4f-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="01b4f-104">Os relatórios do Power BI Embedded agora podem ser criados de um conjunto de dados em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01b4f-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="01b4f-105">O método de autenticação é semelhante ao de inserir relatório.</span><span class="sxs-lookup"><span data-stu-id="01b4f-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="01b4f-106">Ele se baseia em tokens de acesso que são específicos para um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="01b4f-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="01b4f-107">Tokens usados para o PowerBI.com são emitidos pelo AAD (Azure Active Directory) e tokens do Power BI Embedded são emitidos por seu próprio serviço.</span><span class="sxs-lookup"><span data-stu-id="01b4f-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="01b4f-108">Ao criar um relatório inserido, os tokens emitidos são para um conjunto de dados específico.</span><span class="sxs-lookup"><span data-stu-id="01b4f-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="01b4f-109">Tokens devem ser associados com a URL de inserção no mesmo elemento para assegurar que cada um tenha um token exclusivo.</span><span class="sxs-lookup"><span data-stu-id="01b4f-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="01b4f-110">Para criar um relatório inserido, os escopos *Dataset.Read e Workspace.Report.Create* devem ser fornecidos no token de acesso.</span><span class="sxs-lookup"><span data-stu-id="01b4f-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="01b4f-111">Criar o token de acesso necessário para criar um novo relatório</span><span class="sxs-lookup"><span data-stu-id="01b4f-111">Create access token needed to create new report</span></span>

<span data-ttu-id="01b4f-112">O Power BI Embedded usa tokens de inserção, que são Tokens Web JSON assinados por HMAC.</span><span class="sxs-lookup"><span data-stu-id="01b4f-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="01b4f-113">Os tokens são assinados com a tecla de acesso da sua coleção de espaço de trabalho do Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="01b4f-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="01b4f-114">Tokens de inserção, por padrão, são usados para fornecer acesso somente leitura a um relatório a ser inserido em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01b4f-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="01b4f-115">Tokens de inserção são emitidos para um relatório específico e devem ser associados uma URL de inserção.</span><span class="sxs-lookup"><span data-stu-id="01b4f-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="01b4f-116">Tokens de acesso devem ser criados no servidor conforme as chaves de acesso são usadas para assinar/criptografar os tokens.</span><span class="sxs-lookup"><span data-stu-id="01b4f-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="01b4f-117">Para obter informações sobre como criar um token de acesso, consulte [Autenticação e autorização com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="01b4f-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="01b4f-118">Você também pode examinar o método [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="01b4f-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="01b4f-119">Aqui está um exemplo de qual seria a aparência disso usando o SDK do .NET para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="01b4f-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="01b4f-120">Neste exemplo, temos nossa ID de conjunto de dados na qual desejamos criar o novo relatório.</span><span class="sxs-lookup"><span data-stu-id="01b4f-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="01b4f-121">Também precisamos adicionar escopos para *Dataset.Read e Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="01b4f-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="01b4f-122">A *classe PowerBIToken* exige que você instale o [pacote NuGet do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="01b4f-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="01b4f-123">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="01b4f-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="01b4f-124">**Código C#**</span><span class="sxs-lookup"><span data-stu-id="01b4f-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="01b4f-125">Criar um novo relatório em branco</span><span class="sxs-lookup"><span data-stu-id="01b4f-125">Create a new blank report</span></span>

<span data-ttu-id="01b4f-126">Para criar um novo relatório, a configuração de criação deve ser fornecida.</span><span class="sxs-lookup"><span data-stu-id="01b4f-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="01b4f-127">Isso deve incluir o token de acesso, o embedURL e o datasetID com base nos quais desejamos criar o relatório.</span><span class="sxs-lookup"><span data-stu-id="01b4f-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="01b4f-128">Isso exige que você instale o [pacote JavaScript Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/) do NuGet.</span><span class="sxs-lookup"><span data-stu-id="01b4f-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="01b4f-129">O embedUrl será apenas https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="01b4f-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="01b4f-130">Você pode usar a [Amostra de inserção de relatório JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="01b4f-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="01b4f-131">Ele também fornece exemplos de código para as diferentes operações que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="01b4f-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="01b4f-132">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="01b4f-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="01b4f-133">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="01b4f-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="01b4f-134">Chamar *powerbi.createReport()* fará com que uma tela em branco no modo de edição apareça dentro do elemento *div*.</span><span class="sxs-lookup"><span data-stu-id="01b4f-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="01b4f-135">Salvar novos relatórios</span><span class="sxs-lookup"><span data-stu-id="01b4f-135">Save new reports</span></span>

<span data-ttu-id="01b4f-136">O relatório não será realmente criado até que você chame a operação **salvar como**.</span><span class="sxs-lookup"><span data-stu-id="01b4f-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="01b4f-137">Isso pode ser feito do menu Arquivo ou do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="01b4f-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="01b4f-138">Um novo relatório é criado somente depois que **salvar como** é chamada.</span><span class="sxs-lookup"><span data-stu-id="01b4f-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="01b4f-139">Depois de você salvar, a tela ainda mostrará o conjunto de dados no modo de edição e não no relatório.</span><span class="sxs-lookup"><span data-stu-id="01b4f-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="01b4f-140">Você precisará recarregar o novo relatório como faria com qualquer outro relatório.</span><span class="sxs-lookup"><span data-stu-id="01b4f-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="01b4f-141">Carregar o novo relatório</span><span class="sxs-lookup"><span data-stu-id="01b4f-141">Load the new report</span></span>

<span data-ttu-id="01b4f-142">Para interagir com o novo relatório você precisa inseri-lo da mesma maneira que o aplicativo insere um relatório normal, ou seja, um novo token deve ser emitido especificamente para o novo relatório e, em seguida, o método de inserção deve ser chamado.</span><span class="sxs-lookup"><span data-stu-id="01b4f-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="01b4f-143">Automatizar as ações de salvar e carregar um novo relatório usando o evento "saved"</span><span class="sxs-lookup"><span data-stu-id="01b4f-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="01b4f-144">Para automatizar o processo de "salvar como" e em seguida carregar o novo relatório, você pode fazer uso do evento "saved".</span><span class="sxs-lookup"><span data-stu-id="01b4f-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="01b4f-145">Este evento é disparado quando a operação save for concluída e retorna um objeto JSON que contém o novo reportId, o nome do relatório, o antigo reportId (se houver algum) e se a operação foi saveAs ou save.</span><span class="sxs-lookup"><span data-stu-id="01b4f-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="01b4f-146">Para automatizar o processo, você pode ouvir o evento de "saved", usar o novo reportId, crie o novo token e inseri-lo no novo relatório.</span><span class="sxs-lookup"><span data-stu-id="01b4f-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="01b4f-147">Consulte também</span><span class="sxs-lookup"><span data-stu-id="01b4f-147">See also</span></span>

[<span data-ttu-id="01b4f-148">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="01b4f-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="01b4f-149">Salvar relatórios</span><span class="sxs-lookup"><span data-stu-id="01b4f-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="01b4f-150">Inserir um relatório</span><span class="sxs-lookup"><span data-stu-id="01b4f-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="01b4f-151">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="01b4f-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="01b4f-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="01b4f-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="01b4f-153">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="01b4f-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="01b4f-154">Pacote NuGet do Power BI Core</span><span class="sxs-lookup"><span data-stu-id="01b4f-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="01b4f-155">Pacote JavaScript do Power BI</span><span class="sxs-lookup"><span data-stu-id="01b4f-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="01b4f-156">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="01b4f-156">More questions?</span></span> [<span data-ttu-id="01b4f-157">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="01b4f-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)