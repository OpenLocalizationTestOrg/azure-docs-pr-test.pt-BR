---
title: 'Azure Active Directory B2C: Como adquirir um token usando um aplicativo do Android | Microsoft Docs'
description: "Este artigo mostra como criar um aplicativo do Android que usa AppAuth com o Azure Active Directory B2C para autenticar e gerenciar identidades de usuários."
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
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="f22f8-103">Azure AD B2C: entrar usando um aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="f22f8-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="f22f8-104">A plataforma de identidade da Microsoft usa padrões abertos, como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f22f8-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="f22f8-105">Isso permite aos desenvolvedores aproveitar qualquer biblioteca que queiram integrar aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="f22f8-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="f22f8-106">Para auxiliar os desenvolvedores que usam a nossa plataforma com outras bibliotecas, escrevemos alguns tutoriais como este para demonstrar como configurar bibliotecas de terceiros para que elas se conectem à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f22f8-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="f22f8-107">A maioria das bibliotecas que implementam [a especificação RFC6749 do OAuth2](https://tools.ietf.org/html/rfc6749) poderá conectar-se à Plataforma de Identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f22f8-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="f22f8-108">A Microsoft não fornece correções nem análises para bibliotecas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="f22f8-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="f22f8-109">Esse exemplo usa uma biblioteca de terceiros, AppAuth, que foi testada com relação à compatibilidade em cenários básicos com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f22f8-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="f22f8-110">Os problemas e solicitações de recursos devem ser direcionados ao projeto de software livre da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="f22f8-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="f22f8-111">Para saber mais, confira [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="f22f8-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="f22f8-112">Se você ainda não conhece o OAuth2 ou o OpenID Connect, grande parte desta configuração de exemplo poderá não fazer muito sentido para você.</span><span class="sxs-lookup"><span data-stu-id="f22f8-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="f22f8-113">Recomendamos que você examine uma breve [visão geral do protocolo que documentamos aqui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f22f8-114">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="f22f8-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="f22f8-115">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="f22f8-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="f22f8-116">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="f22f8-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="f22f8-117">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="f22f8-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f22f8-118">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="f22f8-118">Create an application</span></span>

<span data-ttu-id="f22f8-119">Em seguida, você precisa criar um aplicativo em seu diretório B2C.</span><span class="sxs-lookup"><span data-stu-id="f22f8-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="f22f8-120">Isso fornece ao AD do Azure as informações de que ele precisa para se comunicar de forma segura com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f22f8-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="f22f8-121">Para criar um aplicativo móvel, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f22f8-122">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="f22f8-122">Be sure to:</span></span>

* <span data-ttu-id="f22f8-123">Inclua um **cliente nativo** no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f22f8-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="f22f8-124">Copie a **ID de aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f22f8-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="f22f8-125">Você precisará dessas informações posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f22f8-125">You will need this later.</span></span>
* <span data-ttu-id="f22f8-126">Configure um **URI de redirecionamento** de cliente nativo (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="f22f8-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="f22f8-127">Você também precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f22f8-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f22f8-128">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="f22f8-128">Create your policies</span></span>

<span data-ttu-id="f22f8-129">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f22f8-130">Esse aplicativo contém uma experiência de identidade: uma combinação de entrada e inscrição.</span><span class="sxs-lookup"><span data-stu-id="f22f8-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="f22f8-131">Você deve criar esta política seguindo as instruções de [Artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="f22f8-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="f22f8-132">Ao criar a política, não se esqueça de fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f22f8-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="f22f8-133">Escolha o **Nome de exibição** e os atributos de inscrição em sua política.</span><span class="sxs-lookup"><span data-stu-id="f22f8-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="f22f8-134">Escolha as declarações de aplicativo **Nome de exibição** e **ID do Objeto** em todas as políticas.</span><span class="sxs-lookup"><span data-stu-id="f22f8-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="f22f8-135">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="f22f8-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="f22f8-136">Copie o **Nome** de cada política depois de criá-la.</span><span class="sxs-lookup"><span data-stu-id="f22f8-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="f22f8-137">Ele deve ter o prefixo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="f22f8-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="f22f8-138">Posteriormente, você precisará do nome da política.</span><span class="sxs-lookup"><span data-stu-id="f22f8-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f22f8-139">Depois de criar as políticas, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f22f8-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="f22f8-140">Baixe o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="f22f8-140">Download the sample code</span></span>

<span data-ttu-id="f22f8-141">Nós fornecemos um exemplo funcional que usa o AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="f22f8-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="f22f8-142">Você pode baixar o código e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="f22f8-142">You can download the code and run it.</span></span> <span data-ttu-id="f22f8-143">Você pode começar rapidamente com seu próprio aplicativo usando uma configuração personalizada do Azure AD B2C, para isso, basta seguir as instruções de [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f22f8-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="f22f8-144">O exemplo é uma modificação de exemplo fornecido pelo [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="f22f8-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="f22f8-145">Acesse a página para saber mais sobre o AppAuth e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="f22f8-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="f22f8-146">Modificando seu aplicativo para usar o Azure AD B2C com AppAuth</span><span class="sxs-lookup"><span data-stu-id="f22f8-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="f22f8-147">O AppAuth oferece suporte à API Android 16 (Jellybean) e versões superiores.</span><span class="sxs-lookup"><span data-stu-id="f22f8-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="f22f8-148">Recomendamos usar a API 23 ou superior.</span><span class="sxs-lookup"><span data-stu-id="f22f8-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="f22f8-149">Configuração</span><span class="sxs-lookup"><span data-stu-id="f22f8-149">Configuration</span></span>

<span data-ttu-id="f22f8-150">Você pode configurar a comunicação com o Azure AD B2C especificando o URI de descoberta, ou especificando o ponto de extremidade de autorização e os URIs de ponto de extremidade de token.</span><span class="sxs-lookup"><span data-stu-id="f22f8-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="f22f8-151">Em ambos os casos, você precisará das informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="f22f8-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="f22f8-152">ID do locatário (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="f22f8-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="f22f8-153">Nome da política (por exemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="f22f8-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="f22f8-154">Se optar por descobrir automaticamente a autorização e os URIs de ponto de extremidade de token, você terá que buscar informações do URI de descoberta.</span><span class="sxs-lookup"><span data-stu-id="f22f8-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="f22f8-155">O URI de descoberta pode ser gerado ao substituir o Tenant\_ID e o Policy\_Name na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="f22f8-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="f22f8-156">Para adquirir a autorização e os URIs de ponto de extremidade de token e criar um objeto AuthorizationServiceConfiguration, execute:</span><span class="sxs-lookup"><span data-stu-id="f22f8-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

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
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="f22f8-157">Em vez de usar a descoberta para obter a autorização e os URIs de ponto de extremidade de token, você também pode especificá-los explicitamente, substituindo o Tenant\_ID e o Policy\_Name na URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="f22f8-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="f22f8-158">Execute o seguinte código para criar o objeto AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="f22f8-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="f22f8-159">Autorizando</span><span class="sxs-lookup"><span data-stu-id="f22f8-159">Authorizing</span></span>

<span data-ttu-id="f22f8-160">Depois de configurar ou recuperar uma configuração de serviço de autorização, uma solicitação de autorização pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="f22f8-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="f22f8-161">Para criar a solicitação, você precisará das informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="f22f8-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="f22f8-162">ID do cliente (por exemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="f22f8-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="f22f8-163">URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="f22f8-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="f22f8-164">Os dois itens devem ter sido salvos quando você estava [registrando seu aplicativo](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="f22f8-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="f22f8-165">Consulte o [guia AppAuth](https://openid.github.io/AppAuth-Android/) para concluir o processo.</span><span class="sxs-lookup"><span data-stu-id="f22f8-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="f22f8-166">Se quiser trabalhar logo com o seu aplicativo, veja o [nosso exemplo](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="f22f8-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="f22f8-167">Siga as etapas em [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) para inserir sua própria configuração do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f22f8-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="f22f8-168">Estamos sempre abertos a comentários e sugestões!</span><span class="sxs-lookup"><span data-stu-id="f22f8-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="f22f8-169">Caso você tenha alguma dúvida sobre este tópico ou recomendações para melhorar o conteúdo, agradecemos seus comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="f22f8-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="f22f8-170">Para solicitações de recursos, adicione-os ao [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="f22f8-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

