---
title: Logs de streaming e console
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="bb500-103">Logs de streaming e o console</span><span class="sxs-lookup"><span data-stu-id="bb500-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="bb500-104">Logs de streaming</span><span class="sxs-lookup"><span data-stu-id="bb500-104">Streaming Logs</span></span>
<span data-ttu-id="bb500-105">O **portal do Azure** fornece um visualizador de log de streaming integrado que permite exibir os eventos de rastreamento de aplicativos do **Serviço de Aplicativo** em tempo real.</span><span class="sxs-lookup"><span data-stu-id="bb500-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="bb500-106">A configuração desse recurso exige algumas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="bb500-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="bb500-107">Escrever rastreamentos no código</span><span class="sxs-lookup"><span data-stu-id="bb500-107">Write traces in your code</span></span>
* <span data-ttu-id="bb500-108">Habilitar os **Logs de Diagnóstico** para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="bb500-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="bb500-109">Exiba a transmissão da interface de usuário interna **Logs de Streaming** no **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bb500-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="bb500-110">Como escrever rastreamentos no código</span><span class="sxs-lookup"><span data-stu-id="bb500-110">How to write traces in your code</span></span>
<span data-ttu-id="bb500-111">É fácil escrever rastreamentos no código.</span><span class="sxs-lookup"><span data-stu-id="bb500-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="bb500-112">No C#, é tão fácil quanto escrever o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="bb500-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="bb500-113">A classe de rastreamento está no namespace System. Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="bb500-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="bb500-114">Em um aplicativo node.js, você pode escrever esse código para obter o mesmo resultado:</span><span class="sxs-lookup"><span data-stu-id="bb500-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="bb500-115">Como habilitar e exibir os logs de streaming</span><span class="sxs-lookup"><span data-stu-id="bb500-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="bb500-116">Os Diagnósticos do ![][BrowseSitesScreenshot] são habilitados de acordo com cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb500-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="bb500-117">Comece navegando até o site em que deseja habilitar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bb500-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="bb500-118">![][DiagnosticsLogs] No menu de configurações, role para baixo até a seção **Monitoramento** e clique em **(1) Logs de Diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="bb500-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="bb500-119">Em seguida, **(2) habilite** **Log de Aplicativo (Filesystem)** ou **Log de Aplicativo (blob)** A opção **Nível** permite alterar o nível de severidade dos rastreamentos a serem capturados.</span><span class="sxs-lookup"><span data-stu-id="bb500-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="bb500-120">Se estiver apenas tentando se familiarizar com o recurso, defina o nível para **Detalhado** a fim de garantir que todos os demonstrativos de rastreamento sejam coletados.</span><span class="sxs-lookup"><span data-stu-id="bb500-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="bb500-121">Clique em **SALVAR** na parte superior da lâmina, e você está pronto para exibir logs.</span><span class="sxs-lookup"><span data-stu-id="bb500-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="bb500-122">Quanto mais alto o **nível de severidade**, mais recursos serão consumidos para registro e mais rastreamentos serão produzidos.</span><span class="sxs-lookup"><span data-stu-id="bb500-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="bb500-123">Certifique-se de que o **nível de severidade** esteja configurado com o detalhamento correto para um site de produção ou tráfego alto.</span><span class="sxs-lookup"><span data-stu-id="bb500-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="bb500-124">![][StreamingLogsScreenshot] Para exibir os **logs de streaming** de dentro do portal do Azure, clique em **(1) Fluxo de Log** também na seção **Monitoramento** do menu de configurações.</span><span class="sxs-lookup"><span data-stu-id="bb500-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="bb500-125">Se o aplicativo estiver gravando ativamente os demonstrativos de rastreamento, você deverá vê-los na **(2) interface de usuário Logs de Streaming** quase em tempo real.</span><span class="sxs-lookup"><span data-stu-id="bb500-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="bb500-126">Console</span><span class="sxs-lookup"><span data-stu-id="bb500-126">Console</span></span>
<span data-ttu-id="bb500-127">O **portal do Azure** fornece ao console acesso ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb500-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="bb500-128">É possível explorar o sistema de arquivos do aplicativo e executar scripts powershell/cmd.</span><span class="sxs-lookup"><span data-stu-id="bb500-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="bb500-129">Você é vinculado pelas mesmas permissões definidas que seu código de aplicativo em execução ao executar comandos do console.</span><span class="sxs-lookup"><span data-stu-id="bb500-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="bb500-130">O acesso a diretórios protegidos ou a execução de scripts que exigem permissões elevadas é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="bb500-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="bb500-131">![][ConsoleScreenshot] No menu de configurações, role para baixo até a seção **Ferramentas de Desenvolvimento** e clique em **(1) Console**, e a interface de usuário **(2) Console** será aberta à direita.</span><span class="sxs-lookup"><span data-stu-id="bb500-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="bb500-132">Para se familiarizar com o **console**, tente comandos básicos como:</span><span class="sxs-lookup"><span data-stu-id="bb500-132">To get familiar with the **console**, try basic commands like:</span></span>

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
