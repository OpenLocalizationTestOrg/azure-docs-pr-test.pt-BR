---
title: "dados de aaaFind com pesquisas de log na análise de Log do Azure | Microsoft Docs"
description: "Pesquisas de log permitem toocombine e correlacionam dados de computador de várias fontes em seu ambiente."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Localizar dados usando as pesquisas de logs no Log Analytics

>[!NOTE]
> Este artigo descreve as pesquisas de log usando a linguagem de consulta atual Olá na análise de Log.  Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você deve referir-se muito[log Noções básicas sobre pesquisa na análise de Log (novo)](log-analytics-log-search-new.md).


Saudação de núcleo da análise de Log é recurso de pesquisa de log de saudação que permite que você toocombine e correlacionar dados de várias fontes em seu ambiente de máquina. As soluções também são alimentadas pela toobring de pesquisa de log, você as métricas que giram em torno de uma área de problema específica.

Na página de pesquisa hello, você pode criar uma consulta e, em seguida, quando você pesquisa, você pode filtrar os resultados de saudação usando controles da faceta. Você também pode criar consultas avançadas tootransform, filtrar e relatar seus resultados.

As consultas de pesquisa de log comuns aparecem na maioria das páginas de solução. Em todo o console do OMS hello, você pode clicar em blocos ou fazer uma busca de itens tooother tooview detalhes sobre o item de saudação usando a pesquisa de log.

Neste tutorial, examinaremos exemplos toocover todas as Noções básicas de hello quando você usar a pesquisa de log.

Vamos começar com exemplos práticos, simples e desenvolvê-los para que você pode obter um entendimento dos casos de uso prático sobre insights de saudação do toouse Olá sintaxe tooextract de dados de saudação.

