---
title: "aaaAzure AD v2 JS SPA interativa instalação - uso | Microsoft Docs"
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
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="57582-103">Use Olá biblioteca de autenticação da Microsoft (MSAL) Olá toosign no usuário</span><span class="sxs-lookup"><span data-stu-id="57582-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="57582-104">Crie um arquivo chamado `app.js`.</span><span class="sxs-lookup"><span data-stu-id="57582-104">Create a file named `app.js`.</span></span> <span data-ttu-id="57582-105">Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), clique com botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="57582-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="57582-106">Adicionar Olá tooyour de código a seguir `app.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="57582-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="57582-107">Mais informações</span><span class="sxs-lookup"><span data-stu-id="57582-107">More Information</span></span>

<span data-ttu-id="57582-108">Depois que um usuário clica Olá *'Chamar Microsoft Graph API'* botão para Olá primeira vez, `callGraphApi` chamadas de método `loginRedirect` toosign usuário hello.</span><span class="sxs-lookup"><span data-stu-id="57582-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="57582-109">Esse método resulta em redirecionando Olá usuário toohello *o ponto de extremidade do Active Directory do Microsoft Azure v2* tooprompt e validar as credenciais do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="57582-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="57582-110">Como resultado de uma bem-sucedida entrar, o usuário de saudação é redirecionado toohello back original *index* página e um token for recebida, processada por `msal.js` e informações de saudação contidas no token de saudação é armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="57582-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="57582-111">Esse token é conhecido como Olá *token de ID* e contém informações básicas sobre o usuário hello, como nome de exibição do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="57582-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="57582-112">Se você planejar toouse todos os dados fornecidos por esse token para qualquer finalidade, você precisa toomake-se de que esse token é validado por seu tooguarantee de servidor de back-end Olá token foi emitidos tooa de usuário válido para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57582-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="57582-113">Olá SPA gerado por este guia não faz uso diretamente do token de ID de hello – em vez disso, ele chama `acquireTokenSilent` e/ou `acquireTokenRedirect` tooacquire um *token de acesso* usado tooquery Olá Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="57582-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="57582-114">Se você precisar de um exemplo que valida o token de ID hello, dê uma olhada [isso](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemplo active-directory-javascript-singlepageapp-dotnet-webapi-v2 Github") usa o aplicativo de exemplo no GitHub – exemplo hello uma API da Web do ASP.NET para validação de token.</span><span class="sxs-lookup"><span data-stu-id="57582-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="57582-115">Obtendo um token de usuário interativamente</span><span class="sxs-lookup"><span data-stu-id="57582-115">Getting a user token interactively</span></span>

<span data-ttu-id="57582-116">Após a saudação inicial entrar, você não quiser Olá peça tooreauthenticate usuários sempre que precisarem toorequest um token tooaccess um recurso – portanto *acquireTokenSilent* devem ser usados na maioria dos tokens de tooacquire de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="57582-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="57582-117">Há situações porém que você precisa tooforce os usuários interagem com o ponto de extremidade do Active Directory do Azure v2 – alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="57582-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="57582-118">Os usuários podem precisar tooreenter suas credenciais porque Olá senha expirou</span><span class="sxs-lookup"><span data-stu-id="57582-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="57582-119">Seu aplicativo está solicitando o recurso de tooa de acesso que Olá tooconsent de necessidades de usuário para</span><span class="sxs-lookup"><span data-stu-id="57582-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="57582-120">A autenticação de dois fatores é necessária</span><span class="sxs-lookup"><span data-stu-id="57582-120">Two factor authentication is required</span></span>

<span data-ttu-id="57582-121">Olá chamada *acquireTokenRedirect(scope)* resultar em redirecionando o ponto de extremidade do usuários toohello v2 do Active Directory do Azure (ou *acquireTokenPopup(scope)* resultados em uma janela pop-up) em que os usuários precisam toointeract com confirmando a suas credenciais, dando Olá consentimento toohello necessários recursos ou autenticação de dois fatores Olá concluído.</span><span class="sxs-lookup"><span data-stu-id="57582-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="57582-122">Obtendo um token de usuário no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="57582-122">Getting a user token silently</span></span>
<span data-ttu-id="57582-123">Olá ` acquireTokenSilent` método trata aquisições de token e renovação sem qualquer interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="57582-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="57582-124">Depois de `loginRedirect` (ou `loginPopup`) é executado para Olá primeira vez, `acquireTokenSilent` é Olá método usado tooobtain tokens usados tooaccess recursos para as chamadas subsequentes - protegidos como chamadas toorequest ou renovar os tokens são feitas silenciosamente.</span><span class="sxs-lookup"><span data-stu-id="57582-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="57582-125">`acquireTokenSilent`pode falhar em alguns casos – por exemplo, a senha do usuário Olá expirou.</span><span class="sxs-lookup"><span data-stu-id="57582-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="57582-126">O aplicativo pode tratar essa exceção de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="57582-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="57582-127">Fazer uma chamada muito`acquireTokenRedirect` imediatamente, o que resulta em solicitando Olá toosign de usuário no.</span><span class="sxs-lookup"><span data-stu-id="57582-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="57582-128">Esse padrão é comumente usado em aplicativos online onde não há nenhum conteúdo não autenticado no hello aplicativo toohello disponíveis do usuário.</span><span class="sxs-lookup"><span data-stu-id="57582-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="57582-129">exemplo Hello gerado por esta instalação interativa usa esse padrão.</span><span class="sxs-lookup"><span data-stu-id="57582-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="57582-130">Os aplicativos também podem fazer um usuário toohello indicação visual que uma entrada interativa é necessária para que o usuário Olá pode selecionar Olá hora certa toosign em ou aplicativo hello pode repetir `acquireTokenSilent` mais tarde.</span><span class="sxs-lookup"><span data-stu-id="57582-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="57582-131">Isso é geralmente usado quando o usuário Olá pode usar outras funcionalidades de aplicativo hello sem interrupção — por exemplo, há conteúdo não autenticado disponíveis no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="57582-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="57582-132">Nesse caso, o usuário de saudação pode decidir quando quiserem toosign no recurso de saudação protegido tooaccess ou toorefresh Olá desatualizado informações.</span><span class="sxs-lookup"><span data-stu-id="57582-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="57582-133">Chamar API do Microsoft Graph hello usando Olá token obtido apenas</span><span class="sxs-lookup"><span data-stu-id="57582-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="57582-134">Adicionar Olá tooyour de código a seguir `app.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="57582-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="57582-135">Mais informações sobre como fazer uma chamada REST em uma API protegida</span><span class="sxs-lookup"><span data-stu-id="57582-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="57582-136">No aplicativo de exemplo hello criado por este guia, Olá `callWebApiWithToken()` método é usado toomake um HTTP `GET` solicitação em um recurso protegido que requer um chamador de conteúdo toohello Olá token e retornar.</span><span class="sxs-lookup"><span data-stu-id="57582-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="57582-137">Este método adiciona token Olá adquirido em Olá *cabeçalho de autorização HTTP*.</span><span class="sxs-lookup"><span data-stu-id="57582-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="57582-138">Para o aplicativo de exemplo hello criado por este guia, o recurso de saudação é Olá Microsoft Graph API *me* ponto de extremidade – que exibe informações de perfil do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="57582-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="57582-139">Adicionar um toosign método usuário Olá</span><span class="sxs-lookup"><span data-stu-id="57582-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="57582-140">Adicionar Olá tooyour de código a seguir `app.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="57582-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
