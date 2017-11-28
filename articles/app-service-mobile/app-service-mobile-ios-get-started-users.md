---
title: "aaaAdd autenticação no iOS com aplicativos móveis do Azure"
description: "Saiba como usuários de tooauthenticate toouse os aplicativos móveis do Azure do seu aplicativo iOS por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="ce7c3-103">Adicionar aplicativo do iOS tooyour autenticação</span><span class="sxs-lookup"><span data-stu-id="ce7c3-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="ce7c3-104">Neste tutorial, você adicionar autenticação toohello [início rápido do iOS] projeto usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="ce7c3-105">Este tutorial baseia-se a saudação [início rápido do iOS] tutorial, que deve ser concluído primeiro.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="ce7c3-106"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar saudação do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce7c3-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ce7c3-107"><a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce7c3-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="ce7c3-108">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="ce7c3-109">Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="ce7c3-110">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="ce7c3-111">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="ce7c3-112">Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="ce7c3-113">redirecionamento de saudação tooenable no lado do servidor th:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="ce7c3-114">Em Olá [portal do Azure], selecione o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ce7c3-115">Clique em Olá **autenticação / autorização** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ce7c3-116">Clique em **Active Directory do Azure** em Olá **provedores de autenticação** seção.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="ce7c3-117">Saudação de conjunto **modo de gerenciamento** muito**avançado**.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="ce7c3-118">Em Olá **permitidas URLs de redirecionamento externo**, digite `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="ce7c3-119">Olá _appname_ na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ce7c3-120">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="ce7c3-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ce7c3-121">Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="ce7c3-122">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-122">Click **OK**.</span></span>

7. <span data-ttu-id="ce7c3-123">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-123">Click **Save**.</span></span>

## <span data-ttu-id="ce7c3-124"><a name="permissions"></a>Restringir permissões tooauthenticated usuários</span><span class="sxs-lookup"><span data-stu-id="ce7c3-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="ce7c3-125">No Xcode, pressione **executar** toostart Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="ce7c3-126">Uma exceção é gerada porque o aplicativo hello tentativas tooaccess back-end como um usuário não autenticado, mas Olá *TodoItem* tabela agora requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="ce7c3-127"><a name="add-authentication"></a>Adicionar autenticação tooapp</span><span class="sxs-lookup"><span data-stu-id="ce7c3-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="ce7c3-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-128">**Objective-C**:</span></span>

1. <span data-ttu-id="ce7c3-129">No seu Mac, abra *QSTodoListViewController.m* no Xcode e adicione o seguinte método de saudação:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    <span data-ttu-id="ce7c3-130">Alterar *google* muito*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* se você não estiver usando o Google como provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ce7c3-131">Se você estiver usando o Facebook, deverá [colocar os domínios do Facebook na lista de permissões][1] do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ce7c3-132">Substituir saudação **urlScheme** com um nome exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ce7c3-133">Olá urlScheme devem ser Olá mesmo como Olá protocolo de esquema de URL que você especificou no hello **permitidas URLs de redirecionamento externo** campo Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="ce7c3-134">Olá urlScheme é usada pelo Olá autenticação retorno de chamada tooswitch tooyour back aplicativo depois que a solicitação de autenticação for concluída.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ce7c3-135">Substituir `[self refresh]` na `viewDidLoad` na *QSTodoListViewController.m* com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="ce7c3-136">Olá abra `QSAppDelegate.h` e adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="ce7c3-137">Olá abra `QSAppDelegate.m` e adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   <span data-ttu-id="ce7c3-138">Adicione este código diretamente antes da leitura de linha hello `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="ce7c3-139">Substitua o _appname_ urlScheme valor wih Olá usado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="ce7c3-140">Olá abrir `AppName-Info.plist` (substituindo AppName com o nome de saudação do aplicativo) de arquivo e, em seguida, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="ce7c3-141">Esse código deve ser colocado dentro de saudação `<dict>` elemento.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="ce7c3-142">Substituir saudação _appname_ cadeia de caracteres (dentro da matriz para **CFBundleURLSchemes**) com o nome do aplicativo hello escolhido na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="ce7c3-143">Você também pode fazer essas alterações em Olá plist editor - clique em Olá `AppName-Info.plist` em XCode tooopen Olá plist editor.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="ce7c3-144">Substituir saudação `com.microsoft.azure.zumo` de cadeia de caracteres para **CFBundleURLName** identificador de pacote com a Apple.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="ce7c3-145">Pressione *executar* toostart Olá aplicativo e, em seguida, faça logon.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="ce7c3-146">Quando você estiver conectado, você deve ser capaz de tooview lista de tarefas de saudação e faça as atualizações.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="ce7c3-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-147">**Swift**:</span></span>

1. <span data-ttu-id="ce7c3-148">No seu Mac, abra *ToDoTableViewController.swift* no Xcode e adicione o seguinte método de saudação:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    <span data-ttu-id="ce7c3-149">Alterar *google* muito*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* se você não estiver usando o Google como provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="ce7c3-150">Se você estiver usando o Facebook, deverá [colocar os domínios do Facebook na lista de permissões][1] do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="ce7c3-151">Substituir saudação **urlScheme** com um nome exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="ce7c3-152">Olá urlScheme devem ser Olá mesmo como Olá protocolo de esquema de URL que você especificou no hello **permitidas URLs de redirecionamento externo** campo Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="ce7c3-153">Olá urlScheme é usada pelo Olá autenticação retorno de chamada tooswitch tooyour back aplicativo depois que a solicitação de autenticação for concluída.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="ce7c3-154">Remover linhas de saudação `self.refreshControl?.beginRefreshing()` e `self.onRefresh(self.refreshControl)` no final do `viewDidLoad()` na *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="ce7c3-155">Adicionar uma chamada muito`loginAndGetData()` em seu lugar:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="ce7c3-156">Olá abrir `AppDelegate.swift` de arquivos e adicionar Olá toohello linha a seguir `AppDelegate` classe:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    <span data-ttu-id="ce7c3-157">Substituir saudação _appname_ urlScheme valor wih Olá usado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="ce7c3-158">Olá abrir `AppName-Info.plist` (substituindo AppName com o nome de saudação do aplicativo) de arquivo e, em seguida, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce7c3-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    <span data-ttu-id="ce7c3-159">Esse código deve ser colocado dentro de saudação `<dict>` elemento.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="ce7c3-160">Substituir saudação _appname_ cadeia de caracteres (dentro da matriz para **CFBundleURLSchemes**) com o nome do aplicativo hello escolhido na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="ce7c3-161">Você também pode fazer essas alterações em Olá plist editor - clique em Olá `AppName-Info.plist` em XCode tooopen Olá plist editor.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="ce7c3-162">Substituir saudação `com.microsoft.azure.zumo` de cadeia de caracteres para **CFBundleURLName** identificador de pacote com a Apple.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="ce7c3-163">Pressione *executar* toostart Olá aplicativo e, em seguida, faça logon.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="ce7c3-164">Quando você estiver conectado, você deve ser capaz de tooview lista de tarefas de saudação e faça as atualizações.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="ce7c3-165">A autenticação do Serviço de Aplicativo usa a comunicação interaplicativos da Apple.</span><span class="sxs-lookup"><span data-stu-id="ce7c3-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="ce7c3-166">Para obter mais detalhes sobre este assunto, consulte toohello [documentação da Apple][2]</span><span class="sxs-lookup"><span data-stu-id="ce7c3-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portal do Azure]: https://portal.azure.com

[início rápido do iOS]: app-service-mobile-ios-get-started.md

