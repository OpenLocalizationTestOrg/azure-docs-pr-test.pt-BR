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
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="6c87e-103">Agendamento e execução com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="6c87e-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="6c87e-104">Este artigo explica os aspectos de programação e a execução de Olá Olá do Azure Data Factory do modelo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c87e-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="6c87e-105">Este artigo presume que você compreenda as noções básicas sobre conceitos de modelo de aplicativo do data factory, incluindo atividade, pipelines, serviços vinculados e conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="6c87e-106">Para obter conceitos básicos do Azure Data Factory, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c87e-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="6c87e-107">Introdução tooData fábrica</span><span class="sxs-lookup"><span data-stu-id="6c87e-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="6c87e-108">Pipelines</span><span class="sxs-lookup"><span data-stu-id="6c87e-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="6c87e-109">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6c87e-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="6c87e-110">Horas de início e término do pipeline</span><span class="sxs-lookup"><span data-stu-id="6c87e-110">Start and end times of pipeline</span></span>
<span data-ttu-id="6c87e-111">Um pipeline está ativo somente entre sua hora de **início** e de **término**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="6c87e-112">Ele não é executado antes da hora de início do hello, ou após a hora de término hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="6c87e-113">Se Olá pipeline é pausado, ele não é executado independentemente de seu tempo de início e término.</span><span class="sxs-lookup"><span data-stu-id="6c87e-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="6c87e-114">Para um pipeline toorun, ela deve não ser pausada.</span><span class="sxs-lookup"><span data-stu-id="6c87e-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="6c87e-115">Você pode encontrar essas configurações (início, fim, pausado) na definição de pipeline de saudação:</span><span class="sxs-lookup"><span data-stu-id="6c87e-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="6c87e-116">Para obter mais informações sobre essas propriedades, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6c87e-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="6c87e-117">Especificar o agendamento de uma atividade</span><span class="sxs-lookup"><span data-stu-id="6c87e-117">Specify schedule for an activity</span></span>
<span data-ttu-id="6c87e-118">Não é pipeline Olá que é executado.</span><span class="sxs-lookup"><span data-stu-id="6c87e-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="6c87e-119">É atividades Olá Olá pipeline são executadas em Olá contexto geral do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="6c87e-120">Você pode especificar um agendamento recorrente para uma atividade usando Olá **Agendador** seção de JSON da atividade.</span><span class="sxs-lookup"><span data-stu-id="6c87e-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="6c87e-121">Por exemplo, você pode agendar uma atividade toorun por hora da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6c87e-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="6c87e-122">Conforme mostrado no diagrama a seguir de saudação, especificando que uma agenda para uma atividade cria uma série de janelas em cascata com em Olá pipeline de início e término.</span><span class="sxs-lookup"><span data-stu-id="6c87e-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="6c87e-123">Janelas em cascata são uma série de intervalos de tempo de tamanho fixo, não sobrepostos e contínuos.</span><span class="sxs-lookup"><span data-stu-id="6c87e-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="6c87e-124">Essas janelas lógicas em cascata de uma atividade são chamadas de **janelas de atividades**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Exemplo de agendador de atividades](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="6c87e-126">Olá **Agendador** propriedade para uma atividade é opcional.</span><span class="sxs-lookup"><span data-stu-id="6c87e-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="6c87e-127">Se você especificar essa propriedade, ele deve corresponder cadência Olá que seja especificada na definição de saudação do conjunto de dados de saída para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="6c87e-128">Atualmente, o conjunto de dados de saída é quais unidades Olá agenda.</span><span class="sxs-lookup"><span data-stu-id="6c87e-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="6c87e-129">Portanto, você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="6c87e-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="6c87e-130">Especificar o agendamento de um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6c87e-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="6c87e-131">Uma atividade em um pipeline do Data Factory pode usar zero ou mais **conjuntos de dados** de entrada e gerar um ou mais conjuntos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="6c87e-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="6c87e-132">Para uma atividade, você pode especificar o ritmo de saudação em qual Olá dados de entrada estão disponíveis ou dados de saída de saudação são produzidos usando Olá **disponibilidade** seção definições de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="6c87e-133">**Frequência** em Olá **disponibilidade** seção especifica a unidade de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="6c87e-134">Olá valores permitidos para frequência são: minuto, hora, dia, semana e mês.</span><span class="sxs-lookup"><span data-stu-id="6c87e-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="6c87e-135">Olá **intervalo** propriedade na seção de disponibilidade de saudação especifica um multiplicador para frequência.</span><span class="sxs-lookup"><span data-stu-id="6c87e-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="6c87e-136">Por exemplo: se a frequência de saudação for definida tooDay e intervalo é definido too1 para um conjunto de dados de saída, dados de saída de saudação são produzidos diariamente.</span><span class="sxs-lookup"><span data-stu-id="6c87e-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="6c87e-137">Se você especificar a frequência de saudação minuto, recomendamos que você defina Olá intervalo toono menos de 15.</span><span class="sxs-lookup"><span data-stu-id="6c87e-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="6c87e-138">No hello exemplo a seguir, os dados de entrada hello estão disponíveis por hora e dados de saída de saudação são gerados por hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="6c87e-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="6c87e-139">**Conjunto de dados de entrada:**</span><span class="sxs-lookup"><span data-stu-id="6c87e-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="6c87e-140">**Conjunto de dados de saída**</span><span class="sxs-lookup"><span data-stu-id="6c87e-140">**Output dataset**</span></span>

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

<span data-ttu-id="6c87e-141">Atualmente, **dataset unidades Olá agenda**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="6c87e-142">Em outras palavras, a agenda de saudação especificada para o conjunto de dados de saída de saudação é usado toorun uma atividade em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6c87e-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="6c87e-143">Portanto, você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="6c87e-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="6c87e-144">Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando.</span><span class="sxs-lookup"><span data-stu-id="6c87e-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="6c87e-145">Seguir Olá pipeline definição, hello **Agendador** propriedade é agenda toospecify usado para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="6c87e-146">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="6c87e-146">This property is optional.</span></span> <span data-ttu-id="6c87e-147">No momento, agenda hello atividade Olá deve coincidir com a agenda Olá especificada para o conjunto de dados de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
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

<span data-ttu-id="6c87e-148">Neste exemplo, hello atividade é executada por hora entre hello início e término horas do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="6c87e-149">Olá dados de saída são produzidos por hora para windows de três horas (8: 00 - 9 AM, 9: 00 - 10: 00 e 10 AM - 11: 00).</span><span class="sxs-lookup"><span data-stu-id="6c87e-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="6c87e-150">Cada unidade de dados consumida ou gerada por uma execução de atividade é chamada de uma **fatia de dados**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="6c87e-151">Olá diagrama a seguir mostra um exemplo de uma atividade com um conjunto de dados de entrada e um conjunto de dados de saída:</span><span class="sxs-lookup"><span data-stu-id="6c87e-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Agendador de disponibilidade](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="6c87e-153">diagrama de saudação mostra por hora Olá fatias de dados para saudação de entrada e saída do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="6c87e-154">diagrama de saudação mostra três fatias de entrada que estão prontas para processamento.</span><span class="sxs-lookup"><span data-stu-id="6c87e-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="6c87e-155">atividade de 10-11 AM Hello está em andamento, produzindo a fatia de saída do hello 10-11 AM.</span><span class="sxs-lookup"><span data-stu-id="6c87e-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="6c87e-156">Você pode acessar o intervalo de tempo de saudação associado com a fatia atual Olá Olá conjunto de dados JSON usando variáveis: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) e [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="6c87e-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="6c87e-157">Da mesma forma, você pode acessar o intervalo de tempo de saudação associado com uma janela de atividade usando hello WindowStart e WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="6c87e-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="6c87e-158">agenda saudação de uma atividade deve coincidir com a agenda de saudação do conjunto de dados de saída de hello atividade Olá.</span><span class="sxs-lookup"><span data-stu-id="6c87e-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="6c87e-159">Portanto, Olá SliceStart e SliceEnd valores são Olá mesmo como valores WindowStart e WindowEnd respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6c87e-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="6c87e-160">Para obter mais informações sobre essas variáveis, consulte os artigos [Funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="6c87e-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="6c87e-161">Você pode usar essas variáveis para finalidades diferentes em sua atividade JSON.</span><span class="sxs-lookup"><span data-stu-id="6c87e-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="6c87e-162">Por exemplo, você pode usá-los tooselect dados de entrada e saídos conjuntos de dados que representa dados de série temporal (por exemplo: Estou too9 de AM 8).</span><span class="sxs-lookup"><span data-stu-id="6c87e-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="6c87e-163">Este exemplo também usa **WindowStart** e **WindowEnd** tooselect de dados relevantes para uma atividade executar e copie-o blob tooa com hello apropriado **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="6c87e-164">Olá **folderPath** é parametrizada toohave uma pasta separada para cada hora.</span><span class="sxs-lookup"><span data-stu-id="6c87e-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="6c87e-165">Em Olá anterior de exemplo, agendamento de saudação especificado para conjuntos de dados de entrada e saídos é Olá mesmo (por hora).</span><span class="sxs-lookup"><span data-stu-id="6c87e-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="6c87e-166">Se o conjunto de dados de entrada de hello atividade hello está disponível em uma frequência diferente, significa que a cada 15 minutos, atividade Olá que produz este conjunto de dados de saída continuará sendo executada uma vez por hora, como conjunto de dados de saída de saudação é quais unidades Olá agenda de atividade.</span><span class="sxs-lookup"><span data-stu-id="6c87e-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="6c87e-167">Para obter mais informações, consulte [Modelar conjuntos de dados com frequências diferentes](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="6c87e-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="6c87e-168">Políticas e disponibilidade do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6c87e-168">Dataset availability and policies</span></span>
<span data-ttu-id="6c87e-169">Você viu que o uso de saudação de frequência e o intervalo de propriedades na seção de disponibilidade de saudação da definição de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="6c87e-170">Há algumas outras propriedades que afetam a saudação de agendamento e execução de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="6c87e-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="6c87e-171">Disponibilidade do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6c87e-171">Dataset availability</span></span> 
<span data-ttu-id="6c87e-172">Olá tabela a seguir descreve as propriedades você pode usar em Olá **disponibilidade** seção:</span><span class="sxs-lookup"><span data-stu-id="6c87e-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="6c87e-173">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6c87e-173">Property</span></span> | <span data-ttu-id="6c87e-174">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c87e-174">Description</span></span> | <span data-ttu-id="6c87e-175">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6c87e-175">Required</span></span> | <span data-ttu-id="6c87e-176">Padrão</span><span class="sxs-lookup"><span data-stu-id="6c87e-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c87e-177">frequência</span><span class="sxs-lookup"><span data-stu-id="6c87e-177">frequency</span></span> |<span data-ttu-id="6c87e-178">Especifica a unidade de tempo de saudação de produção de fatia do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="6c87e-179"><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês</span><span class="sxs-lookup"><span data-stu-id="6c87e-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="6c87e-180">Sim</span><span class="sxs-lookup"><span data-stu-id="6c87e-180">Yes</span></span> |<span data-ttu-id="6c87e-181">ND</span><span class="sxs-lookup"><span data-stu-id="6c87e-181">NA</span></span> |
| <span data-ttu-id="6c87e-182">intervalo</span><span class="sxs-lookup"><span data-stu-id="6c87e-182">interval</span></span> |<span data-ttu-id="6c87e-183">Especifica um multiplicador para frequência</span><span class="sxs-lookup"><span data-stu-id="6c87e-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="6c87e-184">"Intervalo de frequência x" determina com que frequência hello fatia é produzida.</span><span class="sxs-lookup"><span data-stu-id="6c87e-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="6c87e-185">Se você precisar hello toobe de conjunto de dados dividido por hora, defina <b>frequência</b> muito<b>hora</b>, e <b>intervalo</b> muito<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="6c87e-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="6c87e-186"><b>Observação</b>: se você especificar a frequência como minuto, recomendamos que você defina Olá intervalo toono menor que 15</span><span class="sxs-lookup"><span data-stu-id="6c87e-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="6c87e-187">Sim</span><span class="sxs-lookup"><span data-stu-id="6c87e-187">Yes</span></span> |<span data-ttu-id="6c87e-188">ND</span><span class="sxs-lookup"><span data-stu-id="6c87e-188">NA</span></span> |
| <span data-ttu-id="6c87e-189">estilo</span><span class="sxs-lookup"><span data-stu-id="6c87e-189">style</span></span> |<span data-ttu-id="6c87e-190">Especifica se a fatia Olá deve ser produzida no hello início/término do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="6c87e-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="6c87e-191">StartOfInterval</span></span></li><li><span data-ttu-id="6c87e-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6c87e-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="6c87e-193">Quando frequência é definida tooMonth e o estilo definido tooEndOfInterval, fatia de saudação é produzida no último dia do mês de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="6c87e-194">Se o estilo de saudação é definido tooStartOfInterval, Olá fatia é produzida no hello primeiro dia do mês.</span><span class="sxs-lookup"><span data-stu-id="6c87e-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="6c87e-195">Quando frequência é definida tooDay e o estilo definido tooEndOfInterval, fatia de Olá é produzida no hello última hora do dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="6c87e-196">Quando frequência é definida tooHour e o estilo definido tooEndOfInterval, fatia de Olá é produzida no final de saudação de hora hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="6c87e-197">Por exemplo, para uma fatia de período de 1 PM – 14: 00, a fatia de saudação é produzida às 14: 00.</span><span class="sxs-lookup"><span data-stu-id="6c87e-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="6c87e-198">Não</span><span class="sxs-lookup"><span data-stu-id="6c87e-198">No</span></span> |<span data-ttu-id="6c87e-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6c87e-199">EndOfInterval</span></span> |
| <span data-ttu-id="6c87e-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="6c87e-200">anchorDateTime</span></span> |<span data-ttu-id="6c87e-201">Define a posição absoluta Olá no tempo usado pelos limites de fatia do Agendador toocompute conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="6c87e-202"><b>Observação</b>: se Olá AnchorDateTime tem partes de data mais granulares do que a frequência de hello, hello partes mais granulares são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="6c87e-203">Por exemplo, se hello <b>intervalo</b> é <b>por hora</b> (frequência: hora e intervalo: 1) e hello <b>AnchorDateTime</b> contém <b>minutos e segundos</b>, em seguida, Olá <b>minutos e segundos</b> partes da saudação AnchorDateTime são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="6c87e-204">Não</span><span class="sxs-lookup"><span data-stu-id="6c87e-204">No</span></span> |<span data-ttu-id="6c87e-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="6c87e-205">01/01/0001</span></span> |
| <span data-ttu-id="6c87e-206">deslocamento</span><span class="sxs-lookup"><span data-stu-id="6c87e-206">offset</span></span> |<span data-ttu-id="6c87e-207">O intervalo de tempo pelo qual saudação inicial e final de todas as fatias de conjunto de dados são transferidos.</span><span class="sxs-lookup"><span data-stu-id="6c87e-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="6c87e-208"><b>Observação</b>: se anchorDateTime e o deslocamento forem especificados, o resultado de saudação é shift Olá combinado.</span><span class="sxs-lookup"><span data-stu-id="6c87e-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="6c87e-209">Não</span><span class="sxs-lookup"><span data-stu-id="6c87e-209">No</span></span> |<span data-ttu-id="6c87e-210">ND</span><span class="sxs-lookup"><span data-stu-id="6c87e-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="6c87e-211">exemplo de deslocamento</span><span class="sxs-lookup"><span data-stu-id="6c87e-211">offset example</span></span>
<span data-ttu-id="6c87e-212">Por padrão, fatias (`"frequency": "Day", "interval": 1`) diárias começam em hora UTC de 12: 00 (meia-noite).</span><span class="sxs-lookup"><span data-stu-id="6c87e-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="6c87e-213">Se deseja saudação inicial tempo toobe 6 horas UTC em vez disso, defina Olá deslocamento conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c87e-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="6c87e-214">Exemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="6c87e-214">anchorDateTime example</span></span>
<span data-ttu-id="6c87e-215">No hello exemplo a seguir, Olá dataset é produzido cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="6c87e-216">Hello primeira fatia começa no tempo de saudação especificado por anchorDateTime hello, que é definido muito`2017-04-19T08:00:00` (hora UTC).</span><span class="sxs-lookup"><span data-stu-id="6c87e-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="6c87e-217">Exemplo de deslocamento/estilo</span><span class="sxs-lookup"><span data-stu-id="6c87e-217">offset/style Example</span></span>
<span data-ttu-id="6c87e-218">Olá seguinte conjunto de dados é um conjunto de dados mensal e é gerado no dia 3 de cada mês às 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="6c87e-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="6c87e-219">Política do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6c87e-219">Dataset policy</span></span>
<span data-ttu-id="6c87e-220">Um conjunto de dados pode ter uma política de validação definida que especifica como dados de saudação gerados por uma execução de fatia podem ser validados antes de estar pronto para consumo.</span><span class="sxs-lookup"><span data-stu-id="6c87e-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="6c87e-221">Nesses casos, após a fatia Olá concluiu a execução, status da fatia Olá saída será alterada muito**esperando** com um substatus de **validação**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="6c87e-222">Depois de fatias de saudação forem validadas, status da fatia Olá muda muito**pronto**.</span><span class="sxs-lookup"><span data-stu-id="6c87e-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="6c87e-223">Se uma fatia de dados tiver sido gerada, mas não passou na validação de hello, execuções de atividade para frações de downstream que dependem dessa fatia não são processadas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="6c87e-224">[Monitorar e gerenciar pipelines](data-factory-monitor-manage-pipelines.md) abrange Olá vários estados de fatias de dados na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="6c87e-225">Olá **política** seção na definição de conjunto de dados define os critérios de saudação ou condição Olá Olá fatias de conjunto de dados deve ser atendidos.</span><span class="sxs-lookup"><span data-stu-id="6c87e-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="6c87e-226">Olá tabela a seguir descreve as propriedades você pode usar em Olá **política** seção:</span><span class="sxs-lookup"><span data-stu-id="6c87e-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="6c87e-227">Nome da política</span><span class="sxs-lookup"><span data-stu-id="6c87e-227">Policy Name</span></span> | <span data-ttu-id="6c87e-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c87e-228">Description</span></span> | <span data-ttu-id="6c87e-229">Aplicado muito</span><span class="sxs-lookup"><span data-stu-id="6c87e-229">Applied too</span></span>| <span data-ttu-id="6c87e-230">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6c87e-230">Required</span></span> | <span data-ttu-id="6c87e-231">Padrão</span><span class="sxs-lookup"><span data-stu-id="6c87e-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6c87e-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="6c87e-232">minimumSizeMB</span></span> | <span data-ttu-id="6c87e-233">Valida que dados Olá em um **BLOBs do Azure** Olá de atende aos requisitos de tamanho mínimo (em megabytes).</span><span class="sxs-lookup"><span data-stu-id="6c87e-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="6c87e-234">Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="6c87e-234">Azure Blob</span></span> |<span data-ttu-id="6c87e-235">Não</span><span class="sxs-lookup"><span data-stu-id="6c87e-235">No</span></span> |<span data-ttu-id="6c87e-236">ND</span><span class="sxs-lookup"><span data-stu-id="6c87e-236">NA</span></span> |
| <span data-ttu-id="6c87e-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="6c87e-237">minimumRows</span></span> | <span data-ttu-id="6c87e-238">Valida que dados Olá em um **banco de dados do SQL Azure** ou um **tabela do Azure** contém o número mínimo de saudação de linhas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="6c87e-239">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="6c87e-239">Azure SQL Database</span></span></li><li><span data-ttu-id="6c87e-240">tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="6c87e-240">Azure Table</span></span></li></ul> |<span data-ttu-id="6c87e-241">Não</span><span class="sxs-lookup"><span data-stu-id="6c87e-241">No</span></span> |<span data-ttu-id="6c87e-242">ND</span><span class="sxs-lookup"><span data-stu-id="6c87e-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="6c87e-243">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6c87e-243">Examples</span></span>
<span data-ttu-id="6c87e-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="6c87e-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="6c87e-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="6c87e-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="6c87e-246">Para obter mais informações sobre essas propriedades e exemplos, consulte o artigo [Criar conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6c87e-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="6c87e-247">Políticas de atividades</span><span class="sxs-lookup"><span data-stu-id="6c87e-247">Activity policies</span></span>
<span data-ttu-id="6c87e-248">Políticas afetam o comportamento de tempo de execução de saudação de uma atividade, especialmente quando Olá fatia de uma tabela é processada.</span><span class="sxs-lookup"><span data-stu-id="6c87e-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="6c87e-249">Olá, a tabela a seguir fornece detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="6c87e-250">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6c87e-250">Property</span></span> | <span data-ttu-id="6c87e-251">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6c87e-251">Permitted values</span></span> | <span data-ttu-id="6c87e-252">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="6c87e-252">Default Value</span></span> | <span data-ttu-id="6c87e-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="6c87e-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c87e-254">simultaneidade</span><span class="sxs-lookup"><span data-stu-id="6c87e-254">concurrency</span></span> |<span data-ttu-id="6c87e-255">Inteiro </span><span class="sxs-lookup"><span data-stu-id="6c87e-255">Integer</span></span> <br/><br/><span data-ttu-id="6c87e-256">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="6c87e-256">Max value: 10</span></span> |<span data-ttu-id="6c87e-257">1</span><span class="sxs-lookup"><span data-stu-id="6c87e-257">1</span></span> |<span data-ttu-id="6c87e-258">Número de execuções concorrentes da atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="6c87e-259">Ele determina o número de saudação de execuções de atividade paralela que pode ocorrer em intervalos diferentes.</span><span class="sxs-lookup"><span data-stu-id="6c87e-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="6c87e-260">Por exemplo, se precisar de uma atividade toogo por meio de um grande conjunto de dados disponíveis, ter um valor maior da simultaneidade acelera o processamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="6c87e-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="6c87e-261">executionPriorityOrder</span></span> |<span data-ttu-id="6c87e-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="6c87e-262">NewestFirst</span></span><br/><br/><span data-ttu-id="6c87e-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="6c87e-263">OldestFirst</span></span> |<span data-ttu-id="6c87e-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="6c87e-264">OldestFirst</span></span> |<span data-ttu-id="6c87e-265">Determina a saudação ordenação de fatias de dados que estão sendo processadas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="6c87e-266">Por exemplo, se houver duas fatias (uma ocorre às 16h e a outra às 17h),e ambas estiverem com a execução pendente.</span><span class="sxs-lookup"><span data-stu-id="6c87e-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="6c87e-267">Se você definir Olá executionPriorityOrder toobe NewestFirst, a fatia Olá às 17H é processada primeiro.</span><span class="sxs-lookup"><span data-stu-id="6c87e-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="6c87e-268">Da mesma forma se você definir Olá executionPriorityORder toobe OldestFIrst, em seguida, Olá fatia às 16: 00 é processada.</span><span class="sxs-lookup"><span data-stu-id="6c87e-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="6c87e-269">tentar novamente</span><span class="sxs-lookup"><span data-stu-id="6c87e-269">retry</span></span> |<span data-ttu-id="6c87e-270">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="6c87e-270">Integer</span></span><br/><br/><span data-ttu-id="6c87e-271">O valor máximo pode ser 10</span><span class="sxs-lookup"><span data-stu-id="6c87e-271">Max value can be 10</span></span> |<span data-ttu-id="6c87e-272">0</span><span class="sxs-lookup"><span data-stu-id="6c87e-272">0</span></span> |<span data-ttu-id="6c87e-273">Número de tentativas antes do processamento de dados de saudação de fatia Olá é marcado como falha.</span><span class="sxs-lookup"><span data-stu-id="6c87e-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="6c87e-274">A execução da atividade para uma fatia de dados é repetida backup toohello especificado contagem de repetição.</span><span class="sxs-lookup"><span data-stu-id="6c87e-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="6c87e-275">repetição de saudação é feita logo após a falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="6c87e-276">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="6c87e-276">timeout</span></span> |<span data-ttu-id="6c87e-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6c87e-277">TimeSpan</span></span> |<span data-ttu-id="6c87e-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6c87e-278">00:00:00</span></span> |<span data-ttu-id="6c87e-279">Tempo limite para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-279">Timeout for hello activity.</span></span> <span data-ttu-id="6c87e-280">Exemplo: 00:10:00 (implica o tempo limite de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="6c87e-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="6c87e-281">Se um valor não for especificado ou for 0, o tempo limite de saudação é infinito.</span><span class="sxs-lookup"><span data-stu-id="6c87e-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="6c87e-282">Se o tempo de processamento de dados de saudação em uma fatia exceder o valor de tempo limite de Olá, é cancelada e sistema Olá tentativas de processamento de saudação tooretry.</span><span class="sxs-lookup"><span data-stu-id="6c87e-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="6c87e-283">o número de tentativas Olá depende da propriedade de repetição de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="6c87e-284">Quando o tempo limite ocorre, o status de saudação é definido tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="6c87e-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="6c87e-285">atrasar</span><span class="sxs-lookup"><span data-stu-id="6c87e-285">delay</span></span> |<span data-ttu-id="6c87e-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6c87e-286">TimeSpan</span></span> |<span data-ttu-id="6c87e-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6c87e-287">00:00:00</span></span> |<span data-ttu-id="6c87e-288">Especifique o intervalo de saudação antes do processamento de dados de saudação fatia começar.</span><span class="sxs-lookup"><span data-stu-id="6c87e-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="6c87e-289">execução de saudação da atividade de uma fatia de dados é iniciada depois Olá atraso é passado Olá esperado tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6c87e-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="6c87e-290">Exemplo: 00:10:00 (implica um atraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="6c87e-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="6c87e-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="6c87e-291">longRetry</span></span> |<span data-ttu-id="6c87e-292">Inteiro </span><span class="sxs-lookup"><span data-stu-id="6c87e-292">Integer</span></span><br/><br/><span data-ttu-id="6c87e-293">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="6c87e-293">Max value: 10</span></span> |<span data-ttu-id="6c87e-294">1</span><span class="sxs-lookup"><span data-stu-id="6c87e-294">1</span></span> |<span data-ttu-id="6c87e-295">número de saudação de repetição longa tentativas antes da execução da fatia Olá falhou.</span><span class="sxs-lookup"><span data-stu-id="6c87e-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="6c87e-296">Tentativas de longRetry são espaçadas por longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="6c87e-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="6c87e-297">Portanto, se você precisar toospecify um tempo entre tentativas de repetição, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="6c87e-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="6c87e-298">Se Retry e longRetry forem especificados, cada tentativa de longRetry inclui novas tentativas e Olá o número máximo de tentativas é repetir * longRetry.</span><span class="sxs-lookup"><span data-stu-id="6c87e-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="6c87e-299">Por exemplo, se tivermos Olá configurações na política de atividade Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c87e-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="6c87e-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="6c87e-300">Retry: 3</span></span><br/><span data-ttu-id="6c87e-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="6c87e-301">longRetry: 2</span></span><br/><span data-ttu-id="6c87e-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="6c87e-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="6c87e-303">Pressupomos que haja apenas um tooexecute de fatia (status está esperando) e a execução da atividade Olá falha sempre.</span><span class="sxs-lookup"><span data-stu-id="6c87e-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="6c87e-304">Inicialmente haveria três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="6c87e-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="6c87e-305">Após cada tentativa, o status da fatia Olá deve ser Retry.</span><span class="sxs-lookup"><span data-stu-id="6c87e-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="6c87e-306">Depois de tentativas primeiro 3 estão acima, o status da fatia Olá deve ser LongRetry.</span><span class="sxs-lookup"><span data-stu-id="6c87e-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="6c87e-307">Depois de uma hora (ou seja, valor de longRetryInteval), deve haver outro conjunto de três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="6c87e-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="6c87e-308">Depois disso, o status da fatia Olá deve ser Failed e nenhuma outra tentativa será feita.</span><span class="sxs-lookup"><span data-stu-id="6c87e-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="6c87e-309">Portanto, em geral, foram feitas seis tentativas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="6c87e-310">Se qualquer execução for bem-sucedida, o status da fatia Olá seria pronto e não tentativa de nenhuma outra tentativa.</span><span class="sxs-lookup"><span data-stu-id="6c87e-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="6c87e-311">longRetry pode ser usado em situações em que dados dependentes chegam em momentos não determinística ou hello ambiente geral é instável em ocorre o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="6c87e-312">Nesses casos, não pode ajudar a fazer tentativas após o outro e fazer isso após um intervalo de resultados de tempo de saudação desejado de saída.</span><span class="sxs-lookup"><span data-stu-id="6c87e-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="6c87e-313">Advertência: não defina valores altos para longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="6c87e-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="6c87e-314">Normalmente, os valores mais altos implicam outros problemas sistêmicos.</span><span class="sxs-lookup"><span data-stu-id="6c87e-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="6c87e-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="6c87e-315">longRetryInterval</span></span> |<span data-ttu-id="6c87e-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6c87e-316">TimeSpan</span></span> |<span data-ttu-id="6c87e-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6c87e-317">00:00:00</span></span> |<span data-ttu-id="6c87e-318">atraso de saudação entre as tentativas de repetição longa</span><span class="sxs-lookup"><span data-stu-id="6c87e-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="6c87e-319">Para obter mais informações, consulte o artigo [Pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6c87e-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="6c87e-320">Processamento paralelo de fatias de dados</span><span class="sxs-lookup"><span data-stu-id="6c87e-320">Parallel processing of data slices</span></span>
<span data-ttu-id="6c87e-321">Você pode definir data de início de saudação do pipeline de saudação no hello anterior.</span><span class="sxs-lookup"><span data-stu-id="6c87e-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="6c87e-322">Quando você fizer isso, fábrica de dados calcula (back preenchimentos) todas as fatias de dados em Olá anterior e começa a processá-las automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6c87e-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="6c87e-323">Por exemplo: se você criar um pipeline com data de início de 2017-04-01 e Olá a data atual for 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="6c87e-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="6c87e-324">Se cadência de saudação do hello saída de conjunto de dados é diariamente, em seguida, começa a fábrica de dados processar todas as fatias de saudação do 2017-04-01 too2017-04-09 imediatamente porque Olá data de início está no hello anterior.</span><span class="sxs-lookup"><span data-stu-id="6c87e-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="6c87e-325">Olá fatia de 2017-04-10 não é processada ainda porque Olá o valor da propriedade de estilo na seção de disponibilidade de saudação é EndOfInterval por padrão.</span><span class="sxs-lookup"><span data-stu-id="6c87e-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="6c87e-326">Hello mais antiga fatia é processada primeiro como padrão Olá valor executionPriorityOrder é OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="6c87e-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="6c87e-327">Para obter uma descrição da propriedade de estilo hello, consulte [conjunto de dados disponibilidade](#dataset-availability) seção.</span><span class="sxs-lookup"><span data-stu-id="6c87e-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="6c87e-328">Para obter uma descrição da seção de executionPriorityOrder hello, consulte Olá [políticas de atividade](#activity-policies) seção.</span><span class="sxs-lookup"><span data-stu-id="6c87e-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="6c87e-329">Você pode configurar toobe fatias de dados de back-preenchido processado em paralelo por configuração Olá **simultaneidade** propriedade Olá **política** seção de atividade Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="6c87e-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="6c87e-330">Essa propriedade determina o número de saudação de execuções de atividade paralela que pode ocorrer em intervalos diferentes.</span><span class="sxs-lookup"><span data-stu-id="6c87e-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="6c87e-331">saudação padrão valor para a propriedade de simultaneidade Olá é 1.</span><span class="sxs-lookup"><span data-stu-id="6c87e-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="6c87e-332">Portanto, uma única fatia é processada por vez, por padrão.</span><span class="sxs-lookup"><span data-stu-id="6c87e-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="6c87e-333">valor máximo de saudação é 10.</span><span class="sxs-lookup"><span data-stu-id="6c87e-333">hello maximum value is 10.</span></span> <span data-ttu-id="6c87e-334">Quando precisa de um pipeline toogo por meio de um grande conjunto de dados disponíveis, ter um valor maior da simultaneidade acelera o processamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="6c87e-335">Executar novamente uma fatia de dados com falha</span><span class="sxs-lookup"><span data-stu-id="6c87e-335">Rerun a failed data slice</span></span>
<span data-ttu-id="6c87e-336">Quando ocorre um erro durante o processamento de uma fatia de dados, você pode descobrir por que falha no processamento da saudação de uma fatia usando folhas de portal do Azure ou monitorar e gerenciar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6c87e-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="6c87e-337">Confira [Monitorar e gerenciar pipelines usando folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) ou [aplicativo de monitoramento e gerenciamento](data-factory-monitor-manage-app.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6c87e-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="6c87e-338">Considere Olá exemplo, que mostra duas atividades a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c87e-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="6c87e-339">Activity1 e Activity2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="6c87e-340">Atividade1 consome uma fatia de Dataset1 e produz uma fatia de Dataset2, que é utilizada como entrada pelo atividade2 tooproduce uma fatia da saudação Final do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Fatia com falha](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="6c87e-342">Olá diagrama mostra que fora três fatias recentes, houve uma fatia de 9 de 10 AM falha produção Olá para Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="6c87e-343">Fábrica de dados controla automaticamente a dependência de conjunto de dados de série de tempo hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="6c87e-344">Como resultado, ele não for iniciado atividade Olá executar fatia downstream do hello AM 9-10.</span><span class="sxs-lookup"><span data-stu-id="6c87e-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="6c87e-345">Ferramentas de monitoramento e gerenciamento da fábrica de dados permitem toodrill em logs de diagnóstico Olá para a raiz de Olá Olá fatia com falha tooeasily localizar causar problema hello e corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="6c87e-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="6c87e-346">Depois de corrigir o problema de saudação, você pode iniciar facilmente tooproduce Olá falha fatia de execução da atividade hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="6c87e-347">Para obter mais informações sobre como toorerun e entender as transições de estado para fatias de dados, consulte [monitoramento e gerenciamento de pipelines usando folhas de portal do Azure](data-factory-monitor-manage-pipelines.md) ou [monitoramento e gerenciamento de aplicativo](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c87e-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="6c87e-348">Depois de você executar novamente Olá 9 10 AM fatiar para **Dataset2**, Data Factory inicia Olá executar fatia dependentes de 9 de 10 AM Olá no conjunto de dados final hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Executar novamente uma fatia com falha](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="6c87e-350">Várias atividades em um pipeline</span><span class="sxs-lookup"><span data-stu-id="6c87e-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="6c87e-351">Você pode ter mais de uma atividade em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="6c87e-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="6c87e-352">Se você tiver várias atividades em um pipeline e saída de saudação de uma atividade não é uma entrada de outra atividade, atividades Olá podem executados em paralelo, se as fatias de dados de entrada para atividades de saudação estão prontas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="6c87e-353">É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="6c87e-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="6c87e-354">Olá atividades podem ser em Olá mesmo pipeline ou em pipelines diferentes.</span><span class="sxs-lookup"><span data-stu-id="6c87e-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="6c87e-355">atividade de segundo Olá executa somente quando hello primeiro um concluir com êxito.</span><span class="sxs-lookup"><span data-stu-id="6c87e-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="6c87e-356">Por exemplo, considere hello quando um pipeline tem duas atividades a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c87e-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="6c87e-357">A Atividade A1, que exige o conjunto de dados de entrada externo D1 e produz o conjunto de dados de saída D2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="6c87e-358">A Atividade A2, que exige a entrada do conjunto de dados D2 e produz o conjunto de dados de saída D3.</span><span class="sxs-lookup"><span data-stu-id="6c87e-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="6c87e-359">Nesse cenário, as atividades A1 e A2 são em Olá mesmo pipeline.</span><span class="sxs-lookup"><span data-stu-id="6c87e-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="6c87e-360">atividade de saudação que a1 é executado quando dados externos hello estão disponíveis e Olá agendado disponibilidade frequência é atingida.</span><span class="sxs-lookup"><span data-stu-id="6c87e-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="6c87e-361">Hello atividade A2 é executado quando hello agendadas fatias de D2 fiquem disponíveis e hello frequência disponibilidade agendada for atingida.</span><span class="sxs-lookup"><span data-stu-id="6c87e-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="6c87e-362">Se houver um erro em uma das fatias Olá no conjunto de dados D2, A2 não execute essa fatia até ela ficar disponível.</span><span class="sxs-lookup"><span data-stu-id="6c87e-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="6c87e-363">Olá o modo de exibição de diagrama com ambas as atividades no hello mesmo pipeline seria semelhante a saudação diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c87e-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Encadeamento de atividades no hello mesmo pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="6c87e-365">Como mencionado anteriormente, as atividades de saudação podem estar em pipelines diferentes.</span><span class="sxs-lookup"><span data-stu-id="6c87e-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="6c87e-366">Nesse cenário, o modo de exibição de diagrama de saudação seria Olá diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="6c87e-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Encadeando atividades em dois pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="6c87e-368">Consulte Olá [copiar sequencialmente](#copy-sequentially) seção apêndice Olá para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="6c87e-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="6c87e-369">Modelar conjuntos de dados com frequências diferentes</span><span class="sxs-lookup"><span data-stu-id="6c87e-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="6c87e-370">Exemplos de saudação as frequências de saudação de entrada e saída conjuntos de dados e hello atividade janela de agendamento foram Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="6c87e-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="6c87e-371">Alguns cenários exigem a saída de tooproduce hello capacidade em uma frequência diferente de frequências de saudação de uma ou mais entradas.</span><span class="sxs-lookup"><span data-stu-id="6c87e-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="6c87e-372">O Data Factory dá suporte à modelagem desses cenários.</span><span class="sxs-lookup"><span data-stu-id="6c87e-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="6c87e-373">Exemplo 1: gerar um relatório diário de saída para dados de entrada que estão disponíveis de hora em hora</span><span class="sxs-lookup"><span data-stu-id="6c87e-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="6c87e-374">Considere um cenário em que temos dados de medição de entrada de sensores disponíveis a cada hora no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c87e-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="6c87e-375">Você deseja tooproduce um relatório diário de agregação com estatísticas, como média, máximo e mínimo para o dia de saudação com [atividade de hive de fábrica de dados](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="6c87e-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="6c87e-376">Veja como você pode modelar esse cenário com o Data Factory:</span><span class="sxs-lookup"><span data-stu-id="6c87e-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="6c87e-377">**Conjunto de dados de entrada**</span><span class="sxs-lookup"><span data-stu-id="6c87e-377">**Input dataset**</span></span>

<span data-ttu-id="6c87e-378">Olá por hora de entrada arquivos são instalados na pasta Olá Olá dado dia.</span><span class="sxs-lookup"><span data-stu-id="6c87e-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="6c87e-379">A disponibilidade de entrada é definida por **Hora** (frequência: Hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6c87e-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="6c87e-380">**Conjunto de dados de saída**</span><span class="sxs-lookup"><span data-stu-id="6c87e-380">**Output dataset**</span></span>

<span data-ttu-id="6c87e-381">Um arquivo de saída é criado diariamente na pasta de saudação do dia.</span><span class="sxs-lookup"><span data-stu-id="6c87e-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="6c87e-382">A disponibilidade de saída é definida em **Dia** (frequência: Dia e intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6c87e-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="6c87e-383">**Atividade: atividade de hive em um pipeline**</span><span class="sxs-lookup"><span data-stu-id="6c87e-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="6c87e-384">script do hive Olá recebe Olá apropriado *DateTime* informações como parâmetros que usam Olá **WindowStart** , conforme mostrado no hello trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c87e-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="6c87e-385">script do hive Olá usa dados Olá tooload variável da pasta correta Olá dia hello e Olá agregação toogenerate Olá saída.</span><span class="sxs-lookup"><span data-stu-id="6c87e-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

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

<span data-ttu-id="6c87e-386">Olá diagrama a seguir mostra o cenário de saudação de um ponto de vista da dependência de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Dependência de dados](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="6c87e-388">Olá fatia de saída para cada dia depende 24 fatias por hora de um conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="6c87e-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="6c87e-389">Calcula a fábrica dados essas dependências automaticamente descobrindo-Olá fatias de dados de entrada que se enquadram em Olá mesmo período de tempo como Olá toobe de fatias de saída produzido.</span><span class="sxs-lookup"><span data-stu-id="6c87e-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="6c87e-390">Se qualquer uma das fatias de entrada hello 24 não estiver disponível, fábrica de dados aguarda Olá fatia entrada toobe pronto antes de iniciar a execução da atividade diária hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="6c87e-391">Exemplo 2: especificar dependência com expressões e funções do Data Factory</span><span class="sxs-lookup"><span data-stu-id="6c87e-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="6c87e-392">Vamos considerar outro cenário.</span><span class="sxs-lookup"><span data-stu-id="6c87e-392">Let’s consider another scenario.</span></span> <span data-ttu-id="6c87e-393">Suponha que você tenha uma atividade de hive que processa dois conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="6c87e-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="6c87e-394">Um deles tem novos dados diariamente, mas o outro obtém novos dados toda semana.</span><span class="sxs-lookup"><span data-stu-id="6c87e-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="6c87e-395">Suponha que você desejava toodo uma junção entre duas entradas de saudação e produzir uma saída de cada dia.</span><span class="sxs-lookup"><span data-stu-id="6c87e-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="6c87e-396">abordagem simples Hello, no qual fábrica de dados automaticamente descobre entrada direita Olá fatias tooprocess alinhando saída toohello tempo da fatia de dados do período não funciona.</span><span class="sxs-lookup"><span data-stu-id="6c87e-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="6c87e-397">Você deve especificar que para cada execução da atividade, Olá Data Factory deve usar a fatia de dados da semana passada Olá semanal entrada conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="6c87e-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="6c87e-398">Você usar funções do Azure Data Factory conforme mostrado no hello tooimplement de trecho de código a seguir esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="6c87e-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="6c87e-399">**Saída1: blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="6c87e-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="6c87e-400">Olá primeiro entrada hello BLOBs do Azure está sendo atualizado diariamente.</span><span class="sxs-lookup"><span data-stu-id="6c87e-400">hello first input is hello Azure blob being updated daily.</span></span>

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

<span data-ttu-id="6c87e-401">**Entrada2: blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="6c87e-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="6c87e-402">Entrada2 é hello BLOBs do Azure que está sendo atualizada semanalmente.</span><span class="sxs-lookup"><span data-stu-id="6c87e-402">Input2 is hello Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="6c87e-403">**Saída: blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="6c87e-403">**Output: Azure blob**</span></span>

<span data-ttu-id="6c87e-404">Um arquivo de saída é criado diariamente na pasta de saudação do dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c87e-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="6c87e-405">Conjunto de disponibilidade de saída é muito**dia** (frequência: Day, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6c87e-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="6c87e-406">**Atividade: atividade de hive em um pipeline**</span><span class="sxs-lookup"><span data-stu-id="6c87e-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="6c87e-407">atividade de hive Olá usa Olá duas entradas e produz uma fatia de saída todos os dias.</span><span class="sxs-lookup"><span data-stu-id="6c87e-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="6c87e-408">Você pode especificar toodepend de fatia de saída de cada dia em Olá fatia de entrada da semana anterior para a entrada semanal da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="6c87e-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="6c87e-409">Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis às quais o Azure Data Factory dá suporte.</span><span class="sxs-lookup"><span data-stu-id="6c87e-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="6c87e-410">Apêndice</span><span class="sxs-lookup"><span data-stu-id="6c87e-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="6c87e-411">Exemplo: copiar sequencialmente</span><span class="sxs-lookup"><span data-stu-id="6c87e-411">Example: copy sequentially</span></span>
<span data-ttu-id="6c87e-412">Ele é possível toorun várias operações de cópia após o outro de forma ordenada/sequencial.</span><span class="sxs-lookup"><span data-stu-id="6c87e-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="6c87e-413">Por exemplo, você pode ter dois conjuntos de saída cópia atividades em um pipeline (CopyActivity1 e CopyActivity2) com hello após entradas dados:</span><span class="sxs-lookup"><span data-stu-id="6c87e-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="6c87e-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="6c87e-414">CopyActivity1</span></span>

<span data-ttu-id="6c87e-415">Entrada: Dataset.</span><span class="sxs-lookup"><span data-stu-id="6c87e-415">Input: Dataset.</span></span> <span data-ttu-id="6c87e-416">Saída: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-416">Output: Dataset2.</span></span>

<span data-ttu-id="6c87e-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="6c87e-417">CopyActivity2</span></span>

<span data-ttu-id="6c87e-418">Entrada: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-418">Input: Dataset2.</span></span>  <span data-ttu-id="6c87e-419">Saída: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="6c87e-419">Output: Dataset3.</span></span>

<span data-ttu-id="6c87e-420">CopyActivity2 será executado somente se Olá CopyActivity1 foi executada com êxito e Dataset2 está disponível.</span><span class="sxs-lookup"><span data-stu-id="6c87e-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="6c87e-421">Aqui está o JSON de pipeline de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="6c87e-421">Here is hello sample pipeline JSON:</span></span>

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

<span data-ttu-id="6c87e-422">Observe que, no exemplo hello, conjunto de dados de saída de saudação do hello primeira atividade de cópia (Dataset2) é especificado como entrada para a atividade de segundo hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="6c87e-423">Portanto, Olá segunda atividade executa somente quando Olá o conjunto de dados de saída da atividade primeiro hello está pronto.</span><span class="sxs-lookup"><span data-stu-id="6c87e-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="6c87e-424">No exemplo hello, CopyActivity2 pode ter uma entrada diferente, como Dataset3, mas você especificar Dataset2 como uma entrada tooCopyActivity2, para que atividade de saudação não será executado até CopyActivity1 termina.</span><span class="sxs-lookup"><span data-stu-id="6c87e-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="6c87e-425">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6c87e-425">For example:</span></span>

<span data-ttu-id="6c87e-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="6c87e-426">CopyActivity1</span></span>

<span data-ttu-id="6c87e-427">Entrada: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="6c87e-427">Input: Dataset1.</span></span> <span data-ttu-id="6c87e-428">Saída: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-428">Output: Dataset2.</span></span>

<span data-ttu-id="6c87e-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="6c87e-429">CopyActivity2</span></span>

<span data-ttu-id="6c87e-430">Entradas: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="6c87e-431">Saída: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="6c87e-431">Output: Dataset4.</span></span>

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

<span data-ttu-id="6c87e-432">Observe que no exemplo hello, dois conjuntos de dados de entrada são especificados para a segunda atividade de cópia hello.</span><span class="sxs-lookup"><span data-stu-id="6c87e-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="6c87e-433">Quando várias entradas forem especificadas, somente Olá primeira entrada dataset é usado para copiar dados, mas outros conjuntos de dados são usados como as dependências.</span><span class="sxs-lookup"><span data-stu-id="6c87e-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="6c87e-434">CopyActivity2 será iniciada somente depois hello seguintes condições forem atendidas:</span><span class="sxs-lookup"><span data-stu-id="6c87e-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="6c87e-435">CopyActivity1 foi concluído com êxito e Dataset2 está disponível.</span><span class="sxs-lookup"><span data-stu-id="6c87e-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="6c87e-436">Este conjunto de dados não é usado ao copiar dados tooDataset4.</span><span class="sxs-lookup"><span data-stu-id="6c87e-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="6c87e-437">Ele atua apenas como uma dependência de agendamento de CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="6c87e-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="6c87e-438">Dataset3 está disponível.</span><span class="sxs-lookup"><span data-stu-id="6c87e-438">Dataset3 is available.</span></span> <span data-ttu-id="6c87e-439">Este conjunto de dados representa dados de saudação toohello copiado de destino.</span><span class="sxs-lookup"><span data-stu-id="6c87e-439">This dataset represents hello data that is copied toohello destination.</span></span> 
