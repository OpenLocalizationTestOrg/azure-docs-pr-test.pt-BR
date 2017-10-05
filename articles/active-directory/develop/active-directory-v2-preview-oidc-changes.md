---
title: "Alterações no ponto de extremidade do Azure AD v2.0 | Microsoft Docs"
description: "Uma descrição das alterações que estão sendo feitas nos protocolos de visualização pública do modelo de aplicativo v 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="20a1d-103">Atualizações Importantes para os Protocolos de Autenticação v 2.0</span><span class="sxs-lookup"><span data-stu-id="20a1d-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="20a1d-104">Atenção, desenvolvedores!</span><span class="sxs-lookup"><span data-stu-id="20a1d-104">Attention developers!</span></span> <span data-ttu-id="20a1d-105">Nas próximas duas semanas, realizaremos algumas atualizações em nossos protocolos de autenticação v 2.0 que podem significar alterações de interrupção em qualquer aplicativo que você tenha gravado durante o período de visualização.</span><span class="sxs-lookup"><span data-stu-id="20a1d-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="20a1d-106">A quem isso afeta?</span><span class="sxs-lookup"><span data-stu-id="20a1d-106">Who does this affect?</span></span>
<span data-ttu-id="20a1d-107">Todos os aplicativos que foram gravados para usar o ponto de extremidade de autenticação convergido v 2.0, </span><span class="sxs-lookup"><span data-stu-id="20a1d-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="20a1d-108">Mais informações sobre o ponto de extremidade v 2.0 podem ser encontradas [aqui](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20a1d-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="20a1d-109">Se você tiver criado um aplicativo usando o ponto de extremidade v 2.0 codificando diretamente para o protocolo v 2.0, usando qualquer um de nossos middlewares da Web OAuth ou OpenID Connect, ou outras bibliotecas de terceiros para realizar a autenticação, deverá estar preparado para testar seus projetos e fazer as alterações necessárias.</span><span class="sxs-lookup"><span data-stu-id="20a1d-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="20a1d-110">A quem isso não afeta?</span><span class="sxs-lookup"><span data-stu-id="20a1d-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="20a1d-111">Quaisquer aplicativos que foram gravados no ponto de extremidade de autenticação de produção do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="20a1d-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="20a1d-112">Esse protocolo é imutável e não terá qualquer alteração.</span><span class="sxs-lookup"><span data-stu-id="20a1d-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="20a1d-113">Além disso, se seu aplicativo usa **somente** a biblioteca do ADAL para realizar a autenticação, você não precisará alterar nada.</span><span class="sxs-lookup"><span data-stu-id="20a1d-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="20a1d-114">O ADAL protegeu seu aplicativo contra alterações.</span><span class="sxs-lookup"><span data-stu-id="20a1d-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="20a1d-115">Quais são as alterações?</span><span class="sxs-lookup"><span data-stu-id="20a1d-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="20a1d-116">Remover o valor x5t dos cabeçalhos JWT</span><span class="sxs-lookup"><span data-stu-id="20a1d-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="20a1d-117">O ponto de extremidade v 2.0 usa muito os tokens JWT que contêm uma seção de parâmetros do cabeçalho com metadados relevantes sobre o token.</span><span class="sxs-lookup"><span data-stu-id="20a1d-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="20a1d-118">Se você decodificasse o cabeçalho de um dos nossos JWTs atuais, encontraria algo como:</span><span class="sxs-lookup"><span data-stu-id="20a1d-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="20a1d-119">Onde as propriedades "x5t" e "kid" identificam a chave pública que deve ser usada para validar a assinatura do token, conforme recuperada no ponto de extremidade de metadados OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20a1d-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="20a1d-120">A alteração que estamos fazendo aqui é remover a propriedade "x5t".</span><span class="sxs-lookup"><span data-stu-id="20a1d-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="20a1d-121">Você pode continuar a usar os mesmos mecanismos para validar os tokens, mas deve contar somente com a propriedade "kid" para recuperar a chave pública correta, conforme especificado no protocolo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20a1d-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="20a1d-122">**Seu trabalho: Verifique se seu aplicativo não depende da existência do valor x5t.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="20a1d-123">Remover profile_info</span><span class="sxs-lookup"><span data-stu-id="20a1d-123">Removing profile_info</span></span>
<span data-ttu-id="20a1d-124">Anteriormente, o ponto de extremidade v 2.0 retornava um objeto JSON codificado na base64 nas respostas do token chamadas `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="20a1d-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="20a1d-125">Ao solicitar um token de acesso no ponto de extremidade v 2.0 enviando uma solicitação para:</span><span class="sxs-lookup"><span data-stu-id="20a1d-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="20a1d-126">A resposta pareceria com o seguinte objeto JSON:</span><span class="sxs-lookup"><span data-stu-id="20a1d-126">The response would look like the following JSON object:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="20a1d-127">O valor `profile_info` continha informações sobre o usuário que entrou no aplicativo: seu nome de exibição, primeiro nome, sobrenome, endereço de email, identificador, etc.</span><span class="sxs-lookup"><span data-stu-id="20a1d-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="20a1d-128">Basicamente, `profile_info` foi usado para o cache do token e a exibição.</span><span class="sxs-lookup"><span data-stu-id="20a1d-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="20a1d-129">Agora, estamos removendo o valor `profile_info` , mas não se preocupe, ainda fornecemos essas informações para os desenvolvedores em um local ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="20a1d-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="20a1d-130">Em vez de `profile_info`, o ponto de extremidade v 2.0 agora retornará um `id_token` em cada resposta do token:</span><span class="sxs-lookup"><span data-stu-id="20a1d-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="20a1d-131">Você pode decodificar e analisar o id_token para recuperar as mesmas informações recebidas do profile_info.</span><span class="sxs-lookup"><span data-stu-id="20a1d-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="20a1d-132">O id_token é um JSON Web Token (JWT), contendo conteúdo conforme especificado pelo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20a1d-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="20a1d-133">O código para fazer isso deve ser bastante similar. Você só precisa extrair o segmento intermediário (corpo) do id_token e decodificá-lo com base64 para acessar o objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="20a1d-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="20a1d-134">Nas próximas duas semanas, você deverá codificar seu aplicativo para recuperar as informações do usuário em `id_token` ou `profile_info`, o que estiver presente.</span><span class="sxs-lookup"><span data-stu-id="20a1d-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="20a1d-135">Dessa forma, quando a alteração for feita, seu aplicativo poderá lidar com a transição de `profile_info` para `id_token` sem interrupção.</span><span class="sxs-lookup"><span data-stu-id="20a1d-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20a1d-136">**Seu trabalho: Verifique se seu aplicativo não depende da existência do valor `profile_info`.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="20a1d-137">Remover id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="20a1d-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="20a1d-138">Semelhante ao ocorrido com `profile_info`, também estamos removendo o parâmetro `id_token_expires_in` das respostas.</span><span class="sxs-lookup"><span data-stu-id="20a1d-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="20a1d-139">Anteriormente, o ponto de extremidade v 2.0 retornaria um valor `id_token_expires_in` junto com cada resposta id_token, por exemplo, em uma resposta de autorização:</span><span class="sxs-lookup"><span data-stu-id="20a1d-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="20a1d-140">Ou em uma resposta do token:</span><span class="sxs-lookup"><span data-stu-id="20a1d-140">Or in a token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="20a1d-141">O valor `id_token_expires_in` indicaria o número de segundos que o id_token permaneceria válido.</span><span class="sxs-lookup"><span data-stu-id="20a1d-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="20a1d-142">Agora, estamos removendo o valor `id_token_expires_in` em sua totalidade.</span><span class="sxs-lookup"><span data-stu-id="20a1d-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="20a1d-143">Em vez disso, você pode usar as declarações `nbf` e `exp` padrão do OpenID Connect para examinar a validade de um id_token.</span><span class="sxs-lookup"><span data-stu-id="20a1d-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="20a1d-144">Confira a [referência do token v 2.0](active-directory-v2-tokens.md) para obter mais informações sobre essas declarações.</span><span class="sxs-lookup"><span data-stu-id="20a1d-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20a1d-145">**Seu trabalho: Verifique se seu aplicativo não depende da existência do valor `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="20a1d-146">Alterar as declarações retornadas por scope=openid</span><span class="sxs-lookup"><span data-stu-id="20a1d-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="20a1d-147">Essa alteração será a mais importante. Na verdade, isso afetará quase todos os aplicativos que usam o ponto de extremidade v 2.0.</span><span class="sxs-lookup"><span data-stu-id="20a1d-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="20a1d-148">Muitos aplicativos enviam solicitações para o ponto de extremidade v 2.0 usando o escopo de `openid`, como:</span><span class="sxs-lookup"><span data-stu-id="20a1d-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="20a1d-149">Hoje, quando o usuário concede permissão para o escopo de `openid`, seu aplicativo recebe uma grande quantidade de informações sobre o usuário do id_token resultante.</span><span class="sxs-lookup"><span data-stu-id="20a1d-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="20a1d-150">As declarações em um id_token podem incluir o nome, nome de usuário preferido, endereço de email, ID do objeto e mais.</span><span class="sxs-lookup"><span data-stu-id="20a1d-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="20a1d-151">Nesta atualização, estamos alterando as informações às quais o escopo de `openid` dá acesso ao aplicativo para ter uma melhor conformidade com a especificação do OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20a1d-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="20a1d-152">O escopo `openid` apenas permitirá que seu aplicativo conecte o usuário e receba um identificador específico do aplicativo para o usuário na declaração `sub` do id_token.</span><span class="sxs-lookup"><span data-stu-id="20a1d-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="20a1d-153">As declarações em um id_token apenas com o escopo de `openid` concedido serão destituídas de qualquer informação de identificação pessoal.</span><span class="sxs-lookup"><span data-stu-id="20a1d-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="20a1d-154">Os exemplos de declarações do id_token são:</span><span class="sxs-lookup"><span data-stu-id="20a1d-154">Example id_token claims are:</span></span>

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

