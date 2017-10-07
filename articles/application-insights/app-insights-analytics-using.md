---
title: "aaaUsing análise - Olá poderosa ferramenta de pesquisa de informações de aplicativo do Azure | Microsoft Docs"
description: "Usando Olá análise, a ferramenta de diagnóstico avançados de pesquisa de saudação do Application Insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>Usando Análise no Application Insights
[Análise de](app-insights-analytics.md) é o recurso de pesquisa poderoso saudação do [Application Insights](app-insights-overview.md). Essas páginas descrevem a linguagem de consulta do Log Analytics.

* **[Assistir ao vídeo introdutório Olá](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Faça o test drive análise sobre nossos dados simulados](https://analytics.applicationinsights.io/demo)**  se seu aplicativo não esteja enviando dados tooApplication Insights ainda.

## <a name="open-analytics"></a>Abrir Análise
Do recurso de página inicial do seu aplicativo no Application Insights, clique em Análise.

![Abra o portal.azure.com, abra o recurso do Application Insights e clique em Análise.](./media/app-insights-analytics-using/001.png)

tutorial de embutido Olá oferece algumas ideias sobre o que você pode fazer.

Há um [tour mais extenso aqui](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Consultar sua telemetria
### <a name="write-a-query"></a>Escreva uma consulta
![Exibição de esquema](./media/app-insights-analytics-using/150.png)

Começar com nomes de saudação de qualquer uma das tabelas Olá listadas Olá esquerda (ou hello [intervalo](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) ou [união](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operadores). Use `|` toocreate um pipeline de [operadores](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense solicita operadores hello e elementos de expressão Olá que você pode usar. Clique o ícone de informações hello (ou pressione CTRL + espaço) tooget uma descrição mais detalhada e exemplos de como toouse cada elemento.

Consulte Olá [tour de idioma de análise](app-insights-analytics-tour.md) e [referência de linguagem](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Executar uma consulta
![Executando uma consulta](./media/app-insights-analytics-using/130.png)

1. Você pode usar quebras de linha simples em uma consulta.
2. Coloque o cursor hello dentro ou no final de saudação da consulta Olá que ser toorun.
3. Verifique o intervalo de tempo de saudação da sua consulta. (Você pode alterá-lo ou substituí-lo, incluindo sua própria cláusula [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) em sua consulta.)
3. Clique em Ir toorun Olá consulta.
4. Não coloque linhas em branco em sua consulta. Você pode manter várias consultas separadas em uma guia de consulta separando-as com linhas em branco. Somente consulta Olá que tem um cursor de saudação é executada.

### <a name="save-a-query"></a>Salvar uma consulta
![Salvando uma consulta](./media/app-insights-analytics-using/140.png)

1. Salve o arquivo de consulta atual hello.
2. Abra um arquivo de consulta salva.
3. Crie um novo arquivo de consulta.

## <a name="see-hello-details"></a>Consulte os detalhes de saudação
Expanda qualquer linha hello resultados toosee sua lista completa das propriedades. Você pode expandir mais qualquer propriedade que é um valor estruturado - por exemplo, dimensões personalizadas ou pilha Olá listando em uma exceção.

![Expandindo uma linha](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Organizar os resultados de saudação
Classificar, filtrar, paginação e agrupar resultados Olá retornados da consulta.

> [!NOTE]
> Classificação, agrupamento e filtragem no navegador de saudação não execute novamente a consulta. Eles apenas reorganizar resultados Olá que foram retornados por sua última consulta. 
> 
> tooperform essas tarefas no servidor de saudação antes Olá resultados são retornados, gravar a consulta com hello [classificação](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) e [onde](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operadores.
> 
> 

Escolher colunas Olá faria como toosee, arraste toorearrange de cabeçalhos de coluna-los e redimensionar colunas arrastando as bordas.

![Organizando colunas](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Classificar e filtrar itens
Classifica seus resultados clicando head saudação de uma coluna. Clique novamente em toosort Olá outra maneira, e clique em pela terceira vez toorevert toohello original ordenação retornado pela consulta.

Use toonarrow de ícone de filtro Olá sua pesquisa.

![Classificar e filtrar colunas](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Agrupar itens
toosort por mais de uma coluna, use o agrupamento. Primeiro ativá-lo e arraste cabeçalhos de coluna para o espaço de saudação acima da tabela de saudação.

![Agrupar](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Faltando alguns resultados?

Se você acha que você não vir todos os resultados de saudação esperado, há alguns motivos possíveis.

* **Filtro de intervalo de tempo**. Por padrão, você só verá resultados de saudação últimas 24 horas. Há um filtro automático que limita o intervalo de saudação de resultados que são recuperados das tabelas de origem de saudação. 

    No entanto, você pode alterar o intervalo de tempo de saudação filtro usando o menu suspenso de saudação.

    Ou você pode substituir o intervalo automático hello, incluindo sua própria [ `where  ... timestamp ...` cláusula](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) em sua consulta. Por exemplo:

    `requests | where timestamp > ago('2d')`

* **Limite de resultados**. Há um limite de 10 mil linhas nos resultados de saudação retornados do portal de saudação. Um aviso mostra se você vá acima do limite de saudação. Se isso acontecer, classificar seus resultados na tabela de saudação não sempre mostrará todos os Olá primeiro ou últimos resultados reais. 

    É o limite de uma boa prática tooavoid atingir hello. Use o filtro de intervalo de tempo de saudação ou usar operadores, como:

  * [top 100 by timestamp](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(Quer de 10 mil linhas? Considere usar [Exportação contínua](app-insights-export-telemetry.md) em vez disso. A análise foi projetada para análise, em vez de recuperar dados brutos.)

## <a name="diagrams"></a>Diagramas
Selecione o tipo de saudação do diagrama que deseja:

![Selecionar um tipo de diagrama](./media/app-insights-analytics-using/230.png)

Se você tiver várias colunas de tipos de saudação à direita, você pode escolher Olá x e eixos y e uma coluna de resultados de saudação toosplit dimensões por.

Por padrão, resultados são inicialmente exibidos como uma tabela e você selecionar diagrama Olá manualmente. Mas você pode usar o hello [renderizar diretiva](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) final Olá tooselect uma consulta um diagrama.

### <a name="analytics-diagnostics"></a>Diagnóstico de análise


Em um timechart, se houver um aumento repentino ou a etapa em seus dados, você poderá ver um ponto realçado na linha de saudação. Isso indica que o diagnóstico de análise de identificou uma combinação das propriedades filtrar alterações repentinas hello. Clique em Olá ponto tooget obter mais detalhes sobre o filtro hello e toosee Olá filtrado versão. Isso pode ajudá-lo a identificar qual alteração Olá geradas. 

[Saiba mais sobre o Diagnóstico de Análise](app-insights-analytics-diagnostics.md)


![Diagnóstico de análise](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>PIN toodashboard
Você pode fixar um tooone diagrama ou tabela de seu [compartilhado painéis](app-insights-dashboards.md) -apenas clicar em fixar hello. (Talvez seja necessário muito[atualização de pacote de preços do seu aplicativo](app-insights-pricing.md) tooturn sobre esse recurso.) 

![Clique em fixar Olá](./media/app-insights-analytics-using/pin-01.png)

Isso significa que, quando você cria um toohelp painel você monitorar o desempenho de saudação ou o uso de serviços da web, você pode incluir análise bastante complexa junto com hello outras métricas. 

Você pode fixar um painel de toohello de tabela, se ele tem quatro ou menos colunas. Somente Olá sete linhas superiores são exibidas.

### <a name="dashboard-refresh"></a>Atualização do painel
Olá gráfico fixado toohello painel é atualizado automaticamente, executando novamente Olá consulta aproximadamente a cada horas. Você também pode clicar em botão de atualização de saudação.

### <a name="automatic-simplifications"></a>Simplificações automáticas

Determinados simplificações são aplicadas tooa gráfico quando você fixa tooa painel.

**Restrição de tempo:** consultas são automaticamente limitado toohello últimos 14 dias. Olá efeito é Olá mesmo que sua consulta inclui `where timestamp > ago(14d)`.

**Guardar a restrição de contagem:** se você exibir um gráfico que tem vários compartimentos discretos (normalmente um gráfico de barras), Olá menos compartimentos preenchidos automaticamente são agrupados em um único "outros" bin. Por exemplo, esta consulta:

    requests | summarize count_search = count() by client_CountryOrRegion

tem esta aparência no Analytics:

![Gráfico de cauda longa](./media/app-insights-analytics-using/pin-07.png)

mas quando fixá-lo tooa painel, ele se parece com esta:

![Gráfico com compartimentos limitados](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>Exportar tooExcel
Depois de executar uma consulta, você pode baixar um arquivo .csv. Clique em **Exportar, Excel**.

## <a name="export-toopower-bi"></a>Exportar tooPower BI
Coloque o cursor de saudação em uma consulta e escolha **exportar, Power BI**.

![Exportar da análise tooPower BI](./media/app-insights-analytics-using/240.png)

Você executa a consulta de saudação no Power BI. Você pode definir toorefresh em uma agenda.

Com o Power BI, você pode criar painéis que reúnem dados de uma grande variedade de fontes.

[Saiba mais sobre exportação tooPower BI](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Link profundo

Obter um link em **exportação, o vínculo de compartilhamento** que você pode enviar tooanother usuário. Contanto que tenha o usuário Olá [grupo de recursos do acesso tooyour](app-insights-resources-roles-access-control.md), Olá consulta será aberta no hello análise da interface do usuário.

(No link hello, texto de consulta Olá aparece após "? q =", compactado gzip e codificado na base 64. Você pode escrever links profundos de toogenerate de código que você forneça toousers. No entanto, o hello recomendado é de maneira toorun análise de código usando Olá [API REST](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automação

Saudação de uso [API REST de acesso a dados](https://dev.applicationinsights.io/) toorun consultas de análise. [Por exemplo](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (usando o PowerShell):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

Ao contrário Olá análise da interface do usuário, Olá API REST não adiciona automaticamente as consultas de tooyour de limitação de carimbo de hora. Lembre-se de tooadd seu próprios-cláusula where, tooavoid receber respostas enormes.



## <a name="import-data"></a>Importar dados

Você pode importar dados de um arquivo CSV. Um uso típico é tooimport dados estáticos que você pode associar tabelas da sua telemetria. 

Por exemplo, se os usuários autenticados são identificados em sua telemetria por um alias ou id ofuscado, pode importar uma tabela que mapeia nomes de tooreal aliases. Executando uma junção em Telemetria de solicitação hello, você pode identificar os usuários por seus nomes reais em relatórios de análise de saudação.

### <a name="define-your-data-schema"></a>Definir o esquema de dados

1. Clique em **Configurações** (na parte superior esquerda) e, em seguida, **Fontes de dados**. 
2. Adicione uma fonte de dados, seguindo as instruções de saudação. Será solicitado toosupply uma amostra de dados hello, que devem incluir pelo menos dez linhas. Você, em seguida, corrija o esquema hello.

Isso define uma fonte de dados, em seguida, você pode usar tabelas individuais tooimport.

### <a name="import-a-table"></a>Importar uma tabela

1. Abra sua definição de fonte de dados da lista de saudação.
2. Clique em "Carregar" e siga a tabela de Olá Olá instruções tooupload. Isso envolve tooa uma chamada de API REST e por isso, é fácil tooautomate. 

A tabela agora está disponível para uso em consultas de análise. Ele aparecerá na análise 

### <a name="use-hello-table"></a>Use a tabela de saudação

Vamos supor que a definição de fonte de dados é chamada `usermap` e que ela possui dois campos, `realName` e `user_AuthenticatedId`. Olá `requests` tabela também tem um campo chamado `user_AuthenticatedId`, portanto, é fácil toojoin-los:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
a tabela resultante de solicitações Hello tem uma coluna adicional, `realName`.

### <a name="import-from-logstash"></a>Importar do LogStash

Se você usar [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), você pode usar a análise tooquery seus logs. Saudação de uso [plug-in que canaliza os dados para análise de](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

