---
title: "Instalação guiada do JS SPA no Azure AD v2 – teste | Microsoft Docs"
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
ms.openlocfilehash: c888760ab311e8ac08b1e625bb837f91047db645
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="test-your-code"></a><span data-ttu-id="0aa23-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="0aa23-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="0aa23-104">Testes com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0aa23-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="0aa23-105">Se estiver usando o Visual Studio, pressione `F5` para executar o projeto: o navegador abrirá e direcionará você para *http://localhost:{porta}*, no qual você vê o botão *Chamar a API do Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="0aa23-105">If you are using Visual Studio, press `F5` to run your project: the browser opens and directs you to *http://localhost:{port}* where you see the *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="0aa23-106">Testando com Python ou outro servidor Web</span><span class="sxs-lookup"><span data-stu-id="0aa23-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="0aa23-107">Se não estiver usando o Visual Studio, certifique-se de que seu servidor Web tenha sido iniciado e de que esteja configurado para escutar uma porta TCP baseada na parte que contém seu arquivo *index.html*.</span><span class="sxs-lookup"><span data-stu-id="0aa23-107">If you are not using Visual Studio, make sure your web server is started and it is configured to listen to a TCP port based on the folder containing your *index.html* file.</span></span> <span data-ttu-id="0aa23-108">Para o Python, você pode começar a escutar a porta executando o prompt de comando/ terminal, na pasta do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="0aa23-108">For Python, you can start listening to the port by running the in the command prompt/ terminal, from the app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="0aa23-109">Em seguida, abra o navegador e digite *http://localhost:8080* ou *http://localhost:{porta}*, em que *porta* corresponde à porta que o servidor Web está escutando.</span><span class="sxs-lookup"><span data-stu-id="0aa23-109">Then, open the browser and type *http://localhost:8080* or *http://localhost:{port}* - where the *port* corresponds to the port that your web server is listening to.</span></span> <span data-ttu-id="0aa23-110">Você deve ver o conteúdo da página index.html com o botão *Chamar a API do Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="0aa23-110">You should see the contents of your index.html page with the *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="0aa23-111">Teste seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="0aa23-111">Test your application</span></span>

<span data-ttu-id="0aa23-112">Após o navegador carregar seu *index.html*, clique no botão *Chamar a API do Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="0aa23-112">After the browser loads your *index.html*, click the *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="0aa23-113">Se esta for a primeira vez, o navegador o redirecionará para o ponto de extremidade do Microsoft Azure Active Directory v2, em que você precisará entrar.</span><span class="sxs-lookup"><span data-stu-id="0aa23-113">If this is the first time, the browser redirects you to the Microsoft Azure Active Directory v2 endpoint, where you are  prompted to sign in.</span></span>
 
![Captura de tela de exemplo](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="0aa23-115">Consentimento</span><span class="sxs-lookup"><span data-stu-id="0aa23-115">Consent</span></span>
<span data-ttu-id="0aa23-116">Na primeira vez que você entrar no aplicativo, será apresentada uma tela de consentimento semelhante à tela abaixo, na qual você precisa aceitar:</span><span class="sxs-lookup"><span data-stu-id="0aa23-116">The very first time you sign in to your application, you are presented with a consent screen similar to the following, where you need to accept:</span></span>

 ![Tela de consentimento](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="0aa23-118">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="0aa23-118">Expected results</span></span>
<span data-ttu-id="0aa23-119">Você deverá ver as informações de perfil do usuário retornadas pela resposta à chamada à API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="0aa23-119">You should see user profile information returned by the Microsoft Graph API call response.</span></span>
 
 ![Resultados](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="0aa23-121">Você também verá informações básicas sobre o token adquirido nas caixas *Token de Acesso* e *Declarações do Token de ID*.</span><span class="sxs-lookup"><span data-stu-id="0aa23-121">You also see basic information about the token acquired in the *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="0aa23-122">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="0aa23-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="0aa23-123">A API do Microsoft Graph requer o escopo `user.read` para ler o perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="0aa23-123">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="0aa23-124">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="0aa23-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="0aa23-125">Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="0aa23-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="0aa23-126">Por exemplo, para o Microsoft Graph, o escopo `Calendars.Read` é necessário para listar os calendários do usuário.</span><span class="sxs-lookup"><span data-stu-id="0aa23-126">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="0aa23-127">Para acessar o calendário do usuário no contexto de um aplicativo, é necessário adicionar a permissão delegada `Calendars.Read` às informações de registro do aplicativo e, em seguida, adicionar o escopo `Calendars.Read` à chamada `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="0aa23-127">In order to access the user’s calendar in the context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="0aa23-128">Talvez o usuário precise fornecer consentimentos adicionais à medida que o número de escopos aumentar.</span><span class="sxs-lookup"><span data-stu-id="0aa23-128">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<span data-ttu-id="0aa23-129">Se uma API de back-end não exigir um escopo (não recomendado), será possível usar o `clientId` como o escopo nas chamadas `acquireTokenSilent` e/ou `acquireTokenRedirect`.</span><span class="sxs-lookup"><span data-stu-id="0aa23-129">If a backend API does not require a scope (not recommended), you can use the `clientId` as the scope in the `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
