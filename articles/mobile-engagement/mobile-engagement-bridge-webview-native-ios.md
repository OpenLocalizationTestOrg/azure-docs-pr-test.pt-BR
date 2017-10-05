---
title: "Faça a ponte entre o iOS WebView com SDK do Mobile Engagement iOS"
description: Descreve como criar uma ponte entre o WebView com Javascript e o SDK do Mobile Engagement iOS nativo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35f7bdbeb480122513ae2a0b04a6d8cfd426802a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="8333d-103">Faça a ponte entre o iOS WebView com SDK do Mobile Engagement iOS</span><span class="sxs-lookup"><span data-stu-id="8333d-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8333d-104">Ponte do Android</span><span class="sxs-lookup"><span data-stu-id="8333d-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="8333d-105">Ponte do iOS</span><span class="sxs-lookup"><span data-stu-id="8333d-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="8333d-106">Alguns aplicativos móveis são projetados como um aplicativo híbrido onde o aplicativo foi desenvolvido usando o desenvolvimento do iOS Objective-C nativo, mas algumas ou todas as telas são renderizadas em um WebView iOS.</span><span class="sxs-lookup"><span data-stu-id="8333d-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native iOS Objective-C development but some or even all of the screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="8333d-107">Você ainda pode consumir o SDK do Mobile Engagement iOS em tais aplicativos e este tutorial descreve como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="8333d-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how to go about doing this.</span></span> 

<span data-ttu-id="8333d-108">Há duas abordagens para fazer isso, embora nenhuma esteja documentada:</span><span class="sxs-lookup"><span data-stu-id="8333d-108">There are two approaches to achieve this though both are undocumented:</span></span>

* <span data-ttu-id="8333d-109">A primeira é descrita neste [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) e envolve registrar um `UIWebViewDelegate` no modo de exibição da Web e pegar e cancelar imediatamente uma alteração de local feita no Javascript.</span><span class="sxs-lookup"><span data-stu-id="8333d-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="8333d-110">A segunda se baseia nesta [sessão WWDC 2013](https://developer.apple.com/videos/play/wwdc2013/615), essa abordagem é mais simples do que a primeira e é ela que vamos seguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="8333d-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than the first and which we will follow for this guide.</span></span> <span data-ttu-id="8333d-111">Observe que essa abordagem funciona apenas no iOS7 e posterior.</span><span class="sxs-lookup"><span data-stu-id="8333d-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="8333d-112">Siga as etapas abaixo para a ponte de iOS de exemplo:</span><span class="sxs-lookup"><span data-stu-id="8333d-112">Follow the steps below for the iOS bridge sample:</span></span>

