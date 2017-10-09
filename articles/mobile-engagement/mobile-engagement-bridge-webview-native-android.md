---
title: aaaBridge WebView Android com nativo Mobile Engagement Android SDK
description: "Descreve como toocreate uma ponte entre WebView Javascript em execução e Olá nativo Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="b2f74-103">Ponte Android WebView com o SDK do Mobile Engagement Android</span><span class="sxs-lookup"><span data-stu-id="b2f74-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2f74-104">Ponte do Android</span><span class="sxs-lookup"><span data-stu-id="b2f74-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="b2f74-105">Ponte do iOS</span><span class="sxs-lookup"><span data-stu-id="b2f74-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="b2f74-106">Alguns aplicativos móveis são criados como um aplicativo híbrido onde aplicativo hello em si é desenvolvido usando desenvolvimento Android nativo, mas algumas ou todas as telas de saudação são renderizadas dentro de uma exibição da Web Android.</span><span class="sxs-lookup"><span data-stu-id="b2f74-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="b2f74-107">Você ainda pode consumir o Android SDK do Mobile Engagement em tais aplicativos e este tutorial descreve como toogo sobre como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="b2f74-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="b2f74-108">código de exemplo Hello abaixo se baseia Olá documentação Android [aqui](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span><span class="sxs-lookup"><span data-stu-id="b2f74-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="b2f74-109">Descreve como essa abordagem documentada serviria tooimplement Olá mesmo para o Android SDK do Mobile Engagement métodos de uso comum, de forma que uma exibição da Web de um aplicativo híbrido também pode iniciar solicitações tootrack eventos, trabalhos, erros, informações do aplicativo ao canalizá-los por meio de nosso SDK do Android.</span><span class="sxs-lookup"><span data-stu-id="b2f74-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="b2f74-110">Em primeiro lugar, você precisa tooensure que passaram por meio de nosso [tutorial de Introdução](mobile-engagement-android-get-started.md) toointegrate Olá Android SDK do Mobile Engagement em seu aplicativo híbrido.</span><span class="sxs-lookup"><span data-stu-id="b2f74-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="b2f74-111">Depois de fazer isso, seu `OnCreate` método será semelhante ao seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="b2f74-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="b2f74-112">Agora, verifique se seu aplicativo híbrido tem uma tela com WebView.</span><span class="sxs-lookup"><span data-stu-id="b2f74-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="b2f74-113">Olá código para ele será semelhante toohello seguinte onde estamos carregando um arquivo HTML local **Sample.html** em Olá Webview em Olá `onCreate` método da tela.</span><span class="sxs-lookup"><span data-stu-id="b2f74-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="b2f74-114">Agora, crie um arquivo de ponte chamado **WebAppInterface** que cria um wrapper sobre alguns comumente usados métodos Android SDK do Mobile Engagement usando Olá `@JavascriptInterface` abordagem descrita Olá [documentação Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="b2f74-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="b2f74-115">Quando criamos Olá acima arquivo ponte, é preciso tooensure que está associada a nossa Webview.</span><span class="sxs-lookup"><span data-stu-id="b2f74-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="b2f74-116">Para este toohappen, você precisa tooedit seu `SetWebview` método para que ela se pareça com hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2f74-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="b2f74-117">Olá acima trecho, chamamos `addJavascriptInterface` tooassociate nosso ponte classe com nosso Webview e também criou um identificador chamado **EngagementJs** toocall métodos de saudação do arquivo de saudação da ponte.</span><span class="sxs-lookup"><span data-stu-id="b2f74-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="b2f74-118">Agora crie Olá após o arquivo chamado **Sample.html** em seu projeto em uma pasta chamada **ativos** que é carregado no hello Webview e onde chamaremos métodos de saudação do arquivo de saudação da ponte.</span><span class="sxs-lookup"><span data-stu-id="b2f74-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="b2f74-119">Pontos a seguir Olá Observação sobre o arquivo HTML Olá acima:</span><span class="sxs-lookup"><span data-stu-id="b2f74-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="b2f74-120">Ele contém um conjunto de caixas de entrada, onde você pode fornecer dados toobe utilizado como nomes de seu evento, o trabalho, o erro, o AppInfo.</span><span class="sxs-lookup"><span data-stu-id="b2f74-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="b2f74-121">Quando você clica em Olá botão Avançar tooit, é feita uma chamada toohello Javascript que eventualmente chama métodos de saudação da saudação ponte arquivo toopass toohello essa chamada Android SDK do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b2f74-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="b2f74-122">Nós são marcação em alguns eventos de toohello informações estáticas sobre extra, trabalhos e até mesmo erros toodemonstrate como isso pode ser feito.</span><span class="sxs-lookup"><span data-stu-id="b2f74-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="b2f74-123">Essas informações extras é enviada como um JSON de cadeia de caracteres que, se você olhar no hello `WebAppInterface` de arquivo, é analisado e colocar em um Android `Bundle` e é passado juntamente com eventos, trabalhos, erros de envio.</span><span class="sxs-lookup"><span data-stu-id="b2f74-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="b2f74-124">Um trabalho do Mobile Engagement é iniciado com o nome hello você especificar na caixa de entrada hello, executado por 10 segundos e desligar.</span><span class="sxs-lookup"><span data-stu-id="b2f74-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="b2f74-125">Um compromisso de mobilidade appinfo ou uma marca é passada com 'customer_name' como chave estática hello e o valor de saudação que você inseriu na entrada hello como valor Olá para marca de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2f74-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="b2f74-126">Saudação de execução de aplicativo e você verá a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="b2f74-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="b2f74-127">Agora, fornecer algum nome de um evento de teste como Olá a seguir e clique em **enviar** abaixo dela.</span><span class="sxs-lookup"><span data-stu-id="b2f74-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="b2f74-128">Agora, se você for toohello **Monitor** guia do aplicativo e veja em **eventos -> detalhes**, você verá esse evento aparecer junto com hello estático app-info que estamos enviando.</span><span class="sxs-lookup"><span data-stu-id="b2f74-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
