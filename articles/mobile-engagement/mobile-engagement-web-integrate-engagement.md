---
title: "aaaAzure integração do SDK do Mobile Engagement Web | Microsoft Docs"
description: "Olá atualizações mais recentes e procedimentos para Olá Web SDK do Azure Mobile Engagement"
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
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="713a5-103">Integrar o Azure Mobile Engagement em um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="713a5-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="713a5-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="713a5-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="713a5-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="713a5-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="713a5-106">iOS</span><span class="sxs-lookup"><span data-stu-id="713a5-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="713a5-107">Android</span><span class="sxs-lookup"><span data-stu-id="713a5-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="713a5-108">Olá neste artigo descrevem a análise do hello mais simples maneira tooactivate hello e funções no Azure Mobile Engagement em seu aplicativo web de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="713a5-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="713a5-109">Siga Olá etapas tooactivate Olá relatórios de log que são necessária toocompute todas as estatísticas sobre usuários, sessões, atividades, falhas e technicals.</span><span class="sxs-lookup"><span data-stu-id="713a5-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="713a5-110">Para estatísticas depende do aplicativo, como eventos, erros e trabalhos, você deve ativar relatórios de log manualmente usando Olá API do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="713a5-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="713a5-111">Para obter mais informações, saiba [como toouse Olá avançado marcação API em um aplicativo web do Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="713a5-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="713a5-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="713a5-112">Introduction</span></span>
<span data-ttu-id="713a5-113">[Baixar Olá Web SDK do Azure Mobile Engagement](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="713a5-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="713a5-114">Olá Mobile Engagement SDK da Web é enviado como um único arquivo de JavaScript, o azure-engagement.js, você tem tooinclude em cada página do seu site ou aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="713a5-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="713a5-115">Antes de executar esse script, você deve executar um script ou que você escreva tooconfigure Mobile Engagement para o seu aplicativo de trecho de código.</span><span class="sxs-lookup"><span data-stu-id="713a5-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="713a5-116">Compatibilidade de navegador</span><span class="sxs-lookup"><span data-stu-id="713a5-116">Browser compatibility</span></span>
<span data-ttu-id="713a5-117">Olá Web SDK do Mobile Engagement usa JSON nativo de codificação e decodificação, além de solicitações do AJAX toocross domínio (terceira na especificação do W3C CORS Olá).</span><span class="sxs-lookup"><span data-stu-id="713a5-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="713a5-118">Ele é compatível com hello navegadores a seguir:</span><span class="sxs-lookup"><span data-stu-id="713a5-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="713a5-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="713a5-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="713a5-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="713a5-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="713a5-121">Firefox 3.5 e superior</span><span class="sxs-lookup"><span data-stu-id="713a5-121">Firefox 3.5+</span></span>
* <span data-ttu-id="713a5-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="713a5-122">Chrome 4+</span></span>
* <span data-ttu-id="713a5-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="713a5-123">Safari 6+</span></span>
* <span data-ttu-id="713a5-124">Opera 12 e superior</span><span class="sxs-lookup"><span data-stu-id="713a5-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="713a5-125">Configurar o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="713a5-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="713a5-126">Escrever um script que cria um global `azureEngagement` objeto do JavaScript, como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="713a5-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="713a5-127">Pelo fato de que seu site pode ter várias páginas, este exemplo supõe que este script esteja incluído em cada página.</span><span class="sxs-lookup"><span data-stu-id="713a5-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="713a5-128">Neste exemplo, o objeto de JavaScript do hello é denominado `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="713a5-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="713a5-129">Olá `connectionString` valor para seu aplicativo é exibido no portal do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="713a5-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="713a5-130">`appVersionName` e `appVersionCode` são opcionais.</span><span class="sxs-lookup"><span data-stu-id="713a5-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="713a5-131">No entanto, é recomendável configurá-los para que a análise possa processar informações de versão.</span><span class="sxs-lookup"><span data-stu-id="713a5-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="713a5-132">Incluir scripts do Mobile Engagement em suas páginas</span><span class="sxs-lookup"><span data-stu-id="713a5-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="713a5-133">Adicione páginas do Mobile Engagement scripts tooyour em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="713a5-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="713a5-134">Ou assim:</span><span class="sxs-lookup"><span data-stu-id="713a5-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="713a5-135">Alias</span><span class="sxs-lookup"><span data-stu-id="713a5-135">Alias</span></span>
<span data-ttu-id="713a5-136">Depois de saudação script do SDK do Mobile Engagement da Web é carregada, cria Olá **contrato** tooaccess alias Olá APIs do SDK.</span><span class="sxs-lookup"><span data-stu-id="713a5-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="713a5-137">Você não pode usar essa configuração de SDK do alias toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="713a5-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="713a5-138">Esse alias é usado como uma referência nesta documentação.</span><span class="sxs-lookup"><span data-stu-id="713a5-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="713a5-139">Observe que se o alias do saudação padrão em conflito com outra variável global de sua página, você pode redefini-la na configuração Olá da seguinte maneira antes de carregar Olá Web SDK do Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="713a5-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="713a5-140">Relatórios básicos</span><span class="sxs-lookup"><span data-stu-id="713a5-140">Basic reporting</span></span>
<span data-ttu-id="713a5-141">Os relatórios básicos no Mobile Engagement abordam as estatísticas de nível de sessão, como estatísticas sobre usuários, sessões, atividades e falhas.</span><span class="sxs-lookup"><span data-stu-id="713a5-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="713a5-142">Rastreamento de sessão</span><span class="sxs-lookup"><span data-stu-id="713a5-142">Session tracking</span></span>
<span data-ttu-id="713a5-143">Uma sessão do Mobile Engagement é dividida em uma sequência de atividades, cada uma delas identificada por um nome.</span><span class="sxs-lookup"><span data-stu-id="713a5-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="713a5-144">Em um site clássico, é recomendável declarar uma atividade diferente em cada página do site.</span><span class="sxs-lookup"><span data-stu-id="713a5-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="713a5-145">Para um site ou aplicativo web no qual Olá página atual nunca muda, talvez você queira tootrack atividades de saudação em menor escala, como na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="713a5-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="713a5-146">Ou, toostart ou alterar hello atividade do usuário atual, chamada hello `engagement.agent.startActivity` função.</span><span class="sxs-lookup"><span data-stu-id="713a5-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="713a5-147">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="713a5-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="713a5-148">servidor do Mobile Engagement Olá automaticamente encerra uma sessão aberta em três minutos após a página de aplicativo hello está fechada.</span><span class="sxs-lookup"><span data-stu-id="713a5-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="713a5-149">Como alternativa, você pode encerrar uma sessão manualmente chamando `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="713a5-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="713a5-150">Isso define too'Idle de atividade de usuário atual do hello.'</span><span class="sxs-lookup"><span data-stu-id="713a5-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="713a5-151">sessão de saudação terminará 10 segundos mais tarde, a menos que uma nova chamada muito`engagement.agent.startActivity` retoma a sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="713a5-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="713a5-152">Você pode configurar o atraso de 10 segundos Olá no objeto de contrato global hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="713a5-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="713a5-153">Não é possível usar `engagement.agent.endActivity` em Olá `onunload` retorno de chamada porque você não pode fazer chamadas AJAX neste estágio.</span><span class="sxs-lookup"><span data-stu-id="713a5-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="713a5-154">Relatórios avançados</span><span class="sxs-lookup"><span data-stu-id="713a5-154">Advanced reporting</span></span>
<span data-ttu-id="713a5-155">Opcionalmente, se você quiser trabalhos, erros e eventos específicos de aplicativos de tooreport, você precisa toouse Olá Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="713a5-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="713a5-156">Você acessa Olá API do Mobile Engagement por meio de saudação `engagement.agent` objeto.</span><span class="sxs-lookup"><span data-stu-id="713a5-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="713a5-157">Você pode acessar todos Olá avançado de recursos do Mobile Engagement no hello Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="713a5-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="713a5-158">Olá API é detalhado no artigo Olá [como toouse Olá avançado marcação API em um aplicativo web do Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="713a5-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="713a5-159">Personalizar URLs Olá usadas para chamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="713a5-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="713a5-160">Você pode personalizar URLs que Olá que usa o SDK do Mobile Engagement da Web.</span><span class="sxs-lookup"><span data-stu-id="713a5-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="713a5-161">Por exemplo, tooredefine Olá log URL (Olá SDK ponto de extremidade para o log), você pode substituir a configuração de saudação assim:</span><span class="sxs-lookup"><span data-stu-id="713a5-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="713a5-162">Se suas funções de URL retornam uma cadeia de caracteres que começa com `/`, `//`, `http://`, ou `https://`, esquema de padrão de saudação não é usada.</span><span class="sxs-lookup"><span data-stu-id="713a5-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="713a5-163">Por padrão, Olá `https://` esquema é usada para as URLs.</span><span class="sxs-lookup"><span data-stu-id="713a5-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="713a5-164">Se desejar que o esquema padrão do toocustomize hello, substitua configuração hello, assim:</span><span class="sxs-lookup"><span data-stu-id="713a5-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
