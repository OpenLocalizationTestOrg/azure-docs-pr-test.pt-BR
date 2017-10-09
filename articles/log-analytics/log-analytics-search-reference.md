---
title: "referência de pesquisa de análise de Log de aaaAzure | Microsoft Docs"
description: "referência de pesquisa de análise de Log Olá descreve a linguagem de pesquisa hello e fornece opções de sintaxe de consulta geral Olá que você pode usar ao procurar dados e filtrar expressões toohelp restringir sua pesquisa."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Referência da pesquisa do Log Analytics

>[!NOTE]
> Este artigo descreve as pesquisas de log usando a linguagem de consulta atual Olá na análise de Log.  Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você deve referir-se muito[Olá referência de linguagem para a nova linguagem de saudação](https://go.microsoft.com/fwlink/?linkid=856079).

Olá seguinte seção de referência sobre linguagem de pesquisa descreve opções de sintaxe de consulta geral Olá que você pode usar ao procurar dados e filtrar expressões toohelp restringir sua pesquisa. Ele também descreve os comandos que você pode usar a ação tootake sobre Olá dados recuperados.

Você pode ler sobre Olá campos retornados nas pesquisas e facetas Olá ajudarão-lo a descobrir mais sobre categorias semelhantes de dados, em Olá [seção de referência de faceta e campo de pesquisa](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Sintaxe de consulta geral
sintaxe de saudação para consultar geral é o seguinte:

```
filterExpression | command1 | command2 …
```

Olá a expressão de filtro (`filterExpression`) define Olá Olá condição "where" para a consulta. comandos de saudação aplicam toohello resultados retornados pela consulta hello. Vários comandos devem ser separados pelo caractere de pipe de saudação (|).

### <a name="general-syntax-examples"></a>Exemplos de sintaxe geral
Exemplos:

```
system
```

Essa consulta retorna resultados que contêm a palavra hello *sistema* em qualquer campo que tenha sido indexado por texto completo ou de termos de pesquisa.

> [!NOTE]
> Nem todos os campos são indexados dessa maneira, mas hello mais comum de campos textuais (como nomes e descrições) normalmente são.
>
>

```
system error
```

Essa consulta retorna resultados que contêm palavras Olá *sistema* e *erro*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Essa consulta retorna resultados que contêm palavras Olá *sistema* e *erro*. Em seguida, classifica os resultados de saudação pelo Olá *ManagementGroupName* campo (em ordem crescente) e, em seguida, por Olá *TimeGenerated* campo (em ordem decrescente). Ele usa Olá somente 10 primeiros resultados.

> [!IMPORTANT]
> Olá a todos os nomes de campos e valores de saudação para campos de cadeia de caracteres e o texto de saudação diferenciam maiusculas de minúsculas.
>
>

## <a name="filter-expressions"></a>Expressões de filtro
Olá subseções a seguir explica as expressões de filtro hello.

### <a name="string-literals"></a>Literais de cadeia de caracteres
Um literal de cadeia de caracteres é qualquer cadeia de caracteres que não é reconhecida pelo analisador hello como uma palavra-chave ou um tipo de dados predefinido (por exemplo, um número ou data).

Exemplos:

```
These all are string literals
```

Essa consulta pesquisa resultados que contenham ocorrências de todas as cinco palavras. tooperform uma pesquisa de cadeia de caracteres complexa, coloque a cadeia de caracteres de saudação literal entre aspas. Por exemplo:

```
"Windows Server"
```

Isso retorna somente os resultados com correspondências exatas para *Windows Server*.

### <a name="numbers"></a>Números
Analisador de saudação dá suporte a inteiros decimais hello e sintaxe de número de ponto flutuante para campos numéricos.

Exemplos:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Datas e horas
Cada parte dos dados no sistema de saudação tem um *TimeGenerated* propriedade, que representa a data original hello e a hora de registro de saudação. Alguns tipos de dados podem ter mais campos de data e hora (por exemplo, *LastModified*).

Olá cronograma **gráfico/hora** seletor no Azure Log Analytics mostra uma distribuição de resultados ao longo do tempo (acordo toohello consulta atual que está sendo executada). Isso se baseia na Olá *TimeGenerated* campo. Campos de data e hora têm um formato de cadeia de caracteres específica que pode ser usado em consultas toorestrict Olá consulta tooa determinado período. Você também pode usar a sintaxe toorefer toorelative intervalos de tempo (por exemplo, "entre 3 dias atrás e 2 horas atrás").

Olá seguem formulários válidos de sintaxe para datas e horas:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


Por exemplo:

```
TimeGenerated:2013-10-01T12:20
```

comando de saudação anterior retorna somente os registros com um *TimeGenerated* valor de exatamente 12:20 em 1º de outubro de 2013.

Olá analisador também dá suporte ao valor de data/hora mnemônico hello, agora. (É improvável que isso produzirá resultados, porque os dados não passam pelo sistema de saudação tão rápido.)

Esses exemplos são blocos de construção toouse para datas relativas e absolutas. Em Olá próximas três subseções, você verá como toouse-los em mais avançados filtros, com exemplos que usam intervalos de datas relativas.

### <a name="datetime-math"></a>Cálculos de data/hora
Use Olá toooffset de operadores de matemática de data/hora ou arredondar o valor de data/hora hello usando cálculos simples de data/hora.

Sintaxe:

```
datetime/unit
```

```
datetime[+|-]count unit
```

| Operador | Descrição |
| --- | --- |
| / |Arredonda data/hora toohello especificado unidade. Por exemplo, agora / dia Arredonda Olá toomidnight de data/hora atual do hello dia atual. |
| + ou - |Deslocamentos de data/hora Olá número especificado de unidades. Por exemplo, NOW + 1HOUR desloca Olá atual data/hora por uma hora à frente. 2013-10-01t12: 00-10DAYS desloca o valor de data de saudação em 10 dias. |

Você pode encadear os operadores de matemática de data/hora Olá juntos. Por exemplo:

```
NOW+1HOUR-10MONTHS/MINUTE
```

Olá tabela a seguir lista Olá suporte para unidades de data/hora.

| Unidade de data/hora | Descrição |
| --- | --- |
| YEAR, YEARS |Arredonda toocurrent ano ou deslocamentos por Olá número especificado de anos. |
| MONTH, MONTHS |Arredonda toocurrent mês ou deslocamentos por Olá número especificado de meses. |
| DAY, DAYS, DATE |Dia de toocurrent turnos de mês de saudação ou deslocamentos de saudação número especificado de dias. |
| HOUR, HOURS |Arredonda toocurrent hora ou deslocamentos por Olá número especificado de horas. |
| MINUTE, MINUTES |Arredonda toocurrent minuto ou deslocamentos por Olá número especificado de minutos. |
| SECOND, SECONDS |Arredonda toocurrent segundo ou desloca pelo Olá especificado número de segundos. |
| MILLISECOND, MILLISECONDS, MILLI, MILLIS |Milissegundos de toocurrent turnos ou deslocamentos de saudação número especificado de milissegundos. |

### <a name="field-facets"></a>Facetas de campo
Usando as facetas de campo, você pode especificar o critério de pesquisa Olá para campos específicos e seus valores exatos. Isso é diferente de escrever consultas com "texto livre" para vários termos em todo o índice de saudação. Você já viu essa técnica em vários exemplos anteriores. Olá seguem exemplos mais complexos.

**Sintaxe**

```
field:value
```

```
field=value
```

**Descrição**

Pesquisas Olá campo valor específico de saudação. valor de saudação pode ser uma cadeia de caracteres literal, o número, ou a data e a hora.

Por exemplo:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Sintaxe**

*campo>valor*

*campo<valor*

*campo>=valor*

*campo<=valor*

*campo!=valor*

**Descrição**

Fornece comparações.

Por exemplo:

```
TimeGenerated>NOW+2HOURS
```

**Sintaxe**

```
field:[from..to]
```

**Descrição**

Fornece facetamento de intervalo.

Por exemplo:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
Olá **IN** palavra-chave permite que você tooselect em uma lista de valores. Dependendo da sintaxe de saudação usada, isso pode ser uma lista simple de valores que você fornecer, ou uma lista de valores de uma agregação.

Sintaxe 1:

```
field IN {value1,value2,value3,...}
```

Essa sintaxe permite que você tooinclude todos os valores em uma lista simples.



Exemplos:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Sintaxe 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Essa sintaxe permite que você toocreate uma agregação. Você pode, em seguida, feed lista Olá dos valores provenientes dessa agregação em outra pesquisa (primária) externa que procurará eventos com esses valores. Você pode fazer isso envolve a pesquisa interna Olá em chaves e alimentar os resultados como valores possíveis para um campo na pesquisa externa hello usando o operador de IN hello.

Exemplo de consulta interna: *computadores, atualizações de segurança ausentes no momento* com hello consulta de agregação a seguir:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

Olá final de consulta que encontra *todos os eventos do Windows para computadores, atualizações de segurança ausentes no momento* semelhante Olá seguinte:

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contém:
Olá **contém** palavra-chave permite que você toofilter para registros com um campo que contém uma cadeia de caracteres especificada. Isso diferencia maiusculas de minúsculas, funciona somente com campos de cadeia de caracteres e não pode incluir qualquer caractere de escape.

Sintaxe:

```
field:contains("string")
```

Exemplo:

```
Type:contains("Event")
```

Isso retorna registros com um tipo que contém a cadeia de caracteres hello "Evento". Os exemplos incluem **evento**, **SecurityEvent**, e **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Expressões regulares
Você pode especificar um critério de pesquisa para um campo com uma expressão regular, usando Olá **Regex** palavra-chave. Para obter uma descrição completa da sintaxe de saudação, você pode usar em expressões regulares, consulte [usando pesquisas de log de toofilter de expressões regulares na análise de Log](log-analytics-log-searches-regex.md).

Sintaxe:

```
field:Regex("Regular Expression")
```

Exemplo:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Operadores lógicos
consulta Olá idiomas oferecem suporte a operadores lógicos hello (*AND*, *ou*, e *não*) e seus aliases de estilo C (*&&*,  *||* , e *!*, respectivamente). Você pode usar parênteses toogroup esses operadores.

Exemplos:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

Você pode omitir o operador lógico de saudação para argumentos de filtro de nível superior de saudação. Nesse caso, a saudação operador AND será assumida.

| Expressão do filtro... | Equivalente muito|
| --- | --- |
| erro do sistema |erro do sistema AND |
| sistema "Windows Server" OR Gravidade: 1 |sistema AND (“Windows Server” OR Gravidade: 1) |

### <a name="wildcarding"></a>Recurso de curinga
linguagem de consulta Olá oferece suporte ao uso de saudação ( \* ) caractere muito representam um ou mais caracteres para um valor em uma consulta.

Exemplo:

 Localize todos os computadores com "SQL" no nome de saudação, como "Redmond-SQL".

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> Neste momento, os caracteres curinga não podem ser usados entre aspas. Por exemplo, a mensagem de saudação `"*This text*"` considera hello (\*) usado como um literal (\*) caracteres.


## <a name="commands"></a>Comandos


comandos de saudação aplicam toohello resultados retornados pela consulta hello. Use Olá pipe (|) de caractere tooapply toohello um comando recuperar resultados. Vários comandos devem ser separados pelo caractere de pipe de saudação.

> [!NOTE]
> Nomes de comando podem ser escritos em letras maiusculas ou minúsculas, ao contrário de nomes de campo hello e dados saudação.
>
>

### <a name="sort"></a>Classificar
Sintaxe:

    sort field1 asc|desc, field2 asc|desc, …

Classifica os resultados de saudação por campos específicos. resultados de saudação do Hello crescente/decrescente sufixo toosort em ordem crescente ou decrescente é opcional. Se ele for omitido, Olá *asc* ordem de classificação é assumida. Para Olá **TimeGenerated** campo, *desc* ordem de classificação será assumida, para que ela retorne resultados mais recentes Olá primeiro por padrão.

### <a name="toplimit"></a>Superior/limite
Sintaxe:

    top number


    limit number
Limites Olá resposta toohello primeiros N resultados.

Exemplo:

    Type:Alert errors detected | top 10

Retorna Olá 10 principais resultados correspondentes.

### <a name="skip"></a>Skip
Sintaxe:

    skip number

Ignora Olá número de resultados listados.

Exemplo:

    Type:Alert errors detected | top 10 | skip 200

Retorna os 10 primeiros resultados de correspondência, começando no resultado 200.

### <a name="select"></a>Selecionar
Sintaxe:

    select field1, field2, ...

Limita os campos de toohello resultados escolhidos.

Exemplo:

    Type:Alert errors detected | select Name, Severity

Limites Olá campos de resultados retornados muito*nome* e *severidade*.

### <a name="measure"></a>Medida
Olá *medidas* comando é usado tooapply funções estatísticas toohello brutos da pesquisa resultados. Isso é muito útil tooget *Agrupar por* exibições dados saudação. Quando você usa o comando de medida hello, pesquisa de análise de Log exibe uma tabela com resultados agregados.

**Sintaxe:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Agrega os resultados de saudação por *groupField*e calcula os valores de medida Olá agregado usando *aggregatedField*.

| Função estatística Medida | Descrição |
| --- | --- |
| *aggregateFunction* |nome de Olá Olá da função de agregação (não diferencia maiusculas de minúsculas). Olá, funções de agregação a seguir têm suporte: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, percentil # # ou PCT # # (# # é qualquer número entre 1 e 99). |
| *aggregatedField* |campo de saudação que está sendo agregado. Este campo é opcional para Olá função de agregação COUNT, mas tem toobe um campo numérico existente para SUM, MAX, MIN, AVG, STDDEV, percentil # # ou PCT # # (# # é qualquer número entre 1 e 99). Olá aggregatedField também pode ser Olá **estender** funções com suporte. |
| *fieldAlias* |alias (opcional) Olá Olá calculado valor agregado. Se não for especificado, o nome do campo Olá é **AggregatedValue**. |
| *groupField* |saudação de nome de campo de saudação do conjunto de resultados de saudação é agrupada. |
| *Intervalo* |intervalo de tempo de saudação, no formato de saudação:**Nnnnome**. **nnn**é um número inteiro positivo de saudação. **NOME** é o nome do intervalo de saudação. Os nomes de intervalo com suporte fazem distinção entre maiúsculas e minúsculas e incluem: MILLISECOND[S] SECOND[S] MINUTE[S] HOUR[S] DAY[S] MONTH[S] e YEAR[S]. |

opção de intervalo de saudação somente pode ser usada em campos de grupo de data/hora (como *TimeGenerated* e *TimeCreated*). Atualmente, isso não é imposto pelo serviço hello, mas um campo sem data/hora que é passado toohello back-end causará um erro em tempo de execução. Quando a validação de esquema Olá é implementada, Olá API do serviço rejeita as consultas que usam campos sem data/hora para agregação de intervalo. Olá atual *medidas* implementação oferece suporte a agrupamento de intervalo para qualquer função de agregação.

Se Olá BY cláusula for omitida, mas um intervalo for especificado (como uma segunda sintaxe), Olá *TimeGenerated* será considerado por padrão.

Exemplos:

**Exemplo 1**

    Type:Alert | measure count() as Count by ObjectId

Grupos Olá alertas por *ObjectID*e calcula o número de saudação de alertas para cada grupo. Olá valor agregado é retornado como Olá *contagem* campo (alias).

**Exemplo 2**

    Type:Alert | measure count() interval 1HOUR

Grupos Olá alertas por intervalos de 1 hora usando Olá *TimeGenerated* campo e retorna o número de saudação de alertas em cada intervalo.

**Exemplo 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Mesmo que o exemplo anterior hello, mas com um alias de campo agregado (*AlertsPerHour*).

**Exemplo 4**

    * | measure count() by TimeCreated interval 5DAYS

Agrupa os resultados de saudação em intervalos de 5 dias usando Olá *TimeCreated* campo e retorna o número de saudação de resultados em cada intervalo.

**Exemplo 5**

    Type:Alert | measure max(Severity) by WorkflowName

Grupos Olá alertas por cargas de trabalho e retorna Olá valor máximo de severidade de alerta para cada fluxo de trabalho.

**Exemplo 6**

    Type:Alert | measure min(Severity) by WorkflowName

Igual ao exemplo anterior hello, mas com hello *min* função de agregação.

**Exemplo 7**

    Type:Perf | measure avg(CounterValue) by Computer

Grupos de desempenho por computador e calcula Olá média (média).

**Exemplo 8**

    Type:Perf | measure sum(CounterValue) by Computer

Mesmo que o exemplo anterior de saudação, mas usa *soma*.

**Exemplo 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Mesmo que o exemplo anterior de saudação, mas usa *stddev*.

**Exemplo 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Mesmo que o exemplo anterior de saudação, mas usa *percentile70*.

**Exemplo 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Mesmo que o exemplo anterior de saudação, mas usa *pct70*. Observe que *PCT##* é apenas um alias para a função *PERCENTILE##*.

**Exemplo 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Agrupa Perf primeiro por computador e, em seguida, CounterName e calcula Olá média (média).

**Exemplo 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Obtém a saudação principais cinco fluxos de trabalho com o número máximo de saudação de alertas.

**Exemplo 14**

    * | measure countdistinct(Computer) by Type

Conta o número de saudação de emissão de relatórios para cada tipo de computadores exclusivos.

**Exemplo 15**

    * | measure countdistinct(Computer) Interval 1HOUR

Conta o número de saudação de computadores exclusivos de relatório para cada hora.

**Exemplo 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

Grupos de % tempo do processador por computador e retorna a média de saudação para cada hora.

**Exemplo 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

Agrupa W3CIISLog pelo método e retorna Olá máximo para cada 5 minutos.

**Exemplo 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Grupos % tempo do processador por computador e retorna Olá mínimo, média, 75th percentil e máximo para cada hora.

**Exemplo 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Grupos % tempo do processador primeiro por computador e depois por instância nome e o mínimo de saudação retorna, média, 75th percentil e máximo para cada hora.

**Exemplo 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Calcula o máximo de saudação de gravações de disco por minuto para cada disco no computador.

### <a name="where"></a>Where
Sintaxe:

```
**where** AggregatedValue>20
```

Só pode ser usado após uma *medidas* Olá de filtro do comando toofurther agregado resultados que Olá *medidas* produziu.

Exemplos:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Dedup
Sintaxe:

    Dedup FieldName

Retorna Olá documento primeiro encontrado para cada valor exclusivo de Olá dado do campo.

Exemplo:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

Este exemplo retorna um evento (evento mais recente da saudação) por EventID.

### <a name="join"></a>Ingressar
Junções Olá resultados de duas consultas tooform um único conjunto de resultados.  Dá suporte a vários tipos de junção descritos na Olá seguem a tabela.

| Tipo de junção | Descrição |
|:--|:--|
| interna | Retorna somente os registros com um valor correspondente em ambas as consultas. |
| externa | Retorna todos os registros de ambas as consultas.  |
| esquerda  | Retorna todos os registros de consulta à esquerda e os registros correspondentes de consulta à direita. |


- Junções atualmente não dão suporte a consultas que incluem hello **na** palavra-chave, Olá **medidas** comando ou hello **estender** comando se ele se destina a um campo de consulta de saudação à direita.
- No momento, você pode incluir apenas um único campo em uma junção.
- Uma única pesquisa pode não incluir mais de uma junção.

**Sintaxe**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**Exemplos**

tipos de junção diferentes do tooillustrate Olá, considere a possibilidade de ingressar em um tipo de dados coletados de um log personalizado chamado MyBackup_CL heartbeat Olá para cada computador.  Esses tipos de dados têm Olá dados a seguir.

`Type = MyBackup_CL`

| TimeGenerated | Computador | LastBackupStatus |
|:---|:---|:---|
| 20/04/2017 01:26:32.137 AM | srv01.contoso.com | Sucesso |
| 20/04/2017 02:13:12.381 AM | srv02.contoso.com | Sucesso |
| 20/04/2017 02:13:12.381 AM | srv03.contoso.com | Failure |

`Type = Hearbeat`(Apenas um subconjunto dos campos mostrados)

| TimeGenerated | Computador | ComputerIP |
|:---|:---|:---|
| 21/04/2017 12:01:34.482 PM | srv01.contoso.com | 10.10.100.1 |
| 21/04/2017 12:02:21.916 PM | srv02.contoso.com | 10.10.100.2 |
| 21/04/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>junção interna

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Olá retorna registros a seguir em que o campo de saudação do computador corresponde para ambos os tipos de dados.

| Computador| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 20/04/2017 01:26:32.137 AM | Sucesso | 21/04/2017 12:01:34.482 PM | 10.10.100.1 | Pulsação |
| srv02.contoso.com | 20/04/2017 02:13:12.381 AM | Sucesso | 21/04/2017 12:02:21.916 PM | 10.10.100.2 | Pulsação |


#### <a name="outer-join"></a>junção externa

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Olá retorna registros para ambos os tipos de dados a seguir.

| Computador| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 20/04/2017 01:26:32.137 AM | Sucesso  | 21/04/2017 12:01:34.482 PM | 10.10.100.1 | Pulsação |
| srv02.contoso.com | 20/04/2017 02:14:12.381 AM | Sucesso  | 21/04/2017 12:02:21.916 PM | 10.10.100.2 | Pulsação |
| srv03.contoso.com | 20/04/2017 01:33:35.974 AM | Failure  | 21/04/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 21/04/2017 12:01:47.373 PM | 10.10.100.2 | Pulsação |



#### <a name="left-join"></a>associação à esquerda

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Retorna a saudação seguir registros de MyBackup_CL com todos os campos correspondentes de pulsação.

| Computador| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 20/04/2017 01:26:32.137 AM | Sucesso | 21/04/2017 12:01:34.482 PM | 10.10.100.1 | Pulsação |
| srv02.contoso.com | 20/04/2017 02:13:12.381 AM | Sucesso | 21/04/2017 12:02:21.916 PM | 10.10.100.2 | Pulsação |
| srv03.contoso.com | 20/04/2017 02:13:12.381 AM | Failure | | | |


### <a name="extend"></a>Extend
Permite que você toocreate campos de tempo de execução em consultas. Observe que os campos de tempo de execução não podem ser usados com a agregação de tooperform de comando de medida hello.

**Exemplo 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Mostra a pontuação de recomendação ponderada para as recomendações da Avaliação do SQL

**Exemplo 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Mostrar o valor do contador em KBs em vez de bytes

**Exemplo 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Escalas Olá valor de WireData TotalBytes, de modo que todos os resultados estão entre 0 e 100.

**Exemplo 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Marcar os Valores do Contador de Desempenho de menos de 50% como BAIXO e outros como ALTO

**Exemplo 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Calcula o máximo de saudação de gravações de disco por minuto para cada disco no computador.

**Funções com suporte**

| Função | Descrição | Exemplos de sintaxe |
| --- | --- | --- |
| abs |Retorna um valor absoluto Olá de saudação especificado valor ou função. |`abs(x)` <br> `abs(-5)` |
| acos |Retorna o arco cosseno de um valor ou uma função. |`acos(x)` |
| e |Retorna um valor true se e somente se todos os seus operandos avaliarem tootrue. |`and(not(exists(popularity)),exists(price))` |
| asin |Retorna o arco seno de um valor ou uma função. |`asin(x)` |
| atan |Retorna o arco tangente de um valor ou uma função. |`atan(x)` |
| atan2 |Retorna o ângulo de saudação resultante da conversão de saudação de coordenadas retangulares de saudação coordenadas x, y toopolar. |`atan2(x,y)` |
| cbrt |Raiz cúbica. |`cbrt(x)` |
| ceil |Arredonda o tooan inteiro. |`ceil(x)`  <br> `ceil(5.6)` Retorna 6 |
| cos |Retorna o cosseno de um ângulo. |`cos(x)` |
| cosh |Retorna o cosseno hiperbólico de um ângulo. |`cosh(x)` |
| def |Abreviação de padrão. Retorna Olá valor do campo "field". Se o campo de saudação não existir, retorna o valor padrão de saudação especificado e produz Olá primeiro valor onde: `exists()==true`. |`def(rating,5)`. Esta função de def() retorna a classificação hello, ou se nenhuma classificação for especificada no documento hello, retornará 5. <br> `def(myfield, 1.0)`é o equivalente muito`if(exists(myfield),myfield,1.0)`. |
| deg |Converte radianos toodegrees. |`deg(x)` |
| div |`div(x,y)` divide x por y. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dist |Retorna a distância de saudação entre dois vetores, (pontos) em um espaço n-dimensional. Usa power hello, além de duas ou mais, instâncias ValueSource e calcula as distâncias Olá entre dois vetores de saudação. Cada ValueSource deve ser um número. Deve haver um número par de instâncias ValueSource passadas, e o método hello pressupõe que Olá primeira metade representa o primeiro vetor de saudação e Olá segunda metade representa o segundo vetor de saudação. |`dist(2, x, y, 0, 0)`Calcula a distância Euclidiana Olá entre (0,0) e (x, y) para cada documento. <br> `dist(1, x, y, 0, 0)`Calcula a distância de Manhattan (taxicab) Olá entre (0,0) e (x, y) para cada documento. <br> `dist(2,,x,y,z,0,0,0)` a distância Euclidiana entre (0,0,0) e (x,y,z) para cada documento.<br>`dist(1,x,y,z,e,f,g)` distância Manhattan entre (x,y,z) e (e,f,g), em que cada letra é um nome de campo. |
| exists |Retornará TRUE se qualquer membro do campo Olá existe. |`exists(author)`Retorna TRUE para qualquer documento que tem um valor no campo de "autor" hello.<br>`exists(query(price:5.00))` retornará TRUE se "price" corresponder a "5,00". |
| exp |O número de Euler retorna gerado toopower x. |`exp(x)` |
| floor |Arredonda para baixo tooan inteiro. |`floor(x)`  <br> `floor(5.6)` Retorna 5 |
| hypo |Retorna sqrt(sum(pow(x,2),pow(y,2))) sem estouro intermediário ou estouro negativo. |`hypo(x,y)`  <br> ` |
| if |Permite consultas de função condicional. Em `if(test,value1,value2)`, teste é ou refere-se o valor lógico tooa ou uma expressão que retorna um valor lógico (TRUE ou FALSE). `value1`é Olá valor retornado pela função hello se o teste retornar TRUE. `value2`é Olá valor retornado pela função hello se o teste retornar FALSE. Uma expressão pode ser qualquer função que gera valores boolianos. Ele também pode ser uma função que retorna valores numéricos, nesse caso o valor 0 é interpretado como falso ou retornar cadeias de caracteres, na qual cadeia de caracteres vazia caso é interpretado como falso. |`if(termfreq(cat,'electronics'),popularity,42)`Essa função verifica cada documento toosee se ele contém Olá termo "electronics" no campo cat de saudação. Se ele, Olá, em seguida, o valor do campo de popularidade Olá será retornado. Caso contrário, o valor de saudação de 42 será retornado. |
| linear |Implementa `m*x+c` , em que m e c são constantes e x é uma função arbitrária. Isso é equivalente a muito`sum(product(m,x),c)`, mas um pouco mais eficiente, pois ele é implementado como uma única função. |`linear(x,m,c) linear(x,2,4)` retorna `2*x+4` |
| ln |Log natural do hello retorna da saudação função especificada. |`ln(x)` |
| log |Retorna Olá log de função de base 10 da saudação especificada. |`log(x)   log(sum(x,100))` |
| map |Mapeia todos os valores de uma função de entrada x que se enquadram dentro de min e max, inclusive toohello específicos. máximo e mínimo de argumentos Olá devem ser constantes. padrão e o destino dos argumentos Olá podem ser constantes ou funções. Se o valor de saudação de x não estiver entre min e max, ou valor de saudação de x será retornado ou um valor padrão será retornado se for especificado como um 5º argumento. |`map(x,min,max,target) map(x,0,0,1)`Todos os valores de 0 too1 é alterado. Isso pode ser útil para lidar com valores padrão 0.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`Altera quaisquer valores entre 0 e 100 too1 e todos os outros valores muito-1.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Altera quaisquer valores entre 0 e 100 toox + 599 e todos os outros toofrequency valores do termo Olá 'solr' no texto de saudação do campo. |
| max |Retorna um valor numérico máximo de várias funções aninhadas ou constantes, que são especificadas como argumentos de Olá: `max(x,y,...)`. função max Olá também pode ser útil para "chegar ao valor mínimo" outra função ou campo em alguma constante especificada.  Saudação de uso `field(myfield,max)` sintaxe para selecionar Olá o valor máximo de um único campo de múltiplos valores. |`max(myfield,myotherfield,0)` |
| Min |Retorna um valor numérico mínimo de várias funções aninhadas de constantes, que são especificadas como argumentos de Olá: `min(x,y,...)`. função min de saudação também pode ser útil para fornecer um "limite superior" em uma função usando uma constante. Saudação de uso `field(myfield,min)` sintaxe para selecionar Olá o valor mínimo de um único campo de múltiplos valores. |`min(myfield,myotherfield,0)` |
| mod |Calcula o módulo de saudação da função hello x por y de função hello. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| ms |Retorna os milissegundos de diferença entre seus argumentos. As datas são relativa toohello POSIX ou Unix época, meia-noite de 1º de janeiro de 1970 UTC. Argumentos podem ser Olá nome de um TrieDateField indexado ou a matemática de data com base em uma data constante ou NOW. `ms()`é o equivalente muito`ms(NOW)`, o número de milissegundos desde a época de saudação. `ms(a)`Retorna o número de saudação de milissegundos desde a época de saudação que Olá argumento representa. `ms(a,b)`Retorna o número de saudação de milissegundos que b ocorre antes de a, que é `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| não |valor de saudação negada logicamente da saudação encapsulado função. |`not(exists(author))` TRUE somente quando `exists(author)` é false. |
| ou o |Uma disjunção lógica. |`or(value1,value2)` TRUE se value1 ou value2 for verdadeiro. |
| pow |Olá gera especificado toohello base especificado energia. `pow(x,y)`gera x toohello potência de y. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`Olá mesmo que sqrt. |
| product |Retorna Olá produto de vários valores ou funções, que são especificados em uma lista separada por vírgulas. `mul(...)` também pode ser usado como um alias para essa função. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |Executa uma função recíproca com `recip(x,m,a,b)` implementando `a/(m*x+b)`, em que m, a e b são constantes e x é uma função arbitrariamente complexa. Quando a e b são iguais e x>=0, essa função tem um valor máximo de 1 que cai conforme x aumenta. Aumentando o valor de saudação de uma simples b juntos resulta em um movimento da saudação função inteira tooa parte da curva de saudação. Essas propriedades podem tornar isso uma função ideal para impulsionar documentos mais recentes quando x for `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |Converte graus tooradians. |`rad(x)` |
| rint |Arredonda toohello inteiro mais próximo. |`rint(x)`  <br> `rint(5.6)` Retorna 6 |
| sin |Retorna o seno de um ângulo. |`sin(x)` |
| sinh |Retorna o seno hiperbólico de um ângulo. |`sinh(x)` |
| scale |Valores de escala da função hello x, que, de modo que eles se encaixam entre Olá especificado minTarget e o maxtarget, inclusive. implementação atual de saudação percorre todos Olá função valores tooobtain Olá min e max, para que ele pode escolher a escala correta hello. implementação de saudação atual não pode diferenciar quando documentos foram excluídos, ou documentos que não têm nenhum valor. Ela usa valores 0,0 para esses casos. Isso significa que se os valores forem normalmente todos maiores que 0,0, um pode ainda acabar com 0,0 como Olá toomap de valor mínimo do. Nesses casos, um apropriado `map()` função pode ser usada como um valor de tooa toochange 0,0 solução alternativa no intervalo real de hello, conforme mostrado aqui:`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Escalas Olá valores de x, de modo que todos os valores estão entre 1 e 2, inclusive. |
| sqrt |Retorna Olá quadrado raiz de saudação especificado valor ou função. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |Calcula a distância de saudação entre duas cadeias de caracteres. Usa a interface de StringDistance de verificador de ortografia do hello Lucene e dá suporte a todas as implementações de saudação disponíveis no pacote. Também permite que aplicativos tooplug seus próprios, por meio do recurso do Solr recursos de carregamento. strdist usa `(string1, string2, distance measure)`. Os valores possíveis para a medida de distância são:<ul><li>jw: Jaro-Winkler</li><li>edit: distância Levenstein ou de Edição</li><li>ngram: Olá NGramDistance, se especificado, poderá opcionalmente passar o tamanho de ngram Olá muito. O padrão é 2.</li><li>FQN: Nome de uma implementação da interface de StringDistance Olá de classe totalmente qualificado. Deve ter um construtor não arg.</li></ul> |`strdist("SOLR",id,edit)` |
| sub |Retorna x-y de `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Sum |Retorna Olá soma de vários valores ou funções, que são especificados em uma lista separada por vírgulas. `add(...)` pode ser usado como um alias para esta função. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Retorna o número de saudação de vezes termo Olá aparece no campo de saudação do documento. |termfreq(text,'memory') |
| tan |Retorna a tangente de um ângulo. |`tan(x)` |
| tanh |Retorna a tangente hiperbólica de um ângulo. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Campo de pesquisa e referência da faceta
Quando você usa dados de toofind de pesquisa de Log, os resultados exibem vários campos e facetas. Algumas das informações de saudação talvez não pareçam muito descritivas. Use Olá toohelp informações entender os resultados de saudação a seguir.

| Campo | Tipo de pesquisa | Descrição |
| --- | --- | --- |
| TenantId |Todos |Usou dados toopartition. |
| TimeGenerated |Todos |Usado toodrive Olá da linha do tempo, timeselectors (na pesquisa e em outras telas). Representa quando a porção de saudação de dados foi gerada (normalmente no agente de saudação). tempo de saudação é expresso no formato ISO e é sempre UTC. No caso de saudação de tipos que são baseados em instrumentação existente (ou seja, os eventos em um log), isso é normalmente hello tempo real que Olá entrada/linha/registro de log foi registrado em log. Para algumas das Olá outros tipos que são produzidos por meio de pacotes de gerenciamento ou na nuvem de saudação (por exemplo, as recomendações ou alertas), Olá tempo representa algo diferente. Este é o tempo de saudação quando essa nova porção de dados com um instantâneo de uma configuração de algum tipo foi coletada ou um recomendação/alerta foi gerado com base nele. |
| EventID |Evento |EventID no log de eventos do Windows hello. |
| EventLog |Evento |Log de eventos onde o evento Olá foi registrado pelo Windows. |
| EventLevelName |Evento |Crítico/aviso/informação/êxito |
| EventLevel |Evento |Valor numérico de crítico/aviso/informação/êxito (use EventLevelName em vez disso para consultas mais legíveis/mais fáceis). |
| SourceSystem |Todos |Onde Olá dados vêm (em termos de serviço no modo toohello anexar). Exemplos incluem o Microsoft System Center Operations Manager e o armazenamento do Azure. |
| ObjectName |PerfHourly |Nome de objeto de desempenho do Windows. |
| InstanceName |PerfHourly |Nomes da instância do contador de desempenho do Windows. |
| CounteName |PerfHourly |Nome do contador de desempenho do Windows. |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nome de exibição do objeto Olá direcionado por uma regra de coleta de desempenho no Operations Manager. Também pode ser o nome de exibição de saudação do hello objeto descoberto pelo Operational Insights ou contra o qual Olá alerta foi gerado. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nome para exibição do pai de saudação do pai de saudação (em uma relação de hospedagem dupla) do objeto de saudação direcionado por uma regra de coleta de desempenho no Operations Manager. Também pode ser o nome de exibição de saudação do hello objeto descoberto pelo Operational Insights ou contra o qual Olá alerta foi gerado. |
| Computador |Maioria dos tipos |Nome do computador que dados saudação pertencem. |
| DeviceName |ProtectionStatus |Dados de saudação do nome de computador muito pertencem (o mesmo que "Computador"). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Classificação de status de ameaça é uma representação numérica do status de ameaça hello. Códigos de resposta tooHTTP semelhante, classificação de saudação tem lacunas entre os números de saudação (motivo pelo qual nenhuma ameaça é 150 e não 100 ou 0), deixando espaço tooadd novos estados. Para um pacote cumulativo de atualizações de ameaça e status de proteção, a intenção de saudação é tooshow Olá pior estado que Olá computador esteve durante saudação período de tempo selecionada. Olá números classificam Olá diferentes estados, e você pode procurar o registro de saudação com maior número de saudação. |
| ThreatStatus |ProtectionStatus |Descrição do ThreatStatus, mapeia 1:1 com ThreatStatusRank. |
| TypeofProtection |ProtectionStatus |Produto antimalware detectado no computador de saudação: nenhum, ferramenta de remoção de Malware da Microsoft, Forefront e assim por diante. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |ID do HealthService para o agente deste computador. |
| HealthServiceId |Maioria dos tipos |ID do HealthService para o agente deste computador. |
| ManagementGroupName |Maioria dos tipos |Nome do grupo de gerenciamento para agentes anexados ao Operations Manager. Caso contrário, ele será nulo/vazio. |
| ObjectType |ConfigurationObject |O tipo (como em tipo/classe do pacote de gerenciamento do Operations Manager) para esse objeto descoberto pela avaliação de configuração do Log Analytics |
| UpdateTitle |RequiredUpdate |Nome da atualização de saudação encontrada não instalada. |
| PublishDate |RequiredUpdate |Quando a atualização de saudação foi publicada no Microsoft Update. |
| Servidor |RequiredUpdate |Dados de saudação do nome de computador muito pertencem (o mesmo que "Computador"). |
| Produto |RequiredUpdate |Produto Olá atualização aplica-se a. |
| UpdateClassification |RequiredUpdate |Tipo de atualização (por exemplo, o pacote cumulativo de atualizações ou service pack). |
| KBID |RequiredUpdate |ID do artigo KB que melhor descreve essa prática recomendada ou atualização. |
| WorkflowName |ConfigurationAlert |Nome da regra de saudação ou monitor que produziu o alerta de saudação. |
| Severity |ConfigurationAlert |Severidade do alerta de saudação. |
| Prioridade |ConfigurationAlert |Prioridade de alerta de saudação. |
| IsMonitorAlert |ConfigurationAlert |Esse alerta foi gerado por um monitor (true) ou por uma regra (false)? |
| AlertParameters |ConfigurationAlert |XML com parâmetros de saudação do alerta de análise de Log de saudação. |
| Contexto |ConfigurationAlert |XML com o contexto de saudação do alerta de análise de Log de saudação. |
| Carga de trabalho |ConfigurationAlert |Tecnologia ou carga de trabalho Olá alerta se refere. |
| AdvisorWorkload |Recomendações |Tecnologia ou carga de trabalho Olá recomendação se refere. |
| Descrição |ConfigurationAlert |Descrição do alerta (curta). |
| DaysSinceLastUpdate |UpdateAgent |Quantos dias atrás (relativo tooTimeGenerated desse registro) esse agente instalou qualquer atualização do Windows Server Update Service (WSUS) ou o Microsoft Update? |
| DaysSinceLastUpdateBucket |UpdateAgent |Com base em DaysSinceLastUpdate, uma categorização em buckets de tempo de quanto tempo atrás um computador teve instalada pela última vez qualquer atualização do WSUS/Microsoft Update |
| AutomaticUpdateEnabled |UpdateAgent |A verificação de atualização automática está habilitada ou desabilitada nesse agente? |
| AutomaticUpdateValue |UpdateAgent |É a atualização automática verificando conjunto tooautomatically download e instalar, somente baixar ou somente verificar? |
| WindowsUpdateAgentVersion |UpdateAgent |Número de versão do agente do Microsoft Update hello. |
| WSUSServer |UpdateAgent |A qual servidor WSUS se destina esse agente de atualização? |
| OSVersion |UpdateAgent |Versão do sistema operacional de saudação esse agente de atualização está em execução. |
| Nome |Recomendação, ConfigurationObjectProperty |Nome/título da recomendação hello, ou nome da propriedade de saudação da avaliação de configuração de análise de Log. |
| Valor |ConfigurationObjectProperty |Valor de uma propriedade da Avaliação de Configuração do Log Analytics. |
| KBLink |Recomendações |Artigo de toohello KB de URL que descreve essa prática recomendada ou atualização. |
| RecommendationStatus |Recomendações |As recomendações estão entre Olá poucos tipos cujos registros obtém índice de pesquisa toohello atualizado e não recém-adicionada. Esse status se altera se Olá recomendação está ativa/aberta ou se a análise de Log detectar que ele foi resolvido. |
| RenderedDescription |Evento |Descrição renderizada (texto reutilizado com parâmetros populados) de um evento do Windows. |
| ParameterXml |Evento |XML com parâmetros de saudação na seção de dados de saudação de um evento do Windows (como visto no Visualizador de eventos). |
| EventData |Evento |XML com a seção de dados inteiro de saudação de um evento do Windows (como visto no Visualizador de eventos). |
| Fonte |Evento |Origem do log de eventos que gerou o evento de saudação. |
| EventCategory |Evento |Categoria de evento de hello, diretamente do log de eventos do Windows hello. |
| UserName |Evento |Nome de usuário de evento do Windows hello (normalmente, NT AUTHORITY\LOCALSYSTEM). |
| SampleValue |PerfHourly |Valor médio para agregação por hora de saudação de um contador de desempenho. |
| Min |PerfHourly |Valor mínimo no intervalo de hora de saudação de uma agregação por hora do contador de desempenho. |
| max |PerfHourly |Valor máximo no intervalo de hora de saudação de uma agregação por hora do contador de desempenho. |
| Percentile95 |PerfHourly |Olá 95º valor de percentil para o intervalo de hora saudação de uma agregação por hora do contador de desempenho. |
| SampleCount |PerfHourly |Quantas amostras de contador de desempenho bruto foram tooproduce usado por hora de registro de agregação. |
| Ameaça |ProtectionStatus |Nome de malware encontrado. |
| StorageAccount |W3CIISLog |Log Olá da conta de armazenamento do Azure foi lido no. |
| AzureDeploymentID |W3CIISLog |ID de implantação do Azure do log de saudação do serviço de nuvem Olá pertence. |
| Função |W3CIISLog |A função do log de saudação do serviço de nuvem do Azure Olá pertence. |
| RoleInstance |W3CIISLog |RoleInstance da saudação função do Azure que Olá log pertence. |
| sSiteName |W3CIISLog |Site do IIS que Olá log pertence too(metabase notation); campo s-sitename de Olá no log original hello. |
| sComputerName |W3CIISLog |campo s-computername de Olá no log original hello. |
| sIP |W3CIISLog |Endereço IP do servidor Olá solicitação HTTP foi endereçado. campo s-ip de Olá no log original hello. |
| csMethod |W3CIISLog |Método HTTP (por exemplo, GET/POST) usado pelo cliente de saudação na solicitação HTTP de saudação. Olá cs-method no log original hello. |
| cIP |W3CIISLog |Solicitação HTTP de saudação do cliente IP endereço veio. campo de c-ip Olá no log original hello. |
| csUserAgent |W3CIISLog |Agente-usuário HTTP declarado pelo cliente hello (navegador ou de outra forma). Olá cs-user-agent no log original hello. |
| scStatus |W3CIISLog |Código de HTTP Status (por exemplo, 200/403/500) retornado pelo cliente de toohello do servidor de saudação. Olá cs-status no log original hello. |
| TimeTaken |W3CIISLog |Quanto tempo (em milissegundos) que a solicitação Olá levou toocomplete. campo de timetaken Olá no log original hello. |
| csUriStem |W3CIISLog |O Uri relativo (sem hospedar o endereço, ou seja, /search) que foi solicitado. campo de cs-uristem Olá no log original hello. |
| csUriQuery |W3CIISLog |Consulta URI. As consultas URI somente são necessárias para páginas dinâmicas, como as páginas ASP; portanto, esse campo geralmente contém um hífen para páginas estáticas. |
| sPort |W3CIISLog |Porta do servidor que Olá solicitação HTTP foi enviada (e que o IIS escuta, desde que ele a percebeu). |
| csUserName |W3CIISLog |Nome de usuário, autenticado, se a solicitação de saudação for autenticada e não anônima. |
| csVersion |W3CIISLog |Versão do protocolo HTTP usada na solicitação de saudação (por exemplo, HTTP/1.1). |
| csCookie |W3CIISLog |Informações de cookie. |
| csReferer |W3CIISLog |Esse usuário Olá última visitado do site. Esse site fornece um site atual de toohello do link. |
| csHost |W3CIISLog |Cabeçalho de host (por exemplo, 'www.mysite.com') que foi solicitado. |
| scSubStatus |W3CIISLog |Código de erro de substatus. |
| scWin32Status |W3CIISLog |Código de status do Windows. |
| csBytes |W3CIISLog |Bytes enviados na solicitação de saudação do servidor de toohello cliente hello. |
| scBytes |W3CIISLog |Bytes retornados em resposta de saudação do cliente de toohello do servidor de saudação. |
| ConfigChangeType |ConfigurationChange |Tipo de alteração (por exemplo, WindowsServices/Software). |
| ChangeCategory |ConfigurationChange |Categoria da alteração de saudação (modificado/adicionado/removido). |
| SoftwareType |ConfigurationChange |Tipo de software (Atualização/Aplicativo). |
| SoftwareName |ConfigurationChange |Nome do software de saudação (somente alterações toosoftware aplicável). |
| Editor |ConfigurationChange |Fornecedor que publica o software de saudação (somente alterações toosoftware aplicável). |
| SvcChangeType |ConfigurationChange |Tipo de alteração que foi aplicada em um serviço do Windows (estado/StartupType/caminho/ServiceAccount). Isso é aplicável tooWindows somente as alterações de serviço. |
| SvcDisplayName |ConfigurationChange |Nome para exibição do serviço de saudação que foi alterado. |
| SvcName |ConfigurationChange |Nome do serviço de saudação que foi alterado. |
| SvcState |ConfigurationChange |Novo (atual) estado do serviço de saudação. |
| SvcPreviousState |ConfigurationChange |Estado anterior conhecido do serviço de saudação (aplicável somente se o estado do serviço mudou). |
| SvcStartupType |ConfigurationChange |Tipo de inicialização do serviço. |
| SvcPreviousStartupType |ConfigurationChange |Tipo anterior de inicialização do serviço (aplicável somente se o tipo de inicialização de serviço for alterado). |
| SvcAccount |ConfigurationChange |Conta de serviço. |
| SvcPreviousAccount |ConfigurationChange |Conta de serviço anterior (aplicável somente se a conta de serviço for alterada). |
| SvcPath |ConfigurationChange |Executável de toohello do caminho do serviço do Windows hello. |
| SvcPreviousPath |ConfigurationChange |Caminho anterior do hello executável para Olá serviço do Windows (aplicável somente se ele for alterado). |
| SvcDescription |ConfigurationChange |Descrição do serviço de saudação. |
| Voltar |ConfigurationChange |Estado anterior do software (versão Instalada/Não Instalada/anterior). |
| Atual |ConfigurationChange |Estado mais recente do software (versão Instalada/Não Instalada/atual) |

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre pesquisas de log:

* Familiarize-se com [pesquisas de log](log-analytics-log-searches.md) tooview detalhadas informações coletadas por meio de soluções.
* Use [campos personalizados de análise de Log](log-analytics-custom-fields.md) tooextend pesquisas de log.
