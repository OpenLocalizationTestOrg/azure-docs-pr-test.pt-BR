---
title: "Introdução à Área de Trabalho do Windows no Azure AD v2 – Teste | Microsoft Docs"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="556e4-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="556e4-103">Test your code</span></span>

<span data-ttu-id="556e4-104">Para testar seu aplicativo, pressione `F5` para executar o projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="556e4-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="556e4-105">A Janela Principal deve ser exibida:</span><span class="sxs-lookup"><span data-stu-id="556e4-105">Your Main Window should appear:</span></span>

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="556e4-107">Quando você estiver pronto para testar, clique em *Chamar API do Microsoft Graph* e use uma conta do Microsoft Azure Active Directory (conta organizacional) ou uma Conta da Microsoft (live.com, outlook.com) para se conectar.</span><span class="sxs-lookup"><span data-stu-id="556e4-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="556e4-108">Se esta for a primeira vez, você verá uma janela solicitando o usuário a entrar:</span><span class="sxs-lookup"><span data-stu-id="556e4-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Conexão](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="556e4-110">Consentimento</span><span class="sxs-lookup"><span data-stu-id="556e4-110">Consent</span></span>
<span data-ttu-id="556e4-111">Na primeira vez que você entrar no aplicativo, será apresentada uma tela de consentimento semelhante à tela abaixo, na qual você precisa aceitar explicitamente:</span><span class="sxs-lookup"><span data-stu-id="556e4-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Tela de consentimento](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="556e4-113">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="556e4-113">Expected results</span></span>
<span data-ttu-id="556e4-114">Você deverá ver as informações de perfil do usuário retornadas pela chamada à API do Microsoft Graph na tela Resultados da Chamada à API.</span><span class="sxs-lookup"><span data-stu-id="556e4-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="556e4-115">Você também deverá ver informações básicas sobre o token adquirido por meio de `AcquireTokenAsync` ou `AcquireTokenSilentAsync` na caixa Informações de Token:</span><span class="sxs-lookup"><span data-stu-id="556e4-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="556e4-116">Propriedade</span><span class="sxs-lookup"><span data-stu-id="556e4-116">Property</span></span>  |<span data-ttu-id="556e4-117">Formatar</span><span class="sxs-lookup"><span data-stu-id="556e4-117">Format</span></span>  |<span data-ttu-id="556e4-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="556e4-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="556e4-119">Nome</span><span class="sxs-lookup"><span data-stu-id="556e4-119">Name</span></span> | <span data-ttu-id="556e4-120">{Nome completo do usuário}</span><span class="sxs-lookup"><span data-stu-id="556e4-120">{User Full name}</span></span> |<span data-ttu-id="556e4-121">Nome e sobrenome do usuário</span><span class="sxs-lookup"><span data-stu-id="556e4-121">The user’s first and last name</span></span>|
|<span data-ttu-id="556e4-122">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="556e4-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="556e4-123">O nome de usuário usado para identificar o usuário</span><span class="sxs-lookup"><span data-stu-id="556e4-123">The username used to identify the user</span></span>|
|<span data-ttu-id="556e4-124">O Token Expira</span><span class="sxs-lookup"><span data-stu-id="556e4-124">Token Expires</span></span> |<span data-ttu-id="556e4-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="556e4-125">{DateTime}</span></span>         |<span data-ttu-id="556e4-126">A data e a hora em que o token expira.</span><span class="sxs-lookup"><span data-stu-id="556e4-126">The time on which the token expires.</span></span> <span data-ttu-id="556e4-127">A MSAL estenderá a data de expiração para você renovando o token quando necessário</span><span class="sxs-lookup"><span data-stu-id="556e4-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="556e4-128">Token de acesso</span><span class="sxs-lookup"><span data-stu-id="556e4-128">Access token</span></span> |<span data-ttu-id="556e4-129">{String}</span><span class="sxs-lookup"><span data-stu-id="556e4-129">{String}</span></span>         |<span data-ttu-id="556e4-130">A cadeia de caracteres do token enviada que será enviada para solicitações HTTP que exigem um cabeçalho de autorização</span><span class="sxs-lookup"><span data-stu-id="556e4-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="556e4-131">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="556e4-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="556e4-132">A API do Graph precisa do escopo `user.read` para ler o perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="556e4-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="556e4-133">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="556e4-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="556e4-134">Algumas outras APIs do Graph, bem como APIs personalizadas do servidor de back-end, exigem escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="556e4-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="556e4-135">Por exemplo, para o Graph, `Calendars.Read` é necessário para listar os calendários do usuário.</span><span class="sxs-lookup"><span data-stu-id="556e4-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="556e4-136">Para acessar o calendário do usuário no contexto de um aplicativo, você precisa adicionar as informações de registro do aplicativo delegado `Calendars.Read` e, em seguida, adicionar `Calendars.Read` à chamada `AcquireTokenAsync`.</span><span class="sxs-lookup"><span data-stu-id="556e4-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="556e4-137">O usuário pode precisar fornecer consentimentos adicionais à medida que o número de escopos aumenta.</span><span class="sxs-lookup"><span data-stu-id="556e4-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



