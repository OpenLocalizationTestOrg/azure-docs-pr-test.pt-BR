---
title: "Agendamento e execução com o Data Factory | Microsoft Docs"
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="255a5-103">Agendamento e execução com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="255a5-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="255a5-104">Este artigo explica os aspectos de agendamento e execução do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="255a5-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="255a5-105">Este artigo presume que você compreenda as noções básicas sobre conceitos de modelo de aplicativo do data factory, incluindo atividade, pipelines, serviços vinculados e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="255a5-106">Para obter conceitos básicos do Azure Data Factory, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="255a5-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="255a5-107">Introdução ao Data Factory</span><span class="sxs-lookup"><span data-stu-id="255a5-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="255a5-108">Pipelines</span><span class="sxs-lookup"><span data-stu-id="255a5-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="255a5-109">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="255a5-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="255a5-110">Horas de início e término do pipeline</span><span class="sxs-lookup"><span data-stu-id="255a5-110">Start and end times of pipeline</span></span>
<span data-ttu-id="255a5-111">Um pipeline está ativo somente entre suas horas de **início** e **término**.</span><span class="sxs-lookup"><span data-stu-id="255a5-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="255a5-112">Ele não é executado antes da hora de início ou após a hora de término.</span><span class="sxs-lookup"><span data-stu-id="255a5-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="255a5-113">Se o pipeline estiver em pausa, ele não será executado, independentemente de suas horas de início e término.</span><span class="sxs-lookup"><span data-stu-id="255a5-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="255a5-114">Para um pipeline ser executado, ele não deve estar pausado.</span><span class="sxs-lookup"><span data-stu-id="255a5-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="255a5-115">É possível encontrar essas configurações (início, término, em pausa) na definição do pipeline:</span><span class="sxs-lookup"><span data-stu-id="255a5-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="255a5-116">Para obter mais informações sobre essas propriedades, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="255a5-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="255a5-117">Especificar o agendamento de uma atividade</span><span class="sxs-lookup"><span data-stu-id="255a5-117">Specify schedule for an activity</span></span>
<span data-ttu-id="255a5-118">Não é o pipeline que é executado.</span><span class="sxs-lookup"><span data-stu-id="255a5-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="255a5-119">São as atividades no pipeline que são executadas no contexto geral do pipeline.</span><span class="sxs-lookup"><span data-stu-id="255a5-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="255a5-120">É possível especificar um agendamento recorrente para uma atividade usando a seção **agendador** do JSON da atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="255a5-121">Por exemplo, você pode agendar uma atividade para ser executada a cada hora, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="255a5-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="255a5-122">Conforme mostrado no diagrama a seguir, especificar um agendamento para uma atividade cria uma série de janelas em cascata nas horas de início e término do pipeline.</span><span class="sxs-lookup"><span data-stu-id="255a5-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="255a5-123">Janelas em cascata são uma série de intervalos de tempo de tamanho fixo, não sobrepostos e contínuos.</span><span class="sxs-lookup"><span data-stu-id="255a5-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="255a5-124">Essas janelas lógicas em cascata de uma atividade são chamadas de **janelas de atividades**.</span><span class="sxs-lookup"><span data-stu-id="255a5-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Exemplo de agendador de atividades](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="255a5-126">A propriedade **agendador** de uma atividade é opcional.</span><span class="sxs-lookup"><span data-stu-id="255a5-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="255a5-127">Se você especificar essa propriedade, ela deverá corresponder à cadência especificada na definição do conjunto de dados de saída da atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="255a5-128">Atualmente, o conjunto de dados de saída é o que conduz o agendamento.</span><span class="sxs-lookup"><span data-stu-id="255a5-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="255a5-129">Portanto, é necessário criar um conjunto de dados de saída mesmo que a atividade não produza nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="255a5-130">Especificar o agendamento de um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="255a5-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="255a5-131">Uma atividade em um pipeline do Data Factory pode usar zero ou mais **conjuntos de dados** de entrada e gerar um ou mais conjuntos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="255a5-132">Para uma atividade, você pode especificar a cadência na qual os dados de entrada estão disponíveis ou os dados de saída são gerados usando a seção **disponibilidade** nas definições do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="255a5-133">**Frequência** na seção **disponibilidade** especifica a unidade de tempo.</span><span class="sxs-lookup"><span data-stu-id="255a5-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="255a5-134">Os valores permitidos para a frequência são: Minuto, Hora, Dia, Semana e Mês.</span><span class="sxs-lookup"><span data-stu-id="255a5-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="255a5-135">A propriedade **intervalo** na seção de disponibilidade especifica um multiplicador para a frequência.</span><span class="sxs-lookup"><span data-stu-id="255a5-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="255a5-136">Por exemplo: se a frequência for definida como Dia e o intervalo for definido como 1 para um conjunto de dados de saída, os dados de saída serão gerados diariamente.</span><span class="sxs-lookup"><span data-stu-id="255a5-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="255a5-137">Caso você especifique a frequência como minuto, recomendamos que defina o intervalo como não inferior a 15.</span><span class="sxs-lookup"><span data-stu-id="255a5-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="255a5-138">No exemplo a seguir, os dados de entrada estão disponíveis a cada hora e os dados de saída são gerados a cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="255a5-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="255a5-139">**Conjunto de dados de entrada:**</span><span class="sxs-lookup"><span data-stu-id="255a5-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="255a5-140">**Conjunto de dados de saída**</span><span class="sxs-lookup"><span data-stu-id="255a5-140">**Output dataset**</span></span>

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

<span data-ttu-id="255a5-141">Atualmente, **o conjunto de dados de saída conduz o agendamento**.</span><span class="sxs-lookup"><span data-stu-id="255a5-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="255a5-142">Em outras palavras, o agendamento especificado para o conjunto de dados de saída é usado para executar uma atividade em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="255a5-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="255a5-143">Portanto, é necessário criar um conjunto de dados de saída mesmo que a atividade não produza nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="255a5-144">Se a atividade não receber entradas, ignore a criação de conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="255a5-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="255a5-145">Na definição de pipeline a seguir, a propriedade **agendador** é usada para especificar um agendamento para a atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="255a5-146">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="255a5-146">This property is optional.</span></span> <span data-ttu-id="255a5-147">Atualmente, o agendamento da atividade deve corresponder ao agendamento especificado para o conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="255a5-148">Neste exemplo, a atividade é executada a cada hora entre as horas de início e término do pipeline.</span><span class="sxs-lookup"><span data-stu-id="255a5-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="255a5-149">Os dados de saída são gerados a cada hora para janelas de três horas (8h às 9h, 9h às 10h e 10h às 11h).</span><span class="sxs-lookup"><span data-stu-id="255a5-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="255a5-150">Cada unidade de dados consumida ou gerada por uma execução de atividade é chamada de uma **fatia de dados**.</span><span class="sxs-lookup"><span data-stu-id="255a5-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="255a5-151">O seguinte diagrama mostra um exemplo de uma atividade com um conjunto de dados de entrada e um conjunto de dados de saída:</span><span class="sxs-lookup"><span data-stu-id="255a5-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Agendador de disponibilidade](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="255a5-153">O diagrama mostra as fatias de dados por hora para o conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="255a5-154">O diagrama mostra três fatias de entrada que estão prontas para processamento.</span><span class="sxs-lookup"><span data-stu-id="255a5-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="255a5-155">A atividade de 10-11h está em andamento, produzindo a fatia de saída de 10-11h.</span><span class="sxs-lookup"><span data-stu-id="255a5-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="255a5-156">É possível acessar o intervalo de tempo associado à fatia atual no conjunto de dados JSON usando estas variáveis: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) e [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="255a5-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="255a5-157">Da mesma forma, é possível acessar o intervalo de tempo associado a uma janela de atividades usando WindowStart e WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="255a5-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="255a5-158">O agendamento de uma atividade deve corresponder ao agendamento do conjunto de dados de saída da atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="255a5-159">Portanto, os valores de SliceStart e SliceEnd são iguais aos valores de WindowStart e WindowEnd, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="255a5-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="255a5-160">Para obter mais informações sobre essas variáveis, consulte os artigos [Funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="255a5-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="255a5-161">Você pode usar essas variáveis para finalidades diferentes em sua atividade JSON.</span><span class="sxs-lookup"><span data-stu-id="255a5-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="255a5-162">Por exemplo, você pode usá-las para selecionar dados em conjuntos de dados de entrada e saída que representam dados de série temporal (por exemplo: 8h às 9h).</span><span class="sxs-lookup"><span data-stu-id="255a5-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="255a5-163">Este exemplo também usa **WindowStart** e **WindowEnd** para selecionar dados relevantes para uma execução de atividade e copia-os para um blob com o **folderPath** apropriado.</span><span class="sxs-lookup"><span data-stu-id="255a5-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="255a5-164">O **folderPath** é parametrizado para ter uma pasta separada para cada hora.</span><span class="sxs-lookup"><span data-stu-id="255a5-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="255a5-165">No exemplo anterior, o agendamento especificado para conjuntos de dados de entrada e saída é o mesmo (por hora).</span><span class="sxs-lookup"><span data-stu-id="255a5-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="255a5-166">Se o conjunto de dados de entrada da atividade estiver disponível em uma frequência diferente, digamos, a cada 15 minutos, a atividade que produz esse conjunto de dados de saída ainda será executada uma vez por hora, pois o conjunto de dados de saída é o que conduz o agendamento da atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="255a5-167">Para obter mais informações, consulte [Modelar conjuntos de dados com frequências diferentes](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="255a5-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="255a5-168">Políticas e disponibilidade do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="255a5-168">Dataset availability and policies</span></span>
<span data-ttu-id="255a5-169">Você já viu o uso da frequência e das propriedades de intervalo na seção de disponibilidade da definição do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="255a5-170">Há algumas outras propriedades que afetam o agendamento e a execução de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="255a5-171">Disponibilidade do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="255a5-171">Dataset availability</span></span> 
<span data-ttu-id="255a5-172">A tabela a seguir descreve as propriedades que você pode usar na seção de **availability**:</span><span class="sxs-lookup"><span data-stu-id="255a5-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="255a5-173">Propriedade</span><span class="sxs-lookup"><span data-stu-id="255a5-173">Property</span></span> | <span data-ttu-id="255a5-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="255a5-174">Description</span></span> | <span data-ttu-id="255a5-175">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="255a5-175">Required</span></span> | <span data-ttu-id="255a5-176">Padrão</span><span class="sxs-lookup"><span data-stu-id="255a5-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="255a5-177">frequência</span><span class="sxs-lookup"><span data-stu-id="255a5-177">frequency</span></span> |<span data-ttu-id="255a5-178">Especifica a unidade de tempo para a produção da fatia de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="255a5-179"><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês</span><span class="sxs-lookup"><span data-stu-id="255a5-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="255a5-180">Sim</span><span class="sxs-lookup"><span data-stu-id="255a5-180">Yes</span></span> |<span data-ttu-id="255a5-181">ND</span><span class="sxs-lookup"><span data-stu-id="255a5-181">NA</span></span> |
| <span data-ttu-id="255a5-182">intervalo</span><span class="sxs-lookup"><span data-stu-id="255a5-182">interval</span></span> |<span data-ttu-id="255a5-183">Especifica um multiplicador para frequência</span><span class="sxs-lookup"><span data-stu-id="255a5-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="255a5-184">"Intervalo de frequência x" determina a frequência com que a fatia é produzida.</span><span class="sxs-lookup"><span data-stu-id="255a5-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="255a5-185">Se você precisa que o conjunto de dados seja dividido por hora, defina <b>Frequência</b> como <b>Hora</b> e <b>intervalo</b> como <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="255a5-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="255a5-186"><b>Observação:</b>: caso você especifique a frequência como minuto, recomendamos que defina o intervalo como não inferior a 15</span><span class="sxs-lookup"><span data-stu-id="255a5-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="255a5-187">Sim</span><span class="sxs-lookup"><span data-stu-id="255a5-187">Yes</span></span> |<span data-ttu-id="255a5-188">ND</span><span class="sxs-lookup"><span data-stu-id="255a5-188">NA</span></span> |
| <span data-ttu-id="255a5-189">estilo</span><span class="sxs-lookup"><span data-stu-id="255a5-189">style</span></span> |<span data-ttu-id="255a5-190">Especifica se a fatia deve ser produzida no início/término do intervalo.</span><span class="sxs-lookup"><span data-stu-id="255a5-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="255a5-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="255a5-191">StartOfInterval</span></span></li><li><span data-ttu-id="255a5-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="255a5-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="255a5-193">Se a frequência for definida como Mês e o estilo como EndOfInterval, a fatia será produzida no último dia do mês.</span><span class="sxs-lookup"><span data-stu-id="255a5-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="255a5-194">Se o estilo for definido como StartOfInterval, a fatia será produzida no primeiro dia do mês.</span><span class="sxs-lookup"><span data-stu-id="255a5-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="255a5-195">Se a frequência for definida como Dia e o estilo como EndOfInterval, a fatia será produzida na última hora do dia.</span><span class="sxs-lookup"><span data-stu-id="255a5-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="255a5-196">Se a Frequência for definida como Hora e o estilo como EndOfInterval, a fatia será produzida ao final da hora.</span><span class="sxs-lookup"><span data-stu-id="255a5-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="255a5-197">Por exemplo, para uma fatia de período 13h – 14h, a fatia é produzida às 14h.</span><span class="sxs-lookup"><span data-stu-id="255a5-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="255a5-198">Não</span><span class="sxs-lookup"><span data-stu-id="255a5-198">No</span></span> |<span data-ttu-id="255a5-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="255a5-199">EndOfInterval</span></span> |
| <span data-ttu-id="255a5-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="255a5-200">anchorDateTime</span></span> |<span data-ttu-id="255a5-201">Define a posição absoluta no tempo usada pelo agendador para computar limites de fatia do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="255a5-202"><b>Observação:</b> se AnchorDateTime tiver partes de datas mais granulares do que a frequência, as partes mais granulares serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="255a5-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="255a5-203">Por exemplo, se o <b>intervalo</b> for <b>por hora</b> (frequência: hora e intervalo: 1) e o <b>AnchorDateTime</b> contiver <b>minutos e segundos</b>, as partes <b>minutos e segundos</b> do AnchorDateTime serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="255a5-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="255a5-204">Não</span><span class="sxs-lookup"><span data-stu-id="255a5-204">No</span></span> |<span data-ttu-id="255a5-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="255a5-205">01/01/0001</span></span> |
| <span data-ttu-id="255a5-206">deslocamento</span><span class="sxs-lookup"><span data-stu-id="255a5-206">offset</span></span> |<span data-ttu-id="255a5-207">O período de tempo no qual o início e o término de todas as fatias de conjunto de dados são deslocados.</span><span class="sxs-lookup"><span data-stu-id="255a5-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="255a5-208"><b>Observação:</b> se anchorDateTime e o deslocamento forem especificados, o resultado será um deslocamento combinado.</span><span class="sxs-lookup"><span data-stu-id="255a5-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="255a5-209">Não</span><span class="sxs-lookup"><span data-stu-id="255a5-209">No</span></span> |<span data-ttu-id="255a5-210">ND</span><span class="sxs-lookup"><span data-stu-id="255a5-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="255a5-211">exemplo de deslocamento</span><span class="sxs-lookup"><span data-stu-id="255a5-211">offset example</span></span>
<span data-ttu-id="255a5-212">Por padrão, fatias (`"frequency": "Day", "interval": 1`) diárias começam em hora UTC de 12: 00 (meia-noite).</span><span class="sxs-lookup"><span data-stu-id="255a5-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="255a5-213">Se desejar que a hora de início para hora UTC de 6 horas em vez disso, define o deslocamento, conforme mostrado no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="255a5-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="255a5-214">Exemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="255a5-214">anchorDateTime example</span></span>
<span data-ttu-id="255a5-215">No exemplo a seguir, o conjunto de dados é gerado uma vez a cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="255a5-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="255a5-216">Primeira fatia começa no momento especificado pelo anchorDateTime, que é definido como `2017-04-19T08:00:00` (hora UTC).</span><span class="sxs-lookup"><span data-stu-id="255a5-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="255a5-217">Exemplo de deslocamento/estilo</span><span class="sxs-lookup"><span data-stu-id="255a5-217">offset/style Example</span></span>
<span data-ttu-id="255a5-218">O conjunto de dados a seguir é um conjunto de dados mensal e é produzido no dia 3 de cada mês, às 8:00 h (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="255a5-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="255a5-219">Política do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="255a5-219">Dataset policy</span></span>
<span data-ttu-id="255a5-220">Um conjunto de dados pode ter uma política de validação definida que especifica como os dados gerados pela execução de uma fatia podem ser validados antes de estarem prontos para consumo.</span><span class="sxs-lookup"><span data-stu-id="255a5-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="255a5-221">Nesses casos, quando a execução da fatia tiver terminado, o status da fatia de saída será alterado para **Aguardando** com um substatus de **Validação**.</span><span class="sxs-lookup"><span data-stu-id="255a5-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="255a5-222">Depois que as fatias são validadas, o status de fatia é alterado para **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="255a5-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="255a5-223">Se uma fatia de dados foi produzida mas não passou na validação, as execuções de atividade para fatias downstream que dependem dessa fatia não são processadas.</span><span class="sxs-lookup"><span data-stu-id="255a5-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="255a5-224">[Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="255a5-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="255a5-225">A seção **política** na definição do conjunto de dados define os critérios ou a condição que as divisões de conjunto de dados devem atender.</span><span class="sxs-lookup"><span data-stu-id="255a5-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="255a5-226">A seguinte tabela descreve as propriedades que você pode usar na seção **política**:</span><span class="sxs-lookup"><span data-stu-id="255a5-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="255a5-227">Nome da política</span><span class="sxs-lookup"><span data-stu-id="255a5-227">Policy Name</span></span> | <span data-ttu-id="255a5-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="255a5-228">Description</span></span> | <span data-ttu-id="255a5-229">Aplicado a</span><span class="sxs-lookup"><span data-stu-id="255a5-229">Applied To</span></span> | <span data-ttu-id="255a5-230">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="255a5-230">Required</span></span> | <span data-ttu-id="255a5-231">Padrão</span><span class="sxs-lookup"><span data-stu-id="255a5-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="255a5-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="255a5-232">minimumSizeMB</span></span> | <span data-ttu-id="255a5-233">Valida que os dados em um **blob do Azure** atendem aos requisitos de tamanho mínimo (em megabytes).</span><span class="sxs-lookup"><span data-stu-id="255a5-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="255a5-234">blob do Azure</span><span class="sxs-lookup"><span data-stu-id="255a5-234">Azure Blob</span></span> |<span data-ttu-id="255a5-235">Não</span><span class="sxs-lookup"><span data-stu-id="255a5-235">No</span></span> |<span data-ttu-id="255a5-236">ND</span><span class="sxs-lookup"><span data-stu-id="255a5-236">NA</span></span> |
| <span data-ttu-id="255a5-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="255a5-237">minimumRows</span></span> | <span data-ttu-id="255a5-238">Valida que os dados em um **Banco de Dados SQL do Azure** ou uma **tabela do Azure** contêm o número mínimo de linhas.</span><span class="sxs-lookup"><span data-stu-id="255a5-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="255a5-239">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="255a5-239">Azure SQL Database</span></span></li><li><span data-ttu-id="255a5-240">tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="255a5-240">Azure Table</span></span></li></ul> |<span data-ttu-id="255a5-241">Não</span><span class="sxs-lookup"><span data-stu-id="255a5-241">No</span></span> |<span data-ttu-id="255a5-242">ND</span><span class="sxs-lookup"><span data-stu-id="255a5-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="255a5-243">Exemplos</span><span class="sxs-lookup"><span data-stu-id="255a5-243">Examples</span></span>
<span data-ttu-id="255a5-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="255a5-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="255a5-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="255a5-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="255a5-246">Para obter mais informações sobre essas propriedades e exemplos, consulte o artigo [Criar conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="255a5-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="255a5-247">Políticas de atividades</span><span class="sxs-lookup"><span data-stu-id="255a5-247">Activity policies</span></span>
<span data-ttu-id="255a5-248">As políticas afetam o comportamento de tempo de execução de uma atividade, especialmente quando a divisão de uma tabela é processada.</span><span class="sxs-lookup"><span data-stu-id="255a5-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="255a5-249">A tabela a seguir fornece os detalhes.</span><span class="sxs-lookup"><span data-stu-id="255a5-249">The following table provides the details.</span></span>

| <span data-ttu-id="255a5-250">Propriedade</span><span class="sxs-lookup"><span data-stu-id="255a5-250">Property</span></span> | <span data-ttu-id="255a5-251">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="255a5-251">Permitted values</span></span> | <span data-ttu-id="255a5-252">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="255a5-252">Default Value</span></span> | <span data-ttu-id="255a5-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="255a5-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="255a5-254">simultaneidade</span><span class="sxs-lookup"><span data-stu-id="255a5-254">concurrency</span></span> |<span data-ttu-id="255a5-255">Inteiro </span><span class="sxs-lookup"><span data-stu-id="255a5-255">Integer</span></span> <br/><br/><span data-ttu-id="255a5-256">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="255a5-256">Max value: 10</span></span> |<span data-ttu-id="255a5-257">1</span><span class="sxs-lookup"><span data-stu-id="255a5-257">1</span></span> |<span data-ttu-id="255a5-258">Número de execuções simultâneas da atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="255a5-259">Determina o número de execuções de atividade paralela que podem ocorrer em divisões diferentes.</span><span class="sxs-lookup"><span data-stu-id="255a5-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="255a5-260">Por exemplo, se uma atividade precisa passar por um grande conjunto de dados disponíveis, ter um valor de concorrência maior acelera o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="255a5-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="255a5-261">executionPriorityOrder</span></span> |<span data-ttu-id="255a5-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="255a5-262">NewestFirst</span></span><br/><br/><span data-ttu-id="255a5-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="255a5-263">OldestFirst</span></span> |<span data-ttu-id="255a5-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="255a5-264">OldestFirst</span></span> |<span data-ttu-id="255a5-265">Determina a ordem das divisões de dados que estão sendo processadas.</span><span class="sxs-lookup"><span data-stu-id="255a5-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="255a5-266">Por exemplo, se houver duas fatias (uma ocorre às 16h e a outra às 17h),e ambas estiverem com a execução pendente.</span><span class="sxs-lookup"><span data-stu-id="255a5-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="255a5-267">Se você definir executionPriorityOrder como NewestFirst, a divisão às 17h será processada primeiro.</span><span class="sxs-lookup"><span data-stu-id="255a5-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="255a5-268">De modo semelhante, se você definir executionPriorityORder como OldestFIrst, a fatia às 16h será processada.</span><span class="sxs-lookup"><span data-stu-id="255a5-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="255a5-269">tentar novamente</span><span class="sxs-lookup"><span data-stu-id="255a5-269">retry</span></span> |<span data-ttu-id="255a5-270">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="255a5-270">Integer</span></span><br/><br/><span data-ttu-id="255a5-271">O valor máximo pode ser 10</span><span class="sxs-lookup"><span data-stu-id="255a5-271">Max value can be 10</span></span> |<span data-ttu-id="255a5-272">0</span><span class="sxs-lookup"><span data-stu-id="255a5-272">0</span></span> |<span data-ttu-id="255a5-273">Número de novas tentativas antes do processamento de dados da divisão ser marcado como Com falha.</span><span class="sxs-lookup"><span data-stu-id="255a5-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="255a5-274">A execução da atividade para uma divisão de dados é repetida até a contagem de repetição especificada.</span><span class="sxs-lookup"><span data-stu-id="255a5-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="255a5-275">A nova tentativa é feita logo após a falha.</span><span class="sxs-lookup"><span data-stu-id="255a5-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="255a5-276">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="255a5-276">timeout</span></span> |<span data-ttu-id="255a5-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="255a5-277">TimeSpan</span></span> |<span data-ttu-id="255a5-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="255a5-278">00:00:00</span></span> |<span data-ttu-id="255a5-279">Tempo limite para a atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-279">Timeout for the activity.</span></span> <span data-ttu-id="255a5-280">Exemplo: 00:10:00 (implica o tempo limite de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="255a5-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="255a5-281">Se um valor não for especificado ou for 0, o tempo limite será infinito.</span><span class="sxs-lookup"><span data-stu-id="255a5-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="255a5-282">Se o tempo de processamento de dados em uma divisão exceder o valor de tempo limite, ele será cancelado e o sistema tentará repetir o processamento.</span><span class="sxs-lookup"><span data-stu-id="255a5-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="255a5-283">O número de repetições depende da propriedade de repetição.</span><span class="sxs-lookup"><span data-stu-id="255a5-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="255a5-284">Quando atingir o tempo limite, o status será TimedOut.</span><span class="sxs-lookup"><span data-stu-id="255a5-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="255a5-285">atrasar</span><span class="sxs-lookup"><span data-stu-id="255a5-285">delay</span></span> |<span data-ttu-id="255a5-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="255a5-286">TimeSpan</span></span> |<span data-ttu-id="255a5-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="255a5-287">00:00:00</span></span> |<span data-ttu-id="255a5-288">Especifique o atraso antes do processamento de dados da divisão começar.</span><span class="sxs-lookup"><span data-stu-id="255a5-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="255a5-289">A execução da atividade de uma fatia de dados será iniciada após o atraso passar do tempo de execução esperado.</span><span class="sxs-lookup"><span data-stu-id="255a5-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="255a5-290">Exemplo: 00:10:00 (implica um atraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="255a5-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="255a5-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="255a5-291">longRetry</span></span> |<span data-ttu-id="255a5-292">Inteiro </span><span class="sxs-lookup"><span data-stu-id="255a5-292">Integer</span></span><br/><br/><span data-ttu-id="255a5-293">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="255a5-293">Max value: 10</span></span> |<span data-ttu-id="255a5-294">1</span><span class="sxs-lookup"><span data-stu-id="255a5-294">1</span></span> |<span data-ttu-id="255a5-295">O número de tentativas repetidas longas antes que a execução da divisão falhe.</span><span class="sxs-lookup"><span data-stu-id="255a5-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="255a5-296">Tentativas de longRetry são espaçadas por longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="255a5-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="255a5-297">Portanto, se você precisar especificar um tempo entre tentativas de repetição, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="255a5-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="255a5-298">Se Retry e longRetry forem especificados, cada tentativa de longRetry incluirá tentativas de Retry, e o número máximo de tentativas será Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="255a5-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="255a5-299">Por exemplo, se tivermos as seguintes configurações na política de atividade:</span><span class="sxs-lookup"><span data-stu-id="255a5-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="255a5-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="255a5-300">Retry: 3</span></span><br/><span data-ttu-id="255a5-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="255a5-301">longRetry: 2</span></span><br/><span data-ttu-id="255a5-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="255a5-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="255a5-303">Presumindo que haja apenas uma fatia para execução (o status é Aguardando) e a execução da atividade sempre falhe.</span><span class="sxs-lookup"><span data-stu-id="255a5-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="255a5-304">Inicialmente haveria três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="255a5-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="255a5-305">Após cada tentativa, o status de divisão seria Retry.</span><span class="sxs-lookup"><span data-stu-id="255a5-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="255a5-306">Depois das três primeiras tentativas, o status da divisão seria LongRetry.</span><span class="sxs-lookup"><span data-stu-id="255a5-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="255a5-307">Depois de uma hora (ou seja, valor de longRetryInteval), deve haver outro conjunto de três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="255a5-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="255a5-308">Depois disso, o status da divisão seria Com falha e não haveria nova tentativa.</span><span class="sxs-lookup"><span data-stu-id="255a5-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="255a5-309">Portanto, em geral, foram feitas seis tentativas.</span><span class="sxs-lookup"><span data-stu-id="255a5-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="255a5-310">Se qualquer execução for bem-sucedida, o status da fatia seria Ready e não haverá mais nenhuma tentativa.</span><span class="sxs-lookup"><span data-stu-id="255a5-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="255a5-311">longRetry pode ser usado em situações em que dados dependentes chegam em horários não determinísticos ou o ambiente geral está instável onde o processamento de dados ocorre.</span><span class="sxs-lookup"><span data-stu-id="255a5-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="255a5-312">Nesses casos, fazer novas tentativas uma após a outra pode não ajudar e fazer isso após um intervalo de tempo resulta na saída desejada.</span><span class="sxs-lookup"><span data-stu-id="255a5-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="255a5-313">Advertência: não defina valores altos para longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="255a5-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="255a5-314">Normalmente, os valores mais altos implicam outros problemas sistêmicos.</span><span class="sxs-lookup"><span data-stu-id="255a5-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="255a5-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="255a5-315">longRetryInterval</span></span> |<span data-ttu-id="255a5-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="255a5-316">TimeSpan</span></span> |<span data-ttu-id="255a5-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="255a5-317">00:00:00</span></span> |<span data-ttu-id="255a5-318">O intervalo entre tentativas de repetição longa</span><span class="sxs-lookup"><span data-stu-id="255a5-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="255a5-319">Para obter mais informações, consulte o artigo [Pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="255a5-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="255a5-320">Processamento paralelo de fatias de dados</span><span class="sxs-lookup"><span data-stu-id="255a5-320">Parallel processing of data slices</span></span>
<span data-ttu-id="255a5-321">Você pode definir a data de início do pipeline no passado.</span><span class="sxs-lookup"><span data-stu-id="255a5-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="255a5-322">Quando você faz isso, o Data Factory calcula automaticamente (faz preenchimento de fundo) todas as fatias de dados no passado e começa a processá-las.</span><span class="sxs-lookup"><span data-stu-id="255a5-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="255a5-323">Por exemplo: se você criar um pipeline com a data de início 01/04/2017 e a data atual for 10/04/2017.</span><span class="sxs-lookup"><span data-stu-id="255a5-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="255a5-324">Se a cadência do conjunto de dados de saída for diária, o Data Factory começará a processar todas as fatias de 01/04/2017 a 09/04/2017 imediatamente porque a data de início está no passado.</span><span class="sxs-lookup"><span data-stu-id="255a5-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="255a5-325">A fatia de 10/04/2017 ainda não será processada porque o valor da propriedade de estilo na seção de disponibilidade é EndOfInterval por padrão.</span><span class="sxs-lookup"><span data-stu-id="255a5-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="255a5-326">A fatia mais antiga é processada primeiro, pois o valor padrão de executionPriorityOrder é OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="255a5-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="255a5-327">Para obter uma descrição da propriedade de estilo, consulte a seção [disponibilidade do conjunto de dados](#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="255a5-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="255a5-328">Para obter uma descrição da seção executionPriorityOrder, consulte a seção [políticas de atividades](#activity-policies).</span><span class="sxs-lookup"><span data-stu-id="255a5-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="255a5-329">Você pode configurar as fatias de dados com preenchimento de fundo para serem processadas em paralelo definindo a propriedade **simultaneidade** na seção **política** do JSON da atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="255a5-330">Essa propriedade determina o número de execuções de atividade paralela que podem ocorrer em fatias diferentes.</span><span class="sxs-lookup"><span data-stu-id="255a5-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="255a5-331">O valor padrão da propriedade de simultaneidade é 1.</span><span class="sxs-lookup"><span data-stu-id="255a5-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="255a5-332">Portanto, uma única fatia é processada por vez, por padrão.</span><span class="sxs-lookup"><span data-stu-id="255a5-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="255a5-333">O valor máximo é 10.</span><span class="sxs-lookup"><span data-stu-id="255a5-333">The maximum value is 10.</span></span> <span data-ttu-id="255a5-334">Quando um pipeline precisa passar por um grande conjunto de dados disponíveis, ter um valor de simultaneidade maior acelera o processamento dos dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="255a5-335">Executar novamente uma fatia de dados com falha</span><span class="sxs-lookup"><span data-stu-id="255a5-335">Rerun a failed data slice</span></span>
<span data-ttu-id="255a5-336">Quando ocorre um erro durante o processamento de uma fatia de dados, você pode descobrir por que o processamento de uma fatia falhou usando folhas do portal do Azure ou o Aplicativo Monitorar e Gerenciar.</span><span class="sxs-lookup"><span data-stu-id="255a5-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="255a5-337">Confira [Monitorar e gerenciar pipelines usando folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) ou [aplicativo de monitoramento e gerenciamento](data-factory-monitor-manage-app.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="255a5-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="255a5-338">Considere o exemplo a seguir, que mostra duas atividades.</span><span class="sxs-lookup"><span data-stu-id="255a5-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="255a5-339">Activity1 e Activity2.</span><span class="sxs-lookup"><span data-stu-id="255a5-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="255a5-340">A Activity1 consome uma fatia do Dataset1 e produz uma fatia do Dataset2, que é consumida como entrada pela Activity2 para gerar uma fatia do Conjunto de Dados Final.</span><span class="sxs-lookup"><span data-stu-id="255a5-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Fatia com falha](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="255a5-342">O diagrama mostra que, de três fatias recentes, houve uma falha ao produzir a fatia de 9-10h para Dataset2.</span><span class="sxs-lookup"><span data-stu-id="255a5-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="255a5-343">O Data Factory controla automaticamente a dependência para o conjunto de dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="255a5-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="255a5-344">Como resultado, ele não inicia a execução da atividade para a fatia downstream de 9-10h.</span><span class="sxs-lookup"><span data-stu-id="255a5-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="255a5-345">Ferramentas de gerenciamento e monitoramento do data factory permitem analisar os logs de diagnóstico da fatia com falha, para que você localize facilmente a causa raiz do problema e corrija-o.</span><span class="sxs-lookup"><span data-stu-id="255a5-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="255a5-346">Depois de corrigir o problema, você pode iniciar facilmente a execução da atividade para produzir a fatia com falha.</span><span class="sxs-lookup"><span data-stu-id="255a5-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="255a5-347">Para obter mais informações sobre como executar novamente e entender as transições de estado de fatias de dados, consulte [Monitorando e gerenciando pipelines usando folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) ou [Aplicativo de Monitoramento e Gerenciamento](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="255a5-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="255a5-348">Após você executar novamente a fatia de 9-10h para o **Dataset2**, o Data Factory iniciará a execução da fatia dependente de 9-10h no conjunto de dados final.</span><span class="sxs-lookup"><span data-stu-id="255a5-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Executar novamente uma fatia com falha](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="255a5-350">Várias atividades em um pipeline</span><span class="sxs-lookup"><span data-stu-id="255a5-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="255a5-351">Você pode ter mais de uma atividade em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="255a5-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="255a5-352">Caso você tenha várias atividades em um pipeline e a saída de uma atividade não seja uma entrada de outra atividade, as atividades poderão ser executadas em paralelo se as fatias de dados de entrada das atividades estiverem prontas.</span><span class="sxs-lookup"><span data-stu-id="255a5-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="255a5-353">É possível encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="255a5-354">As atividades podem estar no mesmo pipeline ou em pipelines diferentes.</span><span class="sxs-lookup"><span data-stu-id="255a5-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="255a5-355">A segunda atividade é executada apenas quando a primeira é concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="255a5-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="255a5-356">Por exemplo, considere o seguinte caso em que um pipeline tem duas atividades:</span><span class="sxs-lookup"><span data-stu-id="255a5-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="255a5-357">A Atividade A1, que exige o conjunto de dados de entrada externo D1 e produz o conjunto de dados de saída D2.</span><span class="sxs-lookup"><span data-stu-id="255a5-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="255a5-358">A Atividade A2, que exige a entrada do conjunto de dados D2 e produz o conjunto de dados de saída D3.</span><span class="sxs-lookup"><span data-stu-id="255a5-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="255a5-359">Nesse cenário, as atividades A1 e A2 estão no mesmo pipeline.</span><span class="sxs-lookup"><span data-stu-id="255a5-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="255a5-360">A atividade A1 é executada quando os dados externos estão disponíveis e a frequência de disponibilidade agendada é alcançada.</span><span class="sxs-lookup"><span data-stu-id="255a5-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="255a5-361">A atividade A2 é executada quando as fatias agendadas de D2 ficam disponíveis e a frequência de disponibilidade agendada é alcançada.</span><span class="sxs-lookup"><span data-stu-id="255a5-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="255a5-362">Se houver um erro em uma das fatias no conjunto de dados D2, A2 não será executada para essa fatia até que fique disponível.</span><span class="sxs-lookup"><span data-stu-id="255a5-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="255a5-363">O modo de exibição de Diagrama com ambas as atividades no mesmo pipeline seria semelhante ao seguinte diagrama:</span><span class="sxs-lookup"><span data-stu-id="255a5-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Encadeando atividades no mesmo pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="255a5-365">Conforme mencionado anteriormente, as atividades poderiam estar em pipelines diferentes.</span><span class="sxs-lookup"><span data-stu-id="255a5-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="255a5-366">Nesse cenário, a exibição de diagrama seria parecida com o seguinte diagrama:</span><span class="sxs-lookup"><span data-stu-id="255a5-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Encadeando atividades em dois pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="255a5-368">Consulte a seção [copiar sequencialmente](#copy-sequentially) no apêndice para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="255a5-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="255a5-369">Modelar conjuntos de dados com frequências diferentes</span><span class="sxs-lookup"><span data-stu-id="255a5-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="255a5-370">Nos exemplos, as frequências de conjuntos de dados de entrada e saída e a janela de agendamento de atividade foram iguais.</span><span class="sxs-lookup"><span data-stu-id="255a5-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="255a5-371">Alguns cenários exigem a capacidade de produzir saída em uma frequência diferente de frequências de uma ou mais entradas.</span><span class="sxs-lookup"><span data-stu-id="255a5-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="255a5-372">O Data Factory dá suporte à modelagem desses cenários.</span><span class="sxs-lookup"><span data-stu-id="255a5-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="255a5-373">Exemplo 1: gerar um relatório diário de saída para dados de entrada que estão disponíveis de hora em hora</span><span class="sxs-lookup"><span data-stu-id="255a5-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="255a5-374">Considere um cenário em que temos dados de medição de entrada de sensores disponíveis a cada hora no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="255a5-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="255a5-375">Você deseja produzir um relatório diário de agregação com estatísticas, como média, máximo e mínimo para o dia com a [Atividade hive do Data Factory](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="255a5-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="255a5-376">Veja como você pode modelar esse cenário com o Data Factory:</span><span class="sxs-lookup"><span data-stu-id="255a5-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="255a5-377">**Conjunto de dados de entrada**</span><span class="sxs-lookup"><span data-stu-id="255a5-377">**Input dataset**</span></span>

<span data-ttu-id="255a5-378">Os arquivos de entrada por hora são instalados na pasta para o dia determinado.</span><span class="sxs-lookup"><span data-stu-id="255a5-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="255a5-379">A disponibilidade de entrada é definida por **Hora** (frequência: Hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="255a5-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="255a5-380">**Conjunto de dados de saída**</span><span class="sxs-lookup"><span data-stu-id="255a5-380">**Output dataset**</span></span>

<span data-ttu-id="255a5-381">Um arquivo de saída é criado diariamente na pasta do dia.</span><span class="sxs-lookup"><span data-stu-id="255a5-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="255a5-382">A disponibilidade de saída é definida em **Dia** (frequência: Dia e intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="255a5-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="255a5-383">**Atividade: atividade de hive em um pipeline**</span><span class="sxs-lookup"><span data-stu-id="255a5-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="255a5-384">O script do hive recebe as informações de *DateTime* apropriadas como parâmetros que usam a variável **WindowStart** conforme mostrado no trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="255a5-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="255a5-385">O script do hive usa essa variável para carregar os dados da pasta correta para o dia e executar a agregação para gerar a saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="255a5-386">O diagrama a seguir mostra o cenário de um ponto de vista de dependência de dados.</span><span class="sxs-lookup"><span data-stu-id="255a5-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Dependência de dados](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="255a5-388">A fatia de saída para cada dia depende de 24 fatias horárias do conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="255a5-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="255a5-389">O Data Factory calcula essas dependências automaticamente descobrindo as fatias de dados de entrada que equivalem ao mesmo período de tempo utilizado para a produção da fatia de saída.</span><span class="sxs-lookup"><span data-stu-id="255a5-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="255a5-390">Se qualquer uma das 24 fatias de entrada não estiver disponível, o Data Factory aguardará até que a fatia de entrada esteja pronta antes de iniciar a execução da atividade diária.</span><span class="sxs-lookup"><span data-stu-id="255a5-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="255a5-391">Exemplo 2: especificar dependência com expressões e funções do Data Factory</span><span class="sxs-lookup"><span data-stu-id="255a5-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="255a5-392">Vamos considerar outro cenário.</span><span class="sxs-lookup"><span data-stu-id="255a5-392">Let’s consider another scenario.</span></span> <span data-ttu-id="255a5-393">Suponha que você tenha uma atividade de hive que processa dois conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="255a5-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="255a5-394">Um deles tem novos dados diariamente, mas o outro obtém novos dados toda semana.</span><span class="sxs-lookup"><span data-stu-id="255a5-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="255a5-395">Suponha que você queira fazer uma associação entre as duas entradas e produzir uma saída diariamente.</span><span class="sxs-lookup"><span data-stu-id="255a5-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="255a5-396">A abordagem simples, na qual o Data Factory detecta automaticamente as fatias de entrada certas a serem processadas alinhando-se ao período de tempo da fatia de dados de saída, não funciona.</span><span class="sxs-lookup"><span data-stu-id="255a5-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="255a5-397">Você precisa especificar isso para cada execução de atividade, o Data Factory deve usar a fatia de dados da semana passada para o conjunto de dados de entrada semanal.</span><span class="sxs-lookup"><span data-stu-id="255a5-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="255a5-398">Use as funções do Azure Data Factory conforme mostrado no trecho a seguir para implementar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="255a5-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="255a5-399">**Saída1: blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="255a5-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="255a5-400">A primeira entrada é blob do Azure que está sendo atualizado diariamente.</span><span class="sxs-lookup"><span data-stu-id="255a5-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="255a5-401">**Entrada2: blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="255a5-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="255a5-402">Entrada2 é o blob do Azure que está sendo atualizado semanalmente.</span><span class="sxs-lookup"><span data-stu-id="255a5-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="255a5-403">**Saída: blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="255a5-403">**Output: Azure blob**</span></span>

<span data-ttu-id="255a5-404">Um arquivo de saída é criado diariamente na pasta para o dia.</span><span class="sxs-lookup"><span data-stu-id="255a5-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="255a5-405">A disponibilidade de saída é definida como **dia** (frequência: Dia, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="255a5-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="255a5-406">**Atividade: atividade de hive em um pipeline**</span><span class="sxs-lookup"><span data-stu-id="255a5-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="255a5-407">A atividade de hive usa as duas entradas e produz uma fatia de saída todos os dias.</span><span class="sxs-lookup"><span data-stu-id="255a5-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="255a5-408">É possível especificar que a fatia de saída de cada dia dependa da fatia de entrada da semana anterior para a entrada semanal, como demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="255a5-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="255a5-409">Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis às quais o Azure Data Factory dá suporte.</span><span class="sxs-lookup"><span data-stu-id="255a5-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="255a5-410">Apêndice</span><span class="sxs-lookup"><span data-stu-id="255a5-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="255a5-411">Exemplo: copiar sequencialmente</span><span class="sxs-lookup"><span data-stu-id="255a5-411">Example: copy sequentially</span></span>
<span data-ttu-id="255a5-412">É possível executar várias operações de cópia, uma após a outra de maneira sequencial/ordenada.</span><span class="sxs-lookup"><span data-stu-id="255a5-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="255a5-413">Por exemplo, você pode ter duas atividades de cópia em um pipeline (CopyActivity1 e CopyActivity2) com os seguintes conjuntos de dados de saída dos dados de entrada:</span><span class="sxs-lookup"><span data-stu-id="255a5-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="255a5-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="255a5-414">CopyActivity1</span></span>

<span data-ttu-id="255a5-415">Entrada: Dataset.</span><span class="sxs-lookup"><span data-stu-id="255a5-415">Input: Dataset.</span></span> <span data-ttu-id="255a5-416">Saída: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="255a5-416">Output: Dataset2.</span></span>

<span data-ttu-id="255a5-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="255a5-417">CopyActivity2</span></span>

<span data-ttu-id="255a5-418">Entrada: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="255a5-418">Input: Dataset2.</span></span>  <span data-ttu-id="255a5-419">Saída: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="255a5-419">Output: Dataset3.</span></span>

<span data-ttu-id="255a5-420">CopyActivity2 seria executado somente se CopyActivity1 tivesse sido executado com êxito e Dataset2 estivesse disponível.</span><span class="sxs-lookup"><span data-stu-id="255a5-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="255a5-421">Veja o exemplo de JSON do pipeline:</span><span class="sxs-lookup"><span data-stu-id="255a5-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="255a5-422">Observe que no exemplo, o conjunto de dados de saída da primeira atividade de cópia (Dataset2) é especificado como entrada para a segunda atividade.</span><span class="sxs-lookup"><span data-stu-id="255a5-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="255a5-423">Portanto, a segunda atividade será executada somente quando o conjunto de dados de saída da primeira atividade estiver pronto.</span><span class="sxs-lookup"><span data-stu-id="255a5-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="255a5-424">No exemplo, CopyActivity2 pode ter uma entrada diferente como Dataset3, mas você especifica Dataset2 como uma entrada para CopyActivity2 para que a atividade não seja executada até que CopyActivity1 seja concluída.</span><span class="sxs-lookup"><span data-stu-id="255a5-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="255a5-425">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="255a5-425">For example:</span></span>

<span data-ttu-id="255a5-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="255a5-426">CopyActivity1</span></span>

<span data-ttu-id="255a5-427">Entrada: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="255a5-427">Input: Dataset1.</span></span> <span data-ttu-id="255a5-428">Saída: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="255a5-428">Output: Dataset2.</span></span>

<span data-ttu-id="255a5-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="255a5-429">CopyActivity2</span></span>

<span data-ttu-id="255a5-430">Entradas: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="255a5-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="255a5-431">Saída: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="255a5-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="255a5-432">Observe que no exemplo, dois conjuntos de dados de entrada são especificados para a segunda atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="255a5-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="255a5-433">Quando várias entradas forem especificadas, somente o primeiro conjunto de dados de entrada será usado para copiar dados, mas outros conjuntos de dados serão usados como dependências.</span><span class="sxs-lookup"><span data-stu-id="255a5-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="255a5-434">CopyActivity2 começaria apenas quando as seguintes condições fossem atendidas:</span><span class="sxs-lookup"><span data-stu-id="255a5-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="255a5-435">CopyActivity1 foi concluído com êxito e Dataset2 está disponível.</span><span class="sxs-lookup"><span data-stu-id="255a5-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="255a5-436">Esse conjunto de dados não é usado ao copiar dados para Dataset4.</span><span class="sxs-lookup"><span data-stu-id="255a5-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="255a5-437">Ele atua apenas como uma dependência de agendamento de CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="255a5-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="255a5-438">Dataset3 está disponível.</span><span class="sxs-lookup"><span data-stu-id="255a5-438">Dataset3 is available.</span></span> <span data-ttu-id="255a5-439">Esse conjunto de dados representa os dados que são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="255a5-439">This dataset represents the data that is copied to the destination.</span></span> 