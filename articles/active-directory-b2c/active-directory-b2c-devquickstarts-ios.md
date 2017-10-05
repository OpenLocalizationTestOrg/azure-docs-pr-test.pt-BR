---
title: Adquirindo um token usando um aplicativo iOS - Azure AD B2C | Microsoft Docs
description: "Este artigo mostra como criar um aplicativo iOS que usa AppAuth com o Azure Active Directory B2C para gerenciar identidades de usuário e autenticar usuários."
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
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="8b5f3-103">Azure AD B2C: entrar usando um aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="8b5f3-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="8b5f3-104">A plataforma de identidade da Microsoft usa padrões abertos, como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="8b5f3-105">O uso de um protocolo de padrão aberto oferece mais opções de desenvolvedor ao selecionar uma biblioteca para integrar aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="8b5f3-106">Fornecemos este passo a passo e outros como ele para ajudar os desenvolvedores a escrever aplicativos que se conectam à plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="8b5f3-107">A maioria das bibliotecas que implementam [a especificação RFC6749 do OAuth2](https://tools.ietf.org/html/rfc6749) pode conectar-se à plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="8b5f3-108">A Microsoft não fornece correções para bibliotecas de terceiros e não as analisou.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="8b5f3-109">Esse exemplo usa uma biblioteca de terceiros chamada AppAuth que foi testada com relação à compatibilidade em cenários básicos com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="8b5f3-110">Os problemas e solicitações de recursos devem ser direcionados ao projeto de software livre da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="8b5f3-111">Para obter mais informações, consulte [este artigo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="8b5f3-112">Se você ainda não conhece o OAuth2 ou o OpenID Connect, grande parte desta configuração de exemplo poderá não fazer muito sentido para você.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="8b5f3-113">Recomendamos que você examine uma breve [visão geral do protocolo que documentamos aqui](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="8b5f3-114">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="8b5f3-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="8b5f3-115">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="8b5f3-116">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="8b5f3-117">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="8b5f3-118">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="8b5f3-118">Create an application</span></span>
<span data-ttu-id="8b5f3-119">Em seguida, você precisa criar um aplicativo em seu diretório B2C.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="8b5f3-120">O registro do aplicativo dá ao Azure AD as informações de que ele precisa para se comunicar de forma segura com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="8b5f3-121">Para criar um aplicativo móvel, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="8b5f3-122">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-122">Be sure to:</span></span>

