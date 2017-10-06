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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Monitorar um site do SharePoint com o Application Insights
Ideias de aplicativo do Azure monitora a disponibilidade hello, desempenho e uso de seus aplicativos. Aqui você aprenderá como tooset-a para um site do SharePoint.

## <a name="create-an-application-insights-resource"></a>Criar um recurso do Application Insights
Em Olá [portal do Azure](https://portal.azure.com), criar um novo recurso do Application Insights. Escolha o ASP.NET como o tipo de aplicativo hello.

![Clique em propriedades, selecione a chave de saudação e pressione ctrl + C](./media/app-insights-sharepoint/01-new.png)

folha de saudação que abre é o local de saudação onde você verá os dados de uso e desempenho sobre seu aplicativo. tooit back tooget próxima vez que fizer logon tooAzure, você deve encontrar um bloco para ele na tela de início de saudação. Como alternativa, clique em Procurar toofind-lo.

## <a name="add-our-script-tooyour-web-pages"></a>Adicionar páginas da web tooyour script
No início rápido, obter o script hello para páginas da web:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Inserir o script hello antes Olá &lt;/head&gt; marca de cada página que você deseja tootrack. Se o site tiver uma página mestre, você pode colocar o script hello existe. Por exemplo, em um projeto ASP.NET MVC, você deve colocá-lo em View\Shared\_Layout. cshtml

script Hello contém a chave de instrumentação Olá que direciona o recurso do Application Insights do hello telemetria tooyour.

### <a name="add-hello-code-tooyour-site-pages"></a>Adicionar o código de saudação tooyour páginas de site
#### <a name="on-hello-master-page"></a>Na página mestre Olá
Se você pode editar a página mestra saudação do site, que fornecem monitoramento para cada página no site de saudação.

Confira a página mestra hello e editá-lo usando o SharePoint Designer ou qualquer outro editor.

![](./media/app-insights-sharepoint/03-master.png)

Adicione código de saudação antes Olá </head> marca. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>Ou em páginas individuais
toomonitor um conjunto limitado de páginas, adicionar script hello separadamente tooeach página. 

Inserir uma web part e inserir o trecho de código Olá nele.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Exibir dados sobre seu aplicativo
Reimplante o aplicativo.

Folha de aplicativos de retorno tooyour em Olá [portal do Azure](https://portal.azure.com).

eventos de primeira Hello serão exibidos na pesquisa. 

![](./media/app-insights-sharepoint/09-search.png)

Se você estiver esperando mais dados, clique em Atualizar depois de alguns segundos.

Na folha de visão geral de saudação, clique em **a análise de uso** toocharts toosee de usuários, sessões e modos de exibição de página:

![](./media/app-insights-sharepoint/06-usage.png)

Clique em qualquer toosee gráfico mais detalhes - por exemplo modos de exibição de página:

![](./media/app-insights-sharepoint/07-pages.png)

Ou Usuários:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Capturando a ID de usuário
trecho de código de página da web padrão Olá não captura o id de usuário de saudação do SharePoint, mas você pode fazer isso com uma pequena modificação.

1. Copie a chave de instrumentação do aplicativo de saudação Essentials suspensa no Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Substitua por chave de instrumentação Olá 'XXXX' no trecho de saudação abaixo. 
2. Inseri script hello em seu aplicativo do SharePoint, em vez de trecho Olá que obter do portal de saudação.

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



## <a name="next-steps"></a>Próximas etapas
* [Testes na Web](app-insights-monitor-web-app-availability.md) toomonitor disponibilidade de saudação do seu site.
* [Application Insights](app-insights-overview.md) para outros tipos de aplicativos.

<!--Link references-->


