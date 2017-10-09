---
title: "roteiro do aaaAzure análise de Log consulta idioma | Microsoft Docs"
description: "Este artigo fornece assistência na transição toohello nova linguagem de consulta de análise de Log se você já estiver familiarizado com a linguagem herdados hello."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>Transição tooAzure análise de logs nova linguagem de consulta

> [!NOTE]
> Você pode ler mais sobre Olá análise de logs nova linguagem de consulta e obter Olá procedimento tooupgrade seu espaço de trabalho de uma atualização do seu [pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).

Este artigo fornece assistência na transição toohello nova linguagem de consulta de análise de Log se você já estiver familiarizado com a linguagem herdados hello.

## <a name="language-converter"></a>Conversor de linguagem

Se você estiver familiarizado com a linguagem de consulta de análise de Log herdada hello, hello toocreate Olá a mesma consulta em linguagem novo Olá de maneira mais fácil é toouse hello conversor de idioma que é instalada no portal de pesquisa de Log de saudação quando seu espaço de trabalho é convertido.  Usar o conversor de saudação é tão simple quanto digitando uma consulta herdada na caixa de texto superior hello e, em seguida, clicando em **converter**.  Clique Olá botão toorun Olá pesquisa ou copie e cole-o toouse-lo em outro lugar.

![Conversor de linguagem](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>Roteiro

Olá tabela a seguir fornece uma comparação entre uma variedade de consultas comuns tooequivalent comandos entre a linguagem de consulta herdados e novos de saudação na análise de Log do Azure.

| Descrição | Herdada | novo |
|:--|:--|:--|
| Pesquisar todas as tabelas      | error | Pesquisar “erro” (não diferencia maiúsculas de minúsculas) |
| Selecione os dados da tabela | Type=Event |  Evento |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| Comparação de cadeias de caracteres      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Evento &#124; em que o Computador contém “contoso” (não diferencia maiúsculas de minúsculas)<br>Evento &#124; em que o Computador contains_cs “Contoso” (diferencia maiúsculas de minúsculas) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| Comparação de datas        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| Comparação de boolianos     | Type=Heartbeat IsGatewayInstalled=false  | Pulsação | where IsGatewayInstalled == false |
| Classificar                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event \| sort by Computer asc, EventLog desc, EventLevelName asc |
| Distinct               | Type=Event &#124; dedup Computer \| select Computer | Event &#124; summarize by Computer, EventLog |
| Estender colunas         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" \| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| Agregação            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| Agregação com limite | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| União                  | Type=Event or Type=Syslog | union Event, Syslog |
| Ingressar                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>Próximas etapas
- Check-out de um [tutorial sobre como escrever consultas](https://go.microsoft.com/fwlink/?linkid=856078) usando Olá nova linguagem de consulta.
- Consulte toohello [referência de linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856079) para obter detalhes sobre todas as funções hello nova linguagem de consulta, operadores e comando.  
