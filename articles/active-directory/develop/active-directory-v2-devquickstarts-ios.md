---
title: Adicionar entrada a um aplicativo iOS usando o ponto de extremidade do Azure AD v2.0 | Microsoft Docs
description: "Como criar um aplicativo iOS que conecte usuários com a conta pessoal e as contas corporativas ou de estudante da Microsoft usando bibliotecas de terceiros."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="2c954-103">Adicionar entrada a um aplicativo iOS usando uma biblioteca de terceiros com a API do Graph usando o ponto de extremidade v2.0</span><span class="sxs-lookup"><span data-stu-id="2c954-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="2c954-104">A plataforma de identidade da Microsoft usa padrões abertos, como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2c954-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="2c954-105">Os desenvolvedores podem usar qualquer biblioteca desejada para integrar aos nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="2c954-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="2c954-106">Para ajudar os desenvolvedores a usar nossa plataforma com outras bibliotecas, escrevemos alguns guias passo a passo como este para demonstrar como configurar bibliotecas de terceiros que se conectam à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c954-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="2c954-107">A maioria das bibliotecas que implementa [a especificação RFC6749 do OAuth2](https://tools.ietf.org/html/rfc6749) pode se conectar à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c954-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="2c954-108">Com o aplicativo que esse passo a passo cria, os usuários podem entrar na respectiva organização e pesquisar outros na organização usando a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2c954-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="2c954-109">Se ainda não conhece o OAuth2 ou o OpenID Connect, grande parte desta configuração de exemplo pode não fazer muito sentido para você.</span><span class="sxs-lookup"><span data-stu-id="2c954-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="2c954-110">Recomendamos ler o artigo [Protocolos v 2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="2c954-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="2c954-111">Alguns recursos da nossa plataforma que possuem uma expressão nos padrões OAuth2 ou OpenID Connect, como o Acesso Condicional e o gerenciamento de políticas do Intune, exigem que você use nossas Bibliotecas de Identidade do Microsoft Azure de software livre.</span><span class="sxs-lookup"><span data-stu-id="2c954-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="2c954-112">O ponto de extremidade v2.0 não dá suporte a todos os cenários e recursos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c954-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="2c954-113">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="2c954-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="2c954-114">Baixar o código do GitHub</span><span class="sxs-lookup"><span data-stu-id="2c954-114">Download code from GitHub</span></span>
<span data-ttu-id="2c954-115">O código para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="2c954-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="2c954-116">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="2c954-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="2c954-117">Você também pode apenas baixar o exemplo e começar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="2c954-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="2c954-118">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="2c954-118">Register an app</span></span>
<span data-ttu-id="2c954-119">Crie um novo aplicativo no [Portal de registro de aplicativos](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga as etapas detalhadas em [Como registrar um aplicativo com o ponto de extremidade v 2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="2c954-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="2c954-120">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="2c954-120">Make sure to:</span></span>

* <span data-ttu-id="2c954-121">Copiar a **ID do Aplicativo** atribuída ao seu aplicativo, pois você precisará dela em breve.</span><span class="sxs-lookup"><span data-stu-id="2c954-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="2c954-122">Adicione a plataforma **Móvel** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c954-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="2c954-123">Copiar o **URI de redirecionamento** do portal.</span><span class="sxs-lookup"><span data-stu-id="2c954-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="2c954-124">Você deve usar o valor padrão de `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="2c954-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="2c954-125">Baixar a biblioteca de terceiros NXOAuth2 e criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="2c954-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="2c954-126">Neste passo a passo, você usará o OAuth2Client do GitHub, que é uma biblioteca do OAuth2 para Mac OS X e iOS (Cocoa e Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="2c954-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="2c954-127">Essa biblioteca baseia-se no rascunho 10 da especificação OAuth2.</span><span class="sxs-lookup"><span data-stu-id="2c954-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="2c954-128">Ela implementa o perfil de aplicativo nativo e dá suporte ao ponto de extremidade de autorização do usuário.</span><span class="sxs-lookup"><span data-stu-id="2c954-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="2c954-129">Isso é tudo de que você precisa para a integração à plataforma de identidade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c954-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="2c954-130">Adicionar a biblioteca ao seu projeto usando o CocoaPods</span><span class="sxs-lookup"><span data-stu-id="2c954-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="2c954-131">O CocoaPods é um gerenciador de dependência para projetos do Xcode.</span><span class="sxs-lookup"><span data-stu-id="2c954-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="2c954-132">Ele gerencia automaticamente as etapas de instalação anteriores.</span><span class="sxs-lookup"><span data-stu-id="2c954-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="2c954-133">Adicione o seguinte a esse podfile:</span><span class="sxs-lookup"><span data-stu-id="2c954-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="2c954-134">Carregue o podfile usando o CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="2c954-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="2c954-135">Isso criará um novo espaço de trabalho Xcode que será carregado.</span><span class="sxs-lookup"><span data-stu-id="2c954-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="2c954-136">Explorar a estrutura do projeto</span><span class="sxs-lookup"><span data-stu-id="2c954-136">Explore the structure of the project</span></span>
<span data-ttu-id="2c954-137">Temos a seguinte estrutura configurada para nosso projeto no esqueleto:</span><span class="sxs-lookup"><span data-stu-id="2c954-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="2c954-138">Um modo de exibição mestre com uma pesquisa UPN</span><span class="sxs-lookup"><span data-stu-id="2c954-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="2c954-139">Uma Exibição de Detalhes para os dados sobre o usuário selecionado</span><span class="sxs-lookup"><span data-stu-id="2c954-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="2c954-140">Um Modo de Exibição de Logon onde um usuário pode se conectar ao aplicativo para consultar o gráfico</span><span class="sxs-lookup"><span data-stu-id="2c954-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="2c954-141">Passaremos por diversos arquivos no esqueleto para adicionar autenticação.</span><span class="sxs-lookup"><span data-stu-id="2c954-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="2c954-142">Outras partes do código, como o código visual, não pertencem à identidade, mas são fornecidas para você.</span><span class="sxs-lookup"><span data-stu-id="2c954-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="2c954-143">Configurar o arquivo settings.plst na biblioteca</span><span class="sxs-lookup"><span data-stu-id="2c954-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="2c954-144">No projeto Início rápido, abra o arquivo `settings.plist` .</span><span class="sxs-lookup"><span data-stu-id="2c954-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="2c954-145">Substitua os valores dos elementos na seção para refletir os valores que você usou no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c954-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="2c954-146">Seu código fará referência a esses valores sempre que ele usar a Biblioteca de Autenticação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c954-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="2c954-147">O `clientId` é a ID do cliente do seu aplicativo que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="2c954-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="2c954-148">O `redirectUri` é a URL de redirecionamento fornecida pelo portal.</span><span class="sxs-lookup"><span data-stu-id="2c954-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="2c954-149">Configurar a biblioteca NXOAuth2Client no seu LoginViewController</span><span class="sxs-lookup"><span data-stu-id="2c954-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="2c954-150">A biblioteca NXOAuth2Client requer alguns valores para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="2c954-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="2c954-151">Depois de concluir essa tarefa, você poderá usar o token obtido para chamar a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2c954-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="2c954-152">Como `LoginView` será chamado sempre que você precisar autenticar, faz sentido colocar os valores de configuração nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="2c954-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="2c954-153">Vamos adicionar alguns valores ao arquivo `LoginViewController.m` para definir o contexto para autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="2c954-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="2c954-154">Os detalhes sobre os valores estão abaixo do código.</span><span class="sxs-lookup"><span data-stu-id="2c954-154">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="2c954-155">Vamos examinar os detalhes do código.</span><span class="sxs-lookup"><span data-stu-id="2c954-155">Let's look at details about the code.</span></span>

<span data-ttu-id="2c954-156">A primeira cadeia de caracteres é para `scopes`.</span><span class="sxs-lookup"><span data-stu-id="2c954-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="2c954-157">O valor `User.Read` permite que você leia o perfil básico do usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="2c954-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="2c954-158">É possível saber mais sobre todos os escopos disponíveis em [Escopos de permissão do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="2c954-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="2c954-159">Para `authURL`, `loginURL`, `bhh` e `tokenURL`, você deve usar os valores fornecidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2c954-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="2c954-160">Se usar as Bibliotecas de Identidades do Microsoft Azure de software livre, obteremos esses dados para você usando nosso ponto de extremidade de metadados.</span><span class="sxs-lookup"><span data-stu-id="2c954-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="2c954-161">Fizemos o trabalho pesado de extrair esses valores para você.</span><span class="sxs-lookup"><span data-stu-id="2c954-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="2c954-162">O valor `keychain` é o contêiner que a biblioteca NXOAuth2Client usará na criação de um conjunto de chaves para armazenar seus tokens.</span><span class="sxs-lookup"><span data-stu-id="2c954-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="2c954-163">Se quiser obter SSO (logon único) entre vários aplicativos, você poderá especificar o mesmo conjunto de chaves em cada um dos aplicativos, bem como solicitar o uso desse conjunto de chaves em seus direitos de XCode.</span><span class="sxs-lookup"><span data-stu-id="2c954-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="2c954-164">Isso é explicado na documentação da Apple.</span><span class="sxs-lookup"><span data-stu-id="2c954-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="2c954-165">O restante desses valores é necessário para usar a biblioteca e criar locais para transmitir valores ao contexto.</span><span class="sxs-lookup"><span data-stu-id="2c954-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="2c954-166">Criar um cache de URL</span><span class="sxs-lookup"><span data-stu-id="2c954-166">Create a URL cache</span></span>
<span data-ttu-id="2c954-167">Dentro de `(void)viewDidLoad()`, que sempre é chamado depois que o modo de exibição é carregado, o código a seguir inicia um cache para nosso uso.</span><span class="sxs-lookup"><span data-stu-id="2c954-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="2c954-168">Adicione os códigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c954-168">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="2c954-169">Criar um Modo de Exibição da Web para conexão</span><span class="sxs-lookup"><span data-stu-id="2c954-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="2c954-170">Um Modo de Exibição da Web pode solicitar ao usuário fatores adicionais, como mensagem de texto SMS (se configurada), ou retornar mensagens de erro ao usuário.</span><span class="sxs-lookup"><span data-stu-id="2c954-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="2c954-171">Aqui, vamos configurar o Modo de Exibição da Web e, posteriormente, escreveremos o código para manipular os retornos de chamada que ocorrerão no Modo de Exibição da Web dos serviços de identidade.</span><span class="sxs-lookup"><span data-stu-id="2c954-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="2c954-172">Substituir os métodos do Modo de Exibição da Web para manipular a autenticação</span><span class="sxs-lookup"><span data-stu-id="2c954-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="2c954-173">Para informar ao Modo de Exibição da Web o que acontecerá quando um usuário precisa se conectar, conforme discutido anteriormente, você pode colar o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c954-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="2c954-174">Escrever código para manipular o resultado da solicitação de OAuth2</span><span class="sxs-lookup"><span data-stu-id="2c954-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="2c954-175">O código a seguir vai manipular a URL de redirecionamento que retorna do Modo de Exibição da Web.</span><span class="sxs-lookup"><span data-stu-id="2c954-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="2c954-176">Se a autenticação não foi bem-sucedida, o código tentará novamente.</span><span class="sxs-lookup"><span data-stu-id="2c954-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="2c954-177">Enquanto isso, a biblioteca fornecerá o erro que você pode ver no console ou manipular de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="2c954-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="2c954-178">Configurar o contexto de OAuth (chamado repositório de conta)</span><span class="sxs-lookup"><span data-stu-id="2c954-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="2c954-179">Aqui, você pode chamar `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` no repositório de conta compartilhado para cada serviço que deseja que o aplicativo possa acessar.</span><span class="sxs-lookup"><span data-stu-id="2c954-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="2c954-180">O tipo de conta é uma cadeia de caracteres usada como um identificador para um determinado serviço.</span><span class="sxs-lookup"><span data-stu-id="2c954-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="2c954-181">Como você está acessando a API do Graph, o código se refere a ele como `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="2c954-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="2c954-182">Em seguida, configure um observador que informará quando algo mudar no token.</span><span class="sxs-lookup"><span data-stu-id="2c954-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="2c954-183">Assim que obtiver o token, você retornará o usuário de volta para `masterView`.</span><span class="sxs-lookup"><span data-stu-id="2c954-183">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="2c954-184">Configurar o Modo de Exibição Mestre para pesquisar e exibir os usuários da API do Graph</span><span class="sxs-lookup"><span data-stu-id="2c954-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="2c954-185">Um aplicativo MVC (Master-View-Controller) que exibe os dados retornados na grade está além do escopo deste passo a passo, e muitos tutoriais online explicam como criar um.</span><span class="sxs-lookup"><span data-stu-id="2c954-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="2c954-186">Todo esse código está no arquivo de esqueleto.</span><span class="sxs-lookup"><span data-stu-id="2c954-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="2c954-187">No entanto, você precisa realizar algumas tarefas nesse aplicativo MVC:</span><span class="sxs-lookup"><span data-stu-id="2c954-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="2c954-188">Interceptar quando um usuário digitar algo no campo de pesquisa</span><span class="sxs-lookup"><span data-stu-id="2c954-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="2c954-189">Fornecer um objeto de dados de volta para o MasterView para poder exibir os resultados na grade</span><span class="sxs-lookup"><span data-stu-id="2c954-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="2c954-190">Faremos isso a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c954-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="2c954-191">Adicionar uma verificação para ver se você se conectou</span><span class="sxs-lookup"><span data-stu-id="2c954-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="2c954-192">O aplicativo fará muito pouco se o usuário não estiver conectado. Portanto, é uma boa ideia verificar se já há um token no cache.</span><span class="sxs-lookup"><span data-stu-id="2c954-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="2c954-193">Caso contrário, redirecione para o Modo de Exibição de Logon para que o usuário se conecte.</span><span class="sxs-lookup"><span data-stu-id="2c954-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="2c954-194">Como você sabe, a melhor maneira de realizar ações quando um modo de exibição é carregado é usar o método `viewDidLoad()` fornecido pela Apple.</span><span class="sxs-lookup"><span data-stu-id="2c954-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="2c954-195">Atualizar o Modo de Exibição de Tabela após o recebimento de dados</span><span class="sxs-lookup"><span data-stu-id="2c954-195">Update the Table View when data is received</span></span>
<span data-ttu-id="2c954-196">Quando a API do Graph retorna dados, você precisa exibi-los.</span><span class="sxs-lookup"><span data-stu-id="2c954-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="2c954-197">Para simplificar, aqui está todo o código para atualizar a tabela.</span><span class="sxs-lookup"><span data-stu-id="2c954-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="2c954-198">Você pode simplesmente colar os valores corretos em seu código de texto clichê do MVC.</span><span class="sxs-lookup"><span data-stu-id="2c954-198">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="2c954-199">Fornecer uma maneira de chamar a API do Graph quando alguém digitar no campo de pesquisa</span><span class="sxs-lookup"><span data-stu-id="2c954-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="2c954-200">Quando um usuário digita uma pesquisa na caixa, é preciso transmitir isso para a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2c954-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="2c954-201">A classe `GraphAPICaller` , que você criará no código a seguir, separa a funcionalidade de pesquisa da apresentação.</span><span class="sxs-lookup"><span data-stu-id="2c954-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="2c954-202">Por enquanto, vamos escrever o código que alimenta todos os caracteres de pesquisa na API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2c954-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="2c954-203">Fazemos isso fornecendo um método chamado `lookupInGraph`, que usa a cadeia de caracteres que queremos pesquisar.</span><span class="sxs-lookup"><span data-stu-id="2c954-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="2c954-204">Escrever uma classe auxiliar para acessar a API do Graph</span><span class="sxs-lookup"><span data-stu-id="2c954-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="2c954-205">Essa é a parte principal do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c954-205">This is the core of our application.</span></span> <span data-ttu-id="2c954-206">Enquanto o restante estava inserindo código no padrão MVC da Apple, aqui vamos escrever código para consultar o gráfico conforme o usuário digita e retornar os dados.</span><span class="sxs-lookup"><span data-stu-id="2c954-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="2c954-207">O código está abaixo e uma explicação detalhada vem a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c954-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="2c954-208">Criar um novo arquivo de cabeçalho em Objective-C</span><span class="sxs-lookup"><span data-stu-id="2c954-208">Create a new Objective C header file</span></span>
<span data-ttu-id="2c954-209">Nomeie o arquivo `GraphAPICaller.h`e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c954-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="2c954-210">Aqui, você vê que um método especificado usa uma cadeia de caracteres e retorna um completionBlock.</span><span class="sxs-lookup"><span data-stu-id="2c954-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="2c954-211">Este completionBlock, como você já deve ter adivinhado, atualizará a tabela ao fornecer um objeto com os dados populados em tempo real à medida que o usuário pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2c954-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="2c954-212">Criar um novo arquivo Objective-C</span><span class="sxs-lookup"><span data-stu-id="2c954-212">Create a new Objective C file</span></span>
<span data-ttu-id="2c954-213">Nomeie o arquivo `GraphAPICaller.m`e adicione o método a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c954-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="2c954-214">Vamos analisar esse método em detalhes.</span><span class="sxs-lookup"><span data-stu-id="2c954-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="2c954-215">A parte principal desse código está no método `NXOAuth2Request`, que usa os parâmetros que você já definiu no arquivo settings.plist.</span><span class="sxs-lookup"><span data-stu-id="2c954-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="2c954-216">A primeira etapa é construir a chamada correta à da API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2c954-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="2c954-217">Uma vez que você está chamando `/users`, especifique isso acrescentando-o ao recurso da API do Graph com a versão.</span><span class="sxs-lookup"><span data-stu-id="2c954-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="2c954-218">Faz sentido colocar tudo em um arquivo de configurações externas, pois eles podem mudar conforme a API evolui.</span><span class="sxs-lookup"><span data-stu-id="2c954-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="2c954-219">Em seguida, é preciso especificar parâmetros que você também fornecerá à chamada da API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2c954-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="2c954-220">É *muito importante* que você não coloque os parâmetros no ponto de extremidade do recurso, já que ele é removido de todos os caracteres fora de conformidade com o URI no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="2c954-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="2c954-221">Todo o código de consulta deve ser fornecido nos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="2c954-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="2c954-222">Observe que isso chama um método `convertParamsToDictionary` que você ainda não escreveu.</span><span class="sxs-lookup"><span data-stu-id="2c954-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="2c954-223">Vamos fazer isso agora no final do arquivo:</span><span class="sxs-lookup"><span data-stu-id="2c954-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="2c954-224">Em seguida, vamos usar o método `NXOAuth2Request` para obtermos dados da API no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2c954-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="2c954-225">Por fim, veremos como é possível retornar os dados para o MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="2c954-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="2c954-226">Os dados são retornados como serializados e precisam ser desserializados e carregados em um objeto que o MainViewController possa consumir.</span><span class="sxs-lookup"><span data-stu-id="2c954-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="2c954-227">Para essa finalidade, o esqueleto tem um arquivo `User.m/h` que cria um objeto User.</span><span class="sxs-lookup"><span data-stu-id="2c954-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="2c954-228">Popule esse objeto User com informações do gráfico.</span><span class="sxs-lookup"><span data-stu-id="2c954-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="2c954-229">Execute o exemplo</span><span class="sxs-lookup"><span data-stu-id="2c954-229">Run the sample</span></span>
<span data-ttu-id="2c954-230">Se você tiver usado o esqueleto ou seguido junto com o passo a passo, seu aplicativo já poderá ser executado.</span><span class="sxs-lookup"><span data-stu-id="2c954-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="2c954-231">Inicie o simulador e clique em **Entrar** para usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2c954-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="2c954-232">Obter atualizações de segurança para nosso produto</span><span class="sxs-lookup"><span data-stu-id="2c954-232">Get security updates for our product</span></span>
<span data-ttu-id="2c954-233">É recomendável obter notificações quando ocorrerem incidentes de segurança visitando a página [Segurança TechCenter](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="2c954-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

