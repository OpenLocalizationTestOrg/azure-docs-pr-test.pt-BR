---
title: "escala de aaaAutomatically nós de computação em um pool de lote do Azure | Microsoft Docs"
description: "Habilitar o dimensionamento automático em um toodynamically de pool de nuvem ajustar o número de saudação de nós de computação no pool de saudação."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Criar uma fórmula de dimensionamento automático para expandir nós de computação em um pool do Lote

Lote do Azure pode escalar automaticamente os pools baseado nos parâmetros que você definir. Com o dimensionamento automático, lote adiciona dinamicamente pool tooa de nós como aumento de demandas de tarefa e remove nós de computação conforme eles diminuem. Você pode poupar tempo e dinheiro ajustar automaticamente o número de saudação de nós de computação usados pelo seu aplicativo de lote. 

Você habilita o dimensionamento automático em um pool de nós de computação, associando a ele uma *fórmula de dimensionamento automático* definida por você. Olá serviço de lote usa Olá AutoEscala toodetermine fórmula Olá quantos nós de computação que são necessária tooexecute sua carga de trabalho. Os nós de computação podem ser nós dedicados ou [nós de baixa prioridade](batch-low-pri-vms.md). Lote responde tooservice dados de métricas coletadas periodicamente. Usando esses dados de métricas, lote ajusta o número de saudação de nós de computação no pool de saudação com base em sua fórmula e em um intervalo configurável.

É possível habilitar a escala automática quando um pool é criado ou em um pool existente. Além disso, você pode alterar uma fórmula existente em um pool configurado para dimensionamento automático. Lote permite que você tooevaluate suas fórmulas antes de atribuí-los toopools e toomonitor status Olá de dimensionamento automático é executado.

Este artigo aborda Olá várias entidades que compõem as fórmulas de dimensionamento automático, incluindo variáveis, operações, funções e operadores. Discutiremos como tooobtain várias métricas de recursos e tarefas em lote de computação. Você pode usar esses tooadjust métricas contagem de nós do pool com base no status de tarefa e uso de recursos. Em seguida, descreveremos como tooconstruct uma fórmula e habilitação automáticas de escala em um pool usando Olá restante do lote e APIs .NET. Finalmente, concluímos utilizando algumas fórmulas de exemplo.

