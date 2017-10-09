---
title: "aaaHow tooBuild agendas complexos e recorrência avançadas com o Agendador do Azure"
description: "Como tooBuild complexo agenda e recorrência avançadas com o Agendador do Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Como tooBuild complexo agenda e recorrência avançadas com o Agendador do Azure
## <a name="overview"></a>Visão geral
Essência Olá um agendador do Azure o trabalho é hello *agenda*. agendamento de saudação determina quando e como Olá Agendador executa trabalho hello.

O Agendador do Azure permite que você toospecify única e recorrente cronogramas diferentes para um trabalho. Os agendamentos *únicos* são acionados uma vez em um momento especificado: na verdade, eles são agendamentos *recorrentes* que são executados somente uma vez. Os agendamentos recorrentes são acionados com uma frequência predeterminada.

Com essa flexibilidade, o Agendador do Azure permite que você dê suporte a uma ampla variedade de cenários de negócios:

* Limpeza periódica de dados: por exemplo, todos os dias, excluir todos os tweets com mais de três meses
* Arquivamento – por exemplo, cada mês, por push fatura histórico toobackup serviço
* Solicitações de dados externos: por exemplo, a cada 15 minutos, receber um novo relatório de previsão do tempo de Esqui da NOAA
* Imagem de processamento – por exemplo, cada dia da semana, fora do horário de pico, usar imagens de computação toocompress carregado naquele dia de nuvem

