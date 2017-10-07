---
title: iOS aaaBridge WebView com o SDK do iOS nativo do Mobile Engagement
description: "Descreve como toocreate uma ponte entre a exibição da Web que executa o Javascript e hello nativo do Mobile Engagement iOS SDK"
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
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="b62d4-103">Faça a ponte entre o iOS WebView com SDK do Mobile Engagement iOS</span><span class="sxs-lookup"><span data-stu-id="b62d4-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b62d4-104">Ponte do Android</span><span class="sxs-lookup"><span data-stu-id="b62d4-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="b62d4-105">Ponte do iOS</span><span class="sxs-lookup"><span data-stu-id="b62d4-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="b62d4-106">Alguns aplicativos móveis são criados como um aplicativo híbrido onde aplicativo hello em si é desenvolvido usando desenvolvimento iOS nativo Objective-C, mas algumas ou todas as telas de saudação são renderizadas dentro de um exibição da Web do iOS.</span><span class="sxs-lookup"><span data-stu-id="b62d4-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="b62d4-107">Você ainda pode consumir o SDK do iOS do Mobile Engagement em tais aplicativos e este tutorial descreve como toogo sobre como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="b62d4-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="b62d4-108">Há dois tooachieve de abordagens isso Embora ambos sejam documentadas:</span><span class="sxs-lookup"><span data-stu-id="b62d4-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="b62d4-109">A primeira é descrita neste [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) e envolve registrar um `UIWebViewDelegate` no modo de exibição da Web e pegar e cancelar imediatamente uma alteração de local feita no Javascript.</span><span class="sxs-lookup"><span data-stu-id="b62d4-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="b62d4-110">Segundo uma baseada nessa [WWDC 2013 sessão](https://developer.apple.com/videos/play/wwdc2013/615), uma abordagem que é mais fácil do que Olá primeiro e que vamos seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="b62d4-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="b62d4-111">Observe que essa abordagem funciona apenas no iOS7 e posterior.</span><span class="sxs-lookup"><span data-stu-id="b62d4-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="b62d4-112">Siga as etapas de saudação abaixo para iOS Olá ponte exemplo:</span><span class="sxs-lookup"><span data-stu-id="b62d4-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="b62d4-113">Em primeiro lugar, você precisa tooensure que passaram por meio de nosso [tutorial de Introdução](mobile-engagement-ios-get-started.md) toointegrate Olá iOS SDK do Mobile Engagement em seu aplicativo híbrido.</span><span class="sxs-lookup"><span data-stu-id="b62d4-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="b62d4-114">Opcionalmente, você também pode habilitar teste log da seguinte maneira para que você pode ver os métodos SDK Olá como podemos dispará-los do webview Olá.</span><span class="sxs-lookup"><span data-stu-id="b62d4-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="b62d4-115">Agora, verifique se seu aplicativo híbrido tem uma tela com WebView.</span><span class="sxs-lookup"><span data-stu-id="b62d4-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="b62d4-116">Você pode adicionar toohello `Main.storyboard` do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b62d4-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="b62d4-117">Associar este webview com seu **ViewController** clicando e arrastando Olá webview da saudação exibição controlador cena toohello `ViewController.h` Editar tela, colocando-o abaixo Olá `@interface` linha.</span><span class="sxs-lookup"><span data-stu-id="b62d4-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="b62d4-118">Quando você fizer isso, uma caixa de diálogo será exibida solicitando um nome.</span><span class="sxs-lookup"><span data-stu-id="b62d4-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="b62d4-119">Forneça nome hello como **webView**.</span><span class="sxs-lookup"><span data-stu-id="b62d4-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="b62d4-120">O `ViewController.h` arquivo deve ser semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="b62d4-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="b62d4-121">Atualizaremos Olá `ViewController.m` arquivo mais tarde, mas primeiro vamos criar arquivo de saudação da ponte que cria um wrapper sobre alguns iOS Mobile Engagement comumente usados métodos do SDK.</span><span class="sxs-lookup"><span data-stu-id="b62d4-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="b62d4-122">Criar um novo arquivo de cabeçalho chamado **EngagementJsExports.h** que usa Olá `JSExport` mecanismo descrito em Olá mencionados acima [sessão](https://developer.apple.com/videos/play/wwdc2013/615) métodos do tooexpose Olá iOS nativo.</span><span class="sxs-lookup"><span data-stu-id="b62d4-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="b62d4-123">Em seguida, vamos criar a segunda parte Olá do arquivo de saudação da ponte.</span><span class="sxs-lookup"><span data-stu-id="b62d4-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="b62d4-124">Crie um arquivo chamado **EngagementJsExports.m** que conterá a implementação de saudação criando Olá wrappers reais chamando métodos do SDK Olá Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="b62d4-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="b62d4-125">Observe também que podemos estiver analisando Olá `extras` sendo passados do hello webview javascript e colocá-lo para um `NSMutableDictionary` toobe objeto passado com hello método do SDK do contrato chamadas.</span><span class="sxs-lookup"><span data-stu-id="b62d4-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="b62d4-126">Agora podemos voltar toohello **ViewController.m** e atualizá-lo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b62d4-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="b62d4-127">Pontos a seguir Olá Observação sobre Olá **ViewController.m** arquivo:</span><span class="sxs-lookup"><span data-stu-id="b62d4-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="b62d4-128">Em Olá `loadWebView` método, estamos carregando um arquivo HTML local chamado **LocalPage.html** cujo código analisaremos lado.</span><span class="sxs-lookup"><span data-stu-id="b62d4-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="b62d4-129">Em Olá `webViewDidFinishLoad` método, são captando Olá `JsContext` e associando nossa classe wrapper ele.</span><span class="sxs-lookup"><span data-stu-id="b62d4-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="b62d4-130">Isso permitirá que chamar métodos SDK usando o identificador de saudação de nosso wrapper **EngagementJs** do webView hello.</span><span class="sxs-lookup"><span data-stu-id="b62d4-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="b62d4-131">Crie um arquivo chamado **LocalPage.html** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b62d4-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
                       // Example of how extras info can be passed with hello Engagement logs
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
10. <span data-ttu-id="b62d4-132">Pontos a seguir Olá Observação sobre o arquivo HTML Olá acima:</span><span class="sxs-lookup"><span data-stu-id="b62d4-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="b62d4-133">Ele contém um conjunto de caixas de entrada, onde você pode fornecer dados toobe utilizado como nomes de seu evento, o trabalho, o erro, o AppInfo.</span><span class="sxs-lookup"><span data-stu-id="b62d4-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="b62d4-134">Quando você clica em Olá botão Avançar tooit, é feita uma chamada toohello Javascript que eventualmente chama métodos de saudação da saudação ponte arquivo toopass toohello essa chamada do SDK do Mobile Engagement iOS.</span><span class="sxs-lookup"><span data-stu-id="b62d4-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="b62d4-135">Nós são marcação em alguns eventos de toohello informações estáticas sobre extra, trabalhos e até mesmo erros toodemonstrate como isso pode ser feito.</span><span class="sxs-lookup"><span data-stu-id="b62d4-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="b62d4-136">Essas informações extras é enviada como um JSON de cadeia de caracteres que, se você olhar no hello `EngagementJsExports.m` de arquivo, é analisado e passadas junto com eventos, trabalhos, erros de envio.</span><span class="sxs-lookup"><span data-stu-id="b62d4-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="b62d4-137">Um trabalho do Mobile Engagement é iniciado com o nome hello você especificar na caixa de entrada hello, executado por 10 segundos e desligar.</span><span class="sxs-lookup"><span data-stu-id="b62d4-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="b62d4-138">Um compromisso de mobilidade appinfo ou uma marca é passada com 'customer_name' como chave estática hello e o valor de saudação que você inseriu na entrada hello como valor Olá para marca de saudação.</span><span class="sxs-lookup"><span data-stu-id="b62d4-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="b62d4-139">Saudação de execução de aplicativo e você verá a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="b62d4-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="b62d4-140">Agora, fornecer algum nome de um evento de teste como Olá a seguir e clique em **enviar** tooit Avançar.</span><span class="sxs-lookup"><span data-stu-id="b62d4-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="b62d4-141">Agora, se você for toohello **Monitor** guia do aplicativo e veja em **eventos -> detalhes**, você verá esse evento aparecer junto com hello estático app-info que estamos enviando.</span><span class="sxs-lookup"><span data-stu-id="b62d4-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
