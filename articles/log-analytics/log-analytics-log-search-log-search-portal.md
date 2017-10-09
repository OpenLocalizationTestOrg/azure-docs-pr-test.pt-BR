---
title: "portal de pesquisa de Log de saudação aaaUsing na análise de Log do Azure | Microsoft Docs"
description: "Este artigo inclui um tutorial que descreve como toocreate pesquisas de log e analisar dados armazenados em seu espaço de trabalho de análise de Log usando o portal de pesquisa de Log de saudação.  tutorial de saudação inclui executar algumas consultas simples tooreturn diferentes tipos de dados e analisar os resultados."
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
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Criar pesquisas de log na análise de Log do Azure usando o portal de pesquisa de Log de saudação

> [!NOTE]
> Este artigo descreve o portal de pesquisa de Log de saudação na análise de Log do Azure usando Olá nova linguagem de consulta.  Você pode saber mais sobre a nova linguagem de saudação e obter Olá procedimento tooupgrade seu espaço de trabalho em [atualizar sua pesquisa de log de toonew de espaço de trabalho do Azure Log Analytics](log-analytics-log-search-upgrade.md).  
>
> Se o espaço de trabalho não tiver sido atualizado toohello nova linguagem de consulta, você deve referir-se muito[localizar os dados usando pesquisas de log na análise de Log](log-analytics-log-searches.md) para obter informações sobre a versão atual de saudação do portal de pesquisa de Log de saudação.

Este artigo inclui um tutorial que descreve como toocreate pesquisas de log e analisar dados armazenados em seu espaço de trabalho de análise de Log usando o portal de pesquisa de Log de saudação.  tutorial de saudação inclui executar algumas consultas simples tooreturn diferentes tipos de dados e analisar os resultados.  Ele se concentra nos recursos no portal de pesquisa de Log de saudação para modificar Olá consulta em vez de modificá-la diretamente.  Para obter detalhes sobre a edição direta consulta hello, consulte Olá [referência de linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856079).

