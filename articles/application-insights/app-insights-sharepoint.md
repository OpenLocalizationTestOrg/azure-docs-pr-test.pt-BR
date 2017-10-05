---
title: Monitorar um site do SharePoint com o Application Insights
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
ms.openlocfilehash: a3b37674469a131016f46af590e1eee3ba4cdc73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="4155a-103">Monitorar um site do SharePoint com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="4155a-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="4155a-104">O Azure Application Insights monitora a disponibilidade, o desempenho e o uso de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4155a-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="4155a-105">Aqui você aprenderá a configurá-lo para um site do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4155a-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="4155a-106">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4155a-106">Create an Application Insights resource</span></span>
<span data-ttu-id="4155a-107">No [Portal do Azure](https://portal.azure.com), crie um novo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4155a-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="4155a-108">Escolha ASP.NET como o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4155a-108">Choose ASP.NET as the application type.</span></span>

![Clique em Propriedades, selecione a chave e pressione ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="4155a-110">A folha que será aberta é o local em que você verá os dados de uso e desempenho sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4155a-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="4155a-111">Para retornar a ela na próxima vez em que fizer logon no Azure, você deverá encontrar um bloco para ela na tela inicial.</span><span class="sxs-lookup"><span data-stu-id="4155a-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="4155a-112">Como alternativa, clique em Procurar para localizá-la.</span><span class="sxs-lookup"><span data-stu-id="4155a-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="4155a-113">Adicione nosso script a suas páginas da Web</span><span class="sxs-lookup"><span data-stu-id="4155a-113">Add our script to your web pages</span></span>
<span data-ttu-id="4155a-114">Em Início Rápido, obtenha o script para páginas da Web:</span><span class="sxs-lookup"><span data-stu-id="4155a-114">In Quick Start, get the script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="4155a-115">Insira o script logo antes da marcação &lt;/head&gt; de cada página que você deseja controlar. Se seu site possui uma página mestra, você poderá colocar o script lá.</span><span class="sxs-lookup"><span data-stu-id="4155a-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="4155a-116">Por exemplo, em um projeto ASP.NET MVC, você deve colocá-lo em View\Shared\_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="4155a-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="4155a-117">O script contém a chave de instrumentação que direciona a telemetria para o recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4155a-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="4155a-118">Adicionar o código às páginas do site</span><span class="sxs-lookup"><span data-stu-id="4155a-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="4155a-119">Na página mestra</span><span class="sxs-lookup"><span data-stu-id="4155a-119">On the master page</span></span>
<span data-ttu-id="4155a-120">Se você puder editar a página mestra do site, que fornecerá monitoramento para todas as páginas no site.</span><span class="sxs-lookup"><span data-stu-id="4155a-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="4155a-121">Confira a página mestra e edite-a usando o SharePoint Designer ou qualquer outro editor.</span><span class="sxs-lookup"><span data-stu-id="4155a-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="4155a-122">Adicione o código antes da marca </head> .</span><span class="sxs-lookup"><span data-stu-id="4155a-122">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="4155a-123">Ou em páginas individuais</span><span class="sxs-lookup"><span data-stu-id="4155a-123">Or on individual pages</span></span>
<span data-ttu-id="4155a-124">Para monitorar um conjunto limitado de páginas, adicione o script separadamente a cada página.</span><span class="sxs-lookup"><span data-stu-id="4155a-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="4155a-125">Insira uma web part e insira o trecho de código nela.</span><span class="sxs-lookup"><span data-stu-id="4155a-125">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="4155a-126">Exibir dados sobre seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="4155a-126">View data about your app</span></span>
<span data-ttu-id="4155a-127">Reimplante o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4155a-127">Redeploy your app.</span></span>

<span data-ttu-id="4155a-128">Retorne à folha de seu aplicativo no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4155a-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4155a-129">Os primeiros eventos aparecerão na Pesquisa.</span><span class="sxs-lookup"><span data-stu-id="4155a-129">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="4155a-130">Se você estiver esperando mais dados, clique em Atualizar depois de alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="4155a-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="4155a-131">Na folha visão geral, clique em **análises de uso** para ver gráficos de usuários, sessões e modos de exibição de página:</span><span class="sxs-lookup"><span data-stu-id="4155a-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="4155a-132">Clique em qualquer gráfico para ver mais detalhes - exibições de página por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4155a-132">Click any chart to see more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="4155a-133">Ou Usuários:</span><span class="sxs-lookup"><span data-stu-id="4155a-133">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="4155a-134">Capturando a ID de usuário</span><span class="sxs-lookup"><span data-stu-id="4155a-134">Capturing User Id</span></span>
<span data-ttu-id="4155a-135">O trecho de código de página da Web padrão não captura a ID de usuário do SharePoint, mas você pode fazer isso com uma pequena modificação.</span><span class="sxs-lookup"><span data-stu-id="4155a-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="4155a-136">Copie a chave de instrumentação do seu aplicativo da lista suspensa Essentials no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4155a-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="4155a-137">Substitua a chave de instrumentação para 'XXXX' no trecho a seguir.</span><span class="sxs-lookup"><span data-stu-id="4155a-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="4155a-138">Insira o script em seu aplicativo do SharePoint, em vez de inserir o trecho de código que você obtém do portal.</span><span class="sxs-lookup"><span data-stu-id="4155a-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="4155a-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4155a-139">Next Steps</span></span>
* <span data-ttu-id="4155a-140">[Testes da web](app-insights-monitor-web-app-availability.md) para monitorar a disponibilidade de seu site.</span><span class="sxs-lookup"><span data-stu-id="4155a-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="4155a-141">[Application Insights](app-insights-overview.md) para outros tipos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4155a-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


