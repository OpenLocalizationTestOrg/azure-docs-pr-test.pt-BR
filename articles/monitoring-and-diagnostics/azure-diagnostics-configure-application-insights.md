---
title: "aaaConfigure diagnóstico do Azure toosend dados tooApplication Insights | Microsoft Docs"
description: "Atualize Olá diagnóstico do Azure configuração pública toosend dados tooApplication Insights."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Enviar dados de diagnóstico de serviço de nuvem, Máquina Virtual ou do Service Fabric tooApplication Insights
Serviços de nuvem, máquinas virtuais, conjuntos de escala de máquinas virtuais e Service Fabric saudação de uso de todos os dados de toocollect de extensão de diagnóstico do Azure.  Diagnóstico do Azure envia dados tooAzure tabelas de armazenamento.  No entanto, você também pode pipe todos ou um subconjunto Olá tooother de locais de dados usando a extensão de diagnóstico do Azure 1.5 ou posterior.

Este artigo descreve como dados toosend Olá tooApplication de extensão de diagnóstico do Azure Insights.

## <a name="diagnostics-configuration-explained"></a>Explicação da configuração do Diagnóstico
Olá Coletores de extensão 1.5 introduzida o diagnóstico do Azure, que são locais adicionais, onde você pode enviar dados de diagnóstico.

Exemplo de configuração de um coletor para o Application Insights:

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- Olá **coletor** *nome* atributo é um valor de cadeia de caracteres que identifica exclusivamente o coletor de saudação.

- Olá **ApplicationInsights** elemento Especifica a chave de instrumentação da saudação onde Olá dados de diagnóstico do Azure é enviado do recurso do Application insights.
    - Se você não tiver um recurso existente do Application Insights, consulte [criar um novo recurso do Application Insights](../application-insights/app-insights-create-new-resource.md) para obter mais informações sobre como criar um recurso e obter a chave de instrumentação hello.
    - Se você estiver desenvolvendo um Serviço de Nuvem com o Azure SDK 2.8 e posterior, essa chave de instrumentação é preenchida automaticamente. valor Olá baseia-se a saudação **APPINSIGHTS_INSTRUMENTATIONKEY** configuração de serviço ao empacotar um projeto de serviço de nuvem hello. Consulte [problemas de serviço de nuvem Use Application Insights com o diagnóstico do Azure tootroubleshoot](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Olá **canais** elemento contém um ou mais **Channel** elementos.
    - Olá *nome* exclusivamente refere-se o atributo toothat canal.
    - Olá *loglevel* atributo permite que você especifique o nível de log Olá Olá canal permite. Olá níveis de log disponíveis na ordem da maioria das informações de tooleast são:
        - Detalhado
        - Informações
        - Aviso
        - Erro
        - Crítico

Um canal atua como um filtro e permite que você tooselect log específico níveis toosend toohello destino coletor. Por exemplo, você pode coletar logs detalhados e enviá-los toostorage, mas enviar somente coletor de toohello de erros.

Olá gráfico a seguir mostra essa relação.

![Configuração pública do Diagnóstico](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Olá gráfico a seguir resume os valores de configuração hello e como elas funcionam. Você pode incluir vários coletores na configuração de saudação em diferentes níveis na hierarquia de saudação. Olá coletor no nível superior Olá atua como uma configuração global e hello um especificado em Olá individual elemento age como uma configuração global de toothat de substituição.

![Configuração dos coletores de diagnóstico com o Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Exemplo de configuração completa do coletor
Aqui está um exemplo completo de configuração pública Olá arquivo
1. envia todos os erros tooApplication Insights (especificado no hello **DiagnosticMonitorConfiguration** nó)
2. também envia logs detalhados de nível para Olá Logs de aplicativo (especificado no hello **Logs** nó).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
Configuração anterior do hello, Olá linhas a seguir têm Olá significados a seguir:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Enviar todos os dados de saudação que estão sendo coletados pelo diagnóstico do Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Enviar somente logs toohello Application Insights coletor de erros

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Enviar logs de aplicativo detalhado tooApplication Insights

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Limitações

- **Os canais só registro o tipo e não contadores de desempenho.** Se você especificar um canal com um elemento contador de desempenho, ele será ignorado.
- **nível de log Olá para um canal não pode exceder o nível de log Olá para o que está sendo coletado pelo diagnóstico do Azure.** Por exemplo, você não pode coletar erros do Log de aplicativo no elemento de Logs hello e tente toosend logs detalhados toohello Application Insight coletor. Olá *scheduledTransferLogLevelFilter* atributo sempre deve coletar igual ou mais logs de saudação logs que você estão tentando toosend tooa coletor.
- **Você não pode enviar dados blob coletados pelo diagnóstico do Azure extensão tooApplication Insights.** Por exemplo, nada especificado em Olá *diretórios* nó. Despejos de memória Olá real despejo de memória é enviado tooblob armazenamento e apenas uma notificação que Olá despejo de memória foi gerada é enviada tooApplication Insights.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[exibir suas informações de diagnóstico do Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) no Application Insights.
* Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable Olá extensão de diagnóstico do Azure para seu aplicativo.
* Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable Olá extensão de diagnóstico do Azure para seu aplicativo