1. <span data-ttu-id="8333d-113">Em primeiro lugar, você precisa concluir nosso [Tutorial de introdução](mobile-engagement-ios-get-started.md) para integrar o SDK do Mobile Engagement iOS ao aplicativo híbrido.</span><span class="sxs-lookup"><span data-stu-id="8333d-113">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) to integrate the Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="8333d-114">Opcionalmente, você também pode habilitar o registro em log de teste da forma indicada a seguir para que possa ver os métodos do SDK conforme vamos disparando-os do Webview.</span><span class="sxs-lookup"><span data-stu-id="8333d-114">Optionally, you can also enable test logging as follows so that you can see the SDK methods as we trigger them from the webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="8333d-115">Agora, verifique se seu aplicativo híbrido tem uma tela com WebView.</span><span class="sxs-lookup"><span data-stu-id="8333d-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="8333d-116">Você pode adicioná-lo ao `Main.storyboard` do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8333d-116">You can add it to the `Main.storyboard` of the app.</span></span> 
3. <span data-ttu-id="8333d-117">Associe esse modo de exibição da Web ao seu **ViewController** clicando e arrastando o modo de exibição da Web da Cena de Controlador de Exibição para a tela de edição do `ViewController.h`, colocando-o logo abaixo da linha `@interface`.</span><span class="sxs-lookup"><span data-stu-id="8333d-117">Associate this webview with your **ViewController** by clicking and dragging the webview from the View Controller Scene to the `ViewController.h` edit screen, placing it just below the `@interface` line.</span></span> 
4. <span data-ttu-id="8333d-118">Quando você fizer isso, uma caixa de diálogo será exibida solicitando um nome.</span><span class="sxs-lookup"><span data-stu-id="8333d-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="8333d-119">Forneça o nome como **webView**.</span><span class="sxs-lookup"><span data-stu-id="8333d-119">Provide the name as **webView**.</span></span> <span data-ttu-id="8333d-120">Seu arquivo `ViewController.h` deverá ter a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="8333d-120">Your `ViewController.h` file should look like the following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="8333d-121">Atualizaremos o arquivo `ViewController.m` mais tarde, mas primeiro vamos criar o arquivo de ponte que cria um wrapper sobre alguns métodos comumente usados do SDK do Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="8333d-121">We will update the `ViewController.m` file later but first we will create the bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="8333d-122">Crie um novo arquivo de cabeçalho chamado **EngagementJsExports.h** que usa o mecanismo do `JSExport` descrito na [sessão](https://developer.apple.com/videos/play/wwdc2013/615) mencionada anteriormente para expor os métodos iOS nativos.</span><span class="sxs-lookup"><span data-stu-id="8333d-122">Create a new header file called **EngagementJsExports.h** which uses the `JSExport` mechanism described in the aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) to expose the native iOS methods.</span></span> 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. <span data-ttu-id="8333d-123">Em seguida, criaremos a segunda parte do arquivo de ponte.</span><span class="sxs-lookup"><span data-stu-id="8333d-123">Next we will create the second part of the bridge file.</span></span> <span data-ttu-id="8333d-124">Crie um arquivo chamado **EngagementJsExports.m** que conterá a implementação que cria os wrappers reais chamando métodos do SDK do Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="8333d-124">Create a file called **EngagementJsExports.m** which will contain the implementation creating the actual wrappers by calling the Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="8333d-125">Observe também que estamos analisando os `extras` que são passados do Webview do Javascript e colocando isso em um objeto `NSMutableDictionary` a ser passado com as chamadas de método do SDK do Engagement.</span><span class="sxs-lookup"><span data-stu-id="8333d-125">Also note that we are parsing the `extras` being passed from the webview javascript and putting that into an `NSMutableDictionary` object to be passed with the Engagement SDK method calls.</span></span>  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. <span data-ttu-id="8333d-126">Agora podemos voltar para o **viewcontroller.m** e atualizá-lo com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="8333d-126">Now we come back to the **ViewController.m** and update it with the following code:</span></span> 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. <span data-ttu-id="8333d-127">Observe os seguintes pontos sobre o arquivo **viewcontroller. M** :</span><span class="sxs-lookup"><span data-stu-id="8333d-127">Note the following points about the **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="8333d-128">No método `loadWebView` , estamos carregando um arquivo HTML local chamado **LocalPage.html** cujo código examinaremos em seguida.</span><span class="sxs-lookup"><span data-stu-id="8333d-128">In the `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="8333d-129">No método `webViewDidFinishLoad`, pegamos o `JsContext` e associamos nossa classe de wrapper a ele.</span><span class="sxs-lookup"><span data-stu-id="8333d-129">In the `webViewDidFinishLoad` method, we are grabbing the `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="8333d-130">Isso permitirá chamar métodos SDK do wrapper usando o identificador **EngagementJs** do webView.</span><span class="sxs-lookup"><span data-stu-id="8333d-130">This will allow calling our wrapper SDK methods using the handle **EngagementJs** from the webView.</span></span> 
9. <span data-ttu-id="8333d-131">Crie um arquivo chamado **LocalPage.html** com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="8333d-131">Create a file called **LocalPage.html** with the following code:</span></span>
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with the Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. <span data-ttu-id="8333d-132">Observe os seguintes pontos sobre o arquivo HTML acima:</span><span class="sxs-lookup"><span data-stu-id="8333d-132">Note the following points about the HTML file above:</span></span>
    
    * <span data-ttu-id="8333d-133">Ele contém um conjunto de caixas de entrada onde você pode fornecer dados a serem usados como nomes de Evento, Erro, Trabalho, AppInfo.</span><span class="sxs-lookup"><span data-stu-id="8333d-133">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="8333d-134">Quando você clica no botão ao lado dele, é feita uma chamada para o Javascript que eventualmente chama os métodos do arquivo de ponte para passar essa chamada para o SDK do Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="8333d-134">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="8333d-135">Estamos marcando algumas informações estáticas adicionais nos eventos, nos trabalhos e até mesmo nos erros para demonstrar como isso pode ser feito.</span><span class="sxs-lookup"><span data-stu-id="8333d-135">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="8333d-136">Essa informação adicional é enviada como uma cadeia de caracteres JSON que, se você olhar o arquivo `EngagementJsExports.m` , é analisada e passada juntamente com envios de Eventos, Trabalhos, Erros.</span><span class="sxs-lookup"><span data-stu-id="8333d-136">This extra info is sent as a JSON string which, if you look in the `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="8333d-137">O Trabalho do Mobile Engagement é inicializado com o nome que você especifica na caixa de entrada, executado por 10 segundos e, em seguida, desligado.</span><span class="sxs-lookup"><span data-stu-id="8333d-137">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="8333d-138">Um appinfo ou marca do Mobile Engagement é passada com “customer_name” como a chave estática e com o valor que você inseriu na entrada como o valor da marca.</span><span class="sxs-lookup"><span data-stu-id="8333d-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
11. <span data-ttu-id="8333d-139">Execute o aplicativo e você verá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8333d-139">Run the app and you will see the following.</span></span> <span data-ttu-id="8333d-140">Agora, forneça um nome para um evento de teste conforme mostrado a seguir e clique em **Enviar** ao lado.</span><span class="sxs-lookup"><span data-stu-id="8333d-140">Now provide some name for a test event like the following and click **Send** next to it.</span></span> 
    
     ![][1]
12. <span data-ttu-id="8333d-141">Agora, se você acessar a guia **Monitor** do aplicativo e procurar em **Eventos -> Detalhes**, verá esse evento aparecer junto ao app-info estático que estamos enviando.</span><span class="sxs-lookup"><span data-stu-id="8333d-141">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
