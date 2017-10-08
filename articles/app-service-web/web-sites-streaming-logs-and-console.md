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
# <a name="streaming-logs-and-hello-console"></a>Os Logs de streaming e hello Console
## <a name="streaming-logs"></a>Logs de streaming
Olá **portal do Azure** fornece um visualizador de log de streaming integrado que permite que você exiba os eventos de rastreamento de seu **do serviço de aplicativo** aplicativos em tempo real.  

A configuração desse recurso exige algumas etapas simples:

* Escrever rastreamentos no código
* Habilitar os **Logs de Diagnóstico** para seu aplicativo
* Fluxo de saudação de exibição de internas Olá **Logs de Streaming** UI de saudação **portal do Azure**.

### <a name="how-toowrite-traces-in-your-code"></a>Como toowrite rastreamentos em seu código
É fácil escrever rastreamentos no código.  No c# é tão fácil quanto escrever Olá código a seguir:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Olá classe Trace reside no namespace System Diagnostics hello.

Em um aplicativo Node. js, você pode escrever este código tooachieve Olá mesmo resultado:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Como tooenable e exibição Olá logs de streaming
Os Diagnósticos do ![][BrowseSitesScreenshot] são habilitados de acordo com cada aplicativo. Comece procurando toohello site você gostaria que tooenable esse recurso no.  

![][DiagnosticsLogs]No menu de configurações, role para baixo toohello **monitoramento** seção e clique em **(1) Logs de diagnóstico**. Em seguida, **enable (2)** **(sistema de arquivos) de log de aplicativo** ou **(blob) de log de aplicativo** Olá **nível** opção permite que você altere Olá nível de severidade de toocapture rastreamentos. Se você estiver apenas tentando tooget familiarizado com o recurso de hello, definir nível de saudação muito**detalhado** tooensure todas as instruções de rastreamento são coletadas.

Clique em **salvar** na parte superior de saudação da folha de saudação e você estiver pronto tooview logs.

> [!NOTE]
> Olá Olá superior **nível de severidade** hello mais recursos são consumido toolog e hello mais rastreamentos são produzidos. Certifique-se de **nível de severidade** é toohello configurado o detalhamento correto para uma produção ou um site de alto tráfego. 
> 
> 

![][StreamingLogsScreenshot]Olá tooview **os logs de streaming** em Olá portal do Azure, clique em **fluxo de Log (1)** também em Olá **monitoramento** seção do menu de configurações de saudação. Se seu aplicativo ativamente está gravando instruções de rastreamento, você deverá vê-los no hello **logs de streaming (2) da interface do usuário** quase em tempo real.

## <a name="console"></a>Console
Olá **portal do Azure** fornece ao aplicativo de tooyour de acesso de console. É possível explorar o sistema de arquivos do aplicativo e executar scripts powershell/cmd. São vinculados por Olá mesmas permissões definidas como o código do aplicativo em execução durante a execução de comandos do console. Acessar os diretórios tooprotected ou execução de scripts que exige permissões elevadas está bloqueada.  

![][ConsoleScreenshot]No menu de configurações, role para baixo demais**ferramentas de desenvolvimento** seção e clique em **(1) o Console** e hello **(2) o console** UI abre toohello direita.

tooget familiarizado com hello **console**, tente comandos básicos, como:

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