> [!IMPORTANT]
> Quando você criar uma conta de lote, você pode especificar Olá [configuração de conta](batch-api-basics.md#account), que determina se os pools são alocados em uma assinatura de serviço de lote (padrão de saudação) ou em sua assinatura do usuário. Se você criou sua conta em lotes com a configuração de serviço de lote padrão hello, sua conta está tooa limita o número máximo de núcleos que podem ser usados para processamento. Olá serviço de lote dimensiona os nós de computação somente o limite de núcleo toothat. Por esse motivo, Olá serviço de lote pode não alcançar o número de destino de saudação de nós de computação especificado por uma fórmula de dimensionamento automático. Consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter informações sobre como exibir e aumentar as cotas de conta.
>
>Se você criou sua conta com a configuração de assinatura de usuário hello, sua conta compartilha na cota de núcleos Olá para assinatura de saudação. Para saber mais, confira[Limites das Máquinas Virtuais](../azure-subscription-service-limits.md#virtual-machines-limits) e [Assinatura e limites de serviço, cotas e restrições do Azure](../azure-subscription-service-limits.md).
>
>

## <a name="automatic-scaling-formulas"></a>Fórmulas de dimensionamento automático
Uma fórmula de dimensionamento automático é um valor de cadeia de caracteres que você definir e que contém uma ou mais instruções. fórmula de dimensionamento automático Olá é atribuída do pool de tooa [autoScaleFormula] [ rest_autoscaleformula] elemento (lote REST) ou [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] propriedade (lote .NET). Olá serviço de lote usa o número de destino Olá toodetermine fórmulas de nós de computação no pool de saudação para o próximo intervalo de saudação do processamento. cadeia de caracteres fórmula Olá não pode exceder 8 KB, pode incluir a instruções de too100 que são separadas por ponto e vírgula e podem incluir quebras de linha e comentários.

Você pode pensar em fórmulas de dimensionamento automático como uma "linguagem" de autoescala do Lote. Instruções de fórmulas são expressões de forma livre que podem incluir variáveis definidas pelo serviço (variáveis definidas pelo serviço de lote de saudação) e variáveis definidas pelo usuário (variáveis que você definir). Eles podem executar várias operações com esses valores usando tipos, operadores e funções internas. Por exemplo, uma instrução pode levar Olá formulário a seguir:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Geralmente, as fórmulas contêm várias instruções que executam operações nos valores que são obtidos nas instruções anteriores. Por exemplo, primeiro obtemos um valor para `variable1`, em seguida, passe tooa função toopopulate `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Inclua essas instruções em seu tooarrive de fórmula de dimensionamento automático em um número de nós de computação de destino. Nós dedicados e nós de baixa prioridade possuem cada um suas próprias configurações de destino, de modo que você pode definir um destino para cada tipo de nó. Uma fórmula de autoescala pode incluir um valor de destino para nós dedicados, um valor de destino para nós de baixa prioridade ou ambos.

número de destino de saudação de nós pode ser superior, inferior ou Olá mesmo que o número atual de nós desse tipo no pool de saudação do hello. O Lote avalia a fórmula de autoescala de um pool em um intervalo específico (consulte [intervalos de dimensionamento automático](#automatic-scaling-interval)). Lote ajusta o número de destino de saudação de cada tipo de nó no número de toohello de pool Olá que especifica a fórmula de dimensionamento automático no tempo de saudação da avaliação.

### <a name="sample-autoscale-formula"></a>Fórmula de dimensionamento automático de exemplo

Aqui está um exemplo de uma fórmula de dimensionamento automático que pode ser ajustada toowork na maioria dos cenários. Olá variáveis `startingNumberOfVMs` e `maxNumberofVMs` em Olá fórmula de exemplo pode ser ajustada tooyour necessidades. Esta fórmula dimensiona nós dedicado, mas pode ser modificado tooapply tooscale também nós de baixa prioridade. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Com esta fórmula de dimensionamento automático, o pool de saudação é criado inicialmente com uma única VM. Olá `$PendingTasks` métrica define o número de saudação de tarefas que estão em execução ou na fila. fórmula de saudação localiza Olá média de tarefas pendentes no hello Últimos 180 segundos e define Olá `$TargetDedicatedNodes` variável adequadamente. fórmula de saudação garante que o número de destino de saudação de nós dedicado nunca excede 25 VMs. Conforme novas tarefas forem enviadas, o pool de saudação cresce automaticamente. Como conclusão de tarefas, as VMs se tornam livre uma e fórmula de dimensionamento automático Olá diminui pool hello.

## <a name="variables"></a>variáveis
Você pode usar as variáveis **definidas pelo serviço** e **definidas pelo usuário** em suas fórmulas de dimensionamento automático. as variáveis definidas pelo serviço Olá baseiam-se no serviço de lote de toohello. Algumas variáveis definidas pelo serviço são de leitura e gravação e algumas são somente leitura. Variáveis definidas pelo usuário são as variáveis que você definir. Fórmula de exemplo hello mostrado na seção anterior do hello, `$TargetDedicatedNodes` e `$PendingTasks` são variáveis definidas pelo serviço. As variáveis de `startingNumberOfVMs` e `maxNumberofVMs` são variáveis definidas pelo usuário.

> [!NOTE]
> As variáveis definidas pelo serviço sempre são precedidas de um sinal de dólar ($). Para variáveis definidas pelo usuário, Olá cifrão é opcional.
>
>

Olá tabelas a seguir mostra as de leitura-gravação e Olá de variáveis somente leitura que são definidas pelo serviço de lote.

Você pode obter e definir valores de saudação dessas variáveis definidas pelo serviço de número de saudação toomanage de nós de computação em um pool de:

| Variáveis definidas pelo serviço de leitura/gravação | Descrição |
| --- | --- |
| $TargetDedicatedNodes |número de destino de saudação de dedicado nós para o pool de saudação de computação. número de saudação de nós dedicado é especificado como um destino porque um pool não pode obter sempre número desejado de saudação de nós. Por exemplo, se o número de destino de saudação de nós dedicado é modificado por uma avaliação de dimensionamento automático antes de saudação pool tiver atingido o destino de saudação inicial e pool Olá pode não alcançar o destino de saudação. <br /><br /> Um pool em uma conta criada com a configuração de serviço de lote de saudação não pode atingir seu destino se o destino de saudação exceder uma cota de nó ou núcleos de conta do lote. Um pool em uma conta criada com a configuração de assinatura de usuário de saudação não pode obter seu destino se o destino Olá excede a cota de núcleo compartilhado Olá para assinatura de saudação.|
| $TargetLowPriorityNodes |nós para o pool de saudação de computação do número de destino de saudação de baixa prioridade. número de saudação de nós de baixa prioridade é especificado como um destino porque um pool não pode obter sempre número desejado de saudação de nós. Por exemplo, se o número de destino de saudação de nós de baixa prioridade é modificado por uma avaliação de dimensionamento automático antes de saudação pool tiver atingido o destino de saudação inicial e pool Olá pode não alcançar o destino de saudação. Um pool pode também obter seu destino não se destino Olá exceder uma cota de nó ou núcleos de conta do lote. <br /><br /> Para obter mais informações sobre nós de computação de baixa prioridade, consulte [Usar VMs de baixa prioridade com o Lote (versão prévia)](batch-low-pri-vms.md). |
| $NodeDeallocationOption |ação de saudação que ocorre quando nós de computação são removidos de um pool. Os valores possíveis são:<ul><li>**enfileiramento**– finaliza as tarefas imediatamente e as coloca novamente na fila de trabalho Olá para que elas sejam reagendadas.<li>**encerrar**– finaliza as tarefas imediatamente e as remove da fila de trabalho hello.<li>**taskcompletion**– aguarda para em execução no momento toofinish as tarefas e, em seguida, remove o nó de saudação do pool de saudação.<li>**retaineddata**– aguarda todos Olá retidos de tarefa dados locais em Olá nó toobe limpos antes de remover o nó de saudação do pool de saudação.</ul> |

Você pode obter o valor de saudação esses ajustes toomake variáveis definidas pelo serviço com base nas métricas de serviço de lote hello:

| Variáveis somente leitura definidas pelo serviço | Descrição |
| --- | --- |
| $CPUPercent |porcentagem média de saudação do uso de CPU. |
| $WallClockSeconds |Olá quantos segundos consumidos. |
| $MemoryBytes |número médio de saudação de megabytes usados. |
| $DiskBytes |número médio de saudação de gigabytes usados em discos locais hello. |
| $DiskReadBytes |número de saudação de bytes lidos. |
| $DiskWriteBytes |número de saudação de bytes gravados. |
| $DiskReadOps |Contagem de saudação de operações de leitura de disco é executada. |
| $DiskWriteOps |Contagem de saudação de operações de gravação de disco executadas. |
| $NetworkInBytes |número de saudação de bytes de entrada. |
| $NetworkOutBytes |número de saudação de bytes de saída. |
| $SampleNodeCount |Contagem de saudação de nós de computação. |
| $ActiveTasks |número de saudação de tarefas tooexecute pronto, mas ainda não está executando. Contagem de saudação $ActiveTasks inclui todas as tarefas que estão em estado ativo hello e cujas dependências foram atendidas. As tarefas que estão no estado ativo Olá mas cujas dependências não foram satisfeitas são excluídas da contagem de saudação $ActiveTasks.|
| $RunningTasks |número de saudação de tarefas em um estado de execução. |
| $PendingTasks |soma de saudação do $ActiveTasks e $RunningTasks. |
| $SucceededTasks |número de saudação de tarefas que foram concluídas com êxito. |
| $FailedTasks |número de saudação de tarefas que falharam. |
| $CurrentDedicatedNodes |número atual de saudação do dedicado de nós de computação. |
| $CurrentLowPriorityNodes |número atual de saudação de baixa prioridade nós, incluindo todos os nós que foram antecipados de computação. |
| $PreemptedNodeCount | número de saudação de nós no pool de saudação que estão em um estado antecipado. |

> [!TIP]
> Olá variáveis somente leitura, definição de serviço que são mostradas na tabela anterior Olá são *objetos* que fornecem vários métodos tooaccess dados associados a cada. Para obter mais informações, consulte [Obter amostras de dados](#getsampledata) a seguir neste artigo.
>
>

## <a name="types"></a>Tipos
Esses tipos têm suporte em uma fórmula:

* double
* doubleVec
* doubleVecList
* string
* timestamp - timestamp é uma estrutura composta que contém Olá membros a seguir:

  * year
  * month (1-12)
  * day (1-31)
  * dia da semana (no formato de saudação do número; por exemplo, 1 para segunda-feira)
  * hour (no formato de número de 24 horas, por exemplo, 13 significa 1 PM)
  * minute (00-59)
  * second (00-59)
* timeinterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>Operações
Essas operações são permitidas nos tipos de saudação que são listados na seção anterior hello.

| Operação | Operadores com suporte | Tipo de resultado |
| --- | --- | --- |
| double *operador* double |+, -, *, / |double |
| double *operador* timeinterval |* |timeinterval |
| doubleVec *operador* double |+, -, *, / |doubleVec |
| doubleVec *operador* doubleVec |+, -, *, / |doubleVec |
| timeinterval *operador* double |*, / |timeinterval |
| timeinterval *operador* timeinterval |+, - |timeinterval |
| timeinterval *operador* timestamp |+ | timestamp |
| timestamp *operador* timeinterval |+ | timestamp |
| timestamp *operador* timestamp |- |timeinterval |
| *operador*double |-, ! |double |
| *operador*timeinterval |- |timeinterval |
| double *operador* double |<, <=, ==, >=, >, != |double |
| string *operador* string |<, <=, ==, >=, >, != |double |
| timestamp *operador* timestamp |<, <=, ==, >=, >, != |double |
| timeinterval *operador* timeinterval |<, <=, ==, >=, >, != |double |
| double *operador* double |&&, &#124;&#124; |double |

Ao testar um double com um operador ternário (`double ? statement1 : statement2`), um item diferente de zero é **true** e zero é **false**.

## <a name="functions"></a>Funções
Esses predefinidos **funções** estão disponíveis para você toouse na definição de uma fórmula de dimensionamento automático.

| Função | Tipo de retorno | Descrição |
| --- | --- | --- |
| avg(doubleVecList) |double |Retorna Olá valor médio para todos os valores no doubleVecList hello. |
| len(doubleVecList) |double |Retorna Olá comprimento do vetor de saudação que é criada a partir de doubleVecList hello. |
| lg(double) |double |Retorna um log Olá base 2 de saudação double. |
| lg(doubleVecList) |doubleVec |Retorna o log component-wise Olá base 2 de saudação doubleVecList. Um vec (Double) deve ser passado explicitamente para o parâmetro hello. Caso contrário, versão de duplo lg(double) Olá será assumido. |
| ln(double) |double |Retorna Olá log natural de saudação dupla. |
| ln(doubleVecList) |doubleVec |Retorna o log component-wise Olá base 2 de saudação doubleVecList. Um vec (Double) deve ser passado explicitamente para o parâmetro hello. Caso contrário, versão de duplo lg(double) Olá será assumido. |
| log(double) |double |Retorna um log Olá base 10 da saudação double. |
| log(doubleVecList) |doubleVec |Retorna o log component-wise Olá base 10 da saudação doubleVecList. Um vec (Double) deve ser passado explicitamente para o único parâmetro double de saudação. Caso contrário, versão de duplo log(double) Olá será assumido. |
| max(doubleVecList) |double |Retorna Olá valor máximo na doubleVecList hello. |
| min(doubleVecList) |double |Retorna Olá valor mínimo na doubleVecList hello. |
| norm(doubleVecList) |double |Retorna Olá norma dupla do vetor de saudação que é criada a partir de doubleVecList hello. |
| percentile(doubleVec v, double p) |double |Retorna Olá elemento percentile do vetor de saudação v. |
| rand() |double |Retorna um valor aleatório entre 0,0 e 1,0. |
| range(doubleVecList) |double |Retorna a diferença de saudação entre Olá valores mínimo e máximos em doubleVecList hello. |
| std(doubleVecList) |double |Retorna Olá desvio padrão dos valores Olá Olá doubleVecList. |
| stop() | |Interrompe a avaliação da expressão de dimensionamento automático hello. |
| sum(doubleVecList) |double |Retorna Olá soma de todos os componentes de saudação do hello doubleVecList. |
| time(string dateTime="") |timestamp |Retorna o carimbo de hora de saudação do hello hora atual se sem parâmetros são transmitidos ou Olá carimbo de data / hora de cadeia de caracteres de data e hora de saudação se ele for passado. Os formatos de dateTime com suporte são W3C-DTF e RFC1123. |
| val(doubleVec v, double i) |double |Retorna o valor de saudação do elemento de saudação no local i no vetor v, com um índice inicial de zero. |

Algumas das funções de saudação que são descritas na tabela anterior Olá podem aceitar uma lista como um argumento. lista separada por vírgulas de saudação é qualquer combinação de *duplo* e *doubleVec*. Por exemplo:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Olá *doubleVecList* valor é convertido tooa único *doubleVec* antes da avaliação. Por exemplo, se `v = [1,2,3]`, em seguida, chamar `avg(v)` é o equivalente toocalling `avg(1,2,3)`. Chamando `avg(v, 7)` é o equivalente toocalling `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Obter dados de exemplo
Fórmulas de dimensionamento automático agir sobre dados de métricas (exemplos) que são fornecidos pelo serviço de lote de saudação. Uma fórmula aumenta ou diminui o tamanho do pool com base nos valores de saudação que ele obtém do serviço de saudação. as variáveis definidas pelo serviço Olá que foram descritas anteriormente são objetos que fornecem vários métodos tooaccess dados que está associados esse objeto. Por exemplo, hello expressão a seguir mostra uma saudação de tooget solicitação últimos cinco minutos de uso da CPU:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Método | Descrição |
| --- | --- |
| GetSample() |Olá `GetSample()` método retorna um vetor de exemplos de dados.<br/><br/>Uma amostra é de 30 segundos de dados de métrica. Em outras palavras, os exemplos são obtidos a cada 30 segundos. Mas, conforme observado a seguir, há um atraso entre quando uma amostra é coletada e quando ele está disponível tooa fórmula. Como tal, é possível que nem todas as amostras para um determinado período de tempo estejam disponíveis para avaliação por uma fórmula.<ul><li>`doubleVec GetSample(double count)`<br/>Especifica o número de saudação de exemplos tooobtain exemplos de hello mais recentes que foram coletados.<br/><br/>`GetSample(1)`Retorna a última amostra disponível de saudação. Para métricas como `$CPUPercent`, no entanto, isso não deve ser usado porque é impossível tooknow *quando* Olá exemplo foi coletado. Pode ser recente ou, devido a problemas do sistema, muito mais antigo. É melhor em tal casos de toouse um intervalo de tempo, conforme mostrado abaixo.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Especifica um intervalo de tempo para coleta de dados de exemplo. Opcionalmente, ela também especifica porcentagem Olá de amostras que deve estar disponível no hello solicitado período de tempo.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`retornaria 20 amostras se todas as amostras para Olá últimos 10 minutos estão presentes no histórico de CPUPercent hello. No entanto, se Olá última hora de histórico não estava disponível, apenas 18 exemplos serão retornados. Nesse caso:<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`falhará porque somente 90% de exemplos de saudação estão disponíveis.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` teria êxito.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Especifica um intervalo de tempo para coleta de dados, com uma hora de início e uma hora de término.<br/><br/>Conforme mencionado acima, há um atraso entre quando uma amostra é coletada e quando ele está disponível tooa fórmula. Considere esse atraso quando você usar o hello `GetSample` método. Veja `GetSamplePercent` abaixo. |
| GetSamplePeriod() |Retorna o período de saudação de exemplos que foram executadas em um conjunto de dados históricos de exemplo. |
| Count() |Retorna Olá número total de amostras no histórico de métrica de saudação. |
| HistoryBeginTime() |Retorna Olá carimbo de hora de exemplo de dados disponível mais antigo hello de métrica de saudação. |
| GetSamplePercent() |Retorna Olá porcentagem de amostras que estão disponíveis para um determinado intervalo. Por exemplo:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Porque Olá `GetSample` método falhará se a porcentagem de saudação de amostras retornado é menor que Olá `samplePercent` especificado, você pode usar o hello `GetSamplePercent` toocheck método primeiro. Em seguida, você pode executar uma ação alternativa se insuficiente exemplos estiverem presentes, sem interromper a avaliação de dimensionamento automático hello. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Olá, a porcentagem de exemplo e exemplos *GetSample()* método
operação principal de saudação de uma fórmula de dimensionamento automático é dados de métrica tarefas e recursos tooobtain e, em seguida, ajustar o tamanho do pool com base nesses dados. Como tal, é importante toohave uma compreensão clara de como as fórmulas de dimensionamento automático interagem com dados de métricas (exemplos).

**Exemplos**

Olá serviço de lote periodicamente usa exemplos de métricas de recursos e tarefas e torna disponível tooyour fórmulas de dimensionamento automático. Esses exemplos são registrados a cada 30 segundos por Olá serviço de lote. No entanto, há geralmente um atraso entre quando esses exemplos foram registrados e quando eles são disponibilizados muito (e podem ser lidos por) suas fórmulas de dimensionamento automático. Além disso, devido a fatores de toovarious, como a rede ou outros problemas de infraestrutura, exemplos podem não ser gravados para um determinado intervalo.

**Exemplo de porcentagem**

Quando `samplePercent` é passado toohello `GetSample()` método ou hello `GetSamplePercent()` método é chamado, _%_ refere-se a comparação de tooa entre o número total possível de saudação de exemplos que são registradas pelo serviço de lote de saudação e número de saudação de exemplos de fórmula de dimensionamento automático tooyour disponíveis.

Vamos examinar um período de 10 minutos como exemplo. Como exemplos são registrados a cada 30 segundos dentro de um período de tempo de 10 minutos, Olá máximo total de exemplos que são registradas pelo lote seria 20 amostras (2 por minuto). No entanto, devido a latência inerente de toohello de saudação reporting mecanismo e outros problemas no Azure, pode haver apenas 15 exemplos de fórmula de dimensionamento automático tooyour disponível para leitura. Assim, por exemplo, para aquele período de 10 minutos, somente 75% do número total de saudação de amostras registrado pode ser fórmula tooyour disponíveis.

**GetSample() e intervalos de exemplo**

As fórmulas de dimensionamento automático são contínuo toobe aumentando e reduzindo os pools &mdash; adicionar nós ou remover nós. Como nós custam dinheiro, convém tooensure que as fórmulas usam um método inteligente de análise com base em dados suficientes. Portanto, recomendamos que você use uma análise de tipo de tendência em suas fórmulas. Este tipo aumenta e diminui seus pools baseado em uma variedade de exemplos coletados.

Assim, use toodo `GetSample(interval look-back start, interval look-back end)` tooreturn um vetor de amostras:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Quando Olá acima da linha é avaliada pelo lote, ele retorna um intervalo de exemplos de como um vetor de valores. Por exemplo:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Depois que você coletou vetor Olá de amostras, você pode usar funções como `min()`, `max()`, e `avg()` tooderive significativo valores hello coletados intervalo.

Para segurança adicional, você pode forçar uma toofail de avaliação de fórmulas se menor que uma determinada porcentagem de exemplo está disponível para um determinado período de tempo. Quando você forçar um toofail de avaliação de fórmulas, você instruir o lote toocease mais avaliação da fórmula Olá se Olá especificado porcentagem de amostras não está disponível. Nesse caso, nenhuma alteração é feita toohello o tamanho do pool. toospecify uma porcentagem necessária de amostras para Olá toosucceed de avaliação, especifique-Olá terceiro parâmetro muito`GetSample()`. Aqui, é especificado um requisito de 75% de exemplos:

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Como pode haver um atraso na disponibilidade de exemplo, é importante tooalways especificar um intervalo de tempo com uma hora de início de retorno de aparência com mais de um minuto. Demora aproximadamente um minuto para exemplos toopropagate por meio do sistema hello, portanto amostras no intervalo de saudação `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` pode não estar disponível. Novamente, você pode usar o parâmetro de percentual de saudação do `GetSample()` tooforce um requisito de porcentagem de exemplo específico.

> [!IMPORTANT]
> **Recomendamos expressamente** que você **evite contar *somente* com `GetSample(1)` em suas fórmulas de dimensionamento automático**. Isso ocorre porque `GetSample(1)` essencialmente diz toohello serviço de lote, "Dê-me Olá última amostra que você tem, não importa quanto tempo atrás recuperá-lo." Como é apenas um único exemplo e pode ser um exemplo mais antigo, pode não ser representativo de imagem maior de saudação do estado de recurso ou tarefa recente. Se você usar `GetSample(1)`, certifique-se de que é parte de uma instrução maior e Olá não apenas o ponto de dados que depende de sua fórmula.
>
>

## <a name="metrics"></a>Métricas
Você pode usar as métricas do recurso e da tarefa quando estiver definindo uma fórmula. Você ajustar o número de destino de saudação de nós dedicado no pool de saudação com base nos dados de métricas de saudação que você obtenha e avalia. Consulte Olá [variáveis](#variables) seção acima para obter mais informações sobre cada métrica.

<table>
  <tr>
    <th>Métrica</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td><b>Recurso</b></td>
    <td><p>Métricas de recursos se baseiam no hello CPU, uso de memória de saudação de nós de computação, de largura de banda de saudação e Olá número de nós.</p>
        <p> Essas variáveis definidas pelo serviço são úteis para fazer ajustes com base na contagem de nós:</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Estas variáveis definidas pelo serviço são úteis para fazer ajustes com base no uso de recursos do nó:</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Tarefa</b></td>
    <td><p>Métricas de tarefa são com base no status de saudação de tarefas, como ativo, pendente e concluídas. Olá a variáveis definidas pelo serviço a seguir são úteis para fazer ajustes de tamanho do pool com base nas métricas de tarefa:</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Criar uma fórmula de autoescala
Criar uma fórmula de dimensionamento automático formando instruções que usam Olá acima componentes, e combinar essas instruções em uma fórmula completa. Nesta seção, criamos um exemplo de fórmula de autoescala que pode executar algumas decisões de dimensionamento do mundo real.

Primeiro, vamos definir requisitos Olá para nossa nova fórmula de dimensionamento automático. fórmula de saudação deve:

1. Aumente o número de destino de saudação de nós de computação dedicado em um pool se o uso da CPU é alto.
2. Diminua o número de destino de saudação de nós de computação dedicado em um pool de quando o uso da CPU é baixo.
3. Sempre restringir o número máximo de saudação de nós dedicado too400.

número de saudação do tooincrease de nós durante o alto uso de CPU, defina a instrução de saudação que preenche uma variável definida pelo usuário (`$totalDedicatedNodes`) com um valor que é 110% do número de destino atual Olá nós dedicado, mas apenas se Olá uso mínimo de CPU média durante a saudação últimos 10 minutos foi acima de 70%. Caso contrário, use o valor de saudação para número atual de saudação de nós dedicado.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

muito*diminuir* Olá número de nós dedicado durante a baixa utilização da CPU, Olá próxima instrução na nossa fórmula conjuntos Olá mesmo `$totalDedicatedNodes` too90 variável % do número de destino atual Olá de nós dedicado se hello média de uso da CPU Olá últimos 60 minutos em era 20 por cento. Caso contrário, use o valor atual de saudação do `$totalDedicatedNodes` que é preenchida na instrução de saudação acima.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Limite o número de destino de saudação de máximo de tooa de nós de computação dedicado de 400 agora:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Aqui está a fórmula completa de saudação:

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>Criar um pool habilitado para autoescala com .NET

toocreate um pool com o dimensionamento automático habilitado no .NET, siga estas etapas:

1. Criar pool de saudação com [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Saudação de conjunto [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) propriedade muito`true`.
3. Saudação de conjunto [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) propriedade com a fórmula de dimensionamento automático.
4. (Opcional) Saudação de conjunto [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) propriedade (o padrão é 15 minutos).
5. Confirmar pool Olá com [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) ou [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Olá trecho de código a seguir cria um pool de AutoEscala habilitada no .NET. Olá fórmula de dimensionamento automático do pool define Olá destino número de nós dedicado too5 às segundas-feiras e 1 em todos os outros dias da semana hello. Olá [intervalo de dimensionamento automático](#automatic-scaling-interval) é definir too30 minutos. Neste e Olá outros trechos de código c# neste artigo, `myBatchClient` é uma instância inicializada corretamente do hello [BatchClient] [ net_batchclient] classe.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Quando você cria um pool de dimensionamento automático habilitado, não especifique Olá _targetDedicatedComputeNodes_ parâmetro ou hello _targetLowPriorityComputeNodes_ parâmetro hello chamar muito** CreatePool**. Em vez disso, especifique Olá **AutoScaleEnabled** e **AutoScaleFormula** propriedades no pool de saudação. valores de Olá para essas propriedades determinam o número de destino de saudação de cada tipo de nó. Além disso, toomanually redimensionar um pool de dimensionamento automático habilitado (por exemplo, com [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), primeiro **desabilitar** o dimensionamento automático em Olá pool e, em seguida, redimensioná-la.
>
>

Além disso tooBatch .NET, você pode usar qualquer um dos outros Olá [SDKs de lote](batch-apis-tools.md#azure-accounts-for-batch-development), [restante do lote](https://docs.microsoft.com/rest/api/batchservice/), [cmdlets do PowerShell do lote](batch-powershell-cmdlets-get-started.md)e hello [lote CLI](batch-cli-get-started.md)tooconfigure AutoEscala.


### <a name="automatic-scaling-interval"></a>Intervalo de dimensionamento automático
Por padrão, Olá serviço de lote ajusta o tamanho do pool de acordo com tooits fórmula de dimensionamento automático a cada 15 minutos. Esse intervalo é configurável usando Olá seguintes propriedades do pool:

* [CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (.NET do Lote)
* [autoScaleEvaluationInterval][rest_autoscaleinterval] (API REST)

intervalo mínimo de saudação é de cinco minutos e Olá máximo é 168 horas. Se for especificado um intervalo fora desse intervalo, Olá serviço de lote retorna um erro de solicitação incorreta (400).

> [!NOTE]
> Dimensionamento automático não é atualmente pretendido toorespond toochanges em menos de um minuto, mas em vez disso é projetada tooadjust tamanho de saudação de seu pool gradualmente como executar uma carga de trabalho.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Habilitar autoescala em um pool existente

Cada lote SDK fornece um dimensionamento automático tooenable de maneira. Por exemplo:

* [BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (.NET do Lote)
* [Habilitar o dimensionamento automático em um pool][rest_enableautoscale] (API REST)

Quando você habilita o dimensionamento automático em um pool existente, lembre-Olá mente pontos a seguir:

* Se o dimensionamento automático está desabilitado no pool hello quando você emite o dimensionamento automático tooenable de solicitação hello, você deve especificar uma fórmula de dimensionamento automático válido quando você emitir a solicitação de saudação. Opcionalmente, é possível especificar um intervalo de avaliação de autoescala. Se você não especificar um intervalo, o valor padrão de saudação de 15 minutos é usado.
* Se o dimensionamento automático estiver habilitado no pool de saudação, você pode especificar uma fórmula de dimensionamento automático, um intervalo de avaliação ou ambos. É necessário especificar pelo menos uma dessas propriedades.

  * Se você especificar um novo intervalo de avaliação de dimensionamento automático, em seguida, Olá agenda de avaliação existente é interrompida e uma nova agenda é iniciada. hora de início da agenda Olá novo é hora de Olá quais Olá dimensionamento automático tooenable de solicitação foi emitido.
  * Se você omitir o intervalo de saudação AutoEscala fórmula ou avaliação, Olá serviço de lote continua toouse Olá atual valor dessa configuração.

> [!NOTE]
> Se você especificou valores para Olá *targetDedicatedComputeNodes* ou *targetLowPriorityComputeNodes* parâmetros de saudação **CreatePool** método quando você criou Olá pool de .NET ou para parâmetros de saudação comparável em outro idioma e, em seguida, esses valores são ignorados quando Olá automática de escala a fórmula é avaliada.
>
>

Este trecho de código c# usa Olá [Batch .NET] [ net_api] dimensionamento automático tooenable de biblioteca em um pool existente:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Atualizar uma fórmula de autoescala

fórmula de saudação tooupdate em um AutoEscala habilitada pool existente, chamada hello operação tooenable autoscaling novamente com a nova fórmula de saudação. Por exemplo, se o dimensionamento automático já está habilitado na `myexistingpool` quando Olá código .NET a seguir é executado, sua fórmula de dimensionamento automático é substituída pelo conteúdo de saudação do `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Intervalo de atualização de dimensionamento automático Olá

intervalo de avaliação tooupdate saudação de dimensionamento automático de um AutoEscala habilitada pool existente, chamada hello operação tooenable autoscaling novamente com o novo intervalo de saudação. Por exemplo, tooset Olá AutoEscala avaliação intervalo too60 minutos para um pool que já está habilitado para dimensionamento automático no .NET:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Avaliar uma fórmula de autoescala

Você pode avaliar uma fórmula antes de aplicá-la tooa pool. Dessa forma, você pode testar Olá toosee fórmula como suas instruções avaliem antes de colocar fórmula Olá em produção.

tooevaluate uma fórmula de dimensionamento automático, você deve primeiro habilitar dimensionamento automático no pool de saudação com uma fórmula válida. tootest uma fórmula em um pool que ainda não tenha o dimensionamento automático habilitado, use fórmula de uma linha de saudação `$TargetDedicatedNodes = 0` quando você primeiro habilita o dimensionamento automático. Em seguida, use um dos Olá seguinte tooevaluate Olá fórmula deseja tootest:

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) ou [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Esses métodos de lote .NET exigem Olá ID de um pool existente e uma cadeia de caracteres que contém tooevaluate de fórmula de dimensionamento automático hello.

* [Avaliar uma fórmula de autoescala](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    Nesta solicitação de API REST, especifique a ID de pool de saudação no URI de saudação e Olá fórmula de dimensionamento automático no hello *autoScaleFormula* elemento Olá do corpo da solicitação. resposta de saudação da operação de saudação contém qualquer informação de erro que pode ser relacionadas toohello fórmula.

Neste trecho de código [ .NET do Lote][net_api], avaliamos uma fórmula de autoescala. Se o pool de saudação não tem o dimensionamento automático habilitado, podemos habilitá-la primeiro.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Avaliação bem-sucedida de fórmula Olá mostrada neste trecho de código produz resultados semelhantes:

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Obter informações sobre execuções de autoescala

tooensure sua fórmula está sendo executado como esperado, é recomendável que você verifique periodicamente resultados Olá Olá execuções de dimensionamento automático que executa o lote em seu pool. toodo assim, get (ou atualizar) toohello uma referência pool e, em seguida, examine as propriedades de saudação do seu último AutoEscala executar.

No .NET em lotes, Olá [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) propriedade tem várias propriedades que fornecem informações sobre hello mais recente o dimensionamento automático executar executada no pool de saudação:

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

Na API REST do hello, Olá [obter informações sobre um pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) solicitação retorna informações sobre o pool de saudação, que inclui hello mais recente o dimensionamento automático informações de execução em Olá [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) propriedade.

Olá, seguinte trecho de código c# usa Olá Batch .NET biblioteca tooprint informações sobre hello autoscaling última execução no pool de _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Exemplo de saída do hello precede o trecho de código:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Fórmulas de autoescala de exemplo
Vamos examinar algumas fórmulas que mostram a quantidade de saudação tooadjust maneiras diferentes de recursos de computação em um pool.

### <a name="example-1-time-based-adjustment"></a>Exemplo 1: ajuste baseado no tempo
Suponha que você deseja que o tamanho do pool de saudação tooadjust com base no dia de saudação da semana hello e a hora do dia. Este exemplo mostra como número de saudação tooincrease ou diminuição de nós no hello pool de adequadamente.

fórmula de saudação primeiro obtém Olá hora atual. Se for um dia da semana (1-5) e dentro do horário comercial (too6 8: 00 PM), tamanho do pool de destino Olá é definido too20 nós. Caso contrário, ele definiu too10 nós.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Exemplo 2: ajuste baseado na tarefa
Neste exemplo, o tamanho do pool de saudação é ajustado com base no número de saudação de tarefas na fila de saudação. Ambos os comentários e as quebras de linha são aceitáveis em cadeias de caracteres de fórmulas.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Exemplo 3: contagem de tarefas paralelas
Este exemplo ajusta o tamanho do pool de saudação com base no número de saudação de tarefas. Esta fórmula também leva em Olá conta [MaxTasksPerComputeNode] [ net_maxtasks] valor tiver sido definido para o pool de saudação. Essa abordagem é útil em situações nas quais a [execução de tarefas paralelas](batch-parallel-node-tasks.md) foi habilitada em seu pool.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Exemplo 4: definindo um tamanho de pool inicial
Este exemplo mostra um c# code trecho com uma fórmula de dimensionamento automático que define Olá tooa de tamanho do pool especificado o número de nós por um período de tempo inicial. Em seguida, ele ajusta o tamanho do pool de saudação com base no número de saudação em execução e tarefas ativas após a saudação inicial período de tempo decorrido.

fórmula Olá Olá trecho de código a seguir:

* Define o pool inicial de saudação nós de toofour de tamanho.
* Não ajustar o tamanho de pool de saudação em Olá primeiros 10 minutos do ciclo de vida do pool de saudação.
* Depois de 10 minutos, obtém o valor máximo de saudação do hello ativo e número de execução as tarefas dentro de saudação nos últimos 60 minutos.
  * Se ambos os valores são 0 (indicando que nenhum tarefas foram em execução ou ativo no hello últimos 60 minutos), o tamanho do pool de saudação é definido too0.
  * Se um dos valores for maior do que zero, nenhuma alteração será feita

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Próximas etapas
* [Maximizar o uso de recursos de computação do Azure Batch com tarefas simultâneas do nó](batch-parallel-node-tasks.md) contém detalhes sobre como você pode executar várias tarefas simultaneamente em nós de computação de saudação em seu pool. Além disso tooautoscaling, esse recurso pode ajudar toolower duração do trabalho para algumas cargas de trabalho, reduzindo os custos.
* Para outro de expansão de eficiência, certifique-se de que suas consultas de aplicativo do lote Olá serviço de lote no hello mais de maneira ideal. Consulte [consultar o serviço de lote do Azure Olá com eficiência](batch-efficient-list-queries.md) toolearn como toolimit Olá a quantidade de dados que passam durante a transmissão hello quando você consulta o status de saudação potencialmente milhares de computação nós ou tarefas.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
