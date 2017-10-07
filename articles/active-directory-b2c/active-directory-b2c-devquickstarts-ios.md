---
title: Adquirindo um token usando um aplicativo iOS - Azure AD B2C | Microsoft Docs
description: "Este artigo mostra como toocreate um aplicativo iOS que usa AppAuth com identidades de usuário do Azure Active Directory B2C toomanage e autenticar usuários."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="d65ba-103">Azure AD B2C: entrar usando um aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="d65ba-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="d65ba-104">plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="d65ba-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="d65ba-105">Usar um protocolo padrão aberto oferece mais opções de desenvolvedor, ao selecionar um toointegrate de biblioteca com os nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="d65ba-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="d65ba-106">Fornecemos este passo a passo e outros como ele tooaid desenvolvedores a gravar aplicativos que se conectam a plataforma do Microsoft Identity toohello.</span><span class="sxs-lookup"><span data-stu-id="d65ba-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="d65ba-107">A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) são capazes de tooconnect toohello Microsoft Identity plataforma.</span><span class="sxs-lookup"><span data-stu-id="d65ba-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="d65ba-108">A Microsoft não fornece correções para bibliotecas de terceiros e não as analisou.</span><span class="sxs-lookup"><span data-stu-id="d65ba-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="d65ba-109">Este exemplo está usando uma biblioteca de terceiros chamada AppAuth foi testada para compatibilidade em cenários básicos com hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d65ba-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="d65ba-110">Problemas e solicitações de recursos devem ser o projeto de código-fonte aberto da biblioteca toohello direcionado.</span><span class="sxs-lookup"><span data-stu-id="d65ba-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="d65ba-111">Para obter mais informações, consulte [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="d65ba-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="d65ba-112">Se você for novo tooOAuth2 ou OpenID Connect, muito dessa configuração de exemplo pode não ter tooyou muito sentido.</span><span class="sxs-lookup"><span data-stu-id="d65ba-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="d65ba-113">Recomendamos que você examinar um breve [visão geral do protocolo de saudação já tenha sido documentadas aqui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d65ba-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="d65ba-114">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="d65ba-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="d65ba-115">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="d65ba-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d65ba-116">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="d65ba-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="d65ba-117">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="d65ba-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="d65ba-118">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="d65ba-118">Create an application</span></span>
<span data-ttu-id="d65ba-119">Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="d65ba-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="d65ba-120">o registro do aplicativo Hello fornece informações do AD do Azure que precisa toocommunicate com segurança com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d65ba-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="d65ba-121">toocreate um aplicativo móvel, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d65ba-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="d65ba-122">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="d65ba-122">Be sure to:</span></span>

