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
## <a name="setting-up-your-web-server-or-project"></a>Configuração do servidor Web ou do projeto

> Preferir toodownload projeto desse exemplo em vez disso? 
> - [Baixe o projeto do Visual Studio Olá](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> ou o
> - [Baixar arquivos de projeto Olá](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) para um servidor web local, como Python
>
> E, em seguida, ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes da execução.

## <a name="prerequisites"></a>Pré-requisitos
Um servidor web local como [Python http.server](https://www.python.org/downloads/), [http server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ou a integração com o IIS Express [2017 do Visual Studio](https://www.visualstudio.com/downloads/) é necessário toorun esta instalação interativa. 

As instruções neste guia são baseadas em Python e 2017 do Visual Studio, mas se sentir livre toouse servidor Web ou qualquer outro ambiente de desenvolvimento.

## <a name="create-your-project"></a>Criar seu projeto 

> ### <a name="option-1-visual-studio"></a>Opção 1: Visual Studio 
> Se você estiver usando o Visual Studio e criar um novo projeto, siga as etapas de saudação abaixo toocreate uma nova solução do Visual Studio:
> 1.    No Visual Studio:  `File` > `New` > `Project`
> 2.    Em `Visual C#\Web`, selecione `ASP.NET Web Application (.NET Framework)`
> 3.    Nomeie o aplicativo e clique em *OK*
> 4.    Em `New ASP.NET Web Application`, selecione `Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Opção 2: Python/outros servidores Web
> Verifique se você instalou [Python](https://www.python.org/downloads/), em seguida, siga a etapa de saudação abaixo:
> - Crie uma pasta toohost seu aplicativo.


## <a name="create-your-single-page-applications-ui"></a>Criar a interface do usuário do aplicativo de página única
1.  Crie um arquivo *index.html* para seu JavaScript SPA. Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), clique com botão direito e selecione: `Add`  >  `New Item`  >  `HTML page` e nomeie-index
2.  Adicione Olá página tooyour de código a seguir:
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
