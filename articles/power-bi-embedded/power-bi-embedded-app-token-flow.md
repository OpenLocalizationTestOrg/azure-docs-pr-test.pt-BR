---
title: aaaAuthenticating e autorizar com o Power BI Embedded
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
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="59449-103">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="59449-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="59449-104">Olá serviço Power BI inserido usa **chaves** e **Tokens do aplicativo** para autenticação e autorização, em vez da autenticação explícita do usuário final.</span><span class="sxs-lookup"><span data-stu-id="59449-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="59449-105">Nesse modelo, seu aplicativo gerencia a autenticação e autorização para os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="59449-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="59449-106">Quando necessário, seu aplicativo cria e envia os Tokens de aplicativo hello que informa ao nosso serviço toorender Olá relatório solicitado.</span><span class="sxs-lookup"><span data-stu-id="59449-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="59449-107">Esse design não requer toouse seu aplicativo do Azure Active Directory para autenticação e autorização, embora você ainda pode.</span><span class="sxs-lookup"><span data-stu-id="59449-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="59449-108">Duas maneiras tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="59449-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="59449-109">**Chave** - você pode usar chaves para todas as chamadas à API de REST do Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="59449-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="59449-110">Olá chaves podem ser encontradas no hello **portal do Azure** clicando em **todas as configurações** e **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="59449-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="59449-111">Sempre use a chave como se fosse uma senha.</span><span class="sxs-lookup"><span data-stu-id="59449-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="59449-112">Essas chaves têm permissões toomake chamar qualquer API REST em uma coleção de espaço de trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="59449-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="59449-113">toouse uma chave em uma chamada REST, adicione Olá cabeçalho de autorização a seguir:</span><span class="sxs-lookup"><span data-stu-id="59449-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="59449-114">**Token de aplicativo** - tokens de aplicativo são usados para todas as solicitações de inserção.</span><span class="sxs-lookup"><span data-stu-id="59449-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="59449-115">Elas são projetadas toobe executado no cliente, para que eles sejam restritos tooa único relatório e suas tooset de prática recomendada de um tempo de expiração.</span><span class="sxs-lookup"><span data-stu-id="59449-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="59449-116">Os tokens de aplicativo são um JWT (Token Web JSON) assinado por uma das suas chaves.</span><span class="sxs-lookup"><span data-stu-id="59449-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="59449-117">O token de seu aplicativo pode conter Olá declarações a seguir:</span><span class="sxs-lookup"><span data-stu-id="59449-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="59449-118">Declaração</span><span class="sxs-lookup"><span data-stu-id="59449-118">Claim</span></span> | <span data-ttu-id="59449-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="59449-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="59449-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="59449-120">**ver**</span></span> |<span data-ttu-id="59449-121">versão de saudação do token de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="59449-121">hello version of hello app token.</span></span> <span data-ttu-id="59449-122">0.2.0 é a versão atual do hello.</span><span class="sxs-lookup"><span data-stu-id="59449-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="59449-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="59449-123">**aud**</span></span> |<span data-ttu-id="59449-124">Olá destinatário do token de saudação.</span><span class="sxs-lookup"><span data-stu-id="59449-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="59449-125">Para uso do Power BI Embedded: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="59449-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="59449-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="59449-126">**iss**</span></span> |<span data-ttu-id="59449-127">Uma cadeia de caracteres que indica o aplicativo hello que emitiu o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="59449-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="59449-128">**tipo**</span><span class="sxs-lookup"><span data-stu-id="59449-128">**type**</span></span> |<span data-ttu-id="59449-129">tipo de saudação do token de aplicativo que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="59449-129">hello type of app token which is being created.</span></span> <span data-ttu-id="59449-130">Tipo de saudação só tem suportada atual é **inserir**.</span><span class="sxs-lookup"><span data-stu-id="59449-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="59449-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="59449-131">**wcn**</span></span> |<span data-ttu-id="59449-132">Token de saudação do nome de coleção do espaço de trabalho está sendo emitido para.</span><span class="sxs-lookup"><span data-stu-id="59449-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="59449-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="59449-133">**wid**</span></span> |<span data-ttu-id="59449-134">Token de saudação de ID do espaço de trabalho está sendo emitido para.</span><span class="sxs-lookup"><span data-stu-id="59449-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="59449-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="59449-135">**rid**</span></span> |<span data-ttu-id="59449-136">Token de saudação do ID de relatório está sendo emitido para.</span><span class="sxs-lookup"><span data-stu-id="59449-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="59449-137">**nome de usuário** (opcional)</span><span class="sxs-lookup"><span data-stu-id="59449-137">**username** (optional)</span></span> |<span data-ttu-id="59449-138">Usado com a RLS, isso é uma cadeia de caracteres que pode ajudar a identificar o usuário Olá ao aplicar regras RLS.</span><span class="sxs-lookup"><span data-stu-id="59449-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="59449-139">**funções** (opcional)</span><span class="sxs-lookup"><span data-stu-id="59449-139">**roles** (optional)</span></span> |<span data-ttu-id="59449-140">Uma cadeia de caracteres que contém a saudação funções tooselect ao aplicar regras de segurança em nível de linha.</span><span class="sxs-lookup"><span data-stu-id="59449-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="59449-141">Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="59449-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="59449-142">**SCP** (opcional)</span><span class="sxs-lookup"><span data-stu-id="59449-142">**scp** (optional)</span></span> |<span data-ttu-id="59449-143">Uma cadeia de caracteres que contém escopos de permissões de saudação.</span><span class="sxs-lookup"><span data-stu-id="59449-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="59449-144">Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="59449-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="59449-145">**exp** (opcional)</span><span class="sxs-lookup"><span data-stu-id="59449-145">**exp** (optional)</span></span> |<span data-ttu-id="59449-146">Indica o tempo de saudação na qual Olá token irá expirar.</span><span class="sxs-lookup"><span data-stu-id="59449-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="59449-147">Elas devem ser transmitidas como carimbos de data/hora do Unix.</span><span class="sxs-lookup"><span data-stu-id="59449-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="59449-148">**nbf** (opcional)</span><span class="sxs-lookup"><span data-stu-id="59449-148">**nbf** (optional)</span></span> |<span data-ttu-id="59449-149">Indica o tempo de saudação na qual Olá token inicia válido.</span><span class="sxs-lookup"><span data-stu-id="59449-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="59449-150">Elas devem ser transmitidas como carimbos de data/hora do Unix.</span><span class="sxs-lookup"><span data-stu-id="59449-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="59449-151">Um token do aplicativo de exemplo terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="59449-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="59449-152">Quando decodificado, ele terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="59449-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="59449-153">Há métodos disponíveis no hello SDKs que facilitam a criação de apptokens.</span><span class="sxs-lookup"><span data-stu-id="59449-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="59449-154">Por exemplo, para .NET você pode examinar Olá [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe e hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) métodos.</span><span class="sxs-lookup"><span data-stu-id="59449-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="59449-155">Para Olá .NET SDK, consulte muito[escopos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="59449-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="59449-156">Escopos</span><span class="sxs-lookup"><span data-stu-id="59449-156">Scopes</span></span>

<span data-ttu-id="59449-157">Ao usar tokens de inserção, talvez você queira toorestrict de uso dos recursos de saudação que concedem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="59449-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="59449-158">Por esse motivo, você pode gerar um token com as permissões no escopo.</span><span class="sxs-lookup"><span data-stu-id="59449-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="59449-159">Olá seguem escopos disponíveis de saudação para Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="59449-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="59449-160">Escopo</span><span class="sxs-lookup"><span data-stu-id="59449-160">Scope</span></span>|<span data-ttu-id="59449-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="59449-161">Description</span></span>|
|---|---|
|<span data-ttu-id="59449-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="59449-162">Dataset.Read</span></span>|<span data-ttu-id="59449-163">Fornece permissão tooread Olá especificado o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="59449-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="59449-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="59449-164">Dataset.Write</span></span>|<span data-ttu-id="59449-165">Fornece permissão toowrite toohello especificado conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="59449-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="59449-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="59449-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="59449-167">Fornece permissão tooread e gravação toohello especificado conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="59449-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="59449-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="59449-168">Report.Read</span></span>|<span data-ttu-id="59449-169">Fornece permissão tooview Olá especificado de relatório.</span><span class="sxs-lookup"><span data-stu-id="59449-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="59449-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="59449-170">Report.ReadWrite</span></span>|<span data-ttu-id="59449-171">Fornece a edição e a permissão tooview Olá relatório especificado.</span><span class="sxs-lookup"><span data-stu-id="59449-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="59449-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="59449-172">Workspace.Report.Create</span></span>|<span data-ttu-id="59449-173">Fornece permissão toocreate um novo relatório em Olá especificado espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="59449-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="59449-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="59449-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="59449-175">Fornece um relatório existente dentro de saudação especificado de permissão tooclone espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="59449-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="59449-176">Você pode fornecer vários escopos usando um espaço entre escopos hello como Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="59449-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="59449-177">**Declarações necessárias - escopos**</span><span class="sxs-lookup"><span data-stu-id="59449-177">**Required claims - scopes**</span></span>

<span data-ttu-id="59449-178">SCP: scopesClaim {scopesClaim} pode ser uma cadeia de caracteres ou uma matriz de cadeias de caracteres, observando Olá permitido permissões tooworkspace recursos (relatório, conjunto de dados, etc.)</span><span class="sxs-lookup"><span data-stu-id="59449-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="59449-179">Um token decodificado, com escopos definidos, seria a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="59449-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="59449-180">Operações e escopos</span><span class="sxs-lookup"><span data-stu-id="59449-180">Operations and scopes</span></span>

|<span data-ttu-id="59449-181">Operação</span><span class="sxs-lookup"><span data-stu-id="59449-181">Operation</span></span>|<span data-ttu-id="59449-182">Recurso de destino</span><span class="sxs-lookup"><span data-stu-id="59449-182">Target resource</span></span>|<span data-ttu-id="59449-183">Permissões de token</span><span class="sxs-lookup"><span data-stu-id="59449-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="59449-184">Criar (na memória) um novo relatório com base em um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="59449-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="59449-185">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="59449-185">Dataset</span></span>|<span data-ttu-id="59449-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="59449-186">Dataset.Read</span></span>|
|<span data-ttu-id="59449-187">Criar um novo relatório com base em um conjunto de dados a (na memória) e salve o relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="59449-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="59449-188">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="59449-188">Dataset</span></span>|<span data-ttu-id="59449-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="59449-189">* Dataset.Read</span></span><br><span data-ttu-id="59449-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="59449-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="59449-191">Exibir e explorar/Editar (na memória) um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="59449-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="59449-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="59449-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="59449-193">Isso não permitirá que permissões toosave edições.</span><span class="sxs-lookup"><span data-stu-id="59449-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="59449-194">Relatório</span><span class="sxs-lookup"><span data-stu-id="59449-194">Report</span></span>|<span data-ttu-id="59449-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="59449-195">Report.Read</span></span>|
|<span data-ttu-id="59449-196">Editar e salvar um relatório existente.</span><span class="sxs-lookup"><span data-stu-id="59449-196">Edit and save an existing report.</span></span>|<span data-ttu-id="59449-197">Relatório</span><span class="sxs-lookup"><span data-stu-id="59449-197">Report</span></span>|<span data-ttu-id="59449-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="59449-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="59449-199">Salvar uma cópia de um relatório (Salvar como).</span><span class="sxs-lookup"><span data-stu-id="59449-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="59449-200">Relatório</span><span class="sxs-lookup"><span data-stu-id="59449-200">Report</span></span>|<span data-ttu-id="59449-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="59449-201">* Report.Read</span></span><br><span data-ttu-id="59449-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="59449-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="59449-203">Como funciona o fluxo de saudação</span><span class="sxs-lookup"><span data-stu-id="59449-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="59449-204">Copie o aplicativo de tooyour de chaves de API hello.</span><span class="sxs-lookup"><span data-stu-id="59449-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="59449-205">Você pode obter chaves de saudação em **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="59449-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="59449-206">O token faz a asserção de uma declaração e tem uma data de validade.</span><span class="sxs-lookup"><span data-stu-id="59449-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="59449-207">O token é assinado com uma chave de acesso de API.</span><span class="sxs-lookup"><span data-stu-id="59449-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="59449-208">Usuário solicita tooview um relatório.</span><span class="sxs-lookup"><span data-stu-id="59449-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="59449-209">O token é validado com uma chave de acesso de API.</span><span class="sxs-lookup"><span data-stu-id="59449-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="59449-210">Power BI inserido envia um relatório toouser.</span><span class="sxs-lookup"><span data-stu-id="59449-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="59449-211">Depois de **Power BI inserido** envia um usuário do relatório toohello, usuário Olá pode exibir o relatório de saudação em seu aplicativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="59449-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="59449-212">Por exemplo, se você importou Olá [exemplo PBIX de dados de vendas analisando](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), aplicativo de web de exemplo hello teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="59449-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="59449-213">Consulte também</span><span class="sxs-lookup"><span data-stu-id="59449-213">See Also</span></span>

[<span data-ttu-id="59449-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="59449-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="59449-215">Introdução ao exemplo do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="59449-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="59449-216">Cenários comuns do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="59449-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="59449-217">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="59449-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="59449-218">Repositório de Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="59449-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="59449-219">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="59449-219">More questions?</span></span> [<span data-ttu-id="59449-220">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="59449-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

