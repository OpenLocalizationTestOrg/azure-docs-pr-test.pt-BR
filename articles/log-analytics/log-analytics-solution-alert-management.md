---
title: "aaaAlert a solução de gerenciamento no OMS Operations Management Suite () | Microsoft Docs"
description: "saudação de solução de gerenciamento de alertas na análise de Log ajuda a analisar todos os alertas de saudação em seu ambiente.  Tooconsolidating de adição alertas gerados no OMS, ele importa alertas de grupos de gerenciamento conectados do System Center Operations Manager para análise de Log."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Solução Gerenciamento de Alertas no OMS (Operations Management Suite)

![Ícone do Gerenciamento de Alertas](media/log-analytics-solution-alert-management/icon.png)

saudação de solução de gerenciamento de alertas ajuda você a analisar todos os alertas de saudação do seu repositório de análise de Log.  Esses alertas podem ser provenientes de várias origens, incluindo aquelas [criadas pelo Log Analytics](log-analytics-alerts.md) ou [importadas do Nagios ou do Zabbix](log-analytics-linux-agents.md).  Olá solução também importa alertas de qualquer [grupos de gerenciamento do System Center Operations Manager conectado](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Pré-requisitos
solução de saudação funciona com qualquer registros no repositório de análise de Log Olá com um tipo de **alerta**, portanto, você deve executar qualquer configuração é necessária toocollect esses registros.

- Para alertas de análise de Log, [criar regras de alerta](log-analytics-alerts.md) toocreate registros de alerta diretamente no repositório de saudação.
- Para alertas de Nagios e Zabbix, [configurar esses servidores](log-analytics-linux-agents.md) toosend alertas tooLog análise.
- Para alertas do System Center Operations Manager, [conectar seu espaço de análise de Log do Operations Manager gerenciamento grupo tooyour](log-analytics-om-agents.md).  Todos os alertas criados no System Center Operations Manager são importados para o Log Analytics.  

## <a name="configuration"></a>Configuração
Adicionar tooyour de solução de gerenciamento de alertas Olá espaço de trabalho do OMS usando Olá processo descrito em [adicionar soluções](log-analytics-add-solutions.md).  Não é necessária nenhuma configuração.

## <a name="management-packs"></a>Pacotes de gerenciamento
Se o grupo de gerenciamento do System Center Operations Manager for conectado tooyour espaço de trabalho do OMS, Olá pacotes de gerenciamento a seguir é instalado no System Center Operations Manager quando você adicionar essa solução.  Não há nenhuma configuração ou manutenção Olá de pacotes de gerenciamento necessários.  

* Gerenciamento de Alertas do Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Para obter mais informações sobre como os pacotes de gerenciamento da solução são atualizados, consulte [tooLog conectar o Operations Manager análise](log-analytics-om-agents.md).

## <a name="data-collection"></a>Coleta de dados
### <a name="agents"></a>Agentes
Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução.

| Fonte Conectada | Suporte | Descrição |
|:--- |:--- |:--- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não |Agentes diretos do Windows não geram alertas.  Alertas do Log Analytics podem ser criados de eventos e dados de desempenho coletados de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não |Agentes diretos do Linux não geram alertas.  Alertas do Log Analytics podem ser criados de eventos e dados de desempenho coletados de agentes do Linux.  Alertas de Nagios e Zabbix são coletados dos servidores que requerem o agente do Linux hello. |
| [Grupo de gerenciamento do System Center Operations Manager](log-analytics-om-agents.md) |Sim |Alertas são gerados em agentes do Operations Manager são entregues toohello grupo de gerenciamento e, em seguida, encaminhados tooLog análise.<br><br>Análise de uma conexão direta de tooLog de agentes do Operations Manager não é necessária. Dados de alerta são encaminhados de repositório de análise de Log toohello do grupo de gerenciamento de saudação. |


### <a name="collection-frequency"></a>Frequência de coleta
- Registros de alerta são solução toohello disponíveis assim que eles são armazenados no repositório de saudação.
- Dados de alertas são enviados de saudação do Operations Manager gerenciamento grupo tooLog análise cada três minutos.  

## <a name="using-hello-solution"></a>Usando a solução de saudação
Quando você adiciona o espaço de trabalho do hello Alert Management solução tooyour OMS, Olá **gerenciamento de alertas** bloco é adicionado tooyour painel do OMS.  Este bloco exibe uma contagem e a representação gráfica do número de saudação de alertas atualmente ativos que foram gerados em Olá últimas 24 horas.  Não é possível alterar esse intervalo de tempo.

![Bloco do Gerenciamento de Alertas](media/log-analytics-solution-alert-management/tile.png)

Clique em Olá **gerenciamento de alertas** bloco tooopen Olá **gerenciamento de alertas** painel.  Painel de saudação inclui colunas de saudação de Olá a tabela a seguir.  Cada coluna lista Olá top 10 alertas por meio da correspondência de contagem critérios da coluna para Olá especificado escopo e tempo de intervalo.  Você pode executar uma pesquisa de log que fornece a lista inteira de saudação clicando **ver todos os** na parte inferior da coluna de saudação ou clicando o cabeçalho de coluna de saudação do hello.

| Coluna | Descrição |
|:--- |:--- |
| Alertas críticos |Todos os alertas com uma severidade de Crítico agrupados por nome do alerta.  Clique em um nome de alerta toorun uma pesquisa de log retornar todos os registros para o alerta. |
| Alertas de aviso |Todos os alertas com uma severidade de Aviso agrupados por nome do alerta.  Clique em um nome de alerta toorun uma pesquisa de log retornar todos os registros para o alerta. |
| Alertas ativos do SCOM |Todos os alertas coletados do Operations Manager com qualquer estado diferente de *fechado* agrupadas por fonte esse alerta Olá gerado. |
| Todos os alertas ativos |Todos os alertas com qualquer severidade agrupados por nome do alerta. Inclui somente alertas do Operations Manager com qualquer estado diferente de *Fechado*. |

Se você rolar para a direita toohello, painel Olá lista várias consultas comuns que você pode clicar em tooperform um [pesquisa de log](log-analytics-log-searches.md) para dados de alerta.

![Painel do Gerenciamento de Alertas](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Registros do Log Analytics
solução de gerenciamento de alertas de saudação analisa qualquer registro com um tipo de **alerta**.  Alertas criados pela análise de Log ou coletadas de Nagios ou Zabbix não são coletadas diretamente pela solução de saudação.

solução de saudação importar alertas do System Center Operations Manager e cria um registro correspondente para cada um com um tipo de **alerta** e um SourceSystem de **OpsManager**.  Esses registros têm propriedades Olá em Olá a tabela a seguir:  

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*OpsManager* |
| AlertContext |Detalhes do item de dados de saudação que causou a saudação toobe alerta gerado em formato XML. |
| AlertDescription |Descrição detalhada do alerta de saudação. |
| AlertId |GUID de alerta de saudação. |
| AlertName |Nome do alerta de saudação. |
| AlertPriority |Nível de prioridade de alerta de saudação. |
| AlertSeverity |Nível de severidade de alerta de saudação. |
| AlertState |Estado mais recente de resolução de alerta de saudação. |
| LastModifiedBy |Nome de usuário de saudação que modificou por último alerta hello. |
| ManagementGroupName |Nome do grupo de gerenciamento Olá onde o alerta de saudação foi gerado. |
| RepeatCount |Número de vezes Olá mesmo alerta foi gerado para Olá que mesmo objeto monitorado desde que está sendo resolvido. |
| ResolvedBy |Nome do usuário Olá Olá alerta resolvido. Vazia se o alerta Olá ainda não foi resolvida. |
| SourceDisplayName |Exibir o nome de objeto que gerou o alerta de saudação de monitoramento de hello. |
| SourceFullName |Nome completo do hello objeto que gerou o alerta de saudação de monitoramento. |
| TicketId |Identificação do tíquete para alerta Olá se o ambiente do System Center Operations Manager Olá estiver integrado com um processo para atribuir permissões para alertas.  Vazio, se nenhuma ID do Tíquete for atribuída. |
| TimeGenerated |Data e hora em que Olá alerta foi criado. |
| TimeLastModified |Data e hora em que Olá alerta foi alterado pela última. |
| TimeRaised |Data e hora em que Olá alerta foi gerado. |
| TimeResolved |Data e hora em que Olá alerta foi resolvido. Vazia se o alerta Olá ainda não foi resolvida. |

## <a name="sample-log-searches"></a>Pesquisas de log de exemplo
Olá tabela a seguir fornece pesquisas de log de exemplo para os registros de alerta coletados por essa solução: 

| Consultar | Descrição |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |Alertas críticos gerados durante a saudação últimas 24 horas |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |Alertas de aviso gerados durante a saudação últimas 24 horas |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Origens com alertas ativos geradas durante a saudação últimas 24 horas |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |Alertas críticos gerados durante a saudação últimas 24 horas que ainda estão ativas |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |Alertas gerados durante a saudação últimas 24 horas que agora estão fechadas |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Alertas gerados durante a saudação dia anterior agrupado por severidade |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Alertas gerados durante a saudação classificado por seu valor de contagem de repetições dia anterior |


>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá anterior consultas alteraria toohello a seguir:
>
>| Consultar | Descrição |
|:---|:---|
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) |Alertas críticos gerados durante a saudação últimas 24 horas |
| Alert &#124; where AlertSeverity == "warning" and TimeRaised > ago(24h) |Alertas de aviso gerados durante a saudação últimas 24 horas |
| Alert &#124; where SourceSystem == "OpsManager" and AlertState != "Closed" and TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |Origens com alertas ativos geradas durante a saudação últimas 24 horas |
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) and AlertState != "Closed" |Alertas críticos gerados durante a saudação últimas 24 horas que ainda estão ativas |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(24h) and AlertState == "Closed" |Alertas gerados durante a saudação últimas 24 horas que agora estão fechadas |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Alertas gerados durante a saudação dia anterior agrupado por severidade |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; sort by RepeatCount desc |Alertas gerados durante a saudação classificado por seu valor de contagem de repetições dia anterior |


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre os [Alertas no Log Analytics](log-analytics-alerts.md) para obter detalhes sobre como gerar alertas por meio do Log Analytics.
