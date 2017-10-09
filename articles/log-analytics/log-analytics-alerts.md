---
title: "alertas de aaaUnderstanding na análise de Log do Azure | Microsoft Docs"
description: "Alertas de análise de Log identificar informações importantes no seu repositório do OMS e podem proativamente notificá-lo de problemas ou invocar ações tooattempt toocorrect-los.  Este artigo descreve Olá diferentes tipos de regras de alerta e como elas são definidas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Noções básicas sobre alertas no Log Analytics

Alertas no Log Analytics identificam informações importante no repositório de Log Analytics.  Este artigo fornece detalhes das regras de alerta como no trabalho de análise de Log e descreve as diferenças de saudação entre tipos diferentes de regras de alerta.

Para obter Olá o processo de criação de regras de alerta, consulte Olá artigos a seguir:

- Criar regras de alerta usando o [Portal do Azure](log-analytics-alerts-creating.md)
- Criar regras de alerta usando o [modelo do Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Criar regras de alerta usando a [API REST](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Regras de alerta

Os alertas são criados por regras de alerta que executam pesquisas de log automaticamente em intervalos regulares.  Se os resultados de saudação de pesquisa de log de saudação corresponderem critérios específicos, será criado um registro de alerta.  regra de saudação poderá, em seguida, executar automaticamente uma ou mais tooproactively de ações notificá-lo de alerta de saudação ou chamar outro processo.  Diferentes tipos de regras de alerta usam uma lógica diferente tooperform essa análise.

![Alertas do Log Analytics](media/log-analytics-alerts/overview.png)

Regras de alerta são definidas por Olá detalhes a seguir:

- **Pesquisa de log**.  consulta de saudação que é executado sempre que a regra de alerta de saudação é acionado.  registros de saudação retornados por essa consulta é toodetermine usado se um alerta será criado.
- **Janela de tempo**.  Especifica o intervalo de tempo de saudação para consulta hello.  consulta de saudação retorna somente os registros que foram criados neste intervalo de saudação hora atual.  Este pode ser qualquer valor entre 5 minutos e 24 horas. Por exemplo, se hello tempo janela é definida too60 minutos e consulta de saudação for executado em 1:15 PM, somente os registros criados entre 12:15 PM e 1:15 PM será retornado.
- **Frequência**.  Especifica com que frequência hello consulta deve ser executada. Pode ser qualquer valor entre 5 minutos e 24 horas. Deve ser igual tooor inferior a janela de tempo de saudação.  Se o valor de saudação for maior que a janela de tempo de saudação, você poderá registros que está sendo ignorados.<br>Por exemplo, considere uma janela de tempo de 30 minutos e uma frequência de 60 minutos.  Se Olá consulta é executada à 1:00, ele retorna registros entre 12:30 e 1:00 PM.  Olá próxima vez consulta Olá executaria é 2:00 quando ela retorna registros entre 30:1 e 2:00.  Todos os registros criados entre 1:00 e 1:30 nunca seriam avaliados.
- **Limite**.  resultados de Olá de pesquisa de log de saudação são avaliada toodetermine se um alerta deve ser criado.  limite de saudação é diferente para diferentes tipos de saudação de regras de alerta.

Cada regra de alerta no Log Analytics é de um entre dois tipos.  Cada um desses tipos é descrita em detalhes nas seções de saudação que seguem.

- **[Número de resultados](#number-of-results-alert-rules)**. Alerta criada quando os registros de número Olá retornados pela pesquisa de log de saudação exceder um número especificado.
- **[Medida métrica](#metric-measurement-alert-rules)**.  Alerta criada para cada objeto em resultados de saudação da pesquisa de log de saudação com valores que excedem o limite especificado.

diferenças de saudação entre tipos de regra de alerta são da seguinte maneira.

- **Número de resultados** regra de alerta sempre criará um pouco de alerta único **medição métrica** regra de alerta cria um alerta para cada objeto que excede o limite de saudação.
- **Número de resultados** regras de alerta criam um alerta quando o limite de saudação for excedido uma única vez. **Medição métrica** regras de alerta podem criar um alerta quando Olá limite for excedido um determinado número de vezes em um intervalo de tempo específico.

## <a name="number-of-results-alert-rules"></a>Regras de alerta de Número de resultados
**Número de resultados** regras de alerta criam um alerta quando o número de Olá de registros retornados pela consulta de pesquisa de saudação exceder o limite especificado de saudação.

### <a name="threshold"></a>Limite
limite de saudação para um **número de resultados** regra de alerta é simplesmente maior ou menor que um valor específico.  Se o número de saudação de registros retornados pela pesquisa de log de saudação corresponder esse critério, um alerta é criado.

### <a name="scenarios"></a>Cenários

#### <a name="events"></a>Eventos
Esse tipo de regra de alerta é ideal para trabalhar com eventos como logs de eventos do Windows, Syslog e logs Personalizados.  Talvez você queira toocreate um alerta quando um evento de erro específico é criado, ou quando vários eventos de erro são criados dentro de uma janela de tempo específico.

tooalert em um único evento, o número de Olá de conjunto de resultados toogreater que 0 e frequência hello e minutos de too5 de janela de tempo.  Que executa a consulta Olá cada 5 minutos e verificar a ocorrência de saudação de um único evento que foi criado como Olá última hora Olá consulta foi executada.  Uma frequência maior pode atrasar o tempo de saudação entre Olá evento sendo coletados e alerta hello está sendo criado.

Alguns aplicativos podem registrar um erro ocasional que não necessariamente gerará um alerta.  Por exemplo, o aplicativo hello pode repetir o processo Olá que criou o evento de erro de saudação e bem-sucedidos hello, em seguida, a próxima vez.  Nesse caso, não convém alerta de saudação toocreate, a menos que vários eventos são criados dentro de uma janela de tempo específico.  

Em alguns casos, convém toocreate um alerta na ausência de saudação de um evento.  Por exemplo, um processo pode registrar eventos regulares tooindicate que ele está funcionando corretamente.  Se ele não registrar um desses eventos dentro de uma janela de tempo específica, um alerta deverá ser criado.  Nesse caso, você configuraria o limite de saudação muito**menos de 1**.

#### <a name="performance-alerts"></a>Alertas de desempenho
[Dados de desempenho](log-analytics-data-sources-performance-counters.md) é armazenado como registros de saudação tooevents semelhante do repositório do OMS.  Se você quiser tooalert quando um contador de desempenho excede um determinado limite, esse limite deve ser incluído na consulta de saudação.

Por exemplo, se você quisesse tooalert quando hello processador executa 90%, você usaria uma consulta como Olá a seguir com o limite de saudação de regra de alerta de saudação **maior que 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Se você quisesse tooalert ao processador Olá média mais de 90% de uma janela de tempo específico, você usaria uma consulta usando Olá [medir comando](log-analytics-search-reference.md#commands) seguinte Olá com limite de saudação de regra de alerta Olá **maior que 0** .

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), e em seguida, Olá acima consultas alteraria toohello a seguir:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Regras de alerta com medição métrica

>[!NOTE]
> Regras de alerta de Medição métrica estão atualmente em visualização pública.

Regras de alerta de **Medição métrica** criam um alerta para cada objeto em uma consulta com um valor que excede um limite especificado.  Tiverem Olá seguintes diferenças marcantes de **número de resultados** regras de alerta.

#### <a name="log-search"></a>Pesquisa de log
Embora você possa usar qualquer consulta para um **número de resultados** regra de alerta, há consulta de saudação requisitos específicos para uma regra de alerta de métrica de medição.  Ele deve incluir um [medir comando](log-analytics-search-reference.md#commands) toogroup resultados de saudação em um determinado campo. Este comando deve incluir Olá elementos a seguir.

- **Função de agregação**.  Determina o cálculo de saudação que é executado e potencialmente tooaggregate um campo numérico.  Por exemplo, **contagem** irá retornar o número de saudação de registros na consulta hello, **avg(CounterValue)** retornará média de saudação do campo de CounterValue Olá durante o intervalo de saudação.
- **Campo Grupo**.  Um registro com um valor agregado será criado para cada instância do campo e um alerta pode ser gerado para cada um deles.  Por exemplo, se você quisesse toogenerate um alerta para cada computador, você usaria **pelo computador**.   
- **Intervalo**.  Define o intervalo de tempo de saudação durante o qual os dados de saudação são agregados.  Por exemplo, se você especificou **5 minutos**, seria criado um registro para cada instância do campo de grupo Olá agregado em intervalos de 5 minutos em janela de tempo de saudação especificada para o alerta de saudação.

#### <a name="threshold"></a>Limite
limite de saudação para regras de alerta de medição métrica é definido por um valor de agregação e um número de violações.  Se qualquer ponto de dados na pesquisa de log de saudação exceder esse valor, é uma violação.  Se excede o número Olá das violações de qualquer objeto nos resultados da saudação Olá especificado valor, um alerta é criado para esse objeto.

#### <a name="example"></a>Exemplo
Considere um cenário em que você deseje um alerta se qualquer computador exceda 90% de utilização do processador por três vezes em 30 minutos.  Você cria uma regra de alerta com hello detalhes a seguir.  

**Consulta:** Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer Interval 5minute<br>
**Janela de tempo:** 30 minutos<br>
**Frequência de alerta:** cinco minutos<br>
**Valor de agregação:** maior que 90<br>
**Disparar alerta com base em:** total de violações maior que cinco<br>

consulta de saudação criaria um valor médio para cada computador em intervalos de 5 minutos.  Essa consulta seria executada a cada 5 minutos por dados coletados pela Olá 30 minutos anteriores.  Abaixo, são mostrados dados de exemplo para três computadores.

![Resultados da consulta de exemplo](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

Neste exemplo, alertas separadas seriam criadas para srv02 e srv03 desde que eles violação de limite de 90% de saudação 3 vezes em janela de tempo de saudação.  Se hello **alerta disparador com base em:** foram alteradas muito**consecutivas** um alerta deve ser criado apenas para srv03 desde que a violação de limite de saudação para 3 amostras consecutivas.

## <a name="alert-records"></a>Registros de alerta
Registros de alerta criados por regras de alerta no Log Analytics têm um **Type** que indica **Alert** e um **SourceSystem** que indica **OMS**.  Eles têm propriedades Olá no Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*OMS* |
| *Objeto*  | [Alertas de medição métrica](#metric-measurement-alert-rules) terão uma propriedade de campo de grupo hello.  Por exemplo, se a pesquisa de log de saudação grupos no computador, Olá registro com tem um campo de computador com o nome de saudação do computador de saudação como valor de saudação do alerta.
| AlertName |Nome do alerta de saudação. |
| AlertSeverity |Nível de severidade de alerta de saudação. |
| LinkToSearchResults |Vincule a pesquisa de log de análise de tooLog que retorna registros de saudação da consulta de saudação que criou o alerta de saudação. |
| Consultar |Texto da consulta Olá que foi executada. |
| QueryExecutionEndTime |Final do intervalo de tempo de saudação para consulta de saudação. |
| QueryExecutionStartTime |Início do intervalo de tempo de saudação para consulta hello. |
| ThresholdOperator | Operador que foi usado pela regra de alerta de saudação. |
| ThresholdValue | Valor que foi usado pela regra de alerta de saudação. |
| TimeGenerated |Alerta de saudação de data e hora foi criado. |

Outros tipos de registros de alertas criados por Olá [solução de gerenciamento de alertas](log-analytics-solution-alert-management.md) e [Power BI exporta](log-analytics-powerbi.md).  Eles têm um **Type** que indica **Alert**, mas são diferenciados por seus **SourceSystem**.


## <a name="next-steps"></a>Próximas etapas
* Instalar Olá [solução de gerenciamento de alertas](log-analytics-solution-alert-management.md) tooanalyze alertas criadas na análise de Log junto com alertas coletados pelo System Center Operations Manager.
* Leia mais sobre [pesquisas de log](log-analytics-log-searches.md) que podem gerar alertas.
* Conclua um passo a passo para [configurar um webhook](log-analytics-alerts-webhooks.md) com uma regra de alerta.  
* Saiba como toowrite [runbooks na automação do Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemas identificados por alertas.
