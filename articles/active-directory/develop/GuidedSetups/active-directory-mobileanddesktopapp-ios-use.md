---
title: "Introdução ao iOS no Azure AD v2 – Uso | Microsoft Docs"
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
ms.openlocfilehash: 2ac1117a31a101705539a1f75520ce8de43809a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="b1ab3-103">Usar a MSAL (Biblioteca de Autenticação da Microsoft) para obter um token para a API do Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b1ab3-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="b1ab3-104">Abra `ViewController.swift` e substitua o código por:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-104">Open `ViewController.swift` and replace the code with:</span></span>

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

     // This button will invoke the call to the Microsoft Graph API. It uses the
     // built in Swift libraries to create a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check to see if we have a current logged in user. If we don't, then we need to sign someone in.
            // We throw an interactionRequired so that we trigger the interactive signin.
            
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
            
            // interactionRequired means we need to ask the user to sign-in. This usually happens
            // when the user's Refresh Token is expired or if the user has changed their password
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
            
            // This is the catch all error.
            
            self.loggingText.text = "Unable to acquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable to create Application Context. Error: \(error)"
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
### <a name="more-information"></a><span data-ttu-id="b1ab3-105">Mais informações</span><span class="sxs-lookup"><span data-stu-id="b1ab3-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="b1ab3-106">Obtendo um token de usuário interativamente</span><span class="sxs-lookup"><span data-stu-id="b1ab3-106">Getting a user token interactively</span></span>
<span data-ttu-id="b1ab3-107">A chamada ao método `acquireToken` resulta em uma janela do navegador que solicita a entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-107">Calling the `acquireToken` method results in a browser window prompting the user to sign in.</span></span> <span data-ttu-id="b1ab3-108">Em geral, os aplicativos exigem que um usuário se conecte de forma interativa na primeira vez que precisam acessar um recurso protegido ou quando uma operação silenciosa para a aquisição de um token falha (por exemplo, a senha do usuário expirou).</span><span class="sxs-lookup"><span data-stu-id="b1ab3-108">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="b1ab3-109">Obtendo um token de usuário no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="b1ab3-109">Getting a user token silently</span></span>
<span data-ttu-id="b1ab3-110">O método `acquireTokenSilent` manipula as aquisições e a renovação de tokens sem nenhuma interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-110">The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="b1ab3-111">Após `acquireToken` ser executado pela primeira vez, `acquireTokenSilent` é o método normalmente usado para obter tokens usados para acessar recursos protegidos nas próximas chamadas – já que as chamadas para solicitar ou renovar tokens são feitas no modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-111">After `acquireToken` is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>

<span data-ttu-id="b1ab3-112">Em certas ocasiões, `acquireTokenSilent` falhará – por exemplo, o usuário saiu do serviço ou alterou sua senha em outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-112">Eventually, `acquireTokenSilent` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="b1ab3-113">Quando a MSAL detecta que o problema pode ser resolvido com a solicitação de uma ação interativa, ela dispara uma exceção `MSALErrorCode.interactionRequired`.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-113">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="b1ab3-114">O aplicativo pode tratar essa exceção de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="b1ab3-115">Faça uma chamada a `acquireToken` imediatamente, o que resultará na solicitação de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-115">Make a call against `acquireToken` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="b1ab3-116">Esse padrão geralmente é usado em aplicativos online em que não há nenhum conteúdo offline no aplicativo disponível para o usuário.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-116">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="b1ab3-117">O aplicativo de exemplo gerado por esta configuração interativa usa esse padrão: você pode vê-lo em ação na primeira vez em que executa o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-117">The sample application generated by this guided setup uses this pattern: you can see it in action the first time you execute the application.</span></span> <span data-ttu-id="b1ab3-118">Como nenhum usuário nunca usou o aplicativo, `applicationContext.users().first` conterá um valor nulo e uma exceção ` MSALErrorCode.interactionRequired ` será lançada.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-118">Because no user ever used the application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="b1ab3-119">Em seguida, o código no exemplo trata a exceção chamando `acquireToken`, o que resulta na solicitação de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-119">The code in the sample then handles the exception by calling `acquireToken` resulting in prompting the user to sign in.</span></span>

