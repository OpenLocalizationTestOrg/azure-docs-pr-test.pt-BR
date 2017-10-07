---
title: "aaaAzure AD v2 JS SPA interativa instalação - teste | Microsoft Docs"
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="fbd14-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="fbd14-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="fbd14-104">Testes com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbd14-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="fbd14-105">Se você estiver usando o Visual Studio, pressione `F5` toorun seu projeto: navegador Olá abre e direciona você muito*http://localhost: {port}* onde você pode ver Olá *chamar a API do Microsoft Graph* botão.</span><span class="sxs-lookup"><span data-stu-id="fbd14-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="fbd14-106">Testando com Python ou outro servidor Web</span><span class="sxs-lookup"><span data-stu-id="fbd14-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="fbd14-107">Se você não estiver usando o Visual Studio, verifique se seu servidor web é iniciado e está configurado a porta TCP de tooa toolisten com base em Olá pasta que contém o *index* arquivo.</span><span class="sxs-lookup"><span data-stu-id="fbd14-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="fbd14-108">Para Python, você pode iniciar a escuta a porta toohello executando Olá no comando Olá prompt / terminal, na pasta do aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="fbd14-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="fbd14-109">Em seguida, abra o navegador hello e digite *http://localhost:8080* ou *http://localhost: {port}* - onde hello *porta* corresponde a porta de toohello seu servidor web escuta.</span><span class="sxs-lookup"><span data-stu-id="fbd14-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="fbd14-110">Você deve ver o conteúdo de saudação da página do index com hello *chamar a API do Microsoft Graph* botão.</span><span class="sxs-lookup"><span data-stu-id="fbd14-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="fbd14-111">Teste seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="fbd14-111">Test your application</span></span>

<span data-ttu-id="fbd14-112">Depois de navegador Olá carrega sua *index*, clique em hello *chamar a API do Microsoft Graph* botão.</span><span class="sxs-lookup"><span data-stu-id="fbd14-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="fbd14-113">Se isso for Olá pela primeira vez, Olá redirecionamentos do navegador você toohello v2 do Active Directory do Microsoft Azure ponto de extremidade, onde você está solicitado toosign no.</span><span class="sxs-lookup"><span data-stu-id="fbd14-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Captura de tela de exemplo](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="fbd14-115">Consentimento</span><span class="sxs-lookup"><span data-stu-id="fbd14-115">Consent</span></span>
<span data-ttu-id="fbd14-116">Hello primeira vez que entrar no aplicativo tooyour, você verá um consentimento tela semelhante toohello seguinte, em que você precisa tooaccept:</span><span class="sxs-lookup"><span data-stu-id="fbd14-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Tela de consentimento](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="fbd14-118">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="fbd14-118">Expected results</span></span>
<span data-ttu-id="fbd14-119">Você deve ver as informações de perfil de usuário retornadas pelo hello resposta de chamada de API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="fbd14-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Resultados](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="fbd14-121">Você também ver informações básicas sobre o token Olá adquirido em Olá *Token de acesso* e *declarações do Token de ID* caixas.</span><span class="sxs-lookup"><span data-stu-id="fbd14-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="fbd14-122">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="fbd14-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="fbd14-123">Olá Microsoft Graph API requer Olá `user.read` tooread Olá perfil de usuário do escopo.</span><span class="sxs-lookup"><span data-stu-id="fbd14-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="fbd14-124">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="fbd14-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="fbd14-125">Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="fbd14-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="fbd14-126">Por exemplo, para o Microsoft Graph, Olá escopo `Calendars.Read` é calendários do usuário de saudação toolist necessária.</span><span class="sxs-lookup"><span data-stu-id="fbd14-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="fbd14-127">Em ordem tooaccess Olá calendário do usuário no contexto de saudação de um aplicativo, você precisa Olá tooadd `Calendars.Read` delegado informações do registro do aplicativo permissão toohello e adicione Olá `Calendars.Read` toohello escopo `acquireTokenSilent` chamar.</span><span class="sxs-lookup"><span data-stu-id="fbd14-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="fbd14-128">usuário Olá pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.</span><span class="sxs-lookup"><span data-stu-id="fbd14-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="fbd14-129">Se uma API de back-end não exigir um escopo (não recomendado), você pode usar o hello `clientId` como escopo Olá Olá `acquireTokenSilent` e/ou `acquireTokenRedirect` chamadas.</span><span class="sxs-lookup"><span data-stu-id="fbd14-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
