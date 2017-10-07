---
title: "aaaCollect e analisar os logs de eventos do Windows na análise de Log do OMS | Microsoft Docs"
description: "Logs de eventos do Windows são uma das fontes de dados mais comuns Olá usados pela análise de Log.  Este artigo descreve como tooconfigure coleta de logs de eventos do Windows e os detalhes de registros de saudação criado no repositório do OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Fontes de dados de log de eventos do Windows no Log Analytics
Logs de eventos do Windows são um dos mais comuns de saudação [fontes de dados](log-analytics-data-sources.md) para coletar dados usando agentes do Windows, pois muitos aplicativos de gravar o log de eventos do Windows toohello.  Você pode coletar eventos de logs padrão como o aplicativo e de sistema na adição toospecifying quaisquer logs personalizados criados por aplicativos, você precisa toomonitor.

![Eventos do Windows](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configurando os logs de eventos do Windows
Configurar logs de eventos do Windows da saudação [menu dados nas configurações de análise de Log](log-analytics-data-sources.md#configuring-data-sources).

Análise de log coleta somente eventos dos logs de eventos do Windows hello são especificadas nas configurações de saudação.  Você pode adicionar um log de eventos digitando o nome de saudação do log hello e clicando em  **+** .  Para cada log, apenas os eventos Olá com severidades de saudação selecionada são coletados.  Verifique severidades Olá para que você deseja toocollect determinado log de saudação.  Você não pode fornecer eventos toofilter quaisquer critérios adicionais.

Conforme você digita o nome de saudação de um log de eventos, análise de Log fornece sugestões de nomes comuns do log de eventos. Se log Olá tooadd você deseja não aparecer na lista de saudação, você ainda poderá adicioná-lo, digitando Olá o nome completo do log de saudação. Você pode encontrar o nome completo de saudação do log hello usando o Visualizador de eventos. No Visualizador de eventos, abra Olá *propriedades* página Olá log e cópia Olá cadeia de caracteres de saudação *nome completo* campo.

![Configurar eventos do Windows](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Coleta de dados
Análise de log coleta cada evento que corresponde a uma severidade selecionada de um log de eventos monitorado como Olá evento será criado.  agente Olá registra seu lugar em cada log de eventos de coleta.  Se agente Olá ficar offline por um período de tempo, em seguida, análise de Log coleta eventos de onde parou, mesmo se os eventos foram criados durante a saudação agent estava offline.  Há um potencial para toonot esses eventos coletados se o log de eventos Olá encapsula com eventos não coletados sendo substituídos enquanto o agente hello está offline.

>[!NOTE]
>Análise de log não coleta eventos de auditoria criados pelo SQL Server de origem *MSSQLSERVER* com a ID de evento 18453 que contém as palavras-chave - *clássico* ou *sucesso de auditoria* e palavra-chave *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Propriedades de registros de eventos do Windows
Registros de eventos do Windows têm um tipo de **evento** e têm propriedades de saudação em Olá a tabela a seguir:

| Propriedade | Descrição |
|:--- |:--- |
| Computador |Nome do computador Olá Olá evento foi coletado do. |
| EventCategory |Categoria de evento de saudação. |
| EventData |Todos os dados de evento em formato bruto. |
| EventID |Número de eventos de saudação. |
| EventLevel |Severidade do evento de saudação no formato numérico. |
| EventLevelName |Severidade do evento de saudação em formato de texto. |
| EventLog |Nome do log de eventos de saudação que Olá evento foi coletado do. |
| ParameterXml |Valores de parâmetro de evento em formato XML. |
| ManagementGroupName |Nome do grupo de gerenciamento de saudação para agentes do System Center Operations Manager.  Para outros agentes, esse valor é AOI-<workspace ID> |
| RenderedDescription |Descrição do evento com valores de parâmetro |
| Fonte |Origem do evento de saudação. |
| SourceSystem |Tipo de evento de saudação do agente foi coletado do. <br> OpsManager - agente do Windows: conexão direta ou Operations Manager gerenciado <br> Linux: todos os agentes do Linux  <br> AzureStorage: Diagnóstico do Azure |
| TimeGenerated |Evento de saudação de data e hora foi criado no Windows. |
| UserName |Nome de usuário da conta de saudação que registrou o evento de saudação. |

## <a name="log-searches-with-windows-events"></a>Pesquisas de log com eventos do Windows
Olá, tabela a seguir fornece exemplos de diferentes de pesquisas de log para recuperar os registros de eventos do Windows.

| Consultar | Descrição |
|:--- |:--- |
| Type=Event |Todos os eventos do Windows. |
| Type=Event EventLevelName=error |Todos os eventos do Windows com severidade de erro. |
| Type=Event &#124; Measure count() by Source |Contagem de eventos do Windows por fonte. |
| Type=Event EventLevelName=error &#124; Measure count() by Source |Contagem de eventos de erro do Windows por fonte. |


>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir.
>
>| Consultar | Descrição |
|:---|:---|
| Evento |Todos os eventos do Windows. |
| Event &#124; where EventLevelName == "error" |Todos os eventos do Windows com severidade de erro. |
| Event &#124; summarize count() by Source |Contagem de eventos do Windows por fonte. |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |Contagem de eventos de erro do Windows por fonte. |


## <a name="next-steps"></a>Próximas etapas
* Configurar análise de Log toocollect outros [fontes de dados](log-analytics-data-sources.md) para análise.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.  
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse registros de eventos de saudação em campos individuais.
* Configure a [coleta de contadores de desempenho](log-analytics-data-sources-performance-counters.md) de seus agentes do Windows.
