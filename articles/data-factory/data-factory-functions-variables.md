---
title: "aaaData variáveis de sistema e funções da fábrica | Microsoft Docs"
description: "Fornece uma lista de funções do Azure Data Factory e variáveis do sistema"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Azure Data Factory - Funções e Variáveis do Sistema
Este artigo fornece informações sobre funções e variáveis com suporte no Azure Data Factory.

## <a name="data-factory-system-variables"></a>Variáveis do sistema do Data Factory
| Nome de variável | Descrição | Escopo do objeto | Escopo JSON e casos de uso |
| --- | --- | --- | --- |
| WindowStart |Início do intervalo de tempo para a janela da execução de atividade atual |atividade |<ol><li>Especifica consultas de seleção de dados. Consulte os artigos de conector referenciados em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo.</li> |
| WindowEnd |Fim do intervalo de tempo para a janela da execução de atividade atual |atividade |igual a WindowStart. |
| SliceStart |Início do intervalo de tempo para a fatia de dados sendo gerada |atividade<br/>conjunto de dados |<ol><li>Especifique caminhos de pasta dinâmicos e nomes de arquivos enquanto estiver trabalhando com o [Blob do Azure](data-factory-azure-blob-connector.md) e [Conjuntos de dados do sistema de arquivos](data-factory-onprem-file-system-connector.md).</li><li>Especificar dependências de entrada com funções de data factory na coleção de entradas da atividade.</li></ol> |
| SliceEnd |Fim do intervalo de tempo da fatia de dados atual. |atividade<br/>dataset |o mesmo que SliceStart. |

> [!NOTE]
> No momento fábrica de dados requer que Olá agendar Olá especificado na atividade corresponde exatamente a agenda de saudação especificada na disponibilidade do conjunto de dados de saída de hello. Portanto, WindowStart, WindowEnd e SliceStart e SliceEnd sempre mapeiam toohello período e uma fatia de saída única a mesma hora.
> 

### <a name="example-for-using-a-system-variable"></a>Exemplo para usar uma variável de sistema
Em Olá seguindo o exemplo, ano, mês, dia e hora do **SliceStart** são extraídos em variáveis separadas que são usadas por **folderPath** e **fileName** propriedades.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Funções do Data Factory
Você pode usar as funções na fábrica de dados juntamente com variáveis de sistema para Olá propósitos a seguir:

