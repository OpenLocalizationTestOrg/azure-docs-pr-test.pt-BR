---
title: "aaaMonitoring funções do Azure | Microsoft Docs"
description: "Saiba como toomonitor as funções do Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Monitoramento do Azure Functions

## <a name="overview"></a>Visão geral 


Olá **Monitor** guia para cada função permite que você tooreview cada execução de uma função.

![guia Monitorar do Azure Functions](./media/functions-monitoring/monitor-tab.png) 

Clicando em uma execução permite que você tooreview Olá duração, dados de entrada, erros e arquivos de log associados. Tudo isso é útil na depuração e no ajuste de desempenho de suas funções.


> [!IMPORTANT]
> Ao usar o hello [consumo de plano de hospedagem](functions-overview.md#pricing) para funções do Azure, Olá **monitoramento** lado a lado na folha de visão geral do aplicativo de função hello não mostrarão nenhum dado. Isso ocorre porque a plataforma de saudação dimensiona dinamicamente e gerencia instâncias de computação, portanto, essas métricas não são significativas em um plano de consumo. uso de saudação toomonitor de seus aplicativos de função, você deve usar em vez disso, as diretrizes de Olá neste artigo.
> 
> Olá captura de tela a seguir mostra um exemplo:
> 
> ![Monitoramento na folha de recursos principais de saudação](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Monitoramento em tempo real

Para acessar o monitoramento em tempo real, clique na **transmissão de evento ao vivo**, como mostrado abaixo. 

![Opção de fluxo de evento para o guia do monitor de saudação de Live](./media/functions-monitoring/monitor-tab-live-event-stream.png)

fluxo de evento ao vivo Hello serão colocados no gráfico em uma nova guia do navegador conforme mostrado abaixo. 

![Exemplo de transmissão de evento ao vivo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Há um problema conhecido que pode fazer com que seu toobe de toofail dados preenchido. Se você enfrentar isso, talvez seja necessário tooclose Olá navegador guia contendo Olá ao vivo fluxo de eventos e clique **fluxo de evento ao vivo** novamente tooallow-tooproperly popular com seus dados de fluxo de evento. 

fluxo de evento ao vivo Hello serão graph Olá estatísticas para a função a seguir:

* Execuções iniciadas por segundo
* Execuções concluídas por segundo
* Execuções com falha por segundo
* Tempo médio de execução em milissegundos.

Essas estatísticas são em tempo real, mas Olá real de gráficos de dados de execução Olá pode ter cerca de 10 segundos de latência.






## <a name="monitoring-log-files-from-a-command-line"></a>Monitoramento de arquivos de log de uma linha de comando


Você pode transmitir uma sessão de linha de comando de tooa de arquivos de log em uma estação de trabalho local usando hello Azure Interface de linha de comando (CLI) ou o PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Monitoramento de arquivos de log de aplicativo de função com hello CLI do Azure

tooget iniciado, [instalar Olá CLI do Azure](../cli-install-nodejs.md)

Efetue login em sua conta do Azure usando os seguintes Olá comando ou qualquer Olá outras opções abordadas, [login tooAzure de saudação CLI do Azure](../xplat-cli-connect.md).

    azure login

Modo de gerenciamento de serviço de CLI do Azure (ASM) tooenable do comando de uso a seguir de saudação:.

    azure config mode asm

Se você tiver várias assinaturas, use Olá toolist comandos a seguir, suas assinaturas e o conjunto Olá assinatura toohello assinatura atual que contém seu aplicativo de função.

    azure account list
    azure account set <subscriptionNameOrId>

Olá comando a seguir será de fluxo de arquivos de log Olá sua função aplicativo toohello da linha de comando:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Monitoramento de arquivos de log do aplicativo de funções com o PowerShell

tooget iniciado, [instalar e configurar o Azure PowerShell](/powershell/azure/overview).

Adicione sua conta do Azure executando Olá comando a seguir:

    PS C:\> Add-AzureAccount

Se você tiver várias assinaturas, você pode listá-los por nome com hello toosee de comando a seguir se Olá correto de assinatura é hello atualmente selecionado com base em `IsCurrent` propriedade:

    PS C:\> Get-AzureSubscription

Se você precisar tooset Olá assinatura ativa toohello uma que contém seu aplicativo de função, use Olá comando a seguir:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Fluxo de sessão do PowerShell Olá logs tooyour com hello comando a seguir:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Para obter mais informações, consulte muito[como: fluxo de logs para aplicativos web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir:

* [Testando uma função](functions-test-a-function.md)
* [Dimensionar uma função](functions-scale.md)

