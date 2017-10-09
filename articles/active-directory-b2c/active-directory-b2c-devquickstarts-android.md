---
title: 'Azure Active Directory B2C: Como adquirir um token usando um aplicativo do Android | Microsoft Docs'
description: "Este artigo mostra como toocreate um aplicativo do Android que usa AppAuth com identidades de usuário do Azure Active Directory B2C toomanage e autenticar usuários."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="3ead4-103">Azure AD B2C: entrar usando um aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="3ead4-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="3ead4-104">plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="3ead4-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="3ead4-105">Isso permite que desenvolvedores tooleverage qualquer biblioteca desejarem toointegrate com nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="3ead4-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="3ead4-106">os desenvolvedores de tooaid usando nossa plataforma com outras bibliotecas, escrevemos algumas instruções passo a passo como esse um toodemonstrate como tooconfigure 3ª parte bibliotecas tooconnect toohello Microsoft plataforma de identidade.</span><span class="sxs-lookup"><span data-stu-id="3ead4-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="3ead4-107">A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) será capaz de tooconnect toohello Microsoft Identity plataforma.</span><span class="sxs-lookup"><span data-stu-id="3ead4-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="3ead4-108">A Microsoft não fornece correções nem análises para bibliotecas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="3ead4-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="3ead4-109">Este exemplo está usando uma biblioteca de terceiros 3º chamada AppAuth foi testada para compatibilidade em cenários básicos com hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="3ead4-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="3ead4-110">Problemas e solicitações de recursos devem ser o projeto de código-fonte aberto da biblioteca toohello direcionado.</span><span class="sxs-lookup"><span data-stu-id="3ead4-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="3ead4-111">Para saber mais, confira [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="3ead4-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="3ead4-112">Se você for novo tooOAuth2 ou OpenID Connect muito nesta configuração de exemplo pode não ter tooyou muito sentido.</span><span class="sxs-lookup"><span data-stu-id="3ead4-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="3ead4-113">Recomendamos que você examinar um breve [visão geral do protocolo de saudação já tenha sido documentadas aqui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3ead4-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="3ead4-114">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="3ead4-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="3ead4-115">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="3ead4-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="3ead4-116">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="3ead4-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="3ead4-117">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="3ead4-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="3ead4-118">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="3ead4-118">Create an application</span></span>

<span data-ttu-id="3ead4-119">Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="3ead4-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="3ead4-120">Isso fornece informações do AD do Azure que precisa toocommunicate com segurança com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ead4-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="3ead4-121">toocreate um aplicativo móvel, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3ead4-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="3ead4-122">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="3ead4-122">Be sure to:</span></span>

* <span data-ttu-id="3ead4-123">Incluir um **Native Client** no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3ead4-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="3ead4-124">Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ead4-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="3ead4-125">Você precisará dessas informações posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3ead4-125">You will need this later.</span></span>
* <span data-ttu-id="3ead4-126">Configure um **URI de redirecionamento** de cliente nativo (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="3ead4-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="3ead4-127">Você também precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3ead4-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="3ead4-128">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="3ead4-128">Create your policies</span></span>

<span data-ttu-id="3ead4-129">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3ead4-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="3ead4-130">Esse aplicativo contém uma experiência de identidade: uma combinação de entrada e inscrição.</span><span class="sxs-lookup"><span data-stu-id="3ead4-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="3ead4-131">Você precisa toocreate essa política, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="3ead4-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="3ead4-132">Ao criar política hello, certifique-se para:</span><span class="sxs-lookup"><span data-stu-id="3ead4-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="3ead4-133">Escolha Olá **nome de exibição** como um atributo de inscrição em sua política.</span><span class="sxs-lookup"><span data-stu-id="3ead4-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="3ead4-134">Escolha Olá **nome de exibição** e **ID de objeto** declarações de aplicativo em cada política.</span><span class="sxs-lookup"><span data-stu-id="3ead4-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="3ead4-135">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="3ead4-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="3ead4-136">Saudação de cópia **nome** de cada política depois de criá-lo.</span><span class="sxs-lookup"><span data-stu-id="3ead4-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="3ead4-137">Ele deve ter o prefixo Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="3ead4-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="3ead4-138">Você precisará nome da política hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3ead4-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="3ead4-139">Depois que você criou as políticas, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ead4-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="3ead4-140">Baixar o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="3ead4-140">Download hello sample code</span></span>

<span data-ttu-id="3ead4-141">Nós fornecemos um exemplo funcional que usa o AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="3ead4-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="3ead4-142">Você pode baixar o código de saudação e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="3ead4-142">You can download hello code and run it.</span></span> <span data-ttu-id="3ead4-143">Você pode começar rapidamente com seu próprio aplicativo usando sua própria configuração do Azure AD B2C seguindo instruções Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="3ead4-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="3ead4-144">exemplo Hello é uma modificação do exemplo hello fornecido pelo [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="3ead4-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="3ead4-145">Visite sua toolearn página mais sobre AppAuth e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="3ead4-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="3ead4-146">Modificando o toouse de aplicativo do Azure AD B2C com AppAuth</span><span class="sxs-lookup"><span data-stu-id="3ead4-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="3ead4-147">O AppAuth oferece suporte à API Android 16 (Jellybean) e versões superiores.</span><span class="sxs-lookup"><span data-stu-id="3ead4-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="3ead4-148">Recomendamos usar a API 23 ou superior.</span><span class="sxs-lookup"><span data-stu-id="3ead4-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="3ead4-149">Configuração</span><span class="sxs-lookup"><span data-stu-id="3ead4-149">Configuration</span></span>

<span data-ttu-id="3ead4-150">Você pode configurar a comunicação com o Azure AD B2C descobrir Olá especificando URI ou especificando o ponto de extremidade de autorização hello e URIs de ponto de extremidade token.</span><span class="sxs-lookup"><span data-stu-id="3ead4-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="3ead4-151">Em ambos os casos, você precisará Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ead4-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="3ead4-152">ID do locatário (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="3ead4-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="3ead4-153">Nome da política (por exemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="3ead4-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="3ead4-154">Se você escolher tooautomatically descobrir Olá autorização e token de ponto de extremidade URIs, você precisará toofetch informações de descoberta de saudação URI.</span><span class="sxs-lookup"><span data-stu-id="3ead4-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="3ead4-155">descoberta de saudação URI pode ser gerado, substituindo Olá locatário\_ID e hello política\_nome no hello URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ead4-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="3ead4-156">Você pode adquirir autorização hello e URIs de ponto de extremidade token e criar um objeto AuthorizationServiceConfiguration executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="3ead4-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="3ead4-157">Em vez de usar autorização de saudação do tooobtain de descoberta e o ponto de extremidade token URIs, você também pode especificá-los explicitamente, substituindo Olá locatário\_ID e hello política\_nome na URL de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="3ead4-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="3ead4-158">Execute seu objeto AuthorizationServiceConfiguration de saudação toocreate de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ead4-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="3ead4-159">Autorizando</span><span class="sxs-lookup"><span data-stu-id="3ead4-159">Authorizing</span></span>

<span data-ttu-id="3ead4-160">Depois de configurar ou recuperar uma configuração de serviço de autorização, uma solicitação de autorização pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="3ead4-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="3ead4-161">Olá toocreate solicitar, você precisará Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ead4-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="3ead4-162">ID do cliente (por exemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="3ead4-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="3ead4-163">URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="3ead4-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="3ead4-164">Os dois itens devem ter sido salvos quando você estava [registrando seu aplicativo](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="3ead4-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="3ead4-165">Consulte toohello [AppAuth guia](https://openid.github.io/AppAuth-Android/) em como toocomplete Olá restante do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ead4-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="3ead4-166">Se você precisar tooquickly começar com um aplicativo de trabalho, check-out [nosso exemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="3ead4-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="3ead4-167">Siga as etapas de Olá Olá [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter sua configuração do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="3ead4-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="3ead4-168">Estamos sempre abrir toofeedback e sugestões!</span><span class="sxs-lookup"><span data-stu-id="3ead4-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="3ead4-169">Se você tiver dificuldade com este tópico ou ter recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ead4-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="3ead4-170">Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="3ead4-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