2.  <span data-ttu-id="b1ab3-120">Os aplicativos também podem fazer uma indicação visual para o usuário de que uma conexão interativa é necessária e, portanto, o usuário pode escolher o momento certo para se conectar ou o aplicativo pode tentar `acquireTokenSilent` novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-120">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="b1ab3-121">Normalmente, isso é usado quando o usuário consegue usar outras funcionalidades do aplicativo sem ser interrompido – por exemplo, há conteúdo offline disponível no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-121">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="b1ab3-122">Nesse caso, o usuário pode decidir quando deseja se conectar para acessar o recurso protegido ou atualizar as informações desatualizadas ou o aplicativo pode decidir tentar `acquireTokenSilent` novamente quando a rede é restaurada depois de ficar temporariamente indisponível.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-122">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="b1ab3-123">Chamar a API do Microsoft Graph usando o token obtido recentemente</span><span class="sxs-lookup"><span data-stu-id="b1ab3-123">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="b1ab3-124">Adicione o novo método abaixo a `ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-124">Add the new method below to `ViewController.swift`.</span></span> <span data-ttu-id="b1ab3-125">Esse método é usado para fazer uma solicitação `GET` na API do Microsoft Graph usando um *Cabeçalho de Autorização HTTP*:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-125">This method is used to make a `GET` request against the Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify the Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set the Authorization header for the request. We use Bearer tokens, so we specify Bearer + the token we got from the result
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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="b1ab3-126">Fazendo uma chamada REST em uma API protegida</span><span class="sxs-lookup"><span data-stu-id="b1ab3-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="b1ab3-127">Neste aplicativo de exemplo, o método `getContentWithToken()` é usado para fazer uma solicitação HTTP `GET` em um recurso protegido que exige um token e, em seguida, retornar o conteúdo para o chamador.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-127">In this sample application, the `getContentWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="b1ab3-128">Esse método adiciona o token adquirido no *cabeçalho de Autorização HTTP*.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-128">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="b1ab3-129">Para esta amostra, o recurso é o ponto de extremidade *me* da API do Microsoft Graph – que exibe as informações de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-129">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="b1ab3-130">Configurar a saída</span><span class="sxs-lookup"><span data-stu-id="b1ab3-130">Set up sign-out</span></span>

<span data-ttu-id="b1ab3-131">Adicione o seguinte método ao `ViewController.swift` para desconectar o usuário:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-131">Add the following method to `ViewController.swift` to sign out the user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from the cache for this application for the provided user
        // first parameter:   The user to remove from the cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="b1ab3-132">Mais informações sobre a saída</span><span class="sxs-lookup"><span data-stu-id="b1ab3-132">More info on sign-out</span></span>

<span data-ttu-id="b1ab3-133">O método `signoutButton` acima remove o usuário do cache de usuário da MSAL – efetivamente, isso informará a MSAL para esquecer o usuário atual; portanto, uma solicitação futura de aquisição de um token terá êxito apenas se for feita para ser interativa.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-133">The `signoutButton` method removes the user from the MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>

<span data-ttu-id="b1ab3-134">Embora o aplicativo nesta amostra dê suporte a um único usuário, a MSAL dá suporte a cenários em que várias contas podem estar conectadas ao mesmo tempo – um exemplo é um aplicativo de email no qual um usuário tem várias contas.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-134">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-the-callback"></a><span data-ttu-id="b1ab3-135">Registrar o retorno de chamada</span><span class="sxs-lookup"><span data-stu-id="b1ab3-135">Register the callback</span></span>

<span data-ttu-id="b1ab3-136">Depois que o usuário é autenticado, o navegador o redireciona para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1ab3-136">Once the user authenticates, the browser redirects the user back to the application.</span></span> <span data-ttu-id="b1ab3-137">Siga as etapas abaixo para registrar esse retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-137">Follow the steps below to register this callback:</span></span>

1.  <span data-ttu-id="b1ab3-138">Abra `AppDelegate.swift` e importe a MSAL:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="b1ab3-139">Adicione o seguinte método à sua classe <code>AppDelegate</code> para tratar de retornos de chamada:</span><span class="sxs-lookup"><span data-stu-id="b1ab3-139">Add the following method to your <code>AppDelegate</code> class to handle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if the URL matches the redirect URI for a pending AppAuth
// authorization request and if so, will look for the code in the response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

