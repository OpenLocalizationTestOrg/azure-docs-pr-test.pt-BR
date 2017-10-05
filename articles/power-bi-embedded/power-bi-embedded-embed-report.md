---
title: "Inserir um relatório no Azure Power BI Embedded | Microsoft Docs"
description: "Saiba como inserir um relatório no Power BI Embedded em seu aplicativo."
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="581e7-103">Inserir um relatório em um Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="581e7-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="581e7-104">Saiba como inserir um relatório no Power BI Embedded em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="581e7-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="581e7-105">Vamos examinar como realmente inserir um relatório em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="581e7-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="581e7-106">Isso presume que você já tenha um relatório que existe dentro de um espaço de trabalho em sua coleção de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="581e7-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="581e7-107">Se você ainda não fez essa etapa, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="581e7-108">É possível usar o SDK para .NET (C#) ou Node.js junto com o JavaScript para criar seu aplicativo facilmente com o Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="581e7-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="581e7-109">Usando as teclas de acesso para usar APIs REST</span><span class="sxs-lookup"><span data-stu-id="581e7-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="581e7-110">Para chamar a API REST, você pode passar a tecla de acesso que você pode obter no Portal do Azure para uma determinada coleção de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="581e7-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="581e7-111">Para obter mais informações, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="581e7-112">Obter uma ID de relatório</span><span class="sxs-lookup"><span data-stu-id="581e7-112">Get a report id</span></span>

<span data-ttu-id="581e7-113">Cada token de acesso se baseia em um relatório.</span><span class="sxs-lookup"><span data-stu-id="581e7-113">Every access token is based on a report.</span></span> <span data-ttu-id="581e7-114">Você precisará obter a ID de relatório específica do relatório que você deseja inserir.</span><span class="sxs-lookup"><span data-stu-id="581e7-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="581e7-115">Isso pode ser feito com base em chamadas para a API REST [Obter Relatórios](https://msdn.microsoft.com/library/azure/mt711510.aspx).</span><span class="sxs-lookup"><span data-stu-id="581e7-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="581e7-116">Isso retornará a ID do relatório e a URL de inserção.</span><span class="sxs-lookup"><span data-stu-id="581e7-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="581e7-117">Isso pode ser feito usando o SDK do .NET do Power BI ou chamando a API REST diretamente.</span><span class="sxs-lookup"><span data-stu-id="581e7-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="581e7-118">Usando o SDK do .NET do Power BI</span><span class="sxs-lookup"><span data-stu-id="581e7-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="581e7-119">Ao usar o SDK do .NET, você precisará criar uma credencial de token que se baseia na tecla de acesso que você obtém do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="581e7-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="581e7-120">Isso exige que você instale o [pacote NuGet da API do Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="581e7-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="581e7-121">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="581e7-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="581e7-122">**Código C#**</span><span class="sxs-lookup"><span data-stu-id="581e7-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="581e7-123">Chamar a API REST diretamente</span><span class="sxs-lookup"><span data-stu-id="581e7-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="581e7-124">Criar um token de acesso</span><span class="sxs-lookup"><span data-stu-id="581e7-124">Create an access token</span></span>

<span data-ttu-id="581e7-125">O Power BI Embedded usa tokens de inserção, que são Tokens Web JSON assinados por HMAC.</span><span class="sxs-lookup"><span data-stu-id="581e7-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="581e7-126">Os tokens são assinados com a tecla de acesso da sua coleção de espaço de trabalho do Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="581e7-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="581e7-127">Tokens de inserção, por padrão, são usados para fornecer acesso somente leitura a um relatório a ser inserido em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="581e7-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="581e7-128">Tokens de inserção são emitidos para um relatório específico e devem ser associados uma URL de inserção.</span><span class="sxs-lookup"><span data-stu-id="581e7-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="581e7-129">Tokens de acesso devem ser criados no servidor conforme as chaves de acesso são usadas para assinar/criptografar os tokens.</span><span class="sxs-lookup"><span data-stu-id="581e7-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="581e7-130">Para obter informações sobre como criar um token de acesso, consulte [Autenticação e autorização com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="581e7-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="581e7-131">Você também pode examinar o método [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="581e7-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="581e7-132">Aqui está um exemplo de qual seria a aparência disso usando o SDK do .NET para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="581e7-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="581e7-133">Você usará a ID de relatório que você recuperou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="581e7-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="581e7-134">Depois de criar o token de inserção, você usará a tecla de acesso para gerar o token que você pode usar da perspectiva do javascript.</span><span class="sxs-lookup"><span data-stu-id="581e7-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="581e7-135">A *classe PowerBIToken* exige que você instale o [pacote NuGet do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="581e7-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="581e7-136">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="581e7-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="581e7-137">**Código C#**</span><span class="sxs-lookup"><span data-stu-id="581e7-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="581e7-138">Adicionando escopos de permissão para tokens de inserção</span><span class="sxs-lookup"><span data-stu-id="581e7-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="581e7-139">Ao usar os tokens de inserção, convém restringir o uso de recursos aos quais você concede acesso.</span><span class="sxs-lookup"><span data-stu-id="581e7-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="581e7-140">Por esse motivo, você pode gerar um token com as permissões no escopo.</span><span class="sxs-lookup"><span data-stu-id="581e7-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="581e7-141">Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="581e7-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="581e7-142">Inserir usando JavaScript</span><span class="sxs-lookup"><span data-stu-id="581e7-142">Embed using JavaScript</span></span>

<span data-ttu-id="581e7-143">Depois de ter o token de acesso e a ID do relatório, é possível inserir o relatório usando JavaScript.</span><span class="sxs-lookup"><span data-stu-id="581e7-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="581e7-144">Isso exige que você instale o [pacote JavaScript Power BI](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/) do NuGet.</span><span class="sxs-lookup"><span data-stu-id="581e7-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="581e7-145">O embedUrl será apenas https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="581e7-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="581e7-146">Você pode usar a [Amostra de inserção de relatório JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) para testar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="581e7-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="581e7-147">Ele também fornece exemplos de código para as diferentes operações que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="581e7-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="581e7-148">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="581e7-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="581e7-149">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="581e7-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="581e7-150">Defina o tamanho dos elementos inseridos</span><span class="sxs-lookup"><span data-stu-id="581e7-150">Set the size of embedded elements</span></span>

<span data-ttu-id="581e7-151">O relatório será inserido automaticamente com base no tamanho do respectivo contêiner.</span><span class="sxs-lookup"><span data-stu-id="581e7-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="581e7-152">Substituir o tamanho padrão das inserções simplesmente adiciona um atributo de classe CSS ou estilos embutidos para largura e altura.</span><span class="sxs-lookup"><span data-stu-id="581e7-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="581e7-153">Consulte também</span><span class="sxs-lookup"><span data-stu-id="581e7-153">See also</span></span>

[<span data-ttu-id="581e7-154">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="581e7-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="581e7-155">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="581e7-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="581e7-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="581e7-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="581e7-157">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="581e7-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="581e7-158">Pacote JavaScript do Power BI</span><span class="sxs-lookup"><span data-stu-id="581e7-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="581e7-159">[Pacote NuGet da API do Power BI](https://www.nuget.org/profiles/powerbi)
[Pacote NuGet do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="581e7-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="581e7-160">Repositório de Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="581e7-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="581e7-161">Repositório de Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="581e7-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="581e7-162">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="581e7-162">More questions?</span></span> [<span data-ttu-id="581e7-163">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="581e7-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
