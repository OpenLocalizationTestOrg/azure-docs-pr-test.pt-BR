---
title: "Adicionar autenticação no iOS com aplicativos móveis do Azure"
description: "Aprenda a usar os aplicativos móveis do Azure para autenticar usuários de seu aplicativo iOS por meio de uma variedade de provedores de identidade, incluindo AAD, Google, Facebook, Twitter e Microsoft."
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
ms.openlocfilehash: 21a2cc6c1eaf4b34cbe8c2d7c4dbb69c8730cf32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-ios-app"></a><span data-ttu-id="b4fb0-103">Adicione autenticação ao seu aplicativo do iOS</span><span class="sxs-lookup"><span data-stu-id="b4fb0-103">Add authentication to your iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="b4fb0-104">Neste tutorial, você adicionará a autenticação ao projeto de [início rápido do iOS] usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-104">In this tutorial, you add authentication to the [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="b4fb0-105">Este tutorial baseia-se no tutorial de [início rápido do iOS] , que você deve concluir primeiro.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-105">This tutorial is based on the [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="b4fb0-106"><a name="register"></a>Registrar seu aplicativo para autenticação e configurar o Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="b4fb0-106"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="b4fb0-107"><a name="redirecturl"></a>Adicionar seu aplicativo às URLs de redirecionamento externo permitidas</span><span class="sxs-lookup"><span data-stu-id="b4fb0-107"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="b4fb0-108">A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="b4fb0-109">Isso permite que o sistema de autenticação redirecione para seu aplicativo após a conclusão do processo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-109">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span>  <span data-ttu-id="b4fb0-110">Neste tutorial, usamos sempre o esquema de URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="b4fb0-111">No entanto, você pode usar o esquema de URL que quiser.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="b4fb0-112">Ele deve ser exclusivo para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-112">It should be unique to your mobile application.</span></span>  <span data-ttu-id="b4fb0-113">Para habilitar o redirecionamento no lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-113">To enable the redirection on th server side:</span></span>

1. <span data-ttu-id="b4fb0-114">No [portal do Azure], selecione sua conta.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-114">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="b4fb0-115">Clique na opção de menu **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-115">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="b4fb0-116">Clique em **Azure Active Directory** na seção **Provedores de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-116">Click **Azure Active Directory** under the **Authentication Providers** section.</span></span>

4. <span data-ttu-id="b4fb0-117">Defina o **Modo de gerenciamento** como **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-117">Set the **Management mode** to **Advanced**.</span></span>

5. <span data-ttu-id="b4fb0-118">Em **URLs de Redirecionamento Externo Permitidas**, insira `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-118">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="b4fb0-119">O _appname_ na cadeia de caracteres é o esquema de URL para seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-119">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="b4fb0-120">Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).</span><span class="sxs-lookup"><span data-stu-id="b4fb0-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="b4fb0-121">Você deve anotar a cadeia de caracteres escolhida, já que precisará ajustar o código do aplicativo móvel com o esquema de URL em vários lugares.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-121">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

6. <span data-ttu-id="b4fb0-122">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-122">Click **OK**.</span></span>

7. <span data-ttu-id="b4fb0-123">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-123">Click **Save**.</span></span>

## <span data-ttu-id="b4fb0-124"><a name="permissions"></a>Restringir permissões a usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="b4fb0-124"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="b4fb0-125">No Xcode, pressione **Executar** para iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-125">In Xcode, press **Run** to start the app.</span></span> <span data-ttu-id="b4fb0-126">Uma exceção é criada porque o aplicativo tenta acessar o back-end como um usuário não autenticado, mas a tabela *TodoItem* agora exige autenticação.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-126">An exception is raised because the app attempts to access the backend as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="b4fb0-127"><a name="add-authentication"></a>Adicionar autenticação ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="b4fb0-127"><a name="add-authentication"></a>Add authentication to app</span></span>
<span data-ttu-id="b4fb0-128">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-128">**Objective-C**:</span></span>

1. <span data-ttu-id="b4fb0-129">Em seu Mac, abra *QSTodoListViewController.m* em Xcode e adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="b4fb0-130">Altere *google* para *microsoftaccount*, *twitter*, *facebook* ou *windowsazureactivedirectory* se não estiver usando o Google como seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-130">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="b4fb0-131">Se você estiver usando o Facebook, deverá [colocar os domínios do Facebook na lista de permissões][1] do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="b4fb0-132">Substitua o **urlScheme** por um nome exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-132">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="b4fb0-133">O urlScheme deve ser o mesmo que o protocolo de esquema de URL especificado no campo **URLs de redirecionamento externo permitidas** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-133">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="b4fb0-134">O urlScheme é usado pelo retorno de chamada de autenticação a fim de voltar para seu aplicativo depois que a solicitação de autenticação é concluída.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-134">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="b4fb0-135">Substitua `[self refresh]` em `viewDidLoad` em *QSTodoListViewController.m* pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with the following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="b4fb0-136">Abra o arquivo `QSAppDelegate.h`e adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-136">Open the `QSAppDelegate.h` file and add the following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="b4fb0-137">Abra o arquivo `QSAppDelegate.m`e adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-137">Open the `QSAppDelegate.m` file and add the following code:</span></span>

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

   <span data-ttu-id="b4fb0-138">Adicione o código diretamente antes da linha que tem `#pragma mark - Core Data stack`.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-138">Add this code directly before the line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="b4fb0-139">Substitua o _appname_ pelo valor de urlScheme que você usou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-139">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="b4fb0-140">Abra o arquivo `AppName-Info.plist` (substituindo AppName pelo nome de seu aplicativo) e adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-140">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="b4fb0-141">Esse código deve ser colocado dentro do elemento `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-141">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="b4fb0-142">Substitua a cadeia de caracteres _appname_ (dentro da matriz de **CFBundleURLSchemes**) pelo nome do aplicativo que você escolheu na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-142">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="b4fb0-143">Você também pode fazer essas alterações no editor de plist: clique no arquivo `AppName-Info.plist` no XCode para abrir o editor de plist.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-143">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="b4fb0-144">Substitua a cadeia de caracteres `com.microsoft.azure.zumo` para **CFBundleURLName** pelo identificador do pacote Apple.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-144">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="b4fb0-145">Pressione *Executar* para iniciar o aplicativo e faça logon.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-145">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="b4fb0-146">Após ter feito o logon você poderá exibir a lista de Tarefas pendentes e fazer atualizações.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-146">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="b4fb0-147">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-147">**Swift**:</span></span>

1. <span data-ttu-id="b4fb0-148">Em seu Mac, abra *ToDoTableViewController.swift* em Xcode e adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add the following method:</span></span>

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

    <span data-ttu-id="b4fb0-149">Altere *google* para *microsoftaccount*, *twitter*, *facebook* ou *windowsazureactivedirectory* se não estiver usando o Google como seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-149">Change *google* to *microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="b4fb0-150">Se você estiver usando o Facebook, deverá [colocar os domínios do Facebook na lista de permissões][1] do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="b4fb0-151">Substitua o **urlScheme** por um nome exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-151">Replace the **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="b4fb0-152">O urlScheme deve ser o mesmo que o protocolo de esquema de URL especificado no campo **URLs de redirecionamento externo permitidas** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-152">The urlScheme should be the same as the URL Scheme protocol that you specified in the **Allowed External Redirect URLs** field in the Azure portal.</span></span> <span data-ttu-id="b4fb0-153">O urlScheme é usado pelo retorno de chamada de autenticação a fim de voltar para seu aplicativo depois que a solicitação de autenticação é concluída.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-153">The urlScheme is used by the authentication callback to switch back to your application after the authentication request is complete.</span></span>

2. <span data-ttu-id="b4fb0-154">Remova as linhas `self.refreshControl?.beginRefreshing()` e `self.onRefresh(self.refreshControl)` ao final de `viewDidLoad()` em *ToDoTableViewController.swift*.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-154">Remove the lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="b4fb0-155">Adicione uma chamada para `loginAndGetData()` em seu lugar:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-155">Add a call to `loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="b4fb0-156">Abra o arquivo `AppDelegate.swift` e adicione a seguinte linha à classe `AppDelegate`:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-156">Open the `AppDelegate.swift` file and add the following line to the `AppDelegate` class:</span></span>

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

    <span data-ttu-id="b4fb0-157">Substitua o _appname_ pelo valor de urlScheme que você usou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-157">Replace the _appname_ wih the urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="b4fb0-158">Abra o arquivo `AppName-Info.plist` (substituindo AppName pelo nome de seu aplicativo) e adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="b4fb0-158">Open the `AppName-Info.plist` file (replacing AppName with the name of your app), and add the following code:</span></span>

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

    <span data-ttu-id="b4fb0-159">Esse código deve ser colocado dentro do elemento `<dict>`.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-159">This code should be placed inside the `<dict>` element.</span></span>  <span data-ttu-id="b4fb0-160">Substitua a cadeia de caracteres _appname_ (dentro da matriz de **CFBundleURLSchemes**) pelo nome do aplicativo que você escolheu na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-160">Replace the _appname_ string (within the array for **CFBundleURLSchemes**) with the app name you chose in step 1.</span></span>  <span data-ttu-id="b4fb0-161">Você também pode fazer essas alterações no editor de plist: clique no arquivo `AppName-Info.plist` no XCode para abrir o editor de plist.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-161">You can also make these changes in the plist editor - click on the `AppName-Info.plist` file in XCode to open the plist editor.</span></span>

    <span data-ttu-id="b4fb0-162">Substitua a cadeia de caracteres `com.microsoft.azure.zumo` para **CFBundleURLName** pelo identificador do pacote Apple.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-162">Replace the `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="b4fb0-163">Pressione *Executar* para iniciar o aplicativo e faça logon.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-163">Press *Run* to start the app, and then log in.</span></span> <span data-ttu-id="b4fb0-164">Após ter feito o logon você poderá exibir a lista de Tarefas pendentes e fazer atualizações.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-164">When you are logged in, you should be able to view the Todo list and make updates.</span></span>

<span data-ttu-id="b4fb0-165">A autenticação do Serviço de Aplicativo usa a comunicação interaplicativos da Apple.</span><span class="sxs-lookup"><span data-stu-id="b4fb0-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="b4fb0-166">Para obter mais detalhes sobre esse assunto, confira a [documentação da Apple][2]</span><span class="sxs-lookup"><span data-stu-id="b4fb0-166">For more details on this subject, refer to the [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
<span data-ttu-id="b4fb0-167">[portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b4fb0-167">[Azure portal]: https://portal.azure.com</span></span>

<span data-ttu-id="b4fb0-168">[início rápido do iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4fb0-168">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>

