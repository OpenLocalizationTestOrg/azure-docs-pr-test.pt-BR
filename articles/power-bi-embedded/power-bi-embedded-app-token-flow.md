---
title: Autenticando e autorizando com o Power BI Embedded
description: Autenticando e autorizando com o Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="0277e-103">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0277e-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="0277e-104">O serviço Power BI Embedded usa **Chaves** e **Tokens de Aplicativo** para autenticação e autorização, em vez de usar autenticação explícita do usuário final.</span><span class="sxs-lookup"><span data-stu-id="0277e-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="0277e-105">Nesse modelo, seu aplicativo gerencia a autenticação e autorização para os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="0277e-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="0277e-106">Quando necessário, seu aplicativo cria e envia os Tokens de Aplicativo que dizem ao nosso serviço para renderizar o relatório solicitado.</span><span class="sxs-lookup"><span data-stu-id="0277e-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="0277e-107">Esse design não requer que o aplicativo use o Azure Active Directory para autorização e autenticação de usuário, embora você possa fazer isso.</span><span class="sxs-lookup"><span data-stu-id="0277e-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="0277e-108">Duas maneiras de autenticar</span><span class="sxs-lookup"><span data-stu-id="0277e-108">Two ways to authenticate</span></span>

<span data-ttu-id="0277e-109">**Chave** - você pode usar chaves para todas as chamadas à API de REST do Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0277e-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="0277e-110">As chaves podem ser encontradas no **Portal do Azure** clicando em **Todas as configurações** e **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="0277e-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="0277e-111">Sempre use a chave como se fosse uma senha.</span><span class="sxs-lookup"><span data-stu-id="0277e-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="0277e-112">Essas chaves têm permissões para fazer qualquer chamada à API REST em uma coleção de espaço de trabalho específica.</span><span class="sxs-lookup"><span data-stu-id="0277e-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="0277e-113">Para usar uma chave em uma chamada REST, adicione o seguinte cabeçalho de autorização:</span><span class="sxs-lookup"><span data-stu-id="0277e-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="0277e-114">**Token de aplicativo** - tokens de aplicativo são usados para todas as solicitações de inserção.</span><span class="sxs-lookup"><span data-stu-id="0277e-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="0277e-115">Eles são projetados para serem executados no lado do cliente e, portanto, estão restritos a um único relatório. É uma prática recomendada definir um tempo de expiração.</span><span class="sxs-lookup"><span data-stu-id="0277e-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="0277e-116">Os tokens de aplicativo são um JWT (Token Web JSON) assinado por uma das suas chaves.</span><span class="sxs-lookup"><span data-stu-id="0277e-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="0277e-117">O token de seu aplicativo pode conter as seguintes declarações:</span><span class="sxs-lookup"><span data-stu-id="0277e-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="0277e-118">Declaração</span><span class="sxs-lookup"><span data-stu-id="0277e-118">Claim</span></span> | <span data-ttu-id="0277e-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="0277e-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0277e-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="0277e-120">**ver**</span></span> |<span data-ttu-id="0277e-121">A versão do token do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0277e-121">The version of the app token.</span></span> <span data-ttu-id="0277e-122">A versão atual é 0.2.0.</span><span class="sxs-lookup"><span data-stu-id="0277e-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="0277e-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="0277e-123">**aud**</span></span> |<span data-ttu-id="0277e-124">O destinatário pretendido do token.</span><span class="sxs-lookup"><span data-stu-id="0277e-124">The intended recipient of the token.</span></span> <span data-ttu-id="0277e-125">Para uso do Power BI Embedded: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="0277e-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="0277e-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="0277e-126">**iss**</span></span> |<span data-ttu-id="0277e-127">Uma cadeia de caracteres que indica o aplicativo que emitiu o token.</span><span class="sxs-lookup"><span data-stu-id="0277e-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="0277e-128">**tipo**</span><span class="sxs-lookup"><span data-stu-id="0277e-128">**type**</span></span> |<span data-ttu-id="0277e-129">O tipo de token do aplicativo que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="0277e-129">The type of app token which is being created.</span></span> <span data-ttu-id="0277e-130">O único tipo com suporte atualmente é **incorporar**.</span><span class="sxs-lookup"><span data-stu-id="0277e-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="0277e-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="0277e-131">**wcn**</span></span> |<span data-ttu-id="0277e-132">Nome da coleção de espaços de trabalho para o qual o token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="0277e-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="0277e-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="0277e-133">**wid**</span></span> |<span data-ttu-id="0277e-134">ID do espaço de trabalho para o qual o token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="0277e-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="0277e-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="0277e-135">**rid**</span></span> |<span data-ttu-id="0277e-136">ID ddo relatório para o qual o token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="0277e-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="0277e-137">**nome de usuário** (opcional)</span><span class="sxs-lookup"><span data-stu-id="0277e-137">**username** (optional)</span></span> |<span data-ttu-id="0277e-138">Usado com RLS, é uma cadeia de caracteres que pode ser usada para ajudar a identificar o usuário ao aplicar regras RLS.</span><span class="sxs-lookup"><span data-stu-id="0277e-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="0277e-139">**funções** (opcional)</span><span class="sxs-lookup"><span data-stu-id="0277e-139">**roles** (optional)</span></span> |<span data-ttu-id="0277e-140">Uma cadeia de caracteres que contém as funções a selecionar ao aplicar regras de segurança em nível de linha.</span><span class="sxs-lookup"><span data-stu-id="0277e-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="0277e-141">Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0277e-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="0277e-142">**SCP** (opcional)</span><span class="sxs-lookup"><span data-stu-id="0277e-142">**scp** (optional)</span></span> |<span data-ttu-id="0277e-143">Uma cadeia de caracteres que contém os escopos de permissões.</span><span class="sxs-lookup"><span data-stu-id="0277e-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="0277e-144">Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0277e-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="0277e-145">**exp** (opcional)</span><span class="sxs-lookup"><span data-stu-id="0277e-145">**exp** (optional)</span></span> |<span data-ttu-id="0277e-146">Indica a hora em que o token irá expirar.</span><span class="sxs-lookup"><span data-stu-id="0277e-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="0277e-147">Elas devem ser transmitidas como carimbos de data/hora do Unix.</span><span class="sxs-lookup"><span data-stu-id="0277e-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="0277e-148">**nbf** (opcional)</span><span class="sxs-lookup"><span data-stu-id="0277e-148">**nbf** (optional)</span></span> |<span data-ttu-id="0277e-149">Indica a hora em que o token começa a valer.</span><span class="sxs-lookup"><span data-stu-id="0277e-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="0277e-150">Elas devem ser transmitidas como carimbos de data/hora do Unix.</span><span class="sxs-lookup"><span data-stu-id="0277e-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="0277e-151">Um token do aplicativo de exemplo terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0277e-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="0277e-152">Quando decodificado, ele terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="0277e-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="0277e-153">Há métodos disponíveis dentro dos SDKs que facilitam a criação de tokens de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0277e-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="0277e-154">Por exemplo, para .NET, você pode examinar a classe [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) e os métodos [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="0277e-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="0277e-155">Para o SDK do .NET, você pode consultar [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="0277e-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="0277e-156">Escopos</span><span class="sxs-lookup"><span data-stu-id="0277e-156">Scopes</span></span>

<span data-ttu-id="0277e-157">Ao usar os tokens de inserção, convém restringir o uso de recursos aos quais você concede acesso.</span><span class="sxs-lookup"><span data-stu-id="0277e-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="0277e-158">Por esse motivo, você pode gerar um token com as permissões no escopo.</span><span class="sxs-lookup"><span data-stu-id="0277e-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="0277e-159">A seguir estão os escopos disponíveis para o Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0277e-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="0277e-160">Escopo</span><span class="sxs-lookup"><span data-stu-id="0277e-160">Scope</span></span>|<span data-ttu-id="0277e-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="0277e-161">Description</span></span>|
|---|---|
|<span data-ttu-id="0277e-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="0277e-162">Dataset.Read</span></span>|<span data-ttu-id="0277e-163">Fornece permissão para ler o conjunto de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="0277e-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="0277e-164">Dataset.Write</span></span>|<span data-ttu-id="0277e-165">Fornece permissão para gravar o conjunto de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="0277e-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="0277e-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="0277e-167">Fornece permissão para leitura e gravação do conjunto de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="0277e-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="0277e-168">Report.Read</span></span>|<span data-ttu-id="0277e-169">Fornece permissão para exibir o relatório especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="0277e-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="0277e-170">Report.ReadWrite</span></span>|<span data-ttu-id="0277e-171">Fornece permissão para exibir e editar o relatório especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="0277e-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="0277e-172">Workspace.Report.Create</span></span>|<span data-ttu-id="0277e-173">Fornece permissão para criar um novo relatório no espaço de trabalho especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="0277e-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="0277e-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="0277e-175">Fornece permissão para clonar um relatório existente no espaço de trabalho especificado.</span><span class="sxs-lookup"><span data-stu-id="0277e-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="0277e-176">Você pode fornecer vários escopos usando um espaço entre os escopos semelhante ao que segue.</span><span class="sxs-lookup"><span data-stu-id="0277e-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="0277e-177">**Declarações necessárias - escopos**</span><span class="sxs-lookup"><span data-stu-id="0277e-177">**Required claims - scopes**</span></span>

<span data-ttu-id="0277e-178">scp: {scopesClaim} scopesClaim pode ser uma cadeia de caracteres ou uma matriz de cadeias de caracteres, observando as permissões permitidas para recursos do espaço de trabalho (relatório, conjunto de dados, etc.)</span><span class="sxs-lookup"><span data-stu-id="0277e-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="0277e-179">Um token decodificado, com escopos definidos, seria semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="0277e-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="0277e-180">Operações e escopos</span><span class="sxs-lookup"><span data-stu-id="0277e-180">Operations and scopes</span></span>

|<span data-ttu-id="0277e-181">Operação</span><span class="sxs-lookup"><span data-stu-id="0277e-181">Operation</span></span>|<span data-ttu-id="0277e-182">Recurso de destino</span><span class="sxs-lookup"><span data-stu-id="0277e-182">Target resource</span></span>|<span data-ttu-id="0277e-183">Permissões de token</span><span class="sxs-lookup"><span data-stu-id="0277e-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="0277e-184">Criar (na memória) um novo relatório com base em um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0277e-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="0277e-185">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0277e-185">Dataset</span></span>|<span data-ttu-id="0277e-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="0277e-186">Dataset.Read</span></span>|
|<span data-ttu-id="0277e-187">Criar (na memória) um novo relatório com base em um conjunto de dados e salvar o relatório.</span><span class="sxs-lookup"><span data-stu-id="0277e-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="0277e-188">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0277e-188">Dataset</span></span>|<span data-ttu-id="0277e-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="0277e-189">* Dataset.Read</span></span><br><span data-ttu-id="0277e-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="0277e-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="0277e-191">Exibir e explorar/Editar (na memória) um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="0277e-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="0277e-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="0277e-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="0277e-193">Isso não lhe dará permissões para salvar as edições.</span><span class="sxs-lookup"><span data-stu-id="0277e-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="0277e-194">Relatório</span><span class="sxs-lookup"><span data-stu-id="0277e-194">Report</span></span>|<span data-ttu-id="0277e-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="0277e-195">Report.Read</span></span>|
|<span data-ttu-id="0277e-196">Editar e salvar um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="0277e-196">Edit and save an existing report.</span></span>|<span data-ttu-id="0277e-197">Relatório</span><span class="sxs-lookup"><span data-stu-id="0277e-197">Report</span></span>|<span data-ttu-id="0277e-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="0277e-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="0277e-199">Salvar uma cópia de um relatório (Salvar como).</span><span class="sxs-lookup"><span data-stu-id="0277e-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="0277e-200">Relatório</span><span class="sxs-lookup"><span data-stu-id="0277e-200">Report</span></span>|<span data-ttu-id="0277e-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="0277e-201">* Report.Read</span></span><br><span data-ttu-id="0277e-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="0277e-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="0277e-203">Como funciona o fluxo</span><span class="sxs-lookup"><span data-stu-id="0277e-203">Here's how the flow works</span></span>
1. <span data-ttu-id="0277e-204">Copie as chaves de API para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0277e-204">Copy the API keys to your application.</span></span> <span data-ttu-id="0277e-205">Você pode obter as chaves no **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0277e-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="0277e-206">O token faz a asserção de uma declaração e tem uma data de validade.</span><span class="sxs-lookup"><span data-stu-id="0277e-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="0277e-207">O token é assinado com uma chave de acesso de API.</span><span class="sxs-lookup"><span data-stu-id="0277e-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="0277e-208">Solicitações do usuário para exibir um relatório.</span><span class="sxs-lookup"><span data-stu-id="0277e-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="0277e-209">O token é validado com uma chave de acesso de API.</span><span class="sxs-lookup"><span data-stu-id="0277e-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="0277e-210">O Power BI Embedded envia um relatório para o usuário.</span><span class="sxs-lookup"><span data-stu-id="0277e-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="0277e-211">Após o **Power BI Embedded** enviar um relatório para o usuário, o usuário pode exibir o relatório em seu aplicativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="0277e-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="0277e-212">Por exemplo, se você importou o [exemplo de PBIX Analisando Dados de Vendas](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), o aplicativo Web de exemplo teria essa aparência:</span><span class="sxs-lookup"><span data-stu-id="0277e-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="0277e-213">Consulte também</span><span class="sxs-lookup"><span data-stu-id="0277e-213">See Also</span></span>

[<span data-ttu-id="0277e-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="0277e-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="0277e-215">Introdução ao exemplo do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0277e-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="0277e-216">Cenários comuns do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0277e-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="0277e-217">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0277e-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="0277e-218">Repositório de Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="0277e-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="0277e-219">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="0277e-219">More questions?</span></span> [<span data-ttu-id="0277e-220">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="0277e-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)

