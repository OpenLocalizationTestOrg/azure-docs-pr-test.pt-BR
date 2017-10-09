---
title: "pesquisas de aaaLog na análise de Log do OMS | Microsoft Docs"
description: "Você requer uma tooretrieve de pesquisa de log todos os dados de análise de Log.  Este artigo descreve como o novo log pesquisas são usadas na análise de Log e apresenta os conceitos que você precisa toounderstand antes de criar um."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Compreendendo as pesquisas de logs no Log Analytics

> [!NOTE]
> Este artigo descreve as pesquisas de log na análise de Log do Azure usando Olá nova linguagem de consulta.  Você pode saber mais sobre a nova linguagem de saudação e obter Olá procedimento tooupgrade seu espaço de trabalho em [atualizar sua pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).  
>
> Se o espaço de trabalho não tiver sido atualizado toohello nova linguagem de consulta, você deve referir-se muito[localizar os dados usando pesquisas de log na análise de Log](log-analytics-log-searches.md).

Você requer uma tooretrieve de pesquisa de log todos os dados de análise de Log.  Se você estiver analisando dados no portal de hello, configurando uma regra de alerta toobe notificado de uma determinada condição ou recuperar dados usando Olá API de análise de Log, você usará um dados saudação do toospecify da pesquisa de log desejado.  Este artigo descreve como novas pesquisas de logs são utilizadas no Log Analytics e fornece conceitos que deverão ser compreendidos antes de criar uma. Consulte Olá [próximas etapas](#next-steps) seção para obter detalhes sobre a criação e edição de pesquisas de log e de referências de linguagem de consulta de saudação.

## <a name="where-log-searches-are-used"></a>Onde as pesquisas de logs são utilizadas

Olá diferentes maneiras que você usará pesquisas de log na análise de Log incluem o seguinte hello:

- **Portais.** Você pode executar análises interativas de dados no repositório de Olá Olá [portal de pesquisa de Log](log-analytics-log-search-log-search-portal.md) ou hello [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587).  Isso permite tooedit sua consulta e analisar os resultados de saudação em uma variedade de formatos e visualizações.  A maioria das consultas que você criar será iniciado em um dos portais hello e, em seguida, copiados depois de verificar se ele funciona conforme esperado.
- **Regras de alerta** As [Regras de alerta](log-analytics-alerts.md) identificam proativamente os problemas dos dados no espaço de trabalho.  Cada regra de alerta é baseada em uma pesquisa de logs que é executada automaticamente em intervalos regulares.  resultados de saudação são inspecionado toodetermine se um alerta deve ser criado.
- **Exibições.**  Você pode criar visualizações de dados toobe incluídas nos painéis de controle de usuário com [Designer de exibição](log-analytics-view-designer.md).  Pesquisas de log fornecem dados Olá usados pelo [blocos](log-analytics-view-designer-tiles.md) e [partes visualização](log-analytics-view-designer-parts.md) em cada exibição.  Você pode fazer drill down de partes de visualização em Olá pesquisa de Log tooperform portal análise detalhada dados saudação.
- **Exportação.**  Quando você exportar dados de saudação tooExcel de espaço de trabalho de análise de Log ou [Power BI](log-analytics-powerbi.md), você cria um log pesquisa toodefine Olá dados tooexport.
- **PowerShell.** Você pode executar um script do PowerShell de uma linha de comando ou um runbook de automação do Azure que usa [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve dados de análise de Log.  Esse cmdlet requer um tooretrieve de dados consulta toodetermine hello.
- **API do Log Analytics.**  Olá [API de pesquisa de log de análise de Log](log-analytics-log-search-api.md) permite que qualquer cliente API REST tooretrieve dados de espaço de trabalho de saudação.  solicitação de API de saudação inclui uma consulta que é executada em análise de Log toodetermine Olá dados tooretrieve.

![Pesquisas de log](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Como os dados do Log Analytics são organizados
Quando você cria uma consulta, iniciar, determinando quais tabelas têm dados Olá que você está procurando. Cada [fonte de dados](log-analytics-data-sources.md) e [solução](../operations-management-suite/operations-management-suite-solutions.md) armazena seus dados em tabelas dedicadas no espaço de trabalho de análise de Log de saudação.  Documentação para cada fonte de dados e a solução inclui nome Olá Olá do tipo de dados que ele cria e uma descrição de cada uma de suas propriedades.     Muitas consultas exigirá apenas dados de um único tabelas, mas podem usar uma variedade de opções tooinclude dados de várias tabelas.

![Tabelas](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Escrevendo uma consulta
Núcleo de saudação do log de pesquisas em análise de Log é [uma linguagem de consulta ampla](https://docs.loganalytics.io/) que permite recuperar e analisar dados do repositório de saudação em uma variedade de maneiras.  Este mesmo idioma de consulta é usado para [Application Insights](../application-insights/app-insights-analytics.md).  Aprender como toowrite uma consulta é crítica toocreating pesquisas de log na análise de Log.  Normalmente, você começará com consultas básicas e, em seguida, progresso toouse mais funções avançadas conforme seus requisitos se tornam mais complexos.

estrutura básica de saudação de uma consulta é uma tabela de origem seguida por uma série de operadores separados por um caractere de pipe `|`.  Você pode encadear vários dados de saudação toorefine de operadores e executar funções avançadas.

Por exemplo, suponha que você desejasse toofind Olá superior dez computadores com hello a maioria dos eventos de erro sobre Olá dia anterior.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

Ou talvez você queira toofind computadores que ainda não tinham uma pulsação no último dia de saudação.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

E quanto um gráfico de linhas com a utilização do processador Olá para cada computador na semana passada?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Você pode ver esses exemplos rápida que, independentemente do tipo de saudação de dados que você está trabalhando, Olá estrutura de consulta de saudação é semelhante.  Você pode dividi-la em etapas distintas, onde os dados resultantes de saudação de um comando são enviados através do seguinte comando do hello pipeline toohello.

Para a documentação completa sobre linguagem de consulta de análise de logs do Azure Olá incluindo tutoriais e referência de linguagem, consulte Olá [documentação da linguagem de consulta de análise de logs do Azure](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre Olá [portais que você use toocreate e editar pesquisas de log](log-analytics-log-search-portals.md).
- Check-out de um [tutorial sobre como escrever consultas](https://go.microsoft.com/fwlink/?linkid=856078) usando Olá nova linguagem de consulta.
