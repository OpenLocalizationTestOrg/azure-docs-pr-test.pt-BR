---
title: "Integração do SDK para Web do Azure Mobile Engagement | Microsoft Docs"
description: "As atualizações e procedimentos mais recentes do SDK para Web do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="6525a-103">Integrar o Azure Mobile Engagement em um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="6525a-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6525a-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="6525a-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="6525a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="6525a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="6525a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="6525a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="6525a-107">Android</span><span class="sxs-lookup"><span data-stu-id="6525a-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="6525a-108">Os procedimentos neste artigo descrevem a maneira mais simples de ativar as funções de análise e monitoramento no Azure Mobile Engagement no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6525a-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="6525a-109">Siga as etapas para ativar os relatórios de log necessários para calcular todas as estatísticas sobre usuários, sessões, atividades, falhas e técnicas.</span><span class="sxs-lookup"><span data-stu-id="6525a-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="6525a-110">Para estatísticas dependes do aplicativo, como eventos, erros e trabalhos, você deve ativar os relatórios de log manualmente usando a API do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6525a-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="6525a-111">Para obter mais informações, aprenda [como usar a API de marcação avançada do Mobile Engagement em um aplicativo Web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="6525a-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="6525a-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="6525a-112">Introduction</span></span>
<span data-ttu-id="6525a-113">[Baixe o SDK para Web do Azure Mobile Engagement](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="6525a-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="6525a-114">O SDK para Web do Mobile Engagement é fornecido como um único arquivo JavaScript, azure-engagement.js, que você precisa incluir em cada página do seu site ou aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6525a-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6525a-115">Antes de executar esse script, você deve executar um script ou trecho de código escrito para configurar o Mobile Engagement para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6525a-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="6525a-116">Compatibilidade de navegador</span><span class="sxs-lookup"><span data-stu-id="6525a-116">Browser compatibility</span></span>
<span data-ttu-id="6525a-117">O SDK para Web do Mobile Engagement usa a codificação e decodificação JSON nativa e solicitações AJAX entre domínios (que dependem da especificação W3C CORS).</span><span class="sxs-lookup"><span data-stu-id="6525a-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="6525a-118">Ele é compatível com os seguintes navegadores:</span><span class="sxs-lookup"><span data-stu-id="6525a-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="6525a-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="6525a-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="6525a-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="6525a-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="6525a-121">Firefox 3.5 e superior</span><span class="sxs-lookup"><span data-stu-id="6525a-121">Firefox 3.5+</span></span>
* <span data-ttu-id="6525a-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="6525a-122">Chrome 4+</span></span>
* <span data-ttu-id="6525a-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="6525a-123">Safari 6+</span></span>
* <span data-ttu-id="6525a-124">Opera 12 e superior</span><span class="sxs-lookup"><span data-stu-id="6525a-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="6525a-125">Configurar o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6525a-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="6525a-126">Escreva um script que crie um objeto JavaScript `azureEngagement` global como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6525a-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="6525a-127">Pelo fato de que seu site pode ter várias páginas, este exemplo supõe que este script esteja incluído em cada página.</span><span class="sxs-lookup"><span data-stu-id="6525a-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="6525a-128">Neste exemplo, o objeto JavaScript é denominado `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="6525a-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="6525a-129">O valor `connectionString` do seu aplicativo é exibido no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6525a-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6525a-130">`appVersionName` e `appVersionCode` são opcionais.</span><span class="sxs-lookup"><span data-stu-id="6525a-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="6525a-131">No entanto, é recomendável configurá-los para que a análise possa processar informações de versão.</span><span class="sxs-lookup"><span data-stu-id="6525a-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="6525a-132">Incluir scripts do Mobile Engagement em suas páginas</span><span class="sxs-lookup"><span data-stu-id="6525a-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="6525a-133">Adicione scripts do Mobile Engagement às suas páginas de uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="6525a-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="6525a-134">Ou assim:</span><span class="sxs-lookup"><span data-stu-id="6525a-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="6525a-135">Alias</span><span class="sxs-lookup"><span data-stu-id="6525a-135">Alias</span></span>
<span data-ttu-id="6525a-136">Depois que o script do SDK para Web do Mobile Engagement for carregado, ele criará o alias **engagement** para acessar as APIs do SDK.</span><span class="sxs-lookup"><span data-stu-id="6525a-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="6525a-137">Você não pode usar esse alias para definir a configuração do SDK.</span><span class="sxs-lookup"><span data-stu-id="6525a-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="6525a-138">Esse alias é usado como uma referência nesta documentação.</span><span class="sxs-lookup"><span data-stu-id="6525a-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="6525a-139">Observe que, se o alias padrão estiver em conflito com outra variável global da sua página, você poderá redefini-lo na configuração da seguinte maneira antes de carregar o SDK para Web do Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="6525a-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="6525a-140">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="6525a-140">Basic reporting</span></span>
<span data-ttu-id="6525a-141">Os relatórios básicos no Mobile Engagement abordam as estatísticas de nível de sessão, como estatísticas sobre usuários, sessões, atividades e falhas.</span><span class="sxs-lookup"><span data-stu-id="6525a-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="6525a-142">Rastreamento de sessão</span><span class="sxs-lookup"><span data-stu-id="6525a-142">Session tracking</span></span>
<span data-ttu-id="6525a-143">Uma sessão do Mobile Engagement é dividida em uma sequência de atividades, cada uma delas identificada por um nome.</span><span class="sxs-lookup"><span data-stu-id="6525a-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="6525a-144">Em um site clássico, é recomendável declarar uma atividade diferente em cada página do site.</span><span class="sxs-lookup"><span data-stu-id="6525a-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="6525a-145">Para um site ou aplicativo Web em que a página atual nunca muda, convém acompanhar as atividades em menor escala, como dentro da página.</span><span class="sxs-lookup"><span data-stu-id="6525a-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="6525a-146">De qualquer forma, para iniciar ou alterar a atividade do usuário atual, chame a função `engagement.agent.startActivity` .</span><span class="sxs-lookup"><span data-stu-id="6525a-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="6525a-147">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6525a-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="6525a-148">O servidor do Mobile Engagement encerra automaticamente uma sessão aberta em três minutos depois que a página do aplicativo é fechada.</span><span class="sxs-lookup"><span data-stu-id="6525a-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="6525a-149">Como alternativa, você pode encerrar uma sessão manualmente chamando `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="6525a-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="6525a-150">Isso define a atividade do usuário atual como 'Ociosa'.</span><span class="sxs-lookup"><span data-stu-id="6525a-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="6525a-151">A sessão será encerrada 10 segundos depois, a menos que uma nova chamada para `engagement.agent.startActivity` retome a sessão.</span><span class="sxs-lookup"><span data-stu-id="6525a-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="6525a-152">Você pode configurar o atraso de 10 segundos no objeto de compromisso global da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="6525a-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="6525a-153">Não é possível usar `engagement.agent.endActivity` no retorno de chamada de `onunload`, porque você não pode fazer chamadas AJAX neste estágio.</span><span class="sxs-lookup"><span data-stu-id="6525a-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="6525a-154">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="6525a-154">Advanced reporting</span></span>
<span data-ttu-id="6525a-155">Opcionalmente, se você deseja relatar trabalhos, erros e eventos específicos do aplicativo, precisa usar a API do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6525a-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="6525a-156">Acesse a API do Mobile Engagement pelo objeto `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="6525a-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="6525a-157">Você pode acessar todos os recursos avançados do Mobile Engagement na API do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6525a-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="6525a-158">A API é detalhada no artigo [Como usar a API de marcação avançada do Mobile Engagement em um aplicativo Web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="6525a-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="6525a-159">Personalizar as URLs usadas para chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="6525a-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="6525a-160">Você pode personalizar as URLs que o SDK para Web do Mobile Engagement usa.</span><span class="sxs-lookup"><span data-stu-id="6525a-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="6525a-161">Por exemplo, para redefinir a URL de log (o ponto de extremidade do SDK para registro em log), você pode substituir a configuração desta forma:</span><span class="sxs-lookup"><span data-stu-id="6525a-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="6525a-162">Se suas funções de URL retornarem uma cadeia de caracteres que começa com `/`, `//`, `http://` ou `https://`, o esquema padrão não será usado.</span><span class="sxs-lookup"><span data-stu-id="6525a-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="6525a-163">Por padrão, o esquema `https://` é usado para essas URLs.</span><span class="sxs-lookup"><span data-stu-id="6525a-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="6525a-164">Se desejar personalizar o esquema padrão, substitua a configuração desta forma:</span><span class="sxs-lookup"><span data-stu-id="6525a-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
