---
title: "aaaEmbed um relatório no Azure Power BI inserido | Microsoft Docs"
description: "Saiba como tooembed um relatório no Power BI inserido em seu aplicativo."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="04fd2-103">Inserir um relatório em um Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="04fd2-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="04fd2-104">Saiba como tooembed um relatório no Power BI inserido em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04fd2-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="04fd2-105">Veremos como tooactually inserir um relatório em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04fd2-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="04fd2-106">Isso presume que você já tenha um relatório que existe dentro de um espaço de trabalho em sua coleção de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="04fd2-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="04fd2-107">Se você ainda não fez essa etapa, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04fd2-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="04fd2-108">Você pode usar o hello .NET (c#) ou o SDK do Node. js, juntamente com JavaScript, tooeasily criar seu aplicativo com o Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="04fd2-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="04fd2-109">Usando toouse de chaves de acesso Olá APIs REST</span><span class="sxs-lookup"><span data-stu-id="04fd2-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="04fd2-110">Na saudação de toocall ordem API REST, você pode passar chave de acesso de saudação que você pode obter de saudação portal do Azure para uma coleção de espaço de trabalho fornecido.</span><span class="sxs-lookup"><span data-stu-id="04fd2-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="04fd2-111">Para obter mais informações, consulte [Introdução ao Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04fd2-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="04fd2-112">Obter uma ID de relatório</span><span class="sxs-lookup"><span data-stu-id="04fd2-112">Get a report id</span></span>

<span data-ttu-id="04fd2-113">Cada token de acesso se baseia em um relatório.</span><span class="sxs-lookup"><span data-stu-id="04fd2-113">Every access token is based on a report.</span></span> <span data-ttu-id="04fd2-114">Você precisará Olá tooget id de relatório fornecida para relatório de saudação que você deseja tooembed.</span><span class="sxs-lookup"><span data-stu-id="04fd2-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="04fd2-115">Isso pode ser feito com base em chamadas toohello [obter relatórios](https://msdn.microsoft.com/library/azure/mt711510.aspx) API REST.</span><span class="sxs-lookup"><span data-stu-id="04fd2-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="04fd2-116">Isso retornará relatório Olá id e hello inserem a url.</span><span class="sxs-lookup"><span data-stu-id="04fd2-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="04fd2-117">Isso pode ser feito usando Olá SDK .NET do Power BI ou chamar hello API REST diretamente.</span><span class="sxs-lookup"><span data-stu-id="04fd2-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="04fd2-118">Usando Olá SDK .NET do Power BI</span><span class="sxs-lookup"><span data-stu-id="04fd2-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="04fd2-119">Ao usar o hello .NET SDK, você precisará toocreate uma credencial de token que se baseia a chave de acesso Olá obtido Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="04fd2-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="04fd2-120">Isso requer que você instale Olá [pacote NuGet de API do Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="04fd2-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="04fd2-121">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="04fd2-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="04fd2-122">**Código C#**</span><span class="sxs-lookup"><span data-stu-id="04fd2-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="04fd2-123">Chamar hello API REST diretamente</span><span class="sxs-lookup"><span data-stu-id="04fd2-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="04fd2-124">Criar um token de acesso</span><span class="sxs-lookup"><span data-stu-id="04fd2-124">Create an access token</span></span>

<span data-ttu-id="04fd2-125">O Power BI Embedded usa tokens de inserção, que são Tokens Web JSON assinados por HMAC.</span><span class="sxs-lookup"><span data-stu-id="04fd2-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="04fd2-126">Olá tokens são assinados com a chave de acesso Olá da coleção de espaço de trabalho do Azure Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="04fd2-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="04fd2-127">Inserir tokens, por padrão, são usada tooprovide ler apenas acesso tooa tooembed de relatório em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04fd2-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="04fd2-128">Tokens de inserção são emitidos para um relatório específico e devem ser associados uma URL de inserção.</span><span class="sxs-lookup"><span data-stu-id="04fd2-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="04fd2-129">Tokens de acesso devem ser criados no servidor de saudação como chaves de acesso hello são usadas toosign/criptografar tokens de saudação.</span><span class="sxs-lookup"><span data-stu-id="04fd2-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="04fd2-130">Para obter informações sobre como toocreate um token de acesso, consulte [autenticando e autorizar com o Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="04fd2-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="04fd2-131">Você também pode analisar Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método.</span><span class="sxs-lookup"><span data-stu-id="04fd2-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="04fd2-132">Aqui está um exemplo de como isso seria usando o SDK .NET de saudação do Power BI.</span><span class="sxs-lookup"><span data-stu-id="04fd2-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="04fd2-133">Você usará a id de relatório de saudação que você recuperou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="04fd2-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="04fd2-134">Depois de inserir Olá token é criado, usará token Olá de toogenerate chave de acesso de saudação que você pode usar do ponto de vista do hello javascript.</span><span class="sxs-lookup"><span data-stu-id="04fd2-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="04fd2-135">Olá *PowerBIToken classe* exige que você instale Olá [NuGut do pacote do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="04fd2-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="04fd2-136">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="04fd2-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="04fd2-137">**Código C#**</span><span class="sxs-lookup"><span data-stu-id="04fd2-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="04fd2-138">Adicionando tokens de tooembed de escopos de permissão</span><span class="sxs-lookup"><span data-stu-id="04fd2-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="04fd2-139">Ao usar tokens de inserção, talvez você queira toorestrict de uso dos recursos de saudação que concedem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="04fd2-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="04fd2-140">Por esse motivo, você pode gerar um token com as permissões no escopo.</span><span class="sxs-lookup"><span data-stu-id="04fd2-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="04fd2-141">Para obter mais informações, consulte [Escopos](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="04fd2-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="04fd2-142">Inserir usando JavaScript</span><span class="sxs-lookup"><span data-stu-id="04fd2-142">Embed using JavaScript</span></span>

<span data-ttu-id="04fd2-143">Depois de ter o token de acesso de saudação e a id de relatório hello, podemos pode inserir relatório hello usando JavaScript.</span><span class="sxs-lookup"><span data-stu-id="04fd2-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="04fd2-144">Isso requer que você instalar o nuget Olá [pacote Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="04fd2-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="04fd2-145">Olá embedUrl será apenas https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="04fd2-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="04fd2-146">Você pode usar o hello [JavaScript relatório incorporar exemplo](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="04fd2-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="04fd2-147">Ele também fornece exemplos de código para operações diferentes de saudação que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="04fd2-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="04fd2-148">**Instalar o pacote NuGet**</span><span class="sxs-lookup"><span data-stu-id="04fd2-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="04fd2-149">**Código JavaScript**</span><span class="sxs-lookup"><span data-stu-id="04fd2-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="04fd2-150">Tamanho de saudação do conjunto de elementos inseridos</span><span class="sxs-lookup"><span data-stu-id="04fd2-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="04fd2-151">relatório de saudação será inserido automaticamente com base no tamanho de saudação de seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="04fd2-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="04fd2-152">tamanho de padrão de saudação toooverride de saudação incorpora simplesmente adicionar um estilos CSS de embutido ou atributo de classe de largura e altura.</span><span class="sxs-lookup"><span data-stu-id="04fd2-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="04fd2-153">Consulte também</span><span class="sxs-lookup"><span data-stu-id="04fd2-153">See also</span></span>

[<span data-ttu-id="04fd2-154">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="04fd2-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="04fd2-155">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="04fd2-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="04fd2-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="04fd2-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="04fd2-157">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="04fd2-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="04fd2-158">Pacote JavaScript do Power BI</span><span class="sxs-lookup"><span data-stu-id="04fd2-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="04fd2-159">[Pacote NuGet da API do Power BI](https://www.nuget.org/profiles/powerbi)
[Pacote NuGet do Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="04fd2-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="04fd2-160">Repositório de Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="04fd2-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="04fd2-161">Repositório de Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="04fd2-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="04fd2-162">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="04fd2-162">More questions?</span></span> [<span data-ttu-id="04fd2-163">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="04fd2-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
