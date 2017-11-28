---
title: "Instalação guiada do JS SPA no Azure AD v2 – uso | Microsoft Docs"
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
ms.openlocfilehash: f52157df298ddfc1c1b29a18dc9a54aae59b52a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-sign-in-the-user"></a><span data-ttu-id="cf49e-103">Use a MSAL (Biblioteca de Autenticação da Microsoft) para conectar o usuário</span><span class="sxs-lookup"><span data-stu-id="cf49e-103">Use the Microsoft Authentication Library (MSAL) to sign-in the user</span></span>

1.  <span data-ttu-id="cf49e-104">Crie um arquivo chamado `app.js`.</span><span class="sxs-lookup"><span data-stu-id="cf49e-104">Create a file named `app.js`.</span></span> <span data-ttu-id="cf49e-105">Se você estiver usando o Visual Studio, selecione o projeto (pasta raiz do projeto), clique com o botão direito do mouse e selecione: `Add` > `New Item` > `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="cf49e-105">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="cf49e-106">Adicione o seguinte código ao seu arquivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="cf49e-106">Add the following code to your `app.js` file:</span></span>

```javascript
// Graph API endpoint to show user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used to obtain the access token to read user profile
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
    // If page is refreshed, continue to display user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call the Microsoft Graph API and display the results on the page. Sign the user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user to sign in via loginRedirect.
        // This will redirect user to the Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // The call to loginRedirect above frontloads the consent to query Graph API during the sign-in.
        // If you want to use dynamic consent, just remove the graphAPIScopes from loginRedirect call.
        // As such, user will be prompted to give consent when requested access to a resource that 
        // he/she hasn't consented before. In the case of this application - 
        // the first time the Graph API call to obtain user's profile is executed.
    } else {
        // If user is already signed in, display the user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API to show the user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order to call the Graph API, an access token needs to be acquired.
        // Try to acquire the token used to query Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After the access token is acquired, call the Web API, sending the acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If the acquireTokenSilent() method fails, then acquire the token interactively via acquireTokenRedirect().
                // In this case, the browser will redirect user back to the Azure Active Directory v2 Endpoint so the user 
                // can reenter the current username/ password and/ or give consent to new permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get the token silently, the Graph API call results will be made and results will be displayed in the page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() to show results.
 * @param {string} errorDesc - If error occur, the error message
 * @param {object} token - The token received from login
 * @param {object} error - The error string
 * @param {string} tokenType - the token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in the page
 * @param {string} endpoint - the endpoint used for the error message
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
### <a name="more-information"></a><span data-ttu-id="cf49e-107">Mais informações</span><span class="sxs-lookup"><span data-stu-id="cf49e-107">More Information</span></span>

<span data-ttu-id="cf49e-108">Depois que um usuário clicar no botão *'Chamar a API do Microsoft Graph'* pela primeira vez, o método `callGraphApi` chama `loginRedirect` para conectar o usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-108">After a user clicks the *‘Call Microsoft Graph API’* button for the first time, `callGraphApi` method calls `loginRedirect` to sign in the user.</span></span> <span data-ttu-id="cf49e-109">Esse método resulta no redirecionamento do usuário para o *ponto de extremidade do Microsoft Azure Active Directory v2* para solicitar e validar as credenciais do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-109">This method results in redirecting the user to the *Microsoft Azure Active Directory v2 endpoint* to prompt and validate the user's credentials.</span></span> <span data-ttu-id="cf49e-110">Como resultado de uma entrada bem-sucedida, o usuário é redirecionado para a página *index.html* original e um token é recebido, processado por `msal.js` e as informações contidas no token são armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="cf49e-110">As a result of a successful sign-in, the user is redirected back to the original *index.html* page, and a token is received, processed by `msal.js` and the information contained in the token is cached.</span></span> <span data-ttu-id="cf49e-111">Esse token é conhecido como o *token de ID* e contém informações básicas sobre o usuário, como o nome de exibição do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-111">This token is known as the *ID token* and contains basic information about the user, such as the user display name.</span></span> <span data-ttu-id="cf49e-112">Se você planeja usar os dados fornecidos por esse token para qualquer finalidade, é necessário certificar-se de que esse token seja validado pelo servidor de back-end para ter certeza de que o token foi emitido para um usuário válido para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf49e-112">If you plan to use any data provided by this token for any purposes, you need to make sure this token is validated by your backend server to guarantee that the token was issued to a valid user for your application.</span></span>

<span data-ttu-id="cf49e-113">O SPA gerado por este guia não faz uso diretamente do Token de ID – em vez disso, ele chama `acquireTokenSilent` e/ou `acquireTokenRedirect` para adquirir um *token de acesso* usado para consultar a API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="cf49e-113">The SPA generated by this guide does not make use directly of the ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` to acquire an *access token* used to query the Microsoft Graph API.</span></span> <span data-ttu-id="cf49e-114">Se você precisar de um exemplo que valida o token de ID, dê uma olhada [neste](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") aplicativo de exemplo no GitHub – o exemplo usa uma API Web ASP.NET para validação de token.</span><span class="sxs-lookup"><span data-stu-id="cf49e-114">If you need a sample that validates the ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – the sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="cf49e-115">Obtendo um token de usuário interativamente</span><span class="sxs-lookup"><span data-stu-id="cf49e-115">Getting a user token interactively</span></span>

<span data-ttu-id="cf49e-116">Depois da entrada inicial, você não deseja solicitar aos usuários que autentiquem novamente sempre que precisam solicitar um token para acessar um recurso – portanto, *acquireTokenSilent* deve ser usado na maioria das vezes para adquirir tokens.</span><span class="sxs-lookup"><span data-stu-id="cf49e-116">After the initial sign-in, you do not want the ask users to reauthenticate every time they need to request a token to access a resource – so *acquireTokenSilent* should be used most of the time to acquire tokens.</span></span> <span data-ttu-id="cf49e-117">No entanto, há situações em que é necessário forçar os usuários a interagir com o ponto de extremidade do Azure Active Directory v2 – alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="cf49e-117">There are situations however that you need to force users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="cf49e-118">Os usuários precisam reinserir as credenciais deles, pois a senha expirou</span><span class="sxs-lookup"><span data-stu-id="cf49e-118">Users may need to reenter their credentials because the password has expired</span></span>
-   <span data-ttu-id="cf49e-119">Seu aplicativo está solicitando acesso a um recurso com o qual o usuário precisa concordar</span><span class="sxs-lookup"><span data-stu-id="cf49e-119">Your application is requesting access to a resource that the user needs to consent to</span></span>
-   <span data-ttu-id="cf49e-120">A autenticação de dois fatores é necessária</span><span class="sxs-lookup"><span data-stu-id="cf49e-120">Two factor authentication is required</span></span>

<span data-ttu-id="cf49e-121">Chamar o *acquireTokenRedirect(scope)* resulta no redirecionamento dos usuários para o ponto de extremidade do Azure Active Directory v2 (ou *acquireTokenPopup(scope)* resulta em uma janela pop-up) em que os usuários precisam interagir confirmando as credenciais deles ou dando consentimento para o recurso necessário, ou ainda concluindo a autenticação de dois fatores.</span><span class="sxs-lookup"><span data-stu-id="cf49e-121">Calling the *acquireTokenRedirect(scope)* result in redirecting users to the Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need to interact with by either confirming their credentials, giving the consent to the required resource, or completing the two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="cf49e-122">Obtendo um token de usuário no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="cf49e-122">Getting a user token silently</span></span>
<span data-ttu-id="cf49e-123">O método ` acquireTokenSilent` manipula as aquisições e a renovação de tokens sem nenhuma interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-123">The ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="cf49e-124">Após `loginRedirect` (ou `loginPopup`) ser executado pela primeira vez, `acquireTokenSilent` é o método normalmente usado para obter tokens usados para acessar recursos protegidos nas próximas chamadas – já que as chamadas para solicitar ou renovar tokens são feitas no modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="cf49e-124">After `loginRedirect` (or `loginPopup`) is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="cf49e-125">`acquireTokenSilent` poderá falhar em alguns casos – por exemplo, se a senha do usuário tiver expirado.</span><span class="sxs-lookup"><span data-stu-id="cf49e-125">`acquireTokenSilent` may fail in some cases – for example, the user's password has expired.</span></span> <span data-ttu-id="cf49e-126">O aplicativo pode tratar essa exceção de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="cf49e-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="cf49e-127">Faça uma chamada a `acquireTokenRedirect` imediatamente, o que resultará na solicitação de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-127">Make a call to `acquireTokenRedirect` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="cf49e-128">Esse padrão é usado frequentemente em aplicativos online em que não há nenhum conteúdo não autenticado no aplicativo disponível para o usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-128">This pattern is commonly used in online applications where there is no unauthenticated content in the application available to the user.</span></span> <span data-ttu-id="cf49e-129">O exemplo gerado por essa instalação guiada usa esse padrão.</span><span class="sxs-lookup"><span data-stu-id="cf49e-129">The sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="cf49e-130">Os aplicativos também podem fazer uma indicação visual para o usuário de que uma conexão interativa é necessária e, portanto, o usuário pode escolher o momento certo para se conectar ou o aplicativo pode tentar `acquireTokenSilent` novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cf49e-130">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="cf49e-131">Isso é frequentemente usado quando o usuário consegue usar outras funcionalidades do aplicativo sem ser interrompido – por exemplo, há conteúdo não autenticado disponível no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf49e-131">This is commonly used when the user can use other functionality of the application without being disrupted - for example, there is unauthenticated content available in the application.</span></span> <span data-ttu-id="cf49e-132">Nesse caso, o usuário pode decidir quando deseja entrar para acessar o recurso protegido ou para atualizar as informações desatualizadas.</span><span class="sxs-lookup"><span data-stu-id="cf49e-132">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="cf49e-133">Chamar a API do Microsoft Graph usando o token obtido recentemente</span><span class="sxs-lookup"><span data-stu-id="cf49e-133">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="cf49e-134">Adicione o seguinte código ao seu arquivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="cf49e-134">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used to display the results
 * @param {object} showTokenElement = HTML element used to display the RAW access token
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
                        // Display response in the page
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
                        // Display response as error in the page
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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="cf49e-135">Mais informações sobre como fazer uma chamada REST em uma API protegida</span><span class="sxs-lookup"><span data-stu-id="cf49e-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="cf49e-136">Nesse aplicativo de exemplo criado por esse guia, o método `callWebApiWithToken()` é usado para fazer uma solicitação HTTP `GET` em um recurso protegido que exige um token e, em seguida, retornar o conteúdo para o chamador.</span><span class="sxs-lookup"><span data-stu-id="cf49e-136">In the sample application created by this guide, the `callWebApiWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="cf49e-137">Esse método adiciona o token adquirido no *cabeçalho de Autorização HTTP*.</span><span class="sxs-lookup"><span data-stu-id="cf49e-137">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="cf49e-138">Para o aplicativo de exemplo criado por esse guia, o recurso é o ponto de extremidade *me* da API do Microsoft Graph – que exibe as informações de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf49e-138">For the sample application created by this guide, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="cf49e-139">Adicionar um método para desconectar o usuário</span><span class="sxs-lookup"><span data-stu-id="cf49e-139">Add a method to sign out the user</span></span>

<span data-ttu-id="cf49e-140">Adicione o seguinte código ao seu arquivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="cf49e-140">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Sign-out the user
 */
function signOut() {
    userAgentApplication.logout();
}
```
