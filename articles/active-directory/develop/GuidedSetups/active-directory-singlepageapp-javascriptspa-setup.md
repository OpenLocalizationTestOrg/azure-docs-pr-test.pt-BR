---
title: "aaaAzure AD v2 JS SPA interativa instalação - instalação | Microsoft Docs"
description: Como aplicativos JavaScript SPA podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="f1430-103">Configuração do servidor Web ou do projeto</span><span class="sxs-lookup"><span data-stu-id="f1430-103">Setting up your web server or project</span></span>

> <span data-ttu-id="f1430-104">Preferir toodownload projeto desse exemplo em vez disso?</span><span class="sxs-lookup"><span data-stu-id="f1430-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="f1430-105">Baixe o projeto do Visual Studio Olá</span><span class="sxs-lookup"><span data-stu-id="f1430-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="f1430-106">ou o</span><span class="sxs-lookup"><span data-stu-id="f1430-106">or</span></span>
> - <span data-ttu-id="f1430-107">[Baixar arquivos de projeto Olá](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) para um servidor web local, como Python</span><span class="sxs-lookup"><span data-stu-id="f1430-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="f1430-108">E, em seguida, ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes da execução.</span><span class="sxs-lookup"><span data-stu-id="f1430-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1430-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f1430-109">Prerequisites</span></span>
<span data-ttu-id="f1430-110">Um servidor web local como [Python http.server](https://www.python.org/downloads/), [http server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ou a integração com o IIS Express [2017 do Visual Studio](https://www.visualstudio.com/downloads/) é necessário toorun esta instalação interativa.</span><span class="sxs-lookup"><span data-stu-id="f1430-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="f1430-111">As instruções neste guia são baseadas em Python e 2017 do Visual Studio, mas se sentir livre toouse servidor Web ou qualquer outro ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f1430-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="f1430-112">Criar seu projeto</span><span class="sxs-lookup"><span data-stu-id="f1430-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="f1430-113">Opção 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f1430-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="f1430-114">Se você estiver usando o Visual Studio e criar um novo projeto, siga as etapas de saudação abaixo toocreate uma nova solução do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f1430-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="f1430-115">No Visual Studio:  `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="f1430-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="f1430-116">Em `Visual C#\Web`, selecione `ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="f1430-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="f1430-117">Nomeie o aplicativo e clique em *OK*</span><span class="sxs-lookup"><span data-stu-id="f1430-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="f1430-118">Em `New ASP.NET Web Application`, selecione `Empty`</span><span class="sxs-lookup"><span data-stu-id="f1430-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="f1430-119">Opção 2: Python/outros servidores Web</span><span class="sxs-lookup"><span data-stu-id="f1430-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="f1430-120">Verifique se você instalou [Python](https://www.python.org/downloads/), em seguida, siga a etapa de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="f1430-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="f1430-121">Crie uma pasta toohost seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1430-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="f1430-122">Criar a interface do usuário do aplicativo de página única</span><span class="sxs-lookup"><span data-stu-id="f1430-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="f1430-123">Crie um arquivo *index.html* para seu JavaScript SPA.</span><span class="sxs-lookup"><span data-stu-id="f1430-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="f1430-124">Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), clique com botão direito e selecione: `Add`  >  `New Item`  >  `HTML page` e nomeie-index</span><span class="sxs-lookup"><span data-stu-id="f1430-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="f1430-125">Adicione Olá página tooyour de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1430-125">Add hello following code tooyour page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