1. Especificando consultas de seleção de dados (consulte os artigos de conector referenciados por Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo.
   
   Olá tooinvoke sintaxe é uma função da fábrica de dados:  **$$ <function>**  para consultas de seleção de dados e outras propriedades na atividade hello e conjuntos de dados.  
2. Especificar dependências de entrada com funções de data factory na coleção de entradas da atividade.
   
    $$ não é necessário para especificar expressões de dependência de entrada.     

Em Olá seguindo a amostra, **sqlReaderQuery** propriedade em um arquivo JSON é atribuída o valor de tooa retornado por Olá `Text.Format` função. Este exemplo também usa uma variável de sistema chamada **WindowStart**, que representa a hora de início de saudação da janela de execução da atividade hello.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

Confira o tópico [Cadeias de caracteres de formato de data e hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx) que descreve as diferentes opções de formatação que você pode usar (por exemplo: aa versus aaaa). 

### <a name="functions"></a>Funções
Olá tabelas a seguir lista todas as funções hello na fábrica de dados do Azure:

| Categoria | Função | Parâmetros | Descrição |
| --- | --- | --- | --- |
| Hora |AddHours(X,Y) |X: DateTime  <br/><br/>Y: int |Adiciona Y horas toohello momento X. <br/><br/>Exemplo: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Hora |AddMinutes(X,Y) |X: DateTime  <br/><br/>Y: int |Adiciona Y minutos tooX.<br/><br/>Exemplo: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Hora |StartOfHour(X) |X: DateTime  |Obtém Olá hora inicial da hora Olá representada pelo componente de hora de saudação do X. <br/><br/>Exemplo: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Data |AddDays(X,Y) |X: DateTime <br/><br/>Y: int |Adiciona Y dias tooX. <br/><br/>Exemplo: 15/9/2013 12:00:00 + 2 dias = 17/9/2013 12:00:00.<br/><br/>Você pode subtrair dias também, especificando Y como um número negativo.<br/><br/>Exemplo: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Data |AddMonths(X,Y) |X: DateTime <br/><br/>Y: int |Adiciona Y meses tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>Você pode subtrair meses também, especificando Y como um número negativo.<br/><br/>Exemplo: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Data |AddQuarters(X,Y) |X: DateTime  <br/><br/>Y: int |Adiciona Y * 3 meses tooX.<br/><br/>Exemplo: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Data |AddWeeks(X,Y) |X: DateTime <br/><br/>Y: int |Adiciona Y * 7 dias tooX<br/><br/>Exemplo: 15/9/2013 12:00:00 + 1 semana = 22/9/2013 12:00:00<br/><br/>Você pode subtrair semanas também, especificando Y como um número negativo.<br/><br/>Exemplo: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Data |AddYears(X,Y) |X: DateTime <br/><br/>Y: int |Adiciona Y anos tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>Você pode subtrair anos também, especificando Y como um número negativo.<br/><br/>Exemplo: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Data |Day(X) |X: DateTime  |Obtém o componente de dia de saudação do X.<br/><br/>Exemplo: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Data |DayOfWeek(X) |X: DateTime  |Obtém o dia de saudação do componente de semana de X.<br/><br/>Exemplo: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Data |DayOfYear(X) |X: DateTime  |Obtém Olá dia no ano Olá representado pelo componente de ano de saudação do X.<br/><br/>Exemplos:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Data |DaysInMonth(X) |X: DateTime  |Obtém os dias de saudação do mês de saudação representado pelo componente de mês de saudação do parâmetro X.<br/><br/>Exemplo: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Data |EndOfDay(X) |X: DateTime  |Obtém a data e hora Olá que representa o fim de saudação do dia de saudação (componente do dia) de X.<br/><br/>Exemplo: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Data |EndOfMonth(X) |X: DateTime  |Obtém a fim de saudação do mês de saudação representado pelo componente de mês do parâmetro X. <br/><br/>Exemplo: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (data que representa a fim de saudação do mês de setembro) |
| Data |StartOfDay(X) |X: DateTime  |Obtém o início de saudação do dia Olá representado pelo componente de dia de saudação do parâmetro X.<br/><br/>Exemplo: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X: Cadeia de caracteres |Analise a cadeia de caracteres X tooa data hora. |
| Datetime |Ticks(X) |X: DateTime  |Obtém tiques Olá propriedade Olá parâmetro X. Um tique é igual a 100 nanossegundos. valor Olá dessa propriedade representa o número de saudação de tiques que passaram desde 12:00:00 meia-noite de 1 de janeiro, 0001. |
| Texto |Format(X) |X: variável de cadeia de caracteres |Olá de formatos de texto (use `\\'` tooescape combinação `'` caractere).|

> [!IMPORTANT]
> Ao usar uma função dentro de outra função, não é necessário toouse  **$$**  prefixo para a função interna de saudação. Por exemplo: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' e RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). Neste exemplo, observe que  **$$**  prefixo não é usado para Olá **Time.AddHours** função. 

#### <a name="example"></a>Exemplo
Olá seguintes parâmetros de exemplo, a entrada e saída para a atividade de Hive Olá são determinados usando Olá `Text.Format` funções e variáveis de sistema SliceStart. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>Exemplo 2

Em Olá exemplo a seguir, Olá parâmetro DateTime hello que atividade de procedimento armazenado é determinada pelo texto de saudação. Formatar a função e Olá SliceStart variável. 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Exemplo 3
tooread dados do dia anterior em vez de dia representado pelo Olá SliceStart, use a função de AddDays de saudação conforme mostrado no exemplo a seguir de saudação: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

Confira o tópico [Cadeias de caracteres de formato de data e hora personalizado](https://msdn.microsoft.com/library/8kb3ddd4.aspx) que descreve as diferentes opções de formatação que você pode usar (por exemplo: aa versus aaaa). 

