---
title: "aaaAzure AD v2 iOS guia de Introdução - uso | Microsoft Docs"
description: Como aplicativos iOS (Swift) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Use Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API

Abra `ViewController.swift` e substitua o código de saudação com:

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Mais informações
#### <a name="getting-a-user-token-interactively"></a>Obtendo um token de usuário interativamente
Olá chamada `acquireToken` método resulta em uma janela do navegador solicitando Olá toosign de usuário no. Aplicativos geralmente exigem toosign um usuário no interativamente Olá primeira vez que precisam tooaccess um recurso protegido, ou quando uma operação silenciosa tooacquire um token de falha (por exemplo, senha do usuário Olá expirado).

#### <a name="getting-a-user-token-silently"></a>Obtendo um token de usuário no modo silencioso
Olá `acquireTokenSilent` método trata aquisições de token e renovação sem qualquer interação do usuário. Depois de `acquireToken` é executado para Olá primeira vez, `acquireTokenSilent` é Olá método usado tooobtain tokens usados tooaccess recursos para as chamadas subsequentes - protegidos como chamadas toorequest ou renovar os tokens são feitas silenciosamente.

Por fim, `acquireTokenSilent` falhará – por exemplo, o usuário Olá foi desconectado ou alterou sua senha em outro dispositivo. Quando MSAL detecta que Olá problema pode ser resolvido, exigindo uma ação interativa, ele dispara um `MSALErrorCode.interactionRequired` exceção. O aplicativo pode tratar essa exceção de duas maneiras:

1.  Fazer uma chamada contra `acquireToken` imediatamente, o que resulta em solicitando Olá toosign de usuário no. Esse padrão é geralmente usado em aplicativos online onde não há nenhum conteúdo offline no aplicativo hello disponíveis para usuário hello. aplicativo de exemplo Hello gerado por esta instalação interativa usa esse padrão: você poderá ver isso no hello ação primeira vez que você executar o aplicativo hello. Porque nenhum usuário já utilizada aplicativo hello, `applicationContext.users().first` conterá um valor nulo e um ` MSALErrorCode.interactionRequired ` exceção será lançada. Olá código no exemplo hello e identificadores Olá exceção chamando `acquireToken` resultando em solicitando Olá usuário toosign no.

2.  Os aplicativos também podem fazer um usuário toohello indicação visual que uma entrada interativa é necessária para que o usuário Olá pode selecionar Olá hora certa toosign em ou aplicativo hello pode repetir `acquireTokenSilent` mais tarde. Isso geralmente é usado quando o usuário Olá pode usar outras funcionalidades de aplicativo hello sem interrupção — por exemplo, há conteúdo off-line disponível no aplicativo hello. Nesse caso, o usuário Olá pode decidir quando quiserem toosign no recurso de saudação protegido tooaccess, Olá toorefresh desatualizado informações ou seu aplicativo pode decidir tooretry `acquireTokenSilent` quando a rede é restaurada depois de ficar indisponível temporariamente.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Chamar API do Microsoft Graph hello usando Olá token obtido apenas

Adicionar Olá novo método abaixo muito`ViewController.swift`. Esse método é usado toomake um `GET` solicitação Olá Microsoft Graph API usando um *cabeçalho de autorização HTTP*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a>Fazendo uma chamada REST em uma API protegida

Este aplicativo de exemplo hello `getContentWithToken()` método é usado toomake um HTTP `GET` solicitação em um recurso protegido que requer um chamador de conteúdo toohello Olá token e retornar. Este método adiciona token Olá adquirido em Olá *cabeçalho de autorização HTTP*. Para este exemplo, o recurso de saudação é Olá Microsoft Graph API *me* ponto de extremidade – que exibe informações de perfil do usuário hello.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Configurar a saída

Adicionar Olá seguinte método muito`ViewController.swift` toosign usuário hello:

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Mais informações sobre a saída

Olá `signoutButton` método Remove o usuário de saudação do hello cache de usuário MSAL – isso efetivamente informará o usuário atual do MSAL tooforget Olá para uma solicitação futuras tooacquire um token terá êxito apenas se ele for feito toobe interativo.

Embora o aplicativo hello neste exemplo dá suporte a um único usuário, MSAL oferece suporte a cenários onde várias contas podem entrar em hello simultaneamente – um exemplo é um aplicativo de email onde um usuário tenha várias contas.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Registrar o retorno de chamada de saudação

Depois que a autenticação do usuário hello, redirecionamentos do navegador Olá Olá usuário toohello back aplicativo. Siga as etapas de saudação abaixo tooregister esse retorno de chamada:

1.  Abra `AppDelegate.swift` e importe a MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Adicionar Olá após o método tooyour <code>AppDelegate</code> toohandle retornos de chamada de classe:
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