* <span data-ttu-id="8b5f3-123">Inclua um **Cliente nativo** no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="8b5f3-124">Copie a **ID de aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="8b5f3-125">Você precisará desse GUID posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-125">You need this GUID later.</span></span>
* <span data-ttu-id="8b5f3-126">Configure um **URI de redirecionamento** com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="8b5f3-127">Você precisará desse URI posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="8b5f3-128">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="8b5f3-128">Create your policies</span></span>
<span data-ttu-id="8b5f3-129">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8b5f3-130">Esse aplicativo contém uma experiência de identidade: uma combinação de entrada e inscrição.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="8b5f3-131">Crie essa política conforme descrito no [artigo de referência da política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="8b5f3-132">Ao criar a política, não se esqueça de fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="8b5f3-133">Em **Atributos de inscrição**, selecione o atributo **Nome de exibição**.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="8b5f3-134">É possível selecionar outros atributos também.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="8b5f3-135">Em **Declarações do aplicativo**, selecione as declarações **Nome de exibição** e **ID de Objeto do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="8b5f3-136">É possível selecionar outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-136">You can select other claims as well.</span></span>
* <span data-ttu-id="8b5f3-137">Copie o **Nome** de cada política depois de criá-la.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="8b5f3-138">O nome da política é prefixado com `b2c_1_` quando a política é salva.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="8b5f3-139">Posteriormente, você precisará do nome da política.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="8b5f3-140">Depois de criar as políticas, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="8b5f3-141">Baixe o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="8b5f3-141">Download the sample code</span></span>
<span data-ttu-id="8b5f3-142">Nós fornecemos um exemplo funcional que usa o AppAuth com o Azure AD B2C [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="8b5f3-143">Você pode baixar o código e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-143">You can download the code and run it.</span></span> <span data-ttu-id="8b5f3-144">Para usar seu próprio locatário Azure AD B2C, siga as instruções de [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="8b5f3-145">Este exemplo foi criado seguindo as instruções do LEIAME no [projeto AppAuth iOS no GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="8b5f3-146">Para obter mais detalhes sobre como o exemplo e a biblioteca funcionam, consulte o LEIAME do AppAuth no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="8b5f3-147">Modificando seu aplicativo para usar o Azure AD B2C com AppAuth</span><span class="sxs-lookup"><span data-stu-id="8b5f3-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="8b5f3-148">O AppAuth dá suporte a iOS 7 e versões superiores.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="8b5f3-149">No entanto, para dar suporte a logons sociais no Google, é necessário ter o SFSafariViewController, que exige iOS 9 ou versão superior.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="8b5f3-150">Configuração</span><span class="sxs-lookup"><span data-stu-id="8b5f3-150">Configuration</span></span>

<span data-ttu-id="8b5f3-151">Você pode configurar a comunicação com o Azure AD B2C especificando o ponto de extremidade de autorização e os URIs de ponto de extremidade de token.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="8b5f3-152">Para gerar esses URIs, você precisa das seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="8b5f3-153">ID do locatário (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="8b5f3-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="8b5f3-154">Nome da política (por exemplo, B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="8b5f3-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="8b5f3-155">O URI do ponto de extremidade de token pode ser gerado substituindo a ID\_do locatário e o nome\_da política na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="8b5f3-156">O URI do ponto de extremidade de autorização pode ser gerado substituindo a ID\_do locatário e o nome\_da política na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="8b5f3-157">Execute o seguinte código para criar o objeto AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="8b5f3-158">Autorizando</span><span class="sxs-lookup"><span data-stu-id="8b5f3-158">Authorizing</span></span>

<span data-ttu-id="8b5f3-159">Depois de configurar ou recuperar uma configuração de serviço de autorização, uma solicitação de autorização pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="8b5f3-160">Para criar a solicitação, você precisará das seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="8b5f3-161">ID do cliente (por exemplo, 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="8b5f3-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="8b5f3-162">URI de redirecionamento com um esquema personalizado (por exemplo, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="8b5f3-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="8b5f3-163">Os dois itens devem ter sido salvos quando você estava [registrando seu aplicativo](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="8b5f3-164">Para configurar seu aplicativo a fim de manipular o redirecionamento para o URI com o esquema personalizado, você precisará atualizar a lista de 'Esquemas de URL' em seu Info.pList:</span><span class="sxs-lookup"><span data-stu-id="8b5f3-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="8b5f3-165">Abra Info.pList.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-165">Open Info.pList.</span></span>
* <span data-ttu-id="8b5f3-166">Focalize uma linha como 'Código do tipo do Sistema Operacional do Pacote' e clique no símbolo \+.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="8b5f3-167">Renomeie a nova linha 'Tipos de URL'.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="8b5f3-168">Clique na seta à esquerda de 'Tipos de URL' para abrir a árvore.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="8b5f3-169">Clique na seta à esquerda do 'Item 0' para abrir a árvore.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="8b5f3-170">Renomeie o primeiro item sob o Item 0 como 'Esquemas de URL'.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="8b5f3-171">Clique na seta à esquerda de 'Esquemas de URL' para abrir a árvore.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="8b5f3-172">Na coluna 'Valor', há um campo em branco à esquerda do “Item 0”, abaixo de 'Esquemas de URL'.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="8b5f3-173">Defina o valor com o esquema exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="8b5f3-174">O valor deve corresponder ao esquema usado na redirectURL ao criar o objeto OIDAuthorizationRequest.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="8b5f3-175">Em nosso exemplo, usamos o esquema 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="8b5f3-176">Consulte o [guia AppAuth](https://openid.github.io/AppAuth-iOS/) para concluir o processo.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="8b5f3-177">Se quiser trabalhar logo com o seu aplicativo, veja o [nosso exemplo](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="8b5f3-178">Siga as etapas em [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) para inserir sua própria configuração do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="8b5f3-179">Estamos sempre abertos a comentários e sugestões!</span><span class="sxs-lookup"><span data-stu-id="8b5f3-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="8b5f3-180">Caso você tenha alguma dúvida sobre este tópico ou recomendações para melhorar o conteúdo, agradecemos seus comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8b5f3-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="8b5f3-181">Para solicitações de recursos, adicione-os ao [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="8b5f3-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
