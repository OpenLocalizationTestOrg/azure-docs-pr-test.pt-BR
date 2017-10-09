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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="5595e-103">Use Olá biblioteca de autenticação da Microsoft (MSAL) tooget um token para Olá Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="5595e-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="5595e-104">Abra `ViewController.swift` e substitua o código de saudação com:</span><span class="sxs-lookup"><span data-stu-id="5595e-104">Open `ViewController.swift` and replace hello code with:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="5595e-105">Mais informações</span><span class="sxs-lookup"><span data-stu-id="5595e-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="5595e-106">Obtendo um token de usuário interativamente</span><span class="sxs-lookup"><span data-stu-id="5595e-106">Getting a user token interactively</span></span>
<span data-ttu-id="5595e-107">Olá chamada `acquireToken` método resulta em uma janela do navegador solicitando Olá toosign de usuário no.</span><span class="sxs-lookup"><span data-stu-id="5595e-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="5595e-108">Aplicativos geralmente exigem toosign um usuário no interativamente Olá primeira vez que precisam tooaccess um recurso protegido, ou quando uma operação silenciosa tooacquire um token de falha (por exemplo, senha do usuário Olá expirado).</span><span class="sxs-lookup"><span data-stu-id="5595e-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="5595e-109">Obtendo um token de usuário no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="5595e-109">Getting a user token silently</span></span>
<span data-ttu-id="5595e-110">Olá `acquireTokenSilent` método trata aquisições de token e renovação sem qualquer interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5595e-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="5595e-111">Depois de `acquireToken` é executado para Olá primeira vez, `acquireTokenSilent` é Olá método usado tooobtain tokens usados tooaccess recursos para as chamadas subsequentes - protegidos como chamadas toorequest ou renovar os tokens são feitas silenciosamente.</span><span class="sxs-lookup"><span data-stu-id="5595e-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="5595e-112">Por fim, `acquireTokenSilent` falhará – por exemplo, o usuário Olá foi desconectado ou alterou sua senha em outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5595e-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="5595e-113">Quando MSAL detecta que Olá problema pode ser resolvido, exigindo uma ação interativa, ele dispara um `MSALErrorCode.interactionRequired` exceção.</span><span class="sxs-lookup"><span data-stu-id="5595e-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="5595e-114">O aplicativo pode tratar essa exceção de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="5595e-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="5595e-115">Fazer uma chamada contra `acquireToken` imediatamente, o que resulta em solicitando Olá toosign de usuário no.</span><span class="sxs-lookup"><span data-stu-id="5595e-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="5595e-116">Esse padrão é geralmente usado em aplicativos online onde não há nenhum conteúdo offline no aplicativo hello disponíveis para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5595e-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="5595e-117">aplicativo de exemplo Hello gerado por esta instalação interativa usa esse padrão: você poderá ver isso no hello ação primeira vez que você executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5595e-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="5595e-118">Porque nenhum usuário já utilizada aplicativo hello, `applicationContext.users().first` conterá um valor nulo e um ` MSALErrorCode.interactionRequired ` exceção será lançada.</span><span class="sxs-lookup"><span data-stu-id="5595e-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="5595e-119">Olá código no exemplo hello e identificadores Olá exceção chamando `acquireToken` resultando em solicitando Olá usuário toosign no.</span><span class="sxs-lookup"><span data-stu-id="5595e-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="5595e-120">Os aplicativos também podem fazer um usuário toohello indicação visual que uma entrada interativa é necessária para que o usuário Olá pode selecionar Olá hora certa toosign em ou aplicativo hello pode repetir `acquireTokenSilent` mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5595e-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="5595e-121">Isso geralmente é usado quando o usuário Olá pode usar outras funcionalidades de aplicativo hello sem interrupção — por exemplo, há conteúdo off-line disponível no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5595e-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="5595e-122">Nesse caso, o usuário Olá pode decidir quando quiserem toosign no recurso de saudação protegido tooaccess, Olá toorefresh desatualizado informações ou seu aplicativo pode decidir tooretry `acquireTokenSilent` quando a rede é restaurada depois de ficar indisponível temporariamente.</span><span class="sxs-lookup"><span data-stu-id="5595e-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="5595e-123">Chamar API do Microsoft Graph hello usando Olá token obtido apenas</span><span class="sxs-lookup"><span data-stu-id="5595e-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="5595e-124">Adicionar Olá novo método abaixo muito`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="5595e-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="5595e-125">Esse método é usado toomake um `GET` solicitação Olá Microsoft Graph API usando um *cabeçalho de autorização HTTP*:</span><span class="sxs-lookup"><span data-stu-id="5595e-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="5595e-126">Fazendo uma chamada REST em uma API protegida</span><span class="sxs-lookup"><span data-stu-id="5595e-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="5595e-127">Este aplicativo de exemplo hello `getContentWithToken()` método é usado toomake um HTTP `GET` solicitação em um recurso protegido que requer um chamador de conteúdo toohello Olá token e retornar.</span><span class="sxs-lookup"><span data-stu-id="5595e-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="5595e-128">Este método adiciona token Olá adquirido em Olá *cabeçalho de autorização HTTP*.</span><span class="sxs-lookup"><span data-stu-id="5595e-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="5595e-129">Para este exemplo, o recurso de saudação é Olá Microsoft Graph API *me* ponto de extremidade – que exibe informações de perfil do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5595e-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="5595e-130">Configurar a saída</span><span class="sxs-lookup"><span data-stu-id="5595e-130">Set up sign-out</span></span>

<span data-ttu-id="5595e-131">Adicionar Olá seguinte método muito`ViewController.swift` toosign usuário hello:</span><span class="sxs-lookup"><span data-stu-id="5595e-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="5595e-132">Mais informações sobre a saída</span><span class="sxs-lookup"><span data-stu-id="5595e-132">More info on sign-out</span></span>

<span data-ttu-id="5595e-133">Olá `signoutButton` método Remove o usuário de saudação do hello cache de usuário MSAL – isso efetivamente informará o usuário atual do MSAL tooforget Olá para uma solicitação futuras tooacquire um token terá êxito apenas se ele for feito toobe interativo.</span><span class="sxs-lookup"><span data-stu-id="5595e-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="5595e-134">Embora o aplicativo hello neste exemplo dá suporte a um único usuário, MSAL oferece suporte a cenários onde várias contas podem entrar em hello simultaneamente – um exemplo é um aplicativo de email onde um usuário tenha várias contas.</span><span class="sxs-lookup"><span data-stu-id="5595e-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="5595e-135">Registrar o retorno de chamada de saudação</span><span class="sxs-lookup"><span data-stu-id="5595e-135">Register hello callback</span></span>

<span data-ttu-id="5595e-136">Depois que a autenticação do usuário hello, redirecionamentos do navegador Olá Olá usuário toohello back aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5595e-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="5595e-137">Siga as etapas de saudação abaixo tooregister esse retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="5595e-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="5595e-138">Abra `AppDelegate.swift` e importe a MSAL:</span><span class="sxs-lookup"><span data-stu-id="5595e-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="5595e-139">Adicionar Olá após o método tooyour <code>AppDelegate</code> toohandle retornos de chamada de classe:</span><span class="sxs-lookup"><span data-stu-id="5595e-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
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

