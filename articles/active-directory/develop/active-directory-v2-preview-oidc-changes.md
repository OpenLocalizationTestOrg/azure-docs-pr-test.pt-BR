---
title: ponto de extremidade do aaaChanges toohello AD do Azure v 2.0 | Microsoft Docs
description: "Uma descrição das alterações que estão sendo feitas protocolos de visualização pública toohello aplicativo modelo v 2.0."
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
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="81f6c-103">V 2.0 de toohello importantes atualizações protocolos de autenticação</span><span class="sxs-lookup"><span data-stu-id="81f6c-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="81f6c-104">Atenção, desenvolvedores!</span><span class="sxs-lookup"><span data-stu-id="81f6c-104">Attention developers!</span></span> <span data-ttu-id="81f6c-105">Sobre Olá próximas duas semanas, realizaremos atualizações alguns protocolos de autenticação do tooour v 2.0 que podem significar últimas alterações para todos os aplicativos que foram gravadas durante o período de nossa visualização.</span><span class="sxs-lookup"><span data-stu-id="81f6c-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="81f6c-106">A quem isso afeta?</span><span class="sxs-lookup"><span data-stu-id="81f6c-106">Who does this affect?</span></span>
<span data-ttu-id="81f6c-107">Todos os aplicativos que foram gravados v 2.0 do toouse Olá convergida ponto de extremidade de autenticação</span><span class="sxs-lookup"><span data-stu-id="81f6c-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="81f6c-108">Obter mais informações sobre o ponto de extremidade do hello v 2.0 podem ser encontradas [aqui](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81f6c-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="81f6c-109">Se você criou um aplicativo usando o ponto de extremidade do hello v 2.0 codificando diretamente toohello v 2.0 protocol usando qualquer um dos nossos middlewares web OpenID Connect ou OAuth ou usando outros 3ª parte bibliotecas tooperform a autenticação, você deve estar preparado tootest seus projetos e verifique alterações necessárias.</span><span class="sxs-lookup"><span data-stu-id="81f6c-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="81f6c-110">A quem isso não afeta?</span><span class="sxs-lookup"><span data-stu-id="81f6c-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="81f6c-111">Todos os aplicativos que foram gravados em relação a saudação produção AD do Azure do ponto de extremidade,</span><span class="sxs-lookup"><span data-stu-id="81f6c-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="81f6c-112">Esse protocolo é imutável e não terá qualquer alteração.</span><span class="sxs-lookup"><span data-stu-id="81f6c-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="81f6c-113">Além disso, se seu aplicativo **somente** usa a autenticação de tooperform nossa biblioteca ADAL, você não terá toochange nada.</span><span class="sxs-lookup"><span data-stu-id="81f6c-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="81f6c-114">ADAL tem blindado seu aplicativo de alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="81f6c-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="81f6c-115">Quais são as alterações de Olá?</span><span class="sxs-lookup"><span data-stu-id="81f6c-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="81f6c-116">Removendo o valor de x5t Olá dos cabeçalhos JWT</span><span class="sxs-lookup"><span data-stu-id="81f6c-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="81f6c-117">o ponto de extremidade do Hello v 2.0 usa tokens JWT extensivamente, que contém uma seção de parâmetros de cabeçalho com metadados relevantes sobre token de saudação.</span><span class="sxs-lookup"><span data-stu-id="81f6c-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="81f6c-118">Se decodificar o cabeçalho de saudação de um dos nossos JWTs atuais, você deve encontrar algo como:</span><span class="sxs-lookup"><span data-stu-id="81f6c-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="81f6c-119">Onde ambas as propriedades de "x5t" e "kid" hello identificam a chave pública de saudação que deve ser assinatura do token de saudação toovalidate usado, conforme recuperados do ponto de extremidade de metadados de OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="81f6c-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="81f6c-120">alteração de saudação que estamos fazendo aqui é propriedade de hello "x5t" de tooremove.</span><span class="sxs-lookup"><span data-stu-id="81f6c-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="81f6c-121">Você pode continuar toouse Olá mesmo toovalidate de mecanismos de tokens, mas deve depender somente hello "kid" propriedade tooretrieve Olá chave pública correta, como especificado em Olá protocolo OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="81f6c-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="81f6c-122">**O trabalho: Verifique se seu aplicativo não depende da existência de saudação do valor de x5t hello.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="81f6c-123">Remover profile_info</span><span class="sxs-lookup"><span data-stu-id="81f6c-123">Removing profile_info</span></span>
<span data-ttu-id="81f6c-124">Anteriormente, o ponto de extremidade do hello v 2.0 tem foi retornar um objeto JSON codificado na base64 em respostas de token chamadas `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="81f6c-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="81f6c-125">Ao solicitar um token de acesso do ponto de extremidade do hello v 2.0 enviando uma solicitação para:</span><span class="sxs-lookup"><span data-stu-id="81f6c-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="81f6c-126">resposta de saudação seria Olá objeto JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="81f6c-126">hello response would look like hello following JSON object:</span></span>

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

<span data-ttu-id="81f6c-127">Olá `profile_info` informações de valor contido sobre o usuário de saudação que assinou o aplicativo hello - seu nome de exibição, nome, sobrenome, endereço de email, identificador e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="81f6c-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="81f6c-128">Primeiramente, Olá `profile_info` foi usado para o cache de token e fins de exibição.</span><span class="sxs-lookup"><span data-stu-id="81f6c-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="81f6c-129">Agora estamos removendo Olá `profile_info` valor – mas não se preocupe, ainda estamos fornecendo essa toodevelopers informações em um local ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="81f6c-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="81f6c-130">Em vez de `profile_info`, o ponto de extremidade do hello v 2.0 agora irá retornar um `id_token` em cada resposta do token:</span><span class="sxs-lookup"><span data-stu-id="81f6c-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="81f6c-131">Você pode decodificar e analisar Olá id_token tooretrieve Olá mesmas informações que você recebeu do profile_info.</span><span class="sxs-lookup"><span data-stu-id="81f6c-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="81f6c-132">Olá id_token é um JSON Web Token (JWT), com conteúdo conforme especificado pelas OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="81f6c-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="81f6c-133">Olá código para fazer isso deve ser bem semelhante – basta intermediária de saudação tooextract segmento (corpo Olá) da saudação id_token e base64 decodificá-la tooaccess objeto JSON hello dentro.</span><span class="sxs-lookup"><span data-stu-id="81f6c-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="81f6c-134">Sobre Olá próximas duas semanas, você deve codificar as informações do usuário do aplicativo tooretrieve Olá de qualquer Olá `id_token` ou `profile_info`; o que está presente.</span><span class="sxs-lookup"><span data-stu-id="81f6c-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="81f6c-135">Dessa forma, quando Olá alteração é feita, seu aplicativo pode lidar com transição de saudação do `profile_info` muito`id_token` sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="81f6c-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81f6c-136">**O trabalho: Verifique se seu aplicativo não depende da existência de saudação do hello `profile_info` valor.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="81f6c-137">Remover id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="81f6c-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="81f6c-138">Semelhante muito`profile_info`, também estamos removendo Olá `id_token_expires_in` parâmetro de respostas.</span><span class="sxs-lookup"><span data-stu-id="81f6c-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="81f6c-139">Anteriormente, o ponto de extremidade do hello v 2.0 retornaria um valor para `id_token_expires_in` junto com cada resposta id_token, por exemplo, em uma resposta de autorização:</span><span class="sxs-lookup"><span data-stu-id="81f6c-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="81f6c-140">Ou em uma resposta do token:</span><span class="sxs-lookup"><span data-stu-id="81f6c-140">Or in a token response:</span></span>

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

<span data-ttu-id="81f6c-141">Olá `id_token_expires_in` valor indicaria Olá quantos segundos Olá id_token permanecerá válido para.</span><span class="sxs-lookup"><span data-stu-id="81f6c-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="81f6c-142">Agora, estamos removendo Olá `id_token_expires_in` valor completamente.</span><span class="sxs-lookup"><span data-stu-id="81f6c-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="81f6c-143">Em vez disso, você pode usar o padrão de OpenID Connect Olá `nbf` e `exp` tooexamine validade de saudação de um id_token de declarações.</span><span class="sxs-lookup"><span data-stu-id="81f6c-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="81f6c-144">Consulte Olá [referência de token v 2.0](active-directory-v2-tokens.md) para obter mais informações sobre essas declarações.</span><span class="sxs-lookup"><span data-stu-id="81f6c-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81f6c-145">**O trabalho: Verifique se seu aplicativo não depende da existência de saudação do hello `id_token_expires_in` valor.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="81f6c-146">Alterando declarações Olá retornadas pelo escopo = openid</span><span class="sxs-lookup"><span data-stu-id="81f6c-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="81f6c-147">Essa alteração será hello mais significativa – na verdade, isso afetará a quase todos os aplicativos que usa o ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="81f6c-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="81f6c-148">Muitos aplicativos enviar solicitações toohello v 2.0 ponto de extremidade usando Olá `openid` escopo, como:</span><span class="sxs-lookup"><span data-stu-id="81f6c-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="81f6c-149">Hoje, quando o usuário de saudação concede permissão para Olá `openid` escopo, seu aplicativo recebe uma grande quantidade de informações sobre o usuário Olá Olá resultante id_token.</span><span class="sxs-lookup"><span data-stu-id="81f6c-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="81f6c-150">As declarações em um id_token podem incluir o nome, nome de usuário preferido, endereço de email, ID do objeto e mais.</span><span class="sxs-lookup"><span data-stu-id="81f6c-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="81f6c-151">Nesta atualização, nós estamos alterando as informações de saudação que Olá `openid` escopo permite ao aplicativo acesso aos toobetter comform com hello especificação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="81f6c-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="81f6c-152">Olá `openid` escopo será somente que seu aplicativo toosign Olá usuário e recebe um identificador específico do aplicativo para o usuário Olá no hello `sub` Olá id_token de declaração.</span><span class="sxs-lookup"><span data-stu-id="81f6c-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="81f6c-153">Olá declarações em um id_token com apenas Olá `openid` escopo concedido será não possui informações pessoalmente identificáveis.</span><span class="sxs-lookup"><span data-stu-id="81f6c-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="81f6c-154">Os exemplos de declarações do id_token são:</span><span class="sxs-lookup"><span data-stu-id="81f6c-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="81f6c-155">Se você quiser tooobtain informações de identificação pessoal (PII) sobre o usuário Olá no seu aplicativo, seu aplicativo precisará de permissões adicionais de toorequest de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="81f6c-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="81f6c-156">Estamos introduzindo o suporte para dois novos escopos de especificação de OpenID Connect hello – hello `email` e `profile` escopos – que permitem toodo.</span><span class="sxs-lookup"><span data-stu-id="81f6c-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="81f6c-157">Olá `email` escopo é muito simples – ele permite que o endereço de email principal do usuário seu aplicativo acesso toohello via Olá `email` Olá id_token de declaração.</span><span class="sxs-lookup"><span data-stu-id="81f6c-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="81f6c-158">Observe que Olá `email` declaração não sempre estarão presente em id_tokens – ele só será incluído se disponíveis no perfil do usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="81f6c-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="81f6c-159">Olá `profile` escopo dá seu tooall de acesso do aplicativo outras informações básicas sobre o usuário hello – seu nome, o nome do usuário preferencial, a ID de objeto e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="81f6c-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="81f6c-160">Isso permite toocode seu aplicativo de forma mínima divulgação – você pode pedir Olá usuário apenas o conjunto de saudação de informações que seu aplicativo requer toodo seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="81f6c-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="81f6c-161">Se você quiser toocontinue obtenção Olá o conjunto completo de informações do usuário que seu aplicativo está recebendo, você deve incluir todos os três escopos em suas solicitações de autorização:</span><span class="sxs-lookup"><span data-stu-id="81f6c-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="81f6c-162">Seu aplicativo pode começar a enviar Olá `email` e `profile` escopos imediatamente e o ponto de extremidade do hello v 2.0 aceitar esses dois escopos e começar solicitando permissões de usuários, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="81f6c-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="81f6c-163">No entanto, a saudação alterar na interpretação Olá Olá `openid` escopo não entrarão em vigor para algumas semanas.</span><span class="sxs-lookup"><span data-stu-id="81f6c-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81f6c-164">**O trabalho: Adicionar Olá `profile` e `email` escopos se seu aplicativo requer informações sobre o usuário hello.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="81f6c-165">Observe que o ADAL incluirá essas duas permissões nas solicitações por padrão.</span><span class="sxs-lookup"><span data-stu-id="81f6c-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="81f6c-166">Removendo Olá emissor barra à direita.</span><span class="sxs-lookup"><span data-stu-id="81f6c-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="81f6c-167">Anteriormente, o valor de emissor Olá que aparece em tokens do ponto de extremidade do hello v 2.0 levou formulário Olá</span><span class="sxs-lookup"><span data-stu-id="81f6c-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="81f6c-168">Onde Olá guid foi tenantId de saudação do locatário de saudação do AD do Azure que emitiu o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="81f6c-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="81f6c-169">Com essas alterações, o valor de emissor Olá torna-se</span><span class="sxs-lookup"><span data-stu-id="81f6c-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="81f6c-170">em ambos os tokens em documento de descoberta de OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="81f6c-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81f6c-171">**O trabalho: Verifique se seu aplicativo aceita o valor de emissor Olá com e sem uma barra à direita durante a validação do emissor.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="81f6c-172">Por que alterar?</span><span class="sxs-lookup"><span data-stu-id="81f6c-172">Why change?</span></span>
<span data-ttu-id="81f6c-173">a principal motivação Olá para introduzir essas alterações é toobe compatível com hello especificação padrão OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="81f6c-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="81f6c-174">Ao ser OpenID Connect compatíveis, esperamos toominimize diferenças entre a integração com serviços de identidade da Microsoft e com outros serviços de identidade no setor de saudação.</span><span class="sxs-lookup"><span data-stu-id="81f6c-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="81f6c-175">Queremos tooenable desenvolvedores toouse suas bibliotecas de autenticação de software livre favorito sem a necessidade de diferenças de Microsoft tooalter Olá bibliotecas tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="81f6c-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="81f6c-176">O que você pode fazer?</span><span class="sxs-lookup"><span data-stu-id="81f6c-176">What can you do?</span></span>
<span data-ttu-id="81f6c-177">A partir de hoje, você pode começar a fazer todas as alterações de saudação descritas acima.</span><span class="sxs-lookup"><span data-stu-id="81f6c-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="81f6c-178">Você deve imediatamente:</span><span class="sxs-lookup"><span data-stu-id="81f6c-178">You should immediately:</span></span>

1. <span data-ttu-id="81f6c-179">**Remova qualquer dependência no hello `x5t` parâmetro de cabeçalho.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="81f6c-180">**Tratar normalmente a transição de saudação do `profile_info` muito`id_token` em respostas de token.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="81f6c-181">**Remova qualquer dependência no hello `id_token_expires_in` parâmetro de resposta.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="81f6c-182">**Adicionar Olá `profile` e `email` escopos tooyour aplicativo se seu aplicativo precisa de informações de usuário básica.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="81f6c-183">**Aceite os valores do emissor nos tokens com e sem uma barra à direita.**</span><span class="sxs-lookup"><span data-stu-id="81f6c-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="81f6c-184">Nosso [v 2.0 documentação do protocolo](active-directory-v2-protocols.md) já foi atualizado tooreflect essas alterações, portanto você pode usá-lo como referência ajudar a atualizar seu código.</span><span class="sxs-lookup"><span data-stu-id="81f6c-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="81f6c-185">Se você tiver outras perguntas no escopo de saudação das alterações de hello, sinta-se livre tooreach out toous no Twitter em @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="81f6c-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="81f6c-186">Com que frequência as alterações do protocolo ocorrerão?</span><span class="sxs-lookup"><span data-stu-id="81f6c-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="81f6c-187">Não podemos prever qualquer mais recentes alterações toohello protocolos de autenticação.</span><span class="sxs-lookup"><span data-stu-id="81f6c-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="81f6c-188">Podemos intencionalmente agrupará essas alterações em uma versão para que você não terá toogo por meio desse tipo de processo de atualização novamente a qualquer momento em breve.</span><span class="sxs-lookup"><span data-stu-id="81f6c-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="81f6c-189">Obviamente, vamos continuar tooadd recursos toohello convergido v 2.0 serviço de autenticação que você pode tirar proveito do, mas essas alterações devem ser aditivo e não quebra código existente.</span><span class="sxs-lookup"><span data-stu-id="81f6c-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="81f6c-190">Por fim, esperamos que toosay Obrigado por experimentar as coisas durante o período de visualização hello.</span><span class="sxs-lookup"><span data-stu-id="81f6c-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="81f6c-191">insights Hello e experiências de nossos usuários iniciais foram inestimáveis até o momento e esperamos que você continue tooshare suas opiniões e ideias.</span><span class="sxs-lookup"><span data-stu-id="81f6c-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="81f6c-192">Boa codificação!</span><span class="sxs-lookup"><span data-stu-id="81f6c-192">Happy coding!</span></span>

<span data-ttu-id="81f6c-193">Olá divisão de identidade da Microsoft</span><span class="sxs-lookup"><span data-stu-id="81f6c-193">hello Microsoft Identity Division</span></span>

