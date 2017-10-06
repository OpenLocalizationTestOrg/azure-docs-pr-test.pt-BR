---
title: "aaaScheduling e a execução com a fábrica de dados | Microsoft Docs"
description: "Aprenda sobre os aspectos de agendamento e execução do modelo de aplicativo do Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Agendamento e execução com o Data Factory
Este artigo explica os aspectos de programação e a execução de Olá Olá do Azure Data Factory do modelo de aplicativo. Este artigo presume que você compreenda as noções básicas sobre conceitos de modelo de aplicativo do data factory, incluindo atividade, pipelines, serviços vinculados e conjuntos de dados. Para obter conceitos básicos do Azure Data Factory, consulte Olá artigos a seguir:

* [Introdução tooData fábrica](data-factory-introduction.md)
* [Pipelines](data-factory-create-pipelines.md)
* [Conjunto de dados](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Horas de início e término do pipeline
Um pipeline está ativo somente entre sua hora de **início** e de **término**. Ele não é executado antes da hora de início do hello, ou após a hora de término hello. Se Olá pipeline é pausado, ele não é executado independentemente de seu tempo de início e término. Para um pipeline toorun, ela deve não ser pausada. Você pode encontrar essas configurações (início, fim, pausado) na definição de pipeline de saudação: 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Para obter mais informações sobre essas propriedades, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md). 


## <a name="specify-schedule-for-an-activity"></a>Especificar o agendamento de uma atividade
Não é pipeline Olá que é executado. É atividades Olá Olá pipeline são executadas em Olá contexto geral do pipeline de saudação. Você pode especificar um agendamento recorrente para uma atividade usando Olá **Agendador** seção de JSON da atividade. Por exemplo, você pode agendar uma atividade toorun por hora da seguinte maneira:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Conforme mostrado no diagrama a seguir de saudação, especificando que uma agenda para uma atividade cria uma série de janelas em cascata com em Olá pipeline de início e término. Janelas em cascata são uma série de intervalos de tempo de tamanho fixo, não sobrepostos e contínuos. Essas janelas lógicas em cascata de uma atividade são chamadas de **janelas de atividades**.

![Exemplo de agendador de atividades](media/data-factory-scheduling-and-execution/scheduler-example.png)

Olá **Agendador** propriedade para uma atividade é opcional. Se você especificar essa propriedade, ele deve corresponder cadência Olá que seja especificada na definição de saudação do conjunto de dados de saída para a atividade de saudação. Atualmente, o conjunto de dados de saída é quais unidades Olá agenda. Portanto, você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. 

## <a name="specify-schedule-for-a-dataset"></a>Especificar o agendamento de um conjunto de dados
Uma atividade em um pipeline do Data Factory pode usar zero ou mais **conjuntos de dados** de entrada e gerar um ou mais conjuntos de dados de saída. Para uma atividade, você pode especificar o ritmo de saudação em qual Olá dados de entrada estão disponíveis ou dados de saída de saudação são produzidos usando Olá **disponibilidade** seção definições de conjunto de dados de saudação. 

**Frequência** em Olá **disponibilidade** seção especifica a unidade de tempo de saudação. Olá valores permitidos para frequência são: minuto, hora, dia, semana e mês. Olá **intervalo** propriedade na seção de disponibilidade de saudação especifica um multiplicador para frequência. Por exemplo: se a frequência de saudação for definida tooDay e intervalo é definido too1 para um conjunto de dados de saída, dados de saída de saudação são produzidos diariamente. Se você especificar a frequência de saudação minuto, recomendamos que você defina Olá intervalo toono menos de 15. 

No hello exemplo a seguir, os dados de entrada hello estão disponíveis por hora e dados de saída de saudação são gerados por hora (`"frequency": "Hour", "interval": 1`). 

**Conjunto de dados de entrada:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Conjunto de dados de saída**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Atualmente, **dataset unidades Olá agenda**. Em outras palavras, a agenda de saudação especificada para o conjunto de dados de saída de saudação é usado toorun uma atividade em tempo de execução. Portanto, você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída. Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando. 

