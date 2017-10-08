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
# <a name="add-authentication-tooyour-ios-app"></a>Adicionar aplicativo do iOS tooyour autenticação
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Neste tutorial, você adicionar autenticação toohello [início rápido do iOS] projeto usando um provedor de identidade com suporte. Este tutorial baseia-se a saudação [início rápido do iOS] tutorial, que deve ser concluído primeiro.

## <a name="register"></a>Registrar seu aplicativo para autenticação e configurar saudação do serviço de aplicativo
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Adicionar URLs de redirecionamento externo permitidos de toohello seu aplicativo

A autenticação segura exige que você defina um novo esquema de URL para seu aplicativo.  Isso permite Olá autenticação sistema tooredirect tooyour back aplicativo após a conclusão do processo de autenticação de saudação.  Neste tutorial, usamos sempre o esquema de URL _appname_.  No entanto, você pode usar o esquema de URL que quiser.  Ele deve ser exclusivo tooyour aplicativo para dispositivos móveis.  redirecionamento de saudação tooenable no lado do servidor th:

1. Em Olá [portal do Azure], selecione o serviço de aplicativo.

2. Clique em Olá **autenticação / autorização** opção de menu.

3. Clique em **Active Directory do Azure** em Olá **provedores de autenticação** seção.

4. Saudação de conjunto **modo de gerenciamento** muito**avançado**.

5. Em Olá **permitidas URLs de redirecionamento externo**, digite `appname://easyauth.callback`.  Olá _appname_ na cadeia de caracteres é hello esquema de URL para seu aplicativo móvel.  Ele deve seguir as especificações de URL normal para um protocolo (use somente letras e números e inicie com uma letra).  Assegure uma anotação de cadeia de caracteres de saudação que você escolha como você precisará tooadjust seu código de aplicativo móvel com hello esquema de URL em vários locais.

6. Clique em **OK**.

7. Clique em **Salvar**.

## <a name="permissions"></a>Restringir permissões tooauthenticated usuários
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

No Xcode, pressione **executar** toostart Olá aplicativo. Uma exceção é gerada porque o aplicativo hello tentativas tooaccess back-end como um usuário não autenticado, mas Olá *TodoItem* tabela agora requer autenticação.

## <a name="add-authentication"></a>Adicionar autenticação tooapp
**Objective-C**:

1. No seu Mac, abra *QSTodoListViewController.m* no Xcode e adicione o seguinte método de saudação:

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

    Alterar *google* muito*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* se você não estiver usando o Google como provedor de identidade. Se você estiver usando o Facebook, deverá [colocar os domínios do Facebook na lista de permissões][1] do aplicativo.

    Substituir saudação **urlScheme** com um nome exclusivo para seu aplicativo.  Olá urlScheme devem ser Olá mesmo como Olá protocolo de esquema de URL que você especificou no hello **permitidas URLs de redirecionamento externo** campo Olá portal do Azure. Olá urlScheme é usada pelo Olá autenticação retorno de chamada tooswitch tooyour back aplicativo depois que a solicitação de autenticação for concluída.

2. Substituir `[self refresh]` na `viewDidLoad` na *QSTodoListViewController.m* com hello código a seguir:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Olá abra `QSAppDelegate.h` e adicione Olá código a seguir:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Olá abra `QSAppDelegate.m` e adicione Olá código a seguir:

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

   Adicione este código diretamente antes da leitura de linha hello `#pragma mark - Core Data stack`.  Substitua o _appname_ urlScheme valor wih Olá usado na etapa 1.

5. Olá abrir `AppName-Info.plist` (substituindo AppName com o nome de saudação do aplicativo) de arquivo e, em seguida, adicione Olá código a seguir:

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

    Esse código deve ser colocado dentro de saudação `<dict>` elemento.  Substituir saudação _appname_ cadeia de caracteres (dentro da matriz para **CFBundleURLSchemes**) com o nome do aplicativo hello escolhido na etapa 1.  Você também pode fazer essas alterações em Olá plist editor - clique em Olá `AppName-Info.plist` em XCode tooopen Olá plist editor.

    Substituir saudação `com.microsoft.azure.zumo` de cadeia de caracteres para **CFBundleURLName** identificador de pacote com a Apple.

6. Pressione *executar* toostart Olá aplicativo e, em seguida, faça logon. Quando você estiver conectado, você deve ser capaz de tooview lista de tarefas de saudação e faça as atualizações.

**Swift**:

1. No seu Mac, abra *ToDoTableViewController.swift* no Xcode e adicione o seguinte método de saudação:

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

    Alterar *google* muito*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* se você não estiver usando o Google como provedor de identidade. Se você estiver usando o Facebook, deverá [colocar os domínios do Facebook na lista de permissões][1] do aplicativo.

    Substituir saudação **urlScheme** com um nome exclusivo para seu aplicativo.  Olá urlScheme devem ser Olá mesmo como Olá protocolo de esquema de URL que você especificou no hello **permitidas URLs de redirecionamento externo** campo Olá portal do Azure. Olá urlScheme é usada pelo Olá autenticação retorno de chamada tooswitch tooyour back aplicativo depois que a solicitação de autenticação for concluída.

2. Remover linhas de saudação `self.refreshControl?.beginRefreshing()` e `self.onRefresh(self.refreshControl)` no final do `viewDidLoad()` na *ToDoTableViewController.swift*. Adicionar uma chamada muito`loginAndGetData()` em seu lugar:

    ```swift
    loginAndGetData()
    ```

3. Olá abrir `AppDelegate.swift` de arquivos e adicionar Olá toohello linha a seguir `AppDelegate` classe:

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

    Substituir saudação _appname_ urlScheme valor wih Olá usado na etapa 1.

4. Olá abrir `AppName-Info.plist` (substituindo AppName com o nome de saudação do aplicativo) de arquivo e, em seguida, adicione Olá código a seguir:

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

    Esse código deve ser colocado dentro de saudação `<dict>` elemento.  Substituir saudação _appname_ cadeia de caracteres (dentro da matriz para **CFBundleURLSchemes**) com o nome do aplicativo hello escolhido na etapa 1.  Você também pode fazer essas alterações em Olá plist editor - clique em Olá `AppName-Info.plist` em XCode tooopen Olá plist editor.

    Substituir saudação `com.microsoft.azure.zumo` de cadeia de caracteres para **CFBundleURLName** identificador de pacote com a Apple.

5. Pressione *executar* toostart Olá aplicativo e, em seguida, faça logon. Quando você estiver conectado, você deve ser capaz de tooview lista de tarefas de saudação e faça as atualizações.

A autenticação do Serviço de Aplicativo usa a comunicação interaplicativos da Apple.  Para obter mais detalhes sobre este assunto, consulte toohello [documentação da Apple][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portal do Azure]: https://portal.azure.com

[início rápido do iOS]: app-service-mobile-ios-get-started.md

