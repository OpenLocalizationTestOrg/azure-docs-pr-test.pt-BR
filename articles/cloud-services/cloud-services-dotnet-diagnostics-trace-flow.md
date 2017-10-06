---
title: "aaaTrace Olá fluxo em um aplicativo de serviços de nuvem com o diagnóstico do Azure | Microsoft Docs"
description: "Adicione a depuração do aplicativo do Azure toohelp do rastreamento mensagens tooan, medir o desempenho, monitoramento, análise de tráfego e muito mais."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Fluxo de saudação do rastreamento de um aplicativo de serviços de nuvem com o diagnóstico do Azure
O rastreamento é uma maneira de você toomonitor Olá execução de seu aplicativo enquanto ele está em execução. Você pode usar o hello [Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), e [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord informações sobre erros e execução do aplicativo em logs, arquivos de texto ou outros dispositivos para análise posterior. Para obter mais informações sobre rastreamento, consulte [Rastreamento e instrumentação de aplicativos](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>Usar instruções e opções de rastreamento
Rastreamento de implementar em seu aplicativo de serviços de nuvem adicionando Olá [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configuração de aplicativo e fazer chamadas tooSystem.Diagnostics.Trace ou debug no seu código do aplicativo. Usar arquivo de configuração de saudação *App. config* para funções de trabalho e hello *Web. config* para funções da web. Quando você cria um novo serviço hospedado usando um modelo do Visual Studio, o diagnóstico do Azure é adicionado automaticamente toohello projeto e Olá DiagnosticMonitorTraceListener é adicionado toohello o arquivo de configuração apropriado para as funções hello que você adicionar.

Para obter informações sobre a inserção de instruções de rastreamento, consulte [como: adicionar instruções de rastreamento tooApplication código](https://msdn.microsoft.com/library/zd83saa2.aspx).

Incluindo [Opções de Rastreamento](https://msdn.microsoft.com/library/3at424ac.aspx) em seu código, você pode controlar se o rastreamento ocorre e qual a sua extensão. Isso lhe permite monitorar o status de saudação do seu aplicativo em um ambiente de produção. Isso é particularmente importante em um aplicativo de negócios que usa vários componentes executados em vários computadores. Para obter mais informações, consulte [Como: configurar opções de rastreamento](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Configurar o ouvinte de rastreamento de saudação em um aplicativo do Azure
Rastreamento, depuração e TraceSource, exigem que você configure "ouvintes" toocollect e mensagens de saudação do registro que são enviadas. Os ouvintes coletam, armazenam e roteiam mensagens de rastreamento. Eles direcionam Olá rastreamento saída tooan destino apropriado, como um log, uma janela ou um arquivo de texto. Diagnóstico do Azure usa Olá [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) classe.

Antes de concluir Olá procedimento a seguir, você deverá inicializar Olá monitor de diagnóstico do Azure. toodo isso, consulte [habilitando o diagnóstico no Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Observe que se você usar modelos de saudação que são fornecidos pelo Visual Studio, configuração de saudação do ouvinte de saudação é adicionada automaticamente para você.

### <a name="add-a-trace-listener"></a>Adicionar um ouvinte de rastreamento
1. Abra o arquivo Web. config ou App. config Olá para sua função.
2. Adicione Olá arquivo toohello de código a seguir. Altere Olá atributo toouse Olá versão número de versão do assembly hello que fazem referência. versão do assembly Hello não altera necessariamente com cada versão do SDK do Azure, a menos que há atualizações tooit.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Verifique se que você tem uma referência de projeto toohello Microsoft.WindowsAzure.Diagnostics assembly. Número de versão de hello atualização no xml de saudação acima toomatch versão Olá Olá referenciado Microsoft.WindowsAzure.Diagnostics assembly.
   > 
   > 
3. Salve o arquivo de configuração de saudação.

Para obter mais informações sobre ouvintes, veja [Ouvintes de rastreamento](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Depois de concluir o ouvinte de Olá Olá etapas tooadd, você pode adicionar código de tooyour de instruções de rastreamento.

### <a name="tooadd-trace-statement-tooyour-code"></a>código de tooyour de instrução de rastreamento tooadd
1. Abra um arquivo de origem para o aplicativo. Por exemplo, Olá <RoleName>arquivo. cs para a função de trabalho de saudação ou função web.
2. Adicione o seguinte Olá usando a instrução se ele já não tiver sido adicionado:
    ```
        using System.Diagnostics;
    ```
3. Adicione instruções de rastreamento onde você deseja toocapture informações sobre o estado de saudação do seu aplicativo. Você pode usar uma variedade de métodos tooformat Olá saída Olá demonstrativo de rastreamento. Para obter mais informações, consulte [como: adicionar instruções de rastreamento tooApplication código](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Salve o arquivo de origem de saudação.

