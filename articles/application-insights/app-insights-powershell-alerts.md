---
title: aaaUse Powershell tooset alertas no Application Insights | Microsoft Docs
description: "Automatize a configuração de emails de tooget Application Insights sobre as alterações da métricas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Use o PowerShell tooset alertas no Application Insights
Você pode automatizar a configuração de saudação do [alertas](app-insights-alerts.md) na [Application Insights](app-insights-overview.md).

Além disso, você pode [definir webhooks tooautomate alerta tooan resposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Se você quiser recursos toocreate e alertas em Olá mesmo tempo, considere [usando um modelo do Azure Resource Manager](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Configuração única
Se você nunca usou o PowerShell com sua assinatura do Azure:

Instale o módulo de Powershell do Azure de saudação na máquina Olá onde deseja toorun Olá scripts.

* Instale o [Microsoft Web Platform Installer (v5 ou superior)](http://www.microsoft.com/web/downloads/platform.aspx).
* Use-tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>Conecte-se tooAzure
Inicie o PowerShell do Azure e [conectar assinatura tooyour](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Obter alertas
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Adicionar alerta
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Exemplo 1
Enviar email para mim se solicitações de tooHTTP de resposta do servidor de saudação, mais de 5 minutos, a média é menor do que 1 segundo. Meu recurso Application Insights é chamado IceCreamWebApp e está no grupo de recursos Fabrikam. Sou proprietário Olá Olá assinatura do Azure.

Olá GUID é o ID de assinatura de saudação (não Olá chave de instrumentação do aplicativo hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Exemplo 2
Tenho um aplicativo em que uso [Trackmetric](app-insights-api-custom-events-metrics.md#trackmetric) tooreport uma métrica denominada "salesPerHour". Envie um email toomy colegas se "salesPerHour" cair abaixo de 100, a média de mais de 24 horas.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

Olá mesma regra pode ser usada para a métrica de saudação relatadas usando Olá [parâmetro medida](app-insights-api-custom-events-metrics.md#properties) da chamada de outro controle como TrackEvent ou trackPageView.

## <a name="metric-names"></a>Nomes de métrica
| Nome da métrica | Nome da tela | Descrição |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Exceções de navegador |Contagem de exceções não capturadas lançadas no navegador de saudação. |
| `basicExceptionServer.count` |Exceções do servidor |Contagem de exceções sem tratamento lançadas pelo aplicativo hello |
| `clientPerformance.clientProcess.value` |Tempo de processamento do cliente |Tempo entre a recepção o último byte de um documento hello até Olá DOM ser carregado. As solicitações assíncronas ainda podem estar sendo processadas. |
| `clientPerformance.networkConnection.value` |Tempo de conexão de rede de carregamento de página |Navegador de saudação do tempo levará tooconnect toohello rede. Pode ser 0 se armazenado em cache. |
| `clientPerformance.receiveRequest.value` |Tempo de resposta de recebimento |Tempo entre enviar solicitação toostarting tooreceive resposta do navegador. |
| `clientPerformance.sendRequest.value` |Tempo de solicitação de envio |Tempo levado pela solicitação de toosend do navegador. |
| `clientPerformance.total.value` |Tempo de carregamento de página do navegador |Tempo de solicitação do usuário até que o DOM, as imagens, os scripts e as folhas de estilo sejam carregados. |
| `performanceCounter.available_bytes.value` |Memória disponível |Memória física disponível imediatamente para um processo ou para uso do sistema. |
| `performanceCounter.io_data_bytes_per_sec.value` |Taxa de processamento de IO |Total de bytes por segundo de leitura e escrita toofiles, redes e dispositivos. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |taxa de exceção |Exceções geradas por segundo. |
| `performanceCounter.percentage_processor_time.value` |CPU do processo |Porcentagem de saudação do tempo decorrido de todos os threads de processo usado por instruções de tooexecution Olá processador no processo de aplicativos de saudação. |
| `performanceCounter.percentage_processor_total.value` |Tempo do processador |Porcentagem de saudação do tempo Olá processador gasta em threads não ociosos. |
| `performanceCounter.process_private_bytes.value` |Processar bytes particulares |Memória atribuída exclusivamente toohello monitorados processos do aplicativo. |
| `performanceCounter.request_execution_time.value` |Tempo de execução de solicitação do ASP.NET |Tempo de execução da solicitação mais recente hello. |
| `performanceCounter.requests_in_application_queue.value` |Solicitações do ASP.NET na fila de execução |Comprimento da fila de solicitações de aplicativo hello. |
| `performanceCounter.requests_per_sec.value` |Taxa de solicitação do ASP.NET |Taxa de todas as solicitações de aplicativo toohello por segundo do ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Falhas de dependência |Contagem de chamadas com falha feitas pelos recursos de tooexternal de aplicativos de servidor de saudação. |
| `request.duration` |Tempo de resposta do servidor |Tempo entre a receber uma solicitação HTTP e a conclusão do envio Olá resposta. |
| `request.rate` |Taxa de solicitação |Taxa de todas as solicitações de aplicativo toohello por segundo. |
| `requestFailed.count` |Solicitações falhas |Contagem de solicitações HTTP que resultaram em um código de resposta >= 400 |
| `view.count` |Visualizações de página |Contagem de solicitações de usuário  cliente para uma página da Web. O tráfego sintético é filtrado. |
| {o nome de métrica personalizada} |{O nome da métrica} |O valor de métrica relatado por [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) ou em Olá [parâmetro medidas de uma chamada de controle](app-insights-api-custom-events-metrics.md#properties). |

métricas de saudação são enviadas por módulos de telemetria diferentes:

| Grupo de métricas | Módulo de coletor |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>view |[JavaScript do navegador](app-insights-javascript.md) |
| performanceCounter |[Desempenho](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Dependência](app-insights-configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[Solicitação do servidor](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhooks
Você pode [automatizar o alerta de tooan resposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md). O Azure ligará para um endereço web de sua escolha quando um alerta for gerado.

## <a name="see-also"></a>Consulte também
* [Script tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Criar recursos de teste da Web e do Application Insights por meio de modelos](app-insights-powershell.md)
* [Automatizar a combinação de diagnóstico do Microsoft Azure tooApplication Insights](app-insights-powershell-azure-diagnostics.md)
* [Automatizar o alerta de tooan de resposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