<span data-ttu-id="20a1d-155">Se você quiser obter informações de identificação pessoal (PII) sobre o usuário em seu aplicativo, seu aplicativo precisará solicitar permissões adicionais do usuário.</span><span class="sxs-lookup"><span data-stu-id="20a1d-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="20a1d-156">Estamos introduzindo o suporte para dois novos escopos da especificação OpenID Connect, os escopos `email` e `profile`, que permitem que você faça isso.</span><span class="sxs-lookup"><span data-stu-id="20a1d-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="20a1d-157">O escopo `email` é muito simples — permite que seu aplicativo acesse o endereço de email principal do usuário por meio da declaração `email` no id_token.</span><span class="sxs-lookup"><span data-stu-id="20a1d-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="20a1d-158">Observe que a declaração `email` nem sempre estará presente nos id_tokens. Ela só será incluída se estiver disponível no perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="20a1d-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="20a1d-159">O escopo `profile` permite que seu aplicativo acesse todas as outras informações básicas sobre o usuário – seu nome, nome de usuário preferido, ID do objeto etc.</span><span class="sxs-lookup"><span data-stu-id="20a1d-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="20a1d-160">Isso permite que você codifique seu aplicativo com uma divulgação mínima – você pode solicitar ao usuário apenas o conjunto de informações que seu aplicativo precisa para fazer seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="20a1d-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="20a1d-161">Se você quiser continuar a obter o conjunto completo de informações do usuário que seu aplicativo recebe atualmente, deverá incluir todos os três escopos em suas solicitações de autorização:</span><span class="sxs-lookup"><span data-stu-id="20a1d-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="20a1d-162">Seu aplicativo pode começar a enviar imediatamente os escopos de `email` e `profile` e o ponto de extremidade v 2.0 aceitará esses dois escopos e começará a solicitar as permissões dos usuários conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="20a1d-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="20a1d-163">No entanto, a alteração na interpretação do escopo de `openid` não entrará em vigor por algumas semanas.</span><span class="sxs-lookup"><span data-stu-id="20a1d-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20a1d-164">**Seu trabalho: adicione os escopos `profile` e `email` se seu aplicativo requer informações sobre o usuário.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="20a1d-165">Observe que o ADAL incluirá essas duas permissões nas solicitações por padrão.</span><span class="sxs-lookup"><span data-stu-id="20a1d-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="20a1d-166">Remover o emissor da barra à direita.</span><span class="sxs-lookup"><span data-stu-id="20a1d-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="20a1d-167">Anteriormente, o valor do emissor que aparece nos tokens do ponto de extremidade v 2.0 assumiu a forma</span><span class="sxs-lookup"><span data-stu-id="20a1d-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="20a1d-168">Onde o guid era o tenantId do locatário do AD do Azure que emitiu o token.</span><span class="sxs-lookup"><span data-stu-id="20a1d-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="20a1d-169">Com essas alterações, o valor do emissor transforma-se</span><span class="sxs-lookup"><span data-stu-id="20a1d-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="20a1d-170">em ambos os tokens e no documento de descoberta do OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20a1d-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20a1d-171">**Seu trabalho: Verifique se seu aplicativo aceita o valor do emissor com e sem uma barra à direita durante a validação do emissor.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="20a1d-172">Por que alterar?</span><span class="sxs-lookup"><span data-stu-id="20a1d-172">Why change?</span></span>
<span data-ttu-id="20a1d-173">A principal motivação para introduzir essas alterações é para que seja compatível com a especificação padrão do OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20a1d-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="20a1d-174">Ao ser compatível com o OpenID Connect, esperamos minimizar as diferenças entre a integração com serviços de identidade do Microsoft e outros serviços de identidade do setor.</span><span class="sxs-lookup"><span data-stu-id="20a1d-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="20a1d-175">Queremos permitir que os desenvolvedores usem suas bibliotecas de autenticação de fonte aberta favoritas sem ter que alterar as bibliotecas para aceitarem as diferenças da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="20a1d-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="20a1d-176">O que você pode fazer?</span><span class="sxs-lookup"><span data-stu-id="20a1d-176">What can you do?</span></span>
<span data-ttu-id="20a1d-177">A partir de hoje, você pode começar a fazer todas as alterações descritas acima.</span><span class="sxs-lookup"><span data-stu-id="20a1d-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="20a1d-178">Você deve imediatamente:</span><span class="sxs-lookup"><span data-stu-id="20a1d-178">You should immediately:</span></span>