Depois que você estiver familiarizado com as técnicas de pesquisa, você pode examinar Olá [referência de pesquisa de log de análise de Log](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Usar filtros básicos
Olá primeiro tooknow faz Olá primeira parte de uma consulta de pesquisa, antes de qualquer "|" caractere de barra vertical, é sempre uma *filtro*. Você pode pensar nela como uma cláusula WHERE em TSQL: ela determina *que* subconjunto de dados toopull fora do repositório de dados do OMS hello. Pesquisar no repositório de dados de saudação é se basicamente de especificar as características de saudação dos dados de saudação que você deseja tooextract, portanto, é natural que uma consulta deva começar com hello cláusula WHERE.

Olá filtros mais básicos que você pode usar são *palavras-chave*, como 'error' ou 'tempo limite' ou um nome de computador. Esses tipos de consultas simples normalmente retornam diversas formas de dados dentro de saudação mesmo conjunto de resultados. Isso ocorre porque a análise de Log tem diferentes *tipos* dos dados no sistema de saudação.

### <a name="tooconduct-a-simple-search"></a>tooconduct uma pesquisa simples
1. No portal do OMS hello, clique em **pesquisa de Log**.  
    ![pesquisar bloco](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. No campo de consulta hello, digite `error` e, em seguida, clique em **pesquisa**.  
    ![pesquisar erro](./media/log-analytics-log-searches/oms-search-error.png)  
    Por exemplo, a consulta Olá para `error` na Olá a imagem a seguir retornou 100.000 **evento** registros (coletados pelo gerenciamento de logs), 18 **ConfigurationAlert** (gerados pela configuração de registros Avaliação) e 12 **ConfigurationChange** registros (capturados pelo Olá controle de alterações).   
    ![pesquisar resultados](./media/log-analytics-log-searches/oms-search-results01.png)  

Esses filtros não são realmente tipos/classes de objeto. *Tipo* é uma marca ou uma propriedade ou uma cadeia de caracteres/nome/categoria, que é anexado tooa parte dos dados. Alguns documentos no sistema de saudação são marcados como **Type: ConfigurationAlert** e alguns são marcados como **tipo: desempenho**, ou **Type: Event**, e assim por diante. Cada resultado da pesquisa, documento, registro ou entrada exibe todas as propriedades de saudação bruto e seus valores para cada uma dessas partes de dados, e você pode usar esses toospecify de nomes de campo no filtro de saudação quando desejar que somente os registros Olá tooretrieve onde o campo Olá tiver aquele valor.

*Type* é realmente apenas um campo que existe em todos os registros; ele não é diferente de qualquer outro campo. Isso foi estabelecido com base no valor de saudação do campo de tipo de saudação. Esse registro terá uma forma diferente. Por acaso, **tipo = Perf**, ou **tipo = evento** também é Olá sintaxe que você precisa toolearn tooquery para dados de desempenho ou eventos.

Você pode usar dois pontos (:) ou um sinal de igual (=) após o nome do campo hello e antes do valor de saudação. **Type: Event** e **tipo = evento** são equivalentes em significado, você pode escolher Olá estilo desejado.

Portanto, se hello, digite = Perf registros têm um campo chamado 'CounterName', em seguida, você pode escrever uma consulta semelhante `Type=Perf CounterName="% Processor Time"`.

Isso lhe dará apenas dados de desempenho de saudação onde o nome do contador de desempenho de saudação é "% Processor Time".

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch para dados de desempenho de tempo do processador
* No campo de consulta de pesquisa hello, digite`Type=Perf CounterName="% Processor Time"`

Você também pode ser mais específico e usar **InstanceName = _ 'Total'** na consulta hello, que é um contador de desempenho do Windows. Você também pode selecionar uma faceta e outro **field:value**. filtro de saudação é adicionado automaticamente tooyour filtro na barra de consulta hello. Você pode ver isso em Olá a imagem a seguir. Ela mostra onde tooclick tooadd **InstanceName: total'** toohello consulta sem digitar nada.

![pesquisar faceta](./media/log-analytics-log-searches/oms-search-facet.png)

A sua consulta agora se torna `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

Neste exemplo, você não tem toospecify **tipo = Perf** tooget toothis resultados. Como Olá campos CounterName e InstanceName existem somente para registros do tipo = Perf, consulta Olá é específica o suficiente tooreturn Olá mesmos resultados como Olá anterior, mais longa:

```
CounterName="% Processor Time" InstanceName="_Total"
```

Isso ocorre porque todos os filtros de saudação na consulta Olá são avaliados como estando em *e* uns com os outros. Efetivamente, hello mais campos você adicionar toohello critérios, você obtém menor, mais específicos e refinados são os resultados.

Por exemplo, a consulta de saudação `Type=Event EventLog="Windows PowerShell"` é idêntico muito`Type=Event AND EventLog="Windows PowerShell"`. Retorna todos os eventos que foram registrados no e coletados do log de eventos do Windows PowerShell hello. Se você adicionar um filtro várias vezes selecionando repetidamente Olá mesma faceta, em seguida, problema de saudação é apenas superficial: ele pode sobrecarregar a barra de pesquisa hello, mas ainda retorna Olá mesmos resultados porque o operador AND implícito de saudação sempre está lá.

Você pode facilmente reverter o operador AND implícito de saudação usando um operador NOT explicitamente. Por exemplo:

`Type:Event NOT(EventLog:"Windows PowerShell")`ou seu equivalente `Type=Event EventLog!="Windows PowerShell"` retornar todos os eventos de todos os outros logs que não são de log do Windows PowerShell hello.

Você pode usar outro operador booliano, como 'OR'. consulta a seguir de saudação retorna registros para qual Olá no log de eventos é um sistema ou aplicativo.

```
EventLog=Application OR EventLog=System
```

Usando Olá acima de consulta, você obterá as entradas para ambos os logs em Olá mesmo conjunto de resultados.

No entanto, se você remover hello ou deixando Olá AND implícito no lugar, em seguida, hello consulta a seguir não produzirá resultados porque não existe uma entrada de log de eventos que pertença tooBOTH logs. Cada entrada de log de eventos foi escrita tooonly um dos dois logs de saudação.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Usar filtros adicionais
Olá, consulta a seguir retorna entradas de logs de evento 2 para todos os computadores de saudação que enviaram dados.

```
EventLog=Application OR EventLog=System
```

![pesquisar resultados](./media/log-analytics-log-searches/oms-search-results03.png)

A seleção de um dos campos de saudação ou filtros restringirá Olá consulta tooa computador específico, excluindo todos os outros. consulta resultante Olá seria semelhante a seguir hello.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Que é o equivalente toohello seguinte, por causa de saudação and implícito.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Cada consulta é avaliada na ordem explícita de saudação. Parênteses de saudação de observação.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Assim como campo de log de eventos do hello, você pode recuperar dados apenas para um conjunto de computadores específicos adicionando ou. Por exemplo:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

Da mesma forma, este Olá retorno da consulta a seguir **% tempo de CPU** Olá selecionada apenas dois computadores.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Tipos de campo
Ao criar filtros, você deve compreender as diferenças de saudação ao trabalhar com tipos diferentes de campos retornados pelas pesquisas de log.

**Campos de pesquisa** aparecem em azul nos resultados da pesquisa.  Você pode usar os campos de pesquisa no campo de toohello específico de condições de pesquisa como seguinte hello:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**Campos de pesquisa de texto livre** são mostrados em cinza nos resultados da pesquisa.  Eles não podem ser usados com o campo de toohello específico de condições de pesquisa como campos de pesquisa.  Eles apenas são pesquisados ao executar uma consulta em todos os campos, como a seguir hello.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Operadores boolianos
Com campos numéricos e de datetime, você pode procurar por valores usando *maior que*, *menor que* e *menor ou igual*. Você pode usar operadores simples como >, <>, =, < =,! = na barra de pesquisa de consulta hello.

Você pode consultar um log de eventos específico para um período de tempo específico. Por exemplo, Olá últimas 24 horas é indicada com hello mnemônico expressão a seguir.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>toosearch usando um operador booliano
* No campo de consulta de pesquisa hello, digite`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![pesquisar com booliano](./media/log-analytics-log-searches/oms-search-boolean.png)

Embora você possa controlar Olá graficamente o intervalo de tempo e a maioria das vezes, você poderá toodo, há vantagens tooincluding um filtro de tempo diretamente na consulta de saudação. Por exemplo, isso funciona muito bem com painéis em você pode substituir o tempo de saudação para cada bloco, independentemente de saudação *global* seletor de tempo na página do painel de saudação. Para saber mais, confira [Assuntos de tempo no Painel](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Ao filtrar por tempo, tenha em mente que você obter resultados de saudação *interseção* de saudação dois períodos de tempo: Olá especificada no portal do OMS hello (S1) e Olá especificado na consulta de saudação (S2).

![interseção](./media/log-analytics-log-searches/oms-search-intersection.png)

Isso significa que, se hello períodos de tempo não se cruzarem, por exemplo no portal do OMS Olá em que você escolhe **esta semana** e na consulta Olá onde você define **última semana**, não haverá nenhuma interseção e você não receba todos os resultados.

Operadores de comparação usados para o campo de TimeGenerated Olá também são úteis em outras situações. Por exemplo, com campos numéricos.

Por exemplo, considerando que os alertas de avaliação de configuração têm Olá valores de severidade a seguir:

* 0 = Informações
* 1= Aviso
* 2 = Crítico

Você pode consultar alertas de avisos e críticos e também excluir os informativos com hello consulta a seguir:

```
Type=ConfigurationAlert  Severity>=1
```


Você também pode usar consultas de intervalo. Isso significa que você pode fornecer o intervalo de início e término hello dos valores em uma sequência. Por exemplo, se você deseja os eventos do log de eventos do Operations Manager Olá onde hello EventID é too2100 maior que ou igual, mas não é maior que 2199, em seguida, Olá consulta a seguir retornaria esses resultados.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> sintaxe de intervalo de saudação, você deve usar é o separador de valor de campo de dois-pontos (:) hello e *não* Olá sinal de igual (=). Inclua a fim de Olá inferior e superior do intervalo de saudação entre colchetes e separe-as com dois pontos (.).
>
>

## <a name="manipulate-search-results"></a>Manipular resultados da pesquisa
Quando você estiver procurando por dados, você deseja toorefine a consulta de pesquisa e ter um bom nível de controle sobre os resultados de saudação. Quando os resultados são recuperados, você pode aplicar comandos tootransform-los.

Comandos em pesquisas de análise de Log *deve* vir após o caractere de barra vertical (|) do hello. Um filtro sempre deve ser Olá primeira parte de uma cadeia de caracteres de consulta. Ele define Olá conjunto de dados que você está trabalhando e "canaliza" esses resultados em um comando. Você pode usar comandos do hello pipe tooadd adicionais. Isso é vagamente semelhante pipeline do Windows PowerShell de toohello.

Em geral, a saudação linguagem de pesquisa de análise de Log tenta toofollow toomake de estilo e as diretrizes do PowerShell it semelhante toohello IT profissionais e a curva de aprendizado tooease hello.

Comandos têm nomes de verbos para que você possa perceber facilmente o que eles fazem.  

### <a name="sort"></a>Classificar
comando de classificação Olá permite Olá toodefine ordem por um ou vários campos de classificação. Mesmo se você não usá-lo, por padrão, a ordem imposta é decrescente por tempo. resultados mais recentes de saudação são sempre na parte superior da saudação dos resultados da pesquisa. Isso significa que quando você executa uma pesquisa com `Type=Event EventID=1234` , o que realmente é executado para você é:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Isso ocorre porque é o tipo de saudação da experiência que conhecer nos logs. Por exemplo, no Visualizador de eventos do Windows hello.

Você pode usar classificar resultados de maneira Olá toochange são retornados. Olá exemplos a seguir mostram como isso funciona.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Olá exemplos simples acima mostram como os comandos funcionam: eles alteram a forma Olá de resultados Olá Olá filtro retornado.

### <a name="limit-and-top"></a>Limite e superior
Outro comando menos conhecido é LIMITE. O limite é um verbo do tipo do PowerShell. Limite é o comando superior toohello funcionalmente idênticos. Olá consultas a seguir retornam Olá mesmos resultados.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>toosearch usando top
* No campo de consulta de pesquisa hello, digite`Type=Event EventID=600 | Top 1`   
    ![pesquisar superior](./media/log-analytics-log-searches/oms-search-top.png)

Imagem de saudação acima, há 358 mil registros com EventID = 600. Olá campos, facetas e filtros de saudação à esquerda sempre mostram informações sobre Olá resultados retornados *pela parte de filtro Olá* de consulta de saudação, que faz parte de saudação antes de qualquer caractere de pipe. Olá **resultados** painel somente retorna o resultado de saudação 1 mais recente, pois o comando de exemplo hello moldou e transformou os resultados de saudação.

### <a name="select"></a>Selecionar
comando SELECT Olá se comporta como Select-Object no PowerShell. Ele retorna resultados filtrados que não têm todas as suas propriedades originais. Em vez disso, ele seleciona somente as propriedades de saudação que você especificar.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun uma pesquisa usando o comando select Olá
1. Na pesquisa, digite `Type=Event` e clique em **Pesquisar**.
2. Clique em **+ Mostrar mais** em uma saudação resultados tooview tem todas as propriedades de Olá Olá resultados.
3. Selecione alguns deles explicitamente e hello alterações de consulta muito`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![pesquisar selecionar](./media/log-analytics-log-searches/oms-search-select.png)

Esse comando é particularmente útil quando você deseja toocontrol saída de pesquisa e escolhe apenas as partes de saudação de dados que realmente importam para exploração, que geralmente não é registro completo de saudação. Isso também é útil quando os registros de tipos diferentes têm *algumas* propriedades em comum, mas não *todas*. Você pode gerar uma saída mais naturalmente parecida com uma tabela ou funciona bem quando exportada tooa arquivo CSV e processada no Excel.

## <a name="use-hello-measure-command"></a>Use o comando de medida Olá
MEDIDA é um dos comandos de hello mais versáteis em pesquisas de análise de Log. Ele permite que você tooapply estatística *funções* tooyour dados e agregue os resultados agrupados por um determinado campo. Há várias funções estatísticas que têm suporte de Medida.

### <a name="measure-count"></a>Contagem de medida()
Olá toowork de primeira função estatística com, e uma das toounderstand mais simples de saudação é Olá *contagem* função.

Os resultados de qualquer consulta de pesquisa, como `Type=Event`, mostram filtros também chamados de facetas Olá lado esquerdo de resultados da pesquisa. Olá filtros mostram uma distribuição de valores por um determinado campo para resultados Olá Olá pesquisa executada.

![pesquisar contagem de medida](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Por exemplo, Olá imagem anteriormente, você verá Olá **computador** campo e ele mostra que, em Olá quase 739 mil eventos resultados hello, há 68 valores exclusivos e distintos para Olá **computador** campo nesses registros. Olá bloco mostra somente Olá 5 principais, que são Olá 5 valores mais comuns que são escritos em Olá **computador** campos), classificados pelo número de saudação de documentos que contêm esse valor específico nesse campo. Na imagem hello, você pode ver que, dentre os quase 369 mil eventos, 90 mil vêm de computador Olá OpsInsights04.contoso.com 83 mil do computador de DB03.contoso.com Olá e assim por diante.

Se quiser toosee todos os valores, como Olá bloco mostra somente Olá apenas 5 principais?

Que é quais medidas Olá comando pode fazer com a função de contagem () do hello. Essa função não usa nenhum parâmetro. Você simplesmente especifica Olá campo pelo qual você deseja toogroup por – Olá **computador** campo nesse caso:

`Type=Event | Measure count() by Computer`

![pesquisar contagem de medida](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

No entanto, **Computer** é somente um campo usado *em* cada porção de dados — nenhum banco de dados relacional está envolvido e não há nenhum objeto **Computer** separado em lugar algum. Olá apenas valores *na* Olá dados podem descrever qual entidade gerou, além de várias outras características e aspectos dos dados hello –, portanto, Olá termo *faceta*. No entanto, você pode também agrupar por outros campos. Como resultados de Olá originais de quase 739 mil eventos que foram canalizados para o comando de medida Olá também têm um campo chamado **EventID**, você pode aplicar Olá mesmo toogroup técnica por esse campo e obter uma contagem de eventos por EventID:

```
Type=Event | Measure count() by EventID
```

Se você não estiver interessado na contagem de registro real Olá que contêm um valor específico, mas em vez disso, se você desejar apenas uma lista de saudação os valores, você pode adicionar uma *selecione* comando final Olá-lo e simplesmente selecione Olá primeira coluna:

```
Type=Event | Measure count() by EventID | Select EventID
```

Em seguida, você pode obter resultados mais complexos e classificar previamente os resultados de saudação consulta hello, ou você pode simplesmente clicar Olá colunas na grade de saudação muito.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch usando contagem de medida
* No campo de consulta de pesquisa hello, digite`Type=Event | Measure count() by EventID`
* Acrescentar `| Select EventID` toohello final da consulta de saudação.
* Por fim, acrescente `| Sort EventID asc` toohello final da consulta de saudação.

Há algumas toonotice de pontos importantes e a enfatizar:

Primeiro, Olá resultados não são resultados brutos originais do hello mais. Em vez disso, eles são resultados agregados: essencialmente, grupos de resultados. Isso não é um problema, mas você deve entender o que você está interagindo com uma forma muito diferente de dados que é diferente da saudação forma bruta original que é criada em Olá rapidamente como resultado da função de agregação/estatística hello.

Segundo, **medidas de contagem** atualmente retorna apenas Olá top 100 resultados distintos. Esse limite não se aplica toohello outras funções estatísticas. Assim, você geralmente precisará toouse um toosearch primeiro do filtro mais preciso para itens específicos antes de aplicar contagem de medida.

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Usar as funções máx e mín Olá com o comando de medida Olá
Há várias situações em que**Measure Max()** e **Measure Min()** são úteis. No entanto, já que elas são opostas, vamos exemplificar Máx() e você pode testar Mín() por conta própria.

Se você consultar eventos de segurança, eles têm uma propriedade de **nível** que pode variar. Por exemplo:

```
Type=SecurityEvent
```

![pesquisar início da contagem de medida](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Se você quiser valor mais alto de saudação tooview de segurança Olá todos os eventos de um mesmo computador, grupo de saudação por campo, você pode usar

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![pesquisar medir máxima computador](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Ela exibirá isso para computadores de saudação que tinham **nível** registros, a maioria deles ter pelo menos 8, o nível muitas tinham um nível de 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![pesquisar tempo máximo gerado computador](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Essa função funciona bem com números, mas também funciona com campos de data e hora. É útil toocheck para Olá última ou carimbo de hora mais recente de qualquer parte dos dados indexados para cada computador. Por exemplo: quando os eventos de segurança mais recentes da saudação foi relatados para cada máquina?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Use a função de média de saudação com o comando de medida Olá
Olá função estatística Méd (), usada com medidas permite que você toocalculate Olá valor médio alguns campos e grupo resultados por Olá mesmo ou outro campo. Isso é útil em muitos casos, como dados de desempenho.

Vamos começar com os dados de desempenho. Observe que o OMS atualmente coleta contadores de desempenho para computadores Windows e Linux.

toosearch para *todos os* dados de desempenho, consulta mais básica Olá é:

```
Type=Perf
```

![pesquisar média início](./media/log-analytics-log-searches/oms-search-avg01.png)

Olá primeira coisa que você pode notar é que a análise de Log mostra três perspectivas: lista, que mostra que mostra os registros reais Olá atrás de gráficos Olá; Tabela, que mostra uma exibição tabular dos dados do contador de desempenho; e métricas, que mostra gráficos para Olá contadores de desempenho.

Imagem de saudação acima, há dois conjuntos de campos marcados que indicam a seguir hello:

* Olá primeiro conjunto identifica o nome de contador de desempenho do Windows, o nome do objeto e o nome da instância no filtro de consulta hello. Esses são os campos de saudação que provavelmente serão mais comumente usados como facetas/filtros
* **CounterValue** é o valor real de saudação do contador de saudação. Neste exemplo, o valor de saudação é *75*.
* **TimeGenerated** é 12:51, no formato de 24 horas.

Aqui está um modo de exibição das métricas de saudação em um gráfico.

![pesquisar média início](./media/log-analytics-log-searches/oms-search-avg02.png)

Depois de ler sobre a forma de registro de desempenho hello e ler sobre outras técnicas de pesquisa, você pode usar esse tipo de dados numéricos medida tooaggregate Avg ().

Eis um exemplo simples:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![pesquisar média valordeexemplo](./media/log-analytics-log-searches/oms-search-avg03.png)

Neste exemplo, você pode selecionar contador de desempenho de tempo Total de CPU hello e média por computador. Se você quiser toonarrow inativo saudação de tooonly seus resultados últimas 6 horas, você pode usar o controle de filtro de tempo de saudação ou especificar em sua consulta, da seguinte maneira:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>toosearch usando a função de média de saudação com o comando de medida Olá
* Na caixa de consulta de pesquisa hello, digite `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

Você pode agregar e correlacionar dados *entre* computadores. Por exemplo, imagine que você tenha um conjunto de hosts em algum tipo de farm onde cada nó é igual tooany outro e que apenas fazer todas as Olá mesmo tipo de trabalho e a carga deve ser balanceada por aproximação. Você pode obter seus contadores que todos sigam com hello seguinte consulta e obtenha as médias para toda a farm hello. Você pode iniciar escolhendo computadores Olá com hello exemplo a seguir:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Agora que você tiver computadores hello, você só deseja tooselect dois indicadores chave de desempenho (KPIs): % de uso de CPU e % espaço livre em disco. Portanto, se torna parte da consulta hello:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

Agora você pode adicionar computadores e contadores com hello exemplo a seguir:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Como você tem uma seleção muito específica, Olá **medir Méd ()** comando pode retornar Olá média não por computador, mas pelo farm hello, simplesmente agrupando por CounterName. Por exemplo:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Isso dá a você uma visualização compacta útil de alguns dos KPIs do seu ambiente.

![pesquisar média agrupamento](./media/log-analytics-log-searches/oms-search-avg04.png)

Facilmente, você pode usar consultas de pesquisa de saudação em um painel. Por exemplo, você pode salvar consulta de pesquisa de saudação e criar um painel de chamado *Web Farm KPIs*. toolearn mais sobre como usar os painéis, consulte [criar um painel personalizado em análise de Log](log-analytics-dashboards.md).

![pesquisar média painel](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Usar a função de soma de saudação com o comando de medida Olá
função de soma de saudação é funções tooother semelhantes de comando de medida hello. Você pode ver um exemplo sobre como toouse Olá a função de soma em [pesquisa de Logs do IIS W3C no Insights operacionais do Microsoft Azure](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

Você pode usar Máx() e Mín() com números, datetimes e cadeias de caracteres de texto. Com cadeias de caracteres de texto, eles são classificados em ordem alfabética e você obtém a primeira e a última.

No entanto, você não pode usar Soma() com algo diferente de campos numéricos. Isso também se aplica a tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Use a função de percentil de saudação com o comando de medida Olá
função de percentil Hello é semelhante tooAvg() e SUM () em que você só pode ser usada para campos numéricos. Você pode usar qualquer percentil entre 1 too99 em um campo numérico. Você também pode usar os comandos **percentile** e **pct**. Veja alguns exemplos:  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Use Olá onde comando
Olá onde o comando funciona como um filtro, mas ele pode ser aplicado no filtro de toofurther pipeline Olá agregado resultados que foram produzidos pelo comando medir, como tooraw contrário resultados filtrados no início de saudação de uma consulta.

Por exemplo:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

Você pode adicionar outro pipe "|" hello e caractere em que o comando tooonly obter computadores cuja média de CPU é acima de 80%, com hello exemplo a seguir:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Se você estiver familiarizado com o Microsoft System Center - Operations Manager, você pode pensar Olá onde o comando em termos de pacote de gerenciamento. Se uma regra de exemplo hello, Olá primeira parte da consulta Olá seria hello e fonte de dados Olá onde o comando seria a detecção de condição hello.

Você pode usar a consulta hello como um bloco em **meu painel**, como um monitor de classificações, toosee ao computador CPUs são utilizadas em excesso. toolearn mais sobre painéis, consulte [criar um painel personalizado em análise de Log](log-analytics-dashboards.md). Você também pode criar e usar painéis utilizando o aplicativo móvel hello. Para saber mais, veja [Aplicativo móvel do OMS ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). Olá dois blocos inferiores da saudação imagem a seguir, você pode ver Olá monitor exibindo uma lista e como um número. Essencialmente, você sempre deseja Olá número toobe zero e Olá lista toobe vazio. Caso contrário, isso indica uma condição de alerta. Se necessário, você pode usar tootake uma olhada em quais computadores estão sob pressão.

![painel móvel](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Saudação de uso no operador
Olá *na* operador, juntamente com *NOT IN* permite que você toouse subpesquisas, que são as pesquisas que incluem outra pesquisa como um argumento. Elas estão contidas em chaves {} dentro de outra pesquisa *primária* ou *externa*. resultado de saudação de uma subpesquisa, muitas vezes uma lista de resultados distintos, em seguida, é usado como um argumento em sua pesquisa primária.

Você pode usar subpesquisas toomatch subconjuntos de dados que você não pode descrever diretamente em uma expressão de pesquisa, mas que podem ser gerados por uma pesquisa. Por exemplo, se você estiver interessado em usar um toofind de pesquisa todos os eventos de *computadores com atualizações de segurança ausentes*, em seguida, você precisa toodesign uma subpesquisa que identifique primeiro *computadores com atualizações de segurança ausentes*  antes de encontrar eventos que pertencem toothose hosts.

Portanto, você pode expressar *atualizações de segurança de computadores atualmente com ausentes necessárias* com hello consulta a seguir:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Exemplo de pesquisa IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Uma vez que a lista de saudação, você pode usar a pesquisa de saudação como uma lista de saudação do toofeed de pesquisa interna de computadores em uma pesquisa (primária) externa que procurará por eventos para esses computadores. Você pode fazer isso envolve a pesquisa interna Olá em chaves e alimentar os resultados como valores possíveis para um filtro/campo na pesquisa externa hello, usando o operador de IN hello. Olá consulta seria semelhante a:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Exemplo de pesquisa IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Também o tempo de saudação do aviso de filtro usado na pesquisa interna Olá porque Olá avaliação de atualização do sistema tira um instantâneo de todos os computadores a cada 24 horas. Você pode fazer consulta interna hello mais simples e precisa apenas procurando por um dia. pesquisa externa Olá usa em vez disso, seleção de tempo de saudação na interface de usuário hello, recuperando os eventos de saudação últimos 7 dias. Confira [Operadores boolianos](#boolean-operators) para saber mais sobre operadores de tempo.

Porque você só use Olá os resultados de pesquisa interna de saudação como um valor de filtro para Olá externa, você ainda poderá aplicar comandos na pesquisa externa hello. Por exemplo, você ainda pode Olá grupo acima eventos com outro comando de medida:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Exemplo de pesquisa IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

Em geral, convém tooexecute sua consulta interna rapidamente porque a análise de Log tem tempos limite do lado do serviço para ele e também tooreturn uma pequena quantidade de resultados. Se a consulta interna Olá retorna mais resultados, lista de resultados de saudação é truncada, o que poderia potencialmente fazer Olá pesquisa externa tooreturn resultados incorretos.

Outra regra é que a pesquisa de saudação interna atualmente precisa tooprovide *agregados* resultados. Em outras palavras, ela deve conter um comando *measure*. Atualmente, você não pode alimentar uma pesquisa externa com resultados brutos.

Além disso, pode haver apenas um operador IN e ele deve ser Olá último filtro na consulta de saudação. Vários operadores IN não podem ser ou – isso basicamente impede a execução de várias subpesquisas: Olá importante ponto é que apenas uma pesquisa interna/subpesquisa é possível para cada pesquisa externa.

Mesmo com esses limites, o IN permite vários tipos de pesquisas correlacionadas e permite que você toodefine toogroups algo semelhante, como computadores, usuários ou arquivos – quaisquer campos Olá em seus dados contêm. Veja mais alguns exemplos:

**Todas as atualizações ausentes em computadores em que a configuração de Atualização Automática está desabilitada**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Todos os eventos de erro de computadores que estejam executando o SQL Server (=onde a Avaliação do SQL foi executada)**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Todos os eventos de segurança a partir de computadores que sejam Controladores de Domínio (= onde a Avaliação do AD foi executada)**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Que outras contas fizerem logon nos toohello mesmos computadores em que a conta BACONLAND\jochan fez logon?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Use o comando distinto Olá
Como Olá nome sugere, esse comando fornece uma lista de valores distintos para um campo. É surpreendentemente simples, mas muito útil. Olá que mesmo também pode ser obtido com o comando de contagem de medida, assim como mostrado abaixo.

```
Type=Event | Measure count() by Computer
```

![Exemplo de comando de pesquisa DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

No entanto, se você estiver interessado em apenas uma lista de valores distintos e não Olá contagem de documentos que tenham que valores, em seguida, DISTINCT pode fornecer tooread limpa e fáceis de saída e sintaxes mais curtas, conforme mostrado abaixo.

```
Type=Event | Distinct Computer
```
![Exemplo de comando de pesquisa DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Use a função de countdistinct de saudação com o comando de medida Olá
função countdistinct de saudação conta o número de saudação de valores distintos dentro de cada grupo. Por exemplo, pode ser usado toocount Olá número de computadores exclusivos de relatório para cada tipo:

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Use o comando de intervalo de medida Olá
Com a coleta de dados de desempenho em tempo real, você pode coletar e visualizar qualquer contador de desempenho no Log Analytics. Basta inserir consulta de saudação **tipo: desempenho** retornará milhares de gráficos de métricas com base no número de saudação de contadores e servidores em seu ambiente de análise de Log. Com a agregação de métrica sob demanda, você pode examinar Olá métricas gerais no ambiente em um alto nível e mergulho no dados mais granulares, conforme necessário.

Digamos que você deseja tooknow novidades Olá média de CPU em todos os computadores. Olhando Olá média de CPU para cada computador pode não ser útil porque os resultados podem obter amenizados. toolook para obter mais detalhes, você pode agregar o resultado em um menor tempo de blocos de janela e aparência em uma série de tempo entre diferentes dimensões. Por exemplo, você pode executar média por hora de saudação do uso de CPU em todos os computadores da seguinte maneira:

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![intervalo médio de medidas](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

Por padrão, esses resultados serão exibidos em um gráfico de linhas interativo com várias séries.  Esse gráfico oferece suporte à alternância de séries (com o redimensionamento do eixo y), ao zoom e à focalização.  opção de exibição de tabela Olá ainda está disponível para exibir dados brutos hello, se necessário.

Você também pode agrupar por outros campos. Neste exemplo, vou analisar todos os contadores de % Olá para um computador específico e desejo tooknow novidades percentuais de saudação 70 por hora de cada contador:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Toonote de uma coisa é que essas consultas não estão limitado tooperformance contadores. Você pode aplicá-los tooany métrica. Neste exemplo, examinarei os logs do IIS W3C. Quero tooknow o que é o tempo máximo de saudação que ele assume um intervalo de 5 minutos para cada solicitação de processamento:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Usar várias agregações em uma consulta
Você pode especificar várias cláusulas agregadas em um comando de medida.  Cada uma delas pode ter um alias de forma independente.  Se não for especificado um resultante de saudação do alias nome do campo será a função de agregação de saudação que foi usada (ou seja, "avg(CounterValue)" para avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Veja outro exemplo:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Próximas etapas
Para obter outras informações sobre pesquisas de log, veja:

* Use [campos personalizados na análise de Log](log-analytics-custom-fields.md) tooextend pesquisas de log.
* Saudação de revisão [referência de pesquisa de log de análise de Log](log-analytics-search-reference.md) tooview todos Olá Pesquisar campos e facetas disponíveis na análise de Log.