Seguir Olá pipeline definição, hello **Agendador** propriedade é agenda toospecify usado para a atividade de saudação. Essa propriedade é opcional. No momento, agenda hello atividade Olá deve coincidir com a agenda Olá especificada para o conjunto de dados de saída de hello.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

Neste exemplo, hello atividade é executada por hora entre hello início e término horas do pipeline de saudação. Olá dados de saída são produzidos por hora para windows de três horas (8: 00 - 9 AM, 9: 00 - 10: 00 e 10 AM - 11: 00). 

Cada unidade de dados consumida ou gerada por uma execução de atividade é chamada de uma **fatia de dados**. Olá diagrama a seguir mostra um exemplo de uma atividade com um conjunto de dados de entrada e um conjunto de dados de saída: 

![Agendador de disponibilidade](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

diagrama de saudação mostra por hora Olá fatias de dados para saudação de entrada e saída do conjunto de dados. diagrama de saudação mostra três fatias de entrada que estão prontas para processamento. atividade de 10-11 AM Hello está em andamento, produzindo a fatia de saída do hello 10-11 AM. 

Você pode acessar o intervalo de tempo de saudação associado com a fatia atual Olá Olá conjunto de dados JSON usando variáveis: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) e [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). Da mesma forma, você pode acessar o intervalo de tempo de saudação associado com uma janela de atividade usando hello WindowStart e WindowEnd. agenda saudação de uma atividade deve coincidir com a agenda de saudação do conjunto de dados de saída de hello atividade Olá. Portanto, Olá SliceStart e SliceEnd valores são Olá mesmo como valores WindowStart e WindowEnd respectivamente. Para obter mais informações sobre essas variáveis, consulte os artigos [Funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md#data-factory-system-variables).  

Você pode usar essas variáveis para finalidades diferentes em sua atividade JSON. Por exemplo, você pode usá-los tooselect dados de entrada e saídos conjuntos de dados que representa dados de série temporal (por exemplo: Estou too9 de AM 8). Este exemplo também usa **WindowStart** e **WindowEnd** tooselect de dados relevantes para uma atividade executar e copie-o blob tooa com hello apropriado **folderPath**. Olá **folderPath** é parametrizada toohave uma pasta separada para cada hora.  

Em Olá anterior de exemplo, agendamento de saudação especificado para conjuntos de dados de entrada e saídos é Olá mesmo (por hora). Se o conjunto de dados de entrada de hello atividade hello está disponível em uma frequência diferente, significa que a cada 15 minutos, atividade Olá que produz este conjunto de dados de saída continuará sendo executada uma vez por hora, como conjunto de dados de saída de saudação é quais unidades Olá agenda de atividade. Para obter mais informações, consulte [Modelar conjuntos de dados com frequências diferentes](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Políticas e disponibilidade do conjunto de dados
Você viu que o uso de saudação de frequência e o intervalo de propriedades na seção de disponibilidade de saudação da definição de conjunto de dados. Há algumas outras propriedades que afetam a saudação de agendamento e execução de uma atividade. 

### <a name="dataset-availability"></a>Disponibilidade do conjunto de dados 
Olá tabela a seguir descreve as propriedades você pode usar em Olá **disponibilidade** seção:

| Propriedade | Descrição | Obrigatório | Padrão |
| --- | --- | --- | --- |
| frequência |Especifica a unidade de tempo de saudação de produção de fatia do conjunto de dados.<br/><br/><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês |Sim |ND |
| intervalo |Especifica um multiplicador para frequência<br/><br/>"Intervalo de frequência x" determina com que frequência hello fatia é produzida.<br/><br/>Se você precisar hello toobe de conjunto de dados dividido por hora, defina <b>frequência</b> muito<b>hora</b>, e <b>intervalo</b> muito<b>1</b>.<br/><br/><b>Observação</b>: se você especificar a frequência como minuto, recomendamos que você defina Olá intervalo toono menor que 15 |Sim |ND |
| estilo |Especifica se a fatia Olá deve ser produzida no hello início/término do intervalo de saudação.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Quando frequência é definida tooMonth e o estilo definido tooEndOfInterval, fatia de saudação é produzida no último dia do mês de saudação. Se o estilo de saudação é definido tooStartOfInterval, Olá fatia é produzida no hello primeiro dia do mês.<br/><br/>Quando frequência é definida tooDay e o estilo definido tooEndOfInterval, fatia de Olá é produzida no hello última hora do dia de saudação.<br/><br/>Quando frequência é definida tooHour e o estilo definido tooEndOfInterval, fatia de Olá é produzida no final de saudação de hora hello. Por exemplo, para uma fatia de período de 1 PM – 14: 00, a fatia de saudação é produzida às 14: 00. |Não |EndOfInterval |
| anchorDateTime |Define a posição absoluta Olá no tempo usado pelos limites de fatia do Agendador toocompute conjunto de dados. <br/><br/><b>Observação</b>: se Olá AnchorDateTime tem partes de data mais granulares do que a frequência de hello, hello partes mais granulares são ignoradas. <br/><br/>Por exemplo, se hello <b>intervalo</b> é <b>por hora</b> (frequência: hora e intervalo: 1) e hello <b>AnchorDateTime</b> contém <b>minutos e segundos</b>, em seguida, Olá <b>minutos e segundos</b> partes da saudação AnchorDateTime são ignoradas. |Não |01/01/0001 |
| deslocamento |O intervalo de tempo pelo qual saudação inicial e final de todas as fatias de conjunto de dados são transferidos. <br/><br/><b>Observação</b>: se anchorDateTime e o deslocamento forem especificados, o resultado de saudação é shift Olá combinado. |Não |ND |

### <a name="offset-example"></a>exemplo de deslocamento
Por padrão, fatias (`"frequency": "Day", "interval": 1`) diárias começam em hora UTC de 12: 00 (meia-noite). Se deseja saudação inicial tempo toobe 6 horas UTC em vez disso, defina Olá deslocamento conforme Olá trecho de código a seguir: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Exemplo de anchorDateTime
No hello exemplo a seguir, Olá dataset é produzido cada 23 horas. Hello primeira fatia começa no tempo de saudação especificado por anchorDateTime hello, que é definido muito`2017-04-19T08:00:00` (hora UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Exemplo de deslocamento/estilo
Olá seguinte conjunto de dados é um conjunto de dados mensal e é gerado no dia 3 de cada mês às 8:00 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Política do conjunto de dados
Um conjunto de dados pode ter uma política de validação definida que especifica como dados de saudação gerados por uma execução de fatia podem ser validados antes de estar pronto para consumo. Nesses casos, após a fatia Olá concluiu a execução, status da fatia Olá saída será alterada muito**esperando** com um substatus de **validação**. Depois de fatias de saudação forem validadas, status da fatia Olá muda muito**pronto**. Se uma fatia de dados tiver sido gerada, mas não passou na validação de hello, execuções de atividade para frações de downstream que dependem dessa fatia não são processadas. [Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md) abrange Olá vários estados de fatias de dados na fábrica de dados.

Olá **política** seção na definição de conjunto de dados define os critérios de saudação ou condição Olá Olá fatias de conjunto de dados deve ser atendidos. Olá tabela a seguir descreve as propriedades você pode usar em Olá **política** seção:

| Nome da política | Descrição | Aplicado muito| Obrigatório | Padrão |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Valida que dados Olá em um **BLOBs do Azure** Olá de atende aos requisitos de tamanho mínimo (em megabytes). |Blob do Azure |Não |ND |
| minimumRows | Valida que dados Olá em um **banco de dados do SQL Azure** ou um **tabela do Azure** contém o número mínimo de saudação de linhas. |<ul><li>Banco de Dados SQL do Azure</li><li>tabela do Azure</li></ul> |Não |ND |

#### <a name="examples"></a>Exemplos
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Para obter mais informações sobre essas propriedades e exemplos, consulte o artigo [Criar conjuntos de dados](data-factory-create-datasets.md). 

## <a name="activity-policies"></a>Políticas de atividades
Políticas afetam o comportamento de tempo de execução de saudação de uma atividade, especialmente quando Olá fatia de uma tabela é processada. Olá, a tabela a seguir fornece detalhes de saudação.

| Propriedade | Valores permitidos | Valor Padrão | Descrição |
| --- | --- | --- | --- |
| simultaneidade |Inteiro  <br/><br/>Valor máximo: 10 |1 |Número de execuções concorrentes da atividade de saudação.<br/><br/>Ele determina o número de saudação de execuções de atividade paralela que pode ocorrer em intervalos diferentes. Por exemplo, se precisar de uma atividade toogo por meio de um grande conjunto de dados disponíveis, ter um valor maior da simultaneidade acelera o processamento de dados de saudação. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Determina a saudação ordenação de fatias de dados que estão sendo processadas.<br/><br/>Por exemplo, se houver duas fatias (uma ocorre às 16h e a outra às 17h),e ambas estiverem com a execução pendente. Se você definir Olá executionPriorityOrder toobe NewestFirst, a fatia Olá às 17H é processada primeiro. Da mesma forma se você definir Olá executionPriorityORder toobe OldestFIrst, em seguida, Olá fatia às 16: 00 é processada. |
| tentar novamente |Número inteiro<br/><br/>O valor máximo pode ser 10 |0 |Número de tentativas antes do processamento de dados de saudação de fatia Olá é marcado como falha. A execução da atividade para uma fatia de dados é repetida backup toohello especificado contagem de repetição. repetição de saudação é feita logo após a falha de saudação. |
| Tempo limite |TimeSpan |00:00:00 |Tempo limite para a atividade de saudação. Exemplo: 00:10:00 (implica o tempo limite de 10 minutos)<br/><br/>Se um valor não for especificado ou for 0, o tempo limite de saudação é infinito.<br/><br/>Se o tempo de processamento de dados de saudação em uma fatia exceder o valor de tempo limite de Olá, é cancelada e sistema Olá tentativas de processamento de saudação tooretry. o número de tentativas Olá depende da propriedade de repetição de saudação. Quando o tempo limite ocorre, o status de saudação é definido tooTimedOut. |
| atrasar |TimeSpan |00:00:00 |Especifique o intervalo de saudação antes do processamento de dados de saudação fatia começar.<br/><br/>execução de saudação da atividade de uma fatia de dados é iniciada depois Olá atraso é passado Olá esperado tempo de execução.<br/><br/>Exemplo: 00:10:00 (implica um atraso de 10 minutos) |
| longRetry |Inteiro <br/><br/>Valor máximo: 10 |1 |número de saudação de repetição longa tentativas antes da execução da fatia Olá falhou.<br/><br/>Tentativas de longRetry são espaçadas por longRetryInterval. Portanto, se você precisar toospecify um tempo entre tentativas de repetição, use longRetry. Se Retry e longRetry forem especificados, cada tentativa de longRetry inclui novas tentativas e Olá o número máximo de tentativas é repetir * longRetry.<br/><br/>Por exemplo, se tivermos Olá configurações na política de atividade Olá a seguir:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Pressupomos que haja apenas um tooexecute de fatia (status está esperando) e a execução da atividade Olá falha sempre. Inicialmente haveria três tentativas consecutivas de execução. Após cada tentativa, o status da fatia Olá deve ser Retry. Depois de tentativas primeiro 3 estão acima, o status da fatia Olá deve ser LongRetry.<br/><br/>Depois de uma hora (ou seja, valor de longRetryInteval), deve haver outro conjunto de três tentativas consecutivas de execução. Depois disso, o status da fatia Olá deve ser Failed e nenhuma outra tentativa será feita. Portanto, em geral, foram feitas seis tentativas.<br/><br/>Se qualquer execução for bem-sucedida, o status da fatia Olá seria pronto e não tentativa de nenhuma outra tentativa.<br/><br/>longRetry pode ser usado em situações em que dados dependentes chegam em momentos não determinística ou hello ambiente geral é instável em ocorre o processamento de dados. Nesses casos, não pode ajudar a fazer tentativas após o outro e fazer isso após um intervalo de resultados de tempo de saudação desejado de saída.<br/><br/>Advertência: não defina valores altos para longRetry ou longRetryInterval. Normalmente, os valores mais altos implicam outros problemas sistêmicos. |
| longRetryInterval |TimeSpan |00:00:00 |atraso de saudação entre as tentativas de repetição longa |

Para obter mais informações, consulte o artigo [Pipelines](data-factory-create-pipelines.md). 

## <a name="parallel-processing-of-data-slices"></a>Processamento paralelo de fatias de dados
Você pode definir data de início de saudação do pipeline de saudação no hello anterior. Quando você fizer isso, fábrica de dados calcula (back preenchimentos) todas as fatias de dados em Olá anterior e começa a processá-las automaticamente. Por exemplo: se você criar um pipeline com data de início de 2017-04-01 e Olá a data atual for 2017-04-10. Se cadência de saudação do hello saída de conjunto de dados é diariamente, em seguida, começa a fábrica de dados processar todas as fatias de saudação do 2017-04-01 too2017-04-09 imediatamente porque Olá data de início está no hello anterior. Olá fatia de 2017-04-10 não é processada ainda porque Olá o valor da propriedade de estilo na seção de disponibilidade de saudação é EndOfInterval por padrão. Hello mais antiga fatia é processada primeiro como padrão Olá valor executionPriorityOrder é OldestFirst. Para obter uma descrição da propriedade de estilo hello, consulte [conjunto de dados disponibilidade](#dataset-availability) seção. Para obter uma descrição da seção de executionPriorityOrder hello, consulte Olá [políticas de atividade](#activity-policies) seção. 

Você pode configurar toobe fatias de dados de back-preenchido processado em paralelo por configuração Olá **simultaneidade** propriedade Olá **política** seção de atividade Olá JSON. Essa propriedade determina o número de saudação de execuções de atividade paralela que pode ocorrer em intervalos diferentes. saudação padrão valor para a propriedade de simultaneidade Olá é 1. Portanto, uma única fatia é processada por vez, por padrão. valor máximo de saudação é 10. Quando precisa de um pipeline toogo por meio de um grande conjunto de dados disponíveis, ter um valor maior da simultaneidade acelera o processamento de dados de saudação. 

## <a name="rerun-a-failed-data-slice"></a>Executar novamente uma fatia de dados com falha
Quando ocorre um erro durante o processamento de uma fatia de dados, você pode descobrir por que falha no processamento da saudação de uma fatia usando folhas de portal do Azure ou monitorar e gerenciar aplicativos. Confira [Monitorar e gerenciar pipelines usando folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) ou [aplicativo de monitoramento e gerenciamento](data-factory-monitor-manage-app.md) para obter detalhes.

Considere Olá exemplo, que mostra duas atividades a seguir. Activity1 e Activity2. Atividade1 consome uma fatia de Dataset1 e produz uma fatia de Dataset2, que é utilizada como entrada pelo atividade2 tooproduce uma fatia da saudação Final do conjunto de dados.

![Fatia com falha](./media/data-factory-scheduling-and-execution/failed-slice.png)

Olá diagrama mostra que fora três fatias recentes, houve uma fatia de 9 de 10 AM falha produção Olá para Dataset2. Fábrica de dados controla automaticamente a dependência de conjunto de dados de série de tempo hello. Como resultado, ele não for iniciado atividade Olá executar fatia downstream do hello AM 9-10.

Ferramentas de monitoramento e gerenciamento da fábrica de dados permitem toodrill em logs de diagnóstico Olá para a raiz de Olá Olá fatia com falha tooeasily localizar causar problema hello e corrigi-lo. Depois de corrigir o problema de saudação, você pode iniciar facilmente tooproduce Olá falha fatia de execução da atividade hello. Para obter mais informações sobre como toorerun e entender as transições de estado para fatias de dados, consulte [monitoramento e gerenciamento de pipelines usando folhas de portal do Azure](data-factory-monitor-manage-pipelines.md) ou [monitoramento e gerenciamento de aplicativo](data-factory-monitor-manage-app.md).

Depois de você executar novamente Olá 9 10 AM fatiar para **Dataset2**, Data Factory inicia Olá executar fatia dependentes de 9 de 10 AM Olá no conjunto de dados final hello.

![Executar novamente uma fatia com falha](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Várias atividades em um pipeline
Você pode ter mais de uma atividade em um pipeline. Se você tiver várias atividades em um pipeline e saída de saudação de uma atividade não é uma entrada de outra atividade, atividades Olá podem executados em paralelo, se as fatias de dados de entrada para atividades de saudação estão prontas.

É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Olá atividades podem ser em Olá mesmo pipeline ou em pipelines diferentes. atividade de segundo Olá executa somente quando hello primeiro um concluir com êxito.

Por exemplo, considere hello quando um pipeline tem duas atividades a seguir:

1. A Atividade A1, que exige o conjunto de dados de entrada externo D1 e produz o conjunto de dados de saída D2.
2. A Atividade A2, que exige a entrada do conjunto de dados D2 e produz o conjunto de dados de saída D3.

Nesse cenário, as atividades A1 e A2 são em Olá mesmo pipeline. atividade de saudação que a1 é executado quando dados externos hello estão disponíveis e Olá agendado disponibilidade frequência é atingida. Hello atividade A2 é executado quando hello agendadas fatias de D2 fiquem disponíveis e hello frequência disponibilidade agendada for atingida. Se houver um erro em uma das fatias Olá no conjunto de dados D2, A2 não execute essa fatia até ela ficar disponível.

Olá o modo de exibição de diagrama com ambas as atividades no hello mesmo pipeline seria semelhante a saudação diagrama a seguir:

![Encadeamento de atividades no hello mesmo pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Como mencionado anteriormente, as atividades de saudação podem estar em pipelines diferentes. Nesse cenário, o modo de exibição de diagrama de saudação seria Olá diagrama a seguir:

![Encadeando atividades em dois pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

Consulte Olá [copiar sequencialmente](#copy-sequentially) seção apêndice Olá para obter um exemplo.

## <a name="model-datasets-with-different-frequencies"></a>Modelar conjuntos de dados com frequências diferentes
Exemplos de saudação as frequências de saudação de entrada e saída conjuntos de dados e hello atividade janela de agendamento foram Olá mesmo. Alguns cenários exigem a saída de tooproduce hello capacidade em uma frequência diferente de frequências de saudação de uma ou mais entradas. O Data Factory dá suporte à modelagem desses cenários.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Exemplo 1: gerar um relatório diário de saída para dados de entrada que estão disponíveis de hora em hora
Considere um cenário em que temos dados de medição de entrada de sensores disponíveis a cada hora no armazenamento de Blobs do Azure. Você deseja tooproduce um relatório diário de agregação com estatísticas, como média, máximo e mínimo para o dia de saudação com [atividade de hive de fábrica de dados](data-factory-hive-activity.md).

Veja como você pode modelar esse cenário com o Data Factory:

**Conjunto de dados de entrada**

Olá por hora de entrada arquivos são instalados na pasta Olá Olá dado dia. A disponibilidade de entrada é definida por **Hora** (frequência: Hora, intervalo: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Conjunto de dados de saída**

Um arquivo de saída é criado diariamente na pasta de saudação do dia. A disponibilidade de saída é definida em **Dia** (frequência: Dia e intervalo: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Atividade: atividade de hive em um pipeline**

script do hive Olá recebe Olá apropriado *DateTime* informações como parâmetros que usam Olá **WindowStart** , conforme mostrado no hello trecho de código a seguir. script do hive Olá usa dados Olá tooload variável da pasta correta Olá dia hello e Olá agregação toogenerate Olá saída.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

Olá diagrama a seguir mostra o cenário de saudação de um ponto de vista da dependência de dados.

![Dependência de dados](./media/data-factory-scheduling-and-execution/data-dependency.png)

Olá fatia de saída para cada dia depende 24 fatias por hora de um conjunto de dados de entrada. Calcula a fábrica dados essas dependências automaticamente descobrindo-Olá fatias de dados de entrada que se enquadram em Olá mesmo período de tempo como Olá toobe de fatias de saída produzido. Se qualquer uma das fatias de entrada hello 24 não estiver disponível, fábrica de dados aguarda Olá fatia entrada toobe pronto antes de iniciar a execução da atividade diária hello.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Exemplo 2: especificar dependência com expressões e funções do Data Factory
Vamos considerar outro cenário. Suponha que você tenha uma atividade de hive que processa dois conjuntos de dados de entrada. Um deles tem novos dados diariamente, mas o outro obtém novos dados toda semana. Suponha que você desejava toodo uma junção entre duas entradas de saudação e produzir uma saída de cada dia.

abordagem simples Hello, no qual fábrica de dados automaticamente descobre entrada direita Olá fatias tooprocess alinhando saída toohello tempo da fatia de dados do período não funciona.

Você deve especificar que para cada execução da atividade, Olá Data Factory deve usar a fatia de dados da semana passada Olá semanal entrada conjunto de dados. Você usar funções do Azure Data Factory conforme mostrado no hello tooimplement de trecho de código a seguir esse comportamento.

**Saída1: blob do Azure**

Olá primeiro entrada hello BLOBs do Azure está sendo atualizado diariamente.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Entrada2: blob do Azure**

Entrada2 é hello BLOBs do Azure que está sendo atualizada semanalmente.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Saída: blob do Azure**

Um arquivo de saída é criado diariamente na pasta de saudação do dia de saudação. Conjunto de disponibilidade de saída é muito**dia** (frequência: Day, intervalo: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Atividade: atividade de hive em um pipeline**

atividade de hive Olá usa Olá duas entradas e produz uma fatia de saída todos os dias. Você pode especificar toodepend de fatia de saída de cada dia em Olá fatia de entrada da semana anterior para a entrada semanal da seguinte maneira.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis às quais o Azure Data Factory dá suporte.

## <a name="appendix"></a>Apêndice

### <a name="example-copy-sequentially"></a>Exemplo: copiar sequencialmente
Ele é possível toorun várias operações de cópia após o outro de forma ordenada/sequencial. Por exemplo, você pode ter dois conjuntos de saída cópia atividades em um pipeline (CopyActivity1 e CopyActivity2) com hello após entradas dados:   

CopyActivity1

Entrada: Dataset. Saída: Dataset2.

CopyActivity2

Entrada: Dataset2.  Saída: Dataset3.

CopyActivity2 será executado somente se Olá CopyActivity1 foi executada com êxito e Dataset2 está disponível.

Aqui está o JSON de pipeline de exemplo hello:

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Observe que, no exemplo hello, conjunto de dados de saída de saudação do hello primeira atividade de cópia (Dataset2) é especificado como entrada para a atividade de segundo hello. Portanto, Olá segunda atividade executa somente quando Olá o conjunto de dados de saída da atividade primeiro hello está pronto.  

No exemplo hello, CopyActivity2 pode ter uma entrada diferente, como Dataset3, mas você especificar Dataset2 como uma entrada tooCopyActivity2, para que atividade de saudação não será executado até CopyActivity1 termina. Por exemplo:

CopyActivity1

Entrada: Dataset1. Saída: Dataset2.

CopyActivity2

Entradas: Dataset3, Dataset2. Saída: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Observe que no exemplo hello, dois conjuntos de dados de entrada são especificados para a segunda atividade de cópia hello. Quando várias entradas forem especificadas, somente Olá primeira entrada dataset é usado para copiar dados, mas outros conjuntos de dados são usados como as dependências. CopyActivity2 será iniciada somente depois hello seguintes condições forem atendidas:

* CopyActivity1 foi concluído com êxito e Dataset2 está disponível. Este conjunto de dados não é usado ao copiar dados tooDataset4. Ele atua apenas como uma dependência de agendamento de CopyActivity2.   
* Dataset3 está disponível. Este conjunto de dados representa dados de saudação toohello copiado de destino. 