1. <span data-ttu-id="20a1d-179">**Remova qualquer dependência no parâmetro do cabeçalho `x5t`.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="20a1d-180">**Lide de modo elegante com a transição de `profile_info` para `id_token` nas respostas de tokens.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="20a1d-181">**Remova qualquer dependência do parâmetro de resposta `id_token_expires_in`.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="20a1d-182">**Adicione os escopos `profile` e `email` ao seu aplicativo se ele precisar de informações básicas do usuário.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="20a1d-183">**Aceite os valores do emissor nos tokens com e sem uma barra à direita.**</span><span class="sxs-lookup"><span data-stu-id="20a1d-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="20a1d-184">Nossa [documentação do protocolo v 2.0](active-directory-v2-protocols.md) já foi atualizada para refletir essas alterações, portanto, você pode usá-la como referência ao ajudar a atualizar seu código.</span><span class="sxs-lookup"><span data-stu-id="20a1d-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="20a1d-185">Se você tiver mais dúvidas sobre o escopo das alterações, fique à vontade para nos contactar no Twitter em @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="20a1d-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="20a1d-186">Com que frequência as alterações do protocolo ocorrerão?</span><span class="sxs-lookup"><span data-stu-id="20a1d-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="20a1d-187">Não podemos prever qualquer alteração de interrupção nos protocolos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="20a1d-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="20a1d-188">Podemos intencionalmente agrupar essas alterações em uma versão para que você não tenha que passar por esse tipo de processo de atualização novamente pouco tempo depois.</span><span class="sxs-lookup"><span data-stu-id="20a1d-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="20a1d-189">Claro, continuaremos a adicionar recursos ao serviço de autenticação v 2.0 convergido que você pode aproveitar, mas essas alterações devem ser aditivas e não interromperem o código existente.</span><span class="sxs-lookup"><span data-stu-id="20a1d-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="20a1d-190">Por fim, gostaríamos de agradecer você por experimentar as coisas durante esse período de visualização.</span><span class="sxs-lookup"><span data-stu-id="20a1d-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="20a1d-191">As informações e experiências de nossos primeiros participantes foram inestimáveis até o momento e esperamos que você continue a compartilhar suas opiniões e ideias.</span><span class="sxs-lookup"><span data-stu-id="20a1d-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="20a1d-192">Boa codificação!</span><span class="sxs-lookup"><span data-stu-id="20a1d-192">Happy coding!</span></span>

<span data-ttu-id="20a1d-193">Divisão de Identidade da Microsoft</span><span class="sxs-lookup"><span data-stu-id="20a1d-193">The Microsoft Identity Division</span></span>