* <span data-ttu-id="d65ba-123">Incluir um **Native client** no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d65ba-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="d65ba-124">Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d65ba-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="d65ba-125">Você precisará desse GUID posteriormente.</span><span class="sxs-lookup"><span data-stu-id="d65ba-125">You need this GUID later.</span></span>
* <span data-ttu-id="d65ba-126">Configure um **URI de redirecionamento** com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="d65ba-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="d65ba-127">Você precisará desse URI posteriormente.</span><span class="sxs-lookup"><span data-stu-id="d65ba-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="d65ba-128">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="d65ba-128">Create your policies</span></span>
<span data-ttu-id="d65ba-129">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d65ba-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d65ba-130">Esse aplicativo contém uma experiência de identidade: uma combinação de entrada e inscrição.</span><span class="sxs-lookup"><span data-stu-id="d65ba-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="d65ba-131">Crie essa política conforme descrito no [artigo de referência da política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="d65ba-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="d65ba-132">Ao criar política hello, certifique-se para:</span><span class="sxs-lookup"><span data-stu-id="d65ba-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="d65ba-133">Em **inscrição atributos**, selecione o atributo de saudação **nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="d65ba-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="d65ba-134">É possível selecionar outros atributos também.</span><span class="sxs-lookup"><span data-stu-id="d65ba-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="d65ba-135">Em **declarações de aplicativo**, selecione Olá declarações **nome de exibição** e **ID de objeto do usuário**.</span><span class="sxs-lookup"><span data-stu-id="d65ba-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="d65ba-136">É possível selecionar outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="d65ba-136">You can select other claims as well.</span></span>
* <span data-ttu-id="d65ba-137">Saudação de cópia **nome** de cada política depois de criá-lo.</span><span class="sxs-lookup"><span data-stu-id="d65ba-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="d65ba-138">O nome da política é prefixado com `b2c_1_` quando você salvar a política Olá.</span><span class="sxs-lookup"><span data-stu-id="d65ba-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="d65ba-139">É necessário o nome da política hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d65ba-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="d65ba-140">Depois que você criou as políticas, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d65ba-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="d65ba-141">Baixar o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="d65ba-141">Download hello sample code</span></span>
<span data-ttu-id="d65ba-142">Nós fornecemos um exemplo funcional que usa o AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d65ba-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="d65ba-143">Você pode baixar o código de saudação e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="d65ba-143">You can download hello code and run it.</span></span> <span data-ttu-id="d65ba-144">toouse seus próprios B2C do AD do Azure locatário, siga as instruções de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d65ba-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="d65ba-145">Este exemplo foi criado, seguindo as instruções do Leiame Olá Olá [iOS AppAuth projeto no GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="d65ba-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="d65ba-146">Para obter mais detalhes sobre como exemplo hello e biblioteca Olá funcionam, referência Olá AppAuth README no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d65ba-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="d65ba-147">Modificando o toouse de aplicativo do Azure AD B2C com AppAuth</span><span class="sxs-lookup"><span data-stu-id="d65ba-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="d65ba-148">O AppAuth dá suporte a iOS 7 e versões superiores.</span><span class="sxs-lookup"><span data-stu-id="d65ba-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="d65ba-149">No entanto, é necessário logons de social toosupport no Google, SFSafariViewController que requer iOS 9 ou superior.</span><span class="sxs-lookup"><span data-stu-id="d65ba-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="d65ba-150">Configuração</span><span class="sxs-lookup"><span data-stu-id="d65ba-150">Configuration</span></span>

<span data-ttu-id="d65ba-151">Você pode configurar a comunicação com o Azure AD B2C especificando o ponto de extremidade de autorização hello e URIs de ponto de extremidade token.</span><span class="sxs-lookup"><span data-stu-id="d65ba-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="d65ba-152">toogenerate esses URIs, você precisa Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d65ba-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="d65ba-153">ID do locatário (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="d65ba-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="d65ba-154">Nome da política (por exemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="d65ba-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="d65ba-155">ponto de extremidade token URI pode ser gerado, substituindo Olá Olá locatário\_ID e hello política\_nome no hello URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="d65ba-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="d65ba-156">ponto de extremidade de autorização URI pode ser gerado, substituindo Olá Olá locatário\_ID e hello política\_nome no hello URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="d65ba-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="d65ba-157">Execute seu objeto AuthorizationServiceConfiguration de saudação toocreate de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d65ba-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="d65ba-158">Autorizando</span><span class="sxs-lookup"><span data-stu-id="d65ba-158">Authorizing</span></span>

<span data-ttu-id="d65ba-159">Depois de configurar ou recuperar uma configuração de serviço de autorização, uma solicitação de autorização pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="d65ba-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="d65ba-160">Olá toocreate solicitar, você precisa Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d65ba-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="d65ba-161">ID do cliente (por exemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="d65ba-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="d65ba-162">URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="d65ba-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="d65ba-163">Os dois itens devem ter sido salvos quando você estava [registrando seu aplicativo](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="d65ba-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="d65ba-164">tooset o seu aplicativo toohandle Olá redirecionamento toohello URI com esquema personalizado Olá, é necessário tooupdate lista de saudação do 'Esquemas de URL' no seu Info. plist:</span><span class="sxs-lookup"><span data-stu-id="d65ba-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="d65ba-165">Abra Info.pList.</span><span class="sxs-lookup"><span data-stu-id="d65ba-165">Open Info.pList.</span></span>
* <span data-ttu-id="d65ba-166">Passe o mouse sobre uma linha como 'Código de tipo de sistema operacional do pacote' e clique em Olá \+ símbolo.</span><span class="sxs-lookup"><span data-stu-id="d65ba-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="d65ba-167">Renomear Olá nova linha 'URL tipos'.</span><span class="sxs-lookup"><span data-stu-id="d65ba-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="d65ba-168">Clique em Olá seta toohello esquerda da árvore de saudação tooopen 'Tipos de URL'.</span><span class="sxs-lookup"><span data-stu-id="d65ba-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="d65ba-169">Clique em Olá seta toohello esquerda da árvore de saudação tooopen 'Item 0'.</span><span class="sxs-lookup"><span data-stu-id="d65ba-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="d65ba-170">Renomeie o primeiro item sob Item too'URL 0 esquemas.</span><span class="sxs-lookup"><span data-stu-id="d65ba-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="d65ba-171">Clique em Olá seta toohello esquerda da árvore de saudação tooopen 'Esquemas de URL'.</span><span class="sxs-lookup"><span data-stu-id="d65ba-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="d65ba-172">Na coluna de 'Value' hello, há esquerda de toohello um campo em branco do 'Item 0' abaixo 'Esquemas de URL'.</span><span class="sxs-lookup"><span data-stu-id="d65ba-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="d65ba-173">Defina o esquema exclusivo do aplicativo do hello valor tooyour.</span><span class="sxs-lookup"><span data-stu-id="d65ba-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="d65ba-174">valor de saudação deve corresponder esquema Olá usada no redirectURL ao criar objeto de OIDAuthorizationRequest hello.</span><span class="sxs-lookup"><span data-stu-id="d65ba-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="d65ba-175">Em nosso exemplo, usamos o esquema de saudação 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="d65ba-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="d65ba-176">Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-iOS/) em como toocomplete Olá restante do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d65ba-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="d65ba-177">Se você precisar tooquickly começar com um aplicativo de trabalho, check-out [nosso exemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="d65ba-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="d65ba-178">Siga as etapas de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter sua configuração do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d65ba-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="d65ba-179">Estamos sempre abrir toofeedback e sugestões!</span><span class="sxs-lookup"><span data-stu-id="d65ba-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="d65ba-180">Se você tiver dificuldade com este tópico ou ter recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="d65ba-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="d65ba-181">Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="d65ba-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
