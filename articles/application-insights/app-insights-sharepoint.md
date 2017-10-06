---
title: aaaMonitor um site do SharePoint com o Application Insights
description: "Iniciar o monitoramento de um novo aplicativo com uma nova chave de instrumentação"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="b6ced-103">Monitorar um site do SharePoint com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="b6ced-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="b6ced-104">Ideias de aplicativo do Azure monitora a disponibilidade hello, desempenho e uso de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b6ced-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="b6ced-105">Aqui você aprenderá como tooset-a para um site do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b6ced-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="b6ced-106">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="b6ced-106">Create an Application Insights resource</span></span>
<span data-ttu-id="b6ced-107">Em Olá [portal do Azure](https://portal.azure.com), criar um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b6ced-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="b6ced-108">Escolha o ASP.NET como o tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b6ced-108">Choose ASP.NET as hello application type.</span></span>

![Clique em propriedades, selecione a chave de saudação e pressione ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="b6ced-110">folha de saudação que abre é o local de saudação onde você verá os dados de uso e desempenho sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6ced-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="b6ced-111">tooit back tooget próxima vez que fizer logon tooAzure, você deve encontrar um bloco para ele na tela de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6ced-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="b6ced-112">Como alternativa, clique em Procurar toofind-lo.</span><span class="sxs-lookup"><span data-stu-id="b6ced-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="b6ced-113">Adicionar páginas da web tooyour script</span><span class="sxs-lookup"><span data-stu-id="b6ced-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="b6ced-114">No início rápido, obter o script hello para páginas da web:</span><span class="sxs-lookup"><span data-stu-id="b6ced-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="b6ced-115">Inserir o script hello antes Olá &lt;/head&gt; marca de cada página que você deseja tootrack.</span><span class="sxs-lookup"><span data-stu-id="b6ced-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="b6ced-116">Se o site tiver uma página mestre, você pode colocar o script hello existe.</span><span class="sxs-lookup"><span data-stu-id="b6ced-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="b6ced-117">Por exemplo, em um projeto ASP.NET MVC, você deve colocá-lo em View\Shared\_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="b6ced-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="b6ced-118">script Hello contém a chave de instrumentação Olá que direciona o recurso do Application Insights do hello telemetria tooyour.</span><span class="sxs-lookup"><span data-stu-id="b6ced-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="b6ced-119">Adicionar o código de saudação tooyour páginas de site</span><span class="sxs-lookup"><span data-stu-id="b6ced-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="b6ced-120">Na página mestre Olá</span><span class="sxs-lookup"><span data-stu-id="b6ced-120">On hello master page</span></span>
<span data-ttu-id="b6ced-121">Se você pode editar a página mestra saudação do site, que fornecem monitoramento para cada página no site de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6ced-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="b6ced-122">Confira a página mestra hello e editá-lo usando o SharePoint Designer ou qualquer outro editor.</span><span class="sxs-lookup"><span data-stu-id="b6ced-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="b6ced-123">Adicione código de saudação antes Olá </head> marca.</span><span class="sxs-lookup"><span data-stu-id="b6ced-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="b6ced-124">Ou em páginas individuais</span><span class="sxs-lookup"><span data-stu-id="b6ced-124">Or on individual pages</span></span>
<span data-ttu-id="b6ced-125">toomonitor um conjunto limitado de páginas, adicionar script hello separadamente tooeach página.</span><span class="sxs-lookup"><span data-stu-id="b6ced-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="b6ced-126">Inserir uma web part e inserir o trecho de código Olá nele.</span><span class="sxs-lookup"><span data-stu-id="b6ced-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="b6ced-127">Exibir dados sobre seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b6ced-127">View data about your app</span></span>
<span data-ttu-id="b6ced-128">Reimplante o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6ced-128">Redeploy your app.</span></span>

<span data-ttu-id="b6ced-129">Folha de aplicativos de retorno tooyour em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6ced-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b6ced-130">eventos de primeira Hello serão exibidos na pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b6ced-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="b6ced-131">Se você estiver esperando mais dados, clique em Atualizar depois de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="b6ced-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="b6ced-132">Na folha de visão geral de saudação, clique em **a análise de uso** toocharts toosee de usuários, sessões e modos de exibição de página:</span><span class="sxs-lookup"><span data-stu-id="b6ced-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="b6ced-133">Clique em qualquer toosee gráfico mais detalhes - por exemplo modos de exibição de página:</span><span class="sxs-lookup"><span data-stu-id="b6ced-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="b6ced-134">Ou Usuários:</span><span class="sxs-lookup"><span data-stu-id="b6ced-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="b6ced-135">Capturando a ID de usuário</span><span class="sxs-lookup"><span data-stu-id="b6ced-135">Capturing User Id</span></span>
<span data-ttu-id="b6ced-136">trecho de código de página da web padrão Olá não captura o id de usuário de saudação do SharePoint, mas você pode fazer isso com uma pequena modificação.</span><span class="sxs-lookup"><span data-stu-id="b6ced-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="b6ced-137">Copie a chave de instrumentação do aplicativo de saudação Essentials suspensa no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b6ced-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="b6ced-138">Substitua por chave de instrumentação Olá 'XXXX' no trecho de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b6ced-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="b6ced-139">Inseri script hello em seu aplicativo do SharePoint, em vez de trecho Olá que obter do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6ced-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="b6ced-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6ced-140">Next Steps</span></span>
* <span data-ttu-id="b6ced-141">[Testes na Web](app-insights-monitor-web-app-availability.md) toomonitor disponibilidade de saudação do seu site.</span><span class="sxs-lookup"><span data-stu-id="b6ced-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="b6ced-142">[Application Insights](app-insights-overview.md) para outros tipos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b6ced-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


