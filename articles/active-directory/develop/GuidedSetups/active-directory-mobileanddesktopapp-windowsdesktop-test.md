---
title: "aaaAzure AD v2 Windows Desktop Introdução - teste | Microsoft Docs"
description: "Como os aplicativos .NET da Área de Trabalho do Windows (XAML) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="7fc2b-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="7fc2b-103">Test your code</span></span>

<span data-ttu-id="7fc2b-104">Em ordem tootest seu aplicativo, pressione `F5` toorun seu projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="7fc2b-105">A Janela Principal deve ser exibida:</span><span class="sxs-lookup"><span data-stu-id="7fc2b-105">Your Main Window should appear:</span></span>

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="7fc2b-107">Quando você estiver pronto tootest, clique em *chamar a API do Microsoft Graph* e usar um Microsoft Azure Active Directory (conta organizacional) ou um toosign de conta Account da Microsoft (live.com, outlook.com) no.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="7fc2b-108">Ele é Olá primeira vez, você verá uma janela solicitando que usuário toosign em:</span><span class="sxs-lookup"><span data-stu-id="7fc2b-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Conexão](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="7fc2b-110">Consentimento</span><span class="sxs-lookup"><span data-stu-id="7fc2b-110">Consent</span></span>
<span data-ttu-id="7fc2b-111">Olá primeira vez que você entrar no aplicativo tooyour, você verá uma tela consentimento com, semelhante toohello de abaixo, onde você precisa aceitar tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="7fc2b-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Tela de consentimento](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="7fc2b-113">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="7fc2b-113">Expected results</span></span>
<span data-ttu-id="7fc2b-114">Você deve ver as informações de perfil do usuário retornadas pela chamada de API do Graph Microsoft hello na tela de resultados de chamadas de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="7fc2b-115">Você também verá informações básicas sobre o token Olá adquirido por meio de `AcquireTokenAsync` ou `AcquireTokenSilentAsync` na caixa de informações de Token hello:</span><span class="sxs-lookup"><span data-stu-id="7fc2b-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="7fc2b-116">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7fc2b-116">Property</span></span>  |<span data-ttu-id="7fc2b-117">Formatar</span><span class="sxs-lookup"><span data-stu-id="7fc2b-117">Format</span></span>  |<span data-ttu-id="7fc2b-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="7fc2b-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="7fc2b-119">Nome</span><span class="sxs-lookup"><span data-stu-id="7fc2b-119">Name</span></span> | <span data-ttu-id="7fc2b-120">{Nome completo do usuário}</span><span class="sxs-lookup"><span data-stu-id="7fc2b-120">{User Full name}</span></span> |<span data-ttu-id="7fc2b-121">primeiro e o último nome de usuário Olá</span><span class="sxs-lookup"><span data-stu-id="7fc2b-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="7fc2b-122">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="7fc2b-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="7fc2b-123">saudação de nome de usuário usado tooidentify usuário de saudação</span><span class="sxs-lookup"><span data-stu-id="7fc2b-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="7fc2b-124">O Token Expira</span><span class="sxs-lookup"><span data-stu-id="7fc2b-124">Token Expires</span></span> |<span data-ttu-id="7fc2b-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="7fc2b-125">{DateTime}</span></span>         |<span data-ttu-id="7fc2b-126">tempo de saudação na qual Olá token expira.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-126">hello time on which hello token expires.</span></span> <span data-ttu-id="7fc2b-127">MSAL estenderá a data de validade Olá para você renovando token hello quando necessário</span><span class="sxs-lookup"><span data-stu-id="7fc2b-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="7fc2b-128">Token de acesso</span><span class="sxs-lookup"><span data-stu-id="7fc2b-128">Access token</span></span> |<span data-ttu-id="7fc2b-129">{String}</span><span class="sxs-lookup"><span data-stu-id="7fc2b-129">{String}</span></span>         |<span data-ttu-id="7fc2b-130">cadeia de caracteres de token do Hello enviados que será enviado solicitações tooHTTP que exigem um cabeçalho de autorização</span><span class="sxs-lookup"><span data-stu-id="7fc2b-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="7fc2b-131">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="7fc2b-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="7fc2b-132">API do Graph requer Olá `user.read` tooread perfil de usuário do escopo.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="7fc2b-133">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="7fc2b-134">Algumas outras APIs do Graph, bem como APIs personalizadas do servidor de back-end, exigem escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="7fc2b-135">Por exemplo, para o gráfico, `Calendars.Read` é calendários do usuário toolist necessária.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="7fc2b-136">Em ordem tooaccess Olá calendário do usuário em um contexto de um aplicativo, você precisa tooadd `Calendars.Read` delegadas informações do registro do aplicativo e, em seguida, adicionar `Calendars.Read` toohello `AcquireTokenAsync` chamar.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="7fc2b-137">Usuário pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.</span><span class="sxs-lookup"><span data-stu-id="7fc2b-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



