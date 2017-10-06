---
title: "aaaAdd tooan entrar iOS aplicativo usando Olá o ponto de extremidade do AD do Azure v 2.0 | Microsoft Docs"
description: "Como toobuild um aplicativo iOS que entra em usuários com ambas as conta pessoal da Microsoft e contas corporativa ou escolar usando bibliotecas de terceiros."
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
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="2ceb4-103">Adicionar aplicativo do iOS tooan entrar usando uma biblioteca de terceiros com a API do Graph usando o ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="2ceb4-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="2ceb4-104">plataforma de identidade do Microsoft Hello usa padrões abertos como OAuth2 e OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="2ceb4-105">Os desenvolvedores podem usar qualquer biblioteca quiserem toointegrate com nossos serviços.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="2ceb4-106">os desenvolvedores de toohelp usar nossa plataforma com outras bibliotecas, escrevemos algumas instruções passo a passo como esse um toodemonstrate como plataforma de identidade da Microsoft tooconnect toohello tooconfigure bibliotecas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="2ceb4-107">A maioria das bibliotecas que implementam [especificação Olá RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) pode se conectar a plataforma de identidade do Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="2ceb4-108">Com o aplicativo hello que cria este passo a passo, os usuários podem entrar tootheir organização e, em seguida, procure outras pessoas em sua organização usando Olá API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="2ceb4-109">Se você for novo tooOAuth2 ou OpenID Connect, muito dessa configuração de exemplo pode não fazer sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="2ceb4-110">Recomendamos ler o artigo [Protocolos v 2.0 – Fluxo de código de autorização do OAuth 2.0](active-directory-v2-protocols-oauth-code.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="2ceb4-111">Alguns recursos de nossa plataforma que têm uma expressão em Olá OAuth2 ou padrões de OpenID Connect, como acesso condicional e gerenciamento de política do Intune, exigem você toouse nosso código-fonte aberto bibliotecas de identidade do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="2ceb4-112">o ponto de extremidade do Hello v 2.0 não oferece suporte a todos os recursos e cenários de Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="2ceb4-113">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="2ceb4-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="2ceb4-114">Baixar o código do GitHub</span><span class="sxs-lookup"><span data-stu-id="2ceb4-114">Download code from GitHub</span></span>
<span data-ttu-id="2ceb4-115">código de saudação para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="2ceb4-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="2ceb4-116">toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="2ceb4-117">Você também pode baixar o exemplo hello e começar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="2ceb4-118">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ceb4-118">Register an app</span></span>
<span data-ttu-id="2ceb4-119">Criar um novo aplicativo no hello [portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga Olá etapas detalhadas em [como tooregister um aplicativo com o ponto de extremidade do hello v 2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="2ceb4-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="2ceb4-120">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-120">Make sure to:</span></span>

* <span data-ttu-id="2ceb4-121">Saudação de cópia **Id do aplicativo** que é atribuído tooyour aplicativo porque você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="2ceb4-122">Adicionar Olá **Mobile** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="2ceb4-123">Saudação de cópia **URI de redirecionamento** do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="2ceb4-124">Você deve usar o valor padrão Olá `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="2ceb4-125">Baixar Olá terceiros NXOAuth2 biblioteca e criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="2ceb4-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="2ceb4-126">Para este passo a passo, você usará Olá OAuth2Client do GitHub, que é uma biblioteca de OAuth2 para Mac OS X e iOS (Cocoa e Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="2ceb4-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="2ceb4-127">Essa biblioteca baseia-se em 10 de rascunho da especificação de OAuth2 hello. Ele implementa um perfil de aplicativo nativo hello e dá suporte ao ponto de extremidade de autorização de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="2ceb4-128">Essas são todas as coisas Olá toointegrate com a plataforma de identidade Microsoft hello, será necessário.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="2ceb4-129">Adicionar projeto de tooyour biblioteca hello usando CocoaPods</span><span class="sxs-lookup"><span data-stu-id="2ceb4-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="2ceb4-130">O CocoaPods é um gerenciador de dependência para projetos do Xcode.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="2ceb4-131">Gerencia automaticamente as etapas de instalação anterior hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="2ceb4-132">Adicione Olá toothis podfile a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="2ceb4-133">Carregar Olá podfile usando CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="2ceb4-134">Isso criará um novo espaço de trabalho Xcode que será carregado.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="2ceb4-135">Explorar a estrutura de saudação do projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="2ceb4-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="2ceb4-136">Olá estrutura a seguir é definido para o nosso projeto de esqueleto hello:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="2ceb4-137">Um modo de exibição mestre com uma pesquisa UPN</span><span class="sxs-lookup"><span data-stu-id="2ceb4-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="2ceb4-138">Uma exibição de detalhes para dados saudação sobre o usuário selecionado Olá</span><span class="sxs-lookup"><span data-stu-id="2ceb4-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="2ceb4-139">Um modo de exibição de logon em que um usuário pode fazer logon no gráfico de saudação do toohello aplicativo tooquery</span><span class="sxs-lookup"><span data-stu-id="2ceb4-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="2ceb4-140">Podemos moverá os arquivos de toovarious na autenticação de esqueleto tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="2ceb4-141">Outras partes do código de saudação, como o código do visual hello, não relacionados tooidentity, mas são fornecidos para você.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="2ceb4-142">Configurar Olá settings.plst arquivo na biblioteca de saudação</span><span class="sxs-lookup"><span data-stu-id="2ceb4-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="2ceb4-143">No projeto de início rápido do hello, abra Olá `settings.plist` arquivo.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="2ceb4-144">Substitua valores de saudação de elementos Olá Olá seção tooreflect Olá os valores que você usou no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="2ceb4-145">Seu código fará referência a esses valores sempre que ele usa Olá biblioteca de autenticação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="2ceb4-146">Olá `clientId` é Olá ID do cliente do aplicativo que você copiou do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="2ceb4-147">Olá `redirectUri` é URL de redirecionamento Olá portal Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="2ceb4-148">Configurar Olá NXOAuth2Client biblioteca no seu LoginViewController</span><span class="sxs-lookup"><span data-stu-id="2ceb4-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="2ceb4-149">a biblioteca de NXOAuth2Client Olá requer alguns tooget valores configurado.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="2ceb4-150">Depois de concluir essa tarefa, você pode usar Olá adquiridos toocall token Olá API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="2ceb4-151">Porque `LoginView` será chamado a qualquer momento precisamos tooauthenticate, faz sentido tooput valores de configuração no arquivo toothat.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="2ceb4-152">Vamos adicionar alguns valores toohello `LoginViewController.m` contexto de saudação do arquivo tooset para autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="2ceb4-153">Detalhes sobre os valores hello execute código hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-153">Details about hello values follow hello code.</span></span>
  
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

<span data-ttu-id="2ceb4-154">Vamos examinar os detalhes sobre o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="2ceb4-155">primeira cadeia de caracteres de saudação é para `scopes`.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="2ceb4-156">Olá `User.Read` valor permite que você tooread perfil básico do hello de saudação usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="2ceb4-157">Você pode aprender mais sobre todos os escopos disponíveis de saudação em [escopos de permissão do Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="2ceb4-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="2ceb4-158">Para `authURL`, `loginURL`, `bhh`, e `tokenURL`, você deve usar valores hello fornecidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="2ceb4-159">Se você usar o software livre de saudação bibliotecas de identidade do Microsoft Azure, é suspenso esses dados para você por meio de nosso ponto de extremidade de metadados.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="2ceb4-160">Fizemos o difícil trabalho Olá de extrair esses valores para você.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="2ceb4-161">Olá `keychain` valor é o contêiner Olá Olá NXOAuth2Client biblioteca usará toocreate toostore um conjunto de chaves seus tokens.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="2ceb4-162">Se você deseja que tooget-logon único (SSO) em vários aplicativos, você pode especificar Olá mesmo conjunto de chaves em cada um dos seus aplicativos e solicitar o uso de saudação desse conjunto de chaves em seus direitos Xcode.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="2ceb4-163">Isso é explicado em Olá documentação da Apple.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="2ceb4-164">rest Olá desses valores são necessários toouse Olá biblioteca e crie locais de contexto de toohello toocarry valores.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="2ceb4-165">Criar um cache de URL</span><span class="sxs-lookup"><span data-stu-id="2ceb4-165">Create a URL cache</span></span>
<span data-ttu-id="2ceb4-166">Dentro de `(void)viewDidLoad()`, sempre que é chamado após a exibição Olá é carregada, o código a seguir hello primes um cache para o nosso uso.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="2ceb4-167">Adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-167">Add hello following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="2ceb4-168">Criar um Modo de Exibição da Web para conexão</span><span class="sxs-lookup"><span data-stu-id="2ceb4-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="2ceb4-169">Uma exibição da Web pode solicitar ao usuário Olá fatores adicionais como mensagem de texto SMS (se configurado) ou retornar o usuário de toohello de mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="2ceb4-170">Aqui você configurará Olá WebView e depois hello de gravação retornos de chamada do código toohandle Olá que ocorrerão em Olá WebView dos serviços de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="2ceb4-171">Autenticação de toohandle Olá WebView métodos de substituição</span><span class="sxs-lookup"><span data-stu-id="2ceb4-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="2ceb4-172">Olá tootell WebView o que acontece quando um usuário precisa toosign em como discutido anteriormente, você pode colar Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

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

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="2ceb4-173">Gravar código toohandle Olá resultado da solicitação de OAuth2 Olá</span><span class="sxs-lookup"><span data-stu-id="2ceb4-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="2ceb4-174">Olá código a seguir tratará redirectURL Olá que retorna da saudação WebView.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="2ceb4-175">Se a autenticação não foi bem-sucedida, o código de saudação tentará novamente.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="2ceb4-176">Enquanto isso, biblioteca Olá fornecerá erro Olá que você pode ver no console de saudação ou tratar de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="2ceb4-177">Configurar Olá contexto OAuth (chamada de repositório de conta)</span><span class="sxs-lookup"><span data-stu-id="2ceb4-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="2ceb4-178">Aqui você pode chamar `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` no repositório de conta compartilhada Olá para cada serviço que você deseja que o aplicativo de saudação toobe tooaccess capaz de.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="2ceb4-179">tipo de conta de saudação é uma cadeia de caracteres que é usada como um identificador para um determinado serviço.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="2ceb4-180">Porque você está acessando Olá API do Graph, o código de saudação refere-se tooit como `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="2ceb4-181">Depois, configure um observador que informará quando algo for alterado com o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="2ceb4-182">Depois de obter token hello, retornar Olá usuário back toohello `masterView`.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="2ceb4-183">Configurar Olá toosearch do modo de exibição mestre e exibir os usuários Olá Olá API do Graph</span><span class="sxs-lookup"><span data-stu-id="2ceb4-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="2ceb4-184">Um aplicativo Master-View-Controller (MVC) que exibe o saudação retornada dados na grade de saudação está além do escopo de saudação deste passo a passo e tutoriais online muitos explicam como toobuild um.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="2ceb4-185">Todo esse código está no arquivo esqueleto hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="2ceb4-186">No entanto, você precisa toodeal com alguns itens neste aplicativo MVC:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="2ceb4-187">Quando um usuário digita algo no campo de pesquisa de saudação de interceptação</span><span class="sxs-lookup"><span data-stu-id="2ceb4-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="2ceb4-188">Forneça um objeto de dados back toohello MasterView para que ele pode exibir resultados de saudação na grade de saudação</span><span class="sxs-lookup"><span data-stu-id="2ceb4-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="2ceb4-189">Faremos isso a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="2ceb4-190">Adicionar um toosee de seleção se você está conectado</span><span class="sxs-lookup"><span data-stu-id="2ceb4-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="2ceb4-191">aplicativo Hello faz pouco se Olá usuário não está conectado, portanto é inteligente toocheck se já houver um token no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="2ceb4-192">Se não, você pode redirecionar toohello LoginView para Olá usuário toosign no.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="2ceb4-193">Se você se lembra, Olá melhor maneira toodo ações quando uma exibição é carregado é Olá toouse `viewDidLoad()` método Apple fornece.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="2ceb4-194">Saudação de atualização quando dados são recebidos de exibição de tabela</span><span class="sxs-lookup"><span data-stu-id="2ceb4-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="2ceb4-195">Quando Olá Graph API retorna dados, você precisa toodisplay dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="2ceb4-196">Para simplificar, aqui está a todas as tabelas de Olá Olá código tooupdate.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="2ceb4-197">Apenas você pode colar valores corretos da saudação em seu código de texto clichê MVC.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

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


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="2ceb4-198">Forneça uma saudação toocall de maneira API do Graph quando alguém digita no campo de pesquisa de saudação</span><span class="sxs-lookup"><span data-stu-id="2ceb4-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="2ceb4-199">Quando um usuário digita uma pesquisa na caixa hello, você precisa tooshove que toohello API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="2ceb4-200">Olá `GraphAPICaller` classe, que você criará no hello código a seguir, separa a funcionalidade de pesquisa de saudação de apresentação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="2ceb4-201">Por enquanto, vamos escrever código Olá feeds quaisquer caracteres de pesquisa toohello API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="2ceb4-202">Podemos fazer isso ao fornecer um método chamado `lookupInGraph`, que usa a cadeia de caracteres de saudação que desejamos toosearch para.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="2ceb4-203">Gravar uma saudação de tooaccess classe auxiliar da Graph API</span><span class="sxs-lookup"><span data-stu-id="2ceb4-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="2ceb4-204">Esse é o núcleo de saudação do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-204">This is hello core of our application.</span></span> <span data-ttu-id="2ceb4-205">Enquanto o restante de saudação estava inserindo código em saudação padrão MVC padrão da Apple, aqui você escrever gráfico de saudação do código tooquery como tipos de usuário hello e, em seguida, retornar os dados.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="2ceb4-206">Aqui está o código de saudação e uma explicação detalhada segue.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="2ceb4-207">Criar um novo arquivo de cabeçalho em Objective-C</span><span class="sxs-lookup"><span data-stu-id="2ceb4-207">Create a new Objective C header file</span></span>
<span data-ttu-id="2ceb4-208">Arquivo de saudação do nome `GraphAPICaller.h`e adicione Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="2ceb4-209">Aqui, você vê que um método especificado usa uma cadeia de caracteres e retorna um completionBlock.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="2ceb4-210">Este completionBlock, como você pode esperar, atualizará Olá tabela fornecendo um objeto populados dados em tempo real conforme Olá pesquisas de usuário.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="2ceb4-211">Criar um novo arquivo Objective-C</span><span class="sxs-lookup"><span data-stu-id="2ceb4-211">Create a new Objective C file</span></span>
<span data-ttu-id="2ceb4-212">Arquivo de saudação do nome `GraphAPICaller.m`e adicione o seguinte método de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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

<span data-ttu-id="2ceb4-213">Vamos analisar esse método em detalhes.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="2ceb4-214">núcleo de saudação do código está em Olá `NXOAuth2Request`, método que usa parâmetros de saudação que já tenha definido no arquivo de settings.plist hello.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="2ceb4-215">Olá primeira etapa é chamada de API do Graph tooconstruct saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="2ceb4-216">Como você está chamando `/users`, você pode especificar que, acrescentando-o recurso da API do Graph toohello junto com a versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="2ceb4-217">Faz sentido tooput em um arquivo externo porque eles podem alterar como Olá API evolui.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="2ceb4-218">Em seguida, você precisa toospecify parâmetros também fornecerá toohello chamada de API do Graph.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="2ceb4-219">É *muito importante* que você não colocar parâmetros Olá no ponto de extremidade de recurso Olá porque que é limpo para todos os caracteres de URI não conformes em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="2ceb4-220">Todo o código de consulta deve ser fornecido em parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="2ceb4-221">Observe que isso chama um método `convertParamsToDictionary` que você ainda não escreveu.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="2ceb4-222">Vamos fazer isso agora no final de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="2ceb4-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="2ceb4-223">Em seguida, vamos usar Olá `NXOAuth2Request` dados do método tooget fazer do hello API no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="2ceb4-224">Por fim, vamos ver como você retornar Olá dados toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="2ceb4-225">dados de saudação retorna como serializada e precisa toobe desserializado e carregados em um objeto que Olá MainViewController pode consumir.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="2ceb4-226">Para essa finalidade, esqueleto Olá tem um `User.m/h` arquivo que cria um objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="2ceb4-227">Preencha esse objeto de usuário com as informações do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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


## <a name="run-hello-sample"></a><span data-ttu-id="2ceb4-228">Executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="2ceb4-228">Run hello sample</span></span>
<span data-ttu-id="2ceb4-229">Se você tiver usado esqueleto hello ou seguido junto com instruções passo a passo de saudação que seu aplicativo seja executado.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="2ceb4-230">Iniciar o simulador hello e clique em **entrar** aplicativo hello de toouse.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="2ceb4-231">Obter atualizações de segurança para nosso produto</span><span class="sxs-lookup"><span data-stu-id="2ceb4-231">Get security updates for our product</span></span>
<span data-ttu-id="2ceb4-232">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando Olá [TechCenter de segurança](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="2ceb4-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

