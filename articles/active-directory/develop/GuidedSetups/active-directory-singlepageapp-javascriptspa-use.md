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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Use Olá biblioteca de autenticação da Microsoft (MSAL) Olá toosign no usuário

1.  Crie um arquivo chamado `app.js`. Se você estiver usando um projeto Visual Studio, selecione hello (pasta raiz do projeto), clique com botão direito e selecione: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Adicionar Olá tooyour de código a seguir `app.js` arquivo:

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
### <a name="more-information"></a>Mais informações

Depois que um usuário clica Olá *'Chamar Microsoft Graph API'* botão para Olá primeira vez, `callGraphApi` chamadas de método `loginRedirect` toosign usuário hello. Esse método resulta em redirecionando Olá usuário toohello *o ponto de extremidade do Active Directory do Microsoft Azure v2* tooprompt e validar as credenciais do usuário hello. Como resultado de uma bem-sucedida entrar, o usuário de saudação é redirecionado toohello back original *index* página e um token for recebida, processada por `msal.js` e informações de saudação contidas no token de saudação é armazenado em cache. Esse token é conhecido como Olá *token de ID* e contém informações básicas sobre o usuário hello, como nome de exibição do usuário hello. Se você planejar toouse todos os dados fornecidos por esse token para qualquer finalidade, você precisa toomake-se de que esse token é validado por seu tooguarantee de servidor de back-end Olá token foi emitidos tooa de usuário válido para o seu aplicativo.

Olá SPA gerado por este guia não faz uso diretamente do token de ID de hello – em vez disso, ele chama `acquireTokenSilent` e/ou `acquireTokenRedirect` tooacquire um *token de acesso* usado tooquery Olá Microsoft Graph API. Se você precisar de um exemplo que valida o token de ID hello, dê uma olhada [isso](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemplo active-directory-javascript-singlepageapp-dotnet-webapi-v2 Github") usa o aplicativo de exemplo no GitHub – exemplo hello uma API da Web do ASP.NET para validação de token.

#### <a name="getting-a-user-token-interactively"></a>Obtendo um token de usuário interativamente

Após a saudação inicial entrar, você não quiser Olá peça tooreauthenticate usuários sempre que precisarem toorequest um token tooaccess um recurso – portanto *acquireTokenSilent* devem ser usados na maioria dos tokens de tooacquire de tempo de saudação. Há situações porém que você precisa tooforce os usuários interagem com o ponto de extremidade do Active Directory do Azure v2 – alguns exemplos incluem:
-   Os usuários podem precisar tooreenter suas credenciais porque Olá senha expirou
-   Seu aplicativo está solicitando o recurso de tooa de acesso que Olá tooconsent de necessidades de usuário para
-   A autenticação de dois fatores é necessária

Olá chamada *acquireTokenRedirect(scope)* resultar em redirecionando o ponto de extremidade do usuários toohello v2 do Active Directory do Azure (ou *acquireTokenPopup(scope)* resultados em uma janela pop-up) em que os usuários precisam toointeract com confirmando a suas credenciais, dando Olá consentimento toohello necessários recursos ou autenticação de dois fatores Olá concluído.

#### <a name="getting-a-user-token-silently"></a>Obtendo um token de usuário no modo silencioso
Olá ` acquireTokenSilent` método trata aquisições de token e renovação sem qualquer interação do usuário. Depois de `loginRedirect` (ou `loginPopup`) é executado para Olá primeira vez, `acquireTokenSilent` é Olá método usado tooobtain tokens usados tooaccess recursos para as chamadas subsequentes - protegidos como chamadas toorequest ou renovar os tokens são feitas silenciosamente.
`acquireTokenSilent`pode falhar em alguns casos – por exemplo, a senha do usuário Olá expirou. O aplicativo pode tratar essa exceção de duas maneiras:

1.  Fazer uma chamada muito`acquireTokenRedirect` imediatamente, o que resulta em solicitando Olá toosign de usuário no. Esse padrão é comumente usado em aplicativos online onde não há nenhum conteúdo não autenticado no hello aplicativo toohello disponíveis do usuário. exemplo Hello gerado por esta instalação interativa usa esse padrão.

2. Os aplicativos também podem fazer um usuário toohello indicação visual que uma entrada interativa é necessária para que o usuário Olá pode selecionar Olá hora certa toosign em ou aplicativo hello pode repetir `acquireTokenSilent` mais tarde. Isso é geralmente usado quando o usuário Olá pode usar outras funcionalidades de aplicativo hello sem interrupção — por exemplo, há conteúdo não autenticado disponíveis no aplicativo hello. Nesse caso, o usuário de saudação pode decidir quando quiserem toosign no recurso de saudação protegido tooaccess ou toorefresh Olá desatualizado informações.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar API do Microsoft Graph hello usando Olá token obtido apenas

Adicionar Olá tooyour de código a seguir `app.js` arquivo:

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Mais informações sobre como fazer uma chamada REST em uma API protegida

No aplicativo de exemplo hello criado por este guia, Olá `callWebApiWithToken()` método é usado toomake um HTTP `GET` solicitação em um recurso protegido que requer um chamador de conteúdo toohello Olá token e retornar. Este método adiciona token Olá adquirido em Olá *cabeçalho de autorização HTTP*. Para o aplicativo de exemplo hello criado por este guia, o recurso de saudação é Olá Microsoft Graph API *me* ponto de extremidade – que exibe informações de perfil do usuário hello.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Adicionar um toosign método usuário Olá

Adicionar Olá tooyour de código a seguir `app.js` arquivo:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