Neste artigo, percorreremos trabalhos de exemplo que você pode criar com o Agendador do Azure. Podemos fornecer dados JSON Olá que descreve cada agenda. Se você usar o hello [API REST do Agendador](https://msdn.microsoft.com/library/mt629143.aspx), você pode usar esse mesmo JSON para [criando um trabalho do Agendador do Azure](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Cenários com suporte
Olá que muitos exemplos neste tópico ilustram amplitude Olá dos cenários que dá suporte ao Agendador do Azure. Em larga escala, estes exemplos ilustram como toocreate agendas para vários padrões de comportamento, incluindo Olá aquelas abaixo:

* Executar uma vez em uma determinada data e hora
* Executar e repetir um número de vezes específico
* Executar imediatamente e repetir
* Executar e repetir a cada *n* minutos, horas, dias, semanas ou meses, começando em um momento específico
* Executar e repetir em frequência semanal ou mensal, mas somente em dias específicos, em dias da semana específicos ou em dias do mês específicos
* Executar e repetir várias vezes em um período: por exemplo, na última sexta-feira e segunda-feira de cada mês ou às 5h15 e 17h15 todos os dias

## <a name="dates-and-datetimes"></a>Datas e DateTimes
Execute as datas em trabalhos do Agendador do Azure Olá [especificação ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) e incluir apenas Olá Data.

Referências de data e hora em trabalhos do Agendador do Azure seguem Olá [ISO 8601 especificação](http://en.wikipedia.org/wiki/ISO_8601) e inclua as partes de data e hora. Uma data e hora que não especifica um deslocamento UTC será assumida toobe UTC.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Como usar JSON e API REST para criar agendamentos
Olá toocreate um agendamento simples usando [API de REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143), primeiro [registrar sua assinatura com um provedor de recursos](https://msdn.microsoft.com/library/azure/dn790548.aspx) (Olá nome do provedor para o Agendador é  *Microsoft.Scheduler*), em seguida, [criar uma coleção de trabalhos](https://msdn.microsoft.com/library/mt629159.aspx)e, finalmente, [criar um trabalho](https://msdn.microsoft.com/library/mt629145.aspx). Quando você cria um trabalho, você pode especificar o agendamento e a recorrência usando JSON como Olá um extraídas abaixo:

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Visão geral: Noções básicas sobre esquemas de trabalho
Olá, a tabela a seguir fornece uma visão geral de saudação elementos principais relacionados toorecurrence e agendar um trabalho:

| **Nome JSON** | **Descrição** |
|:--- |:--- |
| ***startTime*** |*startTime* é uma Data/Hora. Para agendamentos simples, *startTime* é a primeira ocorrência de saudação e para agendamentos complexos, trabalho Olá será iniciado sem antes do *startTime*. |
| ***recurrence*** |Olá *recorrência* objeto especifica regras de recorrência para trabalhos de saudação e Olá Olá de recorrência serão executada com. objeto de recorrência Olá dá suporte a elementos de saudação *frequência, intervalo, endTime, contagem,* e *agenda*. Se *recorrência* for definida, *frequência* é necessário; Olá outros elementos de *recorrência* são opcionais. |
| ***frequency*** |Olá *frequência* cadeia de caracteres que representa a unidade de frequência de saudação com quais Olá trabalho se repete. Os valores com suporte são *"minute", "hour", "day", "week"* ou *"month"*. |
| ***interval*** |Olá *intervalo* é um inteiro positivo e indica o intervalo de saudação para Olá *frequência* que determina com que frequência hello trabalho será executado. Por exemplo, se *intervalo* é 3 e *frequência* é "semana" trabalho Olá se repete a cada três semanas. O Agendador do Azure dá suporte a um valor máximo de *interval* de 18 meses para a frequência mensal, 78 semanas para a frequência semanal ou 548 dias para a frequência diária. De hora e minuto frequência, o intervalo de saudação com suporte é 1 < = *intervalo* < = 1000. |
| ***endTime*** |Olá *endTime* cadeia de caracteres Especifica Olá data e hora após a qual Olá trabalho não deve executar. Não é válido toohave um *endTime* em Olá anterior. Se nenhum *endTime* ou contagem é especificada, o trabalho Olá é executado infinitamente. Ambos *endTime* e *contagem* não podem ser incluídas para Olá mesmo trabalho. |
| ***count*** |<p>Olá *contagem* é um inteiro positivo (maior que zero) que especifica o número de saudação de vezes que esse trabalho deve ser executado antes da conclusão.</p><p>Olá *contagem* representa Olá o número de vezes que trabalho Olá é executado antes que está sendo determinado como concluída. Por exemplo, para um trabalho que é executado diariamente com *contagem* 5 e a data de início do segunda-feira, conclui o trabalho Olá após a execução na sexta-feira. Se iniciar Olá data está em Olá anterior, execução primeiro Olá é calculada de tempo de criação de saudação.</p><p>Se nenhum *endTime* ou *contagem* for especificado, o trabalho de saudação é executado infinitamente. Ambos *endTime* e *contagem* não podem ser incluídas para Olá mesmo trabalho.</p> |
| ***schedule*** |Um trabalho com uma frequência especificada altera sua recorrência com base em um agendamento de recorrência. Um elemento *schedule* contém as modificações com base em minutos, em horas, em dias da semana, em dias do mês e em número da semana. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Visão geral: padrões de esquema, limites e exemplos de trabalho
Após essa visão geral, vamos examinar cada um desses elementos em detalhes.

| **Nome JSON** | **Tipo de valor** | **Obrigatório?** | **Valor padrão** | **Valores válidos** | **Exemplo** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |Cadeia de caracteres |Não |Nenhum |Data e hora ISO 8601 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***recurrence*** |Objeto |Não |Nenhum |Objeto de recorrência |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequency*** |string |Sim |Nenhum |"minuto", "hora", "dia", "semana", "mês" |<code>"frequency" : "hour"</code> |
| ***interval*** |Número |Não |1 |1 too1000. |<code>"interval":10</code> |
| ***endTime*** |Cadeia de caracteres |Não |Nenhum |Valor de data e hora que representa uma hora no futuro de saudação |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***count*** |Número |Não |Nenhum |>= 1 |<code>"count": 5</code> |
| ***schedule*** |Objeto |Não |Nenhum |Objeto Agendamento |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Análise aprofundada: *startTime*
tabela a seguir Olá capturas como *startTime* controla como um trabalho é executado.

| **valor startTime** | **Sem recorrência** | **Recorrência. Sem agendamento** | **Recorrência com agendamento** |
|:--- |:--- |:--- |:--- |
| **Sem hora de início** |Executar uma vez imediatamente |Executar uma vez imediatamente. Fazer as execuções subsequentes com base no cálculo do tempo da última execução |<p>Executar uma vez imediatamente</p><p>Fazer as execuções subsequentes com base no agendamento de recorrência</p> |
| **Hora de início no passado** |Executar uma vez imediatamente |<p>Calcular a primeira hora de execução futura após a hora de início e executar naquela hora</p><p>Fazer as execuções subsequentes com base no cálculo da hora da última execução</p><p>Veja o exemplo depois desta tabela para obter uma explicação mais detalhada</p> |<p>Trabalho iniciado *não antes do* saudação inicial especificada. primeira ocorrência de saudação baseia-se a agenda Olá calculada a partir da hora de início da saudação</p><p>Fazer as execuções subsequentes com base no agendamento de recorrência</p> |
| **Hora de início no futuro ou no momento** |Executar uma vez na hora de início especificada |<p>Executar uma vez na hora de início especificada</p><p>Fazer as execuções subsequentes com base no cálculo do tempo da última execução</p> |<p>Trabalho iniciado *não antes do* saudação inicial especificada. primeira ocorrência de saudação baseia-se a agenda Olá calculada a partir da hora de início da saudação</p><p>Fazer as execuções subsequentes com base no agendamento de recorrência</p> |

Vamos ver um exemplo do que acontece onde *startTime* está em Olá anterior, com *recorrência* mas não *agenda*.  Suponha que Olá hora atual for 2015-04-08 13:00, *startTime* é 2015-04-07 14:00 e *recorrência* é a cada 2 dias (definida com *frequência*: dia e *intervalo*: 2.) Observe que Olá *startTime* está em Olá anterior e ocorre antes da saudação hora atual

Sob essas condições, Olá *primeira execução* será 2015-04-09 às 14:00\. o mecanismo agendador Olá calcula ocorrências de execução da hora de início da saudação.  Todas as instâncias no hello anterior são descartadas. mecanismo de saudação usa próxima ocorrência do hello que ocorre no hello futuras.  Portanto nesse caso, *startTime* é 2015-04-07 às 2:00, portanto, Olá próxima instância 2 dias a partir dessa hora, que é 2015-04-09 às 2:00.

Observe que a primeira execução do hello seria Olá mesmo mesmo se Olá startTime 2015-04-05 14:00 ou 14:00\ 2015-04-01. Após a execução da primeira hello, as execuções subsequentes são calculadas usando Olá agendada – portanto eles seriam em 2015-04-11 às 2:00, em seguida, 2015-04-13 às 2:00, em seguida, 2015-04-15 às 2:00, etc.

Finalmente, quando um trabalho tiver uma agenda, se as horas e/ou minutos não estão definidos na agenda hello, eles horas de toohello padrão e/ou minutos de primeira execução do hello, respectivamente.

## <a name="deep-dive-schedule"></a>Análise aprofundada: *schedule*
Por um lado, uma *agenda* pode *limite* Olá número de execuções de trabalho.  Por exemplo, se um trabalho com uma frequência de "mês" tem um *agenda* que são executados em um único dia 31, o trabalho Olá é executado em apenas esses meses que têm um 31<sup>st</sup> dia.

Olá por outro lado, uma *agenda* também pode *expanda* Olá número de execuções de trabalho. Por exemplo, se um trabalho com uma frequência de "mês" tem um *agenda* que é executada em dias do mês 1 e 2, Olá trabalho é executado em Olá 1<sup>st</sup> e 2<sup>nd</sup> dias do mês de saudação em vez de apenas uma vez um mês.

Se forem especificados vários elementos de programação, ordem de saudação de avaliação é de toosmallest maior hello – número da semana, dia, mês, dia da semana, hora e minuto.

Olá tabela a seguir descreve *agenda* elementos em detalhes.

| **Nome JSON** | **Descrição** | **Valores Válidos** |
|:--- |:--- |:--- |
| **minutos** |Minutos da hora de saudação na qual Olá trabalho será executado |<ul><li>Inteiro ou</li><li>Matriz de inteiros</li></ul> |
| **horas** |Horas do dia Olá no qual Olá trabalho será executado |<ul><li>Inteiro ou</li><li>Matriz de inteiros</li></ul> |
| **Dias da semana** |Dias de trabalho de Olá Olá semana serão executado. Só pode ser especificado com uma frequência semanal. |<ul><li>"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" ou "Sunday"</li><li>Matriz de qualquer um dos Olá acima valores (tamanho da matriz max 7)</li></ul>*Não* diferencia maiúsculas de minúsculas |
| **monthlyOccurences** |Determina quais dias de trabalho de Olá Olá mês serão executado. Só pode ser especificado com uma frequência mensal. |<ul><li>Matriz de objetos monthlyOccurrence:</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *dia* é o dia de saudação do trabalho de saudação do hello semana será executado, por exemplo, {domingo} é todo domingo do mês de saudação. Obrigatório.</p><p>A ocorrência é *ocorrência* do dia Olá durante o mês de hello, por exemplo, {domingo, -1} é Olá último domingo do mês de saudação. Opcional.</p> |
| **Dias do mês** |Dia de trabalho de Olá Olá mês será executado. Só pode ser especificado com uma frequência mensal. |<ul><li>Qualquer valor <= -1 e >= -31.</li><li>Qualquer valor >= 1 e <= 31.</li><li>Uma matriz dos valores acima</li></ul> |

## <a name="examples-recurrence-schedules"></a>Exemplos: agendamentos de recorrência
Olá seguem vários exemplos de agendas de recorrência – nos concentrarmos no objeto do cronograma hello e seus subelementos.

agendas abaixo todos Hello supõem que Olá *intervalo* está definido too1\. Além disso, um deve assumir a frequência de direito Olá no acordo toowhat está em Olá *agenda* – por exemplo, não é possível usar a frequência de "dia" e ter uma modificação "dias do mês" no agendamento de saudação. As restrições estão descritas acima.

| **Exemplo** | **Descrição** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |Executar às 5h da manhã todos os dias. O Agendador do Azure corresponde a cada valor em "horas" com cada valor em "minutos", um por um, toocreate uma lista de todos os tempos de saudação no qual Olá trabalho é toobe de execução. |
| <code>{"minutes":[15], "hours":[5]}</code> |Executar às 5:15 todos os dias |
| <code>{"minutes":[15], "hours":[5,17]}</code> |Executar às 5:15 e 17:15 todos os dias |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |Executar às 5:15, 5:45, 17:15 e 17:45 todos os dias |
| <code>{"minutes":[0,15,30,45]}</code> |Executar a cada 15 minutos |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Executar a cada hora. Esse trabalho é executado a cada hora. minuto de saudação é controlado pelo Olá *startTime*, se um for especificado ou se nenhum for especificado, por hora de criação de saudação. Por exemplo, se o início de saudação hora ou criação (o que for aplicável) é 12:25 PM, Olá trabalho será executado em 25-00:01:25, 02:25,..., 23:25. Olá agenda é equivalente toohaving um trabalho com *frequência* de "Hora", um *intervalo* de 1 e não *agenda*. Olá diferença é que esta agenda pode ser usada com diferentes *frequência* e *intervalo* toocreate outros trabalhos muito. Por exemplo, se hello *frequência* fosse "mês", Olá agenda será executada somente uma vez por mês, em vez de todos os dias se *frequência* foram "dia" |
| <code>{minutes:[0]}</code> |Execute a cada hora em Olá hora. Esse trabalho também será executado a cada hora, mas na hora da saudação (por exemplo, 12 AM, 1 hora, 2 horas etc.) Este é o trabalho tooa equivalente com frequência de "Hora", uma hora de início com zero minutos e nenhuma agenda se frequência hello "dia", mas se frequência hello "semana" ou "mês", agenda Olá seria executado somente um dia de uma semana ou um dia de um mês, respectivamente. |
| <code>{"minutes":[15]}</code> |Executar 15 minutos após a hora exata a cada hora. É executado a cada hora, começando em 00:15, 1:15, 2:15, etc. e terminando às 22:15 e 23:15. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |Executar às 17h aos sábados toda semana |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Executar às 17h às segundas-feiras, quartas-feiras e sextas-feiras toda semana |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Executar às 17:15 e 17:45 às segundas-feiras, quartas-feiras e sextas-feiras toda semana |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Executar às 5h e às 17h toda semana às segundas-feiras, quartas-feiras e sextas-feiras |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Executar às 5:15, 5:45, 17:15 e 17:45 às segundas-feiras, quartas-feiras e sextas-feiras toda semana |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Executar a cada 15 minutos em dias da semana |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Executar a cada 15 minutos nos dias úteis entre 9:00 e 16:45 |
| <code>{"weekDays":["sunday"]}</code> |Executar aos domingos na hora de início |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |Executar às terças e quintas-feiras na hora de início |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |Executar às 6: 00 em Olá 28 de dia de cada mês (supondo que a frequência do mês) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Execute às 6: 00 no último dia do mês de saudação do hello. Se você quiser toorun um trabalho em Olá último dia do mês, use -1 em vez de dia de 28, 29, 30 ou 31. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |Executar às 6: 00 em Olá primeiro e último dia de cada mês |
| <code>{monthDays":[1,-1]}</code> |Executar em Olá primeiro e último dia de cada mês na hora de início |
| <code>{monthDays":[1,14]}</code> |Executar em Olá primeiro e Fourteenth dia de cada mês na hora de início |
| <code>{monthDays":[2]}</code> |Executar no segundo dia de saudação mês, a hora de início da saudação |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |Executar na primeira sexta-feira de cada mês às 5h |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: Executar na primeira sexta-feira de cada mês na hora de início |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Executar na terceira sexta-feira do final do mês, todo mês, na hora de início |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Executar na primeira e na última sexta-feira de cada mês às 5:15 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Executar na primeira e na última sexta-feira de cada mês na hora de início |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Executar na quinta sexta-feira de cada mês na hora de início. Se não houver nenhum quinto sexta-feira em um mês, isso não não executado, pois é toorun agendado no quinto somente sextas-feiras. Você pode considerar o uso de -1 em vez de 5 para ocorrência hello, se desejar que o trabalho toorun Olá Olá ocorrendo última sexta-feira do mês de saudação. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Executar a cada 15 minutos na última sexta-feira do mês de saudação |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |Executar em 5:15 AM, 5:45 AM, 5:15 PM e 5:45 PM em Olá 3º quarta-feira de cada mês |

## <a name="see-also"></a>Consulte também
 [O que é o Agendador?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Agendador do Azure](scheduler-concepts-terms.md)

 [Começar a usar o Agendador no hello portal do Azure](scheduler-get-started-portal.md)

 [Planos e Cobrança no Agendador do Azure](scheduler-plans-billing.md)

 [Referência da API REST do Agendador do Azure](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Agendador do Azure](scheduler-powershell-reference.md)

 [Alta disponibilidade e confiabilidade do Agendador do Azure](scheduler-high-availability-reliability.md)

 [Limites, padrões e códigos de erro do Agendador do Azure](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Agendador do Azure](scheduler-outbound-authentication.md)