pesquisas de toocreate no portal do Advanced Analytics Olá em vez do portal de pesquisa de Log hello, consulte [guia de Introdução com hello Portal da análise de](https://go.microsoft.com/fwlink/?linkid=856587).  Ambos os portais usam Olá consulta mesmo idioma tooaccess Olá mesmos dados no espaço de trabalho de análise de Log de saudação.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial presume que você já tem um espaço de trabalho de análise de Log pelo menos uma origem conectada que gera dados para Olá tooanalyze de consultas.  

- Se você não tiver um espaço de trabalho, você pode criar uma livre usando o procedimento Olá [começar com um espaço de trabalho de análise de Log](log-analytics-get-started.md).
- Conecte-se pelo menos uma [agente do Windows](log-analytics-windows-agents.md) ou um [agente Linux](log-analytics-linux-agents.md) toohello espaço de trabalho.  

## <a name="open-hello-log-search-portal"></a>Portal de pesquisa de Log aberto Olá
Comece abrindo o portal de pesquisa de Log de saudação.  Você pode acessá-lo no portal do OMS hello ou Olá portal do Azure.

1. Olá Abrir portal do Azure.
2. Navegue tooLog análise e selecione seu espaço de trabalho.
3. Selecione **pesquisa de Log** toostay em hello Azure portal ou inicie Olá portal do OMS selecionando **Portal do OMS** e clicando no botão de pesquisa de Log de saudação.

![Botão Pesquisar Log](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Crie uma pesquisa simples
Olá tooretrieve de maneira mais rápida toowork alguns dados com é uma consulta simples que retorna todos os registros na tabela.  Se você tiver qualquer Windows ou Linux clientes conectados tooyour espaço de trabalho, em seguida, você terá dados em hello ou evento (Windows) ou tabela de Syslog (Linux).

Digite uma saudação consultas na caixa de pesquisa Olá a seguir e clique botão de pesquisa de saudação.  

```
Event
```
```
Syslog
```

Dados são retornados na exibição de lista padrão Olá, e você pode ver o número total de registros foram retornados.

![Consulta simples](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Somente hello primeiro algumas propriedades de cada registro são exibidas.  Clique em **Mostrar mais** toodisplay todas as propriedades de um registro específico.

![Detalhes do registro](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Definir o escopo de tempo de saudação
Cada registro coletado pela análise de Log tem um **TimeGenerated** propriedade que contém Olá data e hora que esse registro Olá foi criado.  Uma consulta no portal de pesquisa de Log de saudação retorna somente os registros com um **TimeGenerated** no escopo de tempo de saudação que é exibido no lado esquerdo da tela hello de saudação.  

Você pode alterar o filtro de tempo de saudação selecionando o menu suspenso de saudação ou modificando o controle deslizante de saudação.  controle deslizante de saudação exibe um gráfico de barras que mostra o número relativo de saudação de registros para cada segmento de tempo dentro do intervalo de saudação.  Este segmento irá variar dependendo de intervalo de saudação.

escopo de tempo padrão Olá é **1 dia**.  Alterar esse valor também**7 dias**, e deve aumentar o número total de saudação de registros.

![Escopo de data e hora](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Filtrar resultados de consulta Olá
Em Olá lado esquerdo da tela hello é o painel de filtro de saudação que permite que você tooadd toohello consulta de filtragem sem modificá-lo diretamente.  Várias propriedades de saudação registros retornados são exibidas com seus valores de dez principais com sua contagem de registro.

Se você estiver trabalhando com **evento**, selecione Olá caixa de seleção próxima muito**erro** em **EVENTLEVELNAME**.   Se você estiver trabalhando com **Syslog**, selecione Olá caixa de seleção próxima muito**err** em **SEVERITYLEVEL**.  Isso altera a consulta Olá tooone de Olá Olá toolimit a seguir resulta tooerror eventos.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Painel de filtro de toohello adicionar propriedades selecionando **adicionar toofilters** Olá propriedade no menu de um dos registros de saudação.

![Adicionar menu toofilter](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

Você pode definir Olá mesmo filtro selecionando **filtro** no menu de propriedade de saudação de um registro com o valor de saudação desejado toofilter.  

Você só tiver Olá **filtro** opção para propriedades com seu nome em azul.  Estes são campos *pesquisáveis* que estão indexados para as condições de pesquisa.  Os campos em cinza são *pesquisável de texto livre* campos que têm apenas Olá **Mostrar referências** opção.  Esta opção retorna registros que possuem esse valor em qualquer propriedade.

![Menu de filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Você pode agrupar resultados de saudação em uma única propriedade selecionando Olá **Agrupar por** opção no menu de registro de saudação.  Isso adicionará uma [resumir](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) consulta tooyour de operador que exibe os resultados de saudação em um gráfico.  Você pode agrupar em mais de uma propriedade, mas você precisaria consulta de saudação tooedit diretamente.  Saudação de Avançar Olá Olá selecione menu Registro **computador** propriedade e selecione **Group by 'Computer'**.  

![Agrupar por computador](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Trabalhar com os resultados
portal de pesquisa de Log de saudação tem uma variedade de recursos para trabalhar com os resultados de saudação de uma consulta.  Você pode classificar, filtrar e agrupar resultados de dados de saudação do tooanalyze sem modificar a consulta real hello.  Os resultados de uma consulta não são classificados por padrão.

saudação de tooview dados em formato de tabela que fornece opções adicionais de filtragem e classificação, clique em **tabela**.  

![Exibição da tabela](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Clique em seta Olá por um detalhes de saudação tooview registro para o registro.

![Classificar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Classifique em qualquer campo, clicando no cabeçalho de coluna.

![Classificar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Filtrar resultados de saudação em um valor específico na coluna Olá clicando no botão Filtrar hello e fornecer uma condição de filtro.

![Resultados do filtro](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Arrastando seu superior de toohello do cabeçalho de coluna dos resultados da saudação de grupo em uma coluna.  Você pode agrupar em vários campos arrastando a parte superior de toohello várias colunas.

![Resultados de grupo](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Trabalhe com dados de desempenho
Dados de desempenho para os agentes do Windows e Linux são armazenados no espaço de trabalho de análise de Log de saudação em Olá **Perf** tabela.  Os registros de desempenho são semelhante a qualquer outro registro e é possível gravar uma consulta simples que retorna todos os registros de desempenho, assim como eventos.

```
Perf
```

![Dados de desempenho](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

Retornando milhões de registros para todos contadores e objetos de desempenho, porém, não é muito útil.  Você pode usar o hello mesmos métodos usados acima dados de saudação toofilter ou simplesmente digite Olá seguinte consulta diretamente na caixa de pesquisa de log de saudação.  Isso retorna somente os registros de utilização do processador para computadores Windows e Linux.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilização do processador](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Isso limita o contador específico da saudação dados tooa, mas ela ainda não colocá-la em um formulário que é particularmente útil.  Você pode exibir dados de saudação em um gráfico de linhas, mas primeiro é necessário toogroup-lo por computador e TimeGenerated.  toogroup em vários campos, você precisa de consulta de saudação do toomodify diretamente, para modificar a seguir Olá consulta toohello.  Isso usa Olá [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) função hello **CounterValue** valor médio da propriedade toocalculate Olá cada hora.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Gráfico de dados de desempenho](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Agora que os dados de saudação adequadamente são agrupados, você pode exibi-lo em um gráfico de visual adicionando Olá [renderizar](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operador.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Gráfico de Linhas](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre a linguagem de consulta de análise de Log de saudação em [guia de Introdução com hello Portal da análise de](https://go.microsoft.com/fwlink/?linkid=856079).
- Percorrer um tutorial usando Olá [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) que permite a você toorun Olá mesmo consultas e acesso Olá mesmos dados que o portal de pesquisa de Log de saudação.
