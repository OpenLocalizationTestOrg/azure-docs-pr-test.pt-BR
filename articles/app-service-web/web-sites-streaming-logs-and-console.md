---
title: logs de aaaStreaming e console
description: "Logs de streaming e visão geral do console"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="3ade5-103">Os Logs de streaming e hello Console</span><span class="sxs-lookup"><span data-stu-id="3ade5-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="3ade5-104">Logs de streaming</span><span class="sxs-lookup"><span data-stu-id="3ade5-104">Streaming Logs</span></span>
<span data-ttu-id="3ade5-105">Olá **portal do Azure** fornece um visualizador de log de streaming integrado que permite que você exiba os eventos de rastreamento de seu **do serviço de aplicativo** aplicativos em tempo real.</span><span class="sxs-lookup"><span data-stu-id="3ade5-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="3ade5-106">A configuração desse recurso exige algumas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="3ade5-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="3ade5-107">Escrever rastreamentos no código</span><span class="sxs-lookup"><span data-stu-id="3ade5-107">Write traces in your code</span></span>
* <span data-ttu-id="3ade5-108">Habilitar os **Logs de Diagnóstico** para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3ade5-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="3ade5-109">Fluxo de saudação de exibição de internas Olá **Logs de Streaming** UI de saudação **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3ade5-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="3ade5-110">Como toowrite rastreamentos em seu código</span><span class="sxs-lookup"><span data-stu-id="3ade5-110">How toowrite traces in your code</span></span>
<span data-ttu-id="3ade5-111">É fácil escrever rastreamentos no código.</span><span class="sxs-lookup"><span data-stu-id="3ade5-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="3ade5-112">No c# é tão fácil quanto escrever Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ade5-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="3ade5-113">Olá classe Trace reside no namespace System Diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="3ade5-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="3ade5-114">Em um aplicativo Node. js, você pode escrever este código tooachieve Olá mesmo resultado:</span><span class="sxs-lookup"><span data-stu-id="3ade5-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="3ade5-115">Como tooenable e exibição Olá logs de streaming</span><span class="sxs-lookup"><span data-stu-id="3ade5-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="3ade5-116">Os Diagnósticos do ![][BrowseSitesScreenshot] são habilitados de acordo com cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ade5-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="3ade5-117">Comece procurando toohello site você gostaria que tooenable esse recurso no.</span><span class="sxs-lookup"><span data-stu-id="3ade5-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="3ade5-118">![][DiagnosticsLogs]No menu de configurações, role para baixo toohello **monitoramento** seção e clique em **(1) Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="3ade5-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="3ade5-119">Em seguida, **enable (2)** **(sistema de arquivos) de log de aplicativo** ou **(blob) de log de aplicativo** Olá **nível** opção permite que você altere Olá nível de severidade de toocapture rastreamentos.</span><span class="sxs-lookup"><span data-stu-id="3ade5-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="3ade5-120">Se você estiver apenas tentando tooget familiarizado com o recurso de hello, definir nível de saudação muito**detalhado** tooensure todas as instruções de rastreamento são coletadas.</span><span class="sxs-lookup"><span data-stu-id="3ade5-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="3ade5-121">Clique em **salvar** na parte superior de saudação da folha de saudação e você estiver pronto tooview logs.</span><span class="sxs-lookup"><span data-stu-id="3ade5-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="3ade5-122">Olá Olá superior **nível de severidade** hello mais recursos são consumido toolog e hello mais rastreamentos são produzidos.</span><span class="sxs-lookup"><span data-stu-id="3ade5-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="3ade5-123">Certifique-se de **nível de severidade** é toohello configurado o detalhamento correto para uma produção ou um site de alto tráfego.</span><span class="sxs-lookup"><span data-stu-id="3ade5-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="3ade5-124">![][StreamingLogsScreenshot]Olá tooview **os logs de streaming** em Olá portal do Azure, clique em **fluxo de Log (1)** também em Olá **monitoramento** seção do menu de configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ade5-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="3ade5-125">Se seu aplicativo ativamente está gravando instruções de rastreamento, você deverá vê-los no hello **logs de streaming (2) da interface do usuário** quase em tempo real.</span><span class="sxs-lookup"><span data-stu-id="3ade5-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="3ade5-126">Console</span><span class="sxs-lookup"><span data-stu-id="3ade5-126">Console</span></span>
<span data-ttu-id="3ade5-127">Olá **portal do Azure** fornece ao aplicativo de tooyour de acesso de console.</span><span class="sxs-lookup"><span data-stu-id="3ade5-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="3ade5-128">É possível explorar o sistema de arquivos do aplicativo e executar scripts powershell/cmd.</span><span class="sxs-lookup"><span data-stu-id="3ade5-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="3ade5-129">São vinculados por Olá mesmas permissões definidas como o código do aplicativo em execução durante a execução de comandos do console.</span><span class="sxs-lookup"><span data-stu-id="3ade5-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="3ade5-130">Acessar os diretórios tooprotected ou execução de scripts que exige permissões elevadas está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="3ade5-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="3ade5-131">![][ConsoleScreenshot]No menu de configurações, role para baixo demais**ferramentas de desenvolvimento** seção e clique em **(1) o Console** e hello **(2) o console** UI abre toohello direita.</span><span class="sxs-lookup"><span data-stu-id="3ade5-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="3ade5-132">tooget familiarizado com hello **console**, tente comandos básicos, como:</span><span class="sxs-lookup"><span data-stu-id="3ade5-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
